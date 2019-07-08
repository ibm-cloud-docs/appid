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


# OIDC-Erkennungsdokument
{: #discovery}

OpenID Connect unterstützt ein Erkennungsprotokoll, das Informationen enthält, die Sie zum Konfigurieren Ihrer Anwendungen und zur Authentifizierung von Benutzern verwenden können (z. B. Tokens und öffentliche Schlüssel).
{: shortdesc}


## Endpunkt aufrufen
{: #call-wellknown}

Sie können das Erkennungsdokument und die darin enthaltenen Informationen abrufen, indem Sie den Endpunkt `.well-known` aufrufen.
{: shortdesc}


**Wo befindet sich der Endpunkt?**

Sie finden den Endpunkt unter der folgenden URL:

```
https://{region}.appid.ibm.cloud.com/oauth/v4/{tenantId}/.well-known/openid-configuration
```
{: codeblock}

<table>
  <tr>
    <th>Region</th>
    <th>Endpunkt</th>
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
    <td>Sydney</td>
    <td><code>au-syd</code></td>
  </tr>
  <tr>
    <td>London</td>
    <td><code>eu-gb</code></td>
  </tr>
  <tr>
    <td>Tokio</td>
    <td><code>jp-tok</code></td>
  </tr>
</table>



**Wie rufe ich den Endpunkt auf?**

Um den Endpunkt aufzurufen, müssen Sie über eine gültige Tenant-ID verfügen und den URI des Erkennungsdokuments in der Anwendung fest codieren.

Sehen Sie sich die folgende cURL-Beispielanforderung an:

```bash
curl -X GET "https://{region}.appid.cloud.ibm.com/oauth/v4/{tenant-id}/.well-known/openid-configuration" -H "accept: application/json"
```
{:codeblock}

**Was gibt der Aufruf zurück?**

Die zurückgegebene Antwort ähnelt der im folgenden Beispiel: 

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
    <th> Komponente </th>
    <th> Beschreibung </th>
  </tr>
  <tr>
  <td><code>issuer</code></td>
  <td>Die Position des OIDC-Providers.</td>
  </tr>
  <tr>
    <td><code>authorization_endpoint</code></td>
    <td>Die URL des {{site.data.keyword.appid_short_notm}} OAuth 2.0-Autorisierungsendpunkts.</td>
  </tr>
  <tr>
    <td><code>token_endpoint</code></td>
    <td>Die URL des {{site.data.keyword.appid_short_notm}} OAuth 2.0-Tokenendpunkts.</td>
  </tr>
  <tr>
    <td><code>jwks_uri</code></td>
    <td>Die URL des Dokuments mit dem {{site.data.keyword.appid_short_notm}}-Webschlüsselsatz.</td>
  </tr>
  <tr>
    <td><code>subject_types_supported</code></td>
    <td>Ein JSON-Array, das eine Liste der Subjekt-ID-Typen enthält, die von {{site.data.keyword.appid_short_notm}} unterstützt werden.</td>
  </tr>
  <tr>
    <td><code>id_token_signing_alg_values_supported</code></td>
    <td>Ein JSON-Array, das eine Liste der JWS-Signaturalgorithmen enthält, die vom {{site.data.keyword.appid_short_notm}}-Server unterstützt werden.</td>
  </tr>
  <tr>
    <td><code>userinfo_endpoint</code></td>
    <td>Die URL des {{site.data.keyword.appid_short_notm}}-Endpunkts <code>/userinfo</code>. </td>
  </tr>
  <tr>
    <td><code>scopes_supported</code></td>
    <td>Ein JSON-Array, das eine Liste der OAuth 2.0-'scope'-Werte enthält, die von {{site.data.keyword.appid_short_notm}} unterstützt werden.</td>
  </tr>
  <tr>
    <td><code>response_types_supported</code></td>
    <td>Ein JSON-Array, das eine Liste der OAuth 2.0-'response_type'-Werte enthält, die von {{site.data.keyword.appid_short_notm}} unterstützt werden.</td>
  </tr>
  <tr>
    <td><code>claims_supported</code></td>
    <td>Ein JSON-Array, das eine Liste mit den Namen von Anforderungen (sog. Claims) enthält.</td>
  </tr>
  <tr>
    <td><code>grant_types_supported</code></td>
    <td>Ein JSON-Array, das eine Liste der OAuth 2.0-Grant-Typ-Werte enthält, die von {{site.data.keyword.appid_short_notm}} unterstützt werden.</td>
  </tr>
  <tr>
    <td><code>profiles_endpoint</code></td>
    <td>Die URL des {{site.data.keyword.appid_short_notm}}-Benutzerprofilendpunkts.</td>
  </tr>
</table>


