---

copyright:
  years: 2017, 2018
lastupdated: "2018-09-26"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}


# Validating tokens
{: #token-validation}

Token validation is a very important part of modern app development. By validating tokens, you can protect your app or APIs from unauthorized users. {{site.data.keyword.appid_full}} uses access and identity tokens to ensure that an end-user or app is authenticated before they are granted access.  
{: shortdesc}

For more information about how tokens are used in {{site.data.keyword.appid_short_notm}}, see [Understanding tokens](authorization.html#tokens).
{: tip}

**What is token validation?**

Tokens are used to verify that a person is who they say that they are, as well as confirm any access permissions that the user might hold, for a specified period of time. When a user signs into your application and is issued a token, your app must validate the user before they are given access to your app. In general, the App ID SDKs handle both obtaining and validating your tokens.

**What if I'm working in a language that App ID doesn't have an SDK for?**

Don't worry! You have two options:

* Use any OIDC compliant open source SDK.
* Implement your own validation logic by using the App ID APIs.

The second is a preferred solution, for most.

</br>
</br>

## Validating tokens locally
{: #local-validation}

You can validate your tokens locally by parsing the token, verifying the token signature, and validating the claims that are stored in the token.
{: shortdesc}


1. Parse the tokens. The [JSON Web Token (JWT)](https://tools.ietf.org/html/rfc7519) is a standard way of securely passing information. It consists of 3 main parts: Header, Payload, and Signature. They are base64URL encoded and separated by a dot(.). You can use any base64URL decoder available to parse the token. Alternatively, you can use any of the [libraries listed](https://jwt.io/#libraries-io) to parse the token.

  Example encoded token:

    ```
    eyJhbGciOiJSUzI1NiIsInR5cCI6IkpPU0UiLCJraWQiOiJhMmszIn0
    .eyJpc3MiOiJhcHBpZC1vYXV0aCIsImF1ZCI6ImFiYzEyMyIsImV4cCI6MTU2NDU2Nn0
    .IycnAGUmMHzpTWbe-qaRsx0B4Zi-SVav710Fb_8CTCQvLrHX9d42WuCZ5bW
    d-ikgEsf6waQxeBfhfwYxwHN87LZupApagVMZtylVAnXhG1pHu_32wbZsPvg6QjzNO
    j6ys2Lfl3qfb5Qrp9u4IsZltKPEN8HdfeOcKXxpw6UqP-8
    ```
    {: screen}

  Example decoded header:

    ```
    {
      "alg": "RS256",
      "typ": "JOSE",
      "kid": "a2k3"
    }
    ```
    {: screen}

  Decoded payload:

    ```
    {
      "iss": "appid-oauth",
      "aud": "abc123",
      "exp": 1564566
    }
    ```
    {: screen}

2. Retrieve your public keys by making a call to the [/publickeys endpoint](https://appid-oauth.ng.bluemix.net/swagger-ui/#!/Authorization_Server_V3/publicKeys). The public keys that are returned are formatted as [JSON Web Keys (JWK)](https://tools.ietf.org/html/rfc7517).

  Example Request:

    ```
    GET /oauth/v3/{tenant_id}/publickeys HTTP/1.1
    Host: appid-oauth.ng.bluemix.net
    Cache-Control: no-cache
    ```
    {: screen}

3. Store the keys in your app cache for future use. This speeds up the process and prevents network delay if an additional call is made.

4. Import the public key parameters.

  Example Response:

    ```]
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

  <table>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="More information icon"/> Public key parameters </th>
    </thead>
    <tbody>
      <tr>
        <td><code>kty</code></td>
        <td>Defines the algorithm used.</td>
      </tr>
      <tr>
        <td><code>use</code></td>
        <td>Defines the purpose of the key.</td>
      </tr>
      <tr>
        <td><code>kid</code></td>
        <td>Defines the unique ID of the key.</td>
      </tr>
      <tr>
        <td>Other</td>
        <td>There might be other remaining parameters that are specific to your algorithm that must also be imported.</td>
      </tr>
    </tbody>
  </table>

5. Verify the token's signature. The token header contains the algorithm that was used to sign the token and the Key ID or `kid` claim of the matching public key. Because public keys do not frequently change, you can cache public keys in your app and occasionally refresh them. If your cached key is missing the `kid` claim. then you'll need to validate locally.

  1. Have your application verify that the contents of the incoming token header match the parameters of the public key.
  2. Check specifically that the same algorithms were used and that your public key cache contains a key with the relevant Key ID.
  3. The hash value that is obtained by combining and hashing the header and the payload of the token should be the same as signing the signature with the PEM form of the public key. Because this process can be quite complex to manually implement, so it might be helpful to use one of the [listed libraries](https://jwt.io/) to validate the signature.

6. Validate the claims that are stored in the tokens. To verify additional checks, you can use [this list](http://openid.net/specs/openid-connect-core-1_0.html#IDTokenValidation).
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

By using introspection, you can use {{site.data.keyword.appid_short_notm}} to validate your tokens.
{: shortdesc}

1. Send a POST request to the [/introspect](https://appid-oauth.ng.bluemix.net/swagger-ui/#!/Authorization_Server_V3/introspect) API endpoint to validate your token. The request must contain the token and a basic authorization header which contains the client ID and secret.

  Example Request:

    ```
    POST /oauth/v3/{tenant_id}/introspect HTTP/1.1
    Host: appid-oauth.ng.bluemix.net
    Content-Type: application/x-www-form-urlencoded
    Authorization: Basic jdFlUaGlZUzAwTW0Tjk15TmpFMw==
    Cache-Control: no-cache

    token=XXXXX.YYYYY.ZZZZZ
    ```
    {: screen}

2. The server checks the expiry and signature of the token and returns a JSON object that tells whether the token is active or inactive.

  Example Response:

    ```
    {
      "active": true
    }
    ```
    {: screen}

</br>
</br>
