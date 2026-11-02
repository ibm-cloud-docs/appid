---

copyright:
  years: 2017, 2026
lastupdated: "2026-11-02"

keywords: help, support, error, multiple users, attribute, ticket, identity provider, redirect uri, custom url, virtual user, idp, identity settings, user profile

subcollection: appid

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why are my attributes showing the wrong values?
{: #ts-saml-attribute}
{: troubleshoot}

When you encounter an issue where an attribute value exists in an {{site.data.keyword.appid_short_notm}} user profile but is not associated with the correct attribute, it is likely caused by how your identity provider maps user information during sign-in.
{: shortdesc}

An attribute value exists in a user profile, but it's not associated with the correct attribute.
{: tsSymptoms}

The user profile attribute is not mapped correctly.
{: tsCauses}

Map the attribute in your identity provider settings. {{site.data.keyword.appid_short_notm}} expects the following attributes:
{: tsResolve}

* `name`
* `email`
* `locale`
* `picture`
