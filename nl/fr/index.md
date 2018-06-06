---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Tutoriel Initiation
{: #gettingstarted}

{{site.data.keyword.appid_full}} vous aide à ajouter une authentification à vos applications mobiles et web et protège vos ressources de back-end.
{: shortdesc}

## Création d'une instance de service
{: #create}

Pour commencer, créez une instance d'{{site.data.keyword.appid_short_notm}}.
{: shortdesc}

1. Dans le catalogue {{site.data.keyword.Bluemix}}, sélectionnez {{site.data.keyword.appid_short_notm}}. L'écran de configuration du service s'ouvre.
2. Attribuez un nom à votre instance de service ou utilisez le nom prédéfini.
3. Pour lier votre instance, sélectionnez une application dans le menu
**Connecter à**. Si vous sélectionnez **Laisser non
lié**, vous pourrez lier l'instance de service ultérieurement.
4. Sélectionnez votre plan de tarification, puis cliquez sur **Créer**.

## Configuration d'un modèle d'application
{: #sample-app}

Vous pouvez utiliser l'un des modèles d'application préconfigurés pour vous familiariser avec l'utilisation du service.
{: shortdesc}

Prêts à l'emploi, les modèles d'applications sont configurés avec deux fournisseurs d'identité et offrent la possibilité de passer en revue le processus d'authentification. Vous pouvez également utiliser le widget de connexion afin de personnaliser une page de connexion et voir à quelle vitesse les mises à jour que vous apportez sont intégrées à votre application.

Pour configurer un modèle d'application à partir de l'interface graphique :

1. Après avoir créé une instance du service, vous pouvez sélectionner un modèle d'application rédigé dans le langage qui vous convient. Vous avez le choix entre Swift iOS, Android, Node.js et Java. Si vous ne souhaitez pas utiliser un SDK, Consultez notre blogue sur <a href="https://github.com/mnsn/appid-python-flask-example" target="_blank">l'utilisation d'{{site.data.keyword.appid_short_notm}} avec d'autres langages, tels que Python <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.
2. Suivez les instructions de l'interface graphique pour **générer et exécuter** votre modèle d'application. Etant donné que chaque langage est configuré de manière légèrement différente, assurez-vous de sélectionner le langage de l'application que vous avez téléchargée depuis le menu déroulant. Une fois votre application configurée, ouvrez-la dans un navigateur et connectez-vous à l'aide de vos données d'identification.
  **Remarque** : Vérifiez que les éléments prérequis pour le langage que vous voulez utiliser sont installés.
  <dl>
    <dt> Android </dt>
      <dd><ul><li> API Android 25 ou version ultérieure</li><li> Java 8.x </li><li> Android SDK Tools 25.2.5+ </li><li> Android SDK Platform Tools 25.0.3+ </li><li> Android Build Tools version 25.0.2 </li></ul></dd>
    <dt> Swift iOS </dt>
      <dd><ul><li> CocoaPods (version 1.1.0 ou ultérieure) </li><li> iOS 9 ou version ultérieure </li><li> MacOS 10.11.5 </li><li> Xcode 8.1 25.0.3+ </li></ul></dd>
    <dt> Node.js </dt>
      <dd><ul><li> Interface de ligne de commande Cloud Foundry </li></ul></dd>
    <dt> Java </dt>
      <dd><ul><li> Interface de ligne de commande Cloud Foundry </li><li> Maven </li></ul></dd>
  </dl>
3. Cliquez sur **Vérification de l'activité** pour visualiser les événements d'authentification qui se sont produits. Vous devez voir au moins un événement si vous vous êtes connecté.
4. Personnalisez votre expérience de connexion. Vous pouvez sélectionner une image, tels votre logo et une couleur d'en-tête. Vous pouvez sélectionner les options de couleur ou insérer une valeur hexadécimale. Lorsque vous êtes satisfait de l'aperçu, cliquez sur **Sauvegarder les modifications**. L'image suivante présente un exemple de modèle d'écran de connexion.
5. Dans votre navigateur, actualisez votre page de connexion. Les modifications apportées à l'étape précédente sont déjà visibles.
