---

copyright:
  years: 2017, 2021
lastupdated: "2021-05-24"

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

# How can I debug my SAML connection?
{: #ts-saml-debug-connection}
{: troubleshoot} 

You encounter bugs in your SAML connection. Check out some of the following helpful tips for debugging your SAML connection.
{: shortdesc}


## How do I capture my SAML authentication request and response?
{: #ts-saml-capture}

There are several options for browser plug-ins such as [Firefox](https://addons.mozilla.org/en-US/firefox/addon/saml-tracer/) and [Chrome](https://chrome.google.com/webstore/detail/saml-tracer/mpdajninpobndbfcldcmbpnnbhibjmch?hl=en) that can be used to capture your SAML requests and responses. Don't want to use a plug-in? No problem. Atlassian provides instructions for a more [manual extraction approach](https://confluence.atlassian.com/jirakb/how-to-view-a-saml-responses-in-your-browser-for-troubleshooting-872129244.html).


## I don't understand the messages! How can I decode them?
{: #ts-saml-decode-messages}

If you're still having trouble after using your SAML debug tool, try using the [SAML developer tools](https://www.samltool.com/online_tools.php) for more help decoding your messages. Don't forget! Depending on where you intercept your SAML messages, your request might be [URL encoded](https://www.samltool.com/online_tools.php), [base 64 encoded and deflated](https://www.samltool.com/decode.php), or [encrypted](https://www.samltool.com/decrypt.php).

Do not use online tools for decrypting SAML messages like your SAML response. The tools need access to the encryption private key in order to decrypt the information. The key should be kept private and access controlled. The decryption tool mentioned in this section should be used for debugging purposes only.
{: important}
