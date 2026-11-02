---

copyright:
  years: 2017, 2026
lastupdated: "2026-11-02"

keywords: help, support, error, multiple users, attribute, ticket, identity provider, redirect uri, custom url, virtual user, idp, identity settings, user profile

subcollection: appid

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why am I receiving an error about too many requests?
{: #ts-requests}
{: troubleshoot}
{: support}

{{site.data.keyword.appid_short_notm}} enforces rate limits on authentication requests. If your app exceeds these limits, you receive a too-many-requests error. This topic explains the limits that apply and how to resolve the error.
{: shortdesc}

You attempt to view the home page of your app but receive the following error:
{: tsSymptoms}

```sh
{"error_code":"too many requests","error_description":"too many requests"}
```
{: screen}

You might receive a `too many requests` error if you perform automated testing with only one virtual user. Sign-in attempts are limited to prevent brute force DDoS and other types of similar attacks. For more information, see [{{site.data.keyword.appid_short_notm}} limits](/docs/appid?topic=appid-known-issues-limits#general-limits).
{: tsCauses}

To resolve the issue, you might want to use multiple virtual users when you perform testing.
{: tsResolve}
