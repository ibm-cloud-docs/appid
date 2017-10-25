---

copyright:
  years: 2017
lastupdated: "2017-06-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# Aggiunta di {{site.data.keyword.appid_short_notm}} a un'applicazione esistente

Puoi utilizzare {{site.data.keyword.appid_full}} con la tua applicazione esistente per autenticare e archiviare le informazioni sul profilo per i tuoi utenti.


## Prerequisiti

* Un'applicazione iOS Swift, Android, Node.js o Swift esistente
* Un'istanza esistente di {{site.data.keyword.appid_short_notm}}.


## Aggiunta di {{site.data.keyword.appid_short_notm}} a un'applicazione Android esistente

Puoi aggiungere il servizio ID applicazione alle tue applicazioni Android esistenti.

1. Aggiungi il repository JitPack al tuo file build.gradle root.

  ```gradle
  allprojects {
      		repositories {
         	 ...
         	 maven { url 'https://jitpack.io' }
	    }
  }
  ```
  {: pre}

2. Apri il file build.gradle per la tua applicazione, trova la sezione delle dipendenze del file e aggiungi una dipendenza di compilazione all'SDK client {{site.data.keyword.appid_short_notm}}.

  ```gradle
  dependencies {
      compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:1.+'
   }
  ```
  {: pre}

3. Trova la sezione defaultConfig e aggiungi la seguente riga di codice. 

  ```gradle
  defaultConfig {
                         ...
            manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
  ```
  {: pre}

4. Sincronizza il tuo progetto con Gradle.
5. Inizializza l'SDK client passando i parametri contesto, ID tenant e regione al metodo di inizializzazione. Un punto comune, seppure non obbligatorio, dove inserire il codice di inizializzazione è nel metodo onCreate dell'attività principale nella tua applicazione Android.

  ```Java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, <AppID.REGION>);
  ```
  {: pre}

  <table>
  <caption> Tabella 1. Componenti del comando spiegati </caption>
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
      <td> Puoi trovare la tua regione nella IU. Le opzioni sono `AppID.REGION_US_SOUTH`, `AppID.REGION_UK` o `AppID.REGION_Sydney`. </td>
    </tr>
  </table>

6. Dopo che l'SDK client {{site.data.keyword.appid_short_notm}} è stato inizializzato, puoi autenticare i tuoi utenti eseguendo il widget di accesso.

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
  <caption> Tabella 2. Componenti del comando spiegati </caption>
    <tr>
      <th> Componenti </th>
      <th> Descrizione </th>
    </tr>
    <tr>
      <td> <i> onAuthorizationFailure </i> </td>
      <td> Si è verificata un'eccezione. </td>
    </tr>
    <tr>
      <td> <i> onAuthorizationCanceled </i> </td>
      <td> Il processo di autenticazione è stata annullato dall'utente. </td>
    </tr>
    <tr>
      <td> <i> onAuthorizationSuccess </i> </td>
      <td> L'utente è stato autenticato. </td>
    </tr>
  </table>

## Aggiunta di {{site.data.keyword.appid_short_notm}} a un'applicazione iOS Swift esistente

1. Apri il podfile nella directory del progetto. 
2. Nella tua destinazione del progetto, aggiungi una dipendenza per il pod 'BluemixAppID'. Assicurati che anche il comando `use_frameworks!` sia nella tua destinazione. 
3. Per scaricare la dipendenza `BluemixAppID`, esegui il seguente comando.

  ```
  pod install --repo-update
  ```
  {: pre}

4. Apri il tuo progetto Xcode e abilita Keychain Sharing. In **Project Settings**, fai clic su **Capabilities** > **Keychain Sharing**.
5. In **Project Settings** > **Info** > **URL Types** aggiungi un **URL Type**. Riempi le caselle di testo **Identifier** e **URL Scheme** con il seguente valore. 

  ```
  $(PRODUCT_BUNDLE_IDENTIFIER)
  ```
  {: pre}

6. Aggiungi la seguente importazione al tuo file AppDelegate.swift.

  ```swift
  import BluemixAppID
  import BMSCore
  ```
  {: pre}

