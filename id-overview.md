---

copyright:
  years: 2017
lastupdated: "2017-07-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Identity providers overview
{: #identity-providers-overview}

Identity providers are used to provide authentication to your applications.
{:shortdesc}

You can use the following identity providers in your mobile and web applications:

* **Facebook** - Your users log in to mobile or web apps with their Facebook credentials.
* **Google** -  Your users log in to mobile or web apps with their Google+ credentials.


## Using the default configuration
{: #default-configuration}

{{site.data.keyword.appid_short_notm}} provides a default configuration when you initially set up your identity providers. You can use the default configuration in development mode only. For each identity provider, these credentials are limited to 100 uses per {{site.data.keyword.appid_short_notm}} instance, per day. Before you publish your application, update the [default configuration](/docs/services/appid/identity-providers.html) to your own credentials.
