---

copyright:
  years: 2017
lastupdated: "2017-06-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# {{site.data.keyword.appid_short_notm}} zu einer vorhandenen App hinzufügen

Sie können {{site.data.keyword.appid_full}} mit einer vorhandenen Anwendung zum Authentifizieren und Speichern von Profilinformationen von Benutzern verwenden. 


## Voraussetzungen 

* Eine vorhandene iOS Swift-, Android-, Node.js- oder Swift-Anwendung. 
* Eine vorhandene Instanz von {{site.data.keyword.appid_short_notm}}. 


## {{site.data.keyword.appid_short_notm}} zu einer vorhandenen Android-App hinzufügen

Sie können den App ID-Service zu Ihren vorhandenen Android-Anwendungen hinzufügen. 

1. Fügen Sie das JitPack-Repository zur Stammdatei 'build.gradle' hinzu. 

  ```gradle
  allprojects {
      		repositories {
		    ...
         	 maven { url 'https://jitpack.io' }
	    }
    }
  ```
  {: pre}

2. Öffnen Sie die Datei 'build.gradle' für Ihre Anwendung, suchen Sie den Abschnitt für die Abhängigkeiten der Datei und fügen Sie eine Kompilierungsabhängigkeit für das {{site.data.keyword.appid_short_notm}}-Client-SDK hinzu. 

  ```gradle
  dependencies {
      compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:1.+'
   }
  ```
  {: pre}

3. Suchen Sie den Abschnitt 'defaultConfig' und fügen Sie die folgende Codezeile hinzu. 

  ```gradle
  defaultConfig {
                         ...
            manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
  ```
  {: pre}

4. Synchronisieren Sie Ihr Projekt mit Gradle. 
5. Initialisieren Sie das SDK, indem Sie die Parameter 'context', 'tenantID' und 'region' an die Methode 'initialize' übergeben. Eine gängige, wenngleich nicht verbindliche, Position für den Initialisierungscode ist die Methode 'onCreate' der Hauptaktivität in Ihrer Android-Anwendung.

  ```Java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, <AppID.REGION>);
  ```
  {: pre}

  <table>
  <caption> Tabelle 1. Erklärungen für Komponenten der Befehle</caption>
    <tr>
      <th> Komponenten</th>
      <th> Beschreibung</th>
    </tr>
    <tr>
      <td> <i> tenantID </i> </td>
      <td> Diesen Wert können Sie durch Klicken auf **Berechtigungsnachweise anzeigen** in der Registerkarte **Serviceberechtigungsnachweise** des Service-Dashboards suchen. </td>
    </tr>
    <tr>
      <td> <i> AppID.REGION </i> </td>
      <td> Sie finden Ihre Region in der Benutzerschnittstelle. Die Optionen sind `AppID.REGION_US_SOUTH`, `AppID.REGION_UK` oder `AppID.REGION_Sydney`. </td>
    </tr>
  </table>

6. Nach der Initialisierung des {{site.data.keyword.appid_short_notm}}-Client-SDK können Sie Benutzer authentifizieren, indem Sie das Anmelde-Widget ausführen.

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
  <caption> Tabelle 2. Erklärungen für Komponenten der Befehle</caption>
    <tr>
      <th> Komponenten</th>
      <th> Beschreibung</th>
    </tr>
    <tr>
      <td> <i> onAuthorizationFailure </i> </td>
      <td> Es ist eine Ausnahmebedingung aufgetreten. </td>
    </tr>
    <tr>
      <td> <i> onAuthorizationCanceled </i> </td>
      <td> Der Authentifizierungsprozess wurde vom Benutzer abgebrochen. </td>
    </tr>
    <tr>
      <td> <i> onAuthorizationSuccess </i> </td>
      <td> Der Benutzer wurde authentifiziert. </td>
    </tr>
  </table>

## {{site.data.keyword.appid_short_notm}} zu einer vorhandenen iOS Swift-App hinzufügen

