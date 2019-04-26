---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-08"

keywords: authentication, authorization, identity, app security, secure, compliance, high availability

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

# A propos d'{{site.data.keyword.appid_short_notm}}
{: #about}

La sécurité des applications peut s'avérer être un sujet incroyablement compliqué. Pour la plupart des développeurs, il s'agit de l'une des composantes les plus difficiles du processus de création d'application. Comment pouvez-vous être sûr que vous protégez les informations de vos utilisateurs ? En intégrant {{site.data.keyword.appid_full}} à vos applications, vous pouvez sécuriser les ressources et ajouter un processus d'authentification, même si vous ne possédez pas une grande expérience en matière de sécurité.
{:shortdesc}



## Pourquoi utiliser ce service ?
{: #about-reasons}

{{site.data.keyword.appid_short_notm}} aide les développeurs à ajouter facilement un processus d'authentification à leurs applications Web et mobiles en quelques lignes de code, ainsi qu'à sécuriser leurs applications et leurs services natifs pour le cloud dans {{site.data.keyword.cloud_notm}}. En demandant aux utilisateurs de se connecter à votre application, vous pouvez stocker des données utilisateur telles que les préférences d'application, ou des informations provenant de profils de réseaux sociaux publics, puis optimiser ces données afin de personnaliser chaque expérience d'utilisateur dans votre application. {{site.data.keyword.appid_short_notm}} fournit une infrastructure de connexion pour votre usage, mais vous pouvez également apporter vos propres écrans de marque à utiliser avec Cloud Directory.
{: shortdesc}

Que peut vous apporter Cloud Directory ? Regardez cette vidéo pour en savoir plus sur les différentes façons d'utiliser le service et consultez le tableau suivant des informations sur d'autres scénarios.

<iframe class="embed-responsive-item" id="youtubeplayer" title="A propos d'App ID" type="text/html" width="640" height="390" src="//www.youtube.com/embed/XlrCjHdK43Q?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

<table>
  <tr>
    <th>Scénario</th>
    <th>Solution</th>
  </tr>
  <tr>
    <td>Vous devez ajouter un mécanisme d'[autorisation et d'authentification](/docs/services/appid?topic=appid-key-concepts#key-concepts) à vos applications mobiles et Web, mais vous n'avez pas d'expérience en matière de sécurité.</td>
    <td>{{site.data.keyword.appid_short_notm}} facilite l'ajout d'une étape d'authentification à vos applications. Vous pouvez ajouter une connexion par adresse électronique ou nom d'utilisateur, une connexion par réseau social ou une connexion d'entreprise à vos applications avec des API, des logiciels SDK, des interfaces utilisateur prégénérées ou vos propres interfaces utilisateur de marque.</td>
  </tr>
  <tr>
    <td>Vous voulez limiter l'accès à vos applications et ressources de back end.</td>
    <td>Vous pouvez sécuriser vos applications, vos ressources de back end et vos API facilement en utilisant l'authentification reposant sur des normes fournie par {{site.data.keyword.appid_short_notm}}.</td>
  </tr>
  <tr>
    <td>Vous voulez générer des applications personnalisées pour vos utilisateurs.</td>
    <td>{{site.data.keyword.appid_short_notm}} vous permet de [stocker des données sur les utilisateurs](/docs/services/appid?topic=appid-user-profile#user-profile), telles que leurs préférences d'utilisation des applications ou des informations issues de leurs profils publics dans les réseaux sociaux, puis d'utiliser ces données afin de personnaliser chaque expérience de votre application.</td>
  </tr>
  <tr>
    <td>Vous voulez gérer les utilisateurs de façon évolutive.</td>
    <td> Avec {{site.data.keyword.appid_short_notm}} vous pouvez créer un [répertoire cloud (Cloud Directory)](/docs/services/appid?topic=appid-cloud-directory#cloud-directory) qui vous permet d'ajouter des processus d'inscription et de connexion d'utilisateur à vos applications. Cloud Directory met à disposition l'infrastructure permettant de gérer un registre d'utilisateurs qui peut évoluer avec votre base d'utilisateurs. Avec la fonctionnalité préconfigurée de libre-service, telle que la vérification et la réinitialisation du mot de passe, vous avez la garantie que votre application authentifie les utilisateurs en toute sécurité.</td>
  </tr>
</table>


## Fonctionnement
{: #about-how-it-works}

Avec {{site.data.keyword.appid_short_notm}}, vous pouvez ajouter un niveau de sécurité à vos applications en demandant aux utilisateurs de se connecter. Vous pouvez également utiliser le logiciel SDK serveur ou des API pour protéger vos ressources de back end.
{: shortdesc}

![{{site.data.keyword.appid_short_notm}} - Diagramme de l'architecture](images/appid_architecture1.png)

<dl>
  <dt>Application</dt>
    <dd><strong>Logiciel SDK serveur</strong> : vous pouvez protéger vos ressources de back end hébergées sur {{site.data.keyword.cloud_notm}} et vos applications Web en utilisant le logiciel SDK serveur. Celui-ci extrait le jeton d'accès d'une demande et le valide avec {{site.data.keyword.appid_short_notm}}. </br>
    <strong>Logiciel SDK client</strong> : vous pouvez protéger vos applications mobiles avec le logiciel SDK client Android ou iOS. Le logiciel SDK client communique avec vos ressources cloud pour démarrer le processus d'authentification lorsqu'il détecte une demande d'autorisation.</dd>
  <dt>{{site.data.keyword.cloud_notm}}</dt>
    <dd><strong>{{site.data.keyword.appid_short_notm}}</strong> : une fois que l'authentification a abouti, {{site.data.keyword.appid_short_notm}} renvoie les jetons d'identité et d'accès à votre application.</br>
    <strong>Cloud Directory</strong> : les utilisateurs peuvent s'inscrire à votre service avec leur adresse électronique et un mot de passe. Vous pouvez les gérer dans une liste visible dans l'interface utilisateur. Avec Cloud Directory, {{site.data.keyword.appid_short_notm}} fait office de fournisseur d'identité.</dd>
  <dt>Externe (tierce partie)</dt>
    <dd><strong>Fournisseurs d'identité de réseaux sociaux et d'entreprise</strong> : {{site.data.keyword.appid_short_notm}} prend en charge les fournisseurs d'identité Facebook, Google+ et SAML 2.0 Federation. Le service met en place une redirection vers le fournisseur d'identité et vérifie les jetons d'authentification renvoyés. Si les jetons sont valides, le service autorise l'accès à votre application sans qu'il ne soit nécessaire d'avoir accès à la phrase passe en cours.</dd>
</dl>


## Intégrations
{: #about-integrations}

Vous pouvez utiliser {{site.data.keyword.appid_short_notm}} avec d'autres offres {{site.data.keyword.cloud_notm}}.
{:shortdesc}

<dl>
  <dt>{{site.data.keyword.containerlong_notm}}</dt>
    <dd>En configurant Ingress dans un cluster standard, vous pouvez sécuriser vos applications au niveau du cluster. Consultez l'<a href="/docs/containers?topic=containers-ingress_annotation#appid-auth">{{site.data.keyword.appid_short_notm}}annotation Ingress relative à l'authentification</a> ou l'article de blogue <a href="https://www.ibm.com/blogs/bluemix/2018/05/announcing-app-id-integration-ibm-cloud-kubernetes-service/">Announcing {{site.data.keyword.appid_short_notm}} integration to {{site.data.keyword.containerlong_notm}} <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> pour commencer.</dd>
  <dt>{{site.data.keyword.openwhisk}} et API Connect</dt>
    <dd>Lorsque vous créez vos API avec [{{site.data.keyword.openwhisk_short}}](/docs/openwhisk?topic=cloud-functions-getting_started#getting_started) et [API Connect](/docs/services/apiconnect?topic=apiconnect-index#index), vous avez la possibilité de sécuriser vos applications au niveau de la passerelle plutôt que dans le code applicatif. Pour découvrir le fonctionnement de l'intégration, regardez <a href="https://www.youtube.com/watch?v=Fa9YD2NGZiE" target="_blank">Simple and fast social login OAauth with APIC and {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.</dd>
  <dt>Cloud Foundry</dt>
    <dd>Suivez l'un des exemples d'application Cloud Foundry fournis pour découvrir comment vous pouvez intégrer {{site.data.keyword.appid_short_notm}} à vos applications.</dd>
  <dt>{{site.data.keyword.cloudaccesstrailshort}}</dt>
    <dd>Vous pouvez surveiller l'activité d'administration effectuée dans {{site.data.keyword.appid_short_notm}}, telle que les modifications apportées à la configuration du tableau de bord, à l'aide du [service {{site.data.keyword.cloudaccesstrailshort}}](/docs/services/cloud-activity-tracker/reference?topic=cloud-activity-tracker-getting-started-with-cla#getting-started-with-cla).</dd>
  <dt>Guide de programmation iOS</dt>
    <dd>Vous développez des applications pour Apple ? Consultez le manuel [iOS programming guide](/docs/swift/authenticate?topic=swift-getting_started_swift#getting_started_swift) pour apprendre, expérimenter, et améliorer vos applications iOS existantes avec {{site.data.keyword.cloud_notm}}.</dd>
  <dt>Guide de programmation Node.js</dt>
    <dd>Vous développez des applications dans Node.js ? Consultez le manuel [Node.js programming guide](/docs/node?topic=nodejs-node-getting-started#node-getting-started) pour apprendre, expérimenter, et améliorer vos applications Node.js existantes avec {{site.data.keyword.cloud_notm}}.</dd>
</dl>


## Conformité et normes
{: #about-compliance}

{{site.data.keyword.appid_short_notm}} s'est révélé conforme à plusieurs certifications, audits et normes.
{: shortdesc}

{{site.data.keyword.appid_short_notm}} s'appuie sur un ensemble reconnu de spécifications et de protocoles normalisés de l'industrie fréquemment utilisés à la fois dans les applications d'entreprise et grand public, la structure d'autorisation OAuth 2.0 et OIDC (Open ID Connect). La structure d'autorisation OAuth 2.0 est utilisée pour obtenir et vérifier les autorisations d'accès à des ressources protégées. Open ID Connect ajoute une couche supplémentaire d'authentification et de protection des identités à votre application.

Voir la section 5.4 du rapport sur la compatibilité des produits logiciels {{site.data.keyword.appid_short_notm}} pour la liste complète des [certifications](https://www.ibm.com/software/reports/compatibility/clarity-reports/report/html/softwareReqsForProduct?deliverableId=BF31C8008D7C11E59F9AD7336D7D0FFB). Outre les certifications, {{site.data.keyword.appid_short_notm}} est également conforme aux spécifications suivantes : Oauth 2.0, OpenID Connect, JSON Web Token (JWT), JSON Web Signature (JWS), System for Cross-domain Identity Management (SCIM). 


## Haute disponibilité régionale
{: #ha-dr}

{{site.data.keyword.appid_short_notm}} est un service régional à haute disponibilité qui s'exécute dans plusieurs zones.
{: shortdesc}

Dans chaque région à zones multiples, chaque zone dispose de son propre cluster {{site.data.keyword.containerlong_notm}} avec plusieurs noeuds worker. Chaque noeud worker exécute plusieurs instances des composants {{site.data.keyword.appid_short_notm}}. Devant chaque région se trouvent un équilibreur de charge global et un pare-feu d'application Web.

Les données stockées dans {{site.data.keyword.appid_short_notm}} sont chiffrées et conservées dans un cluster de base de données réparti sur les zones de disponibilité. Les données sont également sauvegardées dans un stockage d'objets chiffré séparé.

Etant donné qu'{{site.data.keyword.appid_short_notm}} est un service régional, il ne fournit pas de basculement interrégional automatisé ou de reprise après incident interrégionale. {{site.data.keyword.appid_short_notm}} fournit toutefois une <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/" target="_blank">API complète<img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> que les développeurs peuvent utiliser pour synchroniser manuellement leur configuration de service avec une ou plusieurs autres instances {{site.data.keyword.appid_short_notm}}.
