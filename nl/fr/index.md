---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:tip: .tip}

# Tutoriel d'initiation
{: #gettingstarted}

La sécurité des applications peut s'avérer être un sujet incroyablement compliqué. Pour la plupart des développeurs, il s'agit de l'une des composantes les plus difficiles du processus de création d'application. Comment pouvez-vous être sûr que vous protégez les informations de vos utilisateurs ? En intégrant {{site.data.keyword.appid_full}} à vos applications, vous pouvez sécuriser les ressources et ajouter un processus d'authentification; même si vous ne possédez pas une grande expérience en matière de sécurité.
{: shortdesc}

En demandant aux utilisateurs de se connecter à votre application, vous pouvez stocker des données utilisateur telles que les préférences d'application ou des informations provenant de profils de réseaux sociaux publics, puis utiliser ces données afin de personnaliser chaque expérience de votre application. App ID fournit une infrastructure de connexion pour votre usage, mais vous pouvez également apporter vos propres écrans de connexion de marque à utiliser avec le répertoire cloud. 

En tant que propriétaire de compte, vous pouvez désormais mettre en place des règles définissant la façon dont les membres de votre équipe peuvent interagir avec des instances d'{{site.data.keyword.appid_short_notm}}. Vous pouvez choisir qui peut créer, mettre à jour et supprimer des instances du service. Pour plus d'informations, voir [Gestion des accès de service](/docs/services/appid/iam.html).
{:tip}

## Création d'une instance de service
{: #create}

Pour commencer, créez et liez une instance d'{{site.data.keyword.appid_short_notm}} à votre application.
{: shortdesc}

1. Dans le catalogue {{site.data.keyword.Bluemix}}, sélectionnez {{site.data.keyword.appid_short_notm}}. L'écran de configuration du service s'ouvre.
2. Attribuez un nom à votre instance de service ou utilisez le nom prédéfini.
3. Sélectionnez votre plan de tarification, puis cliquez sur **Créer**.
4. Liez votre instance d'{{site.data.keyword.appid_short_notm}}.
    1. Pour voir la liste des applications que vous pouvez lier à votre instance de service, cliquez sur **Connexions **.
    2. Cliquez sur **Créer une connexion**. Une page s'ouvre avec toutes les applications que vous pouvez lier.
    3. Cliquez sur **Connexion** sur l'application que vous souhaitez lier.
    4. Cliquez sur **Reconstituer** pour appliquer la modification.

Et voilà ! Vous êtes prêt à débuter la configuration de vos paramètres d'application.


## Configuration d'un modèle d'application
{: #sample-app}

Vous pouvez utiliser l'un des modèles d'application préconfigurés pour vous familiariser avec l'utilisation du service.
{: shortdesc}

Prêts à l'emploi, les modèles d'applications sont configurés avec deux fournisseurs d'identité et offrent la possibilité de passer en revue le processus d'authentification. Vous pouvez également utiliser le widget de connexion afin de personnaliser une page de connexion et voir à quelle vitesse les mises à jour que vous apportez sont intégrées à votre application.

Pour configurer un modèle d'application à partir de l'interface graphique :

1. Après avoir créé une instance du service, vous pouvez sélectionner un modèle d'application rédigé dans le langage qui vous convient. Vous avez le choix entre Swift iOS, Android, Node.js et Java. Si vous ne souhaitez pas utiliser de logiciel SDK, vous pouvez intégrer {{site.data.keyword.appid_short_notm}} à l'aide des API. 
2. Suivez les instructions de l'interface graphique pour **générer et exécuter** votre modèle d'application. Chaque langage étant configuré de manière légèrement différente, assurez-vous de sélectionner le langage de l'application que vous avez téléchargée depuis le menu déroulant. Une fois votre application configurée, ouvrez-la dans un navigateur et connectez-vous à l'aide de vos données d'identification. Assurez-vous que les prérequis pour votre langage d'application sont installés.
  <dl>
    <dt> Android </dt>
      <dd><ul><li> API Android 27 ou version ultérieure </li><li> Java 8.x </li><li> Android SDK Tools 25.2.5+ </li><li> Android SDK Platform Tools 26.1.1+ </li><li> Android Build Tools version 27.0.0+ </li></ul></dd>
    <dt> Swift iOS </dt>
      <dd><ul><li> CocoaPods (version 1.1.0 ou ultérieure) </li><li> iOS 10.0 ou version ultérieure </li><li> MacOS 10.11.5 </li><li> Xcode (version 9.0.1 ou ultérieure) </li></ul></dd>
    <dt> Node.js </dt>
      <dd><ul><li> L'interface de ligne de commande d'{{site.data.keyword.Bluemix_notm}} </li></ul></dd>
    <dt> Java </dt>
      <dd><ul><li> L'interface de ligne de commande d'{{site.data.keyword.Bluemix_notm}} </li><li> Maven </li></ul></dd>
  </dl>

  Vous ne trouvez pas le langage que vous recherchez ? Ne vous inquiétez pas ! Vous pouvez tirer parti d'{{site.data.keyword.appid_short_notm}} grâce aux API. Vous pouvez aussi consulter <a href="https://www.ibm.com/blogs/bluemix/tag/app-id/" target="_blank">nos blogues <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> pour de l'aide supplémentaire relative à d'autres langages. {: tip}

3. Cliquez sur **Vérification de l'activité** pour visualiser les événements d'authentification qui se sont produits. Une fois que vous êtes connecté, vous pouvez afficher un événement.
4. Personnalisez votre expérience de connexion. Vous pouvez sélectionner une image, tels votre logo et une couleur d'en-tête. Vous pouvez sélectionner les options de couleur ou insérer une valeur hexadécimale. Lorsque vous êtes satisfait de l'aperçu, cliquez sur **Sauvegarder les modifications**.
5. Dans votre navigateur, actualisez votre page de connexion. Les modifications apportées à l'étape précédente sont déjà visibles.

## Etapes suivantes
{: #next}

Prêt à vous lancer et à créer vos propres applications ? Commencez par [ajouter le service à votre application](/docs/services/appid/install.md). Il fournit des logiciels SDK pour les langages les plus utilisés, et si vous ne trouvez pas de logiciel SDK pour le langage dans lequel votre application est écrite, vous pouvez utiliser l'API. 

</br>
</br>
