---

copyright:
  years: 2017, 2021
lastupdated: "2021-09-23"

keywords: user information, tokens, custom tokens, secure resources, authorization, identity, authentication, claims, oauth, claims mapping, attributes, app security, access, runtime

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


# Customizing tokens
{: #customizing-tokens}

With {{site.data.keyword.appid_short_notm}}, tokens are used to identify users and secure your resources. You can choose to customize the information that is injected in to the tokens by the service. By injecting the information into your tokens, it's available to your application at run time without you having to configure extra network calls. For more information about tokens and how they're used in {{site.data.keyword.appid_short_notm}}, see [Understanding tokens](/docs/appid?topic=appid-tokens).
{: shortdesc}


By customizing your token configuration, you can ensure that your security and user experience needs are met. However, should a token ever become compromised, a malicious user might have more information or time that can be used to affect your application. Be sure that you understand the security implications of the customizations that you want to make before you make them. 
{: important}


## Understanding custom claims mapping
{: #custom-claims}

A claim is a statement that an entity makes about itself or on behalf of someone else. For example, if you signed into an application by using an identity provider, the provider would send the application a group of claims or statements about you to the app so that it can group with information that it already knows about you. This way, when you sign in, the app is set up with your information, in the way that you configured it. 


### What types of claims can I define?
{: #custom-claim-types}

The claims that are provided by {{site.data.keyword.appid_short_notm}} fall into several categories that are differentiated by their level of customization.

Normalized claims
:   In each identity token, there is a set of claims that is recognized by {{site.data.keyword.appid_short_notm}} as normalized. When available, the claims are mapped directly from your identity provider to the token by default. The claims can't be explicitly omitted but they can be overwritten in your token by custom claims. The claims include `name`, `email`, `picture`, and `locale`.

Restricted claims
:   Restricted claims are those that have limited customization possibilities and cannot be overwritten by custom mappings. For an access token, `scope` is the only restricted claim. Although it cannot be overwritten, it can be extended with your own scope. When a scope is mapped to an access token, the value must be a string and cannot be prefixed by `appid_` or it is ignored. In identity tokens, the claims `identities` and `oauth_clients` cannot be modified or overwritten.

Registered claims
:   Registered claims are present in your access and identity tokens and are defined by {{site.data.keyword.appid_short_notm}}. They **cannot** be overridden by custom mappings. These claims are ignored by the service and include `iss`, `aud`, `sub`, `iat`, `exp`, `amr`, and `tenant`.

Defining a claim for your token does not change or eliminate [the attribute](/docs/appid?topic=appid-profiles). It changes the information that is present in the token at run time.
{: note}


### How are claims mapped to tokens?
{: #custom-claims-mapping}

Each mapping is defined by a data source object and a key that is used to retrieve the claim. You can inject up to 100 claims into each token if the maximum payload remains less than 100 KB. If you want to use nested claims, you can include them by using the dot syntax. For example, `nested.attribute`.

The claims are set for each token separately and are sequentially applied as shown in the following example. 

```json
{
  "accessTokenClaims": [
    {
      "source": "saml",
      "sourceClaim": "moderator"
    },
    {
      "source": "saml",
      "sourceClaim": "viewer",
      "destinationClaim": "reader"
    }
  ],
  "idTokenClaims": [
    {
      "source": "saml",
      "sourceClaim": "attributes.uid"
    },
    {
      "source": "saml",
      "sourceClaim": "Name",
      "destinationClaim": "firstName"
    },
    {
      "source": "saml",
      "sourceClaim": "Country"
    }
  ]
}
```
{: screen}

| Object | Description | 
|-----|----| 
| `source` | Defines the source of the claim. Options include: `saml`, `cloud_directory`, `facebook`, `google`, `appid_custom`, and `attributes`. |
| `sourceClaim` | Defines the claim as provided by the source. It can refer to the identity provider's user information or the user's {{site.data.keyword.appid_short_notm}} custom attributes. |
| `destinationClaim` | Optional: Defines the custom attribute that can override the current claim in token. |
{: caption="Table 1. Claims mapping variables explained" caption-side="top"}


## Configuring tokens
{: #configuring-tokens}

With the API, you can customize the information that is returned in your {{site.data.keyword.appid_short_notm}} tokens.
{: shortdesc}

If you want to configure the lifespan of your token, you can quickly make the changes through the service dashboard. For more information, see [Managing authentication](/docs/appid?topic=appid-managing-idp#idp-token-lifetime).
{: tip}

1. In terminal, run the following command to obtain an API key.

  ```
  ibmcloud iam api-key-create NAME [-d DESCRIPTION] [-f, --file FILE]
  ```
  {: codeblock}

  | Option | Description |
  | ------ | ----------- |
  | `NAME` | The name that you want to give your key. For example, `myKey`. | 
  | `DESCRIPTION` | A description of the key or its use. For example, `"This is my App ID API key"`. |
  | `FILE` | The location where you want to store your key. For example, `key_file`. | 
  {: caption="Table 2. Understanding the creating an API key command options" caption-side="top"}

2. Obtain an IAM token by using the API key that you got in the previous step.

  ```
  curl -k -X POST "https://iam.cloud.ibm.com/identity/token" \
  --header "Content-Type: application/x-www-form-urlencoded" \
  --header "Accept: application/json" \
  --data-urlencode "grant_type=urn:ibm:params:oauth:grant-type:apikey" \
  --data-urlencode "apikey={api_key}"
  ```
  {: codeblock}

3. Get the tenant ID for your instance of the service. You can find the value in either your service or application credentials.

4. Make a PUT request to the `/config/tokens` endpoint with your token configuration.

  ```sh
  curl -X PUT "https://$REGION.appid.cloud.ibm.com/management/v4/$TENANT_ID/config/tokens" \
  -H 'Content-Type: application/json' \
  -H "Authorization: Bearer $IAM_TOKEN" \
  -d '{
      "access": {
          "expires_in": 3600
      },
      "refresh": {
          "enabled": true,
          "expires_in": 2592001
      },
      "anonymousAccess": {
          "enabled": false
      },
      "accessTokenClaims": [
          {
            "source": "roles"
          },
          {
            "source": "saml",
            "sourceClaim": "name_id",
            "destinationClaim": "id"
          }
      ],
      "idTokenClaims": [
          {
            "source": "saml",
            "sourceClaim": "attributes.uid"
          }
      ]
  }'
  ```
  {: codeblock}

  | Variable | Description |
  | -------- | ----------- |
  | `access: expires_in` | The length of time for which access tokens are valid. The smaller the value, the more protection that you have in cases of token theft. The value is provided in seconds and can be any whole number in range `300` and `86400`. The default value is `3600`. |
  | `refresh: expires_in` | The length of time for which refresh tokens are valid. The smaller the value, the more protection that you have in cases of token theft. The value is provided in seconds and can be any whole number in range `86400` and `7776000`. The default value is `2592000` (30 days). |
  | `anonymousAccess` | The length of time for which an anonymous token is valid. Anonymous tokens are assigned to users the moment they begin interacting with your app. When a user signs in, the information in the anonymous token is then transferred to the token associated with the user. The value is provided in seconds and can be any whole number in range `86400` and `7776000`. The default value is `2592000` (30 days). |
  | `accessTokenClaims` | An array that contains the objects that are created when claims that are related to access tokens are mapped. You might want to include information about roles or specific attributes that are returned by a user's identity provider of choice. Note: If you're already using a custom claim with the title "roles" from your identity provider, be sure to use a destination claim in order to see both values. |
  | `idTokenClaims` | An array that contains the information that is present in tokens when you map claims to identity tokens. Depending on your configuration, you might also choose to have "roles" be present in your identity token. |
  {: caption="Table 3. Understanding the token configuration" caption-side="top"}

  You must set the token lifetime in each request that you make. If a value is not set, then the default is used. Each customization request overwrites what is previously configured. Note that the lifetime configuration specifications are different in the API than they are in the service dashboard.
  {: note}

5. After the token is returned and you [decode](/docs/appid?topic=appid-token-validation) it, you see a result similar to the following example:

  ```
  {
    "sub" : "1234567890",
    "name" : "John Doe",
    "exp" : 1564566,
    "roles" : ["admin", "manager"],
    "id": "name_id_from_saml",
    "attributes.uid": "uid_from_saml"
    ...
  }
  ```
  {: screen}

