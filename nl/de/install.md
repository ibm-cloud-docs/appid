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

# SDKs konfigurieren
{: #configuring}


## Android-SDK einrichten
{: #android-setup}

Erstellen Sie Ihre Android-Apps mit dem {{site.data.keyword.appid_short}}-Client-SDK, initialisieren Sie das SDK, authentifizieren Sie Benutzer und senden Sie Anforderungen an geschützte und nicht geschützte Ressourcen.
{:shortdesc}


### Vorbereitungen

Sie benötigen die folgenden Informationen:
  * Eine Instanz des {{site.data.keyword.appid_short_notm}}-Service.
  * Ihre Tenant-ID. Klicken Sie in der Registerkarte **Serviceberechtigungsnachweise** Ihres Service-Dashboards auf **Berechtigungsnachweise anzeigen**. Ihre Tenant-ID ist eine eindeutige ID zur Initialisierung der App.
  * Ihre {{site.data.keyword.Bluemix}}-Region. Sie finden Ihre Region in Ihrer Benutzerschnittstelle. Der Wert wird für die Initialisierung Ihrer App verwendet.
    <table> <caption> Tabelle 1: {{site.data.keyword.Bluemix_notm}}-Regionen und entsprechende SDK-Werte </caption>
    <tr>
      <th>{{site.data.keyword.Bluemix}}-Region </th>
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

### Client-SDK installieren

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

3. Öffnen Sie die Datei `build.gradle` für Ihre Anwendung.

    **Hinweis**: Stellen Sie sicher, dass Sie die Datei für Ihre App öffnen, nicht die Projektdatei `build.gradle`.
4. Suchen Sie den Abschnitt für Abhängigkeiten ('dependencies') in der Datei und fügen Sie die neue Abhängigkeit 'compile' für das {{site.data.keyword.appid_short_notm}}-Client-SDK hinzu.

  ```gradle
   dependencies {
       compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:1.+'
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

### Client-SDK initialisieren

Initialisieren Sie das SDK, indem Sie die Parameter 'context', 'tenantID' und 'region' an die Methode 'initialize' übergeben. Eine gängige, wenngleich nicht verbindliche, Position für den Initialisierungscode ist die Methode 'onCreate' der Hauptaktivität in Ihrer Android-Anwendung.

  ```java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, AppID.REGION_UK);
  ```
  {: codeblock}

1. Ersetzen Sie *tenantId* durch Ihre Service-Tenant-ID.
2. Ersetzen Sie *AppID.REGION_UK* durch Ihre {{site.data.keyword.Bluemix_notm}}-Region.

Weitere Informationen finden Sie im Abschnitt zum <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">{{site.data.keyword.appid_short_notm}}-Android-GitHub-Repository <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>.

## iOS-Swift-SDK einrichten
{: #ios-setup}

Erstellen Sie Ihre Swift-Anwendungen mit dem {{site.data.keyword.appid_short}}-Client-SDK, initialisieren Sie das SDK, authentifizieren Sie Benutzer und senden Sie Anforderungen an geschützte und nicht geschützte Ressourcen.
{:shortdesc}


### Vorbereitungen

Sie benötigen die folgenden Informationen:
  * Eine Instanz von {{site.data.keyword.appid_short_notm}}.
  * Ihre Tenant-ID. Klicken Sie in der Registerkarte **Serviceberechtigungsnachweise** Ihres Service-Dashboards auf **Berechtigungsnachweise anzeigen**. Ihre Tenant-ID ist eine eindeutige ID zur Initialisierung der App.
  * Ihre {{site.data.keyword.Bluemix_notm}}-Region.
  Sie finden Ihre Region in Ihrer Benutzerschnittstelle. Der Wert wird für die Initialisierung Ihrer App verwendet.
  <table> <caption> Tabelle 1: {{site.data.keyword.Bluemix_notm}}-Regionen und entsprechende SDK-Werte </caption>
    <tr>
      <th>{{site.data.keyword.Bluemix}}-Region </th>
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

  * Ein Xcode-Projekt (Version 9.0.1 oder höher).
  * CocoaPods (Version 1.1.0 oder höher).


### Client-SDK installieren

Das {{site.data.keyword.appid_short_notm}}-Client-SDK wird mit CocoaPods verteilt, einem Abhängigkeitenmanager für Swift- und Objective-C Cocoa-Projekte. CocoaPods lädt Artefakte herunter und stellt sie für Ihr Projekt zur Verfügung.

1. Erstellen Sie ein Xcode-Projekt oder öffnen Sie ein vorhandenes Projekt.
2. Öffnen oder erstellen Sie die Podfile im Projektverzeichnis.
3. Fügen Sie nach dem Ziel Ihres Projekts eine Abhängigkeit für den Pod 'BluemixAppID' und den Befehl `use_frameworks!` hinzu. 

  Beispiel:

  ```swift
  target '<yourTarget>' do
     use_frameworks!
     pod 'BluemixAppID'
  end
  ```
  {: codeblock}

4. Führen Sie den folgenden Befehl aus, um die `BluemixAppID`-Abhängigkeit herunterzuladen.

  ```swift
  pod install --repo-update
  ```
  {: codeblock}

6. Öffnen Sie Ihr Xcode-Projekt und aktivieren Sie das Keychain-Sharing. Navigieren Sie zu **Projekteinstellungen > Funktionen > Keychain-Sharing** und wählen Sie **Keychain-Sharing aktivieren** aus.
7. Öffnen Sie **Projekteinstellungen > Info > URL-Typen** und fügen Sie einen **URL-Typ** hinzu. Stellen Sie `$(PRODUCT_BUNDLE_IDENTIFIER)` in die beiden Textfelder **ID** und **URL-Schema**. 


### Client-SDK initialisieren

1. Fügen Sie folgenden Import zu Ihrer Datei `AppDelegate` hinzu. 

  ```swift
  import BluemixAppID
  ```
  {: codeblock}

2. Initialisieren Sie das SDK, indem Sie die Parameter 'tenantID' und 'region' an die Methode 'initialize' übergeben. Eine gängige, wenngleich nicht verbindliche, Position für den Initialisierungscode ist die Methode `application:didFinishLaunchingWithOptions` von AppDelegate in Ihrer Swift-Anwendung.

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, bluemixRegion: AppID.Region_UK)
  ```
  {: codeblock}

  * Ersetzen Sie *tenantId* durch die Tenant-ID für Ihren Service.
  * Ersetzen Sie AppID.REGION_UK durch Ihre {{site.data.keyword.appid_short_notm}}-Region.

3. Fügen Sie den folgenden Code zur AppDelegate-Datei hinzu.

  ```swift
  func application(_ application: UIApplication, open url: URL, options :[UIApplicationOpenURLOptionsKey : Any]) -> Bool {
          return AppID.sharedInstance.application(application, open: url, options: options)
      }
  ```
  {: codeblock}

Weitere Informationen finden Sie im Abschnitt zum <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">{{site.data.keyword.appid_short_notm}}-iOS-GitHub-Repository <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>.

## Node.js-SDK einrichten
{: #nodejs-setup}

### Vorbereitungen

* Sie sollten mit der Entwicklung von Node.js-Apps in {{site.data.keyword.Bluemix_notm}} vertraut sein.
* Das {{site.data.keyword.appid_short_notm}}-Server-SDK erfordert, dass Ihr Node.js-Server mit dem <a href="http://expressjs.com/" target="_blank">Express-Framework <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> implementiert ist.

**Hinweis**: Von anderen Frameworks werden `Express`-Frameworks verwendet, wie zum Beispiel LoopBack. Sie können das {{site.data.keyword.appid_short_notm}}-Server-SDK mit einem beliebigen dieser Frameworks verwenden.


### Server-SDK installieren


1. Öffnen Sie mithilfe der Befehlszeile das Verzeichnis mit Ihrer Node.js-App.
2. Führen Sie die folgenden Befehle aus.

  ```
  npm install -save express
  npm install -save passport
  npm install -save bluemix-appid
  ```
  {: codeblock}

Weitere Informationen finden Sie im Abschnitt zum <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">{{site.data.keyword.appid_short_notm}}-Node.js GitHub-Repository <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>.

## Swift-SDK einrichten
{: #swift-setup}

Schützen Sie Ihre Back-Ends und APIs mit dem {{site.data.keyword.appid_short}}-Server-SDK.
{:shortdesc}


### Vorbereitungen

Vor der Arbeit mit dem Swift-SDK müssen Sie folgende Voraussetzungen erfüllen: 

* Entweder MacOS oder Linux
* OpenSSL 1.0.2 unter Linux
* Installieren Sie Swift 3.0.2.
* Installieren Sie Kitura 1.6.


### SDK installieren

1. Öffnen Sie die Datei `Package.swift`, die sich im Verzeichnis Ihrer Swift-App befindet, und fügen Sie die Abhängigkeit `appid-serversdk-swift` hinzu. Beispiel:

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

  Sie können die Datei openssl.xcconfig vom <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">{{site.data.keyword.appid_short_notm}} Swift GitHub <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> kopieren.
  {: tip}
