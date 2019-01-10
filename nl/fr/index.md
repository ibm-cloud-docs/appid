---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:tip: .tip}

# Tutoriel d'initiation
{: #gettingstarted}

La sécurité des applications peut s'avérer être un sujet incroyablement compliqué. Pour la plupart des développeurs, il s'agit de l'une des composantes les plus difficiles du processus de création d'application. Comment pouvez-vous être sûr que vous protégez les informations de vos utilisateurs ? En intégrant {{site.data.keyword.appid_full}} à vos applications, vous pouvez sécuriser les ressources et ajouter un processus d'authentification; même si vous ne possédez pas une grande expérience en matière de sécurité.
{: shortdesc}

En demandant aux utilisateurs de se connecter à votre application, vous pouvez stocker des données utilisateur telles que les préférences d'application ou des informations provenant de profils de réseaux sociaux publics, puis utiliser ces données afin de personnaliser chaque expérience de votre application. {{site.data.keyword.appid_short_notm}} fournit une infrastructure de connexion pour votre usage, mais vous pouvez également apporter vos propres écrans de connexion de marque à utiliser avec le répertoire cloud.

Nous serions ravis de recevoir vos commentaires et de répondre à vos questions !
* Posez toute question d'ordre technique sur {{site.data.keyword.appid_short_notm}} sur le forum <a href="https://stackoverflow.com/search?q=ibm-appid" target="_blank">Stack Overflow <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> en indiquant la balise `ibm-appid`.
* Posez toute question relative au service et aux instructions de mise en route sur le forum <a href="https://developer.ibm.com/answers/topics/appid/" target="_blank">dW Answers <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> en indiquant la balise `appid`.

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

Prêts à l'emploi, les modèles d'applications sont configurés avec deux fournisseurs d'identité et offrent la possibilité de passer en revue le processus d'authentification. Les modèles d'application proposées sont `iOS Swift`, `Android`, `Node.js` et `Java`. Si vous ne voyez pas de langue dans laquelle vous vous sentez à l'aise pour travailler, ne vous inquiétez pas ! Vous pouvez intégrer {{site.data.keyword.appid_short_notm}} à votre propre modèle d'application à l'aide des API fournies.

Pour générer un modèle d'application :

1. Cliquez sur **Télécharger un exemple**.
2. Cliquez sur la langue de votre choix pour télécharger l'exemple.
  Vous ne trouvez pas la langue que vous recherchez ? Ne vous inquiétez pas ! Vous pouvez tirer parti d'{{site.data.keyword.appid_short_notm}} grâce aux API. Vous pouvez aussi consulter <a href="https://www.ibm.com/blogs/bluemix/tag/app-id/" target="_blank">nos blogues <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> pour de l'aide supplémentaire relative à d'autres langues.
  {: tip}
3. Assurez-vous que les prérequis sont installés ou satisfaits.
4. Suivez les étapes **Build & Run** pour configurer votre exemple avec {{site.data.keyword.appid_short_notm}}.
5. Cliquez sur **Vérification de l'activité** pour visualiser les événements d'authentification qui se sont produits. Tout type de connexion crée un événement visible sur cette page.
6. Personnalisez le widget de connexion.
  1. Ajoutez une image, telle qu'un logo de marque, en cliquant sur **Sélectionner** et parcourez votre système local pour recherche une image à télécharger.
  2. Choisissez un schéma de couleurs en sélectionnant l'une des options de couleur ou en spécifiant une valeur hexadécimale.
  3. Basculez d'une application Web à une application mobile pour voir à quoi ressemble le jeu de couleurs sur chaque type d'appareil.
  4. Lorsque vos choix vous conviennent, cliquez sur **Sauvegarder les modifications**.
7. Dans un navigateur, actualisez votre page de connexion. Les modifications apportées à l'étape précédente sont déjà visibles.


## Etapes suivantes
{: #next}

Prêt à vous lancer et à créer vos propres applications ? Commencez par [ajouter le service à votre application](web-apps.html). Il fournit des logiciels SDK pour les langues les plus utilisées, et si vous ne trouvez pas de logiciel SDK pour la langue dans laquelle votre application est écrite, vous pouvez toujours tirer parti d'{{site.data.keyword.appid_short_notm}} en utilisant les API.

</br>
</br>
