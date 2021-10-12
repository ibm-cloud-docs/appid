---

copyright:
  years: 2017, 2021
lastupdated: "2021-10-12"

keywords: security for {{site.data.keyword.appid_short_notm}}, compliance for {{site.data.keyword.appid_short_notm}}, security and compliance for {{site.data.keyword.appid_short_notm}}, rules for {{site.data.keyword.appid_short_notm}}, 

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
{:release-note: data-hd-content-type='release-note'}


# Managing security and compliance with {{site.data.keyword.appid_short_notm}}
{: #manage-security-compliance}

{{site.data.keyword.appid_short_notm}} is integrated with the {{site.data.keyword.compliance_short}} to help you manage security and compliance for your organization.
{: shortdesc}

With the {{site.data.keyword.compliance_short}}, you can:

* Monitor for controls and goals that pertain to {{site.data.keyword.appid_short_notm}}
* Define rules for {{site.data.keyword.appid_short_notm}} that can help to standardize resource configuration

## Monitoring security and compliance posture with {{site.data.keyword.appid_short_notm}}
{: #monitor-app-id}

As a security or compliance focal, you can use the {{site.data.keyword.appid_short_notm}} [goals](#x2117978){: term} to help ensure that your organization is adhering to the external and internal standards for your industry. By using the {{site.data.keyword.compliance_short}} to validate the resource configurations in your account against a [profile](#x2034950){: term}, you can identify potential issues as they arise.

All of the goals for {{site.data.keyword.appid_short_notm}} are added to the {{site.data.keyword.cloud_notm}} Best Practices Controls 1.0 profile but can also be mapped to other profiles.
{: note}

To start monitoring your resources, check out [Getting started with {{site.data.keyword.compliance_short}}](/docs/security-compliance?topic=security-compliance-getting-started).

### Available goals for {{site.data.keyword.appid_short_notm}} 
{: #app-id-available-goals}

* Check whether {{site.data.keyword.appid_short_notm}} webhooks are using HTTPS only
* Check whether {{site.data.keyword.appid_short_notm}} email dispatchers are using HTTPS only
* Check whether {{site.data.keyword.appid_short_notm}} redirect URIs are using HTTPS only
* Check whether {{site.data.keyword.appid_short_notm}} redirect URIs are not using localhost or 127.0.0.1
* Check whether {{site.data.keyword.appid_short_notm}} redirect URIs are not using wildcards (*)
* Check whether {{site.data.keyword.appid_short_notm}} user data is encrypted
* Check whether {{site.data.keyword.appid_short_notm}} user profile updates from client apps is disabled
* Check whether {{site.data.keyword.appid_short_notm}} Cloud Directory users aren't able to update their own accounts
* Check whether {{site.data.keyword.appid_short_notm}} Cloud Directory users aren't able to self-sign up to applications
* Check whether {{site.data.keyword.appid_short_notm}} runtime activity capture is enabled
* Check whether {{site.data.keyword.appid_short_notm}} social identity providers are disabled
* Check whether {{site.data.keyword.appid_short_notm}} anonymous authentication is disabled
* Check whether {{site.data.keyword.appid_short_notm}} password strength regex is configured
* Check whether {{site.data.keyword.appid_short_notm}} advanced password policies are enabled
* Check whether {{site.data.keyword.appid_short_notm}} avoid password reuse policy is enabled
* Check whether {{site.data.keyword.appid_short_notm}} lockout policy after failed # of sign-in attempts is enabled
* Check whether {{site.data.keyword.appid_short_notm}} lockout policy after a maximum specified time is enabled
* Check whether {{site.data.keyword.appid_short_notm}} minimum period between password changes policy is enabled
* Check whether {{site.data.keyword.appid_short_notm}} password expiration policy is enabled
* Check whether {{site.data.keyword.appid_short_notm}} prevent username in password policy is enabled
* Check whether {{site.data.keyword.appid_short_notm}} email verification is enabled for Cloud Directory users
* Check whether {{site.data.keyword.appid_short_notm}} customer-provided email service is used
* Check whether {{site.data.keyword.appid_short_notm}} multifactor authentication (MFA) is enabled for Cloud Directory users
* Check whether {{site.data.keyword.appid_short_notm}} access tokens are configured to expire within # minutes



