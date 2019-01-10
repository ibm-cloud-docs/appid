---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:pre: .pre}
{:tip: .tip}
{:screen: .screen}

# Applicazioni mobili
{: #adding-mobile}

Con {{site.data.keyword.appid_full}}, puoi velocemente costruire un livello di autenticazione per la tua applicazione mobile nativa o ibrida.
{: shortdesc}

## Descrizione del flusso
{: #understanding}

**Quando questo flusso sarebbe utile?**

Un flusso mobile è utile quando stai sviluppando un'applicazione che deve essere installata sul dispositivo di un utente (un'applicazione nativa). Utilizzando questo flusso, puoi autenticare in modo sicuro gli utenti sulla tua applicazione per poter fornire delle esperienze utente personalizzate tra i dispositivi.

**Quali sono le basi tecniche del flusso?**

Poiché le applicazioni native sono installate direttamente sul dispositivo di un utente, le informazioni sull'utente private e le credenziali dell'applicazione possono essere estratte da terze parti con relativa facilità. Per impostazione predefinita, questi tipi di applicazioni sono noti come client non attendibili perché non possono archiviare le credenziali globali o i token di aggiornamento dell'utente. Di conseguenza, i client non attendibili richiedono agli utenti di immettere le proprie credenziali ogni volta che scadono i loro token di accesso.

Per convertire la tua applicazione in un client attendibile, {{site.data.keyword.appid_short}} utilizza la [Registrazione client dinamica](https://tools.ietf.org/html/rfc7591). Prima che un'istanza dell'applicazione inizi ad autenticare gli utenti, deve essere registrata come un client OAuth2 con {{site.data.keyword.appid_short}}. Come conseguenza alla registrazione del client, la tua applicazione riceve un ID client specifico per l'installazione che può essere firmato digitalmente e utilizzato per autorizzare le richieste con {{site.data.keyword.appid_short}}. Poiché {{site.data.keyword.appid_short}} archivia la chiave pubblica corrispondente della tua applicazione, può convalidare la tua firma della richiesta che consente alla tua applicazione di essere visualizzata come un client riservato. Questo processo riduce il rischio che la tua applicazione esponga le credenziali indefinitamente e migliora notevolmente l'esperienza utente consentendo l'aggiornamento del token automatico.

Dopo la registrazione, i tuoi utenti eseguono l'autenticazione utilizzando i flussi `authorization code` o `resource owner password` [authorization grant](https://tools.ietf.org/html/rfc6749#section-1.3) OAuth2 per autenticare gli utenti.

**A cosa assomiglia questo flusso?**

![{{site.data.keyword.appid_short_notm}} - Flusso da applicazione a applicazione](images/mobile-flow.png)

**Registrazione client dinamica**

1. Un utente esegue un'azione che attiva una richiesta dall'applicazione client all'SDK {{site.data.keyword.appid_short}}.
2. Se la tua applicazione non è registrata ancora come un client mobile, l'SDK avvia un flusso di registrazione dinamica.
3. Dopo una corretta registrazione, {{site.data.keyword.appid_short}} restituisce il tuo ID client specifico per l'installazione.

**Flusso di autorizzazione**

1. L'SDK {{site.data.keyword.appid_short}} avvia il processo di autorizzazione utilizzando l'endpoint {{site.data.keyword.appid_short_notm}} `/authorization`.
2. Il widget di accesso viene visualizzato all'utente.
3. L'utente si autentica utilizzando uno dei provider di identità configurati.
4. {{site.data.keyword.appid_short}} restituisce una concessione di autorizzazione.
5. La concessione di autorizzazione viene scambiata con i token di accesso, identità e aggiornamento dall'endpoint {{site.data.keyword.appid_short_notm}} `/token`.


## Configurazione della tua applicazione mobile con gli SDK {{site.data.keyword.appid_short}} 
{: #configuring}

Inizia ad utilizzare {{site.data.keyword.appid_short}} con i nostri SDK.
{: shortdesc}

**Prima di cominciare**

Hai bisogno delle seguenti informazioni:

* Un'istanza {{site.data.keyword.appid_short_notm}} 

* L'ID tenant della tua istanza. Può essere trovato nella scheda **Service Credentials** del tuo dashboard del servizio.

* La regione {{site.data.keyword.Bluemix}} di distribuzione della tua istanza. Puoi trovare la tua regione cercando nella console. 

  <table><caption> Tabella 1. Regioni {{site.data.keyword.Bluemix_notm}} e valori SDK corrispondenti</caption>
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

## Autenticazione con l'SDK Android
{: #android-setup}

**Prima di cominciare**

Devi avere i seguenti prerequisiti prima di iniziare:

  * API 27 o superiore
  * Java 8.x
  * Strumenti SDK Android 26.1.1+ 
  * Strumenti piattaforma SDK Android 27.0.1+ 
  * Strumenti di build Android versione 27.0.0+

</br>

**Installazione dell'SDK**

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

3. Trova il file `build.gradle` della tua applicazione. **Nota**: assicurati di aprire il file per la tua applicazione, non il file `build.gradle` del progetto.

  1. Aggiungi l'SDK client {{site.data.keyword.appid_short_notm}} alla sezione delle dipendenze.

    ```gradle
    dependencies {
       compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:4.+'
   }
    ```
    {: codeblock}

  2. Nella sezione `defaultConfig`, configura lo schema di reindirizzamento.

    ```gradle
    defaultConfig {
      ...
      manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
    ```
    {: codeblock}

6. Sincronizza il tuo progetto con Gradle. Fai clic su **Tools > Android > Sync Project with Gradle Files**.

</br>

**Inizializzazione dell'SDK**


1. Passa i parametri contesto, ID tenant e regione al metodo di inizializzazione per configurare l'SDK.

    Un punto comune, seppure non obbligatorio, dove inserire il codice di inizializzazione è nel metodo onCreate dell'attività principale nella tua applicazione Android.
    {: tip}

    ```java
    AppID.getInstance().initialize(getApplicationContext(), <tenantId>, <region>);
    ```
    {: codeblock}

</br>
</br>

## Autenticazione con l'SDK iOS Swift
{: #ios-setup}

Proteggi le tue applicazioni mobili utilizzando l'SDK client {{site.data.keyword.appid_short}}.
{:shortdesc}

</br>
**Prima di cominciare**

Devi avere i seguenti prerequisiti prima di iniziare:

  * Xcode 9.0 o superiore
  * CocoaPods 1.1.0 o superiore
  * iOS 10.0 o superiore

</br>

**Installazione dell'SDK**

L'SDK client {{site.data.keyword.appid_short_notm}} è distribuito con CocoaPods, un gestore dipendenze per i progetti Swift e Objective-C Cocoa. CocoaPods scarica le risorse utente e le rende disponibili al tuo progetto.

1. Crea un progetto Xcode oppure aprine uno esistente.

2. Crea un nuovo `Podfile` o aprine uno esistente nella directory del progetto.

3. Aggiungi il pod `IBMCloudAppID` e il comando `use_frameworks!` alle dipendenze della tua destinazione.

  ```swift
  target '<yourTarget>' do
     use_frameworks!
     pod 'IBMCloudAppID'
  end
  ```
  {: codeblock}

4. Installa le tue dipendenze dalla riga di comando all'interno della tua directory del progetto.

  ```swift
  $ pod install --repo-update
  ```
  {: codeblock}

5. Dopo l'installazione, apri il file `<your app>.xcworkspace` che contiene il tuo progetto Xcode e le tue dipendenze collegate.

6. Abilita la condivisione keychain nel progetto Xcode. Passa a **Project Settings > Capabilities > Keychain Sharing** e seleziona **Enable keychain sharing**.

7. Apri **Project Settings > Info > URL Types** e aggiungi un **URL Type**. Inserisci il seguente valore in entrambe le caselle di testo **Identifier** e **URL Scheme**.

  ```
  $(PRODUCT_BUNDLE_IDENTIFIER)
  ```
  {: codeblock}

</br>

**Inizializzazione dell'SDK**

1. Inizializza l'SDK client passando i parametri ID tenant e regione al metodo di inizializzazione.

  ```swift
    AppID.sharedInstance.initialize(tenantId: <tenantId>, region: <region>)
  ```
  {: codeblock}

  Un punto comune, seppure non obbligatorio, dove inserire il codice di inizializzazione è nel metodo `application:didFinishLaunchingWithOptions` del file AppDelegate della tua applicazione Swift.
  {: tip}

2. Importa l'SDK {{site.data.keyword.appid_short}} nel tuo file `AppDelegate`.

  ```swift
  import IBMCloudAppID
  ```
  {: codeblock}

3. Configura la tua applicazione per elaborare i reindirizzamenti tramite {{site.data.keyword.appid_short}}.

  ```swift
  func application( application: UIApplication, open url: URL, options :[UIApplicationOpenURLOptionsKey : Any]) -> Bool {
      return AppID.sharedInstance.application(application, open: url, options: options)
      }
  ```
  {: codeblock}

</br>
</br>

## Accesso alle API protette
{: #accessing-protected-apis}

Dopo un flusso di accesso corretto, puoi utilizzare i tuoi token di accesso e identità per richiamare le risorse di backend protette che utilizzano l'SDK o una libreria di rete di tua scelta.

</br>

### Accesso alle API protette con l'SDK Swift

1.  Aggiungi le seguenti importazioni al file in cui vuoi richiamare una richiesta della risorsa protetta:

  ```swift
  import BMSCore
  import IBMCloudAppID
  ```
  {: codeblock}

2. Richiama la tua risorsa protetta

   ```swift
  BMSClient.sharedInstance.initialize(region: <region>)
  BMSClient.sharedInstance.authorizationManager = AppIDAuthorizationManager(appid: AppID.sharedInstance)

  let request =  Request(url: "<your protected resource url>")

  request.send { (response: Response?, error: Error?) in

      guard let response = response, error == null else {
          print("An error occurred invoking a protected resources", error?.localizedDescription ?? "No response was received")
          return;
      }
      // use your response object
  })
  ```
  {: codeblock}

</br>

### Accesso alle API protette con l'SDK Android

1. Aggiungi le seguenti importazioni al file in cui vuoi richiamare una richiesta della risorsa protetta:

  ```java
  import com.ibm.mobilefirstplatform.clientsdk.android.core.api.BMSClient;
  import com.ibm.cloud.appid.android.api.AppIDAuthorizationManager;
  ```

2. Richiama la tua risorsa protetta

   ```java
   BMSClient bmsClient = BMSClient.getInstance();
   bmsClient.initialize(getApplicationContext(), <region>);

   AppIDAuthorizationManager appIdAuthMgr = new AppIDAuthorizationManager(AppID.getInstance())
  bmsClient.setAuthorizationManager(appIdAuthMgr);

   Request request = new Request("<your protected resource url>", Request.GET);
  request.send(this, new ResponseListener() {

   @Override
		public void onSuccess (Response response) {
       Log.d("My app", "onSuccess :: " + response.getResponseText());
   }

   @Override
		public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
       if (null != t) {
           Log.d("My app", "onFailure :: " + t.getMessage());
       } else if (null != extendedInfo) {
           Log.d("My app", "onFailure :: " + extendedInfo.toString());
       } else {
           Log.d("My app", "onFailure :: " + response.getResponseText());
           }
       }
   });
  ```
  {: codeblock}

</br>

### Accesso alle API protette senza un SDK

Con la libreria di tua scelta, imposta l'intestazione della richiesta `Authorization` in modo da utilizzare lo schema di autenticazione `Bearer` per trasmettere il token di accesso.

Formato della richiesta di esempio:

  ```
  GET /resource HTTP/1.1
  Host: server.example.com
  Authorization: Bearer <access token> <optional identity token>
  ```
  {: screen}

</br>
</br>

## Passi successivi
{: #next}

Con {{site.data.keyword.appid_short}} installato nella tua applicazione, sei quasi pronto ad iniziare ad autenticare gli utenti. Prova ad eseguire una delle seguenti attività:

* Configura i tuoi [provider di identità](/docs/services/appid/identity-providers.html)
* Personalizza e configura [il widget di accesso](/docs/services/appid/login-widget.html)
* Informazioni sull'<a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">SDK Android<img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>
* Informazioni sull'<a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">SDK iOS<img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>
