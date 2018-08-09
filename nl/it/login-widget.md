---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

---

{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:pre: .pre}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# Gestione dell'esperienza di accesso

{{site.data.keyword.appid_full}} fornisce un widget di accesso che ti consente di fornire ai tuoi utenti opzioni di accesso sicuro.
{: shortdesc}

Quando la tua applicazione è configurata per utilizzare un provider di identità, i visitatori della tua applicazione vengono indirizzati a una schermata di accesso dal widget di accesso. Come impostazione predefinita, quando è attivo un solo provider, i visitatori vengono reindirizzati alla schermata di autenticazione di quel provider di identità. Con il widget di accesso puoi visualizzare una schermata di accesso predefinita oppure, con Cloud Directory, puoi riutilizzare le tue IU esistenti.

Puoi aggiornare il tuo flusso di accesso in qualsiasi momento, senza modificare il codice sorgente in alcun modo!
{: tip}

Il servizio utilizza i tipi di concessione OAuth 2 per associare il processo di autorizzazione. Quando configuri i provider di identità sociali come Facebook, viene utilizzato il [flusso Oauth2 Authorization Grant](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html) per richiamare il widget di accesso. Quando visualizzi le tue proprie schermate dell'IU, viene utilizzato il [flusso Resource Owner Password Credentials](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html) per accedere e ottenere i token di accesso e identità.


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


