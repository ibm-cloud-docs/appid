---

copyright:
  years: 2017
lastupdated: "2017-11-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


# {{site.data.keyword.appid_short_notm}} zu einer vorhandenen App hinzufügen

Sie können {{site.data.keyword.appid_full}} mit einer vorhandenen Anwendung zum Authentifizieren und Speichern von Profilinformationen von Benutzern verwenden.


## Voraussetzungen

* Eine vorhandene iOS Swift-, Android-, Node.js-, Swift- oder Liberty for Java-Anwendung.
* Eine vorhandene Instanz von {{site.data.keyword.appid_short_notm}}.


## {{site.data.keyword.appid_short_notm}} zu einer vorhandenen Android-App hinzufügen
{: #existing-android}

Sie können den {{site.data.keyword.appid_short_notm}}-Service zu den vorhandenen Android-Anwendungen hinzufügen.

1. Fügen Sie das JitPack-Repository zur Stammdatei 'build.gradle' hinzu.

  ```gradle
  allprojects {
      		repositories {
         	 ...
         	 maven { url 'https://jitpack.io' }
	    }
  }
  ```
  {: codeblock}

2. Öffnen Sie die Datei 'build.gradle' für Ihre Anwendung, suchen Sie den Abschnitt für die Abhängigkeiten der Datei und fügen Sie eine Kompilierungsabhängigkeit für das {{site.data.keyword.appid_short_notm}}-Client-SDK hinzu.

  ```gradle
  dependencies {
      compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:1.+'
   }
  ```
  {: codeblock}

3. Suchen Sie den Abschnitt 'defaultConfig' und fügen Sie die folgende Codezeile hinzu.

  ```gradle
  defaultConfig {
                         ...
            manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
  ```
  {: codeblock}

4. Synchronisieren Sie Ihr Projekt mit Gradle.
5. Initialisieren Sie das SDK, indem Sie die Parameter 'context', 'tenantID' und 'region' an die Methode 'initialize' übergeben. Eine gängige, wenngleich nicht verbindliche, Position für den Initialisierungscode ist die Methode 'onCreate' der Hauptaktivität in Ihrer Android-Anwendung.

  ```Java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, <AppID.REGION>);
  ```
  {: codeblock}

    <table>
    <caption> Tabelle 1. Erklärungen für Komponenten der Befehle </caption>
      <tr>
        <th> Komponenten </th>
        <th> Beschreibung </th>
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
  {: codeblock}

    <table>
    <caption> Tabelle 2. Erklärungen für Komponenten der Befehle </caption>
      <tr>
        <th> Komponenten </th>
        <th> Beschreibung </th>
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
{: #existing-ios}

1. Öffnen Sie die Podfile im Projektverzeichnis.
2. Fügen Sie unter dem Ziel Ihres Projekts eine Abhängigkeit für den Pod 'BluemixAppID' hinzu. Stellen Sie sicher, dass sich der Befehl `use_frameworks!` auch unter dem Ziel befindet.
3. Führen Sie den folgenden Befehl aus, um die `BluemixAppID`-Abhängigkeit herunterzuladen.

  ```
  pod install --repo-update
  ```
  {: codeblock}

4. Öffnen Sie Ihr Xcode-Projekt und aktivieren Sie das Keychain-Sharing. Klicken Sie in **Projekteinstellungen** auf **Funktionen** > **Keychain-Sharing**.
5. Fügen Sie unter **Projekteinstellungen** > **Info** > **URL-Typen** eine Angabe für **URL-Typ** hinzu. Geben Sie diesen Wert in die Textfelder **ID** und **URL-Schema** ein.

  ```
  $(PRODUCT_BUNDLE_IDENTIFIER)
  ```
  {: codeblock}

6. Fügen Sie den folgenden Import zur Datei 'AppDelegate.swift' hinzu.

  ```swift
  import BluemixAppID
  import BMSCore
  ```
  {: codeblock}

7. Initialisieren Sie das SDK, indem Sie die Parameter 'tenantID' und 'region' an die Methode 'initialize' übergeben. Eine gängige, wenngleich nicht verbindliche, Position für den Initialisierungscode ist die Methode 'application:didFinishLaunchingWithOptions:' von AppDelegate in Ihrer Anwendung.

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, bluemixRegion: <AppID.Region>)
  ```
  {: codeblock}

    <table>
    <caption> Tabelle 3. Erklärungen für Komponenten der Befehle </caption>
      <tr>
        <th> Komponenten </th>
        <th> Beschreibung </th>
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
  {: codeblock}

    <table>
    <caption> Tabelle 4. Erklärungen für Komponenten der Befehle </caption>
      <tr>
        <th> Komponenten </th>
        <th> Beschreibung </th>
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
{: #existing-node}

1. Fügen Sie das Modul `bluemix-appid` zur Anwendung 'Node.js' hinzu.

  ```javaScript
  npm install --save bluemix-appid
  ```
  {: codeblock}

2. Installieren Sie die folgenden Module, sofern diese noch nicht installiert sind.

  ```javaScript
  npm install --save express
  npm install --save passport
  npm install --save express-session
  ```
  {: codeblock}

3. Fügen Sie Ihrer Anwendung die folgende app.js-Datei hinzu:
    * Richten Sie die Express-App so ein, dass Middleware des Typs 'express-session' verwendet wird. **Hinweis**: Sie müssen die Middleware mit dem passenden Sitzungsspeicher für die Produktionsumgebungen konfigurieren. Weitere Informationen finden Sie unter [expressjs-Dokumente](https://github.com/expressjs/session).
    * Konfigurieren Sie passportjs mit Serialisierung und ohne Deserialisierung. Dies ist für eine authentifizierte Sitzungsfortdauer für HTTP-Anforderungen erforderlich. Weitere Informationen finden Sie in den <a href="http://passportjs.org/docs" target="_blank">passportjs-Dokumenten <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>.  
    * Rufen Sie durch Ausführen eines Abrufbefehls für die Callback-URL die Zugriffs- und Identitätstoken vom {{site.data.keyword.appid_short_notm}}-Service ab. 

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

    **Hinweis**: Vom Service wird in der folgenden Reihenfolge weitergeleitet:
    1. Die ursprüngliche URL der Anforderung, von der der Authentifizierungsprozess ausgelöst wurde, wie in der HTTP-Sitzung unter dem Schlüssel `WebAppStrategy.ORIGINAL_URL` dauerhaft festgelegt.
    2. Eine erfolgreiche Weiterleitung, wie in `passport.authenticate(name, {successRedirect: "...."}).`
    3. Stammverzeichnis der Anwendung ("/")

4. Stellen Sie die Anwendung erneut bereit.


## {{site.data.keyword.appid_short_notm}} zu einer vorhandenen Swift-Webanwendung hinzufügen
{: #existing-swift}

1. Öffnen Sie die Datei `Package.swift`, die sich im Verzeichnis Ihrer Swift-App befindet, und fügen Sie die Abhängigkeit `appid-serversdk-swift` hinzu.
  Beispiel:

    ```swift
    import PackageDescription

    let package = Package(
      dependencies: [
           	.Package(url: "https://github.com/ibm-cloud-security/appid-serversdk-swift.git", majorVersion: 1)
      ]
    )
    ```
    {: codeblock}

2. Fügen Sie den folgenden Code zur Ihrer Swift-Anwendung hinzu:
    * Richten Sie Kitura zur Verwendung als Sitzungs-Middleware ein. **Hinweis**: Sie müssen Kitura mit dem passenden Sitzungsspeicher für die Produktionsumgebungen konfigurieren. Weitere Informationen finden Sie in den <a href="https://github.com/IBM-Swift/Kitura-Session" target="_blank">Kitura-Dokumenten <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>.
    * Rufen Sie durch Ausführen eines Abrufbefehls für die Callback-URL die Zugriffs- und Identitätstoken vom {{site.data.keyword.appid_short_notm}}-Service ab. 

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
  <caption> Tabelle 5. Erklärungen für Komponenten der Befehle</caption>
    <tr>
      <th> Komponenten </th>
      <th> Beschreibung </th>
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



## {{site.data.keyword.appid_short_notm}} zu einer vorhandenen Liberty for Java-App hinzufügen
{: #existing-liberty}

Sie können {{site.data.keyword.appid_short_notm}} so konfigurieren, dass die vorhandenen Liberty for Java-Webanwendungen verwendet werden.

1. Fügen Sie ein <a href="https://www.ibm.com/support/knowledgecenter/en/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/twlp_config_oidc_rp.html" target="_blank">OpenID Connect-Feature <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> zur Datei `server.xml` hinzu.

  ```xml
  <feature manager>
  <feature>appSecurity-2.0</feature>
  <feature>openidConnectClient-1.0</feature>  
  ```
  {: codeblock}

2. Definieren Sie im Open ID Connect-Client-Feature die folgenden Platzhalter. Diese werden zu einem späteren Zeitpunkt automatisch von {{site.data.keyword.Bluemix_notm}} ausgefüllt. Die Variable für den Instanznamen muss dem Namen Ihrer {{site.data.keyword.appid_short_notm}}-Instanz exakt entsprechen.

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

  **Hinweis**: Die Variable 'issuerIdentifier' variiert abhängig von der jeweiligen Region. Die folgenden Variablen sind möglich:
  * issuerIdentifier="appid-oauth.ng.bluemix.net"
  * issuerIdentifier="appid-oauth.eu-gb.bluemix.net"
  * issuerIdentifier="appid-oauth.au-syd.bluemix.net"</ul> </td>

3. Definieren Sie einen Berechtigungsfilter für die Angabe geschützter Ressourcen. Ist kein Filter <a href="https://www.ibm.com/support/knowledgecenter/en/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/rwlp_auth_filter.html" target="_blank">definiert <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>, schützt der Service alle Ressourcen.
  ```
  <authFilter id="myAuthFilter">
             <requestUrl id="myRequestUrl" urlPattern="/protected" matchType="contains"/>
    </authFilter>
  ```
  {: codeblock}

3. Definieren Sie in der Datei `server.xml` den speziellen Subjekttyp als ALL_AUTHENTICATED_USERS.

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

4. Im Element `<application-bnd>` müssen Sie die <a href="https://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_authorization.html?cp=SSAW57_8.5.5&cm_mc_uid=18498555367014888859884&cm_mc_sid_50200000=1494855872" target="_blank">Rollen definieren <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>, die in der Web-App angegeben sind: `web.xml`.

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

5. Rufen Sie ein Zertifikat ab.

    a. Klicken Sie im {{site.data.keyword.appid_short_notm}}-Dashboard auf die Serviceberechtigungsnachweise.

    b. Klicken Sie auf **Berechtigungsnachweise anzeigen** und kopieren Sie die `oauthServerUrl`.

    c. Fügen Sie `/token` zur URL hinzu. Verwenden Sie Firefox zum Anzeigen der Ausgabe-URL und zum Abrufen des Zertifikats. Die folgende URL kann als Beispiel verwendet werden.

    ```
    https://appid-oauth.eu-gb.bluemix.net/oauth/v3/5d12852e-b0a0-46a3-9547-67a4a33a7164/token
    ```
    {: screen}

    d. Klicken Sie in der Adressleiste von Firefox auf das Sperrsymbol > **Rechtspfeil** > **Weitere Informationen** > **Zertifikat anzeigen**.

    e. Klicken Sie auf der Registerkarte **Sicherheit** auf **Zertifikat anzeigen** > **Details**.

    f. Exportieren Sie das Zertifikat und speichern Sie es im lokalen Laufwerk als PEM-Datei.

6. Fügen Sie das Zertifikat zur Liberty for Java-Datei 'truststore.jks' hinzu, indem Sie das <a href="https://www.ibm.com/support/knowledgecenter/SSYKE2_6.0.0/com.ibm.java.security.component.60.doc/security-component/keytoolDocs/keytool_overview.html" target="_blank">Liberty Keytool <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> verwenden, und fügen Sie einen Verweis auf den Zertifikatsaliasnamen im OIDC-Element hinzu. Die `.jks`-Datei befindet sich im Serververzeichnis: **Ressourcen** > **Sicherheit** > **<i>Truststore-Dateiname</i>** > **`.jks`-Datei**. Sie können eine der folgenden Optionen verwenden, um das Zertifikat zur Datei hinzuzufügen.

    * Rufen Sie auf dem Terminal den Liberty for Java-Sicherheitsordner auf: wlp > usr > servers > <i>Servername</i> > resources > security. Verwenden Sie den folgenden Befehl, um das Zertifikat hinzuzufügen.

      ```
      keytool -importcert -keystore ./trust.jks -file ~/Documents/secbluemix.cer`
      ```
      {: codeblock}      

      **Hinweis**: `~/Documents/[zertifikatsname].cer` stellt die Dateiposition auf dem lokalen Laufwerk dar.

    * Sie können <a href="http://keystore-explorer.org/index.html" target="_blank">KeyStore Explorer <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> verwenden, um das Zertifikat hinzuzufügen. Öffnen Sie KeyStore Explorer und wählen Sie **Vorhandenen Keystore öffnen** aus.

7. Definieren Sie in der Datei `manifest.yml` Ihre {{site.data.keyword.appid_short_notm}}-Instanz.

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

    Beispiel für eine Datei `server.xml`, die für {{site.data.keyword.appid_short_notm}} konfiguriert ist:

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

      <!-- WAR- und EAR-Dateien automatisch erweitern -->
      <applicationManager autoExpand="true"/>

  </server>
  ```
  {: codeblock}



## {{site.data.keyword.appid_short_notm}} zu einer vorhandenen Anwendung hinzufügen, auf der {{site.data.keyword.Bluemix_notm}} nicht ausgeführt wird
{: #existing}

Wenn Sie über eine Node.js- oder Swift-Anwendung verfügen, auf der Bluemix nicht ausgeführt wird, können Sie WebAppStrategy oder WebAppKituraCredentialsPlugin für die Arbeit über Fernzugriff konfigurieren. Konfigurieren Sie für eine Liberty for Java-App, die nicht unter Bluemix ausgeführt wird, die OIDC-Elementvariablen.


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
  {: codeblock}

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
  {: codeblock}

  <table>
  <caption> Tabelle 6. Erklärungen für Befehlskomponenten für Swift- und Node.js-Apps</caption>
    <tr>
      <th> Komponenten </th>
      <th> Beschreibung </th>
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

Führen Sie in den Liberty for Java-Apps die unter [{{site.data.keyword.appid_short_notm}} zu einer vorhandenen Liberty for Java-App hinzufügen](/docs/services/appid/existing.html#existing-liberty) aufgeführten Schritte aus, ersetzen Sie jedoch die OIDC-Clientelementvariablen durch den folgenden Code.

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
  <caption> Tabelle 7. OIDC-Elementvariablen für Liberty for Java-Apps, die nicht unter Bluemix ausgeführt werden </caption>
    <tr>
      <th> Komponente </th>
      <th> Beschreibung </th>
    </tr>
    <tr>
    <td> <i> clientID </i> </br> <i> secret </i> </br> <i> oauth-server-url </i> </br> </td>
    <td> Diese Werte können Sie durch Klicken auf **Berechtigungsnachweise anzeigen** in der Registerkarte **Serviceberechtigungsnachweise** des Service-Dashboards suchen. </td>
    </tr>
    <tr>
      <td> <i> authorizationEndpointURL </i> </td>
      <td> Fügen Sie `/authorization` am Ende von 'oauthServerURL' hinzu. </td>
    </tr>
    <tr>
      <td> <i> tokenEndpointUrl </i> </td>
      <td> Fügen Sie `/token` am Ende von 'oauthServerURL' hinzu. </td>
    </tr>
    <tr>
      <td> <i> jwkEndpointUrl </i> </td>
      <td> Fügen Sie `/publickeys` am Ende von 'oauthServerURL' hinzu. </td>
    </tr>
    <tr>
      <td> <i> issuerIdentifier </i> </td>
      <td> Variiert abhängig von der jeweiligen Region. Folgendes ist möglich: </br><ul><li> issuerIdentifier="appid-oauth.ng.bluemix.net" </br><li> issuerIdentifier="appid-oauth.eu-gb.bluemix.net" </br><li> issuerIdentifier="appid-oauth.au-syd.bluemix.net" </ul></td>
    </tr>
    <tr>
      <td> <i> tokenEndpointAuthMethod </i> </td>
      <td> Als "basic" angegeben. </td>
    </tr>
    <tr>
      <td> <i> signatureAlgorithm </i> </td>
      <td> Als "RS256" angegeben. </td>
    </tr>
    <tr>
      <td> <i> authFilterid </i> </td>
      <td> Liste der zu schützenden Ressourcen. </td>
    </tr>
    <tr>
      <td> <i> trustAliasName </i> </td>
      <td> Name des Zertifikats im Truststore. </td>
    </tr>
  </table>
