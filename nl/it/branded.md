---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:tip: .tip}

# Personalizzazione della tua applicazione
{: #branding}

Puoi visualizzare le tue proprie schermate personalizzate e sfruttare le funzionalità di autenticazione e autorizzazione di {{site.data.keyword.appid_full}}. Con Cloud Directory come tuo provider di identità, i tuoi utenti potranno interagire con la tua applicazione con meno aiuto da parte tua. Sono in grado di accedere, registrarsi, modificare la propria password e altro ancora senza richiedere assistenza.
{: shortdesc}

Quando utilizzi le tue proprie schermate, viene utilizzato il [flusso Resource Owner Password Credentials](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html) per fornire i token di accesso e identità.


## Personalizzazione della tua applicazione con l'SDK Swift iOS
{: #branded-ui-ios-swift}

Con Cloud Directory abilitato, puoi richiamare le schermate personalizzate con l'SDK iOS Swift.
{: shortdesc}

</br>
**Accedi**

1. Nella scheda del provider di identità della GUI, imposta Cloud Directory su **On**.
2. Richiama il widget di accesso per avviare il flusso di accesso. I token di accesso e identità vengono ottenuti quando un utente tenta di accedere utilizzando i propri nome utente o email e password.
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

**Registrati**

1. Nella scheda del provider di identità nella GUI, imposta Cloud Directory su **On**.
2. Imposta **Allow users to sign up and reset their password** su **ON** nelle impostazioni di Cloud Directory.
3. Richiama il widget di accesso per avviare il flusso di registrazione. 
  ```swift
  class delegate : AuthorizationDelegate {
    public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
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

1. Nella scheda del provider di identità nella GUI, imposta Cloud Directory su **On**.
2. Imposta **Allow users to sign up and reset their password** su **ON** nelle impostazioni di Cloud Directory.
3. Richiama il widget di accesso per avviare il flusso della password dimenticata. 
  ```swift
  class delegate : AuthorizationDelegate {
     public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
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

**Modifica dettagli**

1. Nella scheda del provider di identità nella GUI, imposta Cloud Directory su **On**.
2. Imposta **Allow users to sign up and reset their password** su **ON** nelle impostazioni di Cloud Directory.
3. Richiama il widget di accesso per avviare il flusso di modifica dei dettagli. 
  ```swift
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
         //Utente autenticato e token di aggiornamento ricevuto
      }

      public func onAuthorizationCanceled() {
          //dettagli modificati annullati dall'utente
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          //Si è verificata un'eccezione
      }
  }

   AppID.sharedInstance.loginWidget?.launchChangeDetails(delegate: delegate())
  ```
  {: pre}

</br>

**Modifica della password**

1. Nella scheda del provider di identità nella GUI, imposta Cloud Directory su **On**.
2. Imposta **Allow users to sign up and reset their password** su **ON** nelle impostazioni di Cloud Directory.
3. Richiama il widget di accesso per avviare il flusso di modifica dei dettagli. 
  ```swift
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
          //Utente autenticato e token di aggiornamento ricevuto
      }

      public func onAuthorizationCanceled() {
          //password modificata annullata dall'utente
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
           //Si è verificata un'eccezione
      }
   }

    AppID.sharedInstance.loginWidget?.launchChangePassword(delegate: delegate())
  ```
  {: pre}

</br>


## Personalizzazione della tua applicazione con l'SDK Android
{: #branded-ui-android}

Con Cloud Directory abilitato, puoi richiamare le schermate personalizzate con l'SDK Android. Puoi scegliere la combinazione delle schermate con cui desideri che i tuoi utenti possano interagire. <a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="blank">Consulta questo blog<img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> per un esempio dettagliato.
{: shortdesc}

</br>

**Accedi**

1. Imposta **Cloud Directory** su **On** come un provider di identità.
2. Ottieni un accesso e i token di aggiornamento e identità fornendo la password e il nome utente dell'utente finale. 
3. Richiama il widget di accesso per avviare il flusso di accesso. 
  ```java
  AppID.getInstance().signinWithResourceOwnerPassword(getApplicationContext(), username, password,
         new TokenResponseListener() {
      @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //Si è verificata un'eccezione
      }

      @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          //Utente autenticato
        }
  });
  ```
  {: pre}

</br>

**Registrati**

1. Imposta **Cloud Directory** su **On** come un provider di identità.
2. Imposta **Allow users to sign up and reset their password** su **ON** nelle impostazioni di Cloud Directory.
3. Richiama il widget di accesso per avviare il flusso di registrazione. 
  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launchSignUp(this, new AuthorizationListener() {
      @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //Si è verificata un'eccezione
      }

      @Override
        public void onAuthorizationCanceled () {
          //Registrazione annullata dall'utente
      }

      @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          if (accessToken != null && identityToken != null) {
              //Utente autenticato
          } else {
              //la verifica email è richiesta
          }
      }
  });
  ```
  {: pre}

</br>


**Password dimenticata**

1. Imposta **Cloud Directory** su **On** come un provider di identità.
2. Imposta **Allow users to sign up and reset their password** su **ON** nelle impostazioni di Cloud Directory.
3. Richiama il widget di accesso per avviare il flusso della password dimenticata. 
  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launchForgotPassword(this, new AuthorizationListener() {
      @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //Si è verificata un'eccezione
      }

      @Override
        public void onAuthorizationCanceled () {
          // Password dimenticata annullata dall'utente
      }

      @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          // Password dimenticata terminato, in questo caso accessToken e identityToken saranno null.
      }
  });
  ```
  {: pre}

</br>

**Modifica dettagli**

1. Imposta **Cloud Directory** su **On** come un provider di identità.
2. Imposta **Allow users to sign up and reset their password** su **ON** nelle impostazioni di Cloud Directory.
3. Richiama il widget di accesso per avviare il flusso di modifica dei dettagli. 
  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
   loginWidget.launchChangeDetails(this, new AuthorizationListener() {
      @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //Si è verificata un'eccezione
      }

      @Override
        public void onAuthorizationCanceled () {
          // Dettagli modificati annullati dall'utente
      }

      @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          // Utente autenticato e token di aggiornamento ricevuto
      }
  });
  ```
  {: pre}


</br>

**Modifica della password**

1. Imposta **Cloud Directory** su **On** come un provider di identità.
2. Imposta **Allow users to sign up and reset their password** su **ON** nelle impostazioni di Cloud Directory.
3. Richiama il widget di accesso per avviare il flusso di modifica della password. 
  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launchChangePassword(this, new AuthorizationListener() {
      @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //Si è verificata un'eccezione
      }

      @Override
        public void onAuthorizationCanceled () {
          // Password modificata annullata dall'utente
      }

      @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          // Utente autenticato e token di aggiornamento ricevuto
      }
  });
  ```
  {: pre}

