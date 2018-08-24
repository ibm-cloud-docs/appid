---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-09"

---

{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:pre: .pre}
{:new_window: target="blank"}
{:shortdesc: .shortdesc}


# Visualizzazione delle schermate predefinite
{: #default}

{{site.data.keyword.appid_full}} fornisce un widget di accesso che ti consente di fornire ai tuoi utenti opzioni di accesso sicuro.
{: shortdesc}

Quando la tua applicazione è configurata per utilizzare un provider di identità, i visitatori della tua applicazione vengono indirizzati a una schermata di accesso dal widget di accesso. Come impostazione predefinita, quando è impostato su **On** un solo provider, i visitatori vengono reindirizzati alla schermata di autenticazione di quel provider di identità. Con il widget di accesso puoi visualizzare una schermata di accesso predefinita oppure, con Cloud Directory, puoi riutilizzare le tue IU esistenti. E, come bonus aggiunto, puoi aggiornare il tuo flusso di accesso in qualsiasi momento, senza modificare il codice sorgente in alcun modo! 


Il servizio utilizza i tipi di concessione OAuth 2 per associare il processo di autorizzazione. Quando configuri i provider di identità sociali come Facebook, viene utilizzato il [flusso Oauth2 Authorization Grant](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html) per richiamare il widget di accesso.

Vuoi creare un'esperienza che sia unica per la tua applicazione? Puoi [portare i tuoi schermi](/docs/services/appid/branded.html)!
{: tip}


## Personalizzazione della schermata di accesso predefinita
{: #login-widget}

Puoi personalizzare la schermata di accesso preconfigurata per visualizzare il logo e i colori che preferisci.
{: shortdesc}

Per personalizzare la schermata:

1. Apri il dashboard del servizio {{site.data.keyword.appid_short_notm}}.
2. Seleziona la sezione **Login Customization**. Puoi modificare l'aspetto del widget di accesso per allinearlo al marchio della tua azienda.
3. Carica il tuo logo aziendale selezionando un file PNG o JPG dal tuo sistema locale. La dimensione dell'immagine raccomandata è 320 x 320 pixel. La dimensione del file massima è 100 Kb.
4. Seleziona un colore di intestazione per il widget dal selezionatore del colore o immetti il codice esadecimale per un altro colore.
5. Controlla il pannello dell'anteprima e fai clic su **Save Changes** quando sei soddisfatto delle tue personalizzazioni. Viene visualizzato un messaggio di conferma.
6. Nel tuo browser, aggiorna la pagina di accesso per verificare le tue modifiche.


## Pianificazione di quali schermi visualizzare
{: #plan}

{{site.data.keyword.appid_short_notm}} fornisce una schermata di accesso predefinita che puoi richiamare se non disponi di schermate dell'IU da visualizzare.
{: shortdesc}

A seconda della configurazione del tuo provider di identità, le schermate che puoi visualizzare sono diverse. Il servizio non fornisce funzionalità avanzate per i provider di identità sociali perché non abbiamo mai accesso alle informazioni sugli account utente. Gli utenti devono andare nel provider di identità per gestire le loro informazioni. Ad esempio, se volessero cambiare la loro password di Facebook, dovrebbero andare su www.facebook.com.

Controlla la seguente tabella per vedere quali schermate puoi visualizzare per ciascun tipo di provider di identità.

<table>
  <thead>
    <tr>
      <th>Schermata di visualizzazione</th>
      <th>Provider di identità sociale</th>
      <th>Provider di identità aziendale</th>
      <th>Cloud Directory</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Accedi</td>
      <td><img src="images/confirm.png" width="32" alt="Funzione disponibile" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="Funzione disponibile" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="Funzione disponibile" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Registrati</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Funzione disponibile" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Password dimenticata</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Funzione disponibile" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Modifica della password</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Funzione disponibile" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Dettagli account</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Funzione disponibile" style="width:32px;" /></td>
    </tr>
  </tbody>
</table>

Dopo aver configurato le impostazioni per i [provider di identità sociali](/docs/services/appid/identity-providers.html) e [Cloud Directory](/docs/services/appid/cloud-directory.html), fai clic sul linguaggio che preferisci nella seguente immagine per iniziare a implementare il codice.


Fai clic sull'immagine per utilizzare uno degli SDK forniti o le API. Non dimenticare che puoi trarre vantaggio dall'ID applicazione anche con altre lingue. Utilizzando le nostre API, puoi impostare una directory cloud in qualsiasi applicazione. Per assistenza con le lingue non elencate nell'immagine, consulta i <a href="https://www.ibm.com/blogs/bluemix/tag/app-id/" target="_blank">nostri blog<img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>.
{: shortdesc}

</br>

## Visualizzazione delle schermate predefinite con l'SDK Android
{: #android}

Puoi richiamare le schermate preconfigurate con l'SDK Android.
{: shortdesc}

</br>

**Accedi**
1. Inserisci il seguente comando nel tuo codice.
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
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
            //Utente autenticato
        }
        });
    ```
  {: pre}

</br>
**Registrati**

1. Imposta **Allow users to sign up and reset their password** su **On** nelle impostazioni di Cloud Directory.
2. Richiama LoginWidget per avviare il flusso di registrazione.
  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launchSignUp(this, new AuthorizationListener() {
  		 @Override
          public void onAuthorizationFailure (AuthorizationException exception) {
          }

  		 @Override
          public void onAuthorizationCanceled () {
          }

  		 @Override
  		 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
  			 if (accessToken != null && identityToken != null) {
  			 } else {
  			 }

  		 }
  	 });
  ```
  {: pre}

</br>
**Password dimenticata**

1. Imposta **Allow users to sign up and reset their password** e **Forgot password email** su **On** nelle impostazioni di Cloud Directory.
2. Richiama LoginWidget per avviare il flusso della password dimenticata.
    ```java
    LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launchForgotPassword(this, new AuthorizationListener() {
   			 @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
   			 }

   			 @Override
        public void onAuthorizationCanceled () {
   			 }

   			 @Override
   			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
   			 }
   		 });
    ```
    {: pre}

</br>
**Dettagli account**

1. Imposta **Allow users to sign up and reset their password** su **On** nelle impostazioni di Cloud Directory.
2. Richiama LoginWidget per avviare il flusso di modifica dei dettagli.
   ```java
   LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
   loginWidget.launchChangeDetails(this, new AuthorizationListener() {
  			 @Override
          public void onAuthorizationFailure (AuthorizationException exception) {
          }

  			 @Override
          public void onAuthorizationCanceled () {
          }

  			 @Override
  			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
  			 }
  		 });
   ```
   {: pre}

</br>
**Modifica della password**

1. Imposta **Allow users to sign up and reset their password** su **ON**, nelle impostazioni di Cloud Directory.
2. Richiama LoginWidget per avviare il flusso di modifica della password.
   ```java
    LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launchChangePassword(this, new AuthorizationListener() {
   			 @Override
          public void onAuthorizationFailure (AuthorizationException exception) {
          }

   			 @Override
          public void onAuthorizationCanceled () {
          }

   			 @Override
   			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
   			 }
   		 });
   ```
   {: pre}
</br>
</br>

## Visualizzazione delle schermate predefinite con l'SDK iOS Swift
{: #ios-swift}

Puoi richiamare le schermate preconfigurate con l'SDK iOS Swift.
{: shortdesc}

</br>
**Accedi**

1. Inserisci il seguente comando nel tuo codice.
  ```swift
  import BluemixAppID
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, refreshToken: RefreshToken?) {
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
  {: pre}


</br>
**Registrati**

1. Imposta **Allow users to sign up and reset their password** su **On**, nelle impostazioni di Cloud Directory.
2. Richiama LoginWidget per avviare il flusso di registrazione.
  ```swift
  class delegate : AuthorizationDelegate {
    public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?) {
       if accessToken == nil && identityToken == nil {
        //la verifica email è richiesta
        return
       }
     //Utente autenticato
      }

      public func onAuthorizationCanceled() {
        //Registrazione annullata dall'utente
    }

    public func onAuthorizationFailure(error: AuthorizationError) {
        //Si è verificata un'eccezione
      }
  }

  AppID.sharedInstance.loginWidget?.launchSignUp(delegate: delegate())
  ```
  {: pre}

</br>
**Password dimenticata**

1. Imposta **Allow users to sign up and reset their password** e **Forgot password email** su **On** nelle impostazioni di Cloud Directory.
2. Richiama LoginWidget per avviare il flusso della password dimenticata.
  ```swift
  class delegate : AuthorizationDelegate {
     public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?) {
        //password dimenticata terminato, in questo caso accessToken e identityToken saranno null.
     }

     public func onAuthorizationCanceled() {
         //password dimenticata annullata dall'utente
     }

     public func onAuthorizationFailure(error: AuthorizationError) {
         //Si è verificata un'eccezione
      }
  }

  AppID.sharedInstance.loginWidget?.launchForgotPassword(delegate: delegate())
  ```
  {: pre}

</br>
**Dettagli account**

1. Imposta **Allow users to sign up and reset their password** su **On** nelle impostazioni di Cloud Directory.
2. Richiama LoginWidget per avviare il flusso di modifica dei dettagli.
  ```swift

   class delegate : AuthorizationDelegate {
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?) {
       }

       public func onAuthorizationCanceled() {
     }

       public func onAuthorizationFailure(error: AuthorizationError) {
     }
   }

   AppID.sharedInstance.loginWidget?.launchChangeDetails(delegate: delegate())
  ```
  {: pre}

</br>
**Modifica della password**

1. Imposta **Allow users to sign up and reset their password** su **On** nelle impostazioni di Cloud Directory.
2. Richiama LoginWidget per avviare il flusso di modifica della password.
  ```swift
   class delegate : AuthorizationDelegate {
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?) {
       }

       public func onAuthorizationCanceled() {
     }

       public func onAuthorizationFailure(error: AuthorizationError) {
     }
    }

    AppID.sharedInstance.loginWidget?.launchChangePassword(delegate: delegate())
  ```
  {: pre}
</br>
</br>

## Visualizzazione delle schermate predefinite con l'SDK Node.js
{: #nodejs}

Puoi richiamare le schermate preconfigurate con l'SDK Node.js.
{: shortdesc}

</br>
**Accedi**
1. Imposta Cloud Directory su **On** nelle impostazioni del tuo provider di identità e specifica un endpoint di callback.
2. Aggiungi una rotta post alla tua applicazione che può essere richiamata con i parametri password e nome utente e accedi utilizzando la password del proprietario della risorsa.
    ```javascript
    app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
    	successRedirect: LANDING_PAGE_URL,
    	failureRedirect: ROP_LOGIN_PAGE_URL,
    	failureFlash : true // consenti messaggi flash
    }));
    ```
    {: pre}
    `WebAppStrategy` consente agli utenti di accedere alle tue applicazioni web con un nome utente e una password. Dopo un accesso riuscito, il token di accesso di un utente viene memorizzato nella sessione HTTP ed è disponibile durante la sessione. Una volta eliminata o scaduta la sessione HTTP, il token non è più valido.
    {: tip}

</br>
**Registrati**

1. Imposta **Allow users to sign up and reset their password** su **On** nelle impostazioni di Cloud Directory. Se impostato su no, il processo termina senza richiamare i token di accesso e di identità.
2. Passa la proprietà WebAppStrategy `show`e impostala su `WebAppStrategy.SIGN_UP`.
  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: pre}

</br>
**Password dimenticata**

1. Imposta **Allow users to sign up and reset their password** e **Forgot password email** su **ON** nelle impostazioni di Cloud Directory. Se impostato su no, il processo termina senza richiamare i token di accesso e di identità.
2. Passa la proprietà WebAppStrategy `show`e impostala su `WebAppStrategy.FORGOT_PASSWORD`.
  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: pre}

</br>
**Dettagli account**
1. Imposta **Allow users to sign up and reset their password** su **On** nelle impostazioni di Cloud Directory
2. Passa la proprietà WebAppStrategy `show`e impostala su `WebAppStrategy.CHANGE_DETAILS`.
  ```javascript
  app.get("/change_details", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_DETAILS
  }));
  ```
  {: pre}

</br>
**Modifica della password**
1. Imposta **Allow users to sign up and reset their password** su **On** nelle impostazioni di Cloud Directory.
2. Passa la proprietà WebAppStrategy `show`e impostala su `WebAppStrategy.CHANGE_PASSWORD`.
  ```javascript
  app.get("/change_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_PASSWORD
  }));
  ```
  {: pre}

</br>
</br>

## Visualizzazione delle schermate predefinite con l'SDK Swift
{: #swift}

Con i provider di identità sociali abilitati, puoi richiamare la schermata di accesso preconfigurata con l'SDK Swift.
{: shortdesc}

1. Il seguente codice illustra come utilizzare WebAppKituraCredentialsPlugin in un'applicazione Kitura per proteggere l'endpoint `/protected`.

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
</br>
</br>



