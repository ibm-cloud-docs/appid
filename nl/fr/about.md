---

copyright:
  years: 2017
lastupdated: "2017-12-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


# A propos de
{: #about}

Vous pouvez utiliser {{site.data.keyword.appid_full}} pour ajouter l'authentification à vos applications et protèger vos ressources de back-end.
{:shortdesc}

## Pourquoi utiliser ce service ?
{: #reasons}

Pourquoi utiliser {{site.data.keyword.appid_short_notm}} ? Vérifiez si l'un des scénarios suivants répond à vos attentes.
{: shortdesc}

<table>
  <tr>
    <th> Scénario </th>
    <th> Raison </th>
  </tr>
  <tr>
    <td> Vous devez ajouter un mécanisme
d'[autorisation et d'authentification](/docs/services/appid/authorization.html) à vos applications mobiles et
web, mais vous n'avez pas d'expérience de la sécurité.
</td>
    <td> {{site.data.keyword.appid_short_notm}} facilite l'ajout d'une étape d'authentification à vos applications. Vous pouvez utiliser
le service pour communiquer avec des [fournisseurs d'identité](/docs/services/appid/identity-providers.html) afin de gérer l'accès à vos applications.
</td>
  </tr>
  <tr>
    <td> Vous voulez limiter l'accès à vos applications et ressources de back end. </td>
    <td> Le service vous permet de [protéger vos ressources](/docs/services/appid/protecting-resources.html) vis-à-vis
des utilisateurs authentifiés et des utilisateurs anonymes. </td>
  </tr>
  <tr>
    <td> Vous voulez générer des applications personnalisées pour vos utilisateurs. </td>
    <td> {{site.data.keyword.appid_short_notm}} vous permet de [stocker des données sur les utilisateurs](/docs/services/appid/user-profile.html),
telles que leurs préférences d'utilisation des applications ou des informations issues de leurs profils publics dans les réseaux sociaux.
Vous pouvez utiliser ces données pour vous assurer que vos utilisateurs bénéficient d'applications personnalisées. </td>
  </tr>
</table>


## Architecture
{: #architecture}

Avec {{site.data.keyword.appid_short_notm}}, vous pouvez ajouter un niveau
de sécurité à vos applications en demandant aux utilisateurs de se connecter.
Vous pouvez également utiliser le SDK du serveur pour protéger vos ressources de back-end.

Le diagramme suivant résume le fonctionnement du service {{site.data.keyword.appid_short_notm}}.

![{{site.data.keyword.appid_short_notm}} - Diagramme de l'architecture](/images/appid_architecture.png)

Figure 1. Diagramme de l'architecture {{site.data.keyword.appid_short_notm}}


<dl>
  <dt> Application </dt>
    <dd> SDK du serveur : vous pouvez protéger vos ressources de back-end hébergées sur {{site.data.keyword.Bluemix_notm}} et
vos applications web en utilisant le SDK du serveur. Celui-ci
extrait le jeton d'accès d'une demande et le valide avec {{site.data.keyword.appid_short_notm}}. </br>
    SDK du client : vous pouvez protéger vos applications mobiles avec le SDK du client Android ou iOS. Le
SDK du client communique avec vos ressources cloud pour démarrer le processus
d'authentification lorsqu'il détecte une demande d'autorisation.
</dd>
  <dt> {{site.data.keyword.Bluemix_notm}} </dt>
    <dd> App ID : une fois que l'authentification a réussi, {{site.data.keyword.appid_short_notm}} renvoie les jetons d'identité et d'accès à votre application. </br>
    Cloud Directory : les utilisateurs peuvent s'inscrire à votre service avec leur adresse e-mail et un mot de passe. Vous pouvez les gérer dans une liste visible dans l'interface utilisateur.</dd>
  <dt> Externe (tierce partie) </dt>
    <dd>  {{site.data.keyword.appid_short_notm}} reconnaît deux fournisseurs d'identité de réseaux sociaux : Facebook et Google+. Le service met en oeuvre une redirection
vers le fournisseur d'identité et accorde l'accès à votre application une fois l'utilisateur authentifié.
{{site.data.keyword.appid_short_notm}} vérifie les données d'identification sans accéder à la phrase de passe proprement dite.
</dd>
</dl>


## Flux de demandes
{: #request}

Le diagramme ci-dessous illustre le cheminement d'une demande entre le SDK du client et vos ressources de back-end et les fournisseurs d'identité.

![{{site.data.keyword.appid_short_notm}} - Flux d'une demande](/images/appidrequestflow.png)

Figure 2. Flux d'une demande {{site.data.keyword.appid_short_notm}}


* Le SDK client {{site.data.keyword.appid_short_notm}} soumet une demande à vos ressources de back end protégées par le SDK serveur {{site.data.keyword.appid_short_notm}}.
* Le SDK serveur {{site.data.keyword.appid_short_notm}} détecte les demandes dépourvues d'autorisation et renvoie une réponse HTTP 401 une portée d'autorisation.
* Le SDK client détecte automatiquement la réponse HTTP 401 et lance la procédure d'autorisation.
* Lorsque le SDK client contacte le service, le SDK serveur renvoie le widget de connexion si plusieurs fournisseurs d'identité ont été configurés. {{site.data.keyword.appid_short_notm}} appelle le fournisseur d'identité et lui présente son formulaire d'identification ou renvoie un code d'acceptation qui lui permet de s'authentifier si aucun fournisseur d'identité n'a été configuré.
* {{site.data.keyword.appid_short_notm}} demande à l'application client de s'authentifier en répondant à une demande d'authentification.
* Si un fournisseur d'identité est configuré, lorsque l'utilisateur se connecte, l'authentification est gérée par le flux OAuth correspondant.
* Si l'authentification se conclut par le même code d'accord, celui-ci est envoyé au noeud final du jeton. Le noeud final renvoie deux jetons : un jeton d'accès et un jeton d'identité. Dès lors, toutes les demandes effectuées avec le SDK client obtiennent un nouvel
en-tête d'autorisation.
* Le SDK client renvoie automatiquement la demande d'origine ayant déclenché le flux d'autorisation.
* Le SDK serveur extrait l'en-tête de l'autorisation depuis la demande, le valide auprès du service et octroie l'accès à une ressource de back end.

**Remarque** : les protocoles implémentés sont totalement compatibles avec Open Connect (OIDC).
