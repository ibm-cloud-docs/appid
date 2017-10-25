---

copyright:
  years: 2017
lastupdated: "2017-06-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# Ajout d'{{site.data.keyword.appid_short_notm}} à une application
existante


Vous pouvez utiliser {{site.data.keyword.appid_full}} avec votre
application existante afin d'authentifier et de stocker des informations de profil sur
vos utilisateurs.



## Conditions requises 

* Une application iOS Swift, Android, Node.js ou Swift existante 
* Une instance existante d'{{site.data.keyword.appid_short_notm}} 


## Ajout d'{{site.data.keyword.appid_short_notm}} à une application
Android existante


Vous pouvez ajouter le service App ID à vos applications Android existantes.


1. Ajoutez le référentiel JitPack à votre fichier build.gradle racine.


  ```gradle
  allprojects {
      		repositories {
         	 ...
         	 maven { url 'https://jitpack.io' }
	    }
  }
  ```
  {: pre}

2. Ouvrez le fichier build.gradle pour votre application, recherchez la section
dependencies du fichier, et ajoutez une dépendance de compilation pour le SDK
client d'{{site.data.keyword.appid_short_notm}}. 

  ```gradle
  dependencies {
      compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:1.+'
   }
  ```
  {: pre}

3. Recherchez la section defaultConfig et ajoutez la ligne de code ci-dessous.


  ```gradle
  defaultConfig {
                         ...
            manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
  ```
  {: pre}

4. Synchronisez votre projet avec Gradle.
5. Initialisez le SDK client en transmettant les paramètres de contexte, d'ID titulaire et de région à la méthode initialize. Bien que ce ne soit pas obligatoire, le code d'initialisation est souvent placé dans la méthode onCreate de l'activité principale dans votre application Android.

  ```Java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, <AppID.REGION>);
  ```
  {: pre}

  <table>
  <caption> Tableau 1. Explication des composants de la commande
</caption>
    <tr>
      <th> Composants </th>
      <th> Description </th>
    </tr>
    <tr>
      <td> <i> tenantID </i> </td>
      <td> Vous pouvez trouver cette valeur en cliquant sur **Afficher les données d'identification** dans l'onglet **Données d'identification pour le service** de votre tableau de bord du service.
</td>
    </tr>
    <tr>
      <td> <i> AppID.REGION </i> </td>
      <td> Vous pouvez trouver votre région dans l'interface utilisateur. Les
options sont `AppID.REGION_US_SOUTH`, `AppID.REGION_UK`
et `AppID.REGION_Sydney`. </td>
    </tr>
  </table>

6. Une fois que le SDK client d'{{site.data.keyword.appid_short_notm}} est initialisé, vous pouvez authentifier vos utilisateurs en exécutant le widget de connexion.

  ```Java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launch(this, new AuthorizationListener() {
          @Override
          public void onAuthorizationFailure (AuthorizationException exception) {
          }

          @Override
          public void onAuthorizationCanceled () {
          }

          @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
          }
        });
  ```
  {: pre}

  <table>
  <caption> Tableau 2. Explication des composants de la commande
</caption>
    <tr>
      <th> Composants </th>
      <th> Description </th>
    </tr>
    <tr>
      <td> <i> onAuthorizationFailure </i> </td>
      <td> Une exception est survenue. </td>
    </tr>
    <tr>
      <td> <i> onAuthorizationCanceled </i> </td>
      <td> Le processus d'authentification a été annulé par l'utilisateur. </td>
    </tr>
    <tr>
      <td> <i> onAuthorizationSuccess </i> </td>
      <td> L'utilisateur a été authentifié. </td>
    </tr>
  </table>

## Ajout d'{{site.data.keyword.appid_short_notm}} à une application iOS
Swift existante


1. Ouvrez le fichier Pod dans le répertoire du projet.

2. Sous la cible de votre projet, ajoutez une dépendance pour le pod
'BluemixAppID'. Vérifiez que la commande `use_frameworks!` est
également
présente sous votre cible.
3. Pour télécharger la dépendance `BluemixAppID`, exécutez la
commande ci-dessous. 

  ```
  pod install --repo-update
  ```
  {: pre}

4. Ouvrez votre projet Xcode et activez le partage de chaîne de certificats. Sous **Paramètres du projet**, cliquez sur **Fonctions** > **Partage de chaîne de certificats**.
5. Sous **Paramètres du projet** >
**Information** > **Types d'URL**, ajoutez un
**type d'URL**. Renseignez les deux zones de texte
**Identificateur** et **Schéma d'URL** avec la
valeur ci-dessous. 

  ```
  $(PRODUCT_BUNDLE_IDENTIFIER)
  ```
  {: pre}

6. Ajoutez l'importation ci-dessous à votre fichier AppDelegate.swift.


  ```swift
  import BluemixAppID
  import BMSCore
  ```
  {: pre}

