---

copyright:
  years: 2017
lastupdated: "2017-06-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Jetons d'accès et d'identité
{: #access-and-identity}

{{site.data.keyword.appid_short}} utilise deux types de jeton : des jetons
d'accès et des jetons d'identité. Les jetons sont au format <a href="https://jwt.io/introduction/" target="_blank">Jeton Web JSON<img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.
{:shortdesc}


## Jeton d'accès
{: #access-tokens}

Le jeton d'accès permet la communication avec des [ressources de back end](/docs/services/appid/protecting-resources.html) qui sont protégées par les filtres d'autorisation
d'{{site.data.keyword.appid_short_notm}}. Il est conforme aux
spécifications JOSE (JavaScript Object Signing and Encryption) et son format est le
suivant :


```
Header: {
    "typ": "JOSE",
    "alg": "RS256",
}
Payload: {
    "iss": "appid-oauth.ng.bluemix.net",
    "exp": "1495562664",
    "aud": "a3b87400-f03b-4956-844e-a52103ef26ba",
    "amr": "facebook",
    "sub": "de6a17d2-693d-4a43-8ea2-2140afd56a22",
    "iat": "1495559064",
    "tenant": "9781974b-6a1c-46c3-aebf-32b7e9bbbaee",
    "scope": "appid_default appid_readprofile appid_readuserattr appid_writeuserattr",
}
```
{:screen}

<table>
<caption> Tableau 1. Explication des composants de jeton d'accès
</caption>
  <tr>
    <th> Composant
</th>
    <th> Description </th>
  </tr>
  <tr>
    <td> <i> typ </i> </td>
    <td> Type d'en-tête, en l'occurrence "JOSE". </td>
  </tr>
  <tr>
    <td> <i> alg </i> </td>
    <td> Algorithme utilisé, en l'occurrence "RS256". </td>
  </tr>
  <tr>
    <td> <i> iss </i> </td>
    <td> Serveur {{site.data.keyword.appid_short}} qui a émis le jeton ; spécifié
sous forme de chaîne ou d'adresse URL.
</td>
  </tr>
  <tr>
    <td> <i> sub </i> </td>
    <td> ID de l'utilisateur pour lequel le jeton est émis. </td>
  </tr>
  <tr>
    <td> <i> aud </i> </td>
    <td> ID client pour lequel le jeton est émis. </td>
  </tr>
  <tr>
    <td> <i> exp </i> </td>
    <td> Expiration de l'horodatage à partir de la date initiale (epoch).
</td>
  </tr>
  <tr>
    <td> <i> iat </i> </td>
    <td> Emission de l'horodatage à partir de la date initiale (epoch).
</td>
  </tr>
  <tr>
    <td> <i> tenant </i> </td>
    <td> ID titulaire pour lequel le jeton est émis.
</td>
  </tr>
  <tr>
    <td> <i> amr </i> </td>
    <td> Fournisseur d'identité utilisé pour l'authentification. Il peut s'agir de
<i>id_app_facebook</i> ou <i>id_app_google</i>. </td>
  </tr>
  <tr>
    <td> <i> scope </i> </td>
    <td> Portée pour laquelle le jeton est émis.</td>
  </tr>
</table>


## Jeton d'identité
{: #identity-tokens}

Le jeton d'identité contient des informations sur l'utilisateur, notamment son nom, son adresse électronique, son sexe, sa photo et son emplacement.

```
Header: {
    "typ": "JOSE",
    "alg": "RS256",
}
Payload: {
    "iss": "appid-oauth.ng.bluemix.net",
    "aud": "a3b87400-f03b-4956-844e-a52103ef26ba",
    "exp: "1495562664",
    "tenant": "9781974b-6a1c-46c3-aebf-32b7e9bbbaee",
    "iat": "1495559064",
    "name": "John Smith",
    "email": "js@mail.com",
    "gender", "male",
    "locale": "en",
    "picture": "https://url.to.photo",
    "sub": "de6a17d2-693d-4a43-8ea2-2140afd56a22",
    "identities": [
        "provider": "facebook"
        "id": "377440159275659",
        "amr: "facebook",
    ],
    "oauth_client":{
      "name": "BluemixApp",
      "type": "serverapp",
      "software_id": "cb638f8f-e24b-41d3-b770-23be158dd8e6.2b94e6bb-bac4-4455-8712-a43fa804d5cc.a3b87400-f03b-4956-844e-a52103ef26ba",
      "software_version": "1.0.0",
    }
}
```
{:screen}


<table>
<caption> Tableau 2. Explication des composants de jeton d'identité
</caption>
  <tr>
    <th> Composant
</th>
    <th> Description </th>
  </tr>
  <tr>
    <td> <i> name </i> </td>
    <td> Nom complet de l'utilisateur, tel qu'indiqué par le fournisseur d'identité. Il
doit être renvoyé. </td>
  </tr>
  <tr>
    <td> <i> email </i> </td>
    <td> Adresse électronique de l'utilisateur, telle qu'indiquée par le fournisseur
d'identité. Renvoyée uniquement si disponible. </td>
  </tr>
  <tr>
    <td> <i> gender </i> </td>
    <td> Sexe de l'utilisateur, tel qu'indiqué par le fournisseur d'identité, si
disponible.
</td>
  </tr>
  <tr>
    <td> <i> locale </i> </td>
    <td> Paramètres régionaux de l'utilisateur, tels qu'indiqués par le fournisseur
d'identité.
</td>
  </tr>
  <tr>
    <td> <i> picture </i> </td>
    <td> Adresse URL d'une image de l'utilisateur, si disponible.
</td>
  </tr>
  <tr>
    <td> <i> identities: </br> <ul><li> provider <li> id <li> amr </ul></i></td>
    <td> </br><ul><li> Fournisseur d'identité utilisé pour l'authentification. Cette
variable peut être <code>id_app_facebook</code>, <code>id_app_google</code> ou
<code>id_app_ibmid</code> et doit être renvoyée. <li> ID utilisateur unique, tel qu'indiqué
par un fournisseur d'identité. <li> Objet JSON qui doit être renvoyé par le fournisseur
d'identité.
</ul></i></td>
  </tr>
  <tr>
    <td> <i> oauth_client: </br> <ul><li> type <li> name <li> software_id <li> software_version</ul></i> </td>
    <td> </br><ul><li> Type d'application déterminé au cours de l'enregistrement du
client. Il peut s'agir de <i>serverapp</i> ou <i>mobileapp</i>. <li> Nom du client, tel
qu'indiqué au cours de l'enregistrement du client.
<li> ID de logiciel, tel qu'indiqué au cours de l'enregistrement du client. <li> Version
du logiciel utilisée au cours de l'enregistrement du client.
</ul></td>
  </tr>
</table>
