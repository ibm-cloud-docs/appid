---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

keywords: authentication, authorization, identity, app security, secure, discovery endpoint, oidc, public keys, tokens, well known endpoint

subcollection: appid

---

{:new_window: target="_blank"}
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


# Usando o terminal de descoberta OIDC
{: #discovery}

A conexão OpenID suporta um protocolo de descoberta que contém informações que podem ser usadas para configurar seus
aplicativos e autenticar usuários, como tokens e chaves públicas.
{: shortdesc}


## Chamando o terminal
{: #call-wellknown}

É possível obter o documento de descoberta e as informações que ele contém chamando o terminal `.well-known`.
{: shortdesc}


**Onde posso localizar o terminal?**

É possível localizar o terminal na URL a seguir:

```
https://[region].appid.ibm.cloud.com/oauth/v4/{tenantId}/.well-known/openid-configuration
```
{: pre}

<table>
  <tr>
    <th>Região</th>
    <th>Ponto de Extremidade</th>
  </tr>
  <tr>
    <td>Dallas</td>
    <td><code> us-south </code></td>
  </tr>
  <tr>
    <td>Frankfurt</td>
    <td><code>eu-de</code></td>
  </tr>
  <tr>
    <td>Sydney</td>
    <td><code>au-syd</code></td>
  </tr>
  <tr>
    <td>London</td>
    <td><code>eu-gb</code></td>
  </tr>
  <tr>
    <td>Tóquio</td>
    <td><code>jp-tok</code></td>
  </tr>
</table>



**Como eu faço a chamada para o terminal?**

Para fazer uma chamada para o terminal, deve-se ter um `tenantID` válido e codificar
permanentemente o URI do documento de descoberta em seu aplicativo.

Consulte a seguinte solicitação de cURL de amostra:

```bash
curl -X GET "https://us-south.appid.cloud.ibm.com/oauth/v4/asd/.well-known/openid-configuration" -H "accept: application/json"
```
{:codeblock}

**O que posso esperar que a chamada retorne?**

A resposta deve ser semelhante ao exemplo a seguir:

```bash
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
  "service_documentation": "https://cloud.ibm.com/docs/services/appid?topic=appid-getting-started#getting-started"
}
```
{: screen}

<table>
  <tr>
    <th> Componente </th>
    <th> Descrição </th>
  </tr>
  <tr>
  <td><code>issuer</code></td>
  <td>O local do provedor OIDC.</td>
  </tr>
  <tr>
    <td><code>authorization_endpoint</code></td>
    <td>A URL do terminal de autorização do OAuth 2.0 do {{site.data.keyword.appid_short_notm}}.</td>
  </tr>
  <tr>
    <td><code>token_endpoint</code></td>
    <td>A URL do terminal do token do OAuth 2.0 do {{site.data.keyword.appid_short_notm}}.</td>
  </tr>
  <tr>
    <td><code>jwks_uri</code></td>
    <td>A URL do documento do conjunto de chaves da web do {{site.data.keyword.appid_short_notm}}.</td>
  </tr>
  <tr>
    <td><code>subject_types_supported</code></td>
    <td>Uma matriz JSON que contém uma lista dos tipos de identificadores de assunto que o {{site.data.keyword.appid_short_notm}} suporta.</td>
  </tr>
  <tr>
    <td><code>id_token_signing_alg_values_supported</code></td>
    <td>Uma matriz JSON que contém uma lista dos algoritmos de assinatura JWS que o servidor {{site.data.keyword.appid_short_notm}} suporta.</td>
  </tr>
  <tr>
    <td><code>userinfo_endpoint</code></td>
    <td>A URL do terminal userinfo do {{site.data.keyword.appid_short_notm}}.</td>
  </tr>
  <tr>
    <td><code>scopes_supported</code></td>
    <td>Uma matriz JSON que contém uma lista dos valores de escopo do OAuth 2.0 que
o {{site.data.keyword.appid_short_notm}} suporta.</td>
  </tr>
  <tr>
    <td><code>response_types_supported</code></td>
    <td>Uma matriz JSON que contém uma lista dos valores response_type do OAuth 2.0 que o {{site.data.keyword.appid_short_notm}} suporta.</td>
  </tr>
  <tr>
    <td><code>claims_supported</code></td>
    <td>Uma matriz JSON que contém uma lista dos nomes de solicitações.</td>
  </tr>
  <tr>
    <td><code>grant_types_supported</code></td>
    <td>Uma matriz JSON que contém uma lista dos valores de tipo de concessão do OAuth 2.0 que o {{site.data.keyword.appid_short_notm}} suporta.</td>
  </tr>
  <tr>
    <td><code>profiles_endpoint</code></td>
    <td>A URL do terminal do perfil do usuário do {{site.data.keyword.appid_short_notm}}.</td>
  </tr>
</table>


