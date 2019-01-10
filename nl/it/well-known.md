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
  https://appid-oauth.[region].bluemix.net/oauth/v3/{tenantId}/.well-known/openid-configuration
  ```
  {: codeblock}

</br>

**Come effettuo una chiamata all'endpoint?**

Per effettuare una chiamata all'endpoint devi avere un `tenantID` valido e devi impostare come hardcoded l'URI del documento di rilevamento nella tua applicazione.

Controlla la seguente richiesta cURL di esempio:

  ```bash
  curl -X GET --header 'Accept: application/json'  'https://appid-oauth.ng.bluemix.net/oauth/v3/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/.well-known/openid-configuration'
  ```
  {:codeblock}

</br>

**Cosa posso aspettarmi che venga restituito dalla chiamata?**

La risposta dovrebbe essere simile al seguente esempio:

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
      <td>Un array JSON che contiene un elenco di nomi dell'attestazione. </td>
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

</br>
</br>


