---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}

# SAML
{: #enterprise}

Security Assertion Markup Language (SAML) is an open standard for exchanging authentication and authorization data between an identity provider who asserts the user identity and a service provider who consumes the user identity information.
{: shortdesc}

{{site.data.keyword.appid_short_notm}} functions as a service provider and initiates a single sign-on (SSO) login to a third-party provider such as Active Directory Federation Services. The <a href="http://saml.xml.org/saml-specifications" target="blank">SAML <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> protocol supports different profiles and bind options. {{site.data.keyword.appid_short_notm}} supports the web browser SSO profile, with HTTP Post binding.

For steps on how to use a specific SAML identity provider, check out these blog posts on setting up {{site.data.keyword.appid_short_notm}} with [Ping One ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-ping-one/), [an Azure Active Directory ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-azure-active-directory/), or [an Active Directory Federation Service ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-active-directory-federation-service/).
{: tip}


## Understanding assertions
{: #saml-assertions}

A SAML assertion is a statement or piece of information about a user, that is returned to App ID by an identity provider. Depending on your app configuration and the identity provider that you use, the information might include a users name, email, or another field that you ask to be returned. In addition to personal information, the assertion response also contains the authorization decision for the user. 

1. A user successfully signs into your application by using an identity provider.
2. The provider returns assertions to App ID.
3. App ID pr

When a user successfully signs into your application by using an identity provider, that provider sends the assertions 


 When a user signs in with an identity provider, that provider sends an assertion to {{site.data.keyword.appid_short_notm}}. {{site.data.keyword.appid_short_notm}} propagates user identity information that is returned in the SAML assertion to your app as OIDC token claims.

If the SAML assertion corresponds to one of the following OIDC claims, it is automatically added to the identity token. The assertions that do not correspond to any of the standard names are ignored.

 * `name`
 * `email`
 * `locale`
 * `picture`

If one or more of those values change on the provider's side, the new values are available only after the user logs in again.
{: note}




## What does {{site.data.keyword.appid_short_notm}} expect a SAML assertion to look like?
{: #faq-saml-example}
{: faq}

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


## What type of algorithms are supported for SAML signatures
{: #faq-saml-signatures}
{: faq}

You can use any of the following algorithms to process XML digital signatures.

<table>
  <tr>
    <th> Type of algorithm </th>
    <th> Algorithm options </th>
  </tr>
  <tr>
    <td>Canonicalization and transformation algorithms with and without comments</td>
    <td><ul><li><a href="http://www.w3.org/TR/2001/REC-xml-c14n-20010315" target="_blank">Canonicalization <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></li>
    <li><a href="http://www.w3.org/2001/10/xml-exc-c14n#" target="_blank">Exclusive Canonicalization with and without comments <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></li>
    <li><a href=" http://www.w3.org/2000/09/xmldsig#enveloped-signature" target="_blank">Enveloped Signature transform <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></li></ul></td>
  </tr>
  <tr>
    <td>Hashing algorithms</td>
    <td><ul><li><a href="http://www.w3.org/2000/09/xmldsig#sha1" target="_blank">SHA1 digests <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmlenc#sha256" target="_blank">SHA256 digests <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmlenc#sha512" target="_blank">SHA512 digests <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></li></ul></td>
  </tr>
  <tr>
    <td>Signature algorithms</td>
    <td><ul><li><a href="http://www.w3.org/2000/09/xmldsig#rsa-sha1" target="_blank">RSA-SHA1 <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmldsig-more#rsa-sha256" target="_blank">RSA-SHA256 <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmldsig-more#rsa-sha512" target="_blank">RSA-SHA512 <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></li>
    <li><a href="http://www.w3.org/2000/09/xmldsig#hmac-sha1" target="_blank">HMAC-SHA1 <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></li></ul></td>
  </tr>
</table>

For more information about using a SAML identity provider, see [Configuring enterprise identity providers](/docs/services/appid?topic=appid-enterprise).


## Obtaining more assertions
{: #saml-more-assertions}

It is possible to obtain extra information from your identity provider and then inject it into your tokens.
{: shortdesc}

You can use assertions in the same way that you use [attributes](/docs/services/appid?topic=appid-user-profile#user-profile). You might use assertions in your code for different reasons. Maybe you use assertions to determine membership, `isMember`. If your SAML provider returns the other assertions, it is possible to obtain the information when a user logs in. Then, by creating an array of the assertions you want to use, you can make a PUT request to the /config/tokens endpoint to inject them into your tokens. For more information, check out [customizing tokens](/docs/services/appid?topic=appid-customizing-tokens#customizing-tokens).

Be sure not to add more information than necessary to your tokens. Tokens are usually sent in http headers and headers are limited in size.
{: tip}

## Providing metadata to your identity provider
{: #saml-provide-idp}

To configure your app, you need to provide information to a SAML compatible identity provider. The information is exchanged through a metadata XML file that also contains configuration data that is used to establish trust.
{: shortdesc}

You cannot enable SAML until after it is configured.
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

3. Provide the data to your identity provider. If your identity provider supports uploading the metadata file, you can do so. If it doesn't, configure the properties manually. Not every identity provider will use the same properties, so if you don't use all of them, it's okay.

  The property names might differ between identity providers.
  {: tip}

4. Toggle **SAML 2.0 Federation** to **Enabled**.

## Providing metadata to {{site.data.keyword.appid_short_notm}}
{: #saml-provide-appid}

You can obtain data from your identity provider and provide it to {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

### Providing metadata with the GUI
{: #saml-provide-gui}

1. Navigate to the **SAML 2.0** tab of the {{site.data.keyword.appid_short_notm}} dashboard. Input the following metadata that you obtained from the identity provider in the **Provide Metadata from SAML IdP** section.
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


### Providing metadata with the API
{: #saml-provide-api}

1. Obtain your SAML metadata by making a GET request to the [/getSamlMetadata API endpoint](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Identity%20Providers/get_saml_idp).

  Example code:
  ```
  <?xml version="1.0"?>
  <getSamlMetadata>
    <?xml version="1.0"?> <EntityDescriptor> <SPSSODescriptor> <NameIDFormat> </NameIDFormat> <AssertionConsumerService /> </SPSSODescriptor>
   </EntityDescriptor>
    </getSamlMetadata>
  ```
  {: codeblock}

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
    },
    "validation_data": {
      "certificates": [
        {
          "certificate_index": 0,
          "expiration_timestamp": 1674473996,
          "warning": "Your certificate will expire in 18 days."
        }
      ]
    }
  }
  ```
  {: screen}

2. Configure your POST request to the [/set_saml_idp API endpoint](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Identity%20Providers/set_saml_idp).

  1. In the following metadata example, replace the variables with your own information.

    ```
    Put {Management URI}/config/idps/saml
    Content-Type: application/json
    {
      "isActive": true,
      "config": {
        "entityID": "https://example.com/saml2/metadata/706634",
        "signInUrl": "https://example.com/saml2/sso-redirect/706634",
        "certificates": [
          "primary-certificate-example-pem-format"
        ],
        "displayName": "my saml example"
      }
    }
    ```
    {: codeblock}

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

  2. Optional: Add a secondary certificate to the certificates array following the primary certificate. The secondary certificate is used if signature validation fails with the primary certificate. If the signing key remains the same, {{site.data.keyword.appid_short_notm}} does not block authentication for expired certificates.

    Example:
    ```
    {
      "isActive": true,
      "config": {
        ...
        "certificates": [
          "primary-certificate-example-pem-format",
          "secondary-certificate-example-pem-format"
        ],
        ...
      }
    }
    ```
    {: screen}
  {: #configuring-saml-new}
  3. Optional: Add an authentication context by adding a class array and comparison string to your code. Be sure to update both the `class` and `comparison` parameters with your values. An Authentication context is used to verify the quality of the authentication and SAML assertions.

    Example:
    ```
    {
      "isActive": true,
      "config": {
        ...
        "authnContext": {
          "class": [
            "urn:oasis:names:tc:SAML:2.0:ac:classes:YourChosenClassValue",
            "urn:oasis:names:tc:SAML:2.0:ac:classes:YourOtherChosenClassValue"
          ],
          "comparison": "sampleComparisonValue"
        }
      }
    }
    ```
    {: screen}

3. Make the request. If you chose to add the optional values, your request should look similar to the following example.

  ```
  Put {Management URI}/config/idps/saml
  Content-Type: application/json
  {
    "isActive": true,
    "config": {
      ...
      "authnContext": {
        "class": [
          "urn:oasis:names:tc:SAML:2.0:ac:classes:YourChosenClassValue",
          "urn:oasis:names:tc:SAML:2.0:ac:classes:YourOtherChosenClassValue"
        ],
        "comparison": "sampleComparisonValue"
      "entityID": "https://example.com/saml2/metadata/706634",
      "signInUrl": "https://example.com/saml2/sso-redirect/706634",
      "certificates": [
        "primary-certificate-example-pem-format"
        "secondary-certificate-example-pem-format"
      ],
      "displayName": "my saml example"
    }
  }
  ```
  {: codeblock}


## Testing your configuration
{: #saml-testing}

You can test the configuration between your SAML Identity Provider and {{site.data.keyword.appid_short_notm}}.

1. Be sure that you've saved your configuration.
2. Navigate to the **SAML 2.0** tab of the {{site.data.keyword.appid_short_notm}} dashboard and click **Test**. A new tab opens.
3. Login in with a user that your identity provider has already authenticated.
4. After you complete the form, you are redirected to another page.
  * Successful authentication: The connection between {{site.data.keyword.appid_short_notm}} and the Identity Provider is working correctly. The page displays valid [access and identity tokens](/docs/services/appid?topic=appid-key-concepts#tokens).
  * Failed authentication: The connection is broken. The page displays the errors and the SAML response XML file.


Having trouble? Check out [Troubleshooting identity provider configurations](/docs/services/appid?topic=appid-troubleshooting-idp).
{: tip}
