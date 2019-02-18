---

copyright:
  years: 2017, 2019
lastupdated: "2019-02-18"

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
    <dd><a href="https://tools.ietf.org/html/rfc6749" target="_blank">OAuth 2 <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> is open standard protocol that is used to provide app authorization.</dd>
  <dt>Open ID Connect (OIDC)</dt>
    <dd><p><a href="http://openid.net/developers/specs/" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> is an authentication layer that works on top of OAuth 2.</p>
    <p>When you use OIDC and {{site.data.keyword.appid_short_notm}} together, your service credentials help to configure your OAuth endpoints. When you use the SDK the endpoint URLs are built automatically. But, you can also build the URLs yourself by using your service credentials.</p> <p>The URL takes the following form: appidServiceEndpoint + "/oauth/v3" + /tenantID.</p>
    <p><pre class="codeblock">
    <code>{
      "appidServiceEndpoint": "https://us-south.appid.cloud.ibm.com",
      "clientId": "e8ac1132-5151-4d8a-934e-0141de8e2b34",
      "secret": "XYZ5ZYXzXYZtNyz5Yi00YzQ2LXYwMZctXyM5ODA4NjFhYxYZ",
      "tenantId": "3x176051-a23x-40y4-9645-804943z660q0",
      "version": 3,
    }</code></pre></p>
    <p>Using this example, the URL would be "https://us-south.appid.cloud.ibm.com/oauth/v3/3x176051-a23x-40y4-9645-804943z660q0. You would then append the endpoint that you wanted to make a request to. Check out the following table to see some example endpoints.</p>
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
    <dd>The service uses three different types of tokens. Access tokens represent authorization and enable communication with [back-end resources](/docs/services/appid/backend-apps.html) that are protected by authorization filters that are set by {{site.data.keyword.appid_short}}. Identity tokens represent authentication and contain information about the user. A refresh token can be used to obtain a new access token without re-authenticating the user. By using refresh tokens, users can allow their information to be remembered by the application. This way they can remain signed in. Tokens are set in the <em>Identity Providers > Manage</em> of the {{site.data.keyword.appid_short}} dashboard. For more information about tokens and how they're used in {{site.data.keyword.appid_short}}, check out [Managing tokens](/docs/services/appid/manageidp.html).
  </dd>
  <dt>Authorization headers</dt>
    <dd><p>{{site.data.keyword.appid_short}} complies with the <a href="https://tools.ietf.org/html/rfc6750" target="blank">token bearer specification <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> and uses a combination of access and identity tokens that are sent as an HTTP Authorization header. The Authorization header contains three different parts that are separated by white space. The tokens are base64 encoded. The identity token is optional.</br>
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
  <dt>Redirect URIs</dt>
    <dd><p>There are three types of uniform resources that you can use when defining parts of a web address: URI, URL, and URN. A URN is a very specific and must be unique. A URL is a fully qualified link that locates a specific URN. A URI is an identifier. This means that a URI can also be a URN or URL. However, not all URIs are a URN or URL.</pr>
    <p>{{site.data.keyword.appid_short_notm}} uses a list of fully qualified, approved URIs to redirect your users after an interaction with your app. For example, if the user successfully signs in, {{site.data.keyword.appid_short_notm}} could redirect the user to the home page of your app. The format of your URI might change depending on your application. Check out [Adding redirect URIs](?topic=appid-managing-idp#add-redirect-uri) for more information.</p></dd>
</dl>


## Understanding tokens
{: #tokens}

When a user is successfully authenticated, the application receives tokens from {{site.data.keyword.appid_short_notm}}. The service uses three main types of tokens to complete the authentication process.
{: shortdesc}


### Access tokens
{: #access}

Access tokens represent authorization and enable communication with [back-end resources](/docs/services/appid/backend-apps.html) that are protected by authorization filters that are set by {{site.data.keyword.appid_short}}. The token conforms to JavaScript Object Signing and Encryption (JOSE) specifications. The token is formatted as <a href="https://jwt.io/introduction/" target="blank">JSON Web Tokens <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> are signed with a JSON Web Key that uses the RS256 algorithm.

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
  }
  ```
  {: screen}

### What are identity tokens
{: #identity}

Identity tokens represent authentication and contain information about the user. It can give you information about their name, email, gender, and location. A token can also return a URL to an image of the user. The token is formatted as <a href="https://jwt.io/introduction/" target="blank">JSON Web Tokens <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> are signed with a JSON Web Key that uses the RS256 algorithm.

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
        "name": "IBMCloudApp",
        "type": "serverapp",
        "software_id": "cb638f8f-e24b-41d3-b770-23be158dd8e6.2b94e6bb-bac4-4455-8712-a43fa804d5cc.a3b87400-f03b-4956-844e-a52103ef26ba",
        "software_version": "1.0.0",
      }
  }
  ```
  {: screen}

Identity tokens only contain partial user information. To see all of the information that is provided by the identity provider, you can use the [/userinfo endpoint](/docs/services/appid/predefined.html#predefined-access-api).

### What are refresh tokens
{: #refresh}

{{site.data.keyword.appid_short}} supports the ability to acquire new access and identity tokens without reauthentication, as defined in <a href="http://openid.net/specs/openid-connect-core-1_0.html#RefreshTokens" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>. A refresh token can be used to renew the access token so a user doesn't have to take any action to sign in, such as providing credentials. Similar to access tokens, refresh tokens contain data allowing {{site.data.keyword.appid_short_notm}} to determine whether you authorized. However, these tokens are opaque.

Refresh tokens are configured to have a longer life span than a regular access token so when an access token expires, the refresh token will still be valid and can be used to renew the access token. {{site.data.keyword.appid_short_notm}}’s refresh tokens can be configured to last 1 to 90 days. To take full advantage of refresh tokens, persist the tokens for their full life span, or until they are renewed. A user cannot directly access resources with just a refresh token, which makes them much safer to persist than an access token. As best practice, refresh tokens should be securely stored by the client that received them and sent only to the authorization server that issued them.

For added convenience, {{site.data.keyword.appid_short_notm}} also renews its refresh token — and its expiration date — when the access token is renewed, allowing the user to remain logged in as long as they are active at some point before the current refresh token expires. On the other hand, if you would like to use refresh tokens yet force the user to log in periodically, your app could only use the refresh tokens returned when the user logs in by entering their credentials. However, we recommend always using the latest refresh token received from App ID, as described by the <a href="https://tools.ietf.org/html/rfc6749#page-47" target="_blank">Oauth specifications <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.


Although these tokens can streamline the login process, your app should not depend on them, as they can be revoked at any time, such as when you believe your refresh tokens have been compromised. If you need to revoke a refresh token, there are two methods of revoking a refresh token. If you have the refresh token, you can revoke it based on <a href="https://tools.ietf.org/html/rfc7009#section-2" target="_blank">RFC7009 <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>. Alternatively, if you have the user ID, you can revoke the refresh token by using <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/" target="_blank">the Management API <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>. For more information about accessing the management API see [managing service access](/docs/services/appid/iam.html#service-access-management).

For examples of working with refresh tokens and how to use them to implement a remember-me functionality, check out the [getting started samples](/docs/services/appid/index.html).


### Where do the tokens come from?
{: #where}

Tokens are issued through the {{site.data.keyword.appid_short_notm}} OAuth Server and are formatted as [JSON Web Tokens (JWT)](https://jwt.io/introduction/). The tokens have been signed with a [JSON Web Key (JWK)](https://tools.ietf.org/html/rfc7517) with the RS256 algorithm.

### What happens to the information that the token contains?
{: #contains}

The access token contains a set of standard JWT claims and a set of {{site.data.keyword.appid_short_notm}} specific claims such as a tenant ID. The identity token contains user specific information. The information in the tokens is stored as claims as part of a [user's profile](/docs/services/appid/user-profile.html).

### How are tokens received?
{: #received}

The tokens are received by your app after a successful authentication. You app can use the tokens to retrieve information about user authorization and authentication. The access token can be used to gain access to protected resources by sending a request to the resource. In the request, the access token is described in the [Bearer authentication scheme](https://tools.ietf.org/html/rfc6750#page-5) scheme. To extract the tokens, your app must parse the header.

Example request:

  ```
  GET /resource HTTP/1.1
  Host: server.example.com
  Authorization: Bearer  mF_9.B5f-4.1JqM mF_9.B5f-4.1JqM
  ```
  {: screen}

### How are tokens set?
{: #set}

Token configurations can be enabled and disabled through the App ID dashboard. For more information about your configuration options, check out [Managing tokens](/docs/services/appid/manageidp.html).
