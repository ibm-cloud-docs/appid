---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:tip: .tip}

# Personalizzazione dell'esperienza di accesso
{: #branding}

Puoi visualizzare le tue proprie schermate personalizzate e sfruttare le funzionalità di autenticazione e autorizzazione di {{site.data.keyword.appid_full}}. Con Cloud Directory come tuo provider di identità, i tuoi utenti potranno interagire con la tua applicazione con meno aiuto da parte tua. Saranno in grado di accedere senza chiedere assistenza.
{: shortdesc}

Quando utilizzi le tue proprie schermate, viene utilizzato il [flusso Resource Owner Password Credentials](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html) per fornire i token di accesso e identità.


## Visualizzazione delle schermate personalizzate con l'SDK Android
{: #branded-ui-android}

Con Cloud Directory abilitato, puoi richiamare le schermate personalizzate con l'SDK Android.  <a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="blank">Consulta questo blog! <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>
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
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
            //Utente autenticato
        }
         });
  ```
  {: pre}

</br>
</br>

## Visualizzazione delle schermate personalizzate con l'SDK iOS Swift
{: #branded-ui-ios-swift}

Con Cloud Directory abilitato, puoi richiamare le schermate personalizzate con l'SDK iOS Swift.
{: shortdesc}

</br>
**Accedi**

1. Nella scheda del provider di identità nella GUI, imposta Cloud Directory su **On**.
2. Accedi utilizzando la password del proprietario della risorsa. I token di accesso e identità vengono ottenuti quando un utente tenta di accedere utilizzando i propri nome utente e password.
  ```swift
  class delegate : TokenResponseDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
      //Utente autenticato
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
      //Si è verificata un'eccezione
      }
  }

  AppID.sharedInstance.obtainTokensWithROP(username: username, password: password, delegate: delegate())
  ```
  {: pre}


</br>
</br>

## Visualizzazione delle schermate personalizzate con l'SDK Node.js
{: #branded-ui-nodejs}

Con Cloud Directory abilitato, puoi richiamare le schermate personalizzate con l'SDK Node.js.
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

