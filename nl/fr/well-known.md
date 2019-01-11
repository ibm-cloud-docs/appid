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


# Utilisation du noeud final de reconnaissance OIDC
{: #discovery}

OpenID Connect prend en charge un protocole de reconnaissance contenant des informations que vous pouvez utiliser pour configurer vos applications et authentifier des utilisateurs tels que des jetons et des clés publiques.
{: shortdesc}


## Appel du noeud final
{: #call-wellknown}

Vous pouvez obtenir le document de reconnaissance et les informations qu'il contient en appelant le noeud final `.well-known`.
{: shortdesc}


**Où puis-je trouver le noeud final ?**

Vous pouvez trouver le noeud final à l'adresse URL suivante :

  ```
  https://appid-oauth.[region].bluemix.net/oauth/v3/{tenantId}/.well-known/openid-configuration
  ```
  {: codeblock}

</br>

**Comment appeler le noeud final ?**

Pour appeler le noeud final, vous devez disposer d'un ID titulaire `tenantID` valide et vous devez coder l'identificateur URI du document de reconnaissance dans votre application.

Consultez l'exemple de demande cURL suivant :

  ```bash
  curl -X GET --header 'Accept: application/json'  'https://appid-oauth.ng.bluemix.net/oauth/v3/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/.well-known/openid-configuration'
  ```
  {:codeblock}

</br>

**Que puis-je attendre en retour de l'appel ?**

La réponse doit ressembler à l'exemple suivant :

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
      <th> Composant</th>
      <th> Description </th>
    </tr>
    <tr>
    <td><code>issuer</code></td>
    <td>Emplacement du fournisseur OIDC.</td>
    </tr>
    <tr>
      <td><code>authorization_endpoint</code></td>
      <td>Adresse URL du noeud final d'autorisation OAuth 2.0 {{site.data.keyword.appid_short_notm}}.</td>
    </tr>
    <tr>
      <td><code>token_endpoint</code></td>
      <td>Adresse URL du noeud final de jeton OAuth 2.0 {{site.data.keyword.appid_short_notm}}.</td>
    </tr>
    <tr>
      <td><code>jwks_uri</code></td>
      <td>Adresse URL du document de jeu de clés Web {{site.data.keyword.appid_short_notm}}.</td>
    </tr>
    <tr>
      <td><code>subject_types_supported</code></td>
      <td>Tableau JSON contenant la liste des types d'identificateur de sujet pris en charge par {{site.data.keyword.appid_short_notm}}.</td>
    </tr>
    <tr>
      <td><code>id_token_signing_alg_values_supported</code></td>
      <td>Tableau JSON contenant la liste des algorithmes de signature JWS pris en charge par le serveur {{site.data.keyword.appid_short_notm}}.</td>
    </tr>
    <tr>
      <td><code>userinfo_endpoint</code></td>
      <td>Adresse URL du noeud final userinfo {{site.data.keyword.appid_short_notm}}.</td>
    </tr>
    <tr>
      <td><code>scopes_supported</code></td>
      <td>Tableau JSON contenant la liste des valeurs de portée OAuth 2.0 prises en charge par {{site.data.keyword.appid_short_notm}}.</td>
    </tr>
    <tr>
      <td><code>response_types_supported</code></td>
      <td>Tableau JSON contenant la liste des valeurs response_type OAuth 2.0 prises en charge par {{site.data.keyword.appid_short_notm}}.</td>
    </tr>
    <tr>
      <td><code>claims_supported</code></td>
      <td>Tableau JSON contenant la liste des noms de réclamations.</td>
    </tr>
    <tr>
      <td><code>grant_types_supported</code></td>
      <td>Tableau JSON contenant la liste des valeurs de type d'octroi OAuth 2.0 prises en charge par {{site.data.keyword.appid_short_notm}}.</td>
    </tr>
    <tr>
      <td><code>profiles_endpoint</code></td>
      <td>Adresse URL du noeud final de profil utilisateur {{site.data.keyword.appid_short_notm}}.</td>
    </tr>
  </table>

</br>
</br>


