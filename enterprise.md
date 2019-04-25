---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-25"

keywords: authentication, authorization, identity, app security, secure, custom, service provider, identity provider, enterprise, assertions

subcollection: appid

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}

# SAML
{: #enterprise}

When you have a SAML-based identity provider, you can configure {{site.data.keyword.appid_short_notm}} to act as a service provider that initiates a single sign-on (SSO) log in to a third-party provider. During the sign in flow, your users can be easily authenticated and are able obtain {{site.data.keyword.appid_short_notm}} security tokens that allow them to access your apps and protected APIs.
{: shortdesc}

 
Working with a specific SAML identity provider? Check out one of these blog posts on setting up {{site.data.keyword.appid_short_notm}} with [Ping One ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-ping-one/), [an Azure Active Directory ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-azure-active-directory/), or [an Active Directory Federation Service ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-active-directory-federation-service/).
{: tip}


## Understanding SAML
{: #saml-understanding}

Security Assertion Markup Language (SAML) is an open standard for exchanging authentication and authorization data between an identity provider who asserts the user identity and a service provider who consumes the user identity information.
{: shortdesc}

The <a href="http://saml.xml.org/saml-specifications" target="blank">SAML <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> protocol supports different profiles and bind options. {{site.data.keyword.appid_short_notm}}supports the web browser SSO profile, with HTTP Post binding.

### What's the flows technical basis?
{: #saml-tech-basis}

SAML 2.0 is one of the most established frameworks for authentication and authorization standards. It is an XML-based protocol between a service provider ({{site.data.keyword.appid_short_notm}}) and an identity provider. When an identity provider authenticates a user, it creates SAML tokens, which contain assertions, or statements, about the user. The statements might contain:

- authentication information like how the user was authenticated - a password, MFA, etc ...
- attributes associated with the user - which group they belong in.
- authorization decisions which state whether the user is allowed to perform a particular action on a particular resource.

When the assertions are returned to {{site.data.keyword.appid_short_notm}}, the service federates the user identity and the appropriate tokens are generated. If the SAML assertion corresponds to one of the following OIDC claims, it is automatically added to the identity token.  If one or more of those values change on the provider's side, the new values are available only after the user logs in again.

 * `name`
 * `email`
 * `locale`
 * `picture`

The assertions that do not correspond to any of the standard names are ignored by default, but if your SAML provider returns other assertions, it is possible to obtain the information when a user logs in. By creating an array of the assertions that you want to use, you can [inject the information into your tokens](/docs/services/appid?topic=appid-customizing-tokens#customizing-tokens). But, be sure not to add more information than necessary to your tokens. Tokens are usually sent in http headers and headers are limited in size.
{: tip}

### What does the flow look like?
{: #saml-flow}

Although {{site.data.keyword.appid_short_notm}} and your identity provider use the SAML framework to authenticate the user, {{site.data.keyword.appid_short_notm}} still uses the more modern OAuth 2.0/ OIDC framework to exchange security tokens with the application. Check out the following image to see a detailed flow of information.

![SAML enterprise authentication flow](/images/ibmid-flow.png)

1. A user access the login page or restricted resource on their application, which initiates a request to the {{site.data.keyword.appid_short_notm}} `/authorization` endpoint through either an {{site.data.keyword.appid_short_notm}} SDK or API. If the user is unauthorized, the authentication flow begins with a redirect to {{site.data.keyword.appid_short_notm}}.
2. {{site.data.keyword.appid_short_notm}} generates a SAML authentication request (AuthNRequest) and the browser automatically redirects the user to the SAML identity provider.
3. The identity provider parses the SAML request, authenticates the user, and generates a SAML response with its assertions.
4. The identity provider redirects the user and the response back to {{site.data.keyword.appid_short_notm}} with the SAML response.
5. If the authentication is successful, {{site.data.keyword.appid_short_notm}} creates access and identity tokens that represent a user's authorization and authentication and returns them to the app. If the authentication fails, {{site.data.keyword.appid_short_notm}} returns the identity provider error code to the app.
6. The user is granted access to the app or the protected resources.



### Does SSO change the flow?
{: #saml-sso-flow}

The web browser SSO profile that {{site.data.keyword.appid_short_notm}} implements is service provider initiated, which means that {{site.data.keyword.appid_short_notm}} must send a SAML request to the identity provider to initiate the authentication session. 

{{site.data.keyword.appid_short_notm}} does not currently support identity provider initiated flows and they should not be used with the service at this time.
{: note}

If your identity provider supports SSO, then it is possible that the SAML authentication uses the already established SSO session to authenticate the user. If it does not, the user is redirected to a login page. They might be redirected if your identity provider can't match the authentication requirements that are defined in {{site.data.keyword.cloud_notm}}'s authentication request with what it uses to establish SSO. For example, if your identity provider establishes a user SSO session by using biometrics, then {{site.data.keyword.appid_short_notm}}'s default authentication context must be changed. By default, {{site.data.keyword.appid_short_notm}} expects users to be authenticated by password over HTTPS: `urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport`.



## Configuring SAML to work with {{site.data.keyword.appid_short_notm}}
{: #saml-configure}

You can configure SAML to work with {{site.data.keyword.appid_short_notm}} by providing metadata from {{site.data.keyword.appid_short_notm}} to your identity provider and metadata from your identity provider to {{site.data.keyword.appid_short_notm}}.



### Providing metadata to your identity provider
{: #saml-provide-idp}

To configure your app, you need to provide information to a SAML compatible identity provider. The information is exchanged through a metadata XML file that also contains configuration data that is used to establish trust.
{: shortdesc}

You cannot enable SAML until after you have configured it as an identity provider.
{: tip}

1. In the **Manage** tab of the {{site.data.keyword.appid_short_notm}} dashboard, click **Edit** in the **SAML** row to configure your settings.
2. Click **Download SAML Metadata file**. Your identity provider expects the following information from the file.
  <table>
    <tr>
      <th> Variable </th>
      <th> Description </th>
    </tr>
    <tr>
      <td><code>EntityID</code></td>
      <td>The identifier that lets the identity provider know that {{site.data.keyword.appid_short_notm}} has issued the SAML request.</td>
    </tr>
    <tr>
      <td><code>Location URL</code></td>
      <td>The location that the identity provider sends the SAML assertions after successfully authenticating a user.</td>
    </tr>
    <tr>
      <td><code>Binding</code></td>
      <td>The instructions on how the identity provider should send the SAML response.</td>
    </tr>
    <tr>
      <td><code>NameID Format</code></td>
      <td>The way in which the identity provider knows which identifier format it needs to send in the subject of an assertion. The way in which {{site.data.keyword.appid_short_notm}} identifies users.</td>
    </tr>
    <tr>
      <td><code>WantAssertionsSigned</code></td>
      <td>The way that an identity provider checks to see if it needs to sign the assertion. The service expects that the assertion is signed, but does not support encrypted assertions.</td>
    </tr>
  </table>

3. Provide the data to your identity provider. If your identity provider supports uploading the metadata file, you can do so. If it doesn't, configure the properties manually. Not every identity provider uses the same properties, so you might not use all of them.

  The property names might differ between identity providers.
  {: tip}

4. Toggle **SAML 2.0 Federation** to **Enabled**.



### Providing metadata to {{site.data.keyword.appid_short_notm}}
{: #saml-provide-appid}

You can obtain data from your identity provider and provide it to {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

**Providing metadata with the GUI** 

1. Navigate to the **SAML 2.0** tab of the {{site.data.keyword.appid_short_notm}} dashboard. Enter the following metadata that you obtained from the identity provider in the **Provide Metadata from SAML IdP** section.
  <table>
    <tr>
      <th> Variable </th>
      <th> Description </th>
    </tr>
    <tr>
      <td><code>Sign-in URL</code></td>
      <td>The URL that the user is redirected to for authentication. It is hosted by your SAML identity provider.</td>
    </tr>
    <tr>
      <td><code>Entity ID</code></td>
      <td>The globally unique name for a SAML identity provider.</td>
    </tr>
    <tr>
      <td><code>Signing certificate</code></td>
      <td>The certificate issued by your SAML identity provider. It is used for signing and validating SAML assertions. All providers are different, but you might be able to download the signing certificate from your identity provider. The certificate must be in <code>.pem</code> format.</td>
    </tr>
  </table>

2. Optional: Provide a **Secondary certificate** that is used if signature validation fails on the primary certificate. If the signing key remains the same, {{site.data.keyword.appid_short_notm}} does not block authentication for expired certificates.
3. Update the **Provider Name**, and click **Save**. The default name is SAML.

Want to set an authentication context? You can do so through the API.
{: tip}

</br>

**Providing metadata with the API**

1. View your current SAML configuration with App ID including your authentication context and certificates, make a GET request to the  [`/saml` API endpoint](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.get_saml_idp).

  Example code:
  ```
  curl --request GET \
  https://us-south.appid.cloud.ibm.com/management/v4/<tenant-ID>/config/idps/saml \
  --header `Accept: application/json`
  ```
  {: pre}

  Example output:
  ```
  {
    "isActive": true,
    "config": {
      "entityID": "https://example.com/saml2/metadata/706634",
      "signInUrl": "https://example.com/saml2/sso-redirect/706634",
      "certificates": [
        "certificate-example-pem-format"
      ],
      "displayName": "my saml example",
      "authnContext": {
        "class": [
          "urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport"
        ],
        "comparison": "exact"
      }
    }
  }
  ```
  {: screen}

2. Create your SAML configuration by replacing the values in the following example with the information from your provider. The values shown in the example are required, but you can choose to include more information as shown in the table.

  ```
  "config": {
    "authnContext": {
      "class": [
        "urn:oasis:names:tc:SAML:2.0:ac:classes:YourChosenClassValue",
        "urn:oasis:names:tc:SAML:2.0:ac:classes:YourOtherChosenClassValue"
      ],
      "comparison": "sampleComparisonValue"}
    "entityID": "https://example.com/saml2/metadata/706634",
    "signInUrl": "https://example.com/saml2/sso-redirect/706634",
    "certificates": [
      "primary-certificate-example-pem-format"
      "secondary-certificate-example-pem-format"
    ],
    "displayName": "my saml example",
  }
  ```
  {: pre}
  {: #configuring-saml-new}

  <table>
    <tr>
      <th> Variable </th>
      <th> Description </th>
    </tr>
    <tr>
      <td><code>signInUrl</code></td>
      <td>The URL that the user is redirected to for authentication. It is hosted by your SAML identity provider.</td>
    </tr>
    <tr>
      <td><code>entityID</code></td>
      <td>The globally unique name for a SAML identity provider.</td>
    </tr>
    <tr>
      <td><code>displayName</code></td>
      <td>The name that you assign to your SAML configuration.</td>
    </tr>
    <tr>
      <td><code>primary-certificate-example-pem-format</code></td>
      <td>The certificate that is issued by your SAML identity provider. It is used for signing and validating SAML assertions. All providers are different, but you might be able to download the signing certificate from your identity provider. The certificate must be in <code>.pem</code> format.</td>
    </tr>
    <tr>
      <td>Optional: <code>secondary-certificate-example-pem-format</code></td>
      <td>The back up certificate that is issued by your SAML identity provider. It is used if signature validation fails with the primary certificate. <strong>Note</strong>: If the signing key remains the same, {{site.data.keyword.appid_short_notm}} does not block authentication for expired certificates.</td>
    </tr>
    <tr>
      <td>Optional: <code>authnContext</code></td>
      <td>The authentication context is used to verify the quality of the authentication and SAML assertions. You can add an authentication context by adding a class array and comparison string to your code. BE sure to update both the <code>class</code> and <code>comparison</code> parameters with your values. For example, a <code>class</code> parameter might look similar to <code>urn:oasis:names:tc:SAML:2.0:ac:classes:YourChosenClassValue</code>.</td>
    </tr>
  </table>

3. Make a PUT request to the [`/saml` API endpoint](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp) to provide the configuration that you created in step 2 to {{site.data.keyword.appid_short_notm}}. Check out the following example to see what your request might look like.

  ```
  curl --request PUT \
  https://us-south.appid.cloud.ibm.com/management/v4/<tenant-ID>/config/idps/saml \
  --header `Accept: application/json` \
  --data \
  {
    "isActive": true,
    "config": {
      "entityID": "https://example.com/saml2/metadata/706634",
      "signInUrl": "https://example.com/saml2/sso-redirect/706634",
      "certificates": [
        "primary-certificate-example-pem-format"
      ],
      "displayName": "my saml example",
    }
  }
  ```
  {: screen}



## Testing your configuration
{: #saml-testing}

You can test the configuration between your SAML Identity Provider and {{site.data.keyword.appid_short_notm}}.

1. Be sure that you've saved your configuration.
2. Navigate to the **SAML 2.0** tab of the {{site.data.keyword.appid_short_notm}} dashboard and click **Test**. A new tab opens.
3. Login in with a user that your identity provider has already authenticated.
4. After you complete the form, you are redirected to another page.
  * Successful authentication: The connection between {{site.data.keyword.appid_short_notm}} and the Identity Provider is working correctly. The page displays valid [access and identity tokens](/docs/services/appid?topic=appid-tokens#tokens).
  * Failed authentication: The connection is broken. The page displays the errors and the SAML response XML file.


Having trouble? Check out [Troubleshooting: SAML](/docs/services/appid?topic=appid-troubleshooting-idp#troubleshooting-idp).
{: tip}




## SAML FAQ
{: #saml-assertions}

SAML assertions can be returned in different ways. Check out the following examples to see the way in which {{site.data.keyword.appid_short_notm}} expects the response to be formatted.
{: shortdesc}


### What does {{site.data.keyword.appid_short_notm}} expect a SAML assertion to look like?
{: #saml-example}

The service expects a SAML assertion to look like the following example.

```
<samlp:Response xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol" ID="s2202bbbbafa9d270d1c15990b738f4ab36139d463" InResponseTo="_e4a78780-35da-012e-8ea7-0050569200d8" Version="2.0" IssueInstant="2011-03-21T11:22:02Z" Destination="https://example.example.com/">
  <saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">idp_entityId</saml:Issuer>
  <samlp:Status xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <samlp:StatusCode  xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol"Value="urn:oasis:names:tc:SAML:2.0:status:Success"/>
  </samlp:Status>
  <saml:Assertion xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="2.0" ID="pfx539c9774-de5c-5f52-0c3f-b1c2e2697a89" IssueInstant="2018-01-29T13:02:58Z" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <saml:Issuer>idp_entityId</saml:Issuer>
    <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      <ds:SignedInfo>
        <ds:CanonicalizationMethod Algorithm="one_of_supported_algo"/>
        <ds:SignatureMethod Algorithm="one_of_supported_algo"/>
        <ds:Reference URI="#pfx539c9774-de5c-5f52-0c3f-b1c2e2697a89">
          <ds:Transforms>
            <ds:Transform Algorithm="one_of_supported_algo"/>
            <ds:Transform Algorithm="one_of_supported_algo"/>
          </ds:Transforms>
          <ds:DigestMethod Algorithm="one_of_supported_algo"/>
          <ds:DigestValue>huywDPPfOEGyyzE7d5hjOG97p7FDdGrjoSfes6RB19g=</ds:DigestValue>
        </ds:Reference>
      </ds:SignedInfo>
 <ds:SignatureValue>BAwNZFgWF2oxD1ux0WPfeHnzL+IWYqGhkM9DD28nI9v8XtPN8tqmIb5y4bomaYknmNpWYn7TgNO2Rn/XOq+N9fTZXO2RybaC49iF+zWibRIcNwFKCCpDL6H6jA5eqJX2YKBR+K6Yt2JPoUIRLmqdgm2lMr4Nwq1KYcSzQ/yoV5W0SN/V5t8EfctFoaXVPdtfHVXkwqHeufo+L4gobFt9NRTzXB0SQEClA1L8hQ+/LhY4l46k1D0c34iWjVLZr+ecQyubf7rekOG/R7DjWCFMTke822dR+eJTPWFsHGSPWCDDHFYqB4QMinTvUnsngjY3AssPqIOjeUxjL3p+GXn8IQ==</ds:SignatureValue>
    </ds:Signature>
    <saml:Subject>
      <saml:NameID Format="urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress">JohnDoe@gmail.com</saml:NameID>
    </saml:Subject>
    <saml:Conditions NotBefore="2018-01-29T12:59:58Z" NotOnOrAfter="2018-01-29T13:05:58Z">
    </saml:Conditions>
</samlp:Response>
```
{: screen}


### What types of algorithms are supported by {{site.data.keyword.appid_short_notm}}?
{: #saml-signatures}

{{site.data.keyword.appid_short_notm}} uses the <a href="http://www.w3.org/2001/04/xmldsig-more#rsa-sha256" target="_blank">RSA-SHA256 <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> algorithm to process XML digital signatures.

