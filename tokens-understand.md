---

copyright:
  years: 2017, 2021
lastupdated: "2021-10-12"

keywords: tokens, refresh token, access token, identity token, configuration, authorization, authentication, app security, access, identity, refresh

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


# Tokens
{: #tokens}

When a user is successfully authenticated, the application receives tokens from {{site.data.keyword.appid_short_notm}}. The service uses three main types of tokens to complete the authentication process.
{: shortdesc}


## Access tokens
{: #access}

Access tokens represent authorization and enable communication with [back-end resources](/docs/appid?topic=appid-backend) that are protected by authorization filters that are set by {{site.data.keyword.appid_short_notm}}. The token conforms to JavaScript Object Signing and Encryption (JOSE) specifications. The token is formatted as [JSON Web Tokens](https://jwt.io/introduction/){: external} are signed with a JSON Web Key that uses the RS256 algorithm.


Example token:
   ```json
   Header:
   {
      "alg": "RS256",
      "typ": "JWT",
      "kid": "appId-39a37f57-a227-4bfe-a044-93b6e6050a61-2018-08-02T11:57:43.401",
      "ver": 4
   }
   Payload:
   {
      "iss": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61",
      "exp": 1551903163,
      "aud": [
      "968c2306-9aef-4109-bc06-4f5ed6axi24a"
      ],
      "sub": "2b96cc04-eca5-4122-a8de-6e07d14c13a5",
      "email_verified": true,
      "amr": [
      "cloud_directory"
      ],
      "iat": 1551899553,
      "tenant": "39a37f57-a227-4bfe-a044-93b6e6050a61",
      "scope": "openid appid_default appid_readprofile appid_readuserattr appid_writeuserattr appid_authenticated"
   }
   ```
   {: screen}

## Identity tokens
{: #identity}

Identity tokens represent authentication and contain information about the user. It can give you information about their name, email, gender, and location. A token can also return a URL to an image of the user. The token is formatted as [JSON Web Tokens](https://jwt.io/introduction/){: external} are signed with a JSON Web Key that uses the RS256 algorithm.


Example token:
   ```json
   Header:
   {
      "alg": "RS256",
      "typ": "JWT",
      "kid": "appId-39a37f57-a227-4bfe-a044-93b6e6050a61-2018-08-02T11:57:43.401",
      "ver": 4
   }
   Payload:
   {
      "iss": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61",
      "aud": [
      "968c2306-9aef-4109-bc06-4f5ed6axi24a"
      ],
      "exp": 1551903163,
      "tenant": "39a37f57-a227-4bfe-a044-93b6e6050a61",
      "iat": 1551899553,
      "email": "appid155@mailinator.com",
      "name": "appid155@mailinator.com",
      "sub": "2b96cc04-eca5-4122-a8de-6e07d14c13a5",
      "email_verified": true,
      "identities": [
      {
         "provider": "cloud_directory",
         "id": "118c0278-3526-4954-876b-cf70eb88efa2"
      }
      ],
      "amr": [
      "cloud_directory"
      ]
   }
   ```
   {: screen}


Identity tokens only contain partial user information. To see all of the information that is provided by the identity provider, you can use the [/userinfo endpoint](/docs/appid?topic=appid-profiles#profile-predefined-access).

## Refresh tokens
{: #refresh}

{{site.data.keyword.appid_short_notm}} supports the ability to acquire new access and identity tokens without reauthentication, as defined in [OIDC](https://openid.net/specs/openid-connect-core-1_0.html#RefreshTokens){: external}. A refresh token can be used to renew the access token so a user doesn't have to take any action to sign in, such as providing credentials. Similar to access tokens, refresh tokens contain data allowing {{site.data.keyword.appid_short_notm}} to determine whether you authorized. However, these tokens are opaque.

Refresh tokens are configured to have a longer life span than a regular access token so when an access token expires, the refresh token will still be valid and can be used to renew the access token. {{site.data.keyword.appid_short_notm}}’s refresh tokens can be configured to last 1 to 90 days. To take full advantage of refresh tokens, persist the tokens for their full life span, or until they are renewed. A user cannot directly access resources with just a refresh token, which makes them much safer to persist than an access token. As best practice, refresh tokens should be securely stored by the client that received them and sent only to the authorization server that issued them.

For added convenience, {{site.data.keyword.appid_short_notm}} also renews its refresh token — and its expiration date — when the access token is renewed, allowing the user to remain logged in as long as they are active at some point before the current refresh token expires. On the other hand, if you would like to use refresh tokens yet force the user to log in periodically, your app could only use the refresh tokens returned when the user logs in by entering their credentials. However, we recommend always using the latest refresh token received from {{site.data.keyword.appid_short_notm}}, as described by the [OAuth 2.0 specifications](https://datatracker.ietf.org/doc/html/rfc6749.){: external}.


Although these tokens can streamline the login process, your app should not depend on them, as they can be revoked at any time, such as when you believe your refresh tokens have been compromised. If you need to revoke a refresh token, there are two methods of revoking a refresh token. If you have the refresh token, you can revoke it based on [RFC7009](https://datatracker.ietf.org/doc/html/rfc7009#section-2){: external}. Alternatively, if you have the user ID, you can revoke the refresh token by using [the Management API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/){: external}. For more information about accessing the management API see [managing service access](/docs/appid?topic=appid-service-access-management#service-access-management).


For examples of working with refresh tokens and how to use them to implement a remember-me functionality, check out the [getting started samples](/docs/appid?topic=appid-getting-started#getting-started).


## Where do the tokens come from?
{: #where}

Tokens are issued through the {{site.data.keyword.appid_short_notm}} OAuth Server and are formatted as [JSON Web Tokens (JWT)](https://jwt.io/introduction/){: external}. The tokens have been signed with a [JSON Web Key (JWK)](https://datatracker.ietf.org/doc/html/rfc7517){: external} with the RS256 algorithm.

## What happens to the information that the token contains?
{: #contains}

The access token contains a set of standard JWT claims and a set of {{site.data.keyword.appid_short_notm}} specific claims such as a tenant ID. The identity token contains user specific information. The information in the tokens is stored as claims as part of a [user's profile](/docs/appid?topic=appid-profiles).

## How are tokens received?
{: #received}

The tokens are received by your app after a successful authentication. You app can use the tokens to retrieve information about user authorization and authentication. The access token can be used to gain access to protected resources by sending a request to the resource. To extract the tokens, your app must parse the header.

Example request:

   ```sh
   GET /resource HTTP/1.1
   Host: server.example.com
   Authorization: Bearer  mF_9.B5f-4.1JqM mF_9.B5f-4.1JqM
   ```
   {: screen}

## How are tokens configured?
{: #set}

You can customize tokens by using custom claims mapping. For more information, see [Customizing tokens](/docs/appid?topic=appid-customizing-tokens).
