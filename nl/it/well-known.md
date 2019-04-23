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


# Utilizzo dell'endpoint di rilevamento OIDC
{: #discovery}

OpenID Connect supporta un protocollo di rilevamento che contiene delle informazioni che puoi utilizzare per configurare le tue applicazioni e autenticare gli utenti come ad esempio i token e le chiavi pubbliche.
{: shortdesc}


## Richiamo dell'endpoint
{: #call-wellknown}

Puoi ottenere il documento di rilevamento e le informazioni che contiene richiamando l'endpoint `.well-known`.
{: shortdesc}


**Dove posso trovare l'endpoint?**

Puoi trovare l'endpoint al seguente URL:

```
https://[region].appid.ibm.cloud.com/oauth/v4/{tenantId}/.well-known/openid-configuration
```
{: pre}

<table>
  <tr>
    <th>Regione</th>
    <th>Endpoint</th>
  </tr>
  <tr>
    <td>Dallas</td>
    <td><code>us-south</code></td>
  </tr>
  <tr>
    <td>Francoforte</td>
    <td><code>eu-de</code></td>
  </tr>
  <tr>
    <td>Sydney</td>
    <td><code>au-syd</code></td>
  </tr>
  <tr>
    <td>Londra</td>
    <td><code>eu-gb</code></td>
  </tr>
  <tr>
    <td>Tokyo</td>
    <td><code>jp-tok</code></td>
  </tr>
</table>



**Come effettuo una chiamata all'endpoint?**

Per effettuare una chiamata all'endpoint devi avere un `tenantID` valido e devi impostare come hardcoded l'URI del documento di rilevamento nella tua applicazione.

Controlla la seguente richiesta cURL di esempio:

```bash
curl -X GET "https://us-south.appid.cloud.ibm.com/oauth/v4/asd/.well-known/openid-configuration" -H "accept: application/json"
```
{:codeblock}

**Cosa posso aspettarmi che venga restituito dalla chiamata?**

La risposta dovrebbe essere simile al seguente esempio:

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
    <th> Descrizione </th>
  </tr>
  <tr>
  <td><code>issuer</code></td>
  <td>L'ubicazione del provider OIDC.</td>
  </tr>
  <tr>
    <td><code>authorization_endpoint</code></td>
    <td>L'URL dell'endpoint di autorizzazione OAuth 2.0 {{site.data.keyword.appid_short_notm}}.</td>
  </tr>
  <tr>
    <td><code>token_endpoint</code></td>
    <td>L'URL dell'endpoint del token OAuth 2.0 {{site.data.keyword.appid_short_notm}}.</td>
  </tr>
  <tr>
    <td><code>jwks_uri</code></td>
    <td>L'URL del documento della serie di chiavi web {{site.data.keyword.appid_short_notm}}.</td>
  </tr>
  <tr>
    <td><code>subject_types_supported</code></td>
    <td>Un array JSON che contiene un elenco di tipi di identificativo dell'oggetto supportati da {{site.data.keyword.appid_short_notm}}.</td>
  </tr>
  <tr>
    <td><code>id_token_signing_alg_values_supported</code></td>
    <td>Un array JSON che contiene un elenco di algoritmi di firma JWS supportati dal server {{site.data.keyword.appid_short_notm}}.</td>
  </tr>
  <tr>
    <td><code>userinfo_endpoint</code></td>
    <td>L'URL dell'endpoint delle informazioni sull'utente {{site.data.keyword.appid_short_notm}}.</td>
  </tr>
  <tr>
    <td><code>scopes_supported</code></td>
    <td>Un array JSON che contiene un elenco di valori dell'ambito OAuth 2.0 supportati da {{site.data.keyword.appid_short_notm}}.</td>
  </tr>
  <tr>
    <td><code>response_types_supported</code></td>
    <td>Un array JSON che contiene un elenco di valori del tipo di risposta OAuth 2.0 supportati da {{site.data.keyword.appid_short_notm}}.</td>
  </tr>
  <tr>
    <td><code>claims_supported</code></td>
    <td>Un array JSON che contiene un elenco di nomi dell'attestazione.</td>
  </tr>
  <tr>
    <td><code>grant_types_supported</code></td>
    <td>Un array JSON che contiene un elenco di valori del tipo di concessione OAuth 2.0 supportati da {{site.data.keyword.appid_short_notm}}.</td>
  </tr>
  <tr>
    <td><code>profiles_endpoint</code></td>
    <td>L'URL dell'endpoint del profilo utente {{site.data.keyword.appid_short_notm}}.</td>
  </tr>
</table>


