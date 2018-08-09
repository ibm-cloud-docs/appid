---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}

# Configuration des SDK
{: #configuring}


## Configuration du logiciel SDK Android
{: #android-setup}

Construisez vos applications Android avec le SDK client d'{{site.data.keyword.appid_short}}, initialisez le SDK, authentifiez les utilisateurs et soumettez des demandes à des ressources protégées et non protégées.
{:shortdesc}


### Avant de commencer

Vous devez disposer des éléments suivants :
  * Une instance du service {{site.data.keyword.appid_short_notm}}.
  * Votre ID titulaire. Dans l'onglet **Données d'identification pour le service** de votre tableau de bord du service, cliquez sur **Afficher les données d'identification**. Votre ID titulaire est un identificateur unique qui sert à initialiser votre application.
  * Votre région {{site.data.keyword.Bluemix}}. Vous pouvez identifier votre région en recherchant dans l'interface utilisateur. Cette valeur est utilisée pour initialiser votre application.
    <table> <caption> Tableau 1. Régions {{site.data.keyword.Bluemix_notm}} et valeurs de SDK correspondantes </caption>
    <tr>
      <th>Région {{site.data.keyword.Bluemix}}</th>
      <th>Valeur du SDK</th>
    </tr>
    <tr>
      <td>Sud des Etats-Unis</td>
      <td><code>AppID.REGION_US_SOUTH</code> </td>
    </tr>
    <tr>
      <td>Sydney</td>
      <td><code>AppID.REGION_SYDNEY </code></td>
    </tr>
    <tr>
      <td>Royaume-Uni</td>
      <td><code>AppID.REGION_UK </code></td>
    </tr>
    <tr>
      <td>Allemagne</td>
      <td><code>AppID.REGION_GERMANY</code></td>
    </tr>
  </table>

  * Un projet <a href="https://developers.google.com/web/tools/setup/" target="_blank">Android Studio<img src="../../icons/launch-glyph.svg" alt="icône de lien externe"></a>, configuré pour fonctionner avec Gradle.

### Installation du SDK client

1. Créez un projet Android Studio ou ouvrez un projet existant.
2. Ajoutez le référentiel JitPack à votre fichier racine `build.gradle`.

  ```gradle
    allprojects {
	    repositories {
		    ...
		    maven { url 'https://jitpack.io' }
	    }
    }
  ```
  {: codeblock}

3. Ouvrez le fichier `build.gradle` de votre application.

    **Remarque** : assurez-vous d'ouvrir le fichier correspondant à votre application et non pas le fichier `build.gradle` du projet.
4. Recherchez la section dependencies dans le fichier et ajoutez une dépendance de compilation pour le SDK client d'{{site.data.keyword.appid_short_notm}}.

  ```gradle
   dependencies {
       compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:1.+'
   }
  ```
  {: codeblock}

5. Recherchez la section `defaultConfig` et ajoutez-y les lignes de code suivantes.

  ```gradle
  defaultConfig {
  ...
  manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
  ```
  {: codeblock}

6. Synchronisez votre projet avec Gradle. Cliquez sur **Tools > Android > Sync Project with Gradle Files**.

### Initialisation du SDK client

Initialisez le SDK client en transmettant les paramètres de contexte, d'ID titulaire et de région à la méthode initialize. Bien que ce ne soit pas obligatoire, le code d'initialisation est souvent placé dans la méthode onCreate de l'activité principale dans votre application Android.

  ```java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, AppID.REGION_UK);
  ```
  {: codeblock}

1. Remplacez *tenantId* par votre ID titulaire du service.
2. Remplacez *AppID.REGION_UK* par votre région {{site.data.keyword.Bluemix_notm}}.

Pour plus d'informations, consultez le
<a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">référentiel GitHub Android pour {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.

## Configuration du SDK Swift iOS
{: #ios-setup}

Construisez vos applications Swift avec le SDK client d'{{site.data.keyword.appid_short}}, initialisez le SDK, authentifiez les utilisateurs et soumettez des demandes à des ressources protégées et non protégées.
{:shortdesc}


### Avant de commencer

Vous devez disposer des éléments suivants :
  * Une instance d'{{site.data.keyword.appid_short_notm}}.
  * Votre ID titulaire. Dans l'onglet **Données d'identification pour le service** de votre tableau de bord du service, cliquez sur **Afficher les données d'identification**. Il s'agit d'un identificateur unique qui sert à initialiser votre application.
  * Votre région {{site.data.keyword.Bluemix_notm}}. Vous pouvez identifier votre région en recherchant dans l'interface utilisateur. Cette valeur est utilisée pour initialiser votre application.
  <table> <caption> Tableau 1. Régions {{site.data.keyword.Bluemix_notm}} et valeurs de SDK correspondantes </caption>
    <tr>
      <th>Région {{site.data.keyword.Bluemix}}</th>
      <th>Valeur du SDK</th>
    </tr>
    <tr>
      <td>Sud des Etats-Unis</td>
      <td><code>AppID.REGION_US_SOUTH</code> </td>
    </tr>
    <tr>
      <td>Sydney</td>
      <td><code>AppID.REGION_SYDNEY </code></td>
    </tr>
    <tr>
      <td>Royaume-Uni</td>
      <td><code>AppID.REGION_UK </code></td>
    </tr>
    <tr>
      <td>Allemagne</td>
      <td><code>AppID.REGION_GERMANY</code></td>
    </tr>
  </table>

  * Projet Xcode (version 9.0.1 ou ultérieure).
  * CocoaPods (version 1.1.0 ou ultérieure).


### Installation du SDK client

Le SDK client d'{{site.data.keyword.appid_short_notm}} est distribué avec CocoaPods, un gestionnaire de dépendances pour les projets Swift et Cocoa Objective-C . CocoaPods télécharge des artefacts et les rend disponibles dans votre projet.

1. Créez un projet Xcode ou ouvrez un projet existant.
2. Ouvrez ou créez le fichier Pod dans le répertoire du projet.
3. A la suite de la cible de votre projet, ajoutez une dépendance pour le pod 'BluemixAppID' et la commande `use_frameworks!`.

  Par exemple :

  ```swift
  target '<yourTarget>' do
     use_frameworks!
     pod 'BluemixAppID'
  end
  ```
  {: codeblock}

4. Pour télécharger la dépendance `BluemixAppID`, exécutez la commande ci-dessous.

  ```swift
  pod install --repo-update
  ```
  {: codeblock}

6. Ouvrez votre projet Xcode et activez le partage de chaîne de certificats. Accédez à **Paramètres du projet > Capacités > Partage de chaîne de certificats** et sélectionnez l'option d'**activation du partage de chaîne de certificats**.
7. Ouvrez **Paramètres du projet > Information > Types d'URL** et ajoutez un **Type d'URL**. Placez `$(PRODUCT_BUNDLE_IDENTIFIER)` dans les zones de texte **Identificateur** et **Schéma d'URL**.


### Initialisation du SDK client

1. Ajoutez la commande d'importation suivante au fichier `AppDelegate`.

  ```swift
  import BluemixAppID
  ```
  {: codeblock}

2. Initialisez le SDK client en passant les paramètres ID titulaire et région à sa méthode initialize. Bien que ce ne soit pas obligatoire, le code d'initialisation est souvent placé dans la méthode `application:didFinishLaunchingWithOptions` du fichier AppDelegate dans votre application Swift.

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, bluemixRegion: AppID.Region_UK)
  ```
  {: codeblock}

  * Remplacez *tenantId* par l'ID titulaire de votre service.
  * Remplacez AppID.REGION_UK par votre région {{site.data.keyword.appid_short_notm}}.

3. Ajoutez le code suivant à votre fichier AppDelegate.

  ```swift
  func application(_ application: UIApplication, open url: URL, options :[UIApplicationOpenURLOptionsKey : Any]) -> Bool {
          return AppID.sharedInstance.application(application, open: url, options: options)
      }
  ```
  {: codeblock}

Pour plus d'informations, consultez le <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">référentiel GitHub iOS pour {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.

## Configuration du SDK Node.js
{: #nodejs-setup}

### Avant de commencer

* Familiarisez-vous avec le développement d'applications Node.js sur {{site.data.keyword.Bluemix_notm}}.
* Le SDK serveur d'{{site.data.keyword.appid_short_notm}} exige que votre serveur Node.js soit implémenté avec l'<a href="http://expressjs.com/" target="_blank">infrastructure Express<img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.

**Remarque** : D'autres infrastructures, notamment LoopBack, utilisent des infrastructures `Express`. Vous pouvez utiliser le SDK serveur d'{{site.data.keyword.appid_short_notm}} avec toutes ces infrastructures.


### Installation du SDK serveur


1. Depuis la ligne de commande, ouvrez le répertoire dans lequel se trouve votre application Node.js.
2. Exécutez les commandes ci-dessous.

  ```
  npm install -save express
  npm install -save passport
  npm install -save bluemix-appid
  ```
  {: codeblock}

Pour plus d'informations, voir le <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">référentiel GitHub Node.js pour {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.

## Configuration du SDK Swift
{: #swift-setup}

Protégez vos systèmes de back end et vos API avec le SDK serveur {{site.data.keyword.appid_short}}.
{:shortdesc}


### Avant de commencer

Avant d'utiliser le SDK Swift, vous devez satisfaire les prérequis suivants :

* MacOS ou Linux
* OpenSSL 1.0.2 sous Linux
* Installez Swift 3.0.2
* Installez Kitura 1.6


### Installation du SDK

1. Ouvre le fichier `Package.swift` situé dans le répertoire de votre application Swift et ajoutez la dépendance `appid-serversdk-swift`. Par exemple :

  ```swift
  let package = Package(
      name: “myApp",
      dependencies: [
          .package(url: "https://github.com/ibm-cloud-security/appid-serversdk-swift.git", .upToNextMinor(from: “4.0.0")),
      ],
      targets: [
          .target(
              name: "myApp",
              dependencies: ["BluemixAppID"]),
      ]
  )
  ```
  {: codeblock}

2. MacOS : Lorsque vous lancez la génération sur la ligne de commande, tous les packages doivent inclure les balises suivantes :
  ```
  swift build -Xlinker -L/usr/local/opt/openssl/lib -Xcc -I/usr/local/opt/openssl/include
  ```
  {: pre}

3. Utilisez la commande suivante lorsque vous créez un projet xcode :
  ```
  swift package generate-xcodeproj --xcconfig-overrides openssl.xcconfig
  ```
  {: pre}

  Vous pouvez copier le fichier openssl.xcconfig depuis le site <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">{{site.data.keyword.appid_short_notm}} Swift GitHub <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.
  {: tip}