7. Inizializza l'SDK client passando i parametri ID tenant e regione al metodo di inizializzazione. Un punto comune, seppure non obbligatorio, dove inserire il codice di inizializzazione è nel metodo application:didFinishLaunchingWithOptions: di AppDelegate nella tua applicazione. 

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, bluemixRegion: <AppID.Region>)
  ```
  {: pre}

  <table>
  <caption> Tabella 3. Componenti del comando spiegati </caption>
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
      <td> Puoi trovare la tua regione nella IU. Le opzioni sono `AppID.REGION_US_SOUTH`, `AppID.REGION_UK` o `AppID.REGION_Sydney`. </td>
    </tr>
  </table>

8. Aggiungi il seguente codice al tuo file AppDelegate.

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
  <caption> Tabella 4. Componenti del comando spiegati </caption>
    <tr>
      <th> Componenti </th>
      <th> Descrizione </th>
    </tr>
    <tr>
      <td> <i> onAuthorizationSuccess </i> </td>
      <td> L'utente è stato autenticato. </td>
    </tr>
    <tr>
      <td> <i> onAuthorizationCanceled </i> </td>
      <td> Il processo di autenticazione è stata annullato dall'utente. </td>
    </tr>
    <tr>
      <td> <i> onAuthorizationFailure </i> </td>
      <td> Si è verificata un'eccezione. </td>
    </tr>
  </table>

## Aggiunta di {{site.data.keyword.appid_short_notm}} a un'applicazione web Node.js esistente 

1. Aggiungi il modulo `bluemix-appid` alla tua applicazione Node.js.

  ```javaScript
  npm install --save bluemix-appid
  ```
  {: pre}

2. Installa i seguenti moduli se non sono già stati installati.

  ```javaScript
  npm install --save express
  npm install --save passport
  npm install --save express-session
  ```
  {: pre}

3. Aggiungi il seguente codice al tuo file app.js per:
    * Configurare la tua applicazione Express per utilizzare il middleware della sessione Express. **Nota**: devi configurare il middleware con l'archivio della sessione appropriato per gli ambienti di produzione. Per ulteriori informazioni consulta la [documentazione expressjs](https://github.com/expressjs/session).
    * Configurare passportjs con la serializzazione e la deserializzazione. Questo è obbligatorio per la persistenza della sessione autenticata attraverso le richieste HTTP. Per ulteriori informazioni, consulta la [documentazione passportjs](http://passportjs.org/docs). 
    * Richiamare i token di accesso e identità dal servizio ID applicazione eseguendo un comando get per il callback dell'URL.

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

    **Nota**: il servizio reindirizza nel seguente ordine:
    1. L'URL originale della richiesta che ha attivato il processo di autenticazione, come persistente nella sessione HTTP nella chiave `WebAppStrategy.ORIGINAL_URL`.
    2. Un reindirizzamento con esito positivo, come specificato in `passport.authenticate(name, {successRedirect: "...."}).`
    3. La root dell'applicazione ("/")

4. Ridistribuire l'applicazione.


## Aggiunta di {{site.data.keyword.appid_short_notm}} a un'applicazione web Swift esistente 

1. Apri il file `Package.swift` nella directory della tua applicazione Swift e aggiungi la dipendenza `appid-serversdk-swift`.
  Ad esempio:

    ```swift
    import PackageDescription

    let package = Package(
      dependencies: [
           	.Package(url: "https://github.com/ibm-cloud-security/appid-serversdk-swift.git", majorVersion: 1)
      ]
    )
    ```
    {: pre}

2. Aggiungi il seguente codice alla tua applicazione Swift per:
    * Configurare Kitura per utilizzare il middleware della sessione. **Nota**: devi configurare Kitura con l'archivio della sessione appropriato per gli ambienti di produzione. Per ulteriori informazioni consulta la [documentazione Kitura](https://github.com/IBM-Swift/Kitura-Session).
    * Richiamare i token di accesso e identità dal servizio ID applicazione eseguendo un comando get per il callback dell'URL.

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
  <caption> Tabella 6. Componenti del comando spiegati </caption>
    <tr>
      <th> Componenti </th>
      <th> Descrizione </th>
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

5. Ridistribuire l'applicazione.



## Aggiunta di {{site.data.keyword.appid_short_notm}} a un'applicazione esistente non in esecuzione in {{site.data.keyword.Bluemix_notm}}


Se disponi di un'applicazione Node.js o Swift non in esecuzione in Bluemix, puoi configurare WebAppStrategy o WebAppKituraCredentialsPlugin per lavorare in remoto.


Nella tua applicazione Node.js, sostituisci `passport.use(new WebAppStrategy());` con il seguente codice.

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
  {: pre}

<table>
<caption> Tabella 7. Componenti per il comando per le applicazioni Swift e Node.js spiegati </caption>
  <tr>
    <th> Componenti </th>
    <th> Descrizione </th>
  </tr>
  <tr>
    <td> <i> tenantID </i> </br> <i> clientID </i> </br> <i> secret </i> </br> <i> oauth-server-url </i> </br> </td>
    <td> Puoi trovare questi valori facendo clic su **Visualizza credenziali** nella scheda **credenziali del servizio** del tuo dashboard del servizio. </td>
  </tr>
  <tr>
    <td> <i> app-url </i> </td>
    <td> Il tuo URL dell'applicazione. </td>
  </tr>
  <tr>
    <td> <i> CALLBACK_URL </i> </td>
    <td> L'URL che gli utenti della pagina visualizzano dopo il login. </td>
  </tr>
</table>
