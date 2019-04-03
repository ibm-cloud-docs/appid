---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-02"

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

# Identity provider configurations
{: #troubleshooting-idp}

If you have problems when you are configuring identity providers to work with {{site.data.keyword.appid_full}}, consider these techniques for troubleshooting and getting help.
{: shortdesc}


## A user is not redirected to the identity provider
{: #ts-saml-redirect}

{: tsSymptoms}
A user tries to sign in to your application, but the sign-in page doesn't display when prompted.

{: tsCauses}
The identity provider can fail for several reasons:

* Your configured redirect URL is incorrect.
* The identity provider doesn't recognize the authentication request.
* The identity provider expects HTTP-POST binding.
* The identity provider expects a signed authnRequest.

{: tsResolve}
You can try some of these solutions:

* Update your sign-in URL. This URL is sent as part of the authnRequest and must be exact.
* Be sure that your {{site.data.keyword.appid_short_notm}} metadata is set correctly in your identity provider settings.
* Configure your identity provider to accept the authnRequest in the HTTP-Redirect.
* {{site.data.keyword.appid_short_notm}} does not support signing authnRequests.

If none of the solutions work, it is possible that you might have a connection issue.
{: tip}


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



## SAML response validation errors
{: #ts-saml-response}

{{site.data.keyword.appid_short_notm}} imposes the following validity requirements for assertions. All of the attributes are mandatory SAMLResponse XML nodes unless specified otherwise.
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
      <td><strong>Optional</strong>: When a conditions statement is included in an assertion, it must also contain a valid timestamp. {{site.data.keyword.appid_short_notm}} honors the validity period that is specified in an assertion. To verify, the service looks for the <code>NotBefore</code> and <code>NotOnOrAfter</code> constraints that must be defined and valid.</td>
    </tr>
  </tbody>
</table>

{{site.data.keyword.appid_short_notm}} does not support encrypted assertion. If your identity provider is set to encrypt your assertion, disable it. The assertion must be in an unencrypted format.
{: tip}
