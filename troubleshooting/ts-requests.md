---

copyright:
  years: 2017, 2024
lastupdated: "2024-03-21"

keywords: help, support, error, multiple users, attribute, ticket, identity provider, redirect uri, custom url, virtual user, idp, identity settings, user profile

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

# Why am I receiving an error about too many requests?
{: #ts-requests}
{: troubleshoot} 
{: support}

{{site.data.keyword.appid_full}} is deprecated. As of 01 May 2024, you can't create new instances, and access to free instances will be removed. Existing instances are supported until 01 October 2025. Any instances that still exist on that date will be deleted. {: deprecated}

You receive an error about too many requests. 
{: shortdesc}

You attempt to view the home page of your app but receive the following error:
{: tsSymptoms}

```sh
{"error_code":"too many requests","error_description":"too many requests"}
```
{: screen}

You might receive a `too many requests` error if you are performing automated testing with only one virtual user. Sign-in attempts are limited to prevent brute force DDoS and other types of similar attacks. For more information, see [{{site.data.keyword.appid_short_notm}} limits](/docs/appid?topic=appid-known-issues-limits#general-limits).
{: tsCauses}

To resolve the issue, you might want to use multiple virtual users when you perform testing.
{: tsResolve}
