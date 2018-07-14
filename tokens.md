# Validating tokens
{: #token-validation}


Token validation is a very important part of modern app development. By validating tokens, you can protect your app or APIs from unauthorized users. App ID uses access and identity tokens to ensure that an end-user is authenticated before they are granted access.  
{: shortdesc}


## Understanding tokens
{: #tokens}

App ID uses three different types of tokens to protect your apps.
{: shortdesc}


**What is an access token?**

Access tokens represent authorization and enable communication with [back-end resources](/docs/services/appid/protecting-resources.html) that are protected by authorization filters that are set by {{site.data.keyword.appid_short}}. The token conforms to JavaScript Object Signing and Encryption (JOSE) specifications. The tokens are formatted as <a href="https://jwt.io/introduction/" target="blank">JSON Web Tokens <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.

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

Identity tokens represent authentication and contain information about the user. It can give you information about their name, email, gender, and location. A token can also return a URL to an image of the user.

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

**What is a refresh token?**

{{site.data.keyword.appid_short}} supports the ability to acquire new access and identity tokens without reauthentication, as defined in <a href="http://openid.net/specs/openid-connect-core-1_0.html#RefreshTokens" target="blank">OIDC <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>. When signing in with a refresh token, a user doesn't have to take any actions, such as providing credentials. Generally, refresh tokens are configured to have a longer life span than a regular access token. To take full advantage of refresh tokens, persist the tokens for their full life span. A user cannot directly access resources with just a refresh token, which makes them much safer to persist than an access token. For examples of working with refresh tokens and how to use them to implement a *remember me* functionality, check out the getting started samples. >As a best practice, refresh tokens should be securely stored by the client that received them, and should only be sent to the authorization server that issued them.

There are some cases when you would want to have the refresh token revoked, for example when its believed to be compromised. There are two methods of revoking a refresh token. If you have the refresh token, you can revoke it based on <a href="https://tools.ietf.org/html/rfc7009#section-2" target="blank">RFC7009</a>. Alternatively, if you have the user id, you can revoke the refresh token by using <a href="https://appid-management.ng.bluemix.net/swagger-ui/" target="blank">the Management API</a>. For more information about accessing the management API see [managing service access](/docs/services/appid/iam.html#service-access-management).

Revoking the use of either method revokes all active refresh tokens that are assigned to that user that were created before revocation.
{: tip}

**Where do the tokens come from?**

Access and refresh tokens are issued through the App ID OAuth Server and are formatted as [JSON Web Tokens (JWT)](https://jwt.io/introduction/). The tokens have been signed with a [JSON Web Key (JWK)](https://tools.ietf.org/html/rfc7517) using the RS256 algorithm. Identity tokens are returned by an identity provider.

**What happens to the information that the token contains?**

The access token contains a set of standard JWT claims and a set of App Id specific claims such as a tenant ID. The identity token contains user specific information. The information in the tokens is stored as claims as part of a [user's profile](/docs/services/appid/user-profile.html).

**How are tokens sent?**

The tokens are sent to your app by using the [Bearer authentication](https://tools.ietf.org/html/rfc6750#page-5) scheme. Access and identity tokens are appended to the authorization header. To extract the tokens, you app must parse the header.

Example request:

```http request
GET /resource HTTP/1.1
Host: server.example.com
Authorization: Bearer  mF_9.B5f-4.1JqM mF_9.B5f-4.1JqM
```
{: screen}


## Validating tokens locally
{: #local-validation}

You can validate your tokens locally by parsing the token, verifying the token signature, and validating the claims that are stored in the token. Verifying tokens locally is best used for testing.
{: shortdesc}


1. Parse the tokens. The [JSON Web Token (JWT)](https://tools.ietf.org/html/rfc7519) is a standard way of securely passing information. It consists of 3 main parts: Header, Payload, and Signature. They are base64URL encoded and separated by a dot(.). You can use any base64URL decoder available to parse the token. Alternatively, you can use any of the [libraries listed](https://jwt.io/) to parse the token.
  Example:
    ```text
    eyJhbGciOiJSUzI1NiIsInR5cCI6IkpPU0UiLCJraWQiOiJhMmszIn0
    .eyJpc3MiOiJhcHBpZC1vYXV0aCIsImF1ZCI6ImFiYzEyMyIsImV4cCI6MTU2NDU2Nn0
    .IycnAGUmMHzpTWbe-qaRsx0B4Zi-SVav710Fb_8CTCQvLrHX9d42WuCZ5bW
    d-ikgEsf6waQxeBfhfwYxwHN87LZupApagVMZtylVAnXhG1pHu_32wbZsPvg6QjzNO
    j6ys2Lfl3qfb5Qrp9u4IsZltKPEN8HdfeOcKXxpw6UqP-8
    ```
    {: screen}

  Example decoded header:
    ```json
    {
      "alg": "RS256",
      "typ": "JOSE",
      "kid": "a2k3"
    }
    ```
    {: screen}

  Decoded payload:
    ```json
    {
      "iss": "appid-oauth",
      "aud": "abc123",
      "exp": 1564566
    }
    ```
    {: screen}

2. Retrieve your public keys by making a call to the [App ID API](https://appid-oauth.ng.bluemix.net/swagger-ui/#!/Authorization_Server_V3/publicKeys). The public keys that are returned are formatted as [JSON Web Keys (JWK)](https://tools.ietf.org/html/rfc7517).
  Example Request:
    ```http request
    GET /oauth/v3/{tenant_id}/publickeys HTTP/1.1
    Host: appid-oauth.ng.bluemix.net
    Cache-Control: no-cache
    ```
    {: screen}

3. Store the keys in your app cache for future use. This speeds up the process and prevents network delay if an additional call is made.

4. Import the public key parameters.
  1. **kty**: The Key Type parameter indicates the algorithm used.
  2. **use**: The Usage parameter indicates the purpose of the key.
  3. **kid**: The Key Id parameter uniquely identifies the key.
  4. The remaining parameters are algorithm-specific parameters.

  Example Response:
    ```json
    {
      "keys": [
        {
          "kty": "RSA",
          "use": "sig",
          "n": "AsdaE",
          "e": "SDAasw",
          "kid": "ad123dCAz"
        }
      ]
    }
    ```
    {: screen}

5. Verify the token's signature.
  1. The token header contains the algorithm that was used to sign the token and the Key ID of the match public key. Your app must verify that the contents of this header match with the parameters of the public key by using the cache.
  2. The hash value that is obtained by combining and hashing the header and the payload of the token should be the same as signing the signature with the PEM form of the public key. Because this process can be quite complex it might be helpful to use one of the [listed libraries](https://jwt.io/) to validate the signature.

6. Validate the claims that are stored in the tokens. The claims in the following table must be verified. To verify additional checks, you can use [this list](http://openid.net/specs/openid-connect-core-1_0.html#IDTokenValidation).
  <table>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="More information icon"/> Claims that must be validated </th>
    </thead>
    <tbody>
      <tr>
        <td><code>iss</code></td>
        <td>The issuer should be the same as the App ID OAuth server.</td>
      </tr>
      <tr>
        <td><code>exp</code></td>
        <td>The current time should be less than the expiry time.</td>
      </tr>
      <tr>
        <td><code>aud</code></td>
        <td>The audience should contain the client ID of your app.</td>
      </tr>
      <tr>
        <td><code>tenant</code></td>
        <td>The tenant should contain the tenant ID of your app.</td>
      </tr>
      <tr>
        <td><code>scope</code></td>
        <td>The scope of permissions that is granted to the user. This is specific to the access token.</td>
      </tr>
    </tbody>
  </table>


## Validating tokens remotely
{: #remote-validation}

By using introspection, you can use App ID to validate your tokens.
{: shortdesc}

1. Send a POST request to the [/introspect](https://appid-oauth.ng.bluemix.net/swagger-ui/#!/Authorization_Server_V3/introspect) API endpoint to validate your token. The request must contain the token and a basic authorization header which contains the client ID and secret.

  Example Request:
    ```http request
    POST /oauth/v3/{tenant_id}/introspect HTTP/1.1
    Host: appid-oauth.ng.bluemix.net
    Content-Type: application/x-www-form-urlencoded
    Authorization: Basic jdFlUaGlZUzAwTW0Tjk15TmpFMw==
    Cache-Control: no-cache

    token=eyJhb.eyJpcNyG.imMmt0P
    ```
    {: screen}

2. The server checks the expiry and signature of the token and returns a JSON object that tells whether the token is active or inactive.

  Example Response:
    ```json
    {
      "active": true
    }
    ```
    {: screen}
