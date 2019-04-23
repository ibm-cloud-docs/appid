---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-06"

keywords: authentication, authorization, identity, app security, secure, development, sign in, sign up, password, social, enterprise

subcollection: appid

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}


# Visualizzazione del widget di accesso
{: #login-widget}

{{site.data.keyword.appid_full}} fornisce un widget di accesso che ti consente di fornire ai tuoi utenti delle opzioni di accesso sicure.
{: shortdesc}

Quando la tua applicazione è configurata per utilizzare un provider di identità, i visitatori della tua applicazione vengono indirizzati a una schermata di accesso dal widget di accesso. Con il widget di accesso, puoi visualizzare le schermate preconfigurate per i tuoi flussi di accesso. Come bonus, puoi aggiornare il tuo flusso di accesso in qualsiasi momento senza modificare il tuo codice di origine in alcun modo.

Vuoi creare un'esperienza che sia unica per la tua applicazione? Puoi [portare i tuoi schermi](/docs/services/appid?topic=appid-branded)!
{: tip}

## Descrizione del widget di accesso
{: #widget-understanding}

Puoi avvalerti di {{site.data.keyword.appid_short_notm}}, anche senza le tue schermate IU, visualizzando il widget di accesso.
{: shortdesc}

### Qual è il valore predefinito?
{: #widget-default}

Quando viene configurato più di un provider di identità, un utente viene reindirizzato al widget di accesso quando tenta di accedere alla tua applicazione. Utilizzando il widget di accesso, gli utenti possono scegliere il provider con cui vogliono verificare le proprie identità. Ma, quando solo un provider è impostato su **On**, i visitatori vengono reindirizzati alla schermata di autenticazione di quel provider di identità.

### Quante informazioni ottiene {{site.data.keyword.appid_short_notm}} da un provider di identità?
{: #widget-obtain-info}

Quando utilizzi i provider di identità aziendali o social, {{site.data.keyword.appid_short_notm}} ha l'accesso in lettura alle informazioni sull'account degli utenti. Il servizio utilizza un token e le asserzioni restituite dal provider di identità per verificare se un utente è chi dice di essere. Poiché il servizio non ha mai l'accesso in scrittura alle informazioni, gli utenti devono utilizzare il provider di identità di loro scelta per effettuare delle azioni, come il ripristino della propria password. Ad esempio, se un utente accede alla tua applicazione con Facebook e poi volesse modificare la propria password, deve andare all'indirizzo www.facebook.com per farlo.

Quando utilizzi [Cloud Directory](/docs/services/appid?topic=appid-cloud-directory), {{site.data.keyword.appid_short_notm}} è il provider di identità. Il servizio utilizza il tuo registro per verificare l'identità dei tuoi utenti. Poiché {{site.data.keyword.appid_short_notm}} è il provider, gli utenti possono avvalersi della funzionalità avanzata, come il ripristino delle loro password, direttamente nella tua applicazione.


### Quali schermate possono essere visualizzate per ogni provider?
{: #widget-options}

Controlla la seguente tabella per vedere quali schermate puoi visualizzare per ciascun tipo di provider di identità.

<table>
  <thead>
    <tr>
      <th>Schermata del widget di accesso</th>
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

</br>
</br>

## Personalizzazione del widget di accesso
{: #widget-customize}

{{site.data.keyword.appid_short_notm}} fornisce una schermata di accesso predefinita che puoi richiamare se non disponi di schermate dell'IU da visualizzare. Puoi personalizzare la schermata per visualizzare il logo e i colori che preferisci.
{: shortdesc}

Per personalizzare la schermata:

1. Apri il dashboard del servizio {{site.data.keyword.appid_short_notm}}.
2. Seleziona la sezione **Login Customization**. Puoi modificare l'aspetto del widget di accesso per allinearlo al marchio della tua azienda.
3. Carica il tuo logo aziendale selezionando un file PNG o JPG dal tuo sistema locale. La dimensione dell'immagine raccomandata è 320 x 320 pixel. La dimensione del file massima è 100 Kb.
4. Seleziona un colore di intestazione per il widget dal selezionatore del colore o immetti il codice esadecimale per un altro colore.
5. Controlla il pannello dell'anteprima e fai clic su **Save Changes** quando sei soddisfatto delle tue personalizzazioni. Viene visualizzato un messaggio di conferma.
6. Nel tuo browser, aggiorna la pagina di accesso per verificare le tue modifiche.

Importante! Puoi trarre vantaggio da {{site.data.keyword.appid_short_notm}} anche con altri linguaggi. Se non vedi un SDK per il linguaggio con cui stai lavorando, puoi sempre utilizzare le API. Consulta i <a href="https://www.ibm.com/blogs/bluemix/tag/app-id/" target="blank">nostri blog<img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>.
{: tip}


## Visualizzazione del widget di accesso con l'SDK Android
{: #widget-display-android}

Puoi richiamare le schermate preconfigurate con l'[SDK client Android](https://github.com/ibm-cloud-security/appid-clientsdk-android).
{: shortdesc}

Inserisci il seguente comando nel tuo codice.

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
{: codeblock}

</br>

### Registrati
{: #widget-android-signup}

1. Configura le tue [impostazioni](/docs/services/appid?topic=appid-cloud-directory#cd-settings) di Cloud Directory nella GUI. Sia **Allow users to sign up to your app** che **Allow users to manage their account from your app** devono essere impostati su **On**.
2. Aggiungi il seguente codice alla tua applicazione. Quando un utente si registra alla tua applicazione dalla tua schermata personalizzata, viene avviato il flusso di registrazione. La seguente chiamata non solo registra l'utente, ma può anche inviare un'email di verifica per completare la registrazione, a seconda delle tue configurazioni Cloud Directory.

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

### Password dimenticata
{: #widget-android-forgot-password}

1. Configura le tue [impostazioni](/docs/services/appid?topic=appid-cloud-directory#cd-settings) di Cloud Directory nella GUI. **Allow users to manage their account from your app** deve essere impostato su **On**.
2. Nella scheda **Reset Password** del dashboard del servizio, assicurati che **Forgot password email** sia impostato su **On**.
3. Aggiungi il seguente codice alla tua applicazione. Quando un utente fa clic su "forgot password" nella tua applicazione, l'SDK richiama l'API forgot_password per inviare un'email all'utente per consentirgli di ripristinare la propria password.

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
  {: codeblock}

</br>

### Dettagli della modifica
{: #widget-android-change-details}

1. Configura le tue [impostazioni](/docs/services/appid?topic=appid-cloud-directory#cd-settings) di Cloud Directory nella GUI. Sia **Allow users to sign up to your app** che **Allow users to manage their account from your app** devono essere impostati su **On**.
2. Nella scheda **Password changed** del dashboard del servizio, imposta **Password changed email** su
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
  {: codeblock}

</br>

### Modifica della password
{: #widget-android-change-password}

1. Configura le tue [impostazioni](/docs/services/appid?topic=appid-cloud-directory#cd-settings) di Cloud Directory nella GUI. Sia **Allow users to sign up to your app** che **Allow users to manage their account from your app** devono essere impostati su **On**.
2. Inserisci il seguente codice nella tua applicazione per avviare il flusso di modifica della password.

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
  {: codeblock}



## Visualizzazione del widget di accesso con l'SDK iOS Swift
{: #widget-display-ios-swift}

Puoi richiamare le schermate preconfigurate con l'[SDK client iOS Swift](https://github.com/ibm-cloud-security/appid-clientsdk-swift).
{: shortdesc}

Inserisci il seguente comando nel tuo codice.

  ```swift
  import IBMCloudAppID
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
  {: codeblock}

</br>

### Registrati
{: #widget-ios-signup}

1. Configura le tue [impostazioni](/docs/services/appid?topic=appid-cloud-directory#cd-settings) di Cloud Directory nella GUI. Sia **Allow users to sign up to your app** che **Allow users to manage their account from your app** devono essere impostati su **On**.
2. Inserisci il seguente codice nella tua applicazione. Quando un utente tenta di registrarsi alla tua applicazione, il widget di accesso viene richiamato e visualizza la tua pagina di registrazione personalizzata.

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
  {: codeblock}

</br>

### Password dimenticata
{: #widget-ios-forgot-password}

1. Configura le tue [impostazioni](/docs/services/appid?topic=appid-cloud-directory#cd-settings) di Cloud Directory nella GUI. **Allow users to manage their account from your app** deve essere impostato su **On**.
2. Nella scheda **Reset Password** del dashboard del servizio, assicurati che **Forgot password email** sia impostato su **On**.
3. Inserisci il seguente codice nella tua applicazione. Quando uno degli utenti dell'applicazione richiede che la sua password venga aggiornata, viene richiamato il widget di accesso e si avvia il processo.

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
  {: codeblock}

</br>

### Dettagli della modifica
{: #widget-ios-change-details}

1. Configura le tue [impostazioni](/docs/services/appid?topic=appid-cloud-directory#cd-settings) di Cloud Directory nella GUI. Sia **Allow users to sign up to your app** che **Allow users to manage their account from your app** devono essere impostati su **On**.
2. Nella scheda **Password changed** del dashboard del servizio, imposta **Password changed email** su
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
  {: codeblock}

</br>

### Modifica della password
{: #widget-ios-change-password}

1. Configura le tue [impostazioni](/docs/services/appid?topic=appid-cloud-directory#cd-settings) di Cloud Directory nella GUI. Sia **Allow users to sign up to your app** che **Allow users to manage their account from your app** devono essere impostati su **On**.
2. Inserisci il seguente codice nella tua applicazione per avviare il flusso di modifica della password.

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
  {: codeblock}


## Visualizzazione del widget di accesso con l'SDK Node.js
{: #widget-display-nodejs}

Puoi richiamare le schermate preconfigurate con l'[SDK server Node.js](https://github.com/ibm-cloud-security/appid-serversdk-nodejs).
{: shortdesc}

Aggiungi una rotta post alla tua applicazione che può essere richiamata con i parametri password e nome utente e accedi utilizzando la password del proprietario della risorsa.

  ```javascript
  app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
    	failureRedirect: ROP_LOGIN_PAGE_URL,
    	failureFlash : true // consenti messaggi flash
    }));
  ```
  {: codeblock}

`WebAppStrategy` consente agli utenti di accedere alle tue applicazioni web con un nome utente e una password. Dopo un accesso riuscito, il token di accesso di un utente viene memorizzato nella sessione HTTP ed è disponibile durante la sessione. Una volta eliminata o scaduta la sessione HTTP, il token non è più valido.
{: tip}

</br>

### Registrati
{: #widget-nodejs-signup}

1. Configura le tue [impostazioni](/docs/services/appid?topic=appid-cloud-directory#cd-settings) di Cloud Directory nella GUI. Sia **Allow users to sign up to your app** che **Allow users to manage their account from your app** devono essere impostati su **On**.
2. Inserisci il seguente codice nella tua applicazione. Quando un utente tenta di registrarsi alla tua applicazione, il widget di accesso viene richiamato e visualizza la tua pagina di registrazione personalizzata.

  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: codeblock}

</br>

### Password dimenticata
{: #widget-nodejs-forgot-password}

1. Configura le tue [impostazioni](/docs/services/appid?topic=appid-cloud-directory#cd-settings) di Cloud Directory nella GUI. **Allow users to manage their account from your app** deve essere impostato su **On**.
2. Nella scheda **Reset Password** del dashboard del servizio, assicurati che **Forgot password email** sia impostato su **On**.
3. Inserisci il seguente codice nella tua applicazione per passare la proprietà *show* a `WebAppStrategy.FORGOT_PASSWORD`. Quando un utente richiede che la sua password della tua applicazione venga aggiornata, viene richiamato il widget di accesso e si avvia il processo.

  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: codeblock}

</br>

### Dettagli della modifica
{: #widget-nodejs-change-details}

1. Configura le tue [impostazioni](/docs/services/appid?topic=appid-cloud-directory#cd-settings) di Cloud Directory nella GUI. Sia **Allow users to sign up to your app** che **Allow users to manage their account from your app** devono essere impostati su **On**.
2. Nella scheda **Password changed** del dashboard del servizio, imposta **Password changed email** su
3. Inserisci il seguente codice nella tua applicazione per passare la proprietà *show* a `WebAppStrategy.FORGOT_PASSWORD` per avviare il modulo dei dettagli della modifica.

  ```javascript
  app.get("/change_details", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_DETAILS
  }));
  ```
  {: codeblock}

</br>

### Modifica della password
{: #widget-nodejs-change-password}

1. Configura le tue [impostazioni](/docs/services/appid?topic=appid-cloud-directory#cd-settings) di Cloud Directory nella GUI. Sia **Allow users to sign up to your app** che **Allow users to manage their account from your app** devono essere impostati su **On**.
2. Nella scheda **Password changed** del dashboard del servizio, imposta **Password changed email** su
3. Inserisci il seguente codice nella tua applicazione per passare la proprietà *show* a `WebAppStrategy.FORGOT_PASSWORD` per avviare il modulo dei dettagli della modifica.

  ```javascript
  app.get("/change_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_PASSWORD
  }));
  ```
  {: codeblock}