## Visualizzazione delle schermate predefinite
{: #default}

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


Fai clic sul linguaggio che preferisci nella seguente immagine per iniziare a implementare il codice.

<img usemap="#default-options-map" border="0" class="image" id="options" src="images/default-options.png" width="750" alt="Fai clic su un'icona di linguaggio SDK per iniziare ad utilizzare Cloud Directory nelle tue applicazioni." style="width:750px;" />
<map name="default-options-map" id="default-options-map">
<area href="login-widget.html#android" alt="Gestione dell'esperienza di accesso con l'SDK Android" shape="rect" coords="113, 8, 224, 123" />
<area href="login-widget.html#ios-swift" alt="Gestione dell'esperienza di accesso con l'SDK iOS Swift." shape="rect" coords="251, 12, 362, 127" />
<area href="login-widget.html#nodejs" alt="Gestione dell'esperienza di accesso con l'SDK Node.js." shape="rect" coords="387, 10, 498, 125" />
<area href="login-widget.html#swift" alt="Gestione dell'esperienza di accesso con l'SDK Swift." shape="rect" coords="525, 10, 636, 125" />
</map>
</br>

### Visualizzazione delle schermate predefinite con l'SDK Android
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

### Visualizzazione delle schermate predefinite con l'SDK iOS Swift
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

### Visualizzazione delle schermate predefinite con l'SDK Node.js
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
### Visualizzazione dell'IU predefinita con l'SDK Swift
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


### Visualizzazione delle schermate personalizzate con l'SDK Android
{: #branded-ui-android}

Con Cloud Directory abilitato, puoi richiamare le schermate personalizzate con l'SDK Android. Puoi scegliere la combinazione delle schermate con cui desideri che i tuoi utenti possano interagire. <a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="blank">Consulta questo blog<img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> per un esempio dettagliato.
{: shortdesc}

</br>
**Accedi**

1. Imposta **Cloud Directory** su **On** come un provider di identità.
2. Inserisci il seguente comando nel tuo codice.
  ```java
  AppID.getInstance().signinWithResourceOwnerPassword(getApplicationContext(), username, password,
         new TokenResponseListener() {
         @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
             //Si è verificata un'eccezione
      }

          @Override
        public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
            //Utente autenticato
        }
         });
  ```
  {: pre}

</br>
</br>

### Visualizzazione delle schermate personalizzate con l'SDK iOS Swift
{: #branded-ui-ios-swift}

Con Cloud Directory abilitato, puoi richiamare le schermate personalizzate con l'SDK iOS Swift.
{: shortdesc}

</br>
**Accedi**

1. Nella scheda del provider di identità nella GUI, imposta Cloud Directory su **On**.
2. Accedi utilizzando la password del proprietario della risorsa. I token di accesso e identità vengono ottenuti quando un utente tenta di accedere utilizzando i propri nome utente e password.
  ```swift
  class delegate : TokenResponseDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
      //Utente autenticato
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
      //Si è verificata un'eccezione
      }
  }

  AppID.sharedInstance.signinWithResourceOwnerPassword(username: username, password: password, delegate: delegate())
  ```
  {: pre}
</br>
</br>

### Visualizzazione delle schermate personalizzate con l'SDK Node.js
{: #branded-ui-nodejs}

Con Cloud Directory abilitato, puoi richiamare le schermate personalizzate con l'SDK Node.js. Puoi scegliere la combinazione di schermate con cui desideri che i tuoi utenti possono interagire. Se scegli un back-end Node.js, puoi utilizzare il nostro modulo self-service nell'SDK Node.js {{site.data.keyword.appid_short_notm}} (link).
{: shortdesc}

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
</br>

## Visualizzazione delle schermate personalizzate con l'API
{: #branding}

Puoi visualizzare le tue proprie schermate personalizzate e sfruttare le funzionalità di autenticazione e autorizzazione di {{site.data.keyword.appid_short_notm}}. Con Cloud Directory come tuo provider di identità, i tuoi utenti potranno interagire con la tua applicazione con meno aiuto da parte tua. Sono in grado di accedere, registrarsi, reimpostare la loro password e altro ancora senza richiedere assistenza.
{: shortdesc}

Per renderlo possibile, {{site.data.keyword.appid_short_notm}} ha esposto le API REST. Puoi utilizzare l'API REST per creare un server di back-end che funzioni per le tue applicazioni web o per interagire con un'applicazione mobile con le tue schermate personalizzate.

L'API di gestione è protetta con i token generati da IBM Cloud Identity and Access Management. Ciò significa che i proprietari degli account possono specificare chi ha nel proprio team un determinato livello di accesso per ciascuna istanza del servizio. Per ulteriori informazioni su come funzionano insieme IAM e {{site.data.keyword.appid_short_notm}}, vedi [Gestione dell'accesso al servizio](/docs/services/appid/iam.html).

Quando un utente sceglie di accedere dalle tue schermate personalizzate, viene utilizzato il [flusso Resource Owner Password Credentials](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html) per ottenere i token di accesso e identità direttamente dalle tue applicazioni web o mobili.

Dopo aver configurato le tue [impostazioni](/docs/services/appid/cloud-directory.html),


**Registrati**
Puoi utilizzare l'endpoint `/sign_up` per consentire agli utenti di registrarsi alla tua applicazione.
Fornisci i seguenti dati nel corpo della richiesta:
  * Il tuo ID tenant.
  * I dati utente Cloud Directory. Vedi [SCIM Full User Representation](https://tools.ietf.org/html/rfc7643#section-8.2) per ulteriori dettagli.
    * Un attributo `password`.
    * Nell'array di email con un attributo `primary` impostato su `true`, devi avere almeno 1 indirizzo email.

A seconda delle tue [configurazioni email](/docs/services/appid/cloud-directory.html), un utente potrebbe ricevere una richiesta di verifica o un'email di benvenuto quando si registra alla tua applicazione. Entrambi i tipi di email vengono attivati quando un utente si registra alla tua applicazione. L'email di verifica contiene un pulsante **Verify**. Dopo aver premuto il pulsante e confermato la sua identità, {{site.data.keyword.appid_short_notm}} visualizza una schermata che lo ringrazia per la verifica.   

Puoi presentare la tua propria pagina di post-verifica:

1. Passa alla scheda **Custom Landing Pages** del dashboard {{site.data.keyword.appid_short_notm}}.
2. Immetti l'URL per la tua pagina di destinazione in **URL for your custom email address verification page**

Quando viene fornito questo valore, {{site.data.keyword.appid_short_notm}} richiama l'URL insieme a una query `context`. Quando richiami l'endpoint `/sign_up/confirmation_result` e passi il parametro `context` ricevuto, il risultato indica se il tuo utente ha verificato il suo account. Se lo ha fatto, puoi visualizzare la tua pagina personalizzata.

</br>
**Password dimenticata**

Puoi utilizzare l'endpoint `/forgot_password` per consentire agli utenti di recuperare la propria password nel caso in cui la dimentichino.

Fornisci i seguenti dati nel corpo della richiesta:
  * Il tuo ID tenant.
  * L'email dell'utente di Cloud Directory.

Quando l'endpoint viene richiamato, all'utente viene inviata un'email di reimpostazione della password. L'email contiene un pulsante **Reset**. Dopo aver premuto il pulsante, {{site.data.keyword.appid_short_notm}} visualizza una schermata che gli permette di reimpostare la propria password. 

Puoi presentare la tua propria pagina di post-reimpostazione della password:

1. Passa alla scheda **Custom Landing Pages** del dashboard {{site.data.keyword.appid_short_notm}}.
2. Immetti l'URL per la tua pagina di destinazione in **URL for your custom reset password page**  

Quando viene fornito questo valore, {{site.data.keyword.appid_short_notm}} richiama l'URL insieme a una query `context`. Il parametro `context` è utilizzato per ricevere il risultato quando viene richiamato `/forgot_password/confirmation_result`. Se il risultato ha esito positivo, puoi visualizzare la tua pagina personalizzata.

Aggiungi una stringa casuale alla pagina di reimpostazione della password personalizzata e passala al tuo back-end quando la richiesta viene inviata. Chiedi al tuo gestore di convalidare la stringa e chiama l'endpoint `/change_password` solo se è valida. In questo modo, puoi ridurre la vulnerabilità del tuo endpoint di reimpostazione della password di back-end.
{: tip}

</br>
**Modifica della password**

Puoi utilizzare l'endpoint `/change_password` in due modi. Quando un utente invia una richiesta di reimpostazione o quando un utente ha effettuato l'accesso alla tua applicazione e vuole aggiornare la propria password.

Per aggiornare la password dopo una richiesta di reimpostazione:

Fornisci i seguenti dati nel corpo della richiesta:
  * Il tuo ID tenant.
  * La nuova password dell'utente.
  * L'UUID utente di Cloud Directory.
  * Facoltativo: l'indirizzo IP da cui è stata eseguita la reimpostazione della password. Se scegli di passare l'indirizzo IP, è disponibile il segnaposto `%{passwordChangeInfo.ipAddress}` per il template di email di modifica della password.

A seconda della tua configurazione, quando una password viene modificata {{site.data.keyword.appid_short_notm}} potrebbe inviare un'email all'utente facendogli sapere che c'è stata una modifica.

</br>
Per consentire agli utenti di modificare la loro password mentre sono connessi alla tua applicazione:

Fornisci i seguenti dati nel corpo della richiesta:
  * Il tuo ID tenant.
  * La nuova password dell'utente.
  * L'UUID utente di Cloud Directory.

La tua pagina di modifica della password dovrebbe richiedere all'utente di immettere la password corrente e la nuova password.
{: tip}

Il tuo back-end convalida la password corrente dell'utente con l'API ROP e, se valida, richiama l'endpoint con la nuova password. A seconda della tua configurazione, quando una password viene modificata {{site.data.keyword.appid_short_notm}} potrebbe inviare un'email all'utente facendogli sapere che c'è stata una modifica.

</br>
**Invia nuovamente**

Puoi utilizzare `/resend/{templateName}` per inviare nuovamente un'email quando un utente non la riceve per qualche motivo.

Fornisci i seguenti dati nel corpo della richiesta:
  * L'ID tenant.
  * Il nome del template.
  * L'UUID utente di Cloud Directory.


**Modifica dettagli**

Quando un utente accede alla tua applicazione, può aggiornare alcune delle sue informazioni. Puoi utilizzare `/Users/{userId}` per ottenere e aggiornare le sue informazioni.

Quando i dettagli dell'utente vengono aggiornati, l'endpoint riceve i dati utente aggiornati nel corpo della richiesta in [formato SCIM](https://tools.ietf.org/html/rfc7643#section-8.2). Assicurati di modificare solo i dettagli pertinenti.

L'indirizzo email non può essere modificato.
{: tip}
