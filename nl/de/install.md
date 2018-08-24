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

# {{site.data.keyword.appid_short}} zu Ihrer App hinzufügen
{: #configuring}

Beginnen Sie mit {{site.data.keyword.appid_short}}, indem Sie den Service in Ihrer Anwendung einrichten.
{: shortdesc}


## Android-SDK einrichten
{: #android-setup}

Erstellen Sie Ihre Android-Apps mit dem {{site.data.keyword.appid_short}}-Client-SDK, initialisieren Sie das SDK, authentifizieren Sie Benutzer und senden Sie Anforderungen an geschützte und nicht geschützte Ressourcen.
{:shortdesc}


### Vorbereitungen
{: #before-android}

Sie benötigen die folgenden Informationen:
  * Eine Instanz des {{site.data.keyword.appid_short_notm}}-Service.
  * Ihre Tenant-ID. Ihre Tenant-ID ist eine eindeutige ID zur Initialisierung der App und wird auf der Registerkarte **Serviceberechtigungsnachweise** in Ihrem Service-Dashboard angezeigt. 
  * Ihre {{site.data.keyword.Bluemix}}-Region. Sie finden Ihre Region in Ihrer Benutzerschnittstelle. Der Wert wird für die Initialisierung Ihrer App verwendet.
    <table><caption> Tabelle 1: {{site.data.keyword.Bluemix_notm}}-Regionen und entsprechende SDK-Werte</caption>
    <tr>
      <th>{{site.data.keyword.Bluemix}}-Region</th>
      <th>SDK-Wert</th>
    </tr>
    <tr>
      <td>Vereinigte Staaten (Süden)</td>
      <td><code>AppID.REGION_US_SOUTH</code> </td>
    </tr>
    <tr>
      <td>Sydney</td>
      <td><code>AppID.REGION_SYDNEY </code></td>
    </tr>
    <tr>
      <td>Vereinigtes Königreich</td>
      <td><code>AppID.REGION_UK </code></td>
    </tr>
    <tr>
      <td>Deutschland</td>
      <td><code>AppID.REGION_GERMANY</code></td>
    </tr>
  </table>

  * <a href="https://developers.google.com/web/tools/setup/" target="_blank">Android Studio-Projekt<img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>, das für das Arbeiten mit Gradle eingerichtet ist.

### SDK installieren
{: #install-android}

1. Erstellen Sie ein Android Studio-Projekt oder öffnen Sie ein vorhandenes Projekt.
2. Fügen Sie das JitPack-Repository zur Stammdatei `build.gradle` hinzu.

  ```gradle
    allprojects {
	    repositories {
		    ...
		    maven { url 'https://jitpack.io' }
	    }
    }
  ```
  {: codeblock}

3. Suchen Sie den Abschnitt für Abhängigkeiten ('dependencies') in der Datei `build.gradle` und fügen Sie die Abhängigkeit 'compile' für das {{site.data.keyword.appid_short_notm}}-Client-SDK hinzu.**Hinweis**: Stellen Sie sicher, dass Sie die Datei für Ihre App öffnen, nicht die Projektdatei `build.gradle`.

  ```gradle
   dependencies {
       compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:4.+'
   }
  ```
  {: codeblock}

5. Suchen Sie den Abschnitt `defaultConfig` und fügen Sie die folgenden Codezeilen hinzu.

  ```gradle
  defaultConfig {
  ...
  manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
  ```
  {: codeblock}

6. Synchronisieren Sie Ihr Projekt mit Gradle. Klicken Sie auf **Tools > Android > Sync Project with Gradle Files**.

### SDK initialisieren
{: #initialize-android}

Initialisieren Sie das Client-SDK, indem Sie die Parameter 'context', 'tenantID' und 'region' an die Methode 'initialize' übergeben. Eine gängige, wenngleich nicht verbindliche, Position für den Initialisierungscode ist die Methode 'onCreate' der Hauptaktivität in Ihrer Android-Anwendung.

  ```java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, AppID.REGION_UK);
  ```
  {: codeblock}

  <table>
  <caption> Tabelle. Beschreibung von Befehlskomponenten</caption>
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
      <td> Sie finden Ihre Region in der Benutzerschnittstelle. Optionen: `AppID.REGION_US_SOUTH`, `AppID.REGION_UK`, `AppID.REGION_Sydney` und `AppID.REGION_Germany`. </td>
    </tr>
  </table>

Jetzt können Sie mit dem Konfigurieren der Identitätsprovider und der Authentifizierung von Benutzern beginnen! Weitere Informationen finden Sie im Abschnitt zum <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">{{site.data.keyword.appid_short_notm}}-Android-GitHub-Repository <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>.


</br>

## iOS-Swift-SDK einrichten
{: #ios-setup}

Erstellen Sie Ihre Swift-Anwendungen mit dem {{site.data.keyword.appid_short}}-Client-SDK, initialisieren Sie das SDK, authentifizieren Sie Benutzer und senden Sie Anforderungen an geschützte und nicht geschützte Ressourcen.
{:shortdesc}


### Vorbereitungen
{: #before-ios}

Sie benötigen die folgenden Informationen:
  * Eine Instanz von {{site.data.keyword.appid_short_notm}}.
  * Ihre Tenant-ID. Ihre Tenant-ID ist eine eindeutige ID zur Initialisierung der App und wird auf der Registerkarte **Serviceberechtigungsnachweise** in Ihrem Service-Dashboard angezeigt. 
  * Ihre {{site.data.keyword.Bluemix_notm}}-Region.
  Sie finden Ihre Region in Ihrer Benutzerschnittstelle. Der Wert wird für die Initialisierung Ihrer App verwendet.
  <table> <caption> Tabelle. {{site.data.keyword.Bluemix_notm}}-Regionen und entsprechende SDK-Werte</caption>
    <tr>
      <th>{{site.data.keyword.Bluemix}}-Region</th>
      <th>SDK-Wert</th>
    </tr>
    <tr>
      <td>Vereinigte Staaten (Süden)</td>
      <td><code>AppID.REGION_US_SOUTH </code></td>
    </tr>
    <tr>
      <td>Sydney</td>
      <td><code>AppID.REGION_SYDNEY </code></td>
    </tr>
    <tr>
      <td>Vereinigtes Königreich</td>
      <td><code>AppID.REGION_UK </code></td>
    </tr>
    <tr>
      <td>Deutschland</td>
      <td><code>AppID.REGION_GERMANY</code></td>
    </tr>
  </table>

  * Ein Xcode-Projekt (Version 9.0.1 oder höher).
  * CocoaPods (Version 1.1.0 oder höher).


### SDK installieren
{: #install-ios}

Das {{site.data.keyword.appid_short_notm}}-Client-SDK wird mit CocoaPods verteilt, einem Abhängigkeitenmanager für Swift- und Objective-C Cocoa-Projekte. CocoaPods lädt Artefakte herunter und stellt sie für Ihr Projekt zur Verfügung.

1. Erstellen Sie ein Xcode-Projekt oder öffnen Sie ein vorhandenes Projekt.
2. Öffnen oder erstellen Sie die Podfile im Projektverzeichnis.
3. Fügen Sie nach dem Ziel Ihres Projekts eine Abhängigkeit für den Pod 'IBMCloudAppID' und den Befehl `use_frameworks!` hinzu. 

  ```swift
  target '<yourTarget>' do
     use_frameworks!
     pod 'IBMCloudAppID'
  end
  ```
  {: codeblock}

4. Laden Sie die 'IBMCloudAppID'-Abhängigkeit herunter. 

  ```swift
  pod install --repo-update
  ```
  {: codeblock}

6. Ermöglichen Sie die gemeinsame Nutzung der Schlüsselkette in Ihrem XCode-Projekt. Navigieren Sie zu **Projekteinstellungen > Funktionen > Keychain-Sharing** und wählen Sie **Keychain-Sharing aktivieren** aus.
7. Öffnen Sie **Projekteinstellungen > Info > URL-Typen** und fügen Sie einen **URL-Typ** hinzu. Stellen Sie den folgenden Wert in die beiden Textfelder **ID** und **URL-Schema**. 
  ```
  $(PRODUCT_BUNDLE_IDENTIFIER)
  ```
  {: codeblock}


### SDK initialisieren
{: #initialize-ios}

1. Initialisieren Sie das Client-SDK, indem Sie die Parameter 'tenantID' und 'region' an die Methode 'initialize' übergeben. Eine gängige, wenngleich nicht verbindliche, Position für den Initialisierungscode ist die Methode `application:didFinishLaunchingWithOptions` von AppDelegate in Ihrer Swift-Anwendung.

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, region: AppID.Region_UK)
  ```
  {: codeblock}

  <table>
  <caption> Tabelle. Beschreibung von Befehlskomponenten</caption>
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
      <td> Sie finden Ihre Region in der Benutzerschnittstelle. Optionen: `AppID.REGION_US_SOUTH`, `AppID.REGION_UK`, `AppID.REGION_Sydney` und `AppID.REGION_Germany`. </td>
    </tr>
  </table>

2. Fügen Sie folgenden Import zu Ihrer Datei `AppDelegate` hinzu.

    ```swift
    import IBMCloudAppID
    ```
    {: codeblock}

3. Fügen Sie den folgenden Code zur AppDelegate-Datei hinzu.

  ```swift
  func application( application: UIApplication, open url: URL, options :[UIApplicationOpenURLOptionsKey : Any]) -> Bool {
          return AppID.sharedInstance.application(application, open: url, options: options)
      }
  ```
  {: codeblock}

Jetzt können Sie mit dem Konfigurieren der Identitätsprovider und der Authentifizierung von Benutzern beginnen! Weitere Informationen zum iOS-SDK finden Sie im Abschnitt zum <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">{{site.data.keyword.appid_short_notm}}-iOS-GitHub-Repository <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>.

</br>

## Node.js-SDK einrichten
{: #nodejs-setup}

### Vorbereitungen
{: #before-nodejs}

Stellen Sie sicher, dass die folgenden Anforderungen erfüllt werden können: 
1. Installieren Sie [IBM Cloud CLI](../cli/index.html). 
2. Implementieren Sie Ihren Node.js-Server mit dem <a href="http://expressjs.com/" target="_blank">Express-Framework <img src="../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>. Wechseln Sie zum Installieren des Express-Frameworks in der Befehlszeilenschnittstelle zum Verzeichnis mit Ihrer Node.js-App und führen Sie den folgenden Befehl aus: 
  ```
  npm install --save express
  ```
  {: codeblock}
3. Installieren Sie Passport. Wechseln Sie zum Installieren von Passport in der Befehlszeilenschnittstelle zum Verzeichnis mit Ihrer Node.js-App und führen Sie den folgenden Befehl aus: 
  ```
  npm install --save passport
  ```
  {: codeblock}

**Hinweis**: Von anderen Frameworks werden `Express`-Frameworks verwendet, wie zum Beispiel LoopBack. Sie können das {{site.data.keyword.appid_short_notm}}-Server-SDK mit einem beliebigen dieser Frameworks verwenden.


### SDK installieren
{: #install-nodejs}

1. Wechseln Sie in der Befehlszeile zum Verzeichnis mit Ihrer Node.js-App. 
2. Installieren Sie den {{site.data.keyword.appid_short_notm}}-Service. 
  ```
  npm install --save ibmcloud-appid
  ```
  {: codeblock}

### SDK initialisieren
{: #initialize}

1. Fügen Sie die folgenden `require`-Definitionen in Ihrer Datei `server.js` hinzu.
    ```
    const express = require('express');
    const session = require('express-session')
    const passport = require('passport');
    const WebAppStrategy = require("ibmcloud-appid").WebAppStrategy;
    const CALLBACK_URL = "/ibm/cloud/appid/callback";
    ```
    {: codeblock}

2. Richten Sie die Express-App so ein, dass Middleware des Typs 'express-session' verwendet wird. **Hinweis**: Sie müssen die Middleware mit dem passenden Sitzungsspeicher für die Produktionsumgebungen konfigurieren. Weitere Informationen finden Sie in der <a href="https://github.com/expressjs/session" target="_blank">Dokumentation zu expressjs<img src="../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>.
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

3. Übergeben Sie die Tenant-ID und die Berechtigungsnachweise, um das SDK zu initialisieren.
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

 <table summary="Befehlskomponenten: Node.js apps">
  <caption>Befehlskomponenten für Node.js-Apps</caption>
    <tr>
      <th>Komponenten</th>
      <th>Beschreibung</th>
    </tr>
    <tr>
      <td><i> tenantID </i></td>
      <td>Die Tenant-ID ist eine eindeutige ID zur Initialisierung der App. Sie finden diesen Wert, indem Sie im Service-Dashboard für {{site.data.keyword.appid_short_notm}} in der Registerkarte **Serviceberechtigungsnachweise** auf **Berechtigungsnachweise anzeigen** klicken. </td>
    </tr>
    <tr>
      <td><i> clientID </i> </br> <i> secret </i> </br> <i> oauth-server-url </i> </br> </td>
      <td>Diese Werte finden Sie, indem Sie in der Registerkarte **Serviceberechtigungsnachweise** des Service-Dashboards auf **Berechtigungsnachweise anzeigen** klicken. </td>
    </tr>
    <tr><td><i>redirectUri</i></td>
    <td>Der Wert 'redirectUri' kann auf verschiedene Arten bereitgestellt werden: </br>
        1. Manuell im neuen Parameter 'WebAppStrategy({redirectUri: "...."})'</br>
        2. Als Umgebungsvariable namens `redirectUri`</br>
        3. Fehlen diese Angaben, versucht das App ID-SDK den Wert für 'application_uri' der Anwendung abzurufen, die in IBM CLoud ausgeführt wird, und hängt ein Standardsuffix namens '/ibm/cloud/appid/callback' an. </td>
    </tr>
    <tr>
      <td><i> CALLBACK_URL </i></td>
      <td>Die URL für die Seite, die den Benutzern nach ihrer Anmeldung angezeigt wird. </td>
    </tr>
  </table>

4. Konfigurieren Sie Passport mit Serialisierung und ohne Deserialisierung. Dieser Konfigurationsschritt ist für ein Aufrechterhalten authentifizierter Sitzungen für HTTP-Anforderungen erforderlich. Weitere Informationen finden Sie in der <a href="http://passportjs.org/docs" target="_blank">Dokumentation zu Passport<img src="../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>. 

  ```
  passport.serializeUser(function(user, cb) {
    cb(null, user);
    });

  passport.deserializeUser(function(obj, cb) {
    cb(null, obj);
    });
  ```
  {: codeblock}

5. Fügen Sie den nachfolgend dargestellten Code in der Datei `server.js` hinzu, um die Serviceweiterleitungen auszuführen: 
   ```
   app.get(CALLBACK_URL, passport.authenticate(WebAppStrategy.STRATEGY_NAME));
   app.get('/protected', passport.authenticate(WebAppStrategy.STRATEGY_NAME)), function(req, res)
        res.json(req.user);
   });
   ```
   {: codeblock}

   **Hinweis**: Vom Service wird in der folgenden Reihenfolge weitergeleitet:
    1. Die ursprüngliche URL der Anforderung, von der der Authentifizierungsprozess ausgelöst wurde, wie in der HTTP-Sitzung unter dem Schlüssel `WebAppStrategy.ORIGINAL_URL` dauerhaft festgelegt.
    2. Eine erfolgreiche Weiterleitung, wie in `passport.authenticate(name, {successRedirect: "...."}).`
    3. Stammverzeichnis der Anwendung ("/")

6. Stellen Sie die Anwendung erneut bereit.

Weitere Informationen finden Sie im Abschnitt zum <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">{{site.data.keyword.appid_short_notm}}-Node.js GitHub-Repository <img src="../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>.

## Swift-SDK einrichten
{: #swift-setup}

Schützen Sie Ihre Back-Ends und APIs mit dem {{site.data.keyword.appid_short}}-Server-SDK.
{:shortdesc}


### Vorbereitungen
{: #before-swift}

Vor der Arbeit mit dem Swift-SDK müssen Sie folgende Voraussetzungen erfüllen:

* Entweder MacOS oder Linux
* OpenSSL 1.0.2 unter Linux
* Installieren Sie Swift 3.0.2.
* Installieren Sie Kitura 1.6.


### SDK installieren
{: #install-swift}

1. Öffnen Sie die Datei `Package.swift`, die sich im Verzeichnis Ihrer Swift-App befindet, und fügen Sie die Abhängigkeit `appid-serversdk-swift` hinzu.

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

2. Bei MacOS: Wenn Sie den Build über die Befehlszeile erstellen, sollten alle Pakete die folgenden Flags enthalten.
  ```
  swift build -Xlinker -L/usr/local/opt/openssl/lib -Xcc -I/usr/local/opt/openssl/include
  ```
  {: pre}

3. Verwenden Sie folgenden Befehl, wenn Sie ein xcodeproject erstellen:
  ```
  swift package generate-xcodeproj --xcconfig-overrides openssl.xcconfig
  ```
  {: pre}

  Sie können die Datei 'openssl.xcconfig' vom <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">{{site.data.keyword.appid_short_notm}} Swift GitHub <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> kopieren.
  {: tip}

4. Fügen Sie den folgenden Code zur Ihrer Swift-Anwendung hinzu:
    * Richten Sie Kitura zur Verwendung als Sitzungs-Middleware ein. **Hinweis**: Sie müssen Kitura mit dem passenden Sitzungsspeicher für die Produktionsumgebungen konfigurieren. Weitere Informationen finden Sie in der <a href="https://github.com/IBM-Swift/Kitura-Session" target="_blank">Dokumentation zu Kitura<img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>.
    * Rufen Sie durch Ausführen eines Abrufbefehls für die Callback-URL die Zugriffs- und Identitätstoken vom {{site.data.keyword.appid_short_notm}}-Service ab.

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

5. Stellen Sie die Anwendung erneut bereit.

</br>

## Liberty for Java-SDK einrichten
{: #lfj-setup}

Sie können {{site.data.keyword.appid_short_notm}} für eine Verwendung Ihrer Liberty for Java-Webanwendungen konfigurieren.
{:shortdesc}

1. Fügen Sie ein <a href="https://www.ibm.com/support/knowledgecenter/en/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/twlp_config_oidc_rp.html" target="_blank">OpenID Connect-Feature <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> in der Datei `server.xml` hinzu.

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

4. Definieren Sie in der Datei `server.xml` den speziellen Subjekttyp als ALL_AUTHENTICATED_USERS.

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

5. Im Element `<application-bnd>` müssen Sie die <a href="https://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_authorization.html?cp=SSAW57_8.5.5&cm_mc_uid=18498555367014888859884&cm_mc_sid_50200000=1494855872" target="_blank">Rollen definieren <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>, die in der Web-App angegeben sind: `web.xml`.

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

6. Rufen Sie ein Zertifikat ab.

    a. Klicken Sie im {{site.data.keyword.appid_short_notm}}-Dashboard auf die Serviceberechtigungsnachweise.

    b. Klicken Sie auf **Berechtigungsnachweise anzeigen** und kopieren Sie die `oauthServerUrl`.

    c. Fügen Sie `/token` zur URL hinzu. Verwenden Sie Firefox zum Anzeigen der Ausgabe-URL und zum Abrufen des Zertifikats. Die folgende URL kann als Beispiel verwendet werden.

    ```
    https://appid-oauth.ng.bluemix.net/oauth/v3/5d12852e-b0a0-46a3-9547-67a4a33a7164/token
    ```
    {: screen}

    d. Klicken Sie in der Adressleiste von Firefox auf das Sperrsymbol > **Rechtspfeil** > **Weitere Informationen** > **Zertifikat anzeigen**.

    e. Klicken Sie auf der Registerkarte **Sicherheit** auf **Zertifikat anzeigen** > **Details**.

    f. Exportieren Sie das Zertifikat und speichern Sie es im lokalen Laufwerk als PEM-Datei.

7. Fügen Sie das Zertifikat zur Liberty for Java-Datei 'truststore.jks' hinzu, indem Sie das <a href="https://www.ibm.com/support/knowledgecenter/SSYKE2_6.0.0/com.ibm.java.security.component.60.doc/security-component/keytoolDocs/keytool_overview.html" target="_blank">Liberty Keytool <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> verwenden, und fügen Sie einen Verweis auf den Zertifikatsaliasnamen im OIDC-Element hinzu. Die `.jks`-Datei befindet sich im Serververzeichnis: **Ressourcen** > **Sicherheit** > **<i>Truststore-Dateiname</i>** > **`.jks`-Datei**. Sie können eine der folgenden Optionen verwenden, um das Zertifikat zur Datei hinzuzufügen.

    * Rufen Sie auf dem Terminal den Liberty for Java-Sicherheitsordner auf: wlp > usr > servers > <i>Servername</i> > resources > security. Verwenden Sie den folgenden Befehl, um das Zertifikat hinzuzufügen.

      ```
      keytool -importcert -keystore ./trust.jks -file ~/Documents/secbluemix.cer`
      ```
      {: codeblock}      

      **Hinweis**: `~/Documents/[zertifikatsname].cer` stellt die Dateiposition auf dem lokalen Laufwerk dar.

    * Sie können <a href="http://keystore-explorer.org/index.html" target="_blank">KeyStore Explorer <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> verwenden, um das Zertifikat hinzuzufügen. Öffnen Sie KeyStore Explorer und wählen Sie **Vorhandenen Keystore öffnen** aus.

    **Hinweis**: Das Zertifikat ist möglicherweise verfallen oder es wurde geändert. Aktualisieren Sie Ihren Truststore in diesem Fall mit dem neuen Zertifikat. 

8. Definieren Sie in der Datei `manifest.yml` Ihre {{site.data.keyword.appid_short_notm}}-Instanz.

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

## {{site.data.keyword.appid_short_notm}} zu einer vorhandenen Anwendung hinzufügen, auf der {{site.data.keyword.Bluemix_notm}} nicht ausgeführt wird
{: #existing}

Sie können {{site.data.keyword.appid_short_notm}} zu Anwendungen hinzufügen, die nicht in {{site.data.keyword.Bluemix_notm}} ausgeführt werden. Entsprechende Beispiele finden Sie in diesem Abschnitt. Die Beispiele decken jedoch nicht alle Sprachen ab, mit denen Sie den Service verwenden können. 

</br>

**Node.js**

Ersetzen Sie in der Node.js-App `passport.use(new WebAppStrategy());` durch den folgenden Code.

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
  <caption> Tabelle. Beschreibung von Befehlskomponenten für Node.js-Apps</caption>
    <tr>
      <th> Komponenten </th>
      <th> Beschreibung </th>
    </tr>
    <tr>
      <td><code>tenant-id</code> </br> <code> clientID </code> </br> <code> secret </code> </br> <code> oauth-server-url </code> </br></td>
      <td> Diese Werte können Sie durch Klicken auf **Berechtigungsnachweise anzeigen** in der Registerkarte **Serviceberechtigungsnachweise** des Service-Dashboards suchen. </td>
    </tr>
    <tr>
      <td><code> app-url </code></td>
      <td>Die URL der Anwendung.</td>
    </tr>
    <tr>
      <td><code> CALLBACK_URL </code></td>
      <td> Die URL für die Seite, die den Benutzern nach ihrer Registrierung angezeigt wird. </td>
    </tr>
  </table>

</br>

**Swift**

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
  <caption>Tabelle. Beschreibung von Befehlskomponenten für Swift-Apps</caption>
    <tr>
      <th> Komponenten </th>
      <th> Beschreibung </th>
    </tr>
    <tr>
      <td><code>tenant-id</code> </br> <code> clientID </code> </br> <code> secret </code> </br> <code> oauth-server-url </code> </br></td>
      <td> Diese Werte können Sie durch Klicken auf **Berechtigungsnachweise anzeigen** in der Registerkarte **Serviceberechtigungsnachweise** des Service-Dashboards suchen. </td>
    </tr>
    <tr>
      <td><code> app-url </code></td>
      <td>Die URL der Anwendung.</td>
    </tr>
    <tr>
      <td><code> CALLBACK_URL </code></td>
      <td> Die URL für die Seite, die den Benutzern nach ihrer Registrierung angezeigt wird. </td>
    </tr>
  </table>


</br>

**Liberty for Java**

Führen Sie in den Liberty for Java-Apps die im Abschnitt [Liberty for Java-SDK einrichten](#lfj-setup) beschriebenen Schritten aus, ersetzen Sie dabei jedoch die OIDC-Clientelementvariablen durch den folgenden Code. 

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
  <caption>Tabelle. OIDC-Elementvariablen für Liberty for Java-Apps</caption>
    <tr>
      <th> Komponente </th>
      <th> Beschreibung </th>
    </tr>
    <tr>
    <td><code> clientID </code> </br> <code> secret </code> </br> <code> oauth-server-url </code> </br></td>
    <td>Diese Werte können Sie durch Klicken auf **Berechtigungsnachweise anzeigen** in der Registerkarte **Serviceberechtigungsnachweise** des Service-Dashboards suchen.</td>
    </tr>
    <tr>
      <td><code> authorizationEndpointURL </code></td>
      <td> Fügen Sie `/authorization` am Ende von 'oauthServerURL' hinzu.</td>
    </tr>
    <tr>
      <td><code> tokenEndpointUrl </code></td>
      <td>Fügen Sie `/token` am Ende von 'oauthServerURL' hinzu.</td>
    </tr>
    <tr>
      <td><code> jwkEndpointUrl </code></td>
      <td>Fügen Sie `/publickeys` am Ende von 'oauthServerURL' hinzu.</td>
    </tr>
    <tr>
      <td><code> issuerIdentifier </code></td>
      <td>Variiert abhängig von der jeweiligen Region. Folgendes ist möglich: </br><ul><li>issuerIdentifier="appid-oauth.ng.bluemix.net" </br><li> issuerIdentifier="appid-oauth.eu-gb.bluemix.net" </br><li>issuerIdentifier="appid-oauth.au-syd.bluemix.net"</ul></td>
    </tr>
    <tr>
      <td><code> tokenEndpointAuthMethod </code></td>
      <td>Als "basic" angegeben.</td>
    </tr>
    <tr>
      <td><code> signatureAlgorithm </code></td>
      <td>Als "RS256" angegeben.</td>
    </tr>
    <tr>
      <td><code> authFilterid </code></td>
      <td>Liste der zu schützenden Ressourcen.</td>
    </tr>
    <tr>
      <td><code> trustAliasName </code></td>
      <td>Name des Zertifikats im Truststore.</td>
    </tr>
  </table>
