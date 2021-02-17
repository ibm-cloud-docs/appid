---

copyright:
  years: 2017, 2021
lastupdated: "2021-02-17"

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


# Managing security and compliance with {{site.data.keyword.appid_short_notm}}
{: #manage-security-compliance}

{{site.data.keyword.appid_short_notm}} is integrated with the {{site.data.keyword.compliance_short}} to help you manage security and compliance for your organization.
{: shortdesc}

With the {{site.data.keyword.compliance_short}}, you can:

* Monitor for controls and goals that pertain to {{site.data.keyword.appid_short_notm}}
* Define rules for {{site.data.keyword.appid_short_notm}} that can help to standardize resource configuration

## Monitoring security and compliance posture with {{site.data.keyword.appid_short_notm}}
{: #monitor-certificate-manager}

As a security or compliance focal, you can use the {{site.data.keyword.appid_short_notm}} [goals](#x2117978){: term} to help ensure that your organization is adhering to the external and internal standards for your industry. By using the {{site.data.keyword.compliance_short}} to validate the resource configurations in your account against a [profile](#x2034950){: term}, you can identity potential issues as they arise.

All of the goals for {{site.data.keyword.appid_short_notm}} are added to the {{site.data.keyword.cloud_notm}} Best Practices Controls 1.0 profile but can also be mapped to other profiles.
{: note}

To start monitoring your resources, check out [Getting started with {{site.data.keyword.compliance_short}}](/docs/security-compliance?topic=security-compliance-getting-started).

### Available goals for {{site.data.keyword.appid_short_notm}}
{: #certificate-manager-available-goals}

* Ensure webhooks use HTTPS only
* Ensure email dispatcher uses HTTPS
* Ensure redirect URIs use HTTPS only
* Ensure redirect URIs do not use local host or 127.0.0.1
* Ensure user data that is stored in App ID is encrypted
* Ensure the ability to update user profiles from a client app is disabled
* Ensure Cloud Directory users can not update their own account
* Ensure Cloud Directory users can not sign up for an application themselves
* Ensure runtime activity capture is enabled
* Ensure social identity providers are disabled
* Ensure anonymous authentication is disabled
* Ensure password strength regex is set up
* Ensure strong password policies are enabled
* Ensure strong password policies prevents password reuse is enabled
* Ensure strong password policies failed login lockout is enabled
* Ensure strong password policies failed login lockout time is enabled
* Ensure strong password policies time between password changes is enabled
* Ensure strong password policies password expiration is enabled
* Ensure strong password policies no userid in password is enabled
* Ensure email verification is enabled for Cloud Directory users
* Ensure customer-provided email service is used
* Ensure MFA is enabled for Cloud Directory users
* Ensure access tokens are configured to expire in under X minutes

