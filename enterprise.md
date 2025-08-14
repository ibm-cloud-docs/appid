---

copyright:
  years: 2017, 2023
lastupdated: "2025-08-14"

keywords: saml, enterprise apps, assertions, single sign on, tokens, authorization, user authentication, key cloak, redhat, cloud identity, sso, single sign on, xml signature, service provider, identity provider, app security

subcollection: appid

---

{:codeblock: .codeblock}
{:screen: .screen}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:gif: data-image-type='gif'}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:tip: .tip}
{:preview: .preview}
{:deprecated: .deprecated}
{:beta: .beta}
{:term: .term}
{:shortdesc: .shortdesc}
{:script: data-hd-video='script'}
{:support: data-reuse='support'}
{:table: .aria-labeledby="caption"}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:help: data-hd-content-type='help'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:java: .ph data-hd-programlang='java'}
{:javascript: .ph data-hd-programlang='javascript'}
{:swift: .ph data-hd-programlang='swift'}
{:curl: .ph data-hd-programlang='curl'}
{:video: .video}
{:step: data-tutorial-type='step'}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:cli: .ph data-hd-interface='cli'}
{:api: .ph data-hd-interface='api'}
{:terraform: .ph data-hd-interface='terraform'}
{:release-note: data-hd-content-type='release-note'}

