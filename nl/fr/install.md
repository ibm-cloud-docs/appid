---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}

# Ajout d'{{site.data.keyword.appid_short}} à votre application 
{: #configuring}

Pour commencer avec {{site.data.keyword.appid_short}}, configurez le service dans votre application.
{: shortdesc}


## Configuration du logiciel SDK Android
{: #android-setup}

Construisez vos applications Android avec le logiciel SDK client d'{{site.data.keyword.appid_short}}, initialisez le logiciel SDK, authentifiez les utilisateurs et soumettez des demandes à des ressources protégées et non protégées.
{:shortdesc}


### Avant de commencer
{: #before-android}

Vous devez disposer des éléments suivants :
  * Une instance du service {{site.data.keyword.appid_short_notm}}.
  * Votre ID titulaire. Il s'agit d'un identificateur unique qui sert à initialiser votre application et que vous trouverez dans l'onglet **Données d'identification pour le service** de votre tableau de bord du service. 
  * Votre région {{site.data.keyword.Bluemix}}. Vous pouvez identifier votre région en effectuant une recherche dans l'interface utilisateur. Cette valeur est utilisée pour initialiser votre application.
    <table><caption> Tableau 1. Régions {{site.data.keyword.Bluemix_notm}} et valeurs de logiciel SDK correspondantes</caption>
    <tr>
      <th>Région {{site.data.keyword.Bluemix}}</th>
      <th>Valeur de logiciel SDK</th>
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

### Installation du logiciel SDK
{: #install-android}

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

3. Recherchez la section dependencies dans le fichier `build.gradle` et ajoutez une dépendance de compilation pour le logiciel SDK client d'{{site.data.keyword.appid_short_notm}}. **Remarque** : assurez-vous d'ouvrir le fichier correspondant à votre application et non pas le fichier `build.gradle` du projet.

  ```gradle
   dependencies {
       compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:4.+'
   }
  ```
  {: codeblock}

5. Recherchez la section `defaultConfig` et ajoutez les lignes de code suivantes.

  ```gradle
  defaultConfig {
  ...
  manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
  ```
  {: codeblock}

6. Synchronisez votre projet avec Gradle. Cliquez sur **Tools > Android > Sync Project with Gradle Files**.

### Initialisation du logiciel SDK 
{: #initialize-android}

Initialisez le logiciel SDK client en transmettant les paramètres de contexte, d'ID titulaire et de région à la méthode initialize. Bien que ce ne soit pas obligatoire, le code d'initialisation est souvent placé dans la méthode onCreate de l'activité principale dans votre application Android.

  ```java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, AppID.REGION_UK);
  ```
  {: codeblock}

  <table>
  <caption> Tableau. Explication des composantes de commande </caption>
    <tr>
      <th> Composantes </th>
      <th> Description </th>
    </tr>
    <tr>
      <td> <i> tenantID </i> </td>
      <td> Vous pouvez trouver cette valeur en cliquant sur **Afficher les données d'identification** dans l'onglet **Données d'identification pour le service** de votre tableau de bord du service. </td>
    </tr>
    <tr>
      <td> <i> AppID.REGION </i> </td>
      <td> Vous pouvez trouver votre région dans l'interface utilisateur. Les options sont `AppID.REGION_US_SOUTH`, `AppID.REGION_UK`, `AppID.REGION_Sydney` et `AppID.REGION_Germany`. </td>
    </tr>
  </table>

A présent, vous pouvez configurer vos fournisseurs d'identité et commencer à authentifier les utilisateurs. Pour plus d'informations, consultez le
<a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">référentiel GitHub Android pour {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.


</br>

## Configuration du logiciel SDK Swift iOS
{: #ios-setup}

Construisez vos applications Swift avec le logiciel SDK client d'{{site.data.keyword.appid_short}}, initialisez le logiciel SDK, authentifiez les utilisateurs et soumettez des demandes à des ressources protégées et non protégées.
{:shortdesc}


### Avant de commencer
{: #before-ios}

Vous devez disposer des éléments suivants :
  * Une instance d'{{site.data.keyword.appid_short_notm}}.
  * Votre ID titulaire. Il s'agit d'un identificateur unique qui sert à initialiser votre application et que vous trouverez dans l'onglet **Données d'identification pour le service** de votre tableau de bord du service. 
  * Votre région {{site.data.keyword.Bluemix_notm}}.
  Vous pouvez identifier votre région en effectuant une recherche dans l'interface utilisateur. Cette valeur est utilisée pour initialiser votre application.
  <table> <caption> Tableau. Régions {{site.data.keyword.Bluemix_notm}} et valeurs de logiciel SDK correspondantes </caption>
    <tr>
      <th>Région {{site.data.keyword.Bluemix}}</th>
      <th>Valeur de logiciel SDK</th>
    </tr>
    <tr>
      <td>Sud des Etats-Unis</td>
      <td><code>AppID.REGION_US_SOUTH </code></td>
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


### Installation du logiciel SDK
{: #install-ios}

Le logiciel SDK client d'{{site.data.keyword.appid_short_notm}} est distribué avec CocoaPods, un gestionnaire de dépendances pour les projets Swift et Cocoa Objective-C . CocoaPods télécharge des artefacts et les rend disponibles dans votre projet.

1. Créez un projet Xcode ou ouvrez un projet existant.
2. Ouvrez ou créez le fichier Pod dans le répertoire du projet.
3. Après la cible de votre projet, ajoutez une dépendance pour le pod 'IBMCloudAppID' et la commande `use_frameworks!`. 

  ```swift
  target '<yourTarget>' do
     use_frameworks!
     pod 'IBMCloudAppID'
  end
  ```
  {: codeblock}

4. Téléchargez la dépendance 'IBMCloudAppID'. 

  ```swift
  pod install --repo-update
  ```
  {: codeblock}

6. Activez le partage de la chaîne de certificats dans votre projet Xcode. Accédez à **Paramètres du projet > Capacités > Partage de chaîne de certificats** et sélectionnez l'option d'**activation du partage de chaîne de certificats**.
7. Ouvrez **Paramètres du projet > Information > Types d'URL** et ajoutez un **Type d'URL**. Indiquez la valeur suivante dans les zones de texte **Identificateur** et **Schéma d'URL** : 
  ```
  $(PRODUCT_BUNDLE_IDENTIFIER)
  ```
  {: codeblock}


### Initialisation du logiciel SDK 
{: #initialize-ios}

1. Initialisez le logiciel SDK client en transmettant les paramètres d'ID titulaire et de région à sa méthode initialize. Bien que ce ne soit pas obligatoire, le code d'initialisation est souvent placé dans la méthode `application:didFinishLaunchingWithOptions` du fichier AppDelegate dans votre application Swift.

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, region: AppID.Region_UK)
  ```
  {: codeblock}

  <table>
  <caption> Tableau. Explication des composantes de commande </caption>
    <tr>
      <th> Composantes </th>
      <th> Description </th>
    </tr>
    <tr>
      <td> <i> tenantID </i> </td>
      <td> Vous pouvez trouver cette valeur en cliquant sur **Afficher les données d'identification** dans l'onglet **Données d'identification pour le service** de votre tableau de bord du service. </td>
    </tr>
    <tr>
      <td> <i> AppID.REGION </i> </td>
      <td> Vous pouvez trouver votre région dans l'interface utilisateur. Les options sont `AppID.REGION_US_SOUTH`, `AppID.REGION_UK`, `AppID.REGION_Sydney` et `AppID.REGION_Germany`. </td>
    </tr>
  </table>

2. Ajoutez la commande d'importation suivante au fichier `AppDelegate` : 

    ```swift
    import IBMCloudAppID
    ```
    {: codeblock}

3. Ajoutez le code suivant à votre fichier AppDelegate : 

  ```swift
  func application( application: UIApplication, open url: URL, options :[UIApplicationOpenURLOptionsKey : Any]) -> Bool {
          return AppID.sharedInstance.application(application, open: url, options: options)
      }
  ```
  {: codeblock}

A présent, vous pouvez configurer vos fournisseurs d'identité et commencer à authentifier les utilisateurs. Pour plus d'informations sur le logiciel SDK iOS, voir le <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">référentiel GitHub iOS pour {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.

</br>

## Configuration du logiciel SDK Node.js
{: #nodejs-setup}

### Avant de commencer
{: #before-nodejs}

Assurez-vous que les prérequis suivants sont satisfaits : 
1. Vous avez installé l'[interface de ligne de commande d'IBM Cloud](../cli/index.html).
2. Vous avez implémenté votre serveur Node.js avec l'<a href="http://expressjs.com/" target="_blank">infrastructure Express <img src="../icons/launch-glyph.svg" alt="Icône de lien externe"></a>. Afin d'installer l'infrastructure Express, utilisez la ligne de commande pour ouvrir le répertoire contenant votre application Node.js et exécutez la commande suivante :
  ```
  npm install --save express
  ```
  {: codeblock}
3. Vous avez installé Passport. Utilisez la ligne de commande pour ouvrir le répertoire contenant votre application Node.js et exécutez la commande suivante :
  ```
  npm install --save passport
  ```
  {: codeblock}

**Remarque** : d'autres infrastructures, notamment LoopBack, utilisent des infrastructures `Express`. Vous pouvez utiliser le logiciel SDK serveur d'{{site.data.keyword.appid_short_notm}} avec toutes ces infrastructures.


### Installation du logiciel SDK
{: #install-nodejs}

1. Depuis la ligne de commande, ouvrez le répertoire dans lequel se trouve votre application Node.js.
2. Installez le service {{site.data.keyword.appid_short_notm}}. 
  ```
  npm install --save ibmcloud-appid
  ```
  {: codeblock}

### Initialisation du logiciel SDK 
{: #initialize}

1. Ajoutez les définitions `require` suivantes à votre fichier `server.js` :
    ```
    const express = require('express');
    const session = require('express-session')
    const passport = require('passport');
    const WebAppStrategy = require("ibmcloud-appid").WebAppStrategy;
    const CALLBACK_URL = "/ibm/cloud/appid/callback";
    ```
    {: codeblock}

2. Configurez votre application Express pour qu'elle utilise le middleware express-session. **Remarque** : vous devez configurer le middleware avec le stockage de session approprié pour les environnements de production. Pour plus d'informations, consultez
la <a href="https://github.com/expressjs/session" target="_blank">documentation expressjs <img src="../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.
    ```
    const app = express();
    app.use(session({
        secret: "123456",
        resave: true,
        saveUninitialized: true
        }));
    app.use(passport.initialize());
    app.use(passport.session());
    ```
    {: codeblock}

3. Transmettez l'ID titulaire et les données d'identification pour initialiser le logiciel SDK.
    ```
    passport.use(new WebAppStrategy({
    	  tenantId: "{tenant-id}",
   	    clientId: "{client-id}",
      	secret: "{secret}",
      	oauthServerUrl: "{oauth-server-url}",
      	redirectUri: "{app-url}" + CALLBACK_URL
      }));
    ```
    {: codeblock}

 <table summary="Composantes de commande : applications Node.js">
  <caption>Composantes de commande pour les applications Node.js </caption>
    <tr>
      <th>Composantes</th>
      <th>Description</th>
    </tr>
    <tr>
      <td><i> tenantID </i></td>
      <td>L'ID titulaire est un identificateur unique qui est utilisé pour initialiser votre application. Vous pouvez trouver sa valeur dans le tableau de bord du service {{site.data.keyword.appid_short_notm}} en cliquant sur **Afficher les données d'identification** dans l'onglet **Données d'identification pour le service**. </td>
    </tr>
    <tr>
      <td><i> clientID </i> </br> <i> secret </i> </br> <i> oauth-server-url </i> </br> </td>
      <td>Vous pouvez trouver ces valeurs en cliquant sur **Afficher les données d'identification** dans l'onglet **Données d'identification pour le service** de votre tableau de bord du service. </td>
    </tr>
    <tr><td><i>redirectUri</i></td>
    <td>La valeur redirectUri peut être fournie de trois façons : </br>
        1. Manuellement dans new WebAppStrategy({redirectUri: "...."})</br>
        2. Sous forme de variable d'environnement nommée `redirectUri`</br>
        3. Si la valeur n'a pas été fournie de l'une des façons ci-dessus, le logiciel SDK d'App ID tente d'extraire la valeur application_uri de l'application qui s'exécute dans IBM Cloud et ajoute le suffixe par défaut "/ibm/cloud/appid/callback"</td>
    </tr>
    <tr>
      <td><i> CALLBACK_URL </i></td>
      <td>URL de la page que les utilisateurs voient une fois qu'ils sont connectés. </td>
    </tr>
  </table>

4. Configurez passport avec la sérialisation et la désérialisation. Cette étape de configuration est requise pour la persistance de session authentifiée dans les demandes HTTP. Pour plus d'informations, voir la <a href="http://passportjs.org/docs" target="_blank">documentation de passport <img src="../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.

  ```
  passport.serializeUser(function(user, cb) {
    cb(null, user);
    });

  passport.deserializeUser(function(obj, cb) {
    cb(null, obj);
    });
  ```
  {: codeblock}

5. Ajoutez le code suivant dans votre fichier `server.js` pour émettre les redirections de service : 
   ```
   app.get(CALLBACK_URL, passport.authenticate(WebAppStrategy.STRATEGY_NAME));
   app.get('/protected', passport.authenticate(WebAppStrategy.STRATEGY_NAME)), function(req, res)
        res.json(req.user);
   });
   ```
   {: codeblock}

   **Remarque** : le service procède à la redirection dans l'ordre suivant :
    1. Adresse URL d'origine de la demande qui a déclenché le processus d'authentification, telle que conservée dans la session HTTP sous la clé `WebAppStrategy.ORIGINAL_URL`.
    2. Redirection réussie, comme spécifié dans `passport.authenticate(name, {successRedirect: "...."}).`
    3. Racine de l'application ("/").

6. Redéployez votre application.

Pour plus d'informations, voir le <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">référentiel GitHub Node.js pour {{site.data.keyword.appid_short_notm}} <img src="../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.

## Configuration du logiciel SDK Swift
{: #swift-setup}

Protégez vos systèmes de back end et vos API avec le logiciel SDK serveur {{site.data.keyword.appid_short}}.
{:shortdesc}


### Avant de commencer
{: #before-swift}

Avant d'utiliser le logiciel SDK Swift, vous devez satisfaire les prérequis suivants :

* MacOS ou Linux
* OpenSSL 1.0.2 sous Linux
* Installez Swift 3.0.2
* Installez Kitura 1.6


### Installation du logiciel SDK
{: #install-swift}

1. Ouvrez le fichier `Package.swift` situé dans le répertoire de votre application Swift et ajoutez la dépendance `appid-serversdk-swift`. 

  ```swift
  let package = Package(
      name: “myApp",
      dependencies: [
          .package(url: "https://github.com/ibm-cloud-security/appid-serversdk-swift.git", .upToNextMinor(from: “4.0.0")),
      ],
      targets: [
          .target(
              name: "myApp",
              dependencies: ["IBMCloudAppID"]),
      ]
  )
  ```
  {: codeblock}

2. MacOS : lorsque vous lancez la génération sur la ligne de commande, tous les packages doivent inclure les balises suivantes :
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

4. Ajoutez le code suivant à votre application Swift pour :
    * Configurer Kitura en vue de l'utilisation du middleware de session. **Remarque** : vous devez configurer Kitura avec le stockage de session approprié pour les environnements de production. Pour plus d'informations, voir la <a href="https://github.com/IBM-Swift/Kitura-Session" target="_blank">documentation Kitura<img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.
    * Procéder à l'extraction des jetons d'accès et d'identité depuis le service {{site.data.keyword.appid_short_notm}} en exécutant une commande get sur l'URL de rappel.

    ```swift
    import Foundation
    import Kitura
    import KituraSession
    import Credentials
    import SwiftyJSON
    import IBMCloudAppID
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
    {: codeblock}

5. Redéployez votre application.

</br>

## Configuration du logiciel SDK Liberty for Java 
{: #lfj-setup}

Vous pouvez configurer {{site.data.keyword.appid_short_notm}} pour qu'il fonctionne avec vos applications Web Liberty for Java.
{:shortdesc}

1. Ajoutez une fonction <a href="https://www.ibm.com/support/knowledgecenter/en/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/twlp_config_oidc_rp.html" target="_blank">OpenID Connect <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> à votre fichier `server.xml`.

  ```xml
  <feature manager>
  <feature>appSecurity-2.0</feature>
  <feature>openidConnectClient-1.0</feature>  
  ```
  {: codeblock}

2. Dans votre fonction client Open ID Connect, définissez les espaces réservés ci-dessous. Il sont automatiquement remplis ultérieurement par {{site.data.keyword.Bluemix_notm}}. La variable de nom d'instance doit correspondre très exactement à votre nom d'instance {{site.data.keyword.appid_short_notm}}.

  ```
  clientId='${cloud.services.AppID-Instance-Name.credentials.clientId}'
  clientSecret='${cloud.services.AppID-Instance-Name.credentials.clientSecret}'
  authorizationEndpointUrl='${cloud.services.AppID-Instance-Name.credentials.authorizationEndpointUrl}'
  tokenEndpointUrl='${cloud.services.AppID-Instance-Name.credentials.tokenEndpointUrl}'
  jwkEndpointUrl='${cloud.services.AppID-Instance-Name.credentials.jwkEndpointUrl}'
  issuerIdentifier='appid-oauth.ng.bluemix.net'
  tokenEndpointAuthMethod="basic"
  signatureAlgorithm="RS256"
  authFilterid="myAuthFilter"
  ```
  {: codeblock}

  **Remarque** : la variable issuerIdentifier varie en fonction de votre région. Il peut s'agir de l'une des variables suivantes :
  * issuerIdentifier="appid-oauth.ng.bluemix.net"
  * issuerIdentifier="appid-oauth.eu-gb.bluemix.net"
  * issuerIdentifier="appid-oauth.au-syd.bluemix.net"</ul> </td>

3. Définissez un filtre d'autorisation pour indiquer des ressources protégées. Si aucun filtre n'est <a href="https://www.ibm.com/support/knowledgecenter/en/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/rwlp_auth_filter.html" target="_blank">défini <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>, le service protège toutes les ressources.
  ```
  <authFilter id="myAuthFilter">
             <requestUrl id="myRequestUrl" urlPattern="/protected" matchType="contains"/>
    </authFilter>
  ```
  {: codeblock}

4. Dans votre fichier `server.xml`, définissez votre type de sujet spécial en tant que ALL_AUTHENTICATED_USERS.

  ```xml
  <application type="war" id="ProtectedServlet" context-root="/appidSample"
  location="${server.config.dir}/apps/libertySample-1.0.0.war">
    <application-bnd>
        <security-role name="myrole">
        <special-subject type="ALL_AUTHENTICATED_USERS"/>
        </security-role>
            </application-bnd>
        </application>
  ```
  {: codeblock}

5. Dans votre élément `<application-bnd>`, <a href="https://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_authorization.html?cp=SSAW57_8.5.5&cm_mc_uid=18498555367014888859884&cm_mc_sid_50200000=1494855872" target="_blank">définissez les rôles <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> tels qu'indiqués dans votre application Web : `web.xml`.

  ```xml
  <security-role>
  <role-name>myrole</role-name>
  </security-role>

  <security-constraint>
  <web-resource-collection>
  <web-resource-name>ProtectedServlet</web-resource-name>
  <url-pattern>/ProtectedServlet/*</url-pattern>
  <http-method>GET</http-method>
  <http-method>PUT</http-method>
  <http-method>POST</http-method>
  <http-method>DELETE</http-method>
  </web-resource-collection>

  <auth-constraint>
  <role-name>myrole</role-name>
  </auth-constraint>
  <user-data-constraint>
  <transport-guarantee>NONE</transport-guarantee>
  </user-data-constraint>
  </security-constraint>
  ```
  {: codeblock}

6. Obtenez un certificat.

    a. Dans votre tableau de bord {{site.data.keyword.appid_short_notm}}, cliquez sur Données d'identification pour le service.

    b. Cliquez sur **Afficher les données d'identification** et copiez l'URL `oauthServerUrl`.

    c. Ajoutez `/token` à l'URL. Utilisez Firefox pour parcourir l'URL générée et obtenez le certificat. Par exemple, vous pouvez utiliser l'URL suivante :

    ```
    https://appid-oauth.ng.bluemix.net/oauth/v3/5d12852e-b0a0-46a3-9547-67a4a33a7164/token
    ```
    {: screen}

    d. Dans la barre d'adresses Firefox, cliquez sur l'icône de verrouillage > **flèche vers la droite** > **plus d'informations** > **afficher le certificat**.

    e. Dans l'onglet **Sécurité**, cliquez sur **Afficher le certificat** > **Détails**.

    f. Exportez le certificat et sauvegardez-le sur votre unité locale en tant que fichier PEM.

7. Ajoutez le certificat dans votre fichier Liberty for Java truststore.jks à l'aide de <a href="https://www.ibm.com/support/knowledgecenter/SSYKE2_6.0.0/com.ibm.java.security.component.60.doc/security-component/keytoolDocs/keytool_overview.html" target="_blank">Liberty Keytool <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> et ajoutez une référence à l'alias de certificat dans l'élément OIDC. Votre `fichier .jks` se trouve dans votre répertoire de serveur : **resources** > **security** > **<i>nom du fichier de clés de confiance</i>** > **`fichier .jks`**. Vous pouvez utiliser l'une des options suivantes pour ajouter votre certificat au fichier :

    * Sur le terminal, accédez au dossier de sécurité Liberty for Java : wlp > usr > servers > <i>nom de serveur</i> > resources > security et ajoutez le certificat avec la commande suivante :

      ```
      keytool -importcert -keystore ./trust.jks -file ~/Documents/secbluemix.cer`
      ```
      {: codeblock}      

      **Remarque** : `~/Documents/[nom certificat].cer` indique l'emplacement du fichier sur votre unité locale.

    * Vous pouvez utiliser <a href="http://keystore-explorer.org/index.html" target="_blank">KeyStore Explorer <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> pour ajouter le certificat. Ouvrez KeyStore Explorer et sélectionnez **Open an existing KeyStore**.

    **Remarque** : le certificat peut expirer/être changé ; dans ce cas, vous devez mettre à jour votre magasin de clés de confiance avec le nouveau certificat. 

8. Dans votre fichier `manifest.yml`, définissez votre instance {{site.data.keyword.appid_short_notm}}.

  ```yml
  services:
  - <appid service name>

  Manifest.yml file example:
  applications:
  - name: LibertyExampl
  buildpack: liberty-for-java
  instances: 1
  random-route: true
  memory: 512M
  disk_quota: 1024M
  timeout: 180
  services:
  - AppID-Instance-Name
  ```
  {: codeblock}

    Exemple de fichier `server.xml` configuré pour {{site.data.keyword.appid_short_notm}} :

  ```
  <?xml version="1.0" encoding="UTF-8"?>
  <server description="sample server">
      <featureManager>
        <feature>ssl-1.0</feature>
        <feature>servlet-3.1</feature>
        <feature>appSecurity-2.0</feature>
        <feature>openidConnectClient-1.0</feature>  
      </featureManager>
      <openidConnectClient id="MyDefaultRP"
         clientId='${cloud.services.AppID-Instance-Name.credentials.clientId}'
         clientSecret='${cloud.services.AppID-Instance-Name.credentials.clientSecret}'
         authorizationEndpointUrl='${cloud.services.AppID-Instance-Name.credentials.authorizationEndpointUrl}'
         tokenEndpointUrl='${cloud.services.AppID-Instance-Name.credentials.tokenEndpointUrl}'
         jwkEndpointUrl='${cloud.services.AppID-Instance-Name.credentials.jwkEndpointUrl}'
         issuerIdentifier='${cloud.services.AppID-Instance-Name.credentials.appid-oauth.ng.bluemix.net}'
         tokenEndpointAuthMethod="basic"
         signatureAlgorithm="RS256"
         authFilterid="myAuthFilter"/>
      <authFilter id="myAuthFilter">
               <requestUrl id="myRequestUrl" urlPattern="/protected" matchType="contains"/>
      </authFilter>
      <application type="war" id="ProtectedServlet" context-root="/appidSample" location="${server.config.dir}/apps/libertySample-1.0.0.war">
          <application-bnd>
              <security-role name="myrole">
                  <special-subject type="ALL_AUTHENTICATED_USERS" />
              </security-role>
          </application-bnd>
      </application>
   <applicationManager autoExpand="true"/>
  <keyStore id="defaultKeyStore" password="Password"/>
  <keyStore id="defaulttrustore" password="Liberty" location="<FileContainingCertificated>.jks"/>
  <ssl id="defaultSSLSettings" keyStoreRef="defaultKeyStore" trustStoreRef="defaulttrustore"/>
  <sslDefault sslRef="defaultSSLSettings"/>
      <httpEndpoint id="defaultHttpEndpoint" httpPort="9080" host="*" httpsPort="9443" />
      <applicationManager autoExpand="true"/>
  </server>
  ```
  {: codeblock}



</br>

## Ajout d'{{site.data.keyword.appid_short_notm}} à une application existante qui ne s'exécute pas dans {{site.data.keyword.Bluemix_notm}}
{: #existing}

Vous pouvez ajouter {{site.data.keyword.appid_short_notm}} à des applications qui ne s'exécutent pas dans {{site.data.keyword.Bluemix_notm}}. Vous trouverez quelques exemples dans cette rubrique, mais vous pouvez aussi utiliser le service avec d'autres langages. 

</br>

**Node.js**

Dans votre application Node.js, remplacez `passport.use(new WebAppStrategy());` par le code ci-dessous.

  ```
  passport.use(new WebAppStrategy({
    	  tenantId: "{tenant-id}",
   	    clientId: "{client-id}",
      	secret: "{secret}",
      	oauthServerUrl: "{oauth-server-url}",
      	redirectUri: "{app-url}" + CALLBACK_URL
      }));
  ```
  {: codeblock}

  <table>
  <caption> Tableau. Explication des composantes de commande pour les applications Node.js </caption>
    <tr>
      <th> Composantes </th>
      <th> Description </th>
    </tr>
    <tr>
      <td><code>tenant-id</code> </br> <code> clientID </code> </br> <code> secret </code> </br> <code> oauth-server-url </code> </br></td>
      <td> Vous pouvez trouver ces valeurs en cliquant sur **Afficher les données d'identification** dans l'onglet **Données d'identification pour le service** de votre tableau de bord du service. </td>
    </tr>
    <tr>
      <td><code> app-url </code></td>
      <td>Adresse URL de votre application.</td>
    </tr>
    <tr>
      <td><code> CALLBACK_URL </code></td>
      <td> Adresse URL de la page que les utilisateurs voient une fois qu'ils sont connectés. </td>
    </tr>
  </table>

</br>

**Swift**

Dans votre application Swift, remplacez `let webappKituraCredentialsPlugin = WebAppKituraCredentialsPlugin()` par le code ci-dessous.

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
  {: codeblock}

  <table>
  <caption>Tableau. Explication des composantes de commande pour les applications Swift </caption>
    <tr>
      <th> Composantes </th>
      <th> Description </th>
    </tr>
    <tr>
      <td><code>tenant-id</code> </br> <code> clientID </code> </br> <code> secret </code> </br> <code> oauth-server-url </code> </br></td>
      <td> Vous pouvez trouver ces valeurs en cliquant sur **Afficher les données d'identification** dans l'onglet **Données d'identification pour le service** de votre tableau de bord du service. </td>
    </tr>
    <tr>
      <td><code> app-url </code></td>
      <td>Adresse URL de votre application.</td>
    </tr>
    <tr>
      <td><code> CALLBACK_URL </code></td>
      <td> Adresse URL de la page que les utilisateurs voient une fois qu'ils sont connectés. </td>
    </tr>
  </table>


</br>

**Liberty for Java**

Dans vos applications Liberty for Java, effectuez les opérations décrites dans [Configuration du logiciel SDK Liberty for Java](#lfj-setup), mais remplacez les variables d'élément du client OIDC par le code suivant : 

  ```
  clientId='App ID client_ID'
  clientSecret='App Id Secret'      
  authorizationEndpointUrl='oauthServerUrl/authorization'       
  tokenEndpointUrl='oauthServerUrl/token'
  jwkEndpointUrl='oauthServerUrl/publickeys'
  issuerIdentifier='Changed according to the region'
  tokenEndpointAuthMethod="basic"
  signatureAlgorithm="RS256"
  authFilterid="myAuthFilter"
  trustAliasName="my.bluemix.certificate"
  ```
  {: codeblock}

  <table>
  <caption>Tableau. Variables d'élément OIDC pour les applications Liberty for Java </caption>
    <tr>
      <th> Composante </th>
      <th> Description </th>
    </tr>
    <tr>
    <td><code> clientID </code> </br> <code> secret </code> </br> <code> oauth-server-url </code> </br></td>
    <td>Vous pouvez trouver ces valeurs en cliquant sur **Afficher les données d'identification** dans l'onglet **Données d'identification pour le service** de votre tableau de bord du service.</td>
    </tr>
    <tr>
      <td><code> authorizationEndpointURL </code></td>
      <td> Ajoutez `/authorization` à la fin de oauthServerURL.</td>
    </tr>
    <tr>
      <td><code> tokenEndpointUrl </code></td>
      <td>Ajoutez `/token` à la fin de oauthServerURL.</td>
    </tr>
    <tr>
      <td><code> jwkEndpointUrl </code></td>
      <td>Ajoutez `/publickeys` à la fin de oauthServerURL.</td>
    </tr>
    <tr>
      <td><code> issuerIdentifier </code></td>
      <td>Varie en fonction de votre région. Il peut s'agir de l'une des valeurs suivantes : </br><ul><li>issuerIdentifier="appid-oauth.ng.bluemix.net" </br><li> issuerIdentifier="appid-oauth.eu-gb.bluemix.net" </br><li>issuerIdentifier="appid-oauth.au-syd.bluemix.net"</ul></td>
    </tr>
    <tr>
      <td><code> tokenEndpointAuthMethod </code></td>
      <td>Spécifié en tant que "basic".</td>
    </tr>
    <tr>
      <td><code> signatureAlgorithm </code></td>
      <td>Spécifié en tant que "RS256".</td>
    </tr>
    <tr>
      <td><code> authFilterid </code></td>
      <td>Liste des ressources à protéger.</td>
    </tr>
    <tr>
      <td><code> trustAliasName </code></td>
      <td>Nom de votre certificat dans le magasin de clés de confiance.</td>
    </tr>
  </table>
