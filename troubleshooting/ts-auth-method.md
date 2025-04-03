---

copyright:
  years: 2017, 2025
lastupdated: "2025-04-03"

keywords: help, support, error, authentication method, match

subcollection: appid

content-type: troubleshoot

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

# Why doesn't my authentication method match?
{: #ts-auth-method}
{: troubleshoot}

You encounter issues authenticating.
{: shortdesc}

You recieve a message that the provided authentication method doesn't match the requested authentication method.
{: tsSymptoms}

For example:

```txt
AADSTS75011: Authentication method ‘X509, Multifactor, X509Device’ by which the user authenticated with the service doesn't match requested authentication method 'Password, ProtectedTransport'.
```
{: screen}

When {{site.data.keyword.appid_short_notm}} generates an authentication request, the authenciation context is used to request the quality of the authentication and SAML assertions.
{: tsCauses}

By default, {{site.data.keyword.appid_short_notm}} uses `urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport` and `exact` comparison in the `authnContext` as documented in [Understanding SAML](/docs/appid?topic=appid-enterprise), while you're trying to use a different authentication method. In the provided example the `X509, Multifactor` authentication method is used.

To resolve the issue, you can update your authentication context setting for both `class` and `comparison` values in the SAML `authnContext`. To update the context parameter to fit your use case, you can use the API.
{: tsResolve}

Alternatively, you can also set a blank `authnContext` in your SAML configuration as shown in the following example.

```json
  "authnContext": { }
```
{: codeblock}
