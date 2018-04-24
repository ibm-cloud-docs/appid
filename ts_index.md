---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}

# Troubleshooting
{: #troubleshooting}

If you have problems while you're working with {{site.data.keyword.appid_full}}, consider these techniques for troubleshooting and getting help.
{: shortdesc}


## Getting help and support
{: #gettinghelp}

You can get help by searching for information or by asking questions through a forum. You can also open a support ticket. When you are using the forums to ask a question, tag your question so that it is seen by the {{site.data.keyword.Bluemix_notm}} development teams.
  * If you have technical questions about {{site.data.keyword.appid_short_notm}}, post your question on <a href="http://stackoverflow.com/search?q=ibm+" target="_blank">Stack Overflow <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> and tag your question with "ibm-appid".
  * For questions about the service and getting started instructions, use the <a href="https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=appid%20[bluemix]" target="_blank">dW Answers <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> forum. Include the `appid` tag.

For more information about getting support, see [How do I get the support that I need?](/docs/get-support/howtogetsupport.html#getting-customer-support).

</br>

## There is no redirect to the app after sign in
{: #signin-fail}

{: tsSymptoms}
A user signs into your application through an identity provider's sign in page, and either nothing happens or the sign in fails.

{: tsCauses}
Sign in might fail for the following reasons:

* Your redirect URL was not properly added to [the whitelist](identity-providers.html#redirect).
* The user is not authorized.
* The user tried to sign in with the wrong credentials.

{: tsResolve}
For a redirect to occur:

* Verify that your redirect URL is correct. It must be exact for the redirect to work.
* Be sure that your user is signing in with the right credentials
* Check that they're configured in your identity provider user settings.

</br>

## Common issues when working with SAML
{: #common-saml}

Review the following table for explanations and resolutions for the most common issues that are encountered when working with SAML.

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
      <td>There is a <code><saml:Attribute> without a defined value. Contact your identity provider administrator.</code></td>
    </tr>
    <tr>
      <td><code>SAML response body must contain RelayState.</code></td>
      <td>The RelayState parameter was no included in the SAML response body. {{site.data.keyword.appid_short_notm}} provides the parameter to the identity provider as part of the request and the exact parameter must be returned in the response. If the parameter is modified, you can contact your identity provider administrator. </td>
    </tr>
    <tr>
      <td><code>SAML Configuration must have certificates, entityID and signInUrl of the IdP.</code></td>
      <td>The SAML identity provider is not correctly configured. Validate your configuration. For help, see <a href="enterprise.html#configuring-saml" target="_blank">Configuring your app to work with an external SAML identity provider.</a></td>
    </tr>
    <tr>
      <td><code>Error in assertion validation. SAML Assertion signature check failed! Certificate .. may be invalid.</code></td>
      <td>A valid signature and digest must be included in the assertion. The signature must be created by using the private key associated with the certificate that is provided in the SAML configuration; either secondary or primary can be used. <em>Note</em>: {{site.data.keyword.appid_short_notm}} does not support encrypted assertion. If your identity provider does this to your SAML assertion, disable encryption.</td>
    </tr>
  </tbody>
</table>


## There is no redirect to the identity provider when using SAML
{: #saml-redirect}

{: tsSymptoms}
A user tries to sign in to your application, but the sign in page doesn't display when prompted.

{: tsCauses}
The identity provider can fail for several reasons:

* Your configured redirect URL is incorrect.
* The identity provider doesn't recognize the authentication request.
* The identity provider expects HTTP-POST binding.
* The identity provider expects a signed authnRequest.

{: tsResolve}
You can try some of these solutions:

* Update your sign in URL. This URL is sent as part of the authnRequest and must be exact.
* Be sure that your {{site.data.keyword.appid_short_notm}} metadata is set correctly in your identity provider settings.
* Configure your identity provider to accept the authnRequest in the HTTP-Redirect.
* {{site.data.keyword.appid_short_notm}} does not support signing authnRequests.

If none of those solutions work, it is possible that you might have a connection issue.

</br>

## An attribute is showing the wrong value when using SAML
{: #saml-attribute}

{: tsSymptoms}
An attribute value exists in a user profile, but it's not connected to the correct attribute.

{: tsCauses}
The User Profile Attribute is not mapped correctly.

{: tsResolve}
Map the attribute in your identity provider settings. {{site.data.keyword.appid_short_notm}} expects the following attributes:
* `name`
* `email`
* `locale`
* `picture`
