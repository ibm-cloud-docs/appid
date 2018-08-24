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

# Aggiunta di {{site.data.keyword.appid_short}} alla tua applicazione
{: #configuring}

Inizia ad utilizzare {{site.data.keyword.appid_short}} configurando il servizio nella tua applicazione.
{: shortdesc}


## Configurazione dell'SDK Android
{: #android-setup}

Crea le tue applicazioni Android con l'SDK client {{site.data.keyword.appid_short}}, inizializza l'SDK, autentica gli utenti ed effettua le richieste alle risorse protette e non protette.
{:shortdesc}


### Prima di cominciare
{: #before-android}

Hai bisogno delle seguenti informazioni:
  * Un'istanza del servizio {{site.data.keyword.appid_short_notm}}.
  * Il tuo ID tenant. Il tuo ID tenant è un identificativo univoco che viene utilizzato per inizializzare la tua applicazione può essere nella scheda **Service Credentials** del tuo dashboard del servizio.
  * La tua regione {{site.data.keyword.Bluemix}}. Puoi trovare la tua regione cercando nella IU. Il valore viene utilizzato per inizializzare la tua applicazione.
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

  * Un <a href="https://developers.google.com/web/tools/setup/" target="_blank">progetto Android Studio<img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>, configurato per lavorare con Gradle.

### Installazione dell'SDK
{: #install-android}

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

3. Trova la sezione delle dipendenze del file `build.gradle` per la tua applicazione e aggiungi una dipendenza di compilazione per l'SDK client {{site.data.keyword.appid_short_notm}}.**Nota**: assicurati di aprire il file per la tua applicazione, non il file `build.gradle` del progetto.

  ```gradle
   dependencies {
       compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:4.+'
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

### Inizializzazione dell'SDK
{: #initialize-android}

Inizializza l'SDK client passando i parametri contesto, ID tenant e regione al metodo di inizializzazione. Un punto comune, seppure non obbligatorio, dove inserire il codice di inizializzazione è nel metodo onCreate dell'attività principale nella tua applicazione Android.

  ```java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, AppID.REGION_UK);
  ```
  {: codeblock}

  <table>
  <caption> Tabella. Componenti del comando spiegati </caption>
    <tr>
      <th> Componenti </th>
      <th> Descrizione </th>
    </tr>
    <tr>
      <td> <i> tenantID </i> </td>
      <td> Puoi trovare questo valore facendo clic su **Visualizza credenziali** nella scheda **credenziali del servizio** del tuo dashboard del servizio. </td>
    </tr>
    <tr>
      <td> <i> AppID.REGION </i> </td>
      <td> Puoi trovare la tua regione nella IU. Le opzioni sono `AppID.REGION_US_SOUTH`, `AppID.REGION_UK`, `AppID.REGION_Sydney` o `AppID.REGION_Germany`. </td>
    </tr>
  </table>

Ora sei pronto a configurare i tuoi provider di identità e a iniziare a autenticare gli utenti. Per ulteriori informazioni, visita il <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">{{site.data.keyword.appid_short_notm}} Android GitHub repository <img src="../../icons/launch-glyph.svg" alt="icona link esterno"></a>.


</br>

## Configurazione dell'SDK iOS Swift
{: #ios-setup}

Crea le tue applicazioni Swift con l'SDK client {{site.data.keyword.appid_short}}, inizializza l'SDK, autentica gli utenti ed effettua le richieste alle risorse protette e non protette.
{:shortdesc}


### Prima di cominciare
{: #before-ios}

Hai bisogno delle seguenti informazioni:
  * Un'istanza di {{site.data.keyword.appid_short_notm}}.
  * Il tuo ID tenant. Il tuo ID tenant è un identificativo univoco che viene utilizzato per inizializzare la tua applicazione può essere nella scheda **Service Credentials** del tuo dashboard del servizio.
  * La tua regione {{site.data.keyword.Bluemix_notm}}.
  Puoi trovare la tua regione cercando nella IU. Il valore viene utilizzato per inizializzare la tua applicazione.
  <table> <caption> Tabella. Regioni {{site.data.keyword.Bluemix_notm}} e valori SDK corrispondenti</caption>
    <tr>
      <th>Regione {{site.data.keyword.Bluemix}}</th>
      <th>Valore SDK</th>
    </tr>
    <tr>
      <td>Stati Uniti Sud</td>
      <td><code>AppID.REGION_US_SOUTH </code></td>
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


### Installazione dell'SDK
{: #install-ios}

L'SDK client {{site.data.keyword.appid_short_notm}} è distribuito con CocoaPods, un gestore dipendenze per i progetti Swift e Objective-C Cocoa. CocoaPods scarica le risorse utente e le rende disponibili al tuo progetto.

1. Crea un progetto Xcode oppure apri un progetto esistente.
2. Apri o crea il podfile nella directory del progetto.
3. Dopo la destinazione del tuo progetto, aggiungi una dipendenza per il pod 'IBMCloudAppID' e il comando `use_frameworks!`.

  ```swift
  target '<yourTarget>' do
     use_frameworks!
     pod 'IBMCloudAppID'
  end
  ```
  {: codeblock}

4. Scarica la dipendenza 'IBMCloudAppID'.

  ```swift
  pod install --repo-update
  ```
  {: codeblock}

6. Abilita la condivisione keychain nel progetto Xcode. Passa a **Project Settings > Capabilities > Keychain Sharing** e seleziona **Enable keychain sharing**.
7. Apri **Project Settings > Info > URL Types** e aggiungi un **URL Type**. Inserisci il seguente valore in entrambe le caselle di testo **Identifier** e **URL Scheme**.
  ```
  $(PRODUCT_BUNDLE_IDENTIFIER)
  ```
  {: codeblock}


### Inizializzazione dell'SDK
{: #initialize-ios}

1. Inizializza l'SDK client passando i parametri ID tenant e regione al metodo di inizializzazione. Un punto comune, seppure non obbligatorio, dove inserire il codice di inizializzazione è nel metodo `application:didFinishLaunchingWithOptions` di AppDelegate nella tua applicazione Swift.

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, region: AppID.Region_UK)
  ```
  {: codeblock}

  <table>
  <caption> Tabella. Componenti del comando spiegati </caption>
    <tr>
      <th> Componenti </th>
      <th> Descrizione </th>
    </tr>
    <tr>
      <td> <i> tenantID </i> </td>
      <td> Puoi trovare questo valore facendo clic su **Visualizza credenziali** nella scheda **credenziali del servizio** del tuo dashboard del servizio. </td>
    </tr>
    <tr>
      <td> <i> AppID.REGION </i> </td>
      <td> Puoi trovare la tua regione nella IU. Le opzioni sono `AppID.REGION_US_SOUTH`, `AppID.REGION_UK`, `AppID.REGION_Sydney` o `AppID.REGION_Germany`. </td>
    </tr>
  </table>

2. Aggiungi la seguente importazione al tuo file `AppDelegate`.

    ```swift
    import IBMCloudAppID
    ```
    {: codeblock}

3. Aggiungi il seguente codice al tuo file AppDelegate.

  ```swift
  func application( application: UIApplication, open url: URL, options :[UIApplicationOpenURLOptionsKey : Any]) -> Bool {
          return AppID.sharedInstance.application(application, open: url, options: options)
      }
  ```
  {: codeblock}

Ora sei pronto a configurare i tuoi provider di identità e a iniziare a autenticare gli utenti. Per ulteriori informazioni sull'SDK iOS, visita il <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">{{site.data.keyword.appid_short_notm}} iOS GitHub repository <img src="../../icons/launch-glyph.svg" alt="icona link esterno"></a>.

</br>

## Configurazione dell'SDK Node.js
{: #nodejs-setup}

### Prima di cominciare
{: #before-nodejs}

Assicurati di aver installato i seguenti prerequisiti pronti per l'utilizzo: 
1. Installa la [CLI IBM Cloud](../cli/index.html).
2. Implementa il tuo server Node.js con <a href="http://expressjs.com/" target="_blank">Express framework <img src="../icons/launch-glyph.svg" alt="Icona link esterno"></a>. Per installare Express framework, utilizza la riga di comando per aprire la directory con la tua applicazione Node.js ed esegui il seguente comando:
  ```
  npm install --save express
  ```
  {: codeblock}
3. Installa Passport. Utilizza la riga di comando per aprire la directory con la tua applicazione Node.js ed esegui il seguente comando: 
  ```
  npm install --save passport
  ```
  {: codeblock}

**Nota**: altri framework utilizzano i framework `Express`, come ad esempio LoopBack. Puoi utilizzare l'SDK server {{site.data.keyword.appid_short_notm}} con uno qualsiasi di questi framework.


### Installazione dell'SDK
{: #install-nodejs}

1. Utilizzando la riga di comando, apri la directory con la tua applicazione Node.js.
2. Installa il servizio {{site.data.keyword.appid_short_notm}}.
  ```
  npm install --save ibmcloud-appid
  ```
  {: codeblock}

### Inizializzazione dell'SDK
{: #initialize}

1. Aggiungi le seguenti definizioni `require` al tuo file `server.js`.
    ```
    const express = require('express');
    const session = require('express-session')
    const passport = require('passport');
    const WebAppStrategy = require("ibmcloud-appid").WebAppStrategy;
    const CALLBACK_URL = "/ibm/cloud/appid/callback";
    ```
    {: codeblock}

2. Configurare la tua applicazione Express per utilizzare il middleware della sessione Express. **Nota**: devi configurare il middleware con l'archivio della sessione appropriato per gli ambienti di produzione. Per ulteriori informazioni consulta <a href="https://github.com/expressjs/session" target="_blank">expressjs docs <img src="../icons/launch-glyph.svg" alt="Icona link esterno"></a>.
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

3. Passa le credenziali e l'ID tenant all'SDK.
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

 <table summary="Componenti comando: applicazioni Node.js">
  <caption>Componenti del comando per le applicazioni Node.js</caption>
    <tr>
      <th>Componenti</th>
      <th>Descrizione</th>
    </tr>
    <tr>
      <td><i> tenantID </i></td>
      <td>L'ID tenant è un identificativo univoco che viene utilizzato per inizializzare la tua applicazione. Puoi trovare il valore nel dashboard del servizio {{site.data.keyword.appid_short_notm}} facendo clic su **View Credentials** nella scheda **Service Credentials**.</td>
    </tr>
    <tr>
      <td><i> clientID </i> </br> <i> secret </i> </br> <i> oauth-server-url </i> </br> </td>
      <td>Puoi trovare questi valori facendo clic su **View Credentials** nella scheda **Service Credentials** del tuo dashboard del servizio.</td>
    </tr>
    <tr><td><i>redirectUri</i></td>
    <td>Il valore redirectUri può essere fornito in tre modi:</br>
        1. Manualmente nel nuovo WebAppStrategy({redirectUri: "...."})</br>
        2. Come variabile di ambiente denominata `redirectUri`</br>
        3. Se non è stato fornito alcuno dei suddetti dati, l'SDK ID applicazione proverà a richiamare l'application_uri dell'applicazione in esecuzione su IBM Cloud e accoda un suffisso predefinito "/ibm/cloud/appid/callback"</td>
    </tr>
    <tr>
      <td><i> CALLBACK_URL </i></td>
      <td>L'URL che gli utenti della pagina visualizzano dopo il log. </td>
    </tr>
  </table>

4. Configura passport con la serializzazione e la deserializzazione. Questo passo di configurazione è obbligatorio per la persistenza della sessione autenticata attraverso le richieste HTTP. Per ulteriori informazioni, visita il <a href="http://passportjs.org/docs" target="_blank">passport docs <img src="../icons/launch-glyph.svg" alt="icona link esterno"></a>.

  ```
  passport.serializeUser(function(user, cb) {
    cb(null, user);
    });

  passport.deserializeUser(function(obj, cb) {
    cb(null, obj);
    });
  ```
  {: codeblock}

5. Aggiungi il seguente codice al tuo file `server.js` per emettere i reindirizzamenti del servizio:
   ```
   app.get(CALLBACK_URL, passport.authenticate(WebAppStrategy.STRATEGY_NAME));
   app.get('/protected', passport.authenticate(WebAppStrategy.STRATEGY_NAME)), function(req, res)
        res.json(req.user);
   });
   ```
   {: codeblock}

   **Nota**: il servizio reindirizza nel seguente ordine:
    1. L'URL originale della richiesta che ha attivato il processo di autenticazione, come persistente nella sessione HTTP nella chiave `WebAppStrategy.ORIGINAL_URL`.
    2. Un reindirizzamento con esito positivo, come specificato in `passport.authenticate(name, {successRedirect: "...."}).`
    3. La root dell'applicazione ("/")

6. Ridistribuire l'applicazione.

Per ulteriori informazioni, visita il <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">{{site.data.keyword.appid_short_notm}} Node.js GitHub repository <img src="../icons/launch-glyph.svg" alt="icona link esterno"></a>.

## Configurazione dell'SDK Swift
{: #swift-setup}

Proteggi i tuoi back-end e le tue API con l'SDK server {{site.data.keyword.appid_short}}.
{:shortdesc}


### Prima di cominciare
{: #before-swift}

Prima di lavorare con l'SDK Swift, devi disporre dei seguenti prerequisiti:

* MacOS o Linux
* OpenSSL 1.0.2 su Linux
* Installa Swift 3.0.2
* Installa Kitura 1.6


### Installazione dell'SDK
{: #install-swift}

1. Apri il file `Package.swift` nella directory della tua applicazione Swift e aggiungi la dipendenza `appid-serversdk-swift`.

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

  Puoi copiare openssl.xcconfig da <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">{{site.data.keyword.appid_short_notm}} Swift GitHub <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>
  {: tip}

4. Aggiungi il seguente codice alla tua applicazione Swift per:
    * Configurare Kitura per utilizzare il middleware della sessione. **Nota**: devi configurare Kitura con l'archivio della sessione appropriato per gli ambienti di produzione. Per ulteriori informazioni consulta <a href="https://github.com/IBM-Swift/Kitura-Session" target="_blank">Kitura docs <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>.
    * Richiamare i token di accesso e identità dal servizio {{site.data.keyword.appid_short_notm}} eseguendo un comando get per il callback dell'URL.

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

5. Ridistribuire l'applicazione.

</br>

## Configurazione dell'SDK Liberty for Java
{: #lfj-setup}

Puoi configurare {{site.data.keyword.appid_short_notm}} per utilizzare le tue applicazioni web Liberty for Java.
{:shortdesc}

1. Aggiungi una <a href="https://www.ibm.com/support/knowledgecenter/en/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/twlp_config_oidc_rp.html" target="_blank">OpenID Connect <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> al tuo `server.xml`.

  ```xml
  <feature manager>
  <feature>appSecurity-2.0</feature>
  <feature>openidConnectClient-1.0</feature>  
  ```
  {: codeblock}

2. Nella tua funzione Open ID Connect Client, definisci i seguenti segnaposto. Vengono riempiti automaticamente da {{site.data.keyword.Bluemix_notm}} successivamente. La variabile del nome dell'istanza deve corrispondere esattamente al tuo nome dell'istanza {{site.data.keyword.appid_short_notm}}.

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

  **Nota**: la variabile issuerIdentifier è diversa a seconda della tua regione. Può essere una delle seguenti variabili:
  * issuerIdentifier="appid-oauth.ng.bluemix.net"
  * issuerIdentifier="appid-oauth.eu-gb.bluemix.net"
  * issuerIdentifier="appid-oauth.au-syd.bluemix.net"</ul> </td>

3. Definisci un filtro di autorizzazione per specificare le risorse protette. Se non viene <a href="https://www.ibm.com/support/knowledgecenter/en/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/rwlp_auth_filter.html" target="_blank">definito un filtro <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>, il servizio proteggerà tutte le risorse.
  ```
  <authFilter id="myAuthFilter">
             <requestUrl id="myRequestUrl" urlPattern="/protected" matchType="contains"/>
    </authFilter>
  ```
  {: codeblock}

4. Nel tuo file `server.xml`, definisci il tuo tipo di oggetto speciale come ALL_AUTHENTICATED_USERS.

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

5. Nel tuo elemento `<application-bnd>`, <a href="https://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_authorization.html?cp=SSAW57_8.5.5&cm_mc_uid=18498555367014888859884&cm_mc_sid_50200000=1494855872" target="_blank">definisci i ruoli <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> come trovati nella tua applicazione web: `web.xml`.

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

6. Ottieni un certificato.

    a. Nel tuo dashboard {{site.data.keyword.appid_short_notm}}, fai clic sulle credenziali del servizio.

    b. Fai clic su **View credentials** e copia `oauthServerUrl`.

    c. Aggiungi `/token` all'URL. Utilizza Firefox per aprire l'URL di output e ottenere il certificato. Puoi utilizzare il seguente URL come esempio.

    ```
    https://appid-oauth.ng.bluemix.net/oauth/v3/5d12852e-b0a0-46a3-9547-67a4a33a7164/token
    ```
    {: screen}

    d. Nella barra degli indirizzi di Firefox, fai clic sull'icona di blocco > **right arrow** > **more information** > **view certificate**.

    e. Nella scheda **Security**, fai clic su **View certificate** > **details**.

    f. Esporta il certificato e salvalo nella tua unità locale come un file PEM.

7. Aggiungi il certificato alla tuo file truststore.jks Liberty for Java utilizzando <a href="https://www.ibm.com/support/knowledgecenter/SSYKE2_6.0.0/com.ibm.java.security.component.60.doc/security-component/keytoolDocs/keytool_overview.html" target="_blank">Liberty Keytool <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> e aggiungi un riferimento all'alias del certificato nell'elemento OIDC. Il tuo `.jks file` è ubicato nella tua directory del server: **resources** > **security** > **<i>truststore file name</i>** > **`.jks file`**. Puoi utilizzare una delle seguenti opzioni per aggiungere il tuo certificato al file.

    * Nel terminale, passa alla tua cartella di sicurezza Liberty for Java: wlp > usr > servers > <i>servername</i> > resources > security e utilizza il seguente comando per aggiungere il certificato.

      ```
      keytool -importcert -keystore ./trust.jks -file ~/Documents/secbluemix.cer`
      ```
      {: codeblock}      

      **Nota**: `~/Documents/[certificatename].cer` illustra l'ubicazione del file nella tua unità locale.

    * Puoi utilizzare <a href="http://keystore-explorer.org/index.html" target="_blank">KeyStore Explorer <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> per aggiungere il certificato. Apri KeyStore Explorer e seleziona **Open an existing KeyStore**.

    **Nota**: il certificato potrebbe essere scaduto/modificato, in questo caso è necessario aggiornare il trustore con il nuovo certificato.

8. Nel tuo file `manifest.yml`, definisci la tua istanza {{site.data.keyword.appid_short_notm}}.

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

    Un file `server.xml` di esempio configurato per {{site.data.keyword.appid_short_notm}}:

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

## Aggiunta di {{site.data.keyword.appid_short_notm}} a un'applicazione esistente non in esecuzione in {{site.data.keyword.Bluemix_notm}}
{: #existing}

Puoi aggiungere {{site.data.keyword.appid_short_notm}} alle applicazioni che non vengono eseguite su {{site.data.keyword.Bluemix_notm}}. Puoi vedere alcuni esempi in questo argomento, ma queste non sono le sole lingue con cui puoi utilizzare il servizio.

</br>

**Node.js**

Nella tua applicazione Node.js, sostituisci `passport.use(new WebAppStrategy());` con il seguente codice.

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
  <caption> Tabella. Componenti del comando per le applicazioni Node.js spiegati</caption>
    <tr>
      <th> Componenti </th>
      <th> Descrizione </th>
    </tr>
    <tr>
      <td><code>tenant-id</code> </br> <code> clientID </code> </br> <code> secret </code> </br> <code> oauth-server-url </code> </br></td>
      <td> Puoi trovare questi valori facendo clic su **Visualizza credenziali** nella scheda **credenziali del servizio** del tuo dashboard del servizio. </td>
    </tr>
    <tr>
      <td><code> app-url </code></td>
      <td>Il tuo URL dell'applicazione.</td>
    </tr>
    <tr>
      <td><code> CALLBACK_URL </code></td>
      <td> L'URL che gli utenti della pagina visualizzano dopo il login. </td>
    </tr>
  </table>

</br>

**Swift**

Nella tua applicazione Swift, sostituisci `let webappKituraCredentialsPlugin = WebAppKituraCredentialsPlugin()` con il seguente codice.

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
  <caption>Tabella. Componenti del comando per le applicazioni Swift spiegati</caption>
    <tr>
      <th> Componenti </th>
      <th> Descrizione </th>
    </tr>
    <tr>
      <td><code>tenant-id</code> </br> <code> clientID </code> </br> <code> secret </code> </br> <code> oauth-server-url </code> </br></td>
      <td> Puoi trovare questi valori facendo clic su **Visualizza credenziali** nella scheda **credenziali del servizio** del tuo dashboard del servizio. </td>
    </tr>
    <tr>
      <td><code> app-url </code></td>
      <td>Il tuo URL dell'applicazione.</td>
    </tr>
    <tr>
      <td><code> CALLBACK_URL </code></td>
      <td> L'URL che gli utenti della pagina visualizzano dopo il login. </td>
    </tr>
  </table>


</br>

**Liberty for Java**

Nelle tue applicazioni Liberty for Java, completa la seguente procedura in [Configurazione dell'SDK Liberty for Java](#lfj-setup), ma sostituisci le variabili dell'elemento client OIDC con il seguente codice.

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
  <caption>Tabella. Variabili dell'elemento OIDC per le applicazioni Liberty for Java </caption>
    <tr>
      <th> Componente </th>
      <th> Descrizione </th>
    </tr>
    <tr>
    <td><code> clientID </code> </br> <code> secret </code> </br> <code> oauth-server-url </code> </br></td>
    <td>Puoi trovare questi valori facendo clic su **Visualizza credenziali** nella scheda **credenziali del servizio** del tuo dashboard del servizio.</td>
    </tr>
    <tr>
      <td><code> authorizationEndpointURL </code></td>
      <td> Aggiungi `/authorization` alla file di oauthServerURL.</td>
    </tr>
    <tr>
      <td><code> tokenEndpointUrl </code></td>
      <td>Aggiungi `/token` alla file di oauthServerURL.</td>
    </tr>
    <tr>
      <td><code> jwkEndpointUrl </code></td>
      <td>Aggiungi `/publickeys` alla file di oauthServerURL.</td>
    </tr>
    <tr>
      <td><code> issuerIdentifier </code></td>
      <td>Diversa a seconda della regione. Può essere uno dei seguenti valori: </br><ul><li>issuerIdentifier="appid-oauth.ng.bluemix.net" </br><li> issuerIdentifier="appid-oauth.eu-gb.bluemix.net" </br><li>issuerIdentifier="appid-oauth.au-syd.bluemix.net"</ul></td>
    </tr>
    <tr>
      <td><code> tokenEndpointAuthMethod </code></td>
      <td>Specificata come "basic".</td>
    </tr>
    <tr>
      <td><code> signatureAlgorithm </code></td>
      <td>Specificata come "RS256".</td>
    </tr>
    <tr>
      <td><code> authFilterid </code></td>
      <td>L'elenco delle risorse da proteggere.</td>
    </tr>
    <tr>
      <td><code> trustAliasName </code></td>
      <td>Il nome del tuo certificato nel tuo truststore.</td>
    </tr>
  </table>
