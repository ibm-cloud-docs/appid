---

copyright:
  years: 2017, 2019
lastupdated: "2019-10-25"

keywords: Authentication, authorization, identity, app security, secure, custom, tokens, access, claim, attributes

subcollection: appid

---

{:external: target="_blank" .external}
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


# Customizing tokens
{: #customizing-tokens}

With App ID, tokens are used to identify users and secure your resources. You can choose to customize the information that is injected in to the tokens by the service. For more information about tokens and how they're used in App ID, see [Understanding tokens](/docs/services/appid?topic=appid-tokens).
{: shortdesc}

By customizing your token configuration, you can ensure that your security and user experience needs are met. However, should a token ever become compromised, a malicious user has more information or time that can be used to affect your application. Be sure that you understand the security implications of the customizations that you you want to make before you make them. 
{: important}


## Understanding custom claims mapping
{: #custom-claims}

You can map user profile attributes to your access and identity token claims. This means that you don't have to go to the [/userinfo endpoint](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Authorization_Server_V4/userInfo){: external} or pull custom attributes later, because they're already stored in the tokens!
{: shortdesc}

### What is a claim?
{: #custom-claims-defined}

A claim is a statement that an entity makes about itself or on behalf of someone else. For example, if you signed into an application by using an identity provider, the provider would send the application a group of claims or statements about you to the app so that it can group with information that it already knows about you. This way, when you sign in, the app is set up with your information, in the way that you configured it. Check out the following example to see how to format the JSON object.

```
{
  "accessTokenClaims": [
    {
      "source": "saml",
      "sourceClaim": "moderator"
    }
  ],
  "idTokenClaims": [
    {
      "source": "saml",
      "sourceClaim": "moderator"
    }
  ],
  "access": {
    "expires_in": 3600
  },
  "refresh": {
    "expires_in": 2592000,
    "enabled": true
  },
  "anonymousAccess": {
    "expires_in": 2592000,
    "enabled": true
  }
}
```
{: screen}



### Why would I want to add claims to my tokens?
{: #why-custom-claims}

Without having to make extra network calls, everything that your app may need to know about a user or what they can do is already in the token! Provided that you don't have massive amounts of data, this makes you more efficient. Additionally, you can ensure the integrity of these mapped attributes when they are sent across the network because they are stored in a signed token.


### What types of claims can I define?
{: #custom-claim-types}

The claims that are provided by {{site.data.keyword.appid_short_notm}} fall into several categories that are differentiated by their level of customization.

*Registered claims*: There are some claims in the access and identity tokens that are defined by {{site.data.keyword.appid_short_notm}} and cannot be overridden by custom mappings. If your claim is restricted, it is ignored by the service. The claims are `iss`, `aud`, `sub`, `iat`, `exp`, `amr`, and `tenant`.

*Restricted claims*: Depending on the token that the claims are mapped to, some claims have limited customization possibilities. For an access token, `scope` is the only restricted claim. It cannot be overridden by custom mappings, but it can be extended with your own scopes. When the scope claim is mapped to an access token, the value must be a string and cannot be prefixed by `appid_` or it will be ignored. In identity tokens, the claims `identities` and `oauth_clients` cannot be modified or overridden.

*Normalized claims*: Every identity token contains a set of claims that is recognized by {{site.data.keyword.appid_short_notm}} as normalized claims. When they are available, they are directly mapped from your identity provider to the token. These claims cannot be explicitly omitted but can be overwritten in your token by custom claims. The claims include `name`, `email`, `picture`, and `local`. 

Note: This does not change or eliminate the attribute, but does change the information that is present in the token at runtime.


### How are claims mapped to tokens?
{: #custom-claims-mapping}

Each mapping is defined by a data source object and a key that is used to retrieve the claim. Each custom claim is set for each token separately and are sequentially applied. You can register up to 100 claims for each token up to a maximum payload of 100KB.

<table>
  <caption>Table 2. Required claim mapping options</caption>
    <tr>
      <th>Object</th>
      <th>Description</th>
    </tr>
    <tr>
      <td><code><em>source</em></code></td>
      <td>Defines the source of the claim. It can refer to the identity provider's user information or the user's {{site.data.keyword.appid_short_notm}} custom attributes. </br> Options include: <code>saml</code>, <code>cloud_directory</code>, <code>facebook</code>, <code>google</code>, <code>appid_custom</code>,  and <code>attributes</code>.</td>
    </tr>
    <tr>
      <td><code><em>sourceClaim</em></code></td>
      <td>Defines the source data's claim. </td>
    </tr>
  </table>

You can reference nested claims in your mappings by using the dot syntax. Example: `nested.attribute`
{:tip}


## Configuring tokens
{: #configuring-tokens}

With the API, you can customize the information that is returned in your App ID tokens.
{: shortdesc}

If you just want to configure the lifespan of your token, you can quickly make the changes through the service dashboard. For more information, see [Managing authentication](/docs/services/appid?topic=appid-managing-idp#idp-token-lifetime).
{: tip}

1. Obtain an IAM token. For more information, see the [IAM documentation](/docs/iam?topic=iam-getstarted#getstarted).

  1. In the IBM Cloud dashboard, click Manage > Access (IAM).
  2. Select IBM Cloud API keys.
  3. Click Create an IBM Cloud API key
  4. Give your key a name and describe it. Click Create. A screen displays with your your key.
  5. Click Copy or Download your key. When you close the screen, you can no longer access the key.
  6. Make the following cURL request with the API key that you created.

    ```
    curl -k -X POST \
    --header "Content-Type: application/x-www-form-urlencoded" \
    --header "Accept: application/json" \
    --data-urlencode "grant_type=urn:ibm:params:oauth:grant-type:apikey" \
    --data-urlencode "apikey={apikey}" \
    "https://iam.cloud.ibm.com/identity/token"
    ```
    {: codeblock}

2. Get the tenant ID for your instance of the service. You can find the value in either your service or application credentials.

3. Make a PUT request to the `/config/tokens` endpoint with your token configuration.

  Header:
  ```
  PUT -X "https://<region>.appid.cloud.ibm.com/management/v4/{tenantId}/tokens"
    -H Authorization: 'Bearer <IAM_TOKEN>'
    -H Content-Type: application/json
  ```
  {: codeblock}

  Body:
  ```
    {
        "access": {
            "expires_in": 3600,
        },
        "refresh": {
            "expires_in": 2592000,
            "enabled": true
        },
        "anonymous": {
            "expires_in": 2592000,
            "enabled": true
        },
        "accessTokenClaims": [
            {
              "source": "saml",
              "sourceClaim": "name_id"
            }
        ],
        "idTokenClaims": [
            {
              "source": "saml",
              "sourceClaim": "attributes.uid"
            }
        ]
    }
  ```
  {: codeblock}

  <table>
    <caption>Table 3. Understanding the token configuration</caption>
    <tr>
      <th>Variable</th>
      <th>Description</th>
    </tr>
    <tr>
      <td><code><em>access</em></code></td>
      <td>Object containing expiration time, `expires_in`, in minutes of your access and identity tokens. </br> </br> The default expiration is 60 minutes.</td>
    </tr>
    <tr>
      <td><code><em>refresh</em></code></td>
      <td>Object that contains the expiration time, `expires_in`, in days of your refresh token. </br> </br> The default expiration is 30 days. </td>
    </tr>
    <tr>
      <td><code><em>anonymousAccess</em></code></td>
      <td>Object that contains the expiration time, `expires_in`, in days of your anonymous access and identity tokens. </br> </br> The default expiration is 30 days.
    </tr>
    <tr>
      <td><code><em>accessTokenClaims</em></code></td>
      <td>An array that contains the objects that are created when claims related to access tokens are mapped.</td>
    </tr>
    <tr>
      <td><code><em>idTokenClaims</em></code></td>
      <td>An array that contains the objects that are created when claims related to identity tokens are mapped.</td>
    </tr>
  </table>

  You must set the token values in each request that you make. If a value is not set then the default is used. Each customization request overwrites what is previously configured.
  {: note}