# SAML
{: #enterprise}

If you're using a SAML-based identity provider, you can configure {{site.data.keyword.appid_short_notm}} to initiate a single sign-on (SSO) experience. In this type of flow, {{site.data.keyword.appid_short_notm}} acts as a service provider and provides security tokens for your monthly active users (MAU).
{: shortdesc}

## Understanding SAML
{: #saml-understanding}

Security Assertion Markup Language (SAML) is an open standard that is used to exchange authentication and authorization data between the provider that asserts an identity and a provider that consumes the identity information. SAML 2.0 is based in XML and is a well-established framework for authentication and authorization standards.

The SAML protocol provides a bridge between {{site.data.keyword.appid_short_notm}} (service provider) and your identity provider. When the identity provider authenticates a user, it creates SAML tokens that contain information about the user such as how they authenticated, attributes that are associated with them, or authorization parameters. Check out the following table for examples.

| Type of information | Examples         |
|:--------------------|:-----------------|
| Authentication | Users might authenticate with a password, by using MFA, or another way. |
| Attributes | Any attributes such as groups that they belong to or a preference of some kind. |
| Authorization decisions | Occasionally users might be granted more or less permissions than others. |
{: caption="Understanding the types of information returned in a SAML token" caption-side="top"}


### What does the flow look like?
{: #saml-flow}

Although the SAML framework is used to authenticate the user, {{site.data.keyword.appid_short_notm}} still uses a more modern OIDC protocol to exchange security tokens with your application. Check out the following image to see a detailed flow of information.

![SAML enterprise authentication flow](/images/ibmid-flow.svg){: caption="How an enterprise SAML authentication flow works" caption-side="bottom"}


1. A user accesses the login page or restricted resource on their application, which initiates a request to the {{site.data.keyword.appid_short_notm}} `/authorization` endpoint through either an {{site.data.keyword.appid_short_notm}} SDK or API. If the user is unauthorized, the authentication flow begins with a redirect to {{site.data.keyword.appid_short_notm}}.
2. {{site.data.keyword.appid_short_notm}} generates a SAML authentication request (`AuthNRequest`) and the browser automatically redirects the user to the SAML identity provider.
3. The identity provider parses the SAML request, authenticates the user, and generates a SAML response with its assertions.
4. The identity provider redirects the user and the response back to {{site.data.keyword.appid_short_notm}} with the SAML response.
5. If the authentication is successful, {{site.data.keyword.appid_short_notm}} creates access and identity tokens that represent a user's authorization and authentication and returns them to the app. If the authentication fails, {{site.data.keyword.appid_short_notm}} returns the identity provider error code to the app.
6. The user is granted access to the app or the protected resources.


### How does SSO change the flow?
{: #saml-sso-flow}


The workflow for SSO is similar. The only deviation from the described workflow is in step 3 of the previous section. With SSO enabled, before a user is asked to authenticate, the identity provider checks whether a user already has an established authentication session. If yes, the user is not asked to authenticate and the flow continues as usual. If an SSO session is unavailable, then the user is redirected to a log in page. They might also be redirected if your identity provider can't match the authentication requirements that are defined in {{site.data.keyword.appid_short_notm}}'s request with what it uses to establish SSO. For example, if your identity provider establishes a user SSO session by using biometrics, then {{site.data.keyword.appid_short_notm}}'s default authentication must be changed. By default, {{site.data.keyword.appid_short_notm}} expects users to be authenticated by password over HTTPS: `urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport`.



## Understanding assertions
{: #saml-assertions}

When the SAML assertion is returned to {{site.data.keyword.appid_short_notm}}, the service federates the user identity and generates the appropriate tokens. If the SAML assertion corresponds to one of the standard OIDC claims, it's automatically added to the identity token. The assertions that don't have a match, are ignored by default. If your SAML provider returns other assertions, it's possible to configure {{site.data.keyword.appid_short_notm}} to [inject the information into your tokens](/docs/appid?topic=appid-customizing-tokens#customizing-tokens). But, be sure not to add more information than necessary to your tokens as they're typically sent in HTTP headers and limited.

The standard OIDC claims that {{site.data.keyword.appid_short_notm}} attempts to map to your assertion:

* `name`
* `email`
* `locale`
* `picture`

If one or more of those values change on the identity provider's side, the new values are available after the user logs in again.
{: note}


### What does {{site.data.keyword.appid_short_notm}} expect a SAML assertion to look like?
{: #saml-example}

The service expects a SAML assertion to look like the following example.

```sh
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

{{site.data.keyword.appid_short_notm}} uses the [RSA-SHA256](http://www.w3.org/2001/04/xmldsig-more#rsa-sha256){: external} algorithm to process XML digital signatures.



## Configuring SAML identity providers to work with {{site.data.keyword.appid_short_notm}}
{: #saml-configure}

You can configure SAML identity providers to work with {{site.data.keyword.appid_short_notm}} by providing metadata from {{site.data.keyword.appid_short_notm}} to your identity provider, and metadata from your identity provider to {{site.data.keyword.appid_short_notm}}.

### Providing metadata to your identity provider
{: #saml-provide-idp}
{: ui}

To configure your app, you need to provide information to a SAML compatible identity provider. The information is exchanged through a metadata XML file that also contains configuration data that is used to establish trust.
{: shortdesc}

You cannot enable SAML until after you configure it as an identity provider.
{: tip}

1. In the **Manage** tab of the {{site.data.keyword.appid_short_notm}} dashboard, click **Edit** in the **SAML** row to configure your settings.
2. Click **Download SAML Metadata file**. Your identity provider expects the following information from the file.

   | Variable | Description |
   | -------- | ----------- |
   | `EntityID` | The identifier that lets the identity provider know that {{site.data.keyword.appid_short_notm}} issued the SAML request. |
   | `Location URL` | The location that the identity provider sends the SAML assertions after successfully authenticating a user. |
   | `Binding` | The instructions on how the identity provider must send the SAML response. |
   | `NameID Format` | How the identity provider knows that which identifier format it needs to send in the subject of an assertion and how {{site.data.keyword.appid_short_notm}} identifies users. The ID must take the following form: `&lt;saml:NameID Format="urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress"&gt;`. |
   | `WantAssertionsSigned` | The way that an identity provider checks to see whether it needs to sign the assertion. The service expects that the assertion is signed, but does not support encrypted assertions. |
   | `KeyDescriptor` | The SAML signing and encryption certificates that can be used to configure your identity provider to verify the signed SAML request and encrypt the response. |
   {: caption="The information that is found in your metadata file" caption-side="top"}

3. Provide the data to your identity provider. If your identity provider supports uploading the metadata file, you can do so. If it doesn't, configure the properties manually. Not every identity provider uses the same properties, so you might not use all of them.

   The property names might differ between identity providers.
   {: tip}

4. Toggle **SAML 2.0 Federation** to **Enabled**.

### Providing metadata to {{site.data.keyword.appid_short_notm}}
{: #saml-provide-appid}

You can obtain data from your identity provider and provide it to {{site.data.keyword.appid_short_notm}}. You can initiate login to your applications from IBM Cloud or your identity provider.


#### Providing metadata in the console
{: #saml-provide-appid-gui}
{: ui}

To log in to your applications from the IBM Cloud UI, follow these steps.

1. Navigate to the **SAML 2.0** tab of the {{site.data.keyword.appid_short_notm}} dashboard.
2. Add the **Provider name**. The default name is SAML.
3. Enter the following metadata that you obtained from the identity provider in the **Provide Metadata from SAML IdP** section.

   | Variable |  Description |
   | -------- | ------------ |
   | `Sign-in URL` | The URL that the user is redirected to for authentication. It is hosted by your SAML identity provider. |
   | `Entity ID` | The globally unique name for a SAML identity provider. |
   | `Primary certificate` | The certificate issued by your SAML identity provider. It is used for signing and validating SAML assertions. All providers are different, but you might be able to download the signing certificate from your identity provider. The certificate must be in `.pem` format. |
   {: caption="The information that must be provided to {{site.data.keyword.appid_short_notm}}" caption-side="top"}

4. Optional: Provide a **Secondary certificate** that is used if signature validation fails on the primary certificate. If the signing key remains the same, {{site.data.keyword.appid_short_notm}} does not block authentication for expired certificates.
5. Click **Save**.

Want to set an authentication context? You can do so through the API.
{: tip}


#### Configuring IdP-initiated login in the console
{: #idp-login-ui}
{: ui}

Optionally, if you want to log in to your applications on IBM Cloud from your identity provider's UI, you can enable IdP-initiated login.

Follow steps 1 - 4 in the [Providing metadata in the console](/docs/appid?topic=appid-enterprise#saml-provide-appid-gui) section. Then, complete the following process.

5. Enable the **IdP initiated login**.
6. Enter the **IdP redirect URL**.
7. Click **Save**.



#### Providing metadata with the API
{: #saml-provide-appid-api}
{: api}


1. View your current SAML configuration, including your authentication context and certificates, by making a GET request to the [`/saml` API endpoint](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.get_saml_idp){: external}.

   Example code:
   ```sh
   curl --request GET \
   https://us-south.appid.cloud.ibm.com/management/v4/<tenantID>/config/idps/saml \
   --header `Accept: application/json`
   ```
   {: codeblock}

   Example output:
   ```json
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

2. Create your SAML configuration by replacing the values in the following example with the information from your provider. The values that are shown in the example are required, but you can choose to include more information as shown in the table.

   ```json
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
      "signRequest": true ,
      "encryptResponse": true
   }
   ```
   {: codeblock}
   {: #configuring-saml-new-values}

   | Variable | Description |
   | -------- | ----------- |
   | `signInUrl` | The URL that the user is redirected to for authentication. It is hosted by your SAML identity provider. |
   | `entityID` | The globally unique name for a SAML identity provider. |
   | `displayName` | The name that you assign to your SAML configuration. |
   | `primary-certificate-example-pem-format` | The certificate that is issued by your SAML identity provider. It is used for signing and validating SAML assertions. All providers are different, but you might be able to download the signing certificate from your identity provider. The certificate must be in `.pem` format. |
   | Optional: `secondary-certificate-example-pem-format` | The backup certificate that is issued by your SAML identity provider. It is used if signature validation fails with the primary certificate. **Note**: If the signing key remains the same, {{site.data.keyword.appid_short_notm}} does not block authentication for expired certificates. |
   | Optional: `authnContext` | The authentication context is used to verify the quality of the authentication and SAML assertions. You can add an authentication context by adding a class array and comparison string to your code. BE sure to update both the `class` and `comparison` parameters with your values. For example, a `class` parameter might look similar to `urn:oasis:names:tc:SAML:2.0:ac:classes:YourChosenClassValue`. |
   | Optional: `signRequest` | The `signRequest` flag provides the capability to send a signed SAML request to an identity provider that is signed by using the tenant's SAML signing private key. To configure your SAML identity provider to receive a signed request, you need the signing certificate from the metadata file that you can download in the `KeyDescriptor use="signing"` field. By default, request signing is set to `off`. |
   | Optional: `encryptResponse` | The `encryptResponse` flag allows for you to receive an encrypted response from your identity provider as part of the authentication request. To configure your SAML identity provider to send an encrypted response, you need the encryption certificate that can be found in the metadata file in the `KeyDescriptor use="encryption"` field. By default, response encryption is set to `off`.
   {: caption="SAML configuration variables" caption-side="top"}

3. Make a PUT request to the [`/saml` API endpoint](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp){: external} to provide the configuration that you created in step 2 to {{site.data.keyword.appid_short_notm}}. Check out the following example to see what your request might look like.

   ```sh
   curl --request PUT \
   https://us-south.appid.cloud.ibm.com/management/v4/<tenantID>/config/idps/saml \
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




#### Configuring IdP-initiated login with the API
{: #idp-login-api}
{: api}

To configure IdP-initiated login, complete the following steps.

1. View your current SAML configuration, including your authentication context and certificates, by making a GET request to the  [`/saml` API endpoint](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.get_saml_idp){: external}.

   Example code:
   ```sh
   curl --request GET \
   https://us-south.appid.cloud.ibm.com/management/v4/<tenantID>/config/idps/saml \
   --header `Accept: application/json`
   ```
   {: codeblock}

   Example output:
   ```json
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

2. Create your SAML configuration by replacing the values in the following example with the information from your provider. The values that are shown in the example are required, but you can choose to include more information as shown in the table.

   ```json
   "config": {
      "authnContext": {
      "class": [
         "urn:oasis:names:tc:SAML:2.0:ac:classes:YourChosenClassValue",
         "urn:oasis:names:tc:SAML:2.0:ac:classes:YourOtherChosenClassValue"
      ],
      "comparison": "sampleComparisonValue"
      },
      "idpInitEnabled": true,
      "idpRedirectUrl": "https://example.com/redirect/endpoint",
      "entityID": "https://example.com/saml2/metadata/706634",
      "signInUrl": "https://example.com/saml2/sso-redirect/706634",
      "certificates": [
      "primary-certificate-example-pem-format"
      "secondary-certificate-example-pem-format"
      ],
      "displayName": "my saml example",
      "signRequest": true ,
      "encryptResponse": true
   }
   ```
   {: codeblock}
   {: #configuring-saml-new}

   | Variable | Description |
   | -------- | ----------- |
   | `signInUrl` | The URL that the user is redirected to for authentication. It is hosted by your SAML identity provider. |
   | `entityID` | The globally unique name for a SAML identity provider. |
   | `displayName` | The name that you assign to your SAML configuration. |
   | `primary-certificate-example-pem-format` | The certificate that is issued by your SAML identity provider. It is used for signing and validating SAML assertions. All providers are different, but you might be able to download the signing certificate from your identity provider. The certificate must be in `.pem` format. |
   | `DefaultRelayState` | The initial value for `RelayState`. This variable is configured in your identity provider's settings. This variable can be used for the redirect URL instead of `idpRedirectUrl` during SAML requests from your identity provider. If you set both variables, the value of `DefaultRelayState` takes precedence. IdP-initiated login fails if you don't set one of these variables.  |
   | `idpInitEnabled` | A boolean to indicate whether you want to enable IdP initiated login. |
   | `idpRedirectUrl`|  This field's value can be `null`, a string that is empty, or a valid http or https redirect URL. **Note**: If this field's value is null, then you must set the `DefaultRelayState` as the redirect URL. If you set both variables, the value of `DefaultRelayState` takes precedence. IdP-initiated login fails if you don't set one of these variables. |
   | Optional: `secondary-certificate-example-pem-format` | The backup certificate that is issued by your SAML identity provider. It is used if signature validation fails with the primary certificate. **Note**: If the signing key remains the same, {{site.data.keyword.appid_short_notm}} does not block authentication for expired certificates. |
   | Optional: `authnContext` | The authentication context is used to verify the quality of the authentication and SAML assertions. You can add an authentication context by adding a class array and comparison string to your code. BE sure to update both the `class` and `comparison` parameters with your values. For example, a `class` parameter might look similar to `urn:oasis:names:tc:SAML:2.0:ac:classes:YourChosenClassValue`. |
   | Optional: `signRequest` | The `signRequest` flag provides the capability to send a signed SAML request to an identity provider that is signed by using the tenant's SAML signing private key. To configure your SAML identity provider to receive a signed request, you need the signing certificate from the metadata file that you can download in the `KeyDescriptor use="signing"` field. By default, request signing is set to `off`. |
   | Optional: `encryptResponse` | The `encryptResponse` flag allows for you to receive an encrypted response from your identity provider as part of the authentication request. To configure your SAML identity provider to send an encrypted response, you need the encryption certificate that can be found in the metadata file in the `KeyDescriptor use="encryption"` field. By default, response encryption is set to `off`.
   {: caption="SAML configuration variables" caption-side="top"}

3. Make a PUT request to the [`/saml` API endpoint](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp){: external} to provide the configuration that you created in step 2 to {{site.data.keyword.appid_short_notm}}. Check out the following example to see what your request might look like.

   ```sh
   curl --request PUT \
   https://us-south.appid.cloud.ibm.com/management/v4/<tenantID>/config/idps/saml \
   --header `Accept: application/json` \
   --data \
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
            },
            "idpInitEnabled": true,
            "idpRedirectUrl": "https://example.com/redirect/endpoint",
        }
   }
   ```
   {: screen}




### Testing your configuration
{: #saml-testing}

You can test the configuration between your SAML Identity Provider and {{site.data.keyword.appid_short_notm}}.

1. Be sure that you saved your configuration.
2. Navigate to the **SAML 2.0** tab of the {{site.data.keyword.appid_short_notm}} dashboard and click **Test**. A new tab opens.
3. Login in with a user that your identity provider already authenticated.
4. After you complete the form, you are redirected to another page.
   * Successful authentication: The connection between {{site.data.keyword.appid_short_notm}} and the Identity Provider is working correctly. The page displays valid [access and identity tokens](/docs/appid?topic=appid-tokens#tokens).
   * Failed authentication: The connection is broken. The page displays the errors and the SAML response XML file.

The SAML framework supports multiple profiles, flows, and configurations, which means that your identity provider must be configured correctly. If you run into issues, check out some common reasons why your [authentication request might fail](/docs/appid?topic=appid-ts-saml) or review the [SAML specification](https://docs.oasis-open.org/security/saml/Post2.0/sstc-saml-tech-overview-2.0.html){: external} for detailed error codes.
{: tip}
