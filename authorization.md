---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-01"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Authorization and authentication
{: authorization}

With {{site.data.keyword.appid_full}}, users can leverage tokens and authorization filters to ensure their apps are protected. Before a user can grant authorization, their identity must be authenticated by an identity provider.
{: shortdesc}


## Key concepts
{: key-concepts}

In order to truly understand the way that the service breaks down the authorization and authentication process, you'll need to have an understanding of some key terms.

<dl>
  <dt>OAuth 2</dt>
    <dd><a href="https://tools.ietf.org/html/rfc6749" target="_blank">OAuth 2 <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> is open standard protocol that is used to provide app authorization.</dd>
  <dt>Open ID Connect (OIDC)</dt>
    <dd><a href="http://openid.net/developers/specs/" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> is an authentication layer that works on top of OAuth 2.</dd>
  <dt>Access tokens</dt>
    <dd><p>Access tokens represent authorization and enable communication with with [back-end resources](/docs/services/appid/protecting-resources.html) that are protected by authorization filters that are set by {{site.data.keyword.appid_short}}. The token conforms to JavaScript Object Signing and Encryption (JOSE) specifications. The tokens are formatted as <a href="https://jwt.io/introduction/" target="blank">JSON Web Tokens <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.</br>
    Example:</p>
    <pre><code>Header: {
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
    </code></pre></dd>
  <dt>Identity tokens</dt>
    <dd><p>Identity tokens represent authentication and contain information about the user. It can give you information about their name, email, gender, and location. A token can also return a URL to an image of the user.</br>
    Example:</p>
    <pre><code>Header: {
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
        "picture": "https://url.to.photo",
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
    </pre></code></dd>
  <dt>Authorization headers</dt>
    <dd><p>{{site.data.keyword.appid_short}} complies with the <a href="https://tools.ietf.org/html/rfc6750" target="blank">token bearer specification <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> and uses a combination of access and identity tokens that are sent as an HTTP Authorization header. The Authorization header contains three different parts that are separated by white space. The tokens are base64 encoded. The identity token is optional.</br>
    Example:</p>
    <pre><code>Authorization=Bearer {access_token} [{id_token}]</pre></code></dd>
  <dt>API Strategy</dt>
    <dd><p>The API strategy expects requests to contain an authorization header with a valid access token. The request can also include an identity token, but it is not required. If a token is invalid or expired, the API strategy returns an HTTP 401 error that contains the following HTTP header:</p> <pre><code>Www-Authenticate=Bearer scope="{scope}" error="{error}"</code></pre>
    <p>If the request returns a valid token, control is passed to the next middleware and the <code>appIdAuthorizationContext</code> property is injected into the request object. This property contains original access and identity tokens, and decoded payload information as plain JSON objects.</dd>
  <dt>Web app strategy</dt>
    <dd>When the web app strategy detects unauthorized attempts to access a protected resource, it automatically redirects a user's browser to the authentication page, which can be provided by {{site.data.keyword.appid_short}}. After successful authentication, the user is returned to the web app's callback URL. The web app strategy obtains access and identity tokens and stores them in an HTTP session under <code>WebAppStrategy.AUTH_CONTEXT</code>. It is up to the user to decide whether to store access and identity tokens in the app database.</dd>
</dl>

</br>

## How the process works
{: #process}

When coding apps, one of the biggest concerns is security. How can you ensure that only those with the right access, are using your app? You use an authorization process. In most applications, the authorization and authentication process is coupled together; making changes to your security policies and identity providers complicated. With {{site.data.keyword.appid_short}}, authorization and authentication are separate processes.
{: shortdesc}

When you configure social identity providers such as Facebook, the [Oauth2 Authorization Grant flow](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html) is used to call the login widget. With cloud directory as your identity provider, the [Resource Owner Password Credentials flow](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html) is used to provide access and identity tokens.

![The path to becoming an identified user.](/images/authenticationtrail.png)

When a user chooses to sign-in, they become an identified user. Information about the user is obtained from the identity provider that they've signed in with. The identity provider returns access and identity tokens to {{site.data.keyword.appid_short}} that contain information about the user. The service takes the provided tokens and determines whether a user has the proper credentials to access an app. If the tokens are validated then the service authorizes the users access. After a user is authorized, their authentication information is associated with a user record. The record and its attributes can be accessed again from any client that authenticates with the same identity.

### Progressive authentication

With {{site.data.keyword.appid_short_notm}}, an anonymous user can choose to become an identified user.

But how does that work?

When a user chooses not to sign in immediately, they are considered an anonymous user. As an example, a user could immediately start adding items to a shopping cart without signing in. For anonymous users, {{site.data.keyword.appid_short_notm}} creates an ad hoc user record and calls the OAuth login API which returns anonymous access and identity tokens. By using those tokens, the app can create, read, update, and delete the attributes that are stored in the user record.

![The path to becoming an identified user when they start as anonymous.](/images/anon-authenticationtrail.png)

When an anonymous user signs-in, the anonymous access token is passed to the login API. The service authenticates the call with an identity provider. The service uses the access token to find the anonymous record and attaches the identity to it. The new access and identity tokens contain the public information that is shared by the identity provider. After a user is identified, their anonymous tokens become invalid. However, a user is still able to access their attributes because they're accessible with the new token.

**Note**: An identity can only be assigned to an anonymous record if it has not already been assigned to another user. If the identity is already associated with another {{site.data.keyword.appid_short_notm}} user, the tokens contain information of that user record and provide access to their attributes. The previous anonymous users attributes are not accessible through the new token. Until the token expires, the information can still be accessed through the anonymous access token. During development, you can choose how to merge the anonymous attributes to the known user.
