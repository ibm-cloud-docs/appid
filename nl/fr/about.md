---

copyright:
  years: 2017, 2018
lastupdated: "2018-04-27"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# A propos de
{: #about}

Vous pouvez utiliser {{site.data.keyword.appid_full}} pour ajouter l'authentification à vos applications et protéger vos ressources de back end.
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
    <td> Vous devez ajouter un mécanisme d'[autorisation et d'authentification](/docs/services/appid/authorization.html) à vos applications mobiles et Web, mais vous n'avez pas d'expérience de la sécurité. </td>
    <td> {{site.data.keyword.appid_short_notm}} facilite l'ajout d'une étape d'authentification à vos applications. Vous pouvez utiliser le service pour communiquer avec des [fournisseurs d'identité](/docs/services/appid/identity-providers.html) afin de gérer l'accès à vos applications. </td>
  </tr>
  <tr>
    <td> Vous voulez limiter l'accès à vos applications et ressources de back end. </td>
    <td> Le service vous permet de [protéger vos ressources](/docs/services/appid/protecting-resources.html) vis-à-vis des utilisateurs authentifiés et des utilisateurs anonymes. </td>
  </tr>
  <tr>
    <td> Vous voulez générer des applications personnalisées pour vos utilisateurs. </td>
    <td> {{site.data.keyword.appid_short_notm}} vous permet de [stocker des données sur les utilisateurs](/docs/services/appid/user-profile.html), telles que leurs préférences d'utilisation des applications ou des informations issues de leurs profils publics dans les réseaux sociaux, puis d'utiliser ces données afin de personnaliser chaque expérience de votre application. </td>
  </tr>
  <tr>
    <td> Vous voulez autoriser les utilisateurs à accéder à votre application à l'aide de leur e-mail et d'un mot de passe. </td>
    <td> {{site.data.keyword.appid_short_notm}} vous permet de créer un [répertoire cloud](/docs/services/appid/cloud-directory.html), et vous pouvez ainsi ajouter l'inscription et la connexion utilisateurs à vos applications. Le répertoire cloud met à votre disposition l'infrastructure vous permettant de gérer un registre d'utilisateurs que vous pouvez mettre à l'échelle avec votre base utilisateur. Avec la fonctionnalité préconfigurée de libre-service, telle que la vérification et la réinitialisation du mot de passe, vous avez la garantie que votre application authentifie les utilisateurs en toute sécurité. </td>
  </tr>
</table>


