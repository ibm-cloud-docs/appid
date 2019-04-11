---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-11"

keywords: authentication, authorization, identity, app security, secure, access, tokens

subcollection: appid

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}



# Understanding tokens
{: #tokens}

When a user is successfully authenticated, the application receives tokens from {{site.data.keyword.appid_short_notm}}. The service uses three main types of tokens to complete the authentication process.
{: shortdesc}


## Access tokens
{: #access}

Access tokens represent authorization and enable communication with [back-end resources](/docs/services/appid?topic=appid-backend) that are protected by authorization filters that are set by {{site.data.keyword.appid_short}}. The token conforms to JavaScript Object Signing and Encryption (JOSE) specifications. The token is formatted as <a href="https://jwt.io/introduction/" target="blank">JSON Web Tokens <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> are signed with a JSON Web Key that uses the RS256 algorithm.

Example token:
  ```
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

## What are identity tokens?
{: #identity}

Identity tokens represent authentication and contain information about the user. It can give you information about their name, email, gender, and location. A token can also return a URL to an image of the user. The token is formatted as <a href="https://jwt.io/introduction/" target="blank">JSON Web Tokens <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> are signed with a JSON Web Key that uses the RS256 algorithm.

Example token:
  ```
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


Identity tokens only contain partial user information. To see all of the information that is provided by the identity provider, you can use the [/userinfo endpoint](/docs/services/appid?topic=appid-predefined-attributes#predefined-access-api).

## What are refresh tokens?
{: #refresh}

{{site.data.keyword.appid_short}} supports the ability to acquire new access and identity tokens without reauthentication, as defined in <a href="http://openid.net/specs/openid-connect-core-1_0.html#RefreshTokens" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>. A refresh token can be used to renew the access token so a user doesn't have to take any action to sign in, such as providing credentials. Similar to access tokens, refresh tokens contain data allowing {{site.data.keyword.appid_short_notm}} to determine whether you authorized. However, these tokens are opaque.

Refresh tokens are configured to have a longer life span than a regular access token so when an access token expires, the refresh token will still be valid and can be used to renew the access token. {{site.data.keyword.appid_short_notm}}’s refresh tokens can be configured to last 1 to 90 days. To take full advantage of refresh tokens, persist the tokens for their full life span, or until they are renewed. A user cannot directly access resources with just a refresh token, which makes them much safer to persist than an access token. As best practice, refresh tokens should be securely stored by the client that received them and sent only to the authorization server that issued them.

For added convenience, {{site.data.keyword.appid_short_notm}} also renews its refresh token — and its expiration date — when the access token is renewed, allowing the user to remain logged in as long as they are active at some point before the current refresh token expires. On the other hand, if you would like to use refresh tokens yet force the user to log in periodically, your app could only use the refresh tokens returned when the user logs in by entering their credentials. However, we recommend always using the latest refresh token received from {{site.data.keyword.appid_short_notm}}, as described by the <a href="https://tools.ietf.org/html/rfc6749#page-47" target="_blank">OAuth 2.0 specifications <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.


Although these tokens can streamline the login process, your app should not depend on them, as they can be revoked at any time, such as when you believe your refresh tokens have been compromised. If you need to revoke a refresh token, there are two methods of revoking a refresh token. If you have the refresh token, you can revoke it based on <a href="https://tools.ietf.org/html/rfc7009#section-2" target="_blank">RFC7009 <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>. Alternatively, if you have the user ID, you can revoke the refresh token by using <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/" target="_blank">the Management API <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>. For more information about accessing the management API see [managing service access](/docs/services/appid?topic=appid-service-access-management#service-access-management).

For examples of working with refresh tokens and how to use them to implement a remember-me functionality, check out the [getting started samples](/docs/services/appid?topic=appid-getting-started#getting-started).


## Where do the tokens come from?
{: #where}

Tokens are issued through the {{site.data.keyword.appid_short_notm}} OAuth Server and are formatted as [JSON Web Tokens (JWT)](https://jwt.io/introduction/). The tokens have been signed with a [JSON Web Key (JWK)](https://tools.ietf.org/html/rfc7517) with the RS256 algorithm.

## What happens to the information that the token contains?
{: #contains}

The access token contains a set of standard JWT claims and a set of {{site.data.keyword.appid_short_notm}} specific claims such as a tenant ID. The identity token contains user specific information. The information in the tokens is stored as claims as part of a [user's profile](/docs/services/appid?topic=appid-user-profile#user-profile).

## How are tokens received?
{: #received}

The tokens are received by your app after a successful authentication. You app can use the tokens to retrieve information about user authorization and authentication. The access token can be used to gain access to protected resources by sending a request to the resource. In the request, the access token is described in the [Bearer authentication scheme](https://tools.ietf.org/html/rfc6750#page-5). To extract the tokens, your app must parse the header.

Example request:

  ```
  GET /resource HTTP/1.1
  Host: server.example.com
  Authorization: Bearer  mF_9.B5f-4.1JqM mF_9.B5f-4.1JqM
  ```
  {: screen}

## How are tokens set?
{: #set}

Token configurations can be enabled and disabled through the {{site.data.keyword.appid_short_notm}} dashboard. For more information about your configuration options, check out [Managing tokens](/docs/services/appid?topic=appid-managing-idp#managing-idp).
