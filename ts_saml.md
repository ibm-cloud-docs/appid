---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-15"

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


## Common SAML issues
{: #ts-common-saml}

Review the following table for explanations and resolutions for the most common issues that are encountered when you work with SAML.

<table summary="Every table row should be read left to right, with the cluster state in column one and a description in column two.">
  <thead>
    <th>Message</th>
    <th>Description</th>
  </thead>
  <tbody>
    <tr>
      <td><code>Could not parse assertion xml.</code></td>
      <td>The response from SAML was malformed.</td>
    </tr>
    <tr>
      <td><code>Invalid attribute without name. Contact your identity provider administrator.</code></td>
      <td>There is a <code>&lt;saml:Attribute&gt;</code> without a defined value. Contact your identity provider administrator.</td>
    </tr>
    <tr>
      <td><code>SAML response body must contain the RelayState parameter.</code></td>
      <td>The parameter was not included in the SAML response body. {{site.data.keyword.appid_short_notm}} provides the parameter to the identity provider as part of the request and the exact parameter must be returned in the response. If the parameter is modified, you can contact your identity provider administrator. </td>
    </tr>
    <tr>
      <td><code>SAML Configuration must have certificates, entityID and signInUrl of the IdP.</code></td>
      <td>The SAML identity provider is not <a href="/docs/services/appid?topic=appid-enterprise#enterprise" target="_blank">correctly configured</a>. Validate your configuration.</td>
    </tr>
    <tr>
      <td><code>Error in assertion validation. SAML Assertion signature check failed! Certificate .. may be invalid.</code></td>
      <td>A valid signature and digest must be included in the assertion. The signature must be created by using the private key that is associated with the certificate that is provided in the SAML configuration, either secondary or primary can be used. <strong>Note</strong>: {{site.data.keyword.appid_short_notm}} does not support encrypted assertion. If your identity provider encrypts your SAML assertion, disable encryption.</td>
    </tr>
  </tbody>
</table>



### SAML response validation errors
{: #ts-saml-response}

{{site.data.keyword.appid_short_notm}} imposes the following validity requirements for assertions. All of the attributes are mandatory SAML response XML nodes unless specified otherwise.
{: shortdesc}


<table summary="Every table row should be read left to right, with the response element in column one and a description in column two.">
  <thead>
    <th>Response element</th>
    <th>Description</th>
  </thead>
  <tbody>
    <tr>
      <td><code>samlp:Response</code></td>
      <td>The response element must be included in the Response XML.</td>
    </tr>
    <tr>
      <td><code>SAML version</code></td>
      <td>{{site.data.keyword.appid_short_notm}} accepts only <code>SAML version 2.0</code>.</td>
    </tr>
    <tr>
      <td><code>InResponseTo</code></td>
      <td>{{site.data.keyword.appid_short_notm}} verifies that the response element <code>InResponseTo</code> returned in the assertion matches the saved request ID from the SAML request.</td>
    </tr>
    <tr>
      <td><code>saml:issuer</code></td>
      <td>The issuer that is specified in an assertion must match the issuer that is specified in the {{site.data.keyword.appid_short_notm}} identity provider configuration.</td>
    </tr>
    <tr>
      <td><code>ds:Signature</code></td>
      <td>A valid signature and digest must be included in the assertion. The signature must be created by using the private key that is associated with the certificate that was provided in the SAML configuration. The digest is validated by using the specified <code>CanonicalizationMethod</code> and <code>Transforms</code>. <strong>Note</strong>: {{site.data.keyword.appid_short_notm}} does not validate certificate expiration. For help managing your certificates, try out [Certificate Manager](/docs/services/certificate-manager?topic=certificate-manager-getting-started#getting-started).</td>
    </tr>
    <tr>
      <td><code>saml:subject</code></td>
      <td>The subject or <code>name_id</code> of the assertion must be the Federation email of the user.</td>
    </tr>
    <tr>
      <td><code>saml:AttributeStatement</code></td>
      <td>Asserts that certain attributes are associated with a specific authenticated user.</td>
    </tr>
    <tr>
      <td><code>saml:Conditions</code></td>
      <td><strong>Optional</strong>: When a conditions statement is included in an assertion, it must also contain a valid timestamp. {{site.data.keyword.appid_short_notm}} honors the validity period that is specified in an assertion. To verify, the service looks for the <code>NotBefore</code> and <code>NotOnOrAcd fter</code> constraints that must be defined and valid.</td>
    </tr>
  </tbody>
</table>

{{site.data.keyword.appid_short_notm}} does not support encrypted assertion. If your identity provider is set to encrypt your assertion, disable it. The assertion must be in an unencrypted format.
{: tip}




### Responder error code
{: #ts-saml-responder}

{: tsSymptoms}
When you send an authentication request you receive a the following generic error message:

```
urn:oasis:names:tc:SAML:2.0:status:Responder
```
{: screen}

{: tsCauses}
Although App ID sends the initial authentication request, the identity provider must perform the user authentication and return the response. There are several reasons that might cause your identity provider to throw this error message.

You might see the message if your identity provider: 

* cannot find or verify the username.
* does not support the `NameID` format that is defined in the authentication request (`AuthNRequest`).
* does not support the authentication context.
* Requires the authentication request to be signed or use a specific algorithm in the signature.

{: tsResolve}
To resolve the issue, verify your configuration and username. Verify that you have the correct authentication context and variables defined. Check to see if your request needs to be signed in a specific way.


### Unsupported authentication request
{: #ts-saml-unsupported-request}

{: tsSymptoms}
You receive a message regarding an unsupported authentication request.

{: tsCauses}
When App ID generates an authentication request, it can use the authentication context to request the quality of the authentication and SAML assertions.

{: tsResolve}
To resolve the issue, you can update your authentication context. By default, App ID uses the authentication class `urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport` and comparison `exact`. You can update the context parameter to fit your use case by using the APIs.


### SAML request signing failure
{: #ts-saml-unsupported-request}

{: tsSymptoms}
You receive an error that states that an authentication request cannot be verified.

{: tsCauses}
App ID can be configured to sign the SAML authentication request (`AuthNRequest`), but your identity provider must be configured to expect the corresponding configuration.

{: tsResolve}
To resolve the issue:

* *Verify that App ID configure to sign the authentication request by setting the `signRequest` parameter to `true` by using the [set SAML IdP API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp). You can check to see if your authentication request is signed by looking at the request URL. The signature is included as a query parameter. For example: `https://idp.example.org/SAML2/SSO/Redirect?SAMLRequest=request&SigAlg=value&Signature=value&RelayState=token`

* Verify that your identity provider is configured with the correct certificate. To obtain the signing certificate check the App ID metadata XML file that you downloaded from the App ID dashboard. Ensure that you define the key as `<KeyDescriptor use="signing">`.

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

There are several options for browser plugins such as [Firefox](https://addons.mozilla.org/en-US/firefox/addon/saml-tracer/) and [Chrome](https://chrome.google.com/webstore/detail/saml-tracer/mpdajninpobndbfcldcmbpnnbhibjmch?hl=en) that can be used to capture your SAML requests and responses. Don't want to use a plug-in? No problem. Atlassian provides an instructions for a more [manual extraction approach](https://confluence.atlassian.com/jirakb/how-to-view-a-saml-responses-in-your-browser-for-troubleshooting-872129244.html).


### My SAML messages are gibberish! How can I decode them?
{: #ts-saml-decode-messages}

If you're still having trouble after using your SAML debug tool, try using the [SAML developer tools](https://www.samltool.com/online_tools.php) for more help decoding your messages. Don't forget! Depending on where you intercept your SAML messages, your request might be [URL encoded](https://www.samltool.com/online_tools.php), [base 64 encoded and deflated](https://www.samltool.com/decode.php), or [encrypted](https://www.samltool.com/decrypt.php).

Do not use online tools for decrypting SAML messages like your SAML response because the tools need access to the encryption private key in order to decrypt the information. The private key should be kept private and access controlled. The decryption tool mentioned in this section should be used for debugging purposes only.
{: important}