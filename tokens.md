---

copyright:
  years: 2017, 2022
lastupdated: "2022-02-10"

keywords: token validation, validate token, protect app, public key, token header, base64, decode payload, authorized, access permissions, app security, identity, jwt 

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


# Validating tokens
{: #token-validation}

Token validation is an important part of modern app development. By validating tokens, you can protect your app or APIs from unauthorized users. {{site.data.keyword.appid_full}} uses access and identity tokens to ensure that a user or app is authenticated before they are granted access. If you're using one of the SDKs provided by {{site.data.keyword.appid_short_notm}}, both obtaining and validating your tokens is done for you!
{: shortdesc}

For more information about how tokens are used in {{site.data.keyword.appid_short_notm}}, see [Understanding tokens](/docs/appid?topic=appid-tokens).
{: tip}

Tokens are used to verify that a person is who they say that they are. They confirm any access permissions that the user might hold, for a specified length of time. When a user signs in to your application and is issued a token, your app must validate the user before they are given access.



**What if I'm working in a language that {{site.data.keyword.appid_short_notm}} doesn't have an SDK for?**

Don't worry! You have three options:

* Work with the {{site.data.keyword.appid_short_notm}} APIs
* Implement your own validation logic
* Use any OIDC-compliant open source SDK



## Using the {{site.data.keyword.appid_short_notm}} APIs
{: #remote-validation}

By using introspection, you can use {{site.data.keyword.appid_short_notm}} to validate your tokens.
{: shortdesc}

1. Send a POST request to the [/introspect](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Authorization%20Server%20-%20Authorization%20Server%20V4/oauth-server.introspect) API endpoint to validate your token. The request must provide the token and a basic authorization header that contains the client ID and secret.

   Example request:

      ```sh
      POST /oauth/v4/{tenant_id}/introspect HTTP/1.1
      Host: us-south.appid.cloud.ibm.com
      Content-Type: application/x-www-form-urlencoded
      Authorization: Basic jdFlUaGlZUzAwTW0Tjk15TmpFMw==
      Cache-Control: no-cache

      token=XXXXX.YYYYY.ZZZZZ
      ```
      {: screen}

2. The server checks the expiry and signature of the token and returns a JSON object that tells whether the token is active or inactive.

   Example response:

      ```json
      {
      "active": true
      }
      ```
      {: screen}


## Manually Validating Tokens
{: #local-validation}

You can validate your tokens locally by parsing the token, verifying the token signature, and validating the claims that are stored in the token.
{: shortdesc}


1. Parse the tokens. The [JSON Web Token (JWT)](https://datatracker.ietf.org/doc/html/rfc7519){: external} is a standard way of securely passing information. It consists of three main parts: Header, Payload, and Signature. They are base64URL encoded and separated by a dot(.). You can use any base64URL decoder available to parse the token. Alternatively, you can use any of the [libraries that are listed](https://jwt.io/#libraries-io){: external} to parse the token.

   Example encoded token:

      ```sh
      eyJhbGciOiJSUzI1NiIsInR5cCI6IkpPU0UiLCJraWQiOiJhMmszIn0
      .eyJpc3MiOiJhcHBpZC1vYXV0aCIsImF1ZCI6ImFiYzEyMyIsImV4cCI6MTU2NDU2Nn0
      .IycnAGUmMHzpTWbe-qaRsx0B4Zi-SVav710Fb_8CTCQvLrHX9d42WuCZ5bW
      d-ikgEsf6waQxeBfhfwYxwHN87LZupApagVMZtylVAnXhG1pHu_32wbZsPvg6QjzNO
      j6ys2Lfl3qfb5Qrp9u4IsZltKPEN8HdfeOcKXxpw6UqP-8
      ```
      {: screen}

   Example decoded token:

      ```json
      {
      "alg": "RS256",
      "typ": "JOSE",
      "kid": "a2k3",
      "iss": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61",
      "aud": "abc123",
      "exp": 1564566
      }
      ```
      {: screen}

2. Make a call to the [/publickeys endpoint](https://us-south.appid.cloud.ibm.com/swagger-ui/#!/Authorization%20Server%20-%20Authorization%20Server%20V4/oauth-server.publicKeys){: external} to retrieve your public keys. The public keys that are returned are formatted as [JSON Web Keys (JWK)](https://datatracker.ietf.org/doc/html/rfc7517){: external}.

   Example request:

      ```sh
      GET /oauth/v4/{tenant_id}/publickeys HTTP/1.1
      Host: us-south.appid.cloud.ibm.com
      Cache-Control: no-cache
      ```
      {: screen}

3. Store the keys in your app cache for future use. Storing the keys speeds up the process and prevents network delay if another call is made.

4. Import the public key parameters.

   Example response:

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

   | Parameter | Description |
   | --------- | ----------- |
   | `kty` | Defines the algorithm that is used. |
   | `use` | Defines the purpose of the key. |
   | `kid` | Defines the unique ID of the key. | 
   | Other | There might be other remaining parameters that are specific to your algorithm that must also be imported. | 
   {: caption="Table 1. Public key parameters" caption-side="top"}

5. Verify the token's signature. The token header contains the algorithm that was used to sign the token and the Key ID or `kid` claim of the matching public key. Because public keys do not frequently change, you can cache public keys in your app and occasionally refresh them. If your cached key is missing the `kid` claim, you can validate the tokens locally.

   1. Have your application verify that the contents of the incoming token header match the parameters of the public key.
   2. Check specifically that the same algorithms were used and that your public key cache contains a key with the relevant Key ID.
   3. Ensure that your hash value is the same as the signature of the PEM form of the public key. Your hash value can be obtained by combining and hashing the header of the payload of the token. Because this process can be complex to manually implement, it might be helpful to use one of the [listed libraries](https://jwt.io/) to validate the signature.

6. Validate the claims that are stored in the tokens. To verify future checks, you can use [this list](https://openid.net/specs/openid-connect-core-1_0.html#IDTokenValidation).
  
   | Claim | Description |
   | ----- | ----------- |
   | `iss` | The issuer must be the same as the {{site.data.keyword.appid_short_notm}} OAuth server. |
   | `exp` | The current time must be less than the expiry time. |
   | `aud` | The audience must contain the client ID of your app. |
   | `tenant` | The tenant must contain the tenant ID of your app. |
   | `scope` | The scope of permissions that is granted to the user. This is specific to the access token. | 
   {: caption="Table 2. Claims that must be validated" caption-side="top"}
