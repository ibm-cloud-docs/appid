---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}


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
  https://appid-oauth.[region].bluemix.net/oauth/v3/{tenantId}/.well-known/openid-configuration
  ```
  {: codeblock}

</br>

**Como eu faço a chamada para o terminal?**

Para fazer uma chamada para o terminal, deve-se ter um `tenantID` válido e codificar
permanentemente o URI do documento de descoberta em seu aplicativo.

Consulte a seguinte solicitação de cURL de amostra:

  ```bash
  curl -X GET --header 'Accept: application/json'  'https://appid-oauth.ng.bluemix.net/oauth/v3/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/.well-known/openid-configuration'
  ```
  {:codeblock}

</br>

**O que posso esperar que a chamada retorne?**

A resposta deve ser semelhante ao exemplo a seguir:

  ```bash
  {
    "issuer" : "appid-oauth.ng.bluemix.net",
    "authorization_endpoint": "https://appid-oauth.ng.bluemix.net/oauth/v3/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/authorization",
    "token_endpoint": "https://appid-oauth.ng.bluemix.net/oauth/v3/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/token",
    "jwks_uri": "https://appid-oauth.ng.bluemix.net/oauth/v3/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/publickeys",
    "subject_types_supported": [
      "public"
    ],
    "id_token_signing_alg_values_supported": [
      "RS256"
    ],
    "userinfo_endpoint": "https://appid-oauth.ng.bluemix.net/oauth/v3/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/userinfo",
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
    "profiles_endpoint": "https://appid-profiles.ng.bluemix.net",
    "service_documentation": "https://console.bluemix.net/docs/services/appid/index.html"
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

</br>
</br>


