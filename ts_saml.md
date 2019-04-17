---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-17"

keywords: authentication, authorization, identity, app security, secure, development, idp, troubleshooting, redirected, validation

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
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}

# Troubleshooting: SAML
{: #troubleshooting-idp}

If you have problems when you are configuring SAML to work with {{site.data.keyword.appid_full}}, consider these techniques for troubleshooting and getting help.
{: shortdesc}


## Common configuration issues
{: #ts-common-saml}

The SAML framework supports multiple profiles, flows, and configurations, which means that it is essential that your identity provider configuration is configured correctly. Check out the following topics for help resolving some of the common issues that you might encounter when working with SAML.
{: shortdesc}



### Service provider initiated
{: #ts-samle-sp-initiated}

The web browser SSO profile that App ID implements is service provider initiated, which means that App ID must send a SAML request to the identity provider to initiate the authentication session. App ID does not currently support identity provider initiated flows and they should not be used with the service at this time.




### Missing RelayState parameter
{: #ts-saml-relaystate}

App ID sends a RelayState as part of its authentication request. The RelayState is App ID specific information and must be returned, unmodified, by the identity provider. The RelayState takes the following form.

```
https://idp.example.org/SAML2/SSO/Redirect?SAMLRequest=request&RelayState=token
```
{: screen}


### Identity provider supports SSO
{: #ts-saml-idp-support-sso}

If your identity provider supports SSO, then it is possible that the SAML authentication uses the already established SSO session to authenticate the user. If it does not, the user is redirected to a login page. They might be redirected if your identity provider can't match the authentication requirements that are defined in App ID's authentication request with what it uses to establish SSO. For example, if your identity provider establishes a user SSO session by using biometrics, then App ID's default authentication context must be changed. By default, App ID expects users to be authenticated by password over HTTPS: `urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport`.





### Missing or incorrect NameID field
{: #ts-saml-nameid}

**What's happening**

When you send an authentication request, you receive an error regarding the `NameID`.

**Why it's happening**

App ID as the service provider, defines the way that users are identitfied by the service and by the identity provider. With App ID, users are identitified in the `NameID` authentication request in the `NameID` field as shown in the following example.

```
<NameIDFormat>urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress</NameIDFormat>
```
{: screen}

**How to fix it**

To resolve the issue, be sure that your identity provider `NameID` is formatted as an email address. Verify that all of the users in your identity provider registry have a valid email address format. Then, verify that the `NameID` field is appropriately defined so that a valid email is always returned - even if users in your registry have multiple emails.





### Response signing failure
{: #ts-saml-response-sign-fail}

**What's happening**

When you send an authentication request you receive the following error message:

```
Could not verify SAML assertion signature. Ensure App ID is configurated with your SAML provider's signing certificate.
```
{: screen}

**Why it's happening**

App ID expects all SAML assertions in your response to be signed. If the service cannot find or verify the signature in the response, the error is returned.

**How to fix it**

To resolve the issue, be sure that:

* You have extracted the signing certificate from your identity providers metadata XML file. Be sure that you use the key with `<KeyDescriptor use="signing">`.
* You have set the response signing algorithm to be XXX. 







### Failure to decrypt the response
{: #ts-saml-decrypt-fail}

**What's happening**

You receive one of the following error messages in response to your authentication request.

Error message 1:

```
Unexpectedly received an encrypted assertion. Please enable response encryption in your App ID SAML configuration.
```
{: screen}

Error message 2: 

```
Could not decrypt SAML assertion. Ensure your SAML provider is configured with the App ID encryption 
```
{: screen}


**Why it's happening**

If your identity provider is configured to encrypt, App ID must be configured to sign the SAML authentication requests (AuthNRequest). Then, your identity provider must be configured to expect the corresponding configuration. You might receive these errors for one of the following reasons:

- App ID is not configured to expect that the identity provider SAML response is encrypted.
- App ID cannot correctly correctly decrypt your assertions.


**How to fix it**

If you receive error message 1, verify that your SAML configuration is set to expect an encrypted response. By default, App ID does not expect the response to be encrypted. To configure encryption, set the `encryptResponse` parameter to **true** by using [the API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp).

If you receive error message 2, ensure that your certificate is correct. You can obtain the signing certificate from the App ID metadata XML file. Be sure that you use the key with `<KeyDescriptor use="signing">`. Verify that your identity provider is configured to use `` as the signature signing algorithm. 


### Responder error code
{: #ts-saml-responder}

**What's happening**

When you send an authentication request you receive the following generic error message:

```
urn:oasis:names:tc:SAML:2.0:status:Responder
```
{: screen}

**Why it's happening**

Although App ID sends the initial authentication request, the identity provider must perform the user authentication and return the response. There are several reasons that might cause your identity provider to throw this error message.

You might see the message if your identity provider: 

* cannot find or verify the username.
* does not support the `NameID` format that is defined in the authentication request (`AuthNRequest`).
* does not support the authentication context.
* requires the authentication request to be signed or use a specific algorithm in the signature.

**How to fix it**

To resolve the issue, verify your configuration and username. Verify that you have the correct authentication context and variables defined. Check to see if your request needs to be signed in a specific way.




### Unsupported authentication request
{: #ts-saml-unsupported-request}

**What's happening**

You receive a message regarding an unsupported authentication request.

**Why it's happening**

When App ID generates an authentication request, it can use the authentication context to request the quality of the authentication and SAML assertions.

**How to fix it**

To resolve the issue, you can update your authentication context. By default, App ID uses the authentication class `urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport` and comparison `exact`. You can update the context parameter to fit your use case by using the APIs.




### SAML request signing failure
{: #ts-saml-request-sign-fail}

**What's happening**

You receive an error that states that an authentication request cannot be verified.

**Why it's happening**

App ID can be configured to sign the SAML authentication request (`AuthNRequest`), but your identity provider must be configured to expect the corresponding configuration.

**How to fix it**

To resolve the issue:

* Verify that App ID configure to sign the authentication request by setting the `signRequest` parameter to `true` by using the [set SAML IdP API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp). You can check to see if your authentication request is signed by looking at the request URL. The signature is included as a query parameter. For example: `https://idp.example.org/SAML2/SSO/Redirect?SAMLRequest=request&SigAlg=value&Signature=value&RelayState=token`

* Verify that your identity provider is configured with the correct certificate. To obtain the signing certificate check the App ID metadata XML file that you downloaded from the App ID dashboard. Ensure that you use the key with `<KeyDescriptor use="signing">`.

* Verify that your identity provider is configured to use `` as the signing algorithm.





## Interpreting SAML error codes
{: #ts-saml-interpret-codes}

For specific error codes and messages from your identity provider that you don't see on this page, it can be helpful to search the [SAML specification](http://docs.oasis-open.org/security/saml/Post2.0/sstc-saml-tech-overview-2.0.html) for detailed explanations. If you don't find what you're looking for, you can reach out to your identity providers admin for more information.
{: shortdesc}


## Debugging your connection
{: #ts-saml-debug-connection}

Have the configuration correct but still have a bug? Check out some of the following helpful tips for debugging your SAML connection.
{: shortdesc}


### How do I capture my SAML authentication request and response?
{: #ts-saml-capture}

There are several options for browser plug-ins such as [Firefox](https://addons.mozilla.org/en-US/firefox/addon/saml-tracer/) and [Chrome](https://chrome.google.com/webstore/detail/saml-tracer/mpdajninpobndbfcldcmbpnnbhibjmch?hl=en) that can be used to capture your SAML requests and responses. Don't want to use a plug-in? No problem. Atlassian provides an instructions for a more [manual extraction approach](https://confluence.atlassian.com/jirakb/how-to-view-a-saml-responses-in-your-browser-for-troubleshooting-872129244.html).


### My SAML messages are gibberish! How can I decode them?
{: #ts-saml-decode-messages}

If you're still having trouble after using your SAML debug tool, try using the [SAML developer tools](https://www.samltool.com/online_tools.php) for more help decoding your messages. Don't forget! Depending on where you intercept your SAML messages, your request might be [URL encoded](https://www.samltool.com/online_tools.php), [base 64 encoded and deflated](https://www.samltool.com/decode.php), or [encrypted](https://www.samltool.com/decrypt.php).

Do not use online tools for decrypting SAML messages like your SAML response. The tools need access to the encryption private key in order to decrypt the information. The key should be kept private and access controlled. The decryption tool mentioned in this section should be used for debugging purposes only.
{: important}