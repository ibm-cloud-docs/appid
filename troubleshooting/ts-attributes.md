---

copyright:
  years: 2017, 2021
lastupdated: "2021-05-24"

keywords: help, support, error, multiple users, attribute, ticket, identity provider, redirect uri, custom url, virtual user, idp, identity settings, user profile

subcollection: appid

content-type: troubleshoot

---

# Why are my attributes showing the wrong values?
{: #ts-saml-attribute}
{: troubleshoot}

You encounter issues with the values your attributes.
{:shortdesc}

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
