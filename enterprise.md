---

copyright:
  years: 2017, 2018
lastupdated: "2018-10-18"

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

{{site.data.keyword.appid_short_notm}} functions as a service provider and initiates a single sign on (SSO) login to a third-party provider such as Active Directory Federation Services. The <a href="http://saml.xml.org/saml-specifications" target="blank">SAML <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> protocol supports different profiles and bind options. {{site.data.keyword.appid_short_notm}} supports the web browser SSO profile, with HTTP Post binding.

For steps on how to use a specific SAML identity provider, check out these blog posts on setting up {{site.data.keyword.appid_short_notm}} with [Ping One ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-ping-one/), [an Azure Active Directory ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-azure-active-directory/), or [an Active Directory Federation Service ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-active-directory-federation-service/).
{: tip}


## SAML assertions and identity token claims

A SAML assertion is a package of information that contains one or more statements. The assertion contains the authorization decision, and it might contain identity information about the user.

When a user signs in with an identity provider, that provider sends an assertion to {{site.data.keyword.appid_short_notm}}. {{site.data.keyword.appid_short_notm}} propagates user identity information that is returned in the SAML assertion to your app as OIDC token claims. The SAML attribute must correspond to 1 of the following OIDC claims to be added to the identity token.

The following claims can be added:
* `name`
* `email`
* `locale`
* `picture`

The remaining SAML attribute elements that do not correspond to any of the standard names are ignored. Note that if one or more of those values change on the provider's side, the new values are available only after the user logs in again.


Looking for an example? Check out <a href="https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-azure-active-directory/" target="_blank">Setting up {{site.data.keyword.appid_long}} with your Azure Active Directory <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> or <a href="https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-ping-one/" target="_blank">Setting up {{site.data.keyword.appid_long}} with Ping One <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.

## Providing metadata to your identity provider
{: #provide-idp}

To configure your app, you need to provide information to a SAML compatible identity provider. The information is exchanged through a metadata XML file that also contains configuration data that is used to establish trust.
{: shortdesc}

1. In the **Manage** tab of the {{site.data.keyword.appid_short_notm}} dashboard, set **SAML 2.0** to **On**. Then, click **Edit** to configure your SAML settings.
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

## Providing metadata to {{site.data.keyword.appid_short_notm}}
{: #provide-appid}

Obtain data from your identity provider and provide it to {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

**Providing metadata with the GUI**

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

</br>
</br>

**Providing metadata with the API**

1. Obtain your SAML metadata by making a GET request to the [/getSamlMetadata API endpoint](https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/getSamlMetadata).

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

2. Configure your POST request to the [/set_saml_idp API endpoint](https://appid-management.ng.bluemix.net/swagger-ui/#!/Identity_Providers/set_saml_idp).

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
{: #testing}

You can test the configuration between your SAML Identity Provider and {{site.data.keyword.appid_short_notm}}.

1. Be sure that you've saved your configuration.
2. Navigate to the **SAML 2.0** tab of the {{site.data.keyword.appid_short_notm}} dashboard and click **Test**. A new tab opens.
3. Login in with a user that your identity provider has already authenticated.
4. After you complete the form, you are redirected to another page.
  * Successful authentication: The connection between {{site.data.keyword.appid_short_notm}} and the Identity Provider is working correctly. The page displays valid [access and identity tokens](/docs/services/appid/authorization.html#tokens).
  * Failed authentication: The connection is broken. The page displays the errors and the SAML response XML file.


Having trouble? Check out [Troubleshooting identity provider configurations](/docs/services/appid/ts_saml.html).
{: tip}
