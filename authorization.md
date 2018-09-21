---

copyright:
  years: 2017, 2018
lastupdated: "2018-09-21"

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





