---

copyright:
  years: 2017, 2022
lastupdated: "2022-02-07"

keywords: authentication, authorization, identity, web flow, backend, identity management, anonymous auth, custom flow, mobile, app to app, kubernetes, ingress, istio, app security,

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


# Adding {{site.data.keyword.appid_short_notm}} overview
{: #adding-overview}


You can quickly add authentication and authorization to your application by integrating {{site.data.keyword.appid_short_notm}}. Regardless of the type of flow that you use, you can securely authenticate users to your app. With authentication in place, you can provide personalized user experiences across all types of devices.
{: shortdesc}


Check out the following table to see how {{site.data.keyword.appid_short_notm}} fits into each type of application.

| Type of authentication flow | Description |
|----|---|
| [Single-page](/docs/appid?topic=appid-single-page) | You can use the single-page flow to securely authenticate users to your applications. An SPA runs entirely in your browser and does not require that the page be reloaded while the application is in use. |
| [Web](/docs/appid?topic=appid-web-apps) | You can use the web flow to securely authenticate users to your application and protect your server-side resources. If your application has a backend that you manage, it's recommended that you use the web flow. |
| [Mobile](/docs/appid?topic=appid-mobile-apps) | The {{site.data.keyword.appid_short_notm}} mobile flow is most helpful when you're developing applications that are made to be installed on a user's device as a native application.|
| [Backend](/docs/appid?topic=appid-backend) | You can protect your development resources and API endpoints from unauthorized access and ensure the security of your app by using the backend flow. |
| [Custom](/docs/appid?topic=appid-custom-auth) | Already have your own custom flow? No problem. You can use the custom identity flow to integrate {{site.data.keyword.appid_short_notm}}  with your app. |
| [Anonymous](/docs/appid?topic=appid-anonymous) | With {{site.data.keyword.appid_short_notm}}, you can begin tracking a users activity before their initial sign-in to your app by using anonymous authentication. |
| [Ingress](/docs/appid?topic=appid-kube-auth) | With {{site.data.keyword.appid_short_notm}}, you can consistently enforce policy-driven security by using the Ingress networking capability in {{site.data.keyword.containerlong_notm}}. |
| [Istio](/docs/appid?topic=appid-istio-adapter) | By using the App Identity and Access adapter, you can centralize all your identity management in a single place. Because enterprises use clouds from multiple providers or a combination of on and off-premise solutions, heterogeneous deployment models can help you to preserve existing infrastructure and avoid vendor lock-in. |
{: caption="Table 1. The different ways in which you can secure your applications with {{site.data.keyword.appid_short_notm}}" caption-side="top"}