## Intégrations
{: #integrations}

Vous pouvez utiliser {{site.data.keyword.appid_short_notm}} avec d'autres offres {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}


<dl>
  <dt>{{site.data.keyword.containerlong_notm}}</dt>
    <dd>En configurant Ingress dans un cluster standard, vous pouvez sécuriser vos applications au niveau cluster. Pour commencer, extrayez l'annotation ingress d'authentification {{site.data.keyword.appid_short_notm}}.</dd>
  <dt>{{site.data.keyword.openwhisk}} et API Connect</dt>
    <dd>Lorsque vous créez vos API avec [{{site.data.keyword.openwhisk_short}}](/docs/openwhisk/index.html) et [API Connect](/docs/apis/management/manage_apis.html), vous avez la possibilité de sécuriser vos applications au niveau de la passerelle plutôt que dans le code applicatif. Pour voir comment fonctionne l'intégration, regardez <a href="https://www.youtube.com/watch?v=Fa9YD2NGZiE" target="_blank">Simple and fast social login OAUTH with APIC and {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.</dd>
  <dt>Cloud Foundry</dt>
    <dd>Essayez l'un de nos exemples d'application Cloud Foundry pour voir comment vous pouvez intégrer App ID à vos applications.</dd>
  <dt>Guide de programmation iOS</dt>
    <dd>Vous développez des applications pour Apple ? Essayez le manuel <a href="https://console.bluemix.net/docs/swift/index.html#overview" target="_blank">iOS Programming Guide <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> pour apprendre, expérimenter et améliorer vos applications iOS existantes avec {{site.data.keyword.Bluemix_notm}}.</dd>
</dl>


## Architecture
{: #architecture}

Avec {{site.data.keyword.appid_short_notm}}, vous pouvez ajouter un niveau de sécurité à vos applications en demandant aux utilisateurs de se connecter. Vous pouvez également utiliser le SDK serveur pour protéger vos ressources de backe end.
{: shortdesc}

![{{site.data.keyword.appid_short_notm}} - Diagramme de l'architecture](/images/appid_architecture.png)

<dl>
  <dt> Application </dt>
    <dd><strong>SDK serveur</strong> : vous pouvez protéger vos ressources de back end hébergées sur {{site.data.keyword.Bluemix_notm}} et vos applications Web en utilisant le SDK serveur. Celui-ci extrait le jeton d'accès d'une demande et le valide avec {{site.data.keyword.appid_short_notm}}. </br>
    <strong>Client SDK</strong> : vous pouvez protéger vos applications mobiles avec le SDK client Android ou iOS. Le SDK client communique avec vos ressources cloud pour démarrer le processus d'authentification lorsqu'il détecte une demande d'autorisation.</dd>
  <dt>{{site.data.keyword.Bluemix_notm}}</dt>
    <dd><strong>{{site.data.keyword.appid_short_notm}}</strong> : une fois que l'authentification a abouti, {{site.data.keyword.appid_short_notm}} renvoie les jetons d'identité et d'accès à votre application.</br>
    <strong>Répertoire Cloud</strong> : les utilisateurs peuvent s'inscrire à votre service avec leur adresse e-mail et un mot de passe. Vous pouvez les gérer dans une liste visible dans l'interface utilisateur. Sans répertoire cloud, {{site.data.keyword.appid_short_notm}} fait office de fournisseur d'identité. </dd>
  <dt>Externe (tierce partie )</dt>
    <dd><strong>Fournisseurs d'identité de réseaux sociaux et d'entreprise</strong> : {{site.data.keyword.appid_short_notm}} prend en charge deux fournisseurs d'identité sociaux, Facebook et Google+, et un fournisseur d'identité d'entreprise, SAML 2.0 Federation. Le service met en place une redirection vers le fournisseur d'identité et vérifie les jetons d'authentification renvoyés. Si les jetons sont valides, le service autorise l'accès à votre application sans accès à la phrase passe en cours.</dd>
</dl>


## Flux de demandes
{: #request}

Le diagramme ci-dessous illustre le cheminement d'une demande entre le SDK client et vos ressources de back end et les fournisseurs d'identité.
{: shortdesc}

![{{site.data.keyword.appid_short_notm}} - Flux d'une demande](/images/appidrequestflow.png)


* Le SDK client {{site.data.keyword.appid_short_notm}} soumet une demande à vos ressources de back end protégées par le SDK serveur {{site.data.keyword.appid_short_notm}}.
* Le SDK serveur {{site.data.keyword.appid_short_notm}} détecte les demandes dépourvues d'autorisation et renvoie une réponse HTTP 401 une portée d'autorisation.
* Le SDK client détecte automatiquement la réponse HTTP 401 et lance la procédure d'autorisation.
* Lorsque le SDK client contacte le service, le SDK serveur renvoie le widget de connexion si plusieurs fournisseurs d'identité ont été configurés. {{site.data.keyword.appid_short_notm}} appelle le fournisseur d'identité et lui présente son formulaire d'identification ou renvoie un code d'acceptation qui lui permet de s'authentifier si aucun fournisseur d'identité n'a été configuré.
* {{site.data.keyword.appid_short_notm}} demande à l'application client de s'authentifier en répondant à une demande d'authentification.
* Si un fournisseur d'identité est configuré, lorsque l'utilisateur se connecte, l'authentification est gérée par le flux OAuth correspondant.
* Si l'authentification se conclut par le même code d'accord, celui-ci est envoyé au noeud final du jeton. Le noeud final renvoie deux jetons : un jeton d'accès et un jeton d'identité. Dès lors, toutes les demandes effectuées avec le SDK client obtiennent un nouvel en-tête d'autorisation.
* Le SDK client renvoie automatiquement la demande d'origine ayant déclenché le flux d'autorisation.
* Le SDK serveur extrait l'en-tête de l'autorisation depuis la demande, le valide auprès du service et octroie l'accès à une ressource de back end.

**Remarque** : les protocoles implémentés sont totalement compatibles avec Open Connect (OIDC).