7. Initialisez le SDK client en transmettant les paramètres d'ID titulaire et de région à la méthode initialize. 
Bien que ce ne soit pas obligatoire, le code d'initialisation est souvent placé dans la
méthode application:didFinishLaunchingWithOptions: du fichier AppDelegate dans votre
application. 

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, bluemixRegion: <AppID.Region>)
  ```
  {: pre}

  <table>
  <caption> Tableau 3. Explication des composants de la commande
</caption>
    <tr>
      <th> Composants </th>
      <th> Description </th>
    </tr>
    <tr>
      <td> <i> tenantID </i> </td>
      <td> Vous pouvez trouver cette valeur en cliquant sur **Afficher les
données d'identification** dans l'onglet **Données d'identification
pour le service** de votre tableau de bord du service.
</td>
    </tr>
    <tr>
      <td> <i> AppID.REGION </i> </td>
      <td> Vous pouvez trouver votre région dans l'interface utilisateur. Les options
sont `AppID.REGION_US_SOUTH`, `AppID.REGION_UK` et
`AppID.REGION_Sydney`. </td>
    </tr>
  </table>

8. Ajoutez le code suivant à votre fichier AppDelegate.

  ```swift
  func application(_ application: UIApplication, open url: URL, options :[UIApplicationOpenURLOptionsKey : Any]) -> Bool {
         	return AppID.sharedInstance.application(application, open: url, options: options)
      }
  class delegate : AuthorizationDelegate {
     public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, response:Response?) {
     }

     public func onAuthorizationCanceled() {
     }

     public func onAuthorizationFailure(error: AuthorizationError) {
     }
  }

  AppID.sharedInstance.loginWidget?.launch(delegate: delegate())
  ```
  {: pre}
  <table>
  <caption> Tableau 4. Explication des composants de la commande
</caption>
    <tr>
      <th> Composants </th>
      <th> Description </th>
    </tr>
    <tr>
      <td> <i> onAuthorizationSuccess </i> </td>
      <td> L'utilisateur a été authentifié. </td>
    </tr>
    <tr>
      <td> <i> onAuthorizationCanceled </i> </td>
      <td> Le processus d'authentification a été annulé par l'utilisateur. </td>
    </tr>
    <tr>
      <td> <i> onAuthorizationFailure </i> </td>
      <td> Une exception est survenue. </td>
    </tr>
  </table>

## Ajout d'{{site.data.keyword.appid_short_notm}} à une application
Node.js existante


1. Ajoutez le module `bluemix-appid` à votre application Node.js.


  ```javaScript
  npm install --save bluemix-appid
  ```
  {: pre}

2. Installez les modules ci-dessous s'ils ne sont pas déjà installés.


  ```javaScript
  npm install --save express
  npm install --save passport
  npm install --save express-session
  ```
  {: pre}

3. Ajoutez le code suivant dans votre fichier app.js pour :

    * Configurer votre application Express pour qu'elle utilise
le middleware
express-session. **Remarque** : vous devez configurer le middleware
avec le stockage de session approprié pour les environnements de production.
Pour plus d'informations, voir la
[documentation expressjs](https://github.com/expressjs/session).
    * Configurer passportjs avec la sérialisation et la désérialisation. Cette
configuration est requise pour la persistance de session authentifiée dans les demandes
HTTP. Pour plus d'informations, voir la
[documentation passportjs](http://passportjs.org/docs).
    * Procéder à l'extraction des jetons d'accès et d'identité depuis le
service App ID en exécutant une commande get sur l'URL de rappel.


  ```javaScript
  const express = require("express");
  const session = require("express-session");
  const passport = require("passport");
  const WebAppStrategy = require("bluemix-appid").WebAppStrategy;
  const app = express();
  const CALLBACK_URL = "/ibm/bluemix/appid/callback";
  app.use(session({
      secret: "123456",
      resave: true,
      saveUninitialized: true
    }));
  app.use(passport.initialize());
    app.use(passport.session());

    passport.use(new WebAppStrategy());
  passport.serializeUser(function(user, cb) {
      cb(null, user);
    });

    passport.deserializeUser(function(obj, cb) {
      cb(null, obj);
    });
  app.get(CALLBACK_URL, passport.authenticate(WebAppStrategy.STRATEGY_NAME));
  app.get("/protected", passport.authenticate(WebAppStrategy.STRATEGY_NAME), function(req, res)
    		res.json(req.user);
    });
  ```
  {: pre}

    **Remarque** : le service procède à la redirection dans
l'ordre suivant :

    1. Adresse URL d'origine de la demande qui a déclenché le processus
d'authentification, telle que conservée dans la session HTTP sous la clé
`WebAppStrategy.ORIGINAL_URL`. 
    2. Redirection réussie, comme spécifié dans `passport.authenticate(name, {successRedirect: "...."}).`
    3. Racine de l'application ("/"). 

4. Redéployez votre application. 


## Ajout d'{{site.data.keyword.appid_short_notm}} à une application Web Swift
existante


1. Ouvrez le fichier `Package.swift` situé dans le répertoire de
votre application Swift et ajoutez la dépendance `appid-serversdk-swift`.
  Exemple :

    ```swift
    import PackageDescription

    let package = Package(
      dependencies: [
           	.Package(url: "https://github.com/ibm-cloud-security/appid-serversdk-swift.git", majorVersion: 1)
      ]
    )
    ```
    {: pre}

2. Ajoutez le code suivant à votre application Swift pour :

    * Configurer Kitura en vue de l'utilisation du middleware de session. **Remarque**
: vous devez configurer Kitura avec le stockage de session approprié pour les
environnements de production. Pour plus d'informations, voir la
[documentation Kitura](https://github.com/IBM-Swift/Kitura-Session).
    * Procédez à l'extraction des jetons d'accès et d'identité depuis le service
App ID en exécutant une commande get sur l'URL de rappel.


  ```swift
  import Foundation
  import Kitura
  import KituraSession
  import Credentials
  import SwiftyJSON
  import BluemixAppID
  let router = Router()
  let session = Session(secret: "Some secret")
  router.all(middleware: session)
  let webappKituraCredentialsPlugin = WebAppKituraCredentialsPlugin()
  let kituraCredentials = Credentials()
  kituraCredentials.register(plugin: webappKituraCredentialsPlugin)
  router.get(CALLBACK_URL,
    handler: kituraCredentials.authenticate(credentialsType: webappKituraCredentialsPlugin.name,
      successRedirect: LANDING_PAGE_URL,
      failureRedirect: LANDING_PAGE_URL
      ))
  router.get("/protected", handler: kituraCredentials.authenticate(credentialsType: webappKituraCredentialsPlugin.name), { (request, response, next) in
    let appIdAuthContext:JSON? = request.session?[WebAppKituraCredentialsPlugin.AuthContext]
      let identityTokenPayload:JSON? = appIdAuthContext?["identityTokenPayload"]
    guard appIdAuthContext?.dictionary != nil, identityTokenPayload?.dictionary != nil else {
      response.status(.unauthorized)
          return next()
      }
    response.send(json: identityTokenPayload!)
    next()
    })
  ```
  {: pre}

  <table>
  <caption> Tableau 6. Explication des composants de la commande
</caption>
    <tr>
      <th> Composants </th>
      <th> Description </th>
    </tr>
    <tr>
      <td> <i> var CALLBACK_URL </i> </td>
      <td> /ibm/bluemix/appid/callback </td>
    </tr>
    <tr>
      <td> <i> var LANDING_PAGE_URL </i> </td>
      <td> /index.html </td>
    </tr>
    </table>

5. Redéployez votre application. 



## Ajout d'{{site.data.keyword.appid_short_notm}} à une application
existante qui ne s'exécute pas dans {{site.data.keyword.Bluemix_notm}}


Si vous disposez d'une application Node.js ou Swift qui ne s'exécute pas dans
Bluemix, vous pouvez configurer le fonctionnement à distance pour WebAppStrategy ou
WebAppKituraCredentialsPlugin.



Dans votre application Node.js, remplacez `passport.use(new
WebAppStrategy());` par le code ci-dessous.

  ```javaScript
  passport.use(new WebAppStrategy({
    	  tenantId: "{tenant-id}",
   	    clientId: "{client-id}",
      	secret: "{secret}",
      	oauthServerUrl: "{oauth-server-url}",
      	redirectUri: "{app-url}" + CALLBACK_URL
      }));
  ```
{: pre}

Dans votre application Swift, remplacez `let
webappKituraCredentialsPlugin =
WebAppKituraCredentialsPlugin()` par le code ci-dessous. 

  ```swift
  let options = [
        "clientId": "{client-id}",
  	"secret": "{secret}",
  	"tenantId": "{tenant-id}",
  	"oauthServerUrl": "{oauth-server-url}",
  	"redirectUri": "{app-url}" + CALLBACK_URL
  ]
    let webappKituraCredentialsPlugin = WebAppKituraCredentialsPlugin(options: options)
  ```
  {: pre}

<table>
<caption> Tableau 7. Explication des composants de la commande pour les applications
Swift et Node.js
</caption>
  <tr>
    <th> Composants </th>
    <th> Description </th>
  </tr>
  <tr>
    <td> <i> tenantID </i> </br> <i> clientID </i> </br> <i> secret </i> </br> <i> oauth-server-url </i> </br> </td>
    <td> Vous pouvez trouver ces valeurs en cliquant sur **Afficher les données
d'identification** dans l'onglet **Données d'identification pour le
service** de votre tableau de bord du service.
</td>
  </tr>
  <tr>
    <td> <i> app-url </i> </td>
    <td> Adresse URL de votre application. </td>
  </tr>
  <tr>
    <td> <i> CALLBACK_URL </i> </td>
    <td> Adresse URL de la page que les utilisateurs voient une fois connectés.
</td>
  </tr>
</table>
