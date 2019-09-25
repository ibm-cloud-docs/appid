---

copyright:
  years: 2017, 2019
lastupdated: "2019-09-25"

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

You can configure your {{site.data.keyword.appid_short_notm}} token to meet the specific needs of your application.
{: shortdesc}

## Understanding customization
{: #understanding-customization}

{{site.data.keyword.appid_short_notm}} uses different types of tokens to protect your applications.

* Access tokens: Enable communication with back-end resources that are protected by authorization filters. If an access token is not associate with a specific user, the token would have limited capabilities.
* Identity tokens: Contain personal information and are used to authenticate a user. Depending on your app configuration, identity tokens can be issued before a user is authenticated. This allows you to start associating attributes with your users before they sign in to your application.
* Refresh tokens: Can be used to extend the amount of time that a user can go without re-authenticating.

Want to learn more about tokens? Read more in [Understanding tokens](/docs/services/appid?topic=appid-tokens).
{: tip}


You can customize your tokens [in the GUI](/docs/services/appid?topic=appid-customizing-tokens#configuring-tokens-ui) or by using [the API](/docs/services/appid?topic=appid-customizing-tokens#configuring-tokens-api){: external} by setting the lifespan validity or by adding custom claims to your tokens. Check out the following table to see how lifespan is configured or continue reading to learn about mapping custom attributes.

<table>
  <caption>Table 1. Token customization options</caption>
  <tr>
    <th>Token type</th>
    <th>Value type</th>
    <th>Default</th>
    <th>Options</th>
  </tr>
  <tr>
    <td>Access</td>
    <td>Minutes</td>
    <td>60</td>
    <td>Any value between 5 and 1440</td>
  </tr>
  <tr>
    <td>Identity</td>
    <td>Minutes</td>
    <td>60</td>
    <td>Any value between 5 and 1440</td>
  </tr>
  <tr>
    <td>Refresh</td>
    <td>Days</td>
    <td>30</td>
    <td>Any value between 1 and 9</td>
  </tr>
  <tr>
    <td>Anonymous</td>
    <td>Days</td>
    <td>30</td>
    <td>Any value between 1 and 9</td>
  </tr>
</table>


Because tokens are used to identify users and secure your resources, the lifespan of a token affects several different things. By customizing your token configuration you can ensure that your security and user experience needs are met. However, should a token ever become compromised, a malicious user has more time to affect your application. You can learn more about security considerations in [Setting custom attributes](/docs/services/appid?topic=appid-profiles#profile-set-custom).
{: important}


## Understanding custom attributes and claims
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

If you have customized expiration information for your token, you must set it in every request. If you don't, this request overwrites your current configuration and the default is used for anything that is undefined.
{: note}

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



## Configuring token lifespan with the GUI
{: #configuring-tokens}

1. Navigate to your service dashboard.
2. In the **Identity Providers** section of the navigation, select the **Manage** page.
3. In the **Settings** tab configure your tokens.
  1. To allow sign in without the need for user interaction, set **refresh tokens** to **On**.
  2. Set your refresh token lifetime. Expiration is set in days and can be any value in range 1 to 90. The smaller the number, the more frequently a user must sign themselves in.
  3. Set your access token lifetime. The expiration is set in minutes and can be in range 5 to 1440. The smaller the value, the more protection that you have in cases of token theft.
  4. Set your anonymous token lifetime. An [anonymous token](/docs/services/appid?topic=appid-anonymous) is assigned to users the moment they begin interacting with your app. When a user signs in, the information in the anonymous token is then transferred to the token associated with the user. Expiration is set in days and can be any value between 1 and 90.

</br>

## Configuring tokens with the Management APIs
{: #configuring-tokens-api}

### Before you begin
{: #configure-tokens-api-before}

Be sure that you have the following prerequisites:

* Your {{site.data.keyword.appid_short_notm}} instance's tenant ID. This can be found in the **Service Credentials** section of the GUI.
* Your Identity and Access Management (IAM) token. For help obtaining an IAM token, check out the [IAM docs](/docs/iam?topic=iam-iamtoken_from_apikey).

### Mapping your claims
{: #custom-claim-mapping}

Make a PUT request to the `/config/tokens` endpoint with your token configuration.

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
    <td>Object containing expiration time, `expires_in`, in minutes of your access and identity tokens. </br> </br> The default expiration is 60 minutes. </td>
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


