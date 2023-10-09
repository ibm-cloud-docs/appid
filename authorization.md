---

copyright:
  years: 2017, 2023
lastupdated: "2023-10-09"

keywords: authorization, authentication, oidc, oauth, jwks, app security, identity, tokens, redirect uris, api strategy, webapp strategy

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
{:terraform: .ph data-hd-interface='terraform'}
{:release-note: data-hd-content-type='release-note'}

# Technologies
{: #key-concepts}

Confused about the differences between authorization and authentication? You're not alone. Check out the following information to learn about specific terminology, processes, and the technologies that are used when you work with {{site.data.keyword.appid_full}}.
{: shortdesc}

Want to know more about some basic concepts of authorization and authentication? Look no further. In the following video you can learn about OAuth 2.0, grant types, OIDC, and more.

![About the {{site.data.keyword.appid_short_notm}} technologies](https://www.youtube.com/embed/ndlk-ZhKGXM){: video output="iframe" data-script="none" id="youtubeplayer" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen}



## OAuth 2
{: #term-oauth}

[OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc6749){: external} is open standard protocol that is used to provide app authorization.


## Open ID Connect (OIDC)
{: #term-oidc}

[OIDC](https://openid.net/developers/specs/){: external} is an authentication layer that works with OAuth 2. When you use OIDC and {{site.data.keyword.appid_short_notm}} together, your application credentials help to configure your OAuth endpoints. If you use the SDK, the endpoint URLs are built automatically. But, you can also build the URLs yourself by using your service credentials. The URL takes the following form: {{site.data.keyword.appid_short_notm}} service endpoint + "/oauth/v4" + /tenantID.

Example:

```json
{
  "clientId": "7eba72ef-b913-47b0-b3b6-54358bb69035",
  "tenantId": "8f5aa500-357e-443a-aab6-bf878f852b5a",
  "secret": "OWEzZGM4M2UtZjhlYS00MDI2LTkwNGItNDJmYzViMmU2YzIz",
  "name": "testing",
  "oAuthServerUrl": "https://us-south.appid.cloud.ibm.com/oauth/v4/8f5aa500-357e-443a-aab6-bf878f852b5a",
  "profilesUrl": "https://us-south.appid.cloud.ibm.com",
  "discoveryEndpoint": "https://us-south.appid.ibm.cloud.com/oauth/v4/8f5aa500-357e-443a-aab6-bf878f852b5a/.well-known/openid-configuration"
}
```
{: screen}

Using this example, the URL would be `https://us-south.appid.cloud.ibm.com/oauth/v4/8f5aa500-357e-443a-aab6-bf878f852b5a`. You would then append the endpoint that you wanted to make a request to. Check out the following table to see some example endpoints.

| Endpoint | Format |
|-----|----| 
| Authorization | `<oauthServerUrl>/authorization` |
| Token | `<oauthServerUrl>/token` |
| User information | `<oauthServerUrl>/userinfo` |
| JWKS | `<oauthServerUrl>/publickeys` |
{: caption="Table 1. Examples of endpoints" caption-side="top"}

When you use the SDK, the endpoint URLs are built automatically.
{: note}

## Tokens
{: #term-token}

The service uses three different types of tokens. Tokens are set in the **Identity Providers > Manage** of the {{site.data.keyword.appid_short_notm}} dashboard. For more information about tokens and how they're used in {{site.data.keyword.appid_short_notm}}, check out [Managing tokens](/docs/appid?topic=appid-tokens).

* Access tokens: Represent authorization and enable communication with protected [backend resources](/docs/appid?topic=appid-backend). The resources are protected by authorization filters that are set by {{site.data.keyword.appid_short_notm}}.

* Identity tokens: Represent authentication and contain information about the user.

* Refresh tokens: Can be used to obtain a new access token without reauthenticating the user. By using refresh tokens, users can allow their information to be remembered by the application, which means that they can stay signed in. 

## Authorization headers
{: #term-auth-header}

{{site.data.keyword.appid_short_notm}} complies with the [Bearer token specification](https://datatracker.ietf.org/doc/html/rfc6750){: external} and uses a combination of access and identity tokens that are sent as an HTTP Authorization header. The Authorization header has three different parts that are separated by white space. The tokens are base64 encoded. The identity token is optional.

Example:

```sh
Authorization=Bearer <accessToken> [<idToken>]
```
{: screen}


## API Strategy
{: #term-api-strategy}

The API strategy expects requests to contain an authorization header with a valid access token. The request can also include an identity token, but it is not required. If a token is invalid or expired, the API strategy returns an HTTP 401 error that contains the following HTTP header:
```sh
Www-Authenticate=Bearer scope="<scope>" error="<error>"
```
{: screen}

If the request returns a valid token, control is passed to the next middleware and the `appIdAuthorizationContext` property is injected into the request object. This property contains original access and identity tokens, and decoded payload information as plain JSON objects.

## Web app strategy
{: #term-web-strategy}

When the web app strategy detects unauthorized attempts to access a protected resource, it automatically redirects a user's browser to the authentication page, which can be provided by {{site.data.keyword.appid_short_notm}}. After successful authentication, the user is returned to the web app's callback URL. The web app strategy obtains access and identity tokens and stores them in an HTTP session under `WebAppStrategy.AUTH_CONTEXT`. It is up to the user to decide whether to store access and identity tokens in the app database.


## Redirect URIs
{: #term-redirect}

{{site.data.keyword.appid_short_notm}} uses a list of fully qualified, approved URIs to redirect your users after an interaction with your app. For example, if the user successfully signs in, {{site.data.keyword.appid_short_notm}} redirects the user to the home page of your app or to another page that you specify. The format of your URI might change depending on your application. Check out [Adding redirect URIs](/docs/appid?topic=appid-managing-idp#add-redirect-uri) for more information.


## JSON Web Key Set (JWKS)
{: #term-jwks}

A JWKS represents a set of cryptographic keys. {{site.data.keyword.appid_short_notm}} uses a JWKS to verify the authenticity of the tokens that are generated by the service. By using the key ID to verify the signature, we can ensure that the token was issued by a trusted source - {{site.data.keyword.appid_short_notm}}. We can also ensure that the information within the token was never changed.

