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

# Configurazione delle SDK
{: #configuring}


## Configurazione dell'SDK Android
{: #android-setup}

Crea le tue applicazioni Android con l'SDK client {{site.data.keyword.appid_short}}, inizializza l'SDK, autentica gli utenti ed effettua le richieste alle risorse protette e non protette.
{:shortdesc}


### Prima di cominciare

Hai bisogno delle seguenti informazioni:
  * Un'istanza del servizio {{site.data.keyword.appid_short_notm}}.
  * Il tuo ID tenant. Nella scheda **Credenziali del servizio** del tuo dashboard del servizio, fai clic su **Visualizza credenziali**. Il tuo ID tenant è un identificativo univoco che viene utilizzato per inizializzare la tua applicazione.
  * La tua regione {{site.data.keyword.Bluemix}}. Puoi trovare la tua regione cercando nella IU. Il valore viene utilizzato per inizializzare la tua applicazione.
    <table> <caption> Tabella 1. Regioni {{site.data.keyword.Bluemix_notm}} e valori SDK corrispondenti </caption>
    <tr>
      <th>Regione {{site.data.keyword.Bluemix}}</th>
      <th>Valore SDK</th>
    </tr>
    <tr>
      <td>Stati Uniti Sud</td>
      <td><code>AppID.REGION_US_SOUTH</code> </td>
    </tr>
    <tr>
      <td>Sydney</td>
      <td><code>AppID.REGION_SYDNEY </code></td>
    </tr>
    <tr>
      <td>Regno Unito</td>
      <td><code>AppID.REGION_UK </code></td>
    </tr>
    <tr>
      <td>Germania</td>
      <td><code>AppID.REGION_GERMANY</code></td>
    </tr>
  </table>

  * Un <a href="https://developers.google.com/web/tools/setup/" target="_blank">progetto Android Studio<img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>, configurato per lavorare con Gradle.

### Installazione dell'SDK client

1. Crea un progetto Android Studio oppure apri un progetto esistente.
2. Aggiungi JitPack al tuo file `build.gradle` della root.

  ```gradle
    allprojects {
	    repositories {
		    ...
		    maven { url 'https://jitpack.io' }
	    }
    }
  ```
  {: codeblock}

3. Apri il file `build.gradle` per la tua applicazione.

    **Nota**: assicurati di aprire il file per la tua applicazione, non il file `build.gradle` del progetto.
4. Trova la sezione delle dipendenze del file e aggiungi una dipendenza di compilazione per l'SDK client {{site.data.keyword.appid_short_notm}}.

  ```gradle
   dependencies {
       compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:1.+'
   }
  ```
  {: codeblock}

5. Trova la sezione `defaultConfig` e aggiungi le seguenti righe di codice.

  ```gradle
  defaultConfig {
  ...
  manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
  ```
  {: codeblock}

6. Sincronizza il tuo progetto con Gradle. Fai clic su **Tools > Android > Sync Project with Gradle Files**.

### Inizializzazione dell'SDK client

Inizializza l'SDK client passando i parametri contesto, ID tenant e regione al metodo di inizializzazione. Un punto comune, seppure non obbligatorio, dove inserire il codice di inizializzazione è nel metodo onCreate dell'attività principale nella tua applicazione Android.

  ```java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, AppID.REGION_UK);
  ```
  {: codeblock}

1. Sostituisci *tenantId* con il tuo ID tenant del servizio.
2. Sostituisci *AppID.REGION_UK* con la tua regione {{site.data.keyword.Bluemix_notm}}.

Per ulteriori informazioni, visita il <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">{{site.data.keyword.appid_short_notm}} Android GitHub repository <img src="../../icons/launch-glyph.svg" alt="icona link esterno"></a>.

## Configurazione dell'SDK iOS Swift
{: #ios-setup}

Crea le tue applicazioni Swift con l'SDK client {{site.data.keyword.appid_short}}, inizializza l'SDK, autentica gli utenti ed effettua le richieste alle risorse protette e non protette.
{:shortdesc}


### Prima di cominciare

Hai bisogno delle seguenti informazioni:
  * Un'istanza di {{site.data.keyword.appid_short_notm}}.
  * Il tuo ID tenant. Nella scheda **Credenziali del servizio** del tuo dashboard del servizio, fai clic su **Visualizza credenziali**. Il tuo ID tenant è un identificativo univoco che viene utilizzato per inizializzare la tua applicazione.
  * La tua regione {{site.data.keyword.Bluemix_notm}}.
  Puoi trovare la tua regione cercando nella IU. Il valore viene utilizzato per inizializzare la tua applicazione.
  <table> <caption> Tabella 1. Regioni {{site.data.keyword.Bluemix_notm}} e valori SDK corrispondenti </caption>
    <tr>
      <th>Regione {{site.data.keyword.Bluemix}}</th>
      <th>Valore SDK</th>
    </tr>
    <tr>
      <td>Stati Uniti Sud</td>
      <td><code>AppID.REGION_US_SOUTH</code> </td>
    </tr>
    <tr>
      <td>Sydney</td>
      <td><code>AppID.REGION_SYDNEY </code></td>
    </tr>
    <tr>
      <td>Regno Unito</td>
      <td><code>AppID.REGION_UK </code></td>
    </tr>
    <tr>
      <td>Germania</td>
      <td><code>AppID.REGION_GERMANY</code></td>
    </tr>
  </table>

  * Un progetto Xcode (versione 9.0.1 o superiore).
  * CocoaPods (versione 1.1.0 o superiore).


### Installazione dell'SDK client

L'SDK client {{site.data.keyword.appid_short_notm}} è distribuito con CocoaPods, un gestore dipendenze per i progetti Swift e Objective-C Cocoa. CocoaPods scarica le risorse utente e le rende disponibili al tuo progetto.

1. Crea un progetto Xcode oppure apri un progetto esistente.
2. Apri o crea il podfile nella directory del progetto.
3. Dopo la destinazione del tuo progetto, aggiungi una dipendenza per il pod 'BluemixAppID' e il comando `use_frameworks!`.

  Ad esempio:

  ```swift
  target '<yourTarget>' do
     use_frameworks!
     pod 'BluemixAppID'
  end
  ```
  {: codeblock}

4. Per scaricare la dipendenza `BluemixAppID`, esegui il seguente comando.

  ```swift
  pod install --repo-update
  ```
  {: codeblock}

6. Apri il tuo progetto Xcode e abilita Keychain Sharing. Passa a **Project Settings > Capabilities > Keychain Sharing** e seleziona **Enable keychain sharing**.
7. Apri **Project Settings > Info > URL Types** e aggiungi un **URL Type**. Inserisci `$(PRODUCT_BUNDLE_IDENTIFIER)` in entrambe le caselle di testo **Identifier** e **URL Scheme**.


### Inizializzazione dell'SDK client

1. Aggiungi la seguente importazione al tuo file `AppDelegate`.

  ```swift
  import BluemixAppID
  ```
  {: codeblock}

2. Inizializza l'SDK client passando i parametri ID tenant e regione al metodo di inizializzazione. Un punto comune, seppure non obbligatorio, dove inserire il codice di inizializzazione è nel metodo `application:didFinishLaunchingWithOptions` di AppDelegate nella tua applicazione Swift.

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, bluemixRegion: AppID.Region_UK)
  ```
  {: codeblock}

  * Sostituisci *tenantId* con l'ID tenant per il tuo servizio.
  * Sostituisci AppID.REGION_UK con la tua regione {{site.data.keyword.appid_short_notm}}.

3. Aggiungi il seguente codice al tuo file AppDelegate.

  ```swift
  func application(_ application: UIApplication, open url: URL, options :[UIApplicationOpenURLOptionsKey : Any]) -> Bool {
          return AppID.sharedInstance.application(application, open: url, options: options)
      }
  ```
  {: codeblock}

Per ulteriori informazioni, visita il <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">{{site.data.keyword.appid_short_notm}} iOS GitHub repository <img src="../../icons/launch-glyph.svg" alt="icona link esterno"></a>.

## Configurazione dell'SDK Node.js
{: #nodejs-setup}

### Prima di cominciare

* Devi avere dimestichezza con lo sviluppo di applicazioni Node.js su {{site.data.keyword.Bluemix_notm}}.
* L'SDK server {{site.data.keyword.appid_short_notm}} richiede che il tuo server Node.js sia implementato con il <a href="http://expressjs.com/" target="_blank">framework Express <img src="../../icons/launch-glyph.svg" alt="icona link esterno"></a>.

**Nota**: altri framework utilizzano i framework `Express`, come ad esempio LoopBack. Puoi utilizzare l'SDK server {{site.data.keyword.appid_short_notm}} con uno qualsiasi di questi framework.


### Installazione dell'SDK server


1. Utilizzando la riga di comando, apri la directory con la tua applicazione Node.js.
2. Emetti i seguenti comandi.

  ```
  npm install -save express
  npm install -save passport
  npm install -save bluemix-appid
  ```
  {: codeblock}

Per ulteriori informazioni, visita il <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">{{site.data.keyword.appid_short_notm}} Node.js GitHub repository <img src="../../icons/launch-glyph.svg" alt="icona link esterno"></a>.

## Configurazione dell'SDK Swift
{: #swift-setup}

Proteggi i tuoi back-end e le tue API con l'SDK server {{site.data.keyword.appid_short}}.
{:shortdesc}


### Prima di cominciare

Prima di lavorare con l'SDK Swift, devi disporre dei seguenti prerequisiti:

* MacOS o Linux
* OpenSSL 1.0.2 su Linux
* Installa Swift 3.0.2
* Installa Kitura 1.6


### Installazione dell'SDK

1. Apri il file `Package.swift` nella directory della tua applicazione Swift e aggiungi la dipendenza `appid-serversdk-swift`. Ad esempio:

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

2. Per MacOS: quando crei sulla riga di comando, tutti i pacchetti devono includere i seguenti indicatori.
  ```
  swift build -Xlinker -L/usr/local/opt/openssl/lib -Xcc -I/usr/local/opt/openssl/include
  ```
  {: pre}

3. Quando crei un progetto xcode utilizza il seguente comando:
  ```
  swift package generate-xcodeproj --xcconfig-overrides openssl.xcconfig
  ```
  {: pre}

  Puoi copiare openssl.xcconfig da <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">{{site.data.keyword.appid_short_notm}} Swift GitHub <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>.
  {: tip}
