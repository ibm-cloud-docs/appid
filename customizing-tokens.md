---

copyright:
  years: 2017, 2019
lastupdated: "2019-11-01"

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

With {{site.data.keyword.appid_short_notm}}, tokens are used to identify users and secure your resources. You can choose to customize the information that is injected in to the tokens by the service. By injecting the information into your tokens, it's available to your application at run time without you having to configure extra network calls. For more information about tokens and how they're used in {{site.data.keyword.appid_short_notm}}, see [Understanding tokens](/docs/services/appid?topic=appid-tokens).
{: shortdesc}


By customizing your token configuration, you can ensure that your security and user experience needs are met. However, should a token ever become compromised, a malicious user might have more information or time that can be used to affect your application. Be sure that you understand the security implications of the customizations that you want to make before you make them. 
{: important}


## Understanding custom claims mapping
{: #custom-claims}

A claim is a statement that an entity makes about itself or on behalf of someone else. For example, if you signed into an application by using an identity provider, the provider would send the application a group of claims or statements about you to the app so that it can group with information that it already knows about you. This way, when you sign in, the app is set up with your information, in the way that you configured it. 


### What types of claims can I define?
{: #custom-claim-types}

The claims that are provided by {{site.data.keyword.appid_short_notm}} fall into several categories that are differentiated by their level of customization.

<dl>
  <dt>Normalized claims</dt>
    <dd>In each identity token, there is a set of claims that is recognized by {{site.data.keyword.appid_short_notm}} as normalized. When available, the claims are mapped directly from your identity provider to the token by default. The claims can't be explicitly omitted but they can be overwritten in your token by custom claims. The claims include <code>name</code>, <code>email</code>, <code>picture</code>, and <code>locale</code>.</dd>
  <dt>Restricted claims</dt>
    <dd>Restricted claims are those that have limited customization possibilities and cannot be overwritten by custom mappings. For an access token, <code>scope</code> is the only restricted claim. Although it cannot be overwritten, it can be extended with your own scope. When a scope is mapped to an access token, the value must be a string and cannot be prefixed by <code>appid_</code> or it is ignored. In identity tokens, the claims <code>identities</code> and <code>oauth_clients</code> cannot be modified or overwritten.</dd>
  <dt>Registered claims</dt>
    <dd>Registered claims are present in your access and identity tokens and are defined by {{site.data.keyword.appid_short_notm}}. They <b>cannot</b> be overridden by custom mappings. These claims are ignored by the service and include <code>iss</code>, <code>aud</code>, <code>sub</code>, <code>iat</code>, <code>exp</code>, <code>amr</code>, and <code>tenant</code>.</dd>
</dl>

Defining a claim for your token does not change or eliminate [the attribute](/docs/services/appid?topic=appid-profiles). It changes the information that is present in the token at run time.
{: note}


### How are claims mapped to tokens?
{: #custom-claims-mapping}

Each mapping is defined by a data source object and a key that is used to retrieve the claim. You can inject up to 100 claims into each token if the maximum payload remains less than 100 KB. If you want to use nested claims, you can include them by using the dot syntax. For example, `nested.attribute`.

The claims are set for each token separately and are sequentially applied as shown in the following example. 

```
{
  "accessTokenClaims": [
    {
      "source": "saml",
      "sourceClaim": "moderator"
    }
    {
      "source": "saml",
      "sourceClaim": "viewer"
    }
  ],
  "idTokenClaims": [
    {
      "source": "saml",
      "sourceClaim": "attributes.uid"
    }
    {
      "source": "saml",
      "sourceClaim": "Name"
    }
    {
      "source": "saml",
      "sourceClaim": "Country"
    }
  ]
}
```
{: screen}


<table>
  <caption>Table 1. Claims mapping variables explained</caption>
    <tr>
      <th>Object</th>
      <th>Description</th>
    </tr>
    <tr>
      <td><code><em>source</em></code></td>
      <td>Defines the source of the claim. Options include: <code>saml</code>, <code>cloud_directory</code>, <code>facebook</code>, <code>google</code>, <code>appid_custom</code>, and <code>attributes</code>.</td>
    </tr>
    <tr>
      <td><code><em>sourceClaim</em></code></td>
      <td>Defines the claim as provided by the source. It can refer to the identity provider's user information or the user's {{site.data.keyword.appid_short_notm}} custom attributes.</td>
    </tr>
</table>



## Configuring tokens
{: #configuring-tokens}

With the API, you can customize the information that is returned in your {{site.data.keyword.appid_short_notm}} tokens.
{: shortdesc}

If you want to configure the lifespan of your token, you can quickly make the changes through the service dashboard. For more information, see [Managing authentication](/docs/services/appid?topic=appid-managing-idp#idp-token-lifetime).
{: tip}

1. Obtain an IAM token. For more information, see the [IAM documentation](/docs/iam?topic=iam-getstarted#getstarted).

  1. In the IBM Cloud dashboard, click **Manage > Access (IAM)**.
  2. Select **IBM Cloud API keys**.
  3. Click **Create an IBM Cloud API key**.
  4. Give your key a name and describe it. Click **Create**. A screen displays with your key.
  5. Click **Copy** or download your key. When you close the screen, you can no longer access the key.
  6. Make the following cURL request with the API key that you created.

    ```
    curl -k -X POST \
    --header "Content-Type: application/x-www-form-urlencoded" \
    --header "Accept: application/json" \
    --data-urlencode "grant_type=urn:ibm:params:oauth:grant-type:apikey" \
    --data-urlencode "apikey=<api_key>" \
    "https://iam.cloud.ibm.com/identity/token"
    ```
    {: codeblock}

2. Get the tenant ID for your instance of the service. You can find the value in either your service or application credentials.

3. Make a PUT request to the `/config/tokens` endpoint with your token configuration.

  Header:
  ```
  PUT -X "https://<region>.appid.cloud.ibm.com/management/v4/<tenantID>/tokens"
    -H Authorization: 'Bearer <IAM_Token>'
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
    <caption>Table 2. Understanding the token configuration</caption>
    <tr>
      <th>Variable</th>
      <th>Description</th>
    </tr>
    <tr>
      <td><code>access: expires_in</code></td>
      <td>The length of time for which access tokens are valid. The smaller the value, the more protection that you have in cases of token theft. The value is provided in seconds and can be any whole number in range <code>300</code> and <code>86400</code>. The default value is <code>3600</code>.
    </tr>
    <tr>
      <td><code>refresh: expires_in</code></td>
      <td>The length of time for which refresh tokens are valid. The smaller the value, the more protection that you have in cases of token theft. The value is provided in seconds and can be any whole number in range <code>86400</code> and <code>7776000</code>. The default value is <code>2592000</code> (30 days).</td>
    </tr>
    <tr>
      <td><code>anonymousAccess</code></td>
      <td>The length of time for which an anonymous token is valid. Anonymous tokens are assigned to users the moment they begin interacting with your app. When a user signs in, the information in the anonymous token is then transferred to the token associated with the user. The value is provided in seconds and can be any whole number in range <code>86400</code> and <code>7776000</code>. The default value is <code>2592000</code> (30 days).</td>
    </tr>
    <tr>
      <td><code>accessTokenClaims</code></td>
      <td>An array that contains the objects that are created when claims that are related to access tokens are mapped.</td>
    </tr>
    <tr>
      <td><code>idTokenClaims</code></td>
      <td>An array that contains the objects that are created when claims that are related to identity tokens are mapped.</td>
    </tr>
  </table>

  You must set the token lifetime in each request that you make. If a value is not set, then the default is used. Each customization request overwrites what is previously configured. Note that the lifetime configuration specifications are different in the API than they are in the service dashboard.
  {: note}


