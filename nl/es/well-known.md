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


# Utilización del punto final de descubrimiento de OpenID Connect
{: #discovery}

OpenID Connect ofrece soporte a un protocolo de descubrimiento que contiene información que puede utilizar para configurar las apps y autenticar usuarios como, por ejemplo, señales de acceso y claves públicas.
{: shortdesc}


## Llamada al punto final
{: #call-wellknown}

Puede obtener el documento de descubrimiento y la información que contiene llamando al punto final `.well-known`.
{: shortdesc}


**¿Dónde puedo encontrar el punto final?**

Encontrará el punto final en el URL siguiente:

  ```
  https://appid-oauth.[region].bluemix.net/oauth/v3/{tenantId}/.well-known/openid-configuration
  ```
  {: codeblock}

</br>

**¿Cómo puedo llamar al punto final?**

Para llamar al punto final debe tener un `tenantID` válido y debe proteger el URI del documento de descubrimiento en la aplicación.

Consulte la solicitud cURL de ejemplo siguiente:

  ```bash
  curl -X GET --header 'Accept: application/json'  'https://appid-oauth.ng.bluemix.net/oauth/v3/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/.well-known/openid-configuration'
  ```
  {:codeblock}

</br>

**¿Qué puedo esperar de la llamada que se devuelve?**

La respuesta debería tener un aspecto similar al siguiente:

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
      <th> Descripción </th>
    </tr>
    <tr>
    <td><code>issuer</code></td>
    <td>La ubicación del proveedor de OpenID Connect.</td>
    </tr>
    <tr>
      <td><code>authorization_endpoint</code></td>
      <td>El URL del punto final de autorización OAuth 2.0 de {{site.data.keyword.appid_short_notm}}.</td>
    </tr>
    <tr>
      <td><code>token_endpoint</code></td>
      <td>El URL del punto final de la señal OAuth 2.0 de {{site.data.keyword.appid_short_notm}}.</td>
    </tr>
    <tr>
      <td><code>jwks_uri</code></td>
      <td>El URL del documento del conjunto de claves web de {{site.data.keyword.appid_short_notm}}.</td>
    </tr>
    <tr>
      <td><code>subject_types_supported</code></td>
      <td>Una matriz JSON que contiene una lista de los tipos de identificador de sujeto que {{site.data.keyword.appid_short_notm}} soporta.</td>
    </tr>
    <tr>
      <td><code>id_token_signing_alg_values_supported</code></td>
      <td>Una matriz JSON que contiene una lista de algoritmos de firma JSON a los que el servidor de {{site.data.keyword.appid_short_notm}} ofrece soporte.</td>
    </tr>
    <tr>
      <td><code>userinfo_endpoint</code></td>
      <td>El URL del punto final de la información de usuario de {{site.data.keyword.appid_short_notm}}.</td>
    </tr>
    <tr>
      <td><code>scopes_supported</code></td>
      <td>Una matriz JSON que contiene una lista de los valores de ámbito de OAuth 2.0 a los que {{site.data.keyword.appid_short_notm}} ofrece soporte.</td>
    </tr>
    <tr>
      <td><code>response_types_supported</code></td>
      <td>Una matriz JSON que contiene una lista de los valores response_type de OAuth 2.0 a los que {{site.data.keyword.appid_short_notm}} ofrece soporte.</td>
    </tr>
    <tr>
      <td><code>claims_supported</code></td>
      <td>Una matriz JSON que contiene una lista de los nombres de reclamación.</td>
    </tr>
    <tr>
      <td><code>grant_types_supported</code></td>
      <td>Una matriz JSON que contiene una lista de valores de tipo de otorgamiento OAuth 2.0 a los que {{site.data.keyword.appid_short_notm}} ofrece soporte.</td>
    </tr>
    <tr>
      <td><code>profiles_endpoint</code></td>
      <td>El URL del punto final del perfil de usuario de {{site.data.keyword.appid_short_notm}}.</td>
    </tr>
  </table>

</br>
</br>


