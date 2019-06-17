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


# Document de reconnaissance OIDC
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
https://{region}.appid.ibm.cloud.com/oauth/v4/{tenantId}/.well-known/openid-configuration
```
{: codeblock}

<table>
  <tr>
    <th>Région</th>
    <th>Noeud final</th>
  </tr>
  <tr>
    <td>Dallas</td>
    <td><code>us-south</code></td>
  </tr>
  <tr>
    <td>Francfort</td>
    <td><code>eu-de</code></td>
  </tr>
  <tr>
    <td>Sydney</td>
    <td><code>au-syd</code></td>
  </tr>
  <tr>
    <td>Londres</td>
    <td><code>eu-gb</code></td>
  </tr>
  <tr>
    <td>Tokyo</td>
    <td><code>jp-tok</code></td>
  </tr>
</table>



**Comment appelle-t-on le noeud final ?**

Pour effectuer un appel vers le noeud final, vous devez avoir un ID de locataire valide et vous devez coder en dur l'URI du document de reconnaissance dans votre code d'application.

Consultez l'exemple de demande cURL suivant :

```bash
curl -X GET "https://{region}.appid.cloud.ibm.com/oauth/v4/{tenant-id}/.well-known/openid-configuration" -H "accept: application/json"
```
{:codeblock}

**Que puis-je attendre en retour de l'appel ?**

La réponse qui est renvoyée est similaire à l'exemple suivant :

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
    <th> Composant </th>
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
    <td>Adresse URL du noeud final <code>/userinfo</code> de {{site.data.keyword.appid_short_notm}}.</td>
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


