---

copyright:
  years: 2017, 2026
lastupdated: "2026-03-04"

keywords: saml, help, authentication request, error message, signing algorithm, xml file, signing certificate, valid email, error code, saml message signature, 

subcollection: appid

---

{{site.data.keyword.attribute-definition-list}}

# How can I debug my SAML connection?
{: #ts-saml-debug-connection}
{: troubleshoot} 

You encounter bugs in your SAML connection. Check out some following helpful tips for debugging your SAML connection.
{: shortdesc}


## How do I capture my SAML authentication request and response?
{: #ts-saml-capture}

There are several options for browser plug-ins such as [Firefox](https://addons.mozilla.org/en-US/firefox/addon/saml-tracer/) and [Chrome](https://chromewebstore.google.com/detail/saml-tracer/mpdajninpobndbfcldcmbpnnbhibjmch?hl=en) that can be used to capture your SAML requests and responses. If you don't want to use a plug-in, Atlassian provides instructions for a more [manual extraction approach](https://support.atlassian.com/jira/kb/capture-analyze-saml-responses-jira-sso-troubleshooting){: external}.


## I don't understand the messages! How can I decode them?
{: #ts-saml-decode-messages}

If you're still having trouble after using your SAML debug tool, try using the [SAML developer tools](https://www.samltool.com/online_tools.php) for more help decoding your messages. Don't forget! Depending on where you intercept your SAML messages, your request might be [URL encoded](https://www.samltool.com/online_tools.php), [base 64 encoded and deflated](https://www.samltool.com/decode.php), or [encrypted](https://www.samltool.com/decrypt.php).

Do not use online tools for decrypting SAML messages like your SAML response. The tools need access to the encryption private key to decrypt the information. The key should be kept private and access controlled. The decryption tool that is mentioned in this section must be used for debugging purposes only.
{: important}
