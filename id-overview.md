---

copyright:
  years: 2017
lastupdated: "2017-10-23"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Identity providers overview
{: #identity-providers-overview}

Identity providers are used to provide authentication for your mobile and web apps.
{:shortdesc}

You can use the following identity providers:

* Facebook - Your users log in to mobile or web apps with their Facebook credentials.
* Google -  Your users log in to mobile or web apps with their Google+ credentials.




## Using the default configuration
{: #default-configuration}

{{site.data.keyword.appid_short_notm}} provides a default configuration when you initially set up your identity providers. You can use the default configuration in development mode only. For each identity provider, the credentials are limited to 100 uses per {{site.data.keyword.appid_short_notm}} instance, per day. Before you publish your application, update the [default configuration](/docs/services/appid/identity-providers.html) to your own credentials.
