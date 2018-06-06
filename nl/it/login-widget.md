---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-01"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Gestione dell'esperienza di accesso 

Con il widget di accesso, puoi aggiornare il tuo flusso di accesso in qualsiasi momento senza aggiungere, rimuovere o modificare il codice di origine. Puoi essere pronto in pochi minuti utilizzando il codice fornito nelle nostre applicazioni di esempio.
{: shortdesc}

**Nota**: quando configuri i provider di identità sociali come Facebook, viene utilizzato [Oauth2 Authorization Grant flow](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html) per richiamare il widget di accesso.

</br>

## Personalizzazione del codice dell'applicazione di esempio 
{: #login-widget}

Puoi personalizzare la schermata di accesso preconfigurata in modo che visualizzi il logo e i colori di tua scelta. Se vuoi visualizzare la tua propria IU personalizzata, controlla [Cloud Directory](/docs/services/appid/cloud-directory.html).
{: shortdesc}

![Esempio di esperienza di accesso personalizzata](/images/customize.gif)

Per personalizzare la schermata: 

1. Apri il dashboard del servizio {{site.data.keyword.appid_short_notm}}.
2. Seleziona la sezione **Login Customization**, in cui puoi modificare l'aspetto del widget di accesso per allinearlo con il tuo marchio aziendale.
3. Carica il tuo logo aziendale selezionando un file PNG o JPG dal tuo sistema locale. La dimensione dell'immagine raccomandata è 320 x 320 pixel. La dimensione del file massima è 100 Kb.
4. Seleziona un colore di intestazione per il widget dal selezionatore del colore o immetti il codice esadecimale per un altro colore.
5. Controlla il pannello dell'anteprima e fai clic su **Save Changes** quando sei soddisfatto delle tue personalizzazioni. Viene visualizzato un messaggio di conferma.
6. Verifica le tue modifiche visitando la tua applicazione. Non devi ricreare la tua applicazione. Le tue immagini vengono archiviate nel database di {{site.data.keyword.appid_short}} e visualizzate la volta successiva in cui viene richiamato il widget di accesso.


</br>

## Richiamo del widget di accesso con l'SDK Android
{: #android}

Con i provider di identità sociali abilitati, puoi richiamare la schermata di accesso preconfigurata con l'SDK Android.
{: shortdesc}

1. Configura i tuoi provider di identità. 
2. Inserisci il seguente comando nel tuo codice.
    ```java
    LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launch(this, new AuthorizationListener() {
          @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
            //Si è verificata un'eccezione
      }

          @Override
        public void onAuthorizationCanceled () {
            //Autenticazione annullata dall'utente
        }

          @Override
        public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
            //Utente autenticato
        }
        });
    ```
    {: codeblock}


</br>

## Richiamo del widget di accesso con l'SDK iOS Swift
{: ios-swift}

Con i provider di identità sociali abilitati, puoi richiamare la schermata di accesso preconfigurata con l'SDK iOS Swift.
{: shortdesc}

1. Configura i tuoi provider di identità. 
2. Aggiungi il seguente comando al tuo codice dell'applicazione.
  ```swift
  import BluemixAppID
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, response:Response?) {
          //Utente autenticato
      }

      public func onAuthorizationCanceled() {
          //Autenticazione annullata dall'utente
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          //Si è verificata un'eccezione
      }
  }

  AppID.sharedInstance.loginWidget?.launch(delegate: delegate())
  ```
  {: codeblock}


</br>

## Richiamo del widget di accesso con l'SDK Node.js
{: #nodejs}

Con i provider di identità sociali abilitati, puoi richiamare la schermata di accesso preconfigurata con l'SDK Node.js.
{: shortdesc}

1. Configura i tuoi provider di identità. 
2. Aggiungi il seguente comando al tuo codice. 
    ```JavaScript

    var express = require('express');
  var passport = require('passport');
  var WebAppStrategy = require('bluemix-appid').WebAppStrategy;
    ```
    {: codeblock}


</br>

## Richiamo del widget di accesso con l'SDK Swift
{: #swift}

Con i provider di identità sociali abilitati, puoi richiamare la schermata di accesso preconfigurata con l'SDK Swift.
{: shortdesc}

WebAppKituraCredentialsPlugin si basa sul flusso di concessione del codice di autorizzazione OAuth2 e deve essere utilizzato per le applicazioni web che utilizzano i browser. Il plugin fornisce gli strumenti per implementare l'autenticazione e i flussi di autorizzazione. Il plugin inoltre fornisce il meccanismo di individuazione dei tentativi non autenticati di accesso alle risorse protette e automaticamente esegue il reindirizzamento a un browser dell'utente alla pagina di autenticazione. Dopo un'autenticazione corretta, a un utente viene fornito l'URL di callback dell'applicazione web, che utilizza il plugin per ottenere i token di identità e di accesso da {{site.data.keyword.appid_short_notm}}. Dopo aver ottenuto questi token, il plugin li archivia in una sessione HTTP in WebAppKituraCredentialsPlugin.AuthContext.

Il seguente codice illustra come utilizzare WebAppKituraCredentialsPlugin in un'applicazione Kitura per proteggere l'endpoint `/protected`.

  ```swift
  import Foundation
  import Kitura
  import KituraSession
  import Credentials
  import SwiftyJSON
  import BluemixAppID

  // I seguenti URL saranno utilizzati per i flussi AppID OAuth
  var LOGIN_URL = "/ibm/bluemix/appid/login"
  var CALLBACK_URL = "/ibm/bluemix/appid/callback"
  var LOGOUT_URL = "/ibm/bluemix/appid/logout"
  var LANDING_PAGE_URL = "/index.html"

  // Configurare Kitura per utilizzare il middleware della sessione
  // Deve essere configurato con l'archivio della sessione corretto per gli ambienti
  // di produzione. Consulta https://github.com/IBM-Swift/Kitura-Session per
  // ulteriore documentazione
  let router = Router()
  let session = Session(secret: "Some secret")
  router.all(middleware: session)

  let options = [
  	"clientId": "{client-id}",
  	"secret": "{secret}",
  	"tenantId": "{tenant-id}",
  	"oauthServerUrl": "{oauth-server-url}",
  	"redirectUri": "{app-url}" + CALLBACK_URL
  ]
  let webappKituraCredentialsPlugin = WebAppKituraCredentialsPlugin(options: options)
  let kituraCredentials = Credentials()
  kituraCredentials.register(plugin: webappKituraCredentialsPlugin)

  // Endpoint di accesso esplicito
  router.get(LOGIN_URL,
  		   handler: kituraCredentials.authenticate(credentialsType: webappKituraCredentialsPlugin.name,
  												   successRedirect: LANDING_PAGE_URL,
  												   failureRedirect: LANDING_PAGE_URL
  ))

  // Callback per terminare il processo di autorizzazione. Richiamerà i token di identità e di accesso da AppID
  router.get(CALLBACK_URL,
  		   handler: kituraCredentials.authenticate(credentialsType: webappKituraCredentialsPlugin.name,
  												   successRedirect: LANDING_PAGE_URL,
  												   failureRedirect: LANDING_PAGE_URL
  ))

  // Disconnettere l'endpoint. Cancellare le informazioni di autenticazione dalla sessione
  router.get(LOGOUT_URL, handler:  { (request, response, next) in
  	kituraCredentials.logOut(request: request)
  	webappKituraCredentialsPlugin.logout(request: request)
  	_ = try? response.redirect(LANDING_PAGE_URL)
  })

  // Area protetta
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
  var port = 3000
  if let portString = ProcessInfo.processInfo.environment["PORT"]{
      port = Int(portString)!
  }
  print("Starting on \(port)")

  // Aggiungi un server HTTP e collegalo al router
  Kitura.addHTTPServer(onPort: port, with: router)

  // Avvia il runloop Kitura (questa chiamata non viene mai restituita)
  Kitura.run()
  ```
  {: codeblock}
