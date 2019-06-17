---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-21"

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


# Documento de descubrimiento de OIDC
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
https://{region}.appid.ibm.cloud.com/oauth/v4/{tenantId}/.well-known/openid-configuration
```
{: codeblock}

<table>
  <tr>
    <th>Región</th>
    <th>Punto final</th>
  </tr>
  <tr>
    <td>Dallas</td>
    <td><code>us-south</code></td>
  </tr>
  <tr>
    <td>Frankfurt</td>
    <td><code>eu-de</code></td>
  </tr>
  <tr>
    <td>Sídney</td>
    <td><code>au-syd</code></td>
  </tr>
  <tr>
    <td>Londres</td>
    <td><code>eu-gb</code></td>
  </tr>
  <tr>
    <td>Tokio</td>
    <td><code>jp-tok</code></td>
  </tr>
</table>



**¿Cómo puedo llamar al punto final?**

Para llamar al punto final debe tener un ID de arrendatario válido y debe incluir en el código de la aplicación el URI del documento de descubrimiento.

Consulte la solicitud cURL de ejemplo siguiente:

```bash
curl -X GET "https://{region}.appid.cloud.ibm.com/oauth/v4/{tenant-id}/.well-known/openid-configuration" -H "accept: application/json"
```
{:codeblock}

**¿Qué puedo esperar de la llamada que se devuelve?**

La respuesta que se devuelve es similar al ejemplo siguiente:

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
    <td>Una matriz JSON que contiene una lista de algoritmos de firma JWS a los que el servidor de {{site.data.keyword.appid_short_notm}} ofrece soporte.</td>
  </tr>
  <tr>
    <td><code>userinfo_endpoint</code></td>
    <td>El URL del punto final de {{site.data.keyword.appid_short_notm}} <code>/userinfo</code>.</td>
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