</br>
</br>


## Personalizzazione della tua applicazione con l'SDK Node.js
{: #branded-ui-nodejs}

Con Cloud Directory abilitato, puoi richiamare le schermate personalizzate con l'SDK Node.js.
{: shortdesc}

**Accedi**

Utilizzando WebAppStrategy, gli utenti possono accedere alle tue applicazioni web con i propri nome utente e password. Dopo che un utente ha eseguito correttamente l'accesso alla tua applicazione, il loro token di accesso viene memorizzato in una sessione HTTP finché resta attiva. Dopo che la sessione HTTP è stata chiusa o è scaduta, viene distrutto anche il token di accesso.

1. Imposta Cloud Directory su **On** nelle impostazioni del tuo provider di identità e specifica un endpoint di callback.
2. Aggiungi una rotta post alla tua applicazione che può essere richiamata con i parametri password e nome utente e accedi con il flusso della password del proprietario della risorsa.
  ```javascript
  app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
    	failureRedirect: ROP_LOGIN_PAGE_URL,
    	failureFlash : true // consenti messaggi flash
    }));
  ```
  {: pre}
  <table>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="Icona ulteriori informazioni"/> Parametri comando </th>
    </thead>
    <tbody>
      <tr>
        <td><code>successRedirect</code></td>
        <td>L'URL a cui vuoi reindirizzare l'utente dopo un'autenticazione riuscita.</td>
      </tr>
      <tr>
        <td><code>failureRedirect</code></td>
        <td>L'URL a cui vuoi reindirizzare l'utente se l'autenticazione ha esito negativo.</td>
      </tr>
      <tr>
        <td><code>failureFlash</code></td>
        <td>Se impostato su <code>true</code>, viene restituito un messaggio di errore dal servizio Cloud Directory. Per impostazione predefinita, il valore è impostato su <code>false</code>.</td>
      </tr>
    </tbody>
  </table>

  1. Se invii la richiesta nel formato HTML, puoi utilizzare il middle ware [body parser](https://www.npmjs.com/package/body-parser).
  2. Per ottenere il messaggio di errore restituito, puoi utilizzare [connect-flash](https://www.npmjs.com/package/connect-flash). Per ulteriori informazioni, consulta [web app sample](https://github.com/ibm-cloud-security/appid-serversdk-nodejs/blob/master/samples/web-app-sample.js).
  {: tip}

</br>
**Registrati**

1. Imposta Cloud Directory su **On** nelle impostazioni del tuo provider di identità e specifica un endpoint di callback.
2. Imposta **Allow users to sign up and reset their password** su **ON** nelle impostazioni di Cloud Directory.
3. Imposta **Allow users to sign-in without email verification** su **No**. Se non lo fai, non è possibile richiamare i token di accesso e identità {{site.data.keyword.appid_short_notm}}.
4. Aggiungi una rotta post alla tua applicazione che può essere richiamata con i parametri password e nome utente e accedi con il flusso della password del proprietario della risorsa.
  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: pre}

</br>

**Password dimenticata**

1. Imposta Cloud Directory su **On** nelle impostazioni del tuo provider di identità e specifica un endpoint di callback.
2. Imposta **Allow users to sign up and reset their password** su **ON** nelle impostazioni di Cloud Directory.
3. Imposta **Forgot password email** su **ON**.
4. Passa la proprietà *show* a `WebAppStrategy.FORGOT_PASSWORD` per avviare il modulo della password dimenticata.
  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: pre}

</br>

**Modifica dettagli**

1. Imposta Cloud Directory su **On** nelle impostazioni del tuo provider di identità e specifica un endpoint di callback.
2. Imposta **Allow users to sign up and reset their password** su **ON** nelle impostazioni di Cloud Directory.
3. Verifica che l'utente abbia precedentemente eseguito l'autenticazione a {{site.data.keyword.appid_short_notm}}.
4. Passa la proprietà *show* a `WebAppStrategy.CHANGE_DETAILS` per avviare il modulo della password dimenticata.
  ```javascript
  app.get("/change_details", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_DETAILS
  }));
  ```
  {: pre}

</br>

## Personalizzazione della tua applicazione con l'API
{: #branded-ui-api}

Puoi visualizzare le tue proprie schermate personalizzate e sfruttare le funzionalità di autenticazione e autorizzazione di {{site.data.keyword.appid_short_notm}}. Con Cloud Directory come tuo provider di identità, i tuoi utenti potranno interagire con la tua applicazione con meno aiuto da parte tua. Sono in grado di accedere, registrarsi, reimpostare la loro password e altro ancora senza richiedere assistenza.
{: shortdesc}

Per renderlo possibile, {{site.data.keyword.appid_short_notm}} espone le API REST. Puoi utilizzare l'API REST per creare un server di back-end che funzioni per le tue applicazioni web o per interagire con un'applicazione mobile con le tue schermate personalizzate.

L'API di gestione è protetta con i token generati da IBM Cloud Identity and Access Management. Ciò significa che i proprietari degli account possono specificare chi ha nel proprio team un determinato livello di accesso per ciascuna istanza del servizio. Per ulteriori informazioni su come funzionano insieme IAM e {{site.data.keyword.appid_short_notm}}, vedi [Gestione dell'accesso al servizio](/docs/services/appid/iam.html).

Dopo aver configurato le tue [impostazioni](/docs/services/appid/cloud-directory.html), puoi richiamare i seguenti endpoint per visualizzare ogni schermata.


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

Fornisci i seguenti dati nel corpo della richiesta per aggiornare la password dopo una richiesta di reimpostazione: 
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
