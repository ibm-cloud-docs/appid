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

# Personalizzazione dell'esperienza di accesso 
{: #branding}

Puoi visualizzare le tue proprie IU personalizzate mentre sfrutti le funzionalità di autenticazione e di autorizzazione di {{site.data.keyword.appid_full}}. Con Cloud Directory come tuo provider di identità, i tuoi utenti potranno interagire con la tua applicazione con meno aiuto da parte tua. Sono in grado di accedere, registrarsi, modificare la propria password e altro ancora senza richiedere assistenza.
{: shortdesc}

Con Cloud Directory come tuo provider di identità, [Resource Owner Password Credentials flow](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html) viene utilizzato per fornire i token di accesso e di identità.

**Nota**: tu puoi soltanto portare alle pagine di accesso personalizzato quando Cloud Directory è l'unica opzione configurata. Se hai impostato altri provider di identità su **on**, viene visualizzata la schermata di accesso preconfigurata.

## Visualizzazione delle schermate personalizzate con l'SDK Android
{: #branded-ui-android}

Con cloud directory abilitato, puoi richiamare le schermate personalizzate con l'SDK Android. Puoi scegliere la combinazione di schermate con cui desideri i tuoi utenti possono interagire. <a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="blank">Controlla il nostro blog! <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>
{: shortdesc}

</br>
**Accedi**

1. Imposta **Cloud Directory** su **On** come un provider di identità.
2. Inserisci il seguente comando nel tuo codice.
  ```java
  AppID.getInstance().obtainTokensWithROP(getApplicationContext(), username, password,
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
  {: codeblock}

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
		public void onAuthorizationSuccess(AccessToken accessToken, IdentityToken identityToken) {
  			 if (accessToken != null && identityToken != null) {
  			 } else {
  			 }

  		 }
  	 });
  ```
  {: codeblock}

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
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
          }
   		 });
    ```
    {: codeblock}

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
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
          }
  		 });
   ```
   {: codeblock}

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
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
          }
   		 });
   ```
   {: codeblock}

</br>
</br>

## Visualizzazione delle schermate personalizzate con l'SDK iOS Swift
{: #branded-ui-ios-swift}

Con cloud directory abilitato, puoi richiamare le schermate personalizzate con l'SDK ios Swift. Puoi scegliere la combinazione di schermate con cui desideri i tuoi utenti possono interagire.
{: shortdesc}

</br>
**Accedi**

1. Nella scheda del provider di identità nella GUI, imposta Cloud Directory su **On**.
2. Accedi utilizzando la password del proprietario della risorsa. Puoi ottenere un token ID e di accesso fornendo la password e il nome utente dell'utente finale.
  ```swift
  class delegate : TokenResponseDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
      //Utente autenticato
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
      //Si è verificata un'eccezione
      }
  }

  AppID.sharedInstance.obtainTokensWithROP(username: username, password: password, delegate: delegate())
  ```
  {: codeblock}

</br>
**Registrati**

1. Imposta **Allow users to sign up and reset their password** su **On**, nelle impostazioni di Cloud Directory.
2. Richiama LoginWidget per avviare il flusso di registrazione.
  ```swift
  class delegate : AuthorizationDelegate {
    public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
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
  {: codeblock}

</br>
**Password dimenticata**

1. Imposta **Allow users to sign up and reset their password** e **Forgot password email** su **On** nelle impostazioni di Cloud Directory.
2. Richiama LoginWidget per avviare il flusso della password dimenticata. 
  ```swift
  class delegate : AuthorizationDelegate {
     public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
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
  {: codeblock}

</br>
**Dettagli account**

1. Imposta **Allow users to sign up and reset their password** su **On** nelle impostazioni di Cloud Directory.
2. Richiama LoginWidget per avviare il flusso di modifica dei dettagli. 
  ```swift

   class delegate : AuthorizationDelegate {
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
       }

       public func onAuthorizationCanceled() {
     }

       public func onAuthorizationFailure(error: AuthorizationError) {
     }
   }

   AppID.sharedInstance.loginWidget?.launchChangeDetails(delegate: delegate())
  ```
  {: codeblock}

</br>
**Modifica della password**

1. Imposta **Allow users to sign up and reset their password** su **On** nelle impostazioni di Cloud Directory.
2. Richiama LoginWidget per avviare il flusso di modifica della password. 
  ```swift
   class delegate : AuthorizationDelegate {
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
       }

       public func onAuthorizationCanceled() {
     }

       public func onAuthorizationFailure(error: AuthorizationError) {
     }
    }

    AppID.sharedInstance.loginWidget?.launchChangePassword(delegate: delegate())
  ```
  {: codeblock}

</br>

## Visualizzazione delle schermate personalizzate con l'SDK Node.js
{: #branded-ui-nodejs}

Con cloud directory abilitato, puoi richiamare le schermate personalizzate con l'SDK Node.js. Puoi scegliere la combinazione di schermate con cui desideri i tuoi utenti possono interagire.
{: shortdesc}

**Accedi**
1. Imposta Cloud Directory su **On** nelle impostazioni del tuo provider di identità e specifica un endpoint di callback.
2. Aggiungi una rotta post alla tua applicazione che può essere richiamata con i parametri password e nome utente e accedi utilizzando la password del proprietario della risorsa.
    **Nota**: `WebAppStrategy` consente agli utenti di accedere alle tue applicazioni web con un nome utente e una password. Dopo un accesso corretto, viene archiviato un token di accesso dell'utente nella sessione HTTP ed è disponibile per la durata della sessione. Una volta che la sessione HTTP è stata distrutta o è scaduta, il token non è più valido.
    ```javascript
    app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
    	successRedirect: LANDING_PAGE_URL,
    	failureRedirect: ROP_LOGIN_PAGE_URL,
    	failureFlash : true // consenti messaggi flash
    }));
    ```
    {: codeblock}

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
  {: codeblock}

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
  {: codeblock}

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
  {: codeblock}

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
  {: codeblock}
