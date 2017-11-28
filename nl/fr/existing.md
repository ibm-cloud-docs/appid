---

copyright:
  years: 2017
lastupdated: "2017-11-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


# Ajout d'{{site.data.keyword.appid_short_notm}} à une application existante

Vous pouvez utiliser {{site.data.keyword.appid_full}} avec votre
application existante afin d'authentifier et de stocker des informations de profil sur
vos utilisateurs.


## Conditions requises

* Une application iOS Swift, Android, Node.js, Swift ou Liberty for Java existante.
* Une instance existante d'{{site.data.keyword.appid_short_notm}}


## Ajout d'{{site.data.keyword.appid_short_notm}} à une application
Android existante
{: #existing-android}

Vous pouvez ajouter le service {{site.data.keyword.appid_short_notm}} à vos applications Android existantes.

1. Ajoutez le référentiel JitPack à votre fichier build.gradle racine.

  ```gradle
  allprojects {
      		repositories {
         	 ...
         	 maven { url 'https://jitpack.io' }
	    }
  }
  ```
  {: codeblock}

2. Ouvrez le fichier build.gradle pour votre application, recherchez la section
dependencies du fichier, et ajoutez une dépendance de compilation pour le SDK
client d'{{site.data.keyword.appid_short_notm}}.

  ```gradle
  dependencies {
      compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:1.+'
   }
  ```
  {: codeblock}

3. Recherchez la section defaultConfig et ajoutez la ligne de code ci-dessous.

  ```gradle
  defaultConfig {
                         ...
            manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
  ```
  {: codeblock}

4. Synchronisez votre projet avec Gradle.
5. Initialisez le SDK client en transmettant les paramètres de contexte, d'ID titulaire et de région à la méthode initialize. Bien que ce ne soit pas obligatoire, le code d'initialisation est souvent placé dans la méthode onCreate de l'activité principale dans votre application Android.

  ```Java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, <AppID.REGION>);
  ```
  {: codeblock}

    <table>
    <caption> Tableau 1. Explication des composants de la commande </caption>
      <tr>
        <th> Composants </th>
        <th> Description </th>
      </tr>
      <tr>
        <td> <i> tenantID </i> </td>
        <td> Vous pouvez trouver cette valeur en cliquant sur **Afficher les données d'identification** dans l'onglet **Données d'identification pour le service** de votre tableau de bord du service. </td>
      </tr>
      <tr>
        <td> <i> AppID.REGION </i> </td>
        <td> Vous pouvez trouver votre région dans l'interface utilisateur. Les options sont `AppID.REGION_US_SOUTH`, `AppID.REGION_UK` et `AppID.REGION_Sydney`. </td>
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
  {: codeblock}

    <table>
    <caption> Tableau 2. Explication des composants de la commande </caption>
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

## Ajout d'{{site.data.keyword.appid_short_notm}} à une application iOS Swift existante
{: #existing-ios}

1. Ouvrez le fichier Pod dans le répertoire du projet.
2. Sous la cible de votre projet, ajoutez une dépendance pour le pod 'BluemixAppID'. Vérifiez que la commande `use_frameworks!` est également présente sous votre cible.
3. Pour télécharger la dépendance `BluemixAppID`, exécutez la commande ci-dessous.

  ```
  pod install --repo-update
  ```
  {: codeblock}

4. Ouvrez votre projet Xcode et activez le partage de chaîne de certificats. Sous **Paramètres du projet**, cliquez sur **Fonctions** > **Partage de chaîne de certificats**.
5. Sous **Paramètres du projet** > **Information** > **Types d'URL**, ajoutez un **type d'URL**. Renseignez les deux zones de texte **Identificateur** et **Schéma d'URL** avec la valeur ci-dessous.

  ```
  $(PRODUCT_BUNDLE_IDENTIFIER)
  ```
  {: codeblock}

6. Ajoutez l'importation ci-dessous à votre fichier AppDelegate.swift.

  ```swift
  import BluemixAppID
  import BMSCore
  ```
  {: codeblock}

7. Initialisez le SDK client en transmettant les paramètres d'ID titulaire et de région à la méthode initialize. Bien que ce ne soit pas obligatoire, le code d'initialisation est souvent placé dans la méthode application:didFinishLaunchingWithOptions: du fichier AppDelegate dans votre application.

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, bluemixRegion: <AppID.Region>)
  ```
  {: codeblock}

    <table>
    <caption> Tableau 3. Explication des composants de la commande </caption>
      <tr>
        <th> Composants </th>
        <th> Description </th>
      </tr>
      <tr>
        <td> <i> tenantID </i> </td>
        <td> Vous pouvez trouver cette valeur en cliquant sur **Afficher les données d'identification** dans l'onglet **Données d'identification pour le service** de votre tableau de bord du service. </td>
      </tr>
      <tr>
        <td> <i> AppID.REGION </i> </td>
        <td> Vous pouvez trouver votre région dans l'interface utilisateur. Les options sont `AppID.REGION_US_SOUTH`, `AppID.REGION_UK` et `AppID.REGION_Sydney`. </td>
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
  {: codeblock}

    <table>
    <caption> Tableau 4. Explication des composants de la commande </caption>
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

## Ajout d'{{site.data.keyword.appid_short_notm}} à une application Node.js existante
{: #existing-node}

1. Ajoutez le module `bluemix-appid` à votre application Node.js.

  ```javaScript
  npm install --save bluemix-appid
  ```
  {: codeblock}

2. Installez les modules ci-dessous s'ils ne sont pas déjà installés.

  ```javaScript
  npm install --save express
  npm install --save passport
  npm install --save express-session
  ```
  {: codeblock}

3. Ajoutez le code suivant dans votre fichier app.js pour :
    * Configurer votre application Express pour qu'elle utilise le middleware express-session. **Remarque** : vous devez configurer le middleware avec le stockage de session approprié pour les environnements de production. Pour plus d'informations, voir la [documentation expressjs](https://github.com/expressjs/session).
    * Configurer passportjs avec la sérialisation et la désérialisation. Cette configuration est requise pour la persistance de session authentifiée dans les demandes HTTP. Pour plus d'informations, voir la <a href="http://passportjs.org/docs" target="_blank">documentation passportjs<img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.  
    * Procéder à l'extraction des jetons d'accès et d'identité depuis le service {{site.data.keyword.appid_short_notm}} en exécutant une commande get sur l'URL de rappel.

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
  app.get("/protected", passport.authenticate(WebAppStrategy.STRATEGY_NAME)), function(req, res)
    		res.json(req.user);
    });
  ```
  {: codeblock}

    **Remarque** : le service procède à la redirection dans l'ordre suivant :
    1. Adresse URL d'origine de la demande qui a déclenché le processus d'authentification, telle que conservée dans la session HTTP sous la clé `WebAppStrategy.ORIGINAL_URL`.
    2. Redirection réussie, comme spécifié dans `passport.authenticate(name, {successRedirect: "...."}).`
    3. Racine de l'application ("/").

4. Redéployez votre application.


## Ajout d'{{site.data.keyword.appid_short_notm}} à une application Web Swift existante
{: #existing-swift}

1. Ouvrez le fichier `Package.swift` situé dans le répertoire de votre application Swift et ajoutez la dépendance `appid-serversdk-swift`.
  Exemple :

    ```swift
    import PackageDescription

    let package = Package(
      dependencies: [
           	.Package(url: "https://github.com/ibm-cloud-security/appid-serversdk-swift.git", majorVersion: 1)
      ]
    )
    ```
    {: codeblock}

2. Ajoutez le code suivant à votre application Swift pour :
    * Configurer Kitura en vue de l'utilisation du middleware de session. **Remarque** : vous devez configurer Kitura avec le stockage de session approprié pour les environnements de production. Pour plus d'informations, voir la <a href="https://github.com/IBM-Swift/Kitura-Session" target="_blank">documentation Kitura<img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.
    * Procéder à l'extraction des jetons d'accès et d'identité depuis le service {{site.data.keyword.appid_short_notm}} en exécutant une commande get sur l'URL de rappel.

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
  {: codeblock}

  <table>
  <caption> Tableau 5. Explication des composants de la commande </caption>
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



## Ajout d'{{site.data.keyword.appid_short_notm}} à une application Liberty for Java existante
{: #existing-liberty}

Vous pouvez configurer {{site.data.keyword.appid_short_notm}} pour qu'il fonctionne avec vos applications Web Liberty for Java existantes.

1. Ajoutez une fonction <a href="https://www.ibm.com/support/knowledgecenter/en/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/twlp_config_oidc_rp.html" target="_blank">OpenID Connect <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> à votre fichier `server.xml`.

  ```xml
  <feature manager>
  <feature>appSecurity-2.0</feature>
  <feature>openidConnectClient-1.0</feature>  
  ```
  {: codeblock}

2. Dans votre fonction client Open ID Connect, définissez les espaces réservés suivants. Il sont automatiquement remplis ultérieurement par {{site.data.keyword.Bluemix_notm}}. La variable de nom d'instance doit correspondre très exactement à votre nom d'instance {{site.data.keyword.appid_short_notm}}.

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

  **Remarque** : La variable issuerIdentifier varie en fonction de votre région. Il peut s'agir de l'une des variables suivantes :
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

3. Dans votre fichier `server.xml`, définissez votre type de sujet spécial en tant que ALL_AUTHENTICATED_USERS.

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

4. Dans votre élément `<application-bnd>`, <a href="https://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_authorization.html?cp=SSAW57_8.5.5&cm_mc_uid=18498555367014888859884&cm_mc_sid_50200000=1494855872" target="_blank">définissez les rôles <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> tels qu'indiqué dans votre application Web : `web.xml`.

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

5. Obtenez un certificat.

    a. Dans votre tableau de bord {{site.data.keyword.appid_short_notm}}, cliquez sur Données d'identification pour le service.

    b. Cliquez sur **Afficher les données d'identification** et copiez l'URL `oauthServerUrl`.

    c. Ajoutez `/token` à l'URL. Utilisez Firefox pour parcourir l'URL générée et obtenez le certificat. Vous pouvez, par exemple, utiliser l'URL suivante.

    ```
    https://appid-oauth.eu-gb.bluemix.net/oauth/v3/5d12852e-b0a0-46a3-9547-67a4a33a7164/token
    ```
    {: screen}

    d. Dans la barre d'adresses Firefox, cliquez sur l'icône de > **flèche vers la droite** > **plus d'informations** > **afficher le certificat**.

    e. Dans l'onglet **Sécurité**, cliquez sur **Afficher le certificat** > **Détails**.

    f. Exportez le certificat et sauvegardez-le sur votre unité locale en tant que fichier PEM.

6. Ajoutez le certificat dans votre fichier Liberty for Java truststore.jks à l'aide de<a href="https://www.ibm.com/support/knowledgecenter/SSYKE2_6.0.0/com.ibm.java.security.component.60.doc/security-component/keytoolDocs/keytool_overview.html" target="_blank">Liberty Keytool <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> et ajoutez une référence à l'alias de certificat dans l'élément OIDC. Votre `fichier .jks` se trouve dans votre répertoire de serveur : **ressources** > **sécurité** > **<i>nom du fichier de clés certifiées</i>** > **`fichier .jks`**. Vous pouvez utiliser l'une des options suivantes pour ajouter votre certificat au fichier.

    * Sur le terminal, accédez dossier sécurité Liberty for Java : wlp > usr > serveurs > <i>nom de serveur</i> > ressources > sécurité et ajoutez le certificat avec la commande suivante :

      ```
      keytool -importcert -keystore ./trust.jks -file ~/Documents/secbluemix.cer`
      ```
      {: codeblock}      

      **Remarque** : `~/Documents/[nom certificat].cer` indique l'emplacement du fichier sur votre unité locale.

    * Vous pouvez utiliser <a href="http://keystore-explorer.org/index.html" target="_blank">KeyStore Explorer <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> pour ajouter le certificat. Ouvrez KeyStore Explorer et sélectionnez **Open an existing KeyStore**.

7. Dans votre fichier `manifest.yml`, définissez votre instance {{site.data.keyword.appid_short_notm}}.

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

  ```xml
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
         authFilterid="myAuthFilter"
         trustAliasName="my.bluemix.certificate "
      />
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

      <!-- Automatically expand WAR files and EAR files -->
      <applicationManager autoExpand="true"/>

  </server>
  ```
  {: codeblock}



## Ajout d'{{site.data.keyword.appid_short_notm}} à une application existante qui ne s'exécute pas dans {{site.data.keyword.Bluemix_notm}}
{: #existing}

Si vous disposez d'une application Node.js ou Swift qui ne s'exécute pas dans Bluemix, vous pouvez configurer le fonctionnement à distance pour WebAppStrategy ou WebAppKituraCredentialsPlugin. Pour une application Liberty for Java qui ne s'exécute pas sur Bluemix, configurez les variables d'élément OIDC.


Dans votre application Node.js, remplacez `passport.use(new WebAppStrategy());` par le code ci-dessous.

  ```javaScript
  passport.use(new WebAppStrategy({
    	  tenantId: "{tenant-id}",
   	    clientId: "{client-id}",
      	secret: "{secret}",
      	oauthServerUrl: "{oauth-server-url}",
      	redirectUri: "{app-url}" + CALLBACK_URL
      }));
  ```
  {: codeblock}

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
  <caption> Tableau 6. Explication des composants de la commande pour les applications Swift et Node.js </caption>
    <tr>
      <th> Composants </th>
      <th> Description </th>
    </tr>
    <tr>
      <td> <i> tenantID </i> </br> <i> clientID </i> </br> <i> secret </i> </br> <i> oauth-server-url </i> </br> </td>
      <td> Vous pouvez trouver ces valeurs en cliquant sur **Afficher les données d'identification** dans l'onglet **Données d'identification pour le service** de votre tableau de bord du service. </td>
    </tr>
    <tr>
      <td> <i> app-url </i> </td>
      <td> Adresse URL de votre application. </td>
    </tr>
    <tr>
      <td> <i> CALLBACK_URL </i> </td>
      <td> Adresse URL de la page que les utilisateurs voient une fois connectés. </td>
    </tr>
  </table>

Dans vos applications Liberty for Java, effectuez la procédure décrite dans [Ajout d'{{site.data.keyword.appid_short_notm}} à une applicationLiberty for Java existante](/docs/services/appid/existing.html#existing-liberty), mais remplacez les variables d'élément client OIDC par le code suivant.

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
  <caption> Tableau 7. Variables d'élément OIDC pour les applications Liberty for Java qui ne s'exécutent pas sur Bluemix </caption>
    <tr>
      <th> Composant </th>
      <th> Description </th>
    </tr>
    <tr>
    <td> <i> clientID </i> </br> <i> secret </i> </br> <i> oauth-server-url </i> </br> </td>
    <td> Vous pouvez trouver ces valeurs en cliquant sur **Afficher les données d'identification** dans l'onglet **Données d'identification pour le service** de votre tableau de bord du service. </td>
    </tr>
    <tr>
      <td> <i> authorizationEndpointURL </i> </td>
      <td> Ajoutez `/authorization` à la fin de oauthServerURL. </td>
    </tr>
    <tr>
      <td> <i> tokenEndpointUrl </i> </td>
      <td> Ajoutez `/token` à la fin de oauthServerURL. </td>
    </tr>
    <tr>
      <td> <i> jwkEndpointUrl </i> </td>
      <td> Ajoutez `/publickeys` à la fin de oauthServerURL. </td>
    </tr>
    <tr>
      <td> <i> issuerIdentifier </i> </td>
      <td> Varie en fonction de votre région. Il peut s'agir de l'une des valeurs suivantes : </br><ul><li> issuerIdentifier="appid-oauth.ng.bluemix.net" </br><li> issuerIdentifier="appid-oauth.eu-gb.bluemix.net" </br><li> issuerIdentifier="appid-oauth.au-syd.bluemix.net" </ul></td>
    </tr>
    <tr>
      <td> <i> tokenEndpointAuthMethod </i> </td>
      <td> Spécifié en tant que "basic". </td>
    </tr>
    <tr>
      <td> <i> signatureAlgorithm </i> </td>
      <td> Spécifié en tant que "RS256". </td>
    </tr>
    <tr>
      <td> <i> authFilterid </i> </td>
      <td> Liste des ressources à protéger. </td>
    </tr>
    <tr>
      <td> <i> trustAliasName </i> </td>
      <td> Nom de votre certificat dans le magasin de clés de confiance. </td>
    </tr>
  </table>
