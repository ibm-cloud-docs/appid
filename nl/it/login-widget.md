---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-09"

keywords: Authentication, authorization, identity, app security, secure, development, sign in, sign up, password, social, enterprise

subcollection: appid

---

{:external: target="_blank" .external}
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


# Utilizzo del widget di accesso
{: #login-widget}

Con {{site.data.keyword.appid_full}} puoi utilizzare un'IU predefinita, denominata widget di accesso, per consentire agli utenti di scegliete il provider di identità con cui vogliono accedere. Se stai utilizzando Cloud Directory, il widget di accesso fornisce anche ulteriori IU per funzionalità extra come registrazione, password dimenticata, autenticazione multifattore e altro.
{: shortdesc}


## Descrizione del widget di accesso
{: #widget-understanding}

Una delle parti migliori del widget di accesso è che puoi iniziare ad utilizzare {{site.data.keyword.appid_short_notm}} prima di implementare una qualsiasi delle tue IU di autenticazione - il che rende l'esperienza di onboarding degli sviluppatori molto più semplice.

### Qual è il comportamento predefinito del widget di accesso?
{: #widget-default}

Per impostazione predefinita, il widget di accesso può utilizzare Facebook, Google e Cloud Directory. Puoi modificare il comportamento in qualsiasi momento scegliendo quali provider di identità vuoi configurare come opzione di scelta. Quando viene abilitato più di un provider di identità, il widget di accesso visualizza una schermata in cui l'utente può selezionare il proprio provider di identità. Ma, se hai abilitato un solo provider di identità, l'utente non visualizza la suddetta schermata di selezione. Vengono indirizzati direttamente al provider di identità per iniziare il processo di accesso.

Ad esempio, se stai utilizzando i valori predefiniti - Facebook, Google e Cloud Directory - gli utenti visualizzano la schermata. Se hai abilitato solo Facebook, gli utenti vengono indirizzati direttamente a Facebook per l'autenticazione.



### Quali schermate possono essere visualizzate per ogni provider?
{: #widget-options}

Quando utilizzi Cloud Directory, {{site.data.keyword.appid_short_notm}} può fornirti una funzionalità estesa della gestione utenti. La funzionalità estesa si applica anche alle funzionalità del widget di accesso. Gli utenti che vengono archiviati in Cloud Directory possono avvalersi di funzionalità come registrazione e reimpostazione della propria password direttamente nel widget di accesso. Controlla la seguente tabella per vedere quali schermate puoi visualizzare per ciascun tipo di provider di identità.

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


## Personalizzazione del widget di accesso
{: #widget-customize}

Il widget di accesso è dinamico. Puoi personalizzare l'aspetto o la configurazione del provider di identità e tali modifiche vengono applicate immediatamente. Non devi aggiornare il tuo codice applicazione o ridistribuire la tua applicazione in alcun modo.
{: shortdesc}

Ti serve una maggiore personalizzazione rispetto a quella fornita dal widget di accesso? Puoi implementare la tua IU completamente personalizzabile per la registrazione, l'accesso, il ripristino della password o altri flussi dell'utente per creare un'esperienza unica per la tua applicazione. Per iniziare, consulta [personalizzazione della tua applicazione](/docs/services/appid?topic=appid-branded).
{: tip}

Per personalizzare la schermata:

1. Apri il dashboard del servizio {{site.data.keyword.appid_short_notm}}.
2. Seleziona la sezione **Login Customization**. Puoi modificare l'aspetto del widget di accesso per allinearlo al marchio della tua azienda.
3. Carica il tuo logo aziendale selezionando un file PNG o JPG dal tuo sistema locale. La dimensione dell'immagine raccomandata è 320 x 320 pixel. La dimensione del file massima è 100 Kb.
4. Seleziona un colore di intestazione per il widget dal selezionatore del colore o immetti il codice esadecimale per un altro colore.
5. Controlla il pannello dell'anteprima e fai clic su **Save Changes** quando sei soddisfatto delle tue personalizzazioni. Viene visualizzato un messaggio di conferma.
6. Nel tuo browser, aggiorna la pagina di accesso per verificare le tue modifiche.


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
  {: codeblock}

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
