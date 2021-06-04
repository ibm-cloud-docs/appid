---

copyright:
  years: 2017, 2021
lastupdated: "2021-06-02"

keywords: saml, help, authentication request, error message, signing algorithm, xml file, signing certificate, valid email, error code, saml message signature, 

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

# Why did my SAML authentication request fail?
{: #ts-saml}
{: troubleshoot} 
{: support}

You encounter issues with your SAML authentication.
{:shortdesc}

## Why can't my SAML message signature be validated?
{: #ts-saml-validated}

When you test your application, you receive the following error message:
{: tsSymptoms}

```
The SAML message signature could not be validated
```
{: screen}

This error occurs when {{site.data.keyword.appid_short_notm}} cannot verify the signature that is sent by SAML.
{: tsCauses}

To resolve the issue, verify that you have **Inbound Signature** set to **None** in your configuration.
{: tsResolve}

## Why is the `RelayState` parameter missing from my authentication response?
{: #ts-saml-relaystate}

The `RelayState` parameter is missing from your authentication response.
{: tsSymptoms}


{{site.data.keyword.appid_short_notm}} sends an opaque parameter that is known as `RelayState` as part of the authentication request. If you do not see the parameter in your response, your identity provider might not be configured to return it correctly. The `RelayState` takes the following form.
{: tsCauses}

```
https://idp.example.org/SAML2/SSO/Redirect?SAMLRequest=request&RelayState=token
```
{: screen}

Verify that your SAML provider is configured to return the `RelayState` parameter to {{site.data.keyword.appid_short_notm}} without modifying it in any way.
{: tsResolve}

## Why am I receiving an error about my Name ID?
{: #ts-saml-nameid}

When you send an authentication request, you receive an error that regards the `NameID`.
{: tsSymptoms}

{{site.data.keyword.appid_short_notm}}, as the service provider, defines the way that users are identified by the service and by the identity provider. With {{site.data.keyword.appid_short_notm}}, users are identified in the `NameID` authentication request in the `NameID` field as shown in the following example.
{: tsCauses}

```
<NameIDFormat>urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress</NameIDFormat>
```
{: screen}

To resolve the issue, be sure that your identity provider `NameID` is formatted as an email address. Verify that all of the users in your identity provider registry have a valid email address format. Then, verify that the `NameID` field is appropriately defined so that a valid email is always returned - even if users in your registry have multiple emails.
{: tsResolve}

## Failure to decrypt the response
{: #ts-saml-decrypt-fail}

You receive one of the following error messages in response to your authentication request.
{: tsSymptoms}

Error message 1:

```
Unexpectedly received an encrypted assertion. Please enable response encryption in your {{site.data.keyword.appid_short_notm}} SAML configuration.
```
{: screen}

Error message 2: 

```
Could not decrypt SAML assertion. Ensure your SAML provider is configured with the {{site.data.keyword.appid_short_notm}} encryption. 
```
{: screen}


If your identity provider is configured to encrypt, {{site.data.keyword.appid_short_notm}} must be configured to sign the SAML authentication requests (AuthnRequest). Then, your identity provider must be configured to expect the corresponding configuration. You might receive these errors for one of the following reasons:
{: tsCauses}

- {{site.data.keyword.appid_short_notm}} is not configured to expect that the identity provider SAML response is encrypted.
- {{site.data.keyword.appid_short_notm}} cannot correctly decrypt your assertions.


If you receive error message 1, verify that your SAML configuration is set to expect an encrypted response. By default, {{site.data.keyword.appid_short_notm}} does not expect the response to be encrypted. To configure encryption, set the `encryptResponse` parameter to **true** by using [the API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp).
{: tsResolve}

If you receive error message 2, ensure that your certificate is correct. You can obtain the signing certificate from the {{site.data.keyword.appid_short_notm}} metadata XML file. Be sure that you use the key with `<KeyDescriptor use="signing">`. Verify that your identity provider is configured to use `` as the signature signing algorithm. 

## Responder error code
{: #ts-saml-responder}

When you send an authentication request you receive the following generic error message:
{: tsSymptoms}

```
urn:oasis:names:tc:SAML:2.0:status:Responder
```
{: screen}

Although {{site.data.keyword.appid_short_notm}} sends the initial authentication request, the identity provider must perform the user authentication and return the response. There are several reasons that might cause your identity provider to throw this error message.
{: tsCauses}

You might see the message if your identity provider: 

* Cannot find or verify the username.
* Does not support the `NameID` format that is defined in the authentication request (`AuthnRequest`).
* Does not support the authentication context.
* Requires the authentication request to be signed or use a specific algorithm in the signature.

To resolve the issue, verify your configuration and username. Verify that you have the correct authentication context and variables defined. Check to see if your request needs to be signed in a specific way.
{: tsResolve}

## Unsupported authentication request
{: #ts-saml-unsupported-request}

You receive a message regarding an unsupported authentication request.
{: tsSymptoms}

When {{site.data.keyword.appid_short_notm}} generates an authentication request, it can use the authentication context to request the quality of the authentication and SAML assertions.
{: tsCauses}

To resolve the issue, you can update your authentication context. By default, {{site.data.keyword.appid_short_notm}} uses the authentication class `urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport` and comparison `exact`. You can update the context parameter to fit your use case by using the APIs.
{: tsResolve}

## SAML request signing failure
{: #ts-saml-request-sign-fail}

You receive an error that states that an authentication request cannot be verified.
{: tsSymptoms}

{{site.data.keyword.appid_short_notm}} can be configured to sign the SAML authentication request (`AuthNRequest`), but your identity provider must be configured to expect the corresponding configuration.
{: tsCauses}

To resolve the issue:
{: tsResolve}

* Verify that {{site.data.keyword.cloud_notm}} is configured to sign the authentication request by setting the `signRequest` parameter to `true` by using the [set SAML IdP API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp). You can check to see if your authentication request is signed by looking at the request URL. The signature is included as a query parameter. For example: `https://idp.example.org/SAML2/SSO/Redirect?SAMLRequest=request&SigAlg=value&Signature=value&RelayState=token`

* Verify that your identity provider is configured with the correct certificate. To obtain the signing certificate check the {{site.data.keyword.cloud_notm}} metadata XML file that you downloaded from the {{site.data.keyword.cloud_notm}} dashboard. Ensure that you use the key with `<KeyDescriptor use="signing">`.

* Verify that your identity provider is configured to use `` as the signing algorithm.
