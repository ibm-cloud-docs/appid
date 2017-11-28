---

copyright:
  years: 2017
lastupdated: "2017-11-09"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


# A propos de
{: #about}

{{site.data.keyword.appid_full}} vous offre la possibilité de gérer l'accès à vos applications de façon conviviale.
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
    <td> Vous voulez apporter de la sécurité à vos applications Web et mobiles. </td>
    <td> {{site.data.keyword.appid_short_notm}} facilite l'ajout d'une étape d'authentification à vos applications. Vous pouvez utiliser le service pour communiquer avec des fournisseurs d'identité afin de gérer l'accès à vos applications. </td>
  </tr>
  <tr>
    <td> Vous voulez limiter l'accès à vos applications et ressources de back end. </td>
    <td> Le service vous permet de protéger vos ressources pour les utilisateurs authentifiés et anonymes. </td>
  </tr>
  <tr>
    <td> Vous voulez générer des applications personnalisées pour vos utilisateurs. </td>
    <td> {{site.data.keyword.appid_short_notm}} vous permet de stocker des données utilisateur, telles que les préférences d'application ou des informations de leur profil social public. Vous pouvez utiliser ces données pour vous assurer que vos utilisateurs bénéficient d'applications personnalisées. </td>
  </tr>
</table>

**Remarque** : les protocoles implémentés sont totalement compatibles avec Open Connect (OIDC).


## Architecture
{: #architecture}

Avec {{site.data.keyword.appid_short_notm}}, vous pouvez ajouter un niveau de sécurité à vos applications en demandant aux utilisateurs de se connecter. Vous pouvez également utiliser le SDK serveur pour protéger vos ressources de back end.

Le diagramme suivant résume le fonctionnement du service {{site.data.keyword.appid_short_notm}}.


![Diagramme de l'architecture {{site.data.keyword.appid_short_notm}}](/images/appid_architecture2.png)


Figure 1. Diagramme de l'architecture {{site.data.keyword.appid_short_notm}}



<dl>
  <dt> Application </dt>
    <dd> Le SDK client fournit une catégorie de demande pour communiquer avec vos ressources de cloud. Le SDK client démarre automatiquement le processus d'authentification lorsqu'il détecte une demande
d'autorisation. </dd>
  <dt> {{site.data.keyword.Bluemix_notm}} </dt>
    <dd>  Le SDK serveur extrait de la demande le jeton d'accès et le valide auprès d'{{site.data.keyword.appid_short_notm}}. Une fois que l'authentification a réussi, {{site.data.keyword.appid_short_notm}} renvoie les jetons d'identité et d'accès à votre application. </dd>
  <dt> Fournisseurs d'identité </dt>
    <dd> Le service met en oeuvre une redirection vers le fournisseur d'identité et vérifie l'authentification pour accorder l'accès à votre application. {{site.data.keyword.appid_short_notm}} vérifie les données d'identification sans avoir accès à la phrase de passe réelle. </dd>
</dl>


## Flux de demandes
{: #request}

Le diagramme ci-dessous illustre un flux de demandes depuis le SDK client vers votre application de back-end et les fournisseurs d'identité.

Flux de demandes ![{{site.data.keyword.appid_short_notm}}](/images/appidrequestflow.png)

Figure 2. Flux de demandes {{site.data.keyword.appid_short_notm}}


* Le SDK client {{site.data.keyword.appid_short_notm}} soumet une demande à vos ressources de back end protégées par le SDK serveur {{site.data.keyword.appid_short_notm}}.
* Le SDK serveur {{site.data.keyword.appid_short_notm}} détecte les demandes dépourvues d'autorisation et renvoie une réponse HTTP 401 une portée d'autorisation.
* Le SDK client détecte automatiquement la réponse HTTP 401 et lance la procédure d'autorisation.
* Lorsque le SDK client contacte le service, le SDK serveur renvoie le widget de connexion si plusieurs fournisseurs d'identité ont été configurés. {{site.data.keyword.appid_short_notm}} appelle le fournisseur d'identité et lui présente son formulaire d'identification ou renvoie un code d'acceptation qui lui permet de s'authentifier si aucun fournisseur d'identité n'a été configuré.
* {{site.data.keyword.appid_short_notm}} demande à l'application client de s'authentifier en répondant à une demande d'authentification.
* Si un fournisseur d'identité est configuré, lorsque l'utilisateur se connecte, l'authentification est gérée par le flux OAuth correspondant.

* Si l'authentification se conclut par le même code d'accord, celui-ci est envoyé au noeud final du jeton. Le noeud final renvoie deux jetons : un jeton d'accès et un jeton d'identité.
Dès lors, toutes les demandes effectuées avec le SDK client obtiennent un nouvel
en-tête d'autorisation.
* Le SDK client renvoie automatiquement la demande d'origine ayant déclenché le flux d'autorisation.
* Le SDK serveur extrait l'en-tête de l'autorisation depuis la demande, le valide auprès du service et octroie l'accès à une ressource de back end.


## Composants
{: #components}

Le service est constitué des composants suivants.

<dl>
  <dt> Tableau de bord</dt>
    <dd> Dans le tableau de bord du service, vous pouvez télécharger des exemples intégrés, visualiser les journaux d'activité et configurer l'authentification et des fournisseurs d'identité. </dd>
  <dt> SDK client </dt>
    <dd> Vous pouvez utiliser le SDK avec vos applications Web et mobiles pour implémenter l'authentification des utilisateurs. </br></br>
    Prérequise pour Android :
    <ul><ul><li> API 25 (ou version ultérieure) </li>
    <li> Java 8.x </li>
    <li> Android SDK tools 25.2.5 (ou version ultérieure) </li>
    <li> Android SDK Platform Tools 25.0.3 (ou version ultérieure) </li>
    <li> Android Build Tools 25.0.2 (ou version ultérieure) </li></ul></ul></br>
    Prérequis pour iOS :
    </br>
    <ul><ul><li> iOS9 (ou version ultérieure) </li>
    <li> MacOS 10.11.5 </li>
    <li>Xcode 8.2 </li></ul></ul></dd>
  <dt> SDK serveur </dt>
    <dd> Permet de protéger des ressources de back end hébergées sur {{site.data.keyword.Bluemix_notm}} </br>
    Environnements d'exécution pris en charge :
    <ul><ul><li> Node.js </li>
    <li> Liberty for Java </li>
    <li> Swift </li></ul></ul></dd>
</dl>
