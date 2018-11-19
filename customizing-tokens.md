---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}


# Customizing Tokens
{: #customizing-tokens}

You can configure your {{site.data.keyword.appid_short_notm}} tokens to meet the specific needs of your application.
{: shortdesc}

**What kinds of tokens are there?**

{{site.data.keyword.appid_short_notm}} uses four different types of tokens to secure your applications.

* Access tokens: Enable communication with back-end resources that are protected by authorization filters.
* Identity tokens: Contain personal information and are used to authenticate a user.
* Refresh tokens: Can be used to extend the amount of time that a user can go without re-authenticating.
* Anonymous tokens: Are issued to users that have not yet been authenticated. Because these tokens are not associated with a user, they have limited capabilities.

Want to learn more about tokens? Read more in [Understanding tokens](authorization.html#tokens).
{: tip}

</br>

**What are my customization options?**

You can customize your tokens by setting the lifespan validity or by adding custom attributes to your tokens. Check out the following table to see how lifespan is configured or continue reading to learn about mapping custom attributes.

<table>
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

</br>

**Why would I want to add attributes to my tokens?**

There are several reasons that you might want to track extra attributes. When you're working with your app developers, you can map roles and permissions. Or, when you're building profiles on your end-users, you can track extra information that helps you to create personalized experiences. By keeping the information in one place, you can

</br>

**Are there any security considerations?**

Yes. Because tokens are used to identify users and secure your resources, the lifespan of a token affects several different things. By customizing your token configuration you can ensure that your security and user experience needs are met. However, should a token ever become compromised, a malicious user has more time to affect your application.

Want to learn more about the security considerations you should make? Check out [Custom attributes](custom-attributes.html).
{: tip}

</br>
</br>

## Understanding custom attributes and claims
{: #custom-claims}

You can map user attributes to your access and identity tokens. This means that you don't have to go to the [/userinfo endpoint](https://appid-oauth.ng.bluemix.net/swagger-ui/#!/Authorization_Server_V3/userInfo) or pull custom attributes later, because they're already stored in the tokens!
{: shortdesc}


**Why would I add attributes to my tokens?**

Without having to make extra network calls, everything that your app may need to know about a user or what they can do is already in the token! Provided you don't have massive amounts of data, this makes you more efficient. Additionally, you can ensure the integrity of these mapped attributes when they are sent across the network because they are stored in a signed token.

</br>

**What kinds of attributes can I add?**

You can map _any_ type of attribute. You can map scopes or roles for specific users, or even create your own scopes!

</br>

**What types of claims can I define?**

The claims that are provided by {{site.data.keyword.appid_short_notm}} fall into several categories that are differentiated by their level of customization.

*Registered claims*: There are some fields in the access and identity tokens that are defined by {{site.data.keyword.appid_short_notm}} and cannot be overridden by custom mappings. If your claim is restricted, it is ignored by the service. The claims are `iss`, `aud`, `sub`, `iat`, `exp`, `amr`, and `tenant`.

*Restricted claims*: Depending on the token that the claims are mapped to, some claims have limited customization possibilities. For an access token the `scope` field is the only restricted claim. It cannot be overridden by custom mappings, but it can be extended with your own scopes. When the scope field is mapped to an access token, the value must be a string and cannot be prefixed by `appid_` or it will be ignored. In identity tokens, the claims `identities` and `oauth_clients` cannot be modified or overridden.

*Normalized claims*: Every identity token contains a set of claims that is recognized by {{site.data.keyword.appid_short_notm}} as normalized claims. When they are available, they are directly mapped from your identity provider to the token. These claims cannot be explicitly omitted but can be overridden by custom claim mappings. The fields include `name`, `email`, `picture`, `local`, and `gender`.

</br>

**How are claims defined?**

Each mapping is defined by a data source object and a key that is used to retrieve the claim. Each custom claim is set for each token separately and are sequentially applied. You can register up to 100 claims for each token up to a maximum payload of 100KB.

<table>
    <thead>
      <th colspan=3><img src="images/idea.png" alt="Idea icon"/> Understanding claim mapping objects</th>
    </thead>
    <tbody>
      <tr>
        <td><code><em>source</em></code></td>
        <td>Required</td>
        <td>Defines the source of the claim. It can refer to the identity provider's user information or the user's {{site.data.keyword.appid_short_notm}} custom attributes. </br> </br> Options include: `saml`, `cloud_directory`, `facebook`, `google`, `appid_custom`, `ibmid`, and `attributes`.</td>
      </tr>
      <tr>
        <td><code><em>sourceClaim</em></code></td>
        <td>Required</td>
        <td>Defines the source data's claim. </td>
      </tr>
    </tbody>
  </table>

You can reference nested fields in your claim mappings by using the dot syntax. Example: `nested.attribute`
{:tip}

</br>

## Configuring {{site.data.keyword.appid_short_notm}} tokens
{: #configuring-tokens}

You can configure your {{site.data.keyword.appid_short_notm}} tokens by using the GUI or the management APIs.
{: shortdesc}

### Configuring token lifespan with the GUI
{: #configuring-tokens-ui}

1. Navigate to your service dashboard.
2. In the **Identity Providers** section of the navigation, select the **Manage** page.
3. In the **Settings** tab configure your tokens.
  1. To allow sign in without the need for user interaction, set **refresh tokens** to **On**.
  2. Set your refresh token lifetime. Expiration is set in days and can be any value in range 1 to 90. The smaller the number, the more frequently a user must sign themselves in.
  3. Set your access token lifetime. The expiration is set in minutes and can be in range 5 to 1440. The smaller the value, the more protection that you have in cases of token theft.
  4. Set your anonymous token lifetime. An [anonymous token](/docs/services/appid/progressive.html#anonymous) is assigned to users the moment they begin interacting with your app. When a user signs in, the information in the anonymous token is then transferred to the token associated with the user. Expiration is set in days and can be any value between 1 and 90.

</br>

### Configuring tokens with the Management APIs
{: #configuring-tokens-api}

**Before you begin**

Be sure that you have the following prerequisites:

* Your {{site.data.keyword.appid_short_notm}} instance's tenant ID. This can be found in the **Service Credentials** section of the GUI.
* Your Identity and Access Management (IAM) token. For help obtaining an IAM token, check out the [IAM docs](/docs/iam/apikey_iamtoken.html).

**Mapping your claims**

1. Make a PUT request to the `/config/tokens` endpoint with your token configuration.

  Header:
  ```
  PUT {management-url}/management/v4/{tenantId}/tokens
       Host: <management-server-url>
       Authorization: 'Bearer <IAM_TOKEN>'
       Content-Type: application/json
  ```
  {: pre}

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
  {: pre}

  <table>
    <thead>
      <th colspan=3><img src="images/idea.png" alt="Idea icon"/> Understanding the token configuration</th>
    </thead>
    <tbody>
      <tr>
        <td><code><em>access</em></code></td>
        <td>Optional</td>
        <td>Object containing expiration time, `expires_in`, in minutes of your access and identity tokens. </br> </br> The default expiration is 60 minutes. </td>
      </tr>
      <tr>
          <td><code><em>refresh</em></code></td>
          <td>Optional</td>
          <td>Object that contains the expiration time, `expires_in`, in days of your refresh token. </br> </br> The default expiration is 30 days. </td>
      </tr>
      <tr>
          <td><code><em>anonymousAccess</em></code></td>
          <td>Optional</td>
          <td>Object that contains the expiration time, `expires_in`, in days of your anonymous access and identity tokens. </br> </br> The default expiration is 30 days.
      </tr>
      <tr>
          <td><code><em>accessTokenClaims</em></code></td>
          <td>Optional</td>
          <td>An array that contains the objects that are created when claims related to access tokens are mapped.</td>
      </tr>
      <tr>
          <td><code><em>idTokenClaims</em></code></td>
          <td>Optional</td>
          <td>An array that contains the objects that are created when claims related to identity tokens are mapped.</td>
      </tr>
    </tbody>
  </table>

  Example request:
  ```
  $ curl -X PUT
    --header 'Content-Type: application/json'
    --header 'Accept: application/json'
    --header 'Authorization: <IAM Token'
    -d '{
          "accessTokenClaims": [
            {
              "source": "saml",
              "sourceClaim": "name_id"
            }
          ],
          "idTokenClaims": [
            {
              "source": "attributes",
              "sourceClaim": "theme"
            }
          ]
      }'
}' '{management-url}/management/v4/{Tenant ID}/config/tokens'
  ```
  {: screen}
