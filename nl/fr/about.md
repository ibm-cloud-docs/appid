---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# A propos de
{: #about}

La sécurité des applications peut s'avérer être un sujet incroyablement compliqué. Pour la plupart des développeurs, il s'agit de l'une des composantes les plus difficiles du processus de création d'application. Comment pouvez-vous être sûr que vous protégez les informations de vos utilisateurs ? En intégrant {{site.data.keyword.appid_full}} à vos applications, vous pouvez sécuriser les ressources et ajouter un processus d'authentification, même si vous ne possédez pas une grande expérience en matière de sécurité.
{:shortdesc}


## Pourquoi utiliser ce service ?
{: #reasons}

{{site.data.keyword.appid_short_notm}} aide les développeurs à ajouter facilement un processus d'authentification à leurs applications Web et mobiles en quelques lignes de code, ainsi qu'à sécuriser leurs applications et leurs services natifs pour le cloud dans {{site.data.keyword.Bluemix_notm}}. En demandant aux utilisateurs de se connecter à votre application, vous pouvez stocker des données utilisateur telles que les préférences d'application, ou des informations provenant de profils de réseaux sociaux publics, puis optimiser ces données afin de personnaliser chaque expérience d'utilisateur dans votre application. {{site.data.keyword.appid_short_notm}} fournit une infrastructure de connexion pour votre usage, mais vous pouvez également apporter vos propres écrans de connexion de marque à utiliser avec le répertoire cloud.
{: shortdesc}

Pourquoi utiliser {{site.data.keyword.appid_short_notm}} ? Déterminez si l'un des scénarios ci-dessous répond à vos attentes.

<table>
  <tr>
    <th>Scénario</th>
    <th>Solution</th>
  </tr>
  <tr>
    <td>Vous devez ajouter un mécanisme d'[autorisation et d'authentification](/docs/services/appid/authorization.html) à vos applications mobiles et Web, mais vous n'avez pas d'expérience en matière de sécurité.</td>
    <td>{{site.data.keyword.appid_short_notm}} facilite l'ajout d'une étape d'authentification à vos applications. Vous pouvez ajouter une connexion par adresse électronique ou nom d'utilisateur, une connexion par réseau social ou une connexion d'entreprise à vos applications avec des API, des logiciels SDK, des interfaces utilisateur prégénérées ou vos propres interfaces utilisateur de marque. </td>
  </tr>
  <tr>
    <td>Vous voulez limiter l'accès à vos applications et ressources de back end.</td>
    <td>Vous pouvez sécuriser vos applications, vos ressources de back end et vos API facilement en utilisant l'authentification reposant sur des normes fournie par {{site.data.keyword.appid_short_notm}}.</td>
  </tr>
  <tr>
    <td>Vous voulez générer des applications personnalisées pour vos utilisateurs.</td>
    <td>{{site.data.keyword.appid_short_notm}} vous permet de [stocker des données sur les utilisateurs](/docs/services/appid/user-profile.html), telles que leurs préférences d'utilisation des applications ou des informations issues de leurs profils publics dans les réseaux sociaux, puis d'utiliser ces données afin de personnaliser chaque expérience de votre application.</td>
  </tr>
  <tr>
    <td>Vous voulez gérer les utilisateurs de façon évolutive. </td>
    <td> {{site.data.keyword.appid_short_notm}} permet de créer un [répertoire cloud](/docs/services/appid/cloud-directory.html), qui vous permet d'ajouter les processus d'inscription et de connexion d'utilisateur à vos applications. Le répertoire cloud met à disposition l'infrastructure permettant de gérer un registre d'utilisateurs qui peut évoluer avec votre base d'utilisateurs. Avec la fonctionnalité préconfigurée de libre-service, telle que la vérification et la réinitialisation du mot de passe, vous avez la garantie que votre application authentifie les utilisateurs en toute sécurité.</td>
  </tr>
</table>


## Intégrations
{: #integrations}

Vous pouvez utiliser {{site.data.keyword.appid_short_notm}} avec d'autres offres {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}


<dl>
  <dt>{{site.data.keyword.containerlong_notm}}</dt>
    <dd>En configurant Ingress dans un cluster standard, vous pouvez sécuriser vos applications au niveau du cluster. Consultez l'<a href="/docs/containers/cs_annotations.html#appid-auth">annotation Ingress relative à l'authentification {{site.data.keyword.appid_short_notm}}</a> ou l'article de blogue <a href="https://www.ibm.com/blogs/bluemix/2018/05/announcing-app-id-integration-ibm-cloud-kubernetes-service/">Announcing App ID integration to IBM Cloud Kubernetes Service <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> pour commencer. </dd>
  <dt>{{site.data.keyword.openwhisk}} et API Connect</dt>
    <dd>Lorsque vous créez vos API avec [{{site.data.keyword.openwhisk_short}}](/docs/openwhisk/index.html) et [API Connect](/docs/apis/management/manage_apis.html), vous avez la possibilité de sécuriser vos applications au niveau de la passerelle plutôt que dans le code applicatif. Pour découvrir le fonctionnement de l'intégration, regardez <a href="https://www.youtube.com/watch?v=Fa9YD2NGZiE" target="_blank">Simple and fast social login OAUTH with APIC and {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.</dd>
  <dt>Cloud Foundry</dt>
    <dd>Suivez l'un des exemples d'application Cloud Foundry fournis pour découvrir comment vous pouvez intégrer {{site.data.keyword.appid_short_notm}} à vos applications.</dd>
  <dt>Guide de programmation iOS</dt>
    <dd>Vous développez des applications pour Apple ? Suivez le manuel <a href="https://console.bluemix.net/docs/swift/index.html#overview" target="_blank">iOS programming guide <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> pour apprendre, expérimenter, et améliorer vos applications iOS existantes avec {{site.data.keyword.Bluemix_notm}}.</dd>
  <dt>{{site.data.keyword.cloudaccesstrailshort}}</dt>
    <dd>Vous pouvez surveiller l'activité d'administration effectuée dans {{site.data.keyword.appid_short_notm}}, telle que les modifications apportées à la configuration du tableau de bord, à l'aide du [service {{site.data.keyword.cloudaccesstrailshort}}](/docs/services/cloud-activity-tracker/index.html). </dd>
  <dt>Guide de programmation Node.js</dt>
    <dd>Vous développez des applications dans Node.js ? Suivez le manuel <a href="https://console.bluemix.net/docs/node/index.html#getting-started-tutorial" target="_blank">Node.js programming guide <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> pour apprendre, expérimenter, et améliorer vos applications Node.js existantes avec {{site.data.keyword.Bluemix_notm}}. </dd>
</dl>


## Architecture
{: #architecture}

Avec {{site.data.keyword.appid_short_notm}}, vous pouvez ajouter un niveau de sécurité à vos applications en demandant aux utilisateurs de se connecter. Vous pouvez également utiliser le logiciel SDK serveur ou des API pour protéger vos ressources de back end.
{: shortdesc}

![{{site.data.keyword.appid_short_notm}} - Diagramme de l'architecture](/images/appid_architecture1.png)

<dl>
  <dt>Application</dt>
    <dd><strong>Logiciel SDK serveur</strong> : vous pouvez protéger vos ressources de back end hébergées sur {{site.data.keyword.Bluemix_notm}} et vos applications Web en utilisant le logiciel SDK serveur. Celui-ci extrait le jeton d'accès d'une demande et le valide avec {{site.data.keyword.appid_short_notm}}. </br>
    <strong>Logiciel SDK client</strong> : vous pouvez protéger vos applications mobiles avec le logiciel SDK client Android ou iOS. Le logiciel SDK client communique avec vos ressources cloud pour démarrer le processus d'authentification lorsqu'il détecte une demande d'autorisation.</dd>
  <dt>{{site.data.keyword.Bluemix_notm}}</dt>
    <dd><strong>{{site.data.keyword.appid_short_notm}}</strong> : une fois que l'authentification a abouti, {{site.data.keyword.appid_short_notm}} renvoie les jetons d'identité et d'accès à votre application.</br>
    <strong>Répertoire cloud</strong> : les utilisateurs peuvent s'inscrire à votre service avec leur adresse électronique et un mot de passe. Vous pouvez les gérer dans une liste visible dans l'interface utilisateur. Avec le répertoire cloud, {{site.data.keyword.appid_short_notm}} fait office de fournisseur d'identité.</dd>
  <dt>Externe (tierce partie )</dt>
    <dd><strong>Fournisseurs d'identité de réseaux sociaux et d'entreprise</strong> : {{site.data.keyword.appid_short_notm}} prend en charge les fournisseurs d'identité Facebook, Google+ et SAML 2.0 Federation. Le service met en place une redirection vers le fournisseur d'identité et vérifie les jetons d'authentification renvoyés. Si les jetons sont valides, le service autorise l'accès à votre application sans qu'il ne soit nécessaire d'avoir accès à la phrase passe en cours.</dd>
</dl>


## Flux de demandes
{: #request}

Votre flux de demandes peut varier selon la configuration de votre application ; toutefois, vous pourrez rencontrer trois flux principaux lorsque vous utilisez App ID. Vous pouvez créer un flux d'application mobile, un flux d'application Web, ou protéger vos ressources avec un flux différent. Découvrez quelques exemples de flux pour déterminer si vous pouvez les utiliser lorsque vous configurez votre application.
{: shortdesc}

### Flux de demandes d'application Web 
{: #web-flow}

![{{site.data.keyword.appid_short_notm}} - Flux d'une demande](/images/web_flow1.png)

1. Dans un navigateur, un utilisateur effectue une action qui déclenche l'envoi d'une demande au logiciel SDK d'App ID. 
2. Si l'utilisateur n'est pas autorisé, il est redirigé vers App ID. 
3. App ID lance le widget de connexion et l'envoie au navigateur. 
4. L'utilisateur choisit un fournisseur d'identité pour l'authentification et effectue le processus de connexion. 
5. Le fournisseur d'identité est redirigé vers le logiciel SDK d'App ID avec un jeton d'identité. 
6. Le logiciel SDK d'App ID obtient des jetons d'accès depuis le service App ID. 
7. Les jetons sont sauvegardés par le logiciel SDK d'App ID et une redirection a lieu.
8. L'utilisateur obtient l'accès à l'application. 

### Flux de demandes d'application mobile 
{: #mobile-flow}

![{{site.data.keyword.appid_short_notm}} - Flux d'une demande](/images/mobile_flow.png)

1. Un utilisateur effectue une action qui déclenche l'envoi d'une demande de l'application client au logiciel SDK d'App ID. 
2. Si l'utilisateur ne dispose pas de jetons d'accès valides, le logiciel SDK d'App ID lance le processus d'autorisation. 
3. Le widget de connexion est affiché pour l'utilisateur. 
4. L'utilisateur s'authentifie en utilisant l'un des fournisseurs d'identité configurés. 
5. Une fois que l'utilisateur dispose d'un jeton d'identité, le logiciel SDK obtient un jeton d'accès auprès du service App ID. 
6. Le logiciel SDK envoie à nouveau la demande avec les deux jetons. 
7. Si les jetons sont valides, l'utilisateur obtient l'accès à l'application. 

### Flux de demandes pour une ressource protégée 
{: #pr-flow}

![{{site.data.keyword.appid_short_notm}} - Flux d'une demande](/images/pr_flow.png)

1. Pour qu'elle puisse envoyer une demande à la ressource, une application client doit disposer d'un ensemble de clés publiques. 
2. Si elle dispose des clés publiques, l'application client peut envoyer une demande. 
3. S'il n'existe pas de jeton d'accès valide, l'application reçoit une erreur. 
4. Après avoir obtenu un jeton valide, l'application client peut envoyer à nouveau la demande. Mais cette fois, elle inclut le jeton. 
5. Lorsque l'application peut valider les droits qui sont accordés par le jeton d'accès, elle obtient l'accès à la ressource protégée. 
