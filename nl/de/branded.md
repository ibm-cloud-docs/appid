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

# Anmeldeschnittstelle anpassen
{: #branding}

Sie können eigene angepasste Benutzerschnittstellen anzeigen und gleichzeitig die Authentifizierungs- und Berechtigungsfunktionen von {{site.data.keyword.appid_full}} nutzen. Mit Cloud Directory als Identitätsprovider können die Benutzer mit Ihren Apps interagieren und benötigen deutlich weniger Unterstützung durch Sie. Die Benutzer können sich anmelden, das Kennwort ändern und weitere Aktionen durchführen, ohne dass sie Unterstützung anfordern müssen.
{: shortdesc}

Wenn Sie Cloud Directory als Identitätsprovider einsetzen, wird der [Ablauf für Kennwortberechtigungsnachweise von Ressourceneignern](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html) verwendet, um Zugriffs- und Identitätstokens bereitzustellen.

**Hinweis**: Sie können nur dann angepasste Anmeldeseiten integrieren, wenn Cloud Directory die einzige konfigurierte Option ist. Sind weitere Identitätsprovider **aktiviert**, wird die vorkonfigurierte Anmeldeseite angezeigt.

## Angepasste Anzeigen mit dem Android-SDK aufrufen
{: #branded-ui-android}

Wenn Cloud Directory aktiviert ist, können Sie mit dem Android-SDK angepasste Anzeigen aufrufen. Sie können die gewünschte Kombination der Anzeigen auswählen, mit denen die Benutzer interagieren sollen. <a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="blank">Lesen Sie unseren Blog!<img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>
{: shortdesc}

</br>
**Anmelden**

1. **Cloud Directory** als Identitätsprovider **aktivieren**.
2. Den folgenden Befehl in den Code einfügen.
  ```java
  AppID.getInstance().obtainTokensWithROP(getApplicationContext(), username, password,
         new TokenResponseListener() {
         @Override
          public void onAuthorizationFailure (AuthorizationException exception) {
             //Ausnahmebedingung aufgetreten.
  			 }

          @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
            //Benutzer authentifiziert.
          }
         });
  ```
  {: codeblock}

</br>
**Anmeldung**

1. Für **Benutzern die Anmeldung und das Zurücksetzen ihres Kennworts ermöglichen** den Wert **Aktiv** in den Cloud Directory-Einstellungen festlegen.
2. Das Anmeldewidget aufrufen, um den Anmeldeablauf zu starten.
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
 			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
  			 if (accessToken != null && identityToken != null) {
  			 } else {
  			 }

  		 }
  	 });
  ```
  {: codeblock}

</br>
**Kennwort vergessen**

1. Für **Benutzern die Anmeldung und das Zurücksetzen ihres Kennworts ermöglichen** und **E-Mail für vergessenes Kennwort** den Wert **Aktiv** in den Cloud Directory-Einstellungen festlegen.
2. Das Anmeldewidget aufrufen, um den Ablauf beim Vergessen eines Kennworts zu starten.
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
**Kontodetails**

1. Für **Benutzern die Anmeldung und das Zurücksetzen ihres Kennworts ermöglichen** den Wert **Aktiv** in den Cloud Directory-Einstellungen festlegen.
2. Das Anmeldewidget aufrufen, um den Ablauf für das Ändern von Details zu starten.
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
**Kennwort ändern**

1. Für **Benutzern die Anmeldung und das Zurücksetzen ihres Kennworts ermöglichen** den Wert **Aktiv** in den Cloud Directory-Einstellungen festlegen.
2. Das Anmeldewidget aufrufen, um den Ablauf für das Ändern des Kennworts zu starten.
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

## Angepasste Anzeigen mit dem iOS Swift-SDK aufrufen
{: #branded-ui-ios-swift}

Wenn Cloud Directory aktiviert ist, können Sie mit dem ios Swift-SDK angepasste Anzeigen aufrufen. Sie können die gewünschte Kombination der Anzeigen auswählen, mit denen die Benutzer interagieren sollen.
{: shortdesc}

</br>
**Anmelden**

1. Auf der Registerkarte für den Identitätsprovider in der GUI den Wert **Aktiv** für Cloud Directory festlegen.
2. Mit dem Kennwort des Ressourceneigners anmelden. Sie können ein Zugriffs- und ein Identitätstoken abrufen, indem Sie den Benutzernamen und das Kennwort des Endbenutzers verwenden.
  ```swift
  class delegate : TokenResponseDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
      //Benutzer authentifiziert.
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
      //Ausnahmebedingung aufgetreten.
  			 }
  }

  AppID.sharedInstance.obtainTokensWithROP(username: username, password: password, delegate: delegate())
  ```
  {: codeblock}

</br>
**Anmeldung**

1. Für **Benutzern die Anmeldung und das Zurücksetzen ihres Kennworts ermöglichen** den Wert **Aktiv** in den Cloud Directory-Einstellungen festlegen.
2. Das Anmeldewidget aufrufen, um den Anmeldeablauf zu starten.
  ```swift
  class delegate : AuthorizationDelegate {
    public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
       if accessToken == nil && identityToken == nil {
        //E-Mail-Verifizierung erforderlich.
        return
       }
     //Benutzer authentifiziert.
    }

    public func onAuthorizationCanceled() {
        //Anmeldung vom Benutzer abgebrochen.
    }

    public func onAuthorizationFailure(error: AuthorizationError) {
        //Ausnahmebedingung aufgetreten.
  			 }
  }

  AppID.sharedInstance.loginWidget?.launchSignUp(delegate: delegate())
  ```
  {: codeblock}

</br>
**Kennwort vergessen**

1. Für **Benutzern die Anmeldung und das Zurücksetzen ihres Kennworts ermöglichen** und **E-Mail für vergessenes Kennwort** den Wert **Aktiv** in den Cloud Directory-Einstellungen festlegen.
2. Das Anmeldewidget aufrufen, um den Ablauf beim Vergessen eines Kennworts zu starten.
  ```swift
  class delegate : AuthorizationDelegate {
     public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
        //Aktion für vergessenes Kennwort beendet, in diesem Fall sind Zugriffstoken und Identitätstoken null.
     }

     public func onAuthorizationCanceled() {
         //Aktion für vergessenes Kennwort vom Benutzer abgebrochen.
     }

     public func onAuthorizationFailure(error: AuthorizationError) {
         //Ausnahmebedingung aufgetreten.
  			 }
  }

  AppID.sharedInstance.loginWidget?.launchForgotPassword(delegate: delegate())
  ```
  {: codeblock}

</br>
**Kontodetails**

1. Für **Benutzern die Anmeldung und das Zurücksetzen ihres Kennworts ermöglichen** den Wert **Aktiv** in den Cloud Directory-Einstellungen festlegen.
2. Das Anmeldewidget aufrufen, um den Ablauf für das Ändern von Details zu starten.
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
**Kennwort ändern**

1. Für **Benutzern die Anmeldung und das Zurücksetzen ihres Kennworts ermöglichen** den Wert **Aktiv** in den Cloud Directory-Einstellungen festlegen.
2. Das Anmeldewidget aufrufen, um den Ablauf für das Ändern des Kennworts zu starten.
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

## Angepasste Anzeigen mit dem Node.js-SDK aufrufen
{: #branded-ui-nodejs}

Wenn Cloud Directory aktiviert ist, können Sie mit dem Node.js-SDK angepasste Anzeigen aufrufen. Sie können die gewünschte Kombination der Anzeigen auswählen, mit denen die Benutzer interagieren sollen.
{: shortdesc}

**Anmelden**
1. In den Identitätsprovidereinstellungen den Wert **Aktiv** für Cloud Directory festlegen und einen Callback-Endpunkt angeben.
2. Eine POST-Route zu Ihrer App hinzufügen, die mit den Parametern für den Benutzernamen und das Kennwort aufgerufen werden kann, und mit dem Kennwort des Ressourceneigners anmelden.
    **Hinweis**: `WebAppStrategy` ermöglicht den Benutzern die Anmeldung bei Ihren Web-Apps mit einem Benutzernamen und einem Kennwort. Nach einer erfolgreichen Anmeldung wird das Zugriffstoken eines Benutzers in der HTTP-Sitzung gespeichert und ist für die Dauer der Sitzung verfügbar. Sobald die HTTP-Sitzung gelöscht wird oder abgelaufen ist, ist das Token nicht mehr gültig.
    ```javascript
    app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
    	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true // Flash-Nachrichten zulassen.
  }));
    ```
    {: codeblock}

</br>
**Anmeldung**

1. Für **Benutzern die Anmeldung und das Zurücksetzen ihres Kennworts ermöglichen** den Wert **Aktiv** in den Cloud Directory-Einstellungen festlegen. Wird diese Einstellung nicht aktiviert, wird der Prozess beendet, ohne dass Zugriffs- und Identitätstokens abgerufen werden.
2. Die WebAppStrategy-Eigenschaft `show` übergeben und `WebAppStrategy.SIGN_UP` dafür festlegen.
  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: codeblock}

</br>
**Kennwort vergessen**

1. Für **Benutzern die Anmeldung und das Zurücksetzen ihres Kennworts ermöglichen** und **E-Mail für vergessenes Kennwort** den Wert **Aktiv** in den Cloud Directory-Einstellungen festlegen. Wird diese Einstellung nicht aktiviert, wird der Prozess beendet, ohne dass Zugriffs- und Identitätstokens abgerufen werden.
2. Die WebAppStrategy-Eigenschaft `show` übergeben und `WebAppStrategy.FORGOT_PASSWORD` dafür festlegen.
  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: codeblock}

</br>
**Kontodetails**
1. Für **Benutzern die Anmeldung und das Zurücksetzen ihres Kennworts ermöglichen** den Wert **Aktiv** in den Cloud Directory-Einstellungen festlegen.
2. Die WebAppStrategy-Eigenschaft `show` übergeben und `WebAppStrategy.CHANGE_DETAILS` dafür festlegen.
  ```javascript
  app.get("/change_details", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_DETAILS
  }));
  ```
  {: codeblock}

</br>
**Kennwort ändern**
1. Für **Benutzern die Anmeldung und das Zurücksetzen ihres Kennworts ermöglichen** den Wert **Aktiv** in den Cloud Directory-Einstellungen festlegen. 
2. Die WebAppStrategy-Eigenschaft `show` übergeben und `WebAppStrategy.CHANGE_PASSWORD` dafür festlegen.
  ```javascript
  app.get("/change_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_PASSWORD
  }));
  ```
  {: codeblock}
