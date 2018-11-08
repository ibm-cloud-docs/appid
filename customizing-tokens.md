---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-08"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}


# Customizing Tokens
{: #customizing-tokens}

Your {{site.data.keyword.appid_short_notm}} tokens can be configured to fit your applications needs.
{: shortdesc}

## Lifetime
{: #token-lifetime}

Token validity periods can be configured for each token type on per service instance basis and can be set to the period best suited for your particular use-case.
{: shortdesc}

**Access / Identity Tokens**

[Access and identity tokens](authorization.html#tokens) can be used to identify users and securely access protected resources.

Adjusting the lifetime of these tokens is a trade-off between system performance and application security. A longer token lifespan reduces the number of times a client has to initiate a token refresh flow. However, this also means that if your application is ever compromised, a malicious actor has more time to abuse stolen tokens.

system performance = user experience = normal app is user experience but if using app to app then it would be system performance.
User focused is probs the best for now

If you steal my access token then its compromised ... but if I get into your entire app is compromised. Access token

The default lifespan of these tokens is 1 hour. You can set your token expiration (in minutes) to any value between 5 and 1440.

Figure out how to merge token information.

After expiration, the client must acquire new tokens using a refresh token or by forcing the user to re-authenticate.




**Refresh Tokens**

[Refresh Tokens](authorization.html#tokens) are used exclusively for retrieving new access and identity tokens. If using a confidential client, such as a backend server, these can be securely persisted allowing them to have much longer lifespans.

Can have a longer lifespan provided that you can host it on a confidential client. More positive and make sure to explain how refresh tokens get refreshed.

confidential client: need a link (backend server something in OAuth 2 that's trusted to secure user information)

The default lifespan of these tokens is 30 days. You can set your refresh token's expiration (in days) to any value between 1 and 90.

Increase refresh token for better app user experience (no need to explicitly sign-in) without compromising security (i.e. Without reducing access token expiration).

After expiration, if a new refresh token has not been requested, the user must re-authenticate.

**Anonymous Tokens**

Anonymous tokens are issued to users who have not yet authenticated. These access and identity tokens are not associated with a full user and have limited capabilities.

The default lifespan of these tokens is 30 days. You can set anonymous token's expiration (in days) to any value between 1 and 90.

Merge the anonymous token information

</br>

To configure your token lifetime, see our walkthrough on [configuring tokens](#configuring-tokens).


## Custom Claim Mapping
{: #claim-mapping}

You can map any user attribute to your access and identity tokens.
{: shortdesc}

Benefits:

You don't have to go to the user info endpoint or to the custom attributes because it's already in the token ... anything that your app may need to know about a user or what they can do is already in the token. Cut down on network calls.

Add scopes or roles for specific users. Invent your own scopes. Create

You have a lot of control over the way that your app is built. -> in the token is signed

More efficient assuming your data isn't massive.


Update your token configuration to fine-tune your expiration settings, enable or disable refresh and anonymous tokens, or customize access and ID token claims. If you already have custom settings that you want to keep, be sure to include them in your request. If a value is left blank then the default is used.

### Claim Sets

Default claims provided by {{site.data.keyword.appid_short_notm}} fall into several categories differentiated by their level of customization: core claims, restricted claims, and normalized claims.

#### Core claims
Registered claim name

If your claim is restricted we ignore it.

Certain fields in {{site.data.keyword.appid_short_notm}}'s access and identity tokens cannot be overridden by custom claim mappings. These *core claims* are defined by {{site.data.keyword.appid_short_notm}} and exist in all of its tokens.

The following fields are core claims of all access and identity tokens:

- iss
- aud
- sub
- iat
- exp
- amr
- tenant

#### Restricted claims

Restricted claims have limited customization depending on the token they are mapped to.

**Access Token**

Currently, the `scope` field is the only restricted access token claim. It cannot be overridden by custom mappings, but can be extended with your own scopes.

When the `scope` field is mapped to an access token, the value must be a string and cannot be prefixed by `appid_` or it will be ignored.

**Identity Token**

The `identities` and `oauth_clients` claims cannot be modified or overridden in identity tokens. 

### Normalized Claims

Each identity token contains the {{site.data.keyword.appid_short_notm}} normalized claims. These fields include: *name*, *email*, *picture*, *locale*, and *gender* and are directly mapped from your identity provider whenever available

The normalized claims cannot be explicitly omitted, but can be overridden by custom claim mappings.

## Claim Mapping Object
{: #claim-mapping-object}

Define the value of claim mapping
what you can and can't do
How do you use it?


Each claim mapping is defined by its data source object and the key identifying the claim to retrieve from it.

Custom claims are set for each token type separately and are sequentially applied. You can register up to 100 claims for each token to a maximum payload of 100KB.
{:tip}

<table>
    <thead>
      <th colspan=3><img src="images/idea.png" alt="Idea icon"/> Understanding the claim mapping object</th>
    </thead>
    <tbody>
      <tr>
        <td><code><em>source</em></code></td>
        <td>Required</td>
        <td>This property defines where the claim is sourced from. This can refer to the identity provider's user info or the user's {{site.data.keyword.appid_short_notm}} custom attributes. </br> </br> Options include: `saml`, `cloud_directory`, `facebook`, `google`, `appid_custom`, `ibmid`, `attributes`.</td>
      </tr>
      <tr>
        <td><code><em>sourceClaim</em></code></td>
        <td>Required</td>
        <td>Defines the source data's claim to map to your token. </td>
      </tr>
    </tbody>
  </table>

You can reference nested fields in your claim mappings using the dot syntax. `e.g. nested.attribute`
{:tip}

This can be merged with the above -> how do you take information from one of your identity providers and use



## Configuring {{site.data.keyword.appid_short_notm}} tokens
{: #configuring-tokens}

### Configuring Token Lifetime from the UI
{: #configuring-tokens-by-ui}

1. Navigate to your service dashboard.

2. Click the Identity Providers dropdown to view all of your options and select the **Manage** page.

3. Select the `Settings` tab to modify your tokens.

4. Use the GUI to set your Access, Refresh, and Anonymous token expiration.

### Configuring Tokens using the Management APIs
{: #configuring-tokens-by-api}

**Before you begin**

You will need:

1. Your {{site.data.keyword.appid_short_notm}} instance's tenant ID

2. Your IAM Token

**Setting up your claim mappings**

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
        <td>Object containing expiration time, `expires_in`, in minutes of your access and identity tokens. <br/> <br/> Defaults to 60 minutes. </td>
      </tr>
      <tr>
          <td><code><em>refresh</em></code></td>
          <td>Optional</td>
          <td>Object containing expiration time in days,of your refresh token. <br/> <br/> Expiration defaults to 30 days. </td>
      </tr>
      <tr>
          <td><code><em>anonymousAccess</em></code></td>
          <td>Optional</td>
          <td>Object containing expiration time,  `expires_in`, in days of your anonymous access/identity tokens. <br/> <br/> Expiration defaults to 30 days.
      </tr>
      <tr>
          <td><code><em>accessTokenClaims</em></code></td>
          <td>Optional</td>
          <td>An array of claim mapping objects. See section on the [claim mapping object](#claim-mapping-object) for details.</td>
      </tr>
      <tr>
          <td><code><em>idTokenClaims</em></code></td>
          <td>Optional</td>
          <td>An array of claim mapping objects. See section on the [claim mapping object](#claim-mapping-object) for details.</td>
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
