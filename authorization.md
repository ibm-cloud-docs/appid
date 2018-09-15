---

copyright:
  years: 2017, 2018
lastupdated: "2018-09-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}




# Key concepts
{: #key-concepts}

Confused about the differences between authorization and authentication? You're not alone. Check out the information on this page to learn about specific terminology, processes, and the way that the service uses tokens.
{: shortdesc}


## Terminology
{: #terms}


These key terms can help you understand the way that the service breaks down the authorization and authentication process.

<dl>
  <dt>OAuth 2</dt>
    <dd><a href="https://tools.ietf.org/html/rfc6749" target="_">OAuth 2 <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> is open standard protocol that is used to provide app authorization.</dd>
  <dt>Open ID Connect (OIDC)</dt>
    <dd><p><a href="http://openid.net/developers/specs/" target="_">OIDC <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> is an authentication layer that works on top of OAuth 2.</p>
    <p>When you use OIDC and {{site.data.keyword.appid_short_notm}} together, your service credentials help to configure your OAuth endpoints. When you use the SDK the endpoint URLs are built automatically. But, you can also build the URLs yourself by using your service credentials. You can see how to put together the URL in the following example and table.</p>
    <pre class="codeblock">
    <code>{
      "version": 3,
      "clientId": "e8ac1132-5151-4d8a-934e-0141de8e2b34",
      "secret": "XYZ5ZYXzXYZtNyz5Yi00YzQ2LXYwMZctXyM5ODA4NjFhYxYZ",
      "tenantId": "3x176051-a23x-40y4-9645-804943z660q0",
      "oauthServerUrl": "https://appid-oauth.ng.bluemix.net/oauth/v3/3x176051-a23x-40y4-9645-804943z660q0",
      "profilesUrl": "https://appid-profiles.ng.bluemix.net/"
    }</code></pre>
    <table>
      <tr>
        <th>Endpoint</th>
        <th>Format</th>
      </tr>
      <tr>
        <td>Authorization</td>
        <td>{oauthServerUrl}/authorization</td>
      </tr>
      <tr>
        <td>Token</td>
        <td>{oauthServerUrl}/token</td>
      </tr>
      <tr>
        <td>Userinfo</td>
        <td>{oauthServerUrl}/userinfo</td>
      </tr>
      <tr>
        <td>JWKS</td>
        <td>{oauthServerUrl}/publickeys</td>
      </tr>
    </table>
    <p><strong>Note</strong>: When you use the SDK the endpoint URLs are built automatically.</p></dd>
  <dt>Tokens</dt>
    <dd>The service uses three different types of tokens. Access tokens represent authorization and enable communication with [back-end resources](/docs/services/appid/protecting-resources.html) that are protected by authorization filters that are set by {{site.data.keyword.appid_short}}. Identity tokens represent authentication and contain information about the user. A refresh token can be used to obtain a new access token without re-authenticating the user. By using refresh tokens, users can allow their information to be remembered by the application. This way they can remain signed in. For more information about tokens and how they're used in {{site.data.keyword.appid_short}}, check out [Validating tokens](#tokens).
  </dd>
  <dt>Authorization headers</dt>
    <dd><p>{{site.data.keyword.appid_short}} complies with the <a href="https://tools.ietf.org/html/rfc6750" target="Because each identity provider returns its own unique set of [standardized](http://openid.net/specs/openid-connect-core-1_0.html#StandardClaims) claims. {{site.data.keyword.appid_short_notm}} automatically normalizes common properties that are passed into the identity token to create normalized claims.">token bearer specification <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> and uses a combination of access and identity tokens that are sent as an HTTP Authorization header. The Authorization header contains three different parts that are separated by white space. The tokens are base64 encoded. The identity token is optional.</br>
    Example:</p>
    <pre><code>Authorization=Bearer {access_token} [{id_token}]</pre></code></dd>
  <dt>API Strategy</dt>
    <dd><p>The API strategy expects requests to contain an authorization header with a valid access token. The request can also include an identity token, but it is not required. If a token is invalid or expired, the API strategy returns an HTTP 401 error that contains the following HTTP header:</p> <pre><code>Www-Authenticate=Bearer scope="{scope}" error="{error}"</code></pre>
    <p>If the request returns a valid token, control is passed to the next middleware and the <code>appIdAuthorizationContext</code> property is injected into the request object. This property contains original access and identity tokens, and decoded payload information as plain JSON objects.</dd>
  <dt>Web app strategy</dt>
    <dd>When the web app strategy detects unauthorized attempts to access a protected resource, it automatically redirects a user's browser to the authentication page, which can be provided by {{site.data.keyword.appid_short}}. After successful authentication, the user is returned to the web app's callback URL. The web app strategy obtains access and identity tokens and stores them in an HTTP session under <code>WebAppStrategy.AUTH_CONTEXT</code>. It is up to the user to decide whether to store access and identity tokens in the app database.</dd>
  <dt>Data separation and encryption</dt>
    <dd><p>{{site.data.keyword.appid_short_notm}} stores and encrypts user profile attributes. As a multi-tenant service, every tenant has a designated encryption key and user data in each tenant is encrypted with only that tenant's key.</p>
    <p>{{site.data.keyword.appid_short_notm}} ensures that private information is encrypted before it is stored.</p></dd>
</dl>

</br>
</br>


## Understanding tokens
{: #tokens}

When a user is successfully authenticated, the application receives tokens from {{site.data.keyword.appid_short_notm}}. The service uses three main types of tokens to complete the authentication process.
{: shortdesc}


**What is an access token?**

Access tokens represent authorization and enable communication with [back-end resources](/docs/services/appid/protecting-resources.html) that are protected by authorization filters that are set by {{site.data.keyword.appid_short}}. The token conforms to JavaScript Object Signing and Encryption (JOSE) specifications. The token is formatted as <a href="https://jwt.io/introduction/" target="Because each identity provider returns its own unique set of [standardized](http://openid.net/specs/openid-connect-core-1_0.html#StandardClaims) claims. {{site.data.keyword.appid_short_notm}} automatically normalizes common properties that are passed into the identity token to create normalized claims.">JSON Web Tokens <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> are signed with a JSON Web Key that uses the RS256 algorithm.

Example token:
  ```
  Header: {
      "typ": "JOSE",
      "alg": "RS256",
  }
  Payload: {
      "iss": "appid-oauth.ng.bluemix.net",
      "exp": "1495562664",
      "aud": "a3b87400-f03b-4956-844e-a52103ef26ba",
      "amr": ["facebook"],
      "sub": "de6a17d2-693d-4a43-8ea2-2140afd56a22",
      "iat": "1495559064",
      "tenant": "9781974b-6a1c-46c3-aebf-32b7e9bbbaee",
      "scope": "appid_default appid_readprofile appid_readuserattr appid_writeuserattr",
  ```
  {: screen}

**What is an identity token?**

Identity tokens represent authentication and contain information about the user. It can give you information about their name, email, gender, and location. A token can also return a URL to an image of the user. The token is formatted as <a href="https://jwt.io/introduction/" target="Because each identity provider returns its own unique set of [standardized](http://openid.net/specs/openid-connect-core-1_0.html#StandardClaims) claims. {{site.data.keyword.appid_short_notm}} automatically normalizes common properties that are passed into the identity token to create normalized claims.">JSON Web Tokens <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> are signed with a JSON Web Key that uses the RS256 algorithm.

Example token:
  ```
  Header: {
      "typ": "JOSE",
      "alg": "RS256",
  }
  Payload: {
      "iss": "appid-oauth.ng.bluemix.net",
      "aud": "a3b87400-f03b-4956-844e-a52103ef26ba",
      "exp: "1495562664",
      "tenant": "9781974b-6a1c-46c3-aebf-32b7e9bbbaee",
      "iat": "1495559064",
      "name": "John Smith",
      "email": "js@mail.com",
      "gender", "male",
      "locale": "en",
      "picture": "<URL-to-photo>",
      "sub": "de6a17d2-693d-4a43-8ea2-2140afd56a22",
      "identities": [
          "provider": "facebook"
          "id": "377440159275659"
      ],
      "amr": ["facebook"],
      "oauth_client":{
        "name": "BluemixApp",
        "type": "serverapp",
        "software_id": "cb638f8f-e24b-41d3-b770-23be158dd8e6.2b94e6bb-bac4-4455-8712-a43fa804d5cc.a3b87400-f03b-4956-844e-a52103ef26ba",
        "software_version": "1.0.0",
      }
  }
  ```
  {: screen}

**What is a refresh token?**

{{site.data.keyword.appid_short}} supports the ability to acquire new access and identity tokens without reauthentication, as defined in <a href="http://openid.net/specs/openid-connect-core-1_0.html#RefreshTokens" target="Because each identity provider returns its own unique set of [standardized](http://openid.net/specs/openid-connect-core-1_0.html#StandardClaims) claims. {{site.data.keyword.appid_short_notm}} automatically normalizes common properties that are passed into the identity token to create normalized claims.">OIDC <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>. When signing in with a refresh token, a user doesn't have to take any actions, such as providing credentials. Generally, refresh tokens are configured to have a longer life span than a regular access token. To take full advantage of refresh tokens, persist the tokens for their full life span. A user cannot directly access resources with just a refresh token, which makes them much safer to persist than an access token. For examples of working with refresh tokens and how to use them to implement a *remember me* functionality, check out the getting started samples. As a best practice, refresh tokens should be securely stored by the client that received them, and should only be sent to the authorization server that issued them.

There are some cases when you would want to have the refresh token revoked, for example when its believed to be compromised. There are two methods of revoking a refresh token. If you have the refresh token, you can revoke it based on <a href="https://tools.ietf.org/html/rfc7009#section-2" target="Because each identity provider returns its own unique set of [standardized](http://openid.net/specs/openid-connect-core-1_0.html#StandardClaims) claims. {{site.data.keyword.appid_short_notm}} automatically normalizes common properties that are passed into the identity token to create normalized claims.">RFC7009</a>. Alternatively, if you have the user ID, you can revoke the refresh token by using <a href="https://appid-management.ng.bluemix.net/swagger-ui/" target="Because each identity provider returns its own unique set of [standardized](http://openid.net/specs/openid-connect-core-1_0.html#StandardClaims) claims. {{site.data.keyword.appid_short_notm}} automatically normalizes common properties that are passed into the identity token to create normalized claims.">the Management API</a>. For more information about accessing the management API see [managing service access](/docs/services/appid/iam.html#service-access-management).

Revoking the use of either method revokes all active refresh tokens that are assigned to that user that were created before revocation.
{: tip}

**Where do the tokens come from?**

Tokens are issued through the {{site.data.keyword.appid_short_notm}} OAuth Server and are formatted as [JSON Web Tokens (JWT)](https://jwt.io/introduction/). The tokens have been signed with a [JSON Web Key (JWK)](https://tools.ietf.org/html/rfc7517) with the RS256 algorithm.

**What happens to the information that the token contains?**

The access token contains a set of standard JWT claims and a set of {{site.data.keyword.appid_short_notm}} specific claims such as a tenant ID. The identity token contains user specific information. The information in the tokens is stored as claims as part of a [user's profile](/docs/services/appid/user-profile.html).

**How are tokens received?**

The tokens are received by your app after a successful authentication. You app can use the tokens to retrieve information about user authorization and authentication. The access token can be used to gain access to protected resources by sending a request to the resource. In the request, the access token is described in the [Bearer authentication scheme](https://tools.ietf.org/html/rfc6750#page-5) scheme. To extract the tokens, your app must parse the header.

Example request:

  ```
  GET /resource HTTP/1.1
  Host: server.example.com
  Authorization: Bearer  mF_9.B5f-4.1JqM mF_9.B5f-4.1JqM
  ```
  {: screen}

</br>
</br>

## How authorization and authentication work
{: #authorization}

When coding apps, one of the biggest concerns is security. How can you ensure that only users with the right access, are using your app? You use an authorization process. In most processes authorization and authentication are coupled together, which can make changing your security policies and identity providers complicated. With {{site.data.keyword.appid_short}}, authorization and authentication are separate processes.
{: shortdesc}

When you configure social identity providers such as Facebook, the [Oauth2 Authorization Grant flow](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html) is used to call the login widget. With cloud directory as your identity provider, the [Resource Owner Password Credentials flow](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html) is used to provide access and identity tokens.

![The path to becoming an identified user.](/images/authenticationtrail.png)

When a user chooses to sign in, they become an identified user. The identity provider returns access and identity tokens to {{site.data.keyword.appid_short}} that contain information about the user. The service takes the provided tokens and determines whether a user has the proper credentials to access an app. If the tokens are validated, then the service authorizes the users access. The authentication information is associated with the user's record after they're authorized. The record and its attributes can be accessed again from any client that authenticates with the same identity.

### Progressive authentication

With {{site.data.keyword.appid_short_notm}}, an anonymous user can choose to become an identified user.

When a user chooses not to sign in immediately, they are considered an anonymous user. As an example, a user might immediately start adding items to a shopping cart without signing in. For anonymous users, {{site.data.keyword.appid_short_notm}} creates an ad hoc user record and calls the OAuth login API that returns anonymous access and identity tokens. By using those tokens, the app can create, read, update, and delete the attributes that are stored in the user record.

![The path to becoming an identified user when they start as anonymous.](/images/anon-authenticationtrail.png)

When an anonymous user signs in, their access token is passed to the login API. The service authenticates the call with an identity provider. The service uses the access token to find the anonymous record and attaches the identity to it. The new access and identity tokens contain the public information that is shared by the identity provider. After a user is identified, their anonymous token becomes invalid. However, a user is still able to access their attributes because they're accessible with the new token.

An identity can be assigned to an anonymous record only if it is not already assigned to another user.
{: tip}

If the identity is already associated with another {{site.data.keyword.appid_short_notm}} user, the tokens contain information of that user record and provide access to their attributes. The previous anonymous users attributes are not accessible through the new token. Until the token expires, the information can still be accessed through the anonymous access token. During development, you can choose how to merge the anonymous attributes to the known user.




</li></ul></p></dd>
  <dt>Authorization headers</dt>
    <dd><p>{{site.data.keyword.appid_short}} complies with the <a href="https://tools.ietf.org/html/rfc6750" target="_blank">token bearer specification <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> and uses a combination of access and identity tokens that are sent as an HTTP Authorization header. The Authorization header contains three different parts that are separated by white space. The tokens are base64 encoded. The identity token is optional.</br>
    Example:</p>
    <pre><code>Authorization=Bearer {access_token} [{id_token}]</pre></code></dd>
  <dt>API Strategy</dt>
    <dd><p>The API strategy expects requests to contain an authorization header with a valid access token. The request can also include an identity token, but it is not required. If a token is invalid or expired, the API strategy returns an HTTP 401 error that contains the following HTTP header:</p> <pre><code>Www-Authenticate=Bearer scope="{scope}" error="{error}"</code></pre>
    <p>If the request returns a valid token, control is passed to the next middleware and the <code>appIdAuthorizationContext</code> property is injected into the request object. This property contains original access and identity tokens, and decoded payload information as plain JSON objects.</dd>
  <dt>Web app strategy</dt>
    <dd>When the web app strategy detects unauthorized attempts to access a protected resource, it automatically redirects a user's browser to the authentication page, which can be provided by {{site.data.keyword.appid_short}}. After successful authentication, the user is returned to the web app's callback URL. The web app strategy obtains access and identity tokens and stores them in an HTTP session under <code>WebAppStrategy.AUTH_CONTEXT</code>. It is up to the user to decide whether to store access and identity tokens in the app database.</dd>
  <dt>Data separation and encryption</dt>
    <dd><p>{{site.data.keyword.appid_short_notm}} stores and encrypts user profile attributes. As a multi-tenant service, every tenant has a designated encryption key and user data in each tenant is encrypted with only that tenant's key. {{site.data.keyword.appid_short_notm}} ensures that private information is encrypted before it is stored.</p></dd>
</dl>

</br>
</br>

## Authorization vs authentication
{: #auth}

<dl>
  <dt>Authentication</dt>
    <dd>Authentication is the process of verifying the identity of a user; knowing that the user is who they claim to be.</br> On the web, authentication is about knowing the user at the keyboard is who they say they are. This is usually performed when someone passes a username and password to your application. When a user submits these credentials, they are claiming the user identity represented by the username. Once the application validates the provided password, it then trusts the user's identity claim.</dd>
  <dt>Authorization</dt>
    <dd>Authorization is the process of verifying that a user has the right to perform a particular action, such as accessing a protected resource. This often requires user authentication in order to discern the actual user's permissions.</br> Unlike authentication, authorization only focuses on the permissions a particular entity has and what actions those permission enable them to perform. In your app, authorization occurs after a user has already signed-in when they attempt to access data and services. With {{site.data.keyword.appid_short_notm}}, your app verifies that a user is authorized to access the information before the requested is completed.</dd>
</dl>


## Protocols and specifications
{: #protocols}

OAuth 2 is an open standard protocol that is used to provide authorization for apps. It enables a user to grant temporary access to protected resources on another server without directly passing their credentials to it.

When a grant flow completes successfully, <a href="https://tools.ietf.org/html/rfc6749" target="_blank">OAuth 2 <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> provides an access token. The token then acts as verified credentials by describing the protected actions that a particular entity can make.

To solidify your understanding of OAuth 2, check out the following key terms.

<dl>
  <dt>Oauth credentials</dt>
    <dd><p>Client ID: The unique identifier of a client. Specified as <code>client_id</code> when interacting with the resource server.</p>
    <p>Client secret: The secret that is associated with a specific client ID. Specified as <code>client_secret</code> when interacting with the resource server.</p></dd>

  <dt>Resource owner</dt>
    <dd>Typically, this is the end-user of your app but can also be used to grant access to a protected resource.</dd>

  <dt>Resource server</dt>
    <dd>The server that hosts user-owned resources that are protected by OAuth 2. The server holds the API that you are trying to access.</dd>

  <dt>Client</dt>
    <dd>An app that makes API requests to perform actions on protected resources on behalf of the resource owner that is using the authorization.</dd>

  <dt>Authorization server</dt>
    <dd>The server that authenticates the resource owner and issues access tokens to clients that can be used to access protected resources from the resource server. As an example, {{site.data.keyword.appid_short_notm}} is an OAuth 2 authorization server.</dd>

  <dt>Client profiles</dt>
    <dd><p>Each type of client is different and has different security needs.</p>
    <p><strong>Server-side web app</strong>: The most basic OAuth client is a web app that runs on a server. The web app is accessed by a resource owner or user and the app makes the appropriate API calls by using a server-side programing language. The user has no access to the client secret or any access tokens that were issued by the authorization server.</p>
    <p><strong>Client-side app that runs in a web browser</strong>: An OAuth client that runs in a user's web browser where the client has access to the app code and/or API requests. The apps could could be distributed as JavaScript that is included in a web page, a browser extension, or a plugin. Single-page apps that run Angular or React are also included. In these cases the OAuth 2 credentials are not trusted to be kept confidential from the resource owner. This means that some API providers refuse to issue client secrets for apps that use this profile.</p>
    <p><strong>Native app</strong>: Unlike web apps that run in the browser, these are OAuth clients that are installed by the user onto their device, such as an iPhone or Android app. Because these are client apps, they cannot be trusted to keep credentials secure. However, at the same time, it may not have access to the full capabilities of a web browser.</p></dd>

  <dt>Authorization grant types</dt>
    <dd><p>When implementing OAuth solutions, each client profile must utilize an appropriate protocol flow in order to obtain authorization from the resource owner in a secure manner. Before starting the authorization flow, each client registers with an OAuth 2 authentication server to obtain client credentials that can be used to authenticate future requests that are made to the server. After it is registered, the core OAuth 2 protocol and its extension RFCs define several grant types that can be used to obtain authorization.</p>
    <p><strong>Authorization code</strong>: This grant type is most appropriate for server-side web applications. After the resource owner has authorized access to their data, they are redirected back to the web application with an authorization code as a query parameter in the URL. The client can then exchange this code with the authorization server for an access token. This exchange is done server-to-server and requires both the client_id and client_secret, preventing even the resource owner from obtaining the access token. This grant type also allows for long-lived access to an API by using refresh tokens.</p>
    <p>Used by: Web apps executing on a server and mobile apps</p>
    <p><strong>Resource-owner password</strong>: This grant type enables a resource owner’s username and password to be exchanged for an OAuth access token. It is used for only highly-trusted clients, such as a mobile app written by the API provider. While the user’s password is still exposed to the client, it does not need to be stored on the device. After the initial authentication, only the OAuth token needs to be stored. Because the password is not stored, the user can revoke access to the app without changing the password, and the token is scoped to a limited set of data, so this grant type still provides enhanced security over traditional username/password authentication.</p> <p>Used by: Trusted applications</p>
    <p><strong>Client credentials</strong>: The client credentials grant type allows an application to obtain an access token for resources that are owned by the client or when authorization has been previously arranged with an authorization server. This grant type is appropriate for applications that need to access APIs, such as storage services or databases, on behalf of themselves rather than on behalf of a specific user.</p> <p>Used by: App to app communication</p>
    <p><strong>Implicit Grant</strong>:</p>
    <p>Used by: Single page apps or apps that only run in a web browser</p>
    <p><strong>JWT-Bearer</strong>:</p>
    <p>Used by: Custom authentication flows</p></dd>
</dl>


## OpenID Connect
{: #connect}

OpenID Connect (<a href="http://openid.net/developers/specs/" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>) is an identity protocol layer that extends OAuth 2 by allowing clients to verify an end-user's identity and obtain basic profile information about them. In {{site.data.keyword.appid_short_notm}}, OIDC provides authentication while the underlying OAuth 2 is responsible for the authorization in the form of an access token.

At a high level, OIDC defines a set of scopes and processes that enable resource owners to share identity information about themselves with client applications. Check out the following key terms and explanations to learn more about OIDC.

<dl>
  <dt>Relying party</dt>
    <dd>An OAuth 2 client that relies on an identity provider to authenticate users.</dd>
  <dt>End-user</dt>
    <dd>The entity that the the request for identity information is made for. OAuth 2 calls this entity the resource owner.</dd>
  <dt>Claims</dt>
    <dd>OIDC defines a set of standardized claims, or information about a user, that can be returned by an OIDC service. These claims include fields such as <code>name</code>, <code>email</code>, and <code>locale</code> among others; however, OIDC additionally allows for custom claims to be returned. As an OIDC service, {{site.data.keyword.appid_short_notm}} collects a subset of OIDC claims that are called normalized claims. When available, they are injected into identity tokens by {{site.data.keyword.appid_short_notm}}. All of the other claims can be found from the <code>UserInfo</code> endpoint.</dd>
  <dt>UserInfo Endpoint</dt>
    <dd>The UserInfo Endpoint is an OAuth 2.0 Protected Resource that returns claims about the authenticated end-user. In order to retrieve the claims, a client makes a request to the UserInfo endpoint by using an Access Token that they obtained through OIDC Authentication.</dd>
</dl>

When you use OIDC and {{site.data.keyword.appid_short_notm}} together, your service credentials help to configure your OAuth endpoints. When you use the SDK the endpoint URLs are built automatically. But, you can also build the URLs yourself by using your service credentials. You can see how to put together the URL in the following example and table.

```
{
  "version": 3,
  "clientId": "e8ac1132-5151-4d8a-934e-0141de8e2b34",
  "secret": "XYZ5ZYXzXYZtNyz5Yi00YzQ2LXYwMZctXyM5ODA4NjFhYxYZ",
  "tenantId": "3x176051-a23x-40y4-9645-804943z660q0",
  "oauthServerUrl": "https://appid-oauth.ng.bluemix.net/oauth/v3/3x176051-a23x-40y4-9645-804943z660q0",
  "profilesUrl": "https://appid-profiles.ng.bluemix.net/"
}
```
{: codeblock}

<table>
  <tr>
    <th>Endpoint</th>
    <th>Format</th>
  </tr>
  <tr>
    <td>Authorization</td>
    <td>{oauthServerUrl}/authorization</td>
  </tr>
  <tr>
    <td>Token</td>
    <td>{oauthServerUrl}/token</td>
  </tr>
  <tr>
    <td>Userinfo</td>
    <td>{oauthServerUrl}/userinfo</td>
  </tr>
  <tr>
    <td>JWKS</td>
    <td>{oauthServerUrl}/publickeys</td>
  </tr>
</table>

When you use the SDK, the endpoint URLs are built automatically.
{: tip}


## SAML
{: #about-saml}

SAML (Security Assertion Markup Language) is an open standard for exchanging authentication and authorization data between an identity provider who asserts the user identity and a service provider who consumes the user identity information.
{: shortdesc}

A SAML assertion is a package of information. It contains the authorization decision and might also contain identity information about the user. When a user signs in, the SAML provider sends an assertion to {{site.data.keyword.appid_short_notm}}. {{site.data.keyword.appid_short_notm}} propagates the user identity information from the SAML assertion to your applications through OIDC token claims. The remaining SAML attribute assertions that do not correspond to any of the standard claims are stored in a user profile and can be viewed by using the `/userinfo` endpoint.

In order for a SAML attribute to be included in the identity token it must correspond to one of the following OIDC claims: `name`, `email`, `locale`, `picture`, `role`. If any of the values change in anyway on the provider's side, the new values are available after the user signs in again.


## Understanding tokens
{: #tokens}

When a user is successfully authenticated, the application receives tokens from {{site.data.keyword.appid_short_notm}}. The service uses three main types of tokens to complete the authentication process.
{: shortdesc}


### Access tokens

Access tokens represent authorization and enable communication with [back-end resources](/docs/services/appid/protecting-resources.html) that are protected by authorization filters that are set by {{site.data.keyword.appid_short}}. The token conforms to JavaScript Object Signing and Encryption (JOSE) specifications. The token is formatted as <a href="https://jwt.io/introduction/" target="_blank">JSON Web Tokens <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> are signed with a JSON Web Key that uses the RS256 algorithm.

In general, access tokens have a short lifespan for for improved for improved security. After it is expired, a user must authenticate again. By default, {{site.data.keyword.appid_short_notm}} access tokens expire after an hour; however, this can be configured to meet your app's specific needs. An access token scope field determines the amount and type of privileges that are granted to a particular token. With {{site.data.keyword.appid_short_notm}}, you can enforce that any scope or combination of scopes exists to moderate access to your APIs. By default, {{site.data.keyword.appid_short_notm}} adds several default scopes that provide access to its user profile management capabilities.

Example token:
  ```
  Header: {
      "typ": "JOSE",
      "alg": "RS256",
  }
  Payload: {
      "iss": "appid-oauth.ng.bluemix.net",
      "exp": "1495562664",
      "aud": "a3b87400-f03b-4956-844e-a52103ef26ba",
      "amr": ["facebook"],
      "sub": "de6a17d2-693d-4a43-8ea2-2140afd56a22",
      "iat": "1495559064",
      "tenant": "9781974b-6a1c-46c3-aebf-32b7e9bbbaee",
      "scope": "appid_default appid_readprofile appid_readuserattr appid_writeuserattr",
  ```
  {: screen}

<table>
  <tr>
    <th>Scope</th>
    <th>Definition</th>
  </tr>
  <tr>
    <td><code>openid</code></td>
    <td>Required: Informs the authorization server that the client is making an OIDC request.</td>
  </tr>
  <tr>
    <td><code>appid_readprofile</code></td>
    <td>States that the token is authorized to read the associated {{site.data.keyword.appid_short_notm}} profile.</td>
  </tr>
  <tr>
    <td><code>appid_readuserattr</code></td>
    <td>States that the token is authorized to read the associated {{site.data.keyword.appid_short_notm}} user's attributes.</td>
  </tr>
  <tr>
    <td><code>appid_writeuserattr</code></td>
    <td>States that the token is authorized to modify the associated {{site.data.keyword.appid_short_notm}} user's attributes.</td>
  </tr>
</table>

You can add custom scopes to your tokens by using the {{site.data.keyword.appid_short_notm}} custom identity flow.
{: tip}


### Identity tokens

Identity tokens represent authentication and contain information about the user. It can give you information about a user's name, email, gender, and/or location. A token can also return a URL to an image of the user. The token is formatted as a <a href="https://jwt.io/introduction/" target="_blank">JSON Web Token <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> and are signed with a JSON Web Key that uses the RS256 algorithm. These tokens can be used within your app to customize your user experience and to authenticate users against other servers or apps.

As with access tokens, identity tokens have a short lifespan. By default, {{site.data.keyword.appid_short_notm}} identity tokens expire after an hour; however, this can be configured to meet your app's specific needs.

When an identity token is passed to another API, its expiration date and signature must be verified before its identity claims can be trusted. Because each identity provider returns its own unique set of [standardized](http://openid.net/specs/openid-connect-core-1_0.html#StandardClaims) claims. {{site.data.keyword.appid_short_notm}} automatically normalizes common properties that are passed into the identity token to create normalized claims.

Example token:
  ```
  Header: {
      "typ": "JOSE",
      "alg": "RS256",
  }
  Payload: {
      "iss": "appid-oauth.ng.bluemix.net",
      "aud": "a3b87400-f03b-4956-844e-a52103ef26ba",
      "exp: "1495562664",
      "tenant": "9781974b-6a1c-46c3-aebf-32b7e9bbbaee",
      "iat": "1495559064",
      "name": "John Smith",
      "email": "js@mail.com",
      "gender", "male",
      "locale": "en",
      "picture": "<URL-to-photo>",
      "sub": "de6a17d2-693d-4a43-8ea2-2140afd56a22",
      "identities": [
          "provider": "facebook"
          "id": "377440159275659"
      ],
      "amr": ["facebook"],
      "oauth_client":{
        "name": "BluemixApp",
        "type": "serverapp",
        "software_id": "cb638f8f-e24b-41d3-b770-23be158dd8e6.2b94e6bb-bac4-4455-8712-a43fa804d5cc.a3b87400-f03b-4956-844e-a52103ef26ba",
        "software_version": "1.0.0",
      }
  }
  ```
  {: screen}

<table>
  <tr>
    <th>Claim</th>
    <th>Definition</th>
  </tr>
  <tr>
    <td><code>name</code></td>
    <td>The user's full name.</td>
  </tr>
  <tr>
    <td><code>email</code></td>
    <td>The user's email address</td>
  </tr>
  <tr>
    <td><code>picture</code></td>
    <td>The URL of the user's picture.</td>
  </tr>
  <tr>
    <td><code>gender</code></td>
    <td>The user's gender.</td>
  </tr>
  <tr>
    <td><code>locale</code></td>
    <td>The language that the user speaks.</td>
  </tr>
  <tr>
    <td><code>gender</code></td>
    <td>The roles or groups that the user has.</td>
  </tr>
</table>

### Refresh tokens

{{site.data.keyword.appid_short}} supports the ability to acquire new access and identity tokens without reauthentication, as defined in <a href="http://openid.net/specs/openid-connect-core-1_0.html#RefreshTokens" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>. When signing in with a refresh token, a user doesn't have to take any actions, such as providing credentials. Generally, refresh tokens are configured to have a longer life span than a regular access token. To take full advantage of refresh tokens, persist the tokens for their full life span.By default, refresh tokens expire after 30 days. However, this can be configured to meet your app's specific needs.

A user cannot directly access resources with just a refresh token, which makes them much safer to persist than an access token. For examples of working with refresh tokens and how to use them to implement a *remember me* functionality, check out the getting started samples. As a best practice, refresh tokens should be securely stored by the client that received them, and should only be sent to the authorization server that issued them.

There are some cases when you would want to have the refresh token revoked, for example when its believed to be compromised. There are two methods of revoking a refresh token. If you have the refresh token, you can revoke it based on <a href="https://tools.ietf.org/html/rfc7009#section-2" target="_blank">RFC7009</a>. Alternatively, if you have the user ID, you can revoke the refresh token by using <a href="https://appid-management.ng.bluemix.net/swagger-ui/" target="_blank">the Management API</a>. For more information about accessing the management API see [managing service access](/docs/services/appid/iam.html#service-access-management).

Revoking the use of either method revokes all active refresh tokens that are assigned to that user that were created before revocation.
{: tip}

### General token information

**Where do the tokens come from?**

Tokens are issued through the {{site.data.keyword.appid_short_notm}} OAuth Server and are formatted as [JSON Web Tokens (JWT)](https://jwt.io/introduction/). The tokens have been signed with a [JSON Web Key (JWK)](https://tools.ietf.org/html/rfc7517) with the RS256 algorithm.

**What happens to the information that the token contains?**

The access token contains a set of standard JWT claims and a set of {{site.data.keyword.appid_short_notm}} specific claims such as a tenant ID. The identity token contains user specific information. The information in the tokens is stored as claims as part of a [user's profile](/docs/services/appid/user-profile.html).

**How are tokens received?**

The tokens are received by your app after a successful authentication. You app can use the tokens to retrieve information about user authorization and authentication. The access token can be used to gain access to protected resources by sending a request to the resource. In the request, the access token is described in the [Bearer authentication scheme](https://tools.ietf.org/html/rfc6750#page-5) scheme. To extract the tokens, your app must parse the header.

Example request:

```
GET /resource HTTP/1.1
Host: server.example.com
Authorization: Bearer  mF_9.B5f-4.1JqM mF_9.B5f-4.1JqM
```
{: screen}

</br>
</br>


## {{site.data.keyword.appid_short_notm}} components
{: #about-components}

### Login widget

{{site.data.keyword.appid_short_notm}} provides a login widget that lets you give your users secure sign in options through a browser interface.

When your app is configured to use an identity provider, visitors to your app are directed to a sign in screen called the login widget. By default, when only one provider is set to on, visitors to your app are redirected to that identity providers authentication screen directly. With the login widget you can display a default sign in screen, or with Cloud Directory, you can reuse your existing UIs.

You can update your sign in flow at any time without changing your source code in any way!
{: tip}

When multiple identity providers are configured, the login widget is called after initiating the OAuth 2 authorization grant flow. If you are using your own UI screens through Cloud Directory, you use the [Resource Owner Password Credentials flow](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html) to sign in and gain access and identity tokens.


### Management vs runtime APIs
{: #about-apis}

To promote a secure separation or roles for project management and developers, {{site.data.keyword.appid_short_notm}} divides its APIs into 2 categories differentiated by the accounts with permission to make the request.

**Runtime**

The [Runtime APIs](https://appid-oauth.ng.bluemix.net/swagger-ui/#/Authorization_Server_V3) contain all of the endpoints necessary for a specific client app to use an {{site.data.keyword.appid_short_notm}} instance during app execution. This includes all of the supported endpoints defined by OAuth 2 and OIDC. Each Runtime API is protected with either the clients specific `client id` and `secret` as part of a basic authorization header or an {{site.data.keyword.appid_short_notm}} access token.

For example:

```
Authorization: Basic clientId + ":" + secret
```
{: screen}

**Management**

For customizing and managing your {{site.data.keyword.appid_short_notm}} instances, you can leverage the {{site.data.keyword.appid_short_notm}} [Management APIs](https://appid-management.ng.bluemix.net/swagger-ui/).

Unlike the runtime APIs the management APIs are secured with IBM Cloud Identity and Access Management (IAM). As a platform level access management system, IAM enables you to securely authenticate and control access for users to platform services and resources across the IBM Cloud platform.

As an account owner, you can set policies within your account to create different levels of access for different users. For example, certain users can have read only access to one instance, but write access to another. You can decide who is allowed to create, update, and delete instances of {{site.data.keyword.appid_short_notm}}.

With the management APIs you can configure identity providers, manage instances of {{site.data.keyword.appid_short_notm}}, manage cloud directory users, customize your UI, and more.

</staging>
