---

copyright:
  years: 2017, 2023
lastupdated: "2023-04-14"

keywords: secure mobile app, android, ios, authenticate users,  authorization grant, client sdk, trusted client, native app, personalized, custom app, devices, identity flow, app security

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

# Mobile apps
{: #mobile-apps}

With {{site.data.keyword.appid_full}}, you can quickly construct an authentication layer for your native or hybrid mobile app.
{: shortdesc}

## Understanding the flow
{: #understanding-mobile}

A mobile flow is useful when you are developing an app that is to be installed on a user's device (a native application). By using this flow, you can securely authenticate users on your app to provide personalized user experiences across devices.

### What is the flow's technical basis?
{: #mobile-technical-flow}

Since native applications are installed directly on a user's device, private user information and application credentials can be extracted by third-parties with relative ease. By default, these types of applications are known as untrusted clients as they cannot store global credentials or user refresh tokens. As a result, untrusted clients require users to input their credentials every time their access tokens expire.

To convert your application into a trusted client, {{site.data.keyword.appid_short_notm}} uses [Dynamic Client Registration](https://datatracker.ietf.org/doc/html/rfc6749){: external}. Before an application instance begins authenticating users, it first registers as an OAuth2 client with {{site.data.keyword.appid_short_notm}}. Because of client registration, your application receives an installation-specific client ID that can be digitally signed and used to authorize requests with {{site.data.keyword.appid_short_notm}}. Since {{site.data.keyword.appid_short_notm}} stores your application's corresponding public key, it can validate your request signature that allows your application to be viewed as a confidential client. This process minimizes your application's risk of exposing credentials indefinitely and greatly improves the user experience by allowing automatic token refresh.

Following registration, your users authenticate by using either the OAuth2 `authorization code` or `resource owner password` [authorization grant](https://datatracker.ietf.org/doc/html/rfc6749#section-1.3){: external} flows to authenticate users.


### Authorization flow
{: #mobile-auth-flow}

![{{site.data.keyword.appid_short_notm}} mobile request flow](images/mobile-flow.svg){: caption="Figure 1. {{site.data.keyword.appid_short_notm}} mobile request flow" caption-side="bottom"}

1. The {{site.data.keyword.appid_short_notm}} SDK starts the authorization process by using the {{site.data.keyword.appid_short_notm}} `/authorization` endpoint.
2. The login widget is displayed to the user.
3. The user authenticates by using one of the configured identity providers.
4. {{site.data.keyword.appid_short_notm}} returns an authorization grant.
5. The authorization grant is exchanged for access, identity, and refresh tokens from the {{site.data.keyword.appid_short_notm}} `/token` endpoint.


## Configuring your mobile app 
{: #configuring-mobile}

With the library of your choice, set your `Authorization` request header to use the `Bearer` authentication scheme to transmit the access token.

Example request format:

   ```sh
   GET /resource HTTP/1.1
   Host: server.example.com
   Authorization: Bearer <accessToken> <optionalIdentityToken>
   ```
   {: screen}


## Next steps
{: #mobile-next}

With {{site.data.keyword.appid_short_notm}} installed in your application, you're almost ready to start authenticating users! Try doing one of the following activities next:

* Configure your [identity providers](/docs/appid?topic=appid-social)
* Customize and configure [the Login Widget](/docs/appid?topic=appid-login-widget)