1. Öffnen Sie die Podfile im Projektverzeichnis. 
2. Fügen Sie unter dem Ziel Ihres Projekts eine Abhängigkeit für den Pod 'BluemixAppID' hinzu. Stellen Sie sicher, dass sich der Befehl `use_frameworks!` auch unter dem Ziel befindet.
3. Führen Sie den folgenden Befehl aus, um die `BluemixAppID`-Abhängigkeit herunterzuladen. 

  ```
  pod install --repo-update
  ```
  {: pre}

4. Öffnen Sie Ihr Xcode-Projekt und aktivieren Sie das Keychain-Sharing. Klicken Sie in **Projekteinstellungen** auf **Funktionen** > **Keychain-Sharing**.
5. Fügen Sie unter **Projekteinstellungen** > **Info** > **URL-Typen** eine Angabe für **URL-Typ** hinzu. Geben Sie diesen Wert in die Textfelder **ID** und **URL-Schema** ein. 

  ```
  $(PRODUCT_BUNDLE_IDENTIFIER)
  ```
  {: pre}

6. Fügen Sie den folgenden Import zur Datei 'AppDelegate.swift' hinzu. 

  ```swift
  import BluemixAppID
  import BMSCore
  ```
  {: pre}

7. Initialisieren Sie das SDK, indem Sie die Parameter 'tenantID' und 'region' an die Methode 'initialize' übergeben. Eine gängige, wenngleich nicht verbindliche, Position für den Initialisierungscode ist die Methode 'application:didFinishLaunchingWithOptions:' von AppDelegate in Ihrer Anwendung. 

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, bluemixRegion: <AppID.Region>)
  ```
  {: pre}

  <table>
  <caption> Tabelle 3. Erklärungen für Komponenten der Befehle</caption>
    <tr>
      <th> Komponenten</th>
      <th> Beschreibung</th>
    </tr>
    <tr>
      <td> <i> tenantID </i> </td>
      <td> Diesen Wert können Sie durch Klicken auf **Berechtigungsnachweise anzeigen** in der Registerkarte **Serviceberechtigungsnachweise** des Service-Dashboards suchen. </td>
    </tr>
    <tr>
      <td> <i> AppID.REGION </i> </td>
      <td> Sie finden Ihre Region in der Benutzerschnittstelle. Die Optionen sind `AppID.REGION_US_SOUTH`, `AppID.REGION_UK` oder `AppID.REGION_Sydney`. </td>
    </tr>
  </table>

8. Fügen Sie den folgenden Code zur AppDelegate-Datei hinzu. 

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
  <caption> Tabelle 4. Erklärungen für Komponenten der Befehle</caption>
    <tr>
      <th> Komponenten</th>
      <th> Beschreibung</th>
    </tr>
    <tr>
      <td> <i> onAuthorizationSuccess </i> </td>
      <td> Der Benutzer wurde authentifiziert. </td>
    </tr>
    <tr>
      <td> <i> onAuthorizationCanceled </i> </td>
      <td> Der Authentifizierungsprozess wurde vom Benutzer abgebrochen. </td>
    </tr>
    <tr>
      <td> <i> onAuthorizationFailure </i> </td>
      <td> Es ist eine Ausnahmebedingung aufgetreten. </td>
    </tr>
  </table>

## {{site.data.keyword.appid_short_notm}} zu einer vorhandenen Node.js-Web-App hinzufügen

1. Fügen Sie das Modul `bluemix-appid` zur Anwendung 'Node.js' hinzu. 

  ```javaScript
  npm install --save bluemix-appid
  ```
  {: pre}

2. Installieren Sie die folgenden Module, sofern diese noch nicht installiert sind. 

  ```javaScript
  npm install --save express
  npm install --save passport
  npm install --save express-session
  ```
  {: pre}

3. Fügen Sie Ihrer Anwendung die folgende app.js-Datei hinzu: 
    * Richten Sie die Express-App so ein, dass Middleware des Typs 'express-session' verwendet wird.
**Hinweis**: Sie müssen die Middleware mit dem passenden Sitzungsspeicher für die Produktionsumgebungen konfigurieren. Weitere Informationen finden Sie unter [expressjs-Dokumente](https://github.com/expressjs/session). 
    * Konfigurieren Sie passportjs mit Serialisierung und ohne Deserialisierung. Dies ist für eine authentifizierte Sitzungsfortdauer für HTTP-Anforderungen erforderlich. Weitere Informationen finden Sie unter [passportjs-Dokumente](http://passportjs.org/docs). 
    * Rufen Sie durch Ausführen eines Abrufbefehls für die Rückruf-URL die Zugriffs- und Identitätstoken vom App-ID-Service ab. 

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

    **Hinweis**: Vom Service wird in der folgenden Reihenfolge weitergeleitet: 
    1. Die ursprüngliche URL der Anforderung, von der der Authentifizierungsprozess ausgelöst wurde, wie in der HTTP-Sitzung unter dem Schlüssel `WebAppStrategy.ORIGINAL_URL` dauerhaft festgelegt. 
    2. Eine erfolgreiche Weiterleitung, wie in `passport.authenticate(name, {successRedirect: "...."}).`
    3. Stammverzeichnis der Anwendung ("/")

4. Stellen Sie die Anwendung erneut bereit. 


## {{site.data.keyword.appid_short_notm}} zu einer vorhandenen Swift-Webanwendung hinzufügen

1. Öffnen Sie die Datei `Package.swift`, die sich im Verzeichnis Ihrer Swift-App befindet, und fügen Sie die Abhängigkeit `appid-serversdk-swift` hinzu. Beispiel:

    ```swift
    import PackageDescription

    let package = Package(
      dependencies: [
          .Package(url: "https://github.com/ibm-cloud-security/appid-serversdk-swift.git", majorVersion: 1)
      ]
  )
    ```
    {: pre}

2. Fügen Sie den folgenden Code zur Ihrer Swift-Anwendung hinzu: 
    * Richten Sie Kitura zur Verwendung als Sitzungs-Middleware ein.
**Hinweis**: Sie müssen Kitura mit dem passenden Sitzungsspeicher für die Produktionsumgebungen konfigurieren. Weitere Informationen finden Sie unter [Kitura-Dokumente](https://github.com/IBM-Swift/Kitura-Session). 
    * Rufen Sie durch Ausführen eines Abrufbefehls für die Rückruf-URL die Zugriffs- und Identitätstoken vom App-ID-Service ab. 

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
      }      response.send(json: identityTokenPayload!)
      next()
  })
  ```
  {: pre}

  <table>
  <caption> Tabelle 6. Erklärungen für Komponenten der Befehle</caption>
    <tr>
      <th> Komponenten</th>
      <th> Beschreibung</th>
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

