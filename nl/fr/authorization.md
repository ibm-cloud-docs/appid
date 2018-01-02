---

copyright:
  years: 2017
lastupdated: "2017-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


# Autorisation et authentification
{: authorization}

L'autorisation est le processus par lequel vous accordez l'accès à vos applications.
Pour authentifier les utilisateurs,
le service {{site.data.keyword.appid_short}} utilise des jetons (tokens), des
filtres et un en-tête.
{: shortdesc}


## Identité OAuth
{: #oauth}

Lorsque le service appelle l'API de connexion OAuth,
{{site.data.keyword.appid_short_notm}} utilise les protocoles OAuth 2.0 et OpenID Connect (OIDC)
pour autoriser et authentifier l'appelant avec le fournisseur d'identité sélectionné. Après
l'authentification, l'identité est associée à un enregistrement
d'utilisateur
{{site.data.keyword.appid_short_notm}}. {{site.data.keyword.appid_short_notm}} renvoie un jeton d'accès qui peut être
utilisé pour accéder aux attributs de l'utilisateur, et un jeton d'identité qui
contient les informations d'identité communiquées par le fournisseur d'identité.
Un nouvel accès à ce même enregistrement d'utilisateur et à ses attributs peut être
effectué par n'importe quel client qui s'authentifie avec cette même identité.

## Jetons d'accès et d'identité

{{site.data.keyword.appid_short}} utilise deux types de jeton : des jetons d'accès et des jetons d'identité.
{:shortdesc}

**Remarque** : Les jetons sont au format <a href="https://jwt.io/introduction/" target="_blank">Jeton Web JSON<img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.


### Jeton d'accès
{: #access-tokens}

Les jetons d'accès permettent de communiquer avec des [ressources de back-end](/docs/services/appid/protecting-resources.html)
protégées par des filtres d'autorisation appliqués par App ID.
Ils sont conformes aux
spécifications JOSE (JavaScript Object Signing and Encryption).


Exemple de jeton :

```
Header: {
    "typ": "JOSE",
    "alg": "RS256",
}
Payload: {
    "iss": "appid-oauth.ng.bluemix.net",
    "exp": "1495562664",
    "aud": "a3b87400-f03b-4956-844e-a52103ef26ba",
    "amr": ["facebook"],
    "sub": "de6a17d2-693d-4a43-8ea2-2140afd56a22",
    "iat": "1495559064",
    "tenant": "9781974b-6a1c-46c3-aebf-32b7e9bbbaee",
    "scope": "appid_default appid_readprofile appid_readuserattr appid_writeuserattr",
}
```
{:screen}

<table>
<caption> Tableau 1. Explication des composants du jeton d'accès </caption>
  <tr>
    <th> Composant </th>
    <th> Description </th>
  </tr>
  <tr>
    <td><i> typ </i></td>
    <td> Type d'en-tête, en l'occurrence "JOSE". </td>
  </tr>
  <tr>
    <td><i> alg </i></td>
    <td> Algorithme utilisé, en l'occurrence "RS256". </td>
  </tr>
  <tr>
    <td><i> iss </i></td>
    <td> Serveur {{site.data.keyword.appid_short}} qui a émis le jeton ; spécifié
sous forme de chaîne ou d'adresse URL. </td>
  </tr>
  <tr>
    <td><i> sub </i></td>
    <td> ID de l'utilisateur auquel le jeton a été délivré. </td>
  </tr>
  <tr>
    <td><i> aud </i></td>
    <td> ID client pour lequel le jeton est émis. </td>
  </tr>
  <tr>
    <td><i> exp </i></td>
    <td> Horodatage d'expiration du jeton comptabilisé en secondes depuis l'époque Unix. </td>
  </tr>
  <tr>
    <td><i> iat </i></td>
    <td> Horodatage d'émission du jeton comptabilisé en secondes depuis l'époque Unix. </td>
  </tr>
  <tr>
    <td><i> tenant </i></td>
    <td> ID utilisateur unique émis avec le jeton. </td>
  </tr>
  <tr>
    <td><i> amr </i></td>
    <td> Fournisseur d'identité utilisé pour l'authentification. La valeur de cette variable peut être <i>appid_facebook</i>,
<i>appid_google</i> ou <i>cloud_directory</i>. </td>
  </tr>
  <tr>
    <td><i> scope </i></td>
    <td> Portée pour laquelle le jeton est émis. </td>
  </tr>
</table>


### Jetons d'identité
{: #identity-tokens}

Un jeton d'identité contient des informations sur l'utilisateur.
Ces informations peuvent être son nom, son adresse e-mail, son sexe et son emplacement.
Le jeton peut aussi contenir une URL pointant sur une image de l'utilisateur. 

Exemple de jeton :

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
        "id": "377440159275659"
    ],
    "amr": ["facebook"],
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
<caption> Tableau 2. Explication des composants de jeton d'identité </caption>
  <tr>
    <th> Composant </th>
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
disponible. </td>
  </tr>
  <tr>
    <td> <i> locale </i> </td>
    <td> Paramètres régionaux de l'utilisateur, tels qu'indiqués par le fournisseur
d'identité. </td>
  </tr>
  <tr>
    <td> <i> picture </i> </td>
    <td> Adresse URL d'une image de l'utilisateur, si disponible. </td>
  </tr>
  <tr>
    <td> <i> identities: </br> <ul><li> provider <li> id </ul></i></td>
    <td> </br><ul><li> Fournisseur d'identité utilisé pour l'authentification. La valeur de cette variable peut être
<code>appid_facebook</code>, <code>appid_google</code> ou <code>cloud_directory</code>, et sa présence dans le jeton
est obligatoire.
<li> ID utilisateur unique, tel qu'indiqué
par un fournisseur d'identité. <li> Objet JSON qui doit être renvoyé par le fournisseur
d'identité. </ul></li></td>
  </tr>
  <tr>
    <td> <i> oauth_client: </br> <ul><li> type </br><li> name <li> software_id <li> software_version<li> device_id <li>device_model<li>device_os<li>device_os_version </ul></i> </td>
    <td> </br><ul><li> Type d'application déterminé au cours de l'enregistrement du
client. Il peut s'agir de <em>serverapp</em> ou <em>mobileapp</em>. <li> Nom du client, tel
qu'indiqué au cours de l'enregistrement du client. <li> ID de logiciel, tel qu'indiqué au cours de l'enregistrement du client. <li> Version
du logiciel utilisée au cours de l'enregistrement du client. <li> ID d'appareil pour un client mobile. <li> Modèle d'appareil pour un client mobile. <li> Système d'exploitation d'appareil pour un client mobile.<li> Version du système d'exploitation d'appareil pour un client mobile.</ul></td>
  </tr>
</table>

## En-têtes
{: #auth-header}

Un en-tête d'autorisation est la combinaison des jetons retournés.
Pour {{site.data.keyword.appid_short}},
l'en-tête d'autorisation est composé de trois parties séparées par des espaces : Bearer, jeton d'accès et jeton d'identité.
Les parties Bearer et jeton d'accès sont obligatoires pour accorder l'accès à vos applications.
Le jeton d'identité est optionnel, son rôle étant principalement de stocker des informations sur ceux qui utilisent
votre application.


Exemple de structure d'en-tête :

```
Authorization=Bearer {jeton_d'accès} [{jeton_d'identité}]
```
{: screen}


## Filtres 
{: #auth-filter}

Le SDK serveur d'{{site.data.keyword.appid_short}} fournit des stratégies
pour protéger deux types de ressource : les API et les applications Web.
{:shortdesc}

La stratégie de protection de l'API renvoie une réponse HTTP 401 avec une liste de portées afin d'obtenir une autorisation pour un client non authentifié. La stratégie de protection d'application Web renvoie une réponse HTTP 302 suggérant une redirection. La redirection envoie un client non authentifié à la page de connexion hébergée par le service {{site.data.keyword.appid_short_notm}} ou directement
à la page de connexion d'un fournisseur d'identité, selon votre configuration.



### Stratégie d'API
{: #api}

La stratégie d'API s'attend à ce que les demandes contiennent un en-tête d'autorisation avec un jeton d'accès valide. 
La réponse peut également contenir un jeton d'identité, mais cela n'est pas obligatoire.


Si un jeton n'est pas valide ou a expiré, la stratégie d'API renvoie une erreur
HTTP 401 contenant les informations suivantes : www-Authenticate=Bearer scope="{portée}" error="{erreur}". Le composant `error` est facultatif.

Si la demande renvoie un jeton valide, le contrôle passe au middleware suivant et la propriété `appIdAuthorizationContext` est injectée dans l'objet de demande. Cette propriété contient les jetons d'accès et d'identité originaux, ainsi que les
informations de contenu décodées sous forme d'objets JSON ordinaires.


### Stratégie d'application Web
{: #web}

Lorsque la classe de stratégie d'application Web détecte des tentatives non authentifiées d'accès à une ressource protégée, elle redirige automatiquement le navigateur de l'utilisateur vers la page d'authentification. 
Si l'authentification aboutit, l'utilisateur est ramené à l'URL de rappel de
l'application web. Le service utilise la classe de stratégie d'application Web pour obtenir les jetons d'accès et d'identité. Après avoir obtenu ces jetons, la classe de stratégie d'application Web les stocke dans une session HTTP sous `WebAppStrategy.AUTH_CONTEXT`. Il revient à l'utilisateur de décider de stocker ou non les jetons d'accès et d'identité dans la base de données de l'application.


## Authentification progressive
{: #oauth}

{{site.data.keyword.appid_short_notm}} utilise les protocoles OAuth 2.0 et
OIDC pour authentifier et autoriser un utilisateur.
Après la phase d'authentification, l'identité de l'utilisateur est associée à un enregistrement d'utilisateur.
Le service retourne d'une part un jeton d'accès qui peut être
utilisé pour accéder aux attributs de l'utilisateur, d'autre part un jeton d'identité dans lequel figurent
des informations relatives à l'utilisateur, qui ont été communiquées par le fournisseur d'identité.
Un nouvel accès à cet enregistrement d'utilisateur et à ses attributs peut être
effectué par n'importe quel client qui s'authentifie avec cette même identité.

A présent, peut-être aimeriez-vous savoir s'il est possible de laisser à l'utilisateur le choix de
se connecter ou non ?
{{site.data.keyword.appid_short_notm}} utilise le principe
d'authentification progressive pour créer des [profils d'utilisateur](/docs/services/appid/user-profile.html),
même lorsque les utilisateurs sont anonymes.
Les informations contenues dans un tel profil peuvent ensuite être transférées dans un profil d'utilisateur connu, lorsque celui-ci choisit
de s'identifier en se connectant.


![Carte montrant le trajet d'un utilisateur inconnu devenant un utilisateur identifié.](/images/authenticationtrail.png)

Figure 2. Carte montrant le trajet menant au statut d'utilisateur identifié

Lorsqu'un utilisateur choisit de rester anonyme,
{{site.data.keyword.appid_short_notm}} crée un enregistrement d'utilisateur
ad hoc et appelle l'API de connexion OAuth, qui retourne des jetons d'accès anonyme et d'identité.
Grâce à ces jetons, l'application peut créer, lire, mettre
à jour et supprimer les attributs stockés dans l'enregistrement
d'utilisateur.
Par exemple, un utilisateur pourrait commencer immédiatement à ajouter des articles à un panier d'achat sans avoir à se connecter à l'application.



Lorsqu'un utilisateur choisit de se connecter à une application, il devient un utilisateur identifié.
Les informations le concernant sont obtenues du fournisseur d'identité par le biais duquel il choisit
de se connecter.
Les jetons d'accès et d'identité reçus contiennent ces informations.


Un utilisateur anonyme peut choisir de devenir un utilisateur identifié.
Mais comment cela fonctionne-t-il ?


Le jeton d'accès anonyme est passé à l'API de connexion.
Le service authentifie l'appel auprès d'un fournisseur d'identité.
Le service utilise le jeton d'accès pour trouver l'enregistrement d'utilisateur anonyme, puis il lui associe l'identité.
Les nouveaux jetons d'accès et d'identité contiennent les informations publiques partagées par
le fournisseur d'identité.
Une fois l'utilisateur identifié, son jeton d'accès anonyme n'est plus valide.
L'utilisateur garde toutefois la faculté d'accéder à ses attributs, car ceux-ci sont accessibles
avec le nouveau jeton.


**Remarque** : une identité ne peut être affectée à un enregistrement d'utilisateur anonyme que si elle n'a pas déjà été affectée à un autre utilisateur.
Si l'identité est déjà associée à un autre utilisateur
{{site.data.keyword.appid_short_notm}}, les jetons
contiennent les informations de l'enregistrement de cet autre utilisateur et donnent
accès à ses attributs.
Les utilisateurs anonymes précédents et leurs attributs ne sont pas
accessibles via le nouveau jeton.
Jusqu'à l'expiration du jeton, les informations sont toujours accessibles via le jeton d'accès anonyme. Pendant le développement,
vous pouvez choisir comment fusionner les attributs de l'utilisateur anonyme avec ceux de l'utilisateur
connu.

