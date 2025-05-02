---

copyright:
  years: 2017, 2025
lastupdated: "2025-05-02"

keywords: well known endpoint, discovery endpoint, oidc, public keys, user information, claims, attributes, full profile, identity providers, app security, tokens

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
{:terraform: .ph data-hd-interface='terraform'}
{:release-note: data-hd-content-type='release-note'}


# OIDC discovery document
{: #discovery}

OpenID Connect supports a discovery protocol that contains information that you can use to configure your apps and authenticate users such as tokens and public keys.
{: shortdesc}


## Calling the endpoint
{: #call-wellknown}

You can obtain the discovery document and the information that it contains by calling the `.well-known` endpoint.
{: shortdesc}


### Where can I find the endpoint?
{: #wellknown-endpoint}

You can find the endpoint at the following URL:

```sh
https://<region>.appid.cloud.ibm.com/oauth/v4/<tenantID>/.well-known/openid-configuration
```
{: codeblock}

Learn more about the [available regions](/docs/appid?topic=appid-regions-endpoints).
{: tip}



### How do I call the endpoint?
{: #wellknown-endpoint-call}

To call the endpoint, you must have a valid tenant ID and you must hardcode the discovery document URI into your application code.

Check out the following sample cURL request:

```sh
curl -X GET "https://<region>.appid.cloud.ibm.com/oauth/v4/<tenantID>/.well-known/openid-configuration" -H "accept: application/json"
```
{: codeblock}

### What can I expect the call to return?
{: #wellknown-response}

The response that is returned looks similar to the following example:

```json
{
  "issuer": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6060b61",
  "authorization_endpoint": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6060b61/authorization",
  "token_endpoint": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6060b61/token",
  "jwks_uri": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6060b61/publickeys",
  "subject_types_supported": [
    "public"
  ],
  "id_token_signing_alg_values_supported": [
    "RS256"
  ],
  "userinfo_endpoint": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6060b61/userinfo",
  "scopes_supported": [
    "openid"
  ],
  "response_types_supported": [
    "code"
  ],
  "claims_supported": [
    "iss",
    "aud",
    "exp",
    "tenant",
    "iat",
    "sub",
    "nonce",
    "amr",
    "oauth_client"
  ],
  "grant_types_supported": [
    "authorization_code",
    "password",
    "refresh_token",
    "client_credentials",
    "urn:ietf:params:oauth:grant-type:jwt-bearer"
  ],
  "profiles_endpoint": "https://us-south.appid.cloud.ibm.com",
  "management_endpoint": "https://us-south.appid.cloud.ibm.com/management/v4/39a37f57-a227-4bfe-a044-93b6e6060b61",
  "service_documentation": "https://cloud.ibm.com/docs/appid?topic=appid-getting-started"
}
```
{: screen}

| Component | Description | 
|-----|----| 
| `issuer` | The location of the OIDC provider. |
| `authorization_endpoint` | The URL of the {{site.data.keyword.appid_short_notm}} OAuth 2.0 authorization endpoint. |
| `token_endpoint` | The URL of the {{site.data.keyword.appid_short_notm}} OAuth 2.0 token endpoint. |
| `jwks_uri` | The URL of the {{site.data.keyword.appid_short_notm}} web key set document. |
| `subject_types_supported` | A JSON array that contains a list of the subject identifier types that {{site.data.keyword.appid_short_notm}} supports. |
| `id_token_signing_alg_values_supported` | A JSON array that contains a list of the JWS signing algorithms that the {{site.data.keyword.appid_short_notm}} server supports. |
| `userinfo_endpoint` | The URL of the {{site.data.keyword.appid_short_notm}} `/userinfo` endpoint. |
| `scopes_supported` | A JSON array that contains a list of the OAuth 2.0 scope values that {{site.data.keyword.appid_short_notm}} supports. |
| `response_types_supported` | A JSON array that contains a list of the OAuth 2.0 response_type values that {{site.data.keyword.appid_short_notm}} supports. |
| `claims_supported` | A JSON array that contains a list of the claim names. |
| `grant_types_supported` | A JSON array that contains a list of the OAuth 2.0 grant type values that are supported. |
| `profiles_endpoint` | The URL of the {{site.data.keyword.appid_short_notm}} user profile endpoint. | 
   {: caption="The descriptions of components" caption-side="top"}