5. Stellen Sie die Anwendung erneut bereit. 



## {{site.data.keyword.appid_short_notm}} zu einer vorhandenen Anwendung hinzufügen, auf der {{site.data.keyword.Bluemix_notm}} nicht ausgeführt wird


Wenn Sie über eine Node.js- oder Swift-Anwendung verfügen, auf der Bluemix nicht ausgeführt wird, können Sie WebAppStrategy oder WebAppKituraCredentialsPlugin für die Arbeit über Fernzugriff konfigurieren. 


Ersetzen Sie in der Node.js-App `passport.use(new WebAppStrategy());` durch den folgenden Code. 

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

Ersetzen Sie in der Swift-App `let webappKituraCredentialsPlugin = WebAppKituraCredentialsPlugin()` durch den folgenden Code. 

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
<caption> Tabelle 7. Erklärungen für Befehlskomponenten für Swift- und Node.js-Apps</caption>
  <tr>
    <th> Komponenten</th>
    <th> Beschreibung</th>
  </tr>
  <tr>
    <td> <i> tenantID </i> </br> <i> clientID </i> </br> <i> secret </i> </br> <i> oauth-server-url </i> </br> </td>
    <td> Diese Werte können Sie durch Klicken auf **Berechtigungsnachweise anzeigen** in der Registerkarte **Serviceberechtigungsnachweise** des Service-Dashboards suchen. </td>
  </tr>
  <tr>
    <td> <i> app-url </i> </td>
    <td> Die URL der Anwendung. </td>
  </tr>
  <tr>
    <td> <i> CALLBACK_URL </i> </td>
    <td> Die URL für die Seite, die den Benutzern nach ihrer Anmeldung angezeigt wird. </td>
  </tr>
</table>
