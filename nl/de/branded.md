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

# App-Branding
{: #branding}

Sie können eigene angepasste Anzeigen anzeigen und die Authentifizierungs- und Berechtigungsfunktionen von {{site.data.keyword.appid_full}} nutzen. Mit Cloud Directory als Identitätsprovider können die Benutzer mit Ihren Apps interagieren und benötigen deutlich weniger Unterstützung durch Sie. Die Benutzer können sich anmelden, sich registrieren, das Kennwort ändern und weitere Aktionen durchführen, ohne dass sie Unterstützung anfordern müssen.
{: shortdesc}

Wenn Sie Ihre eigenen Anzeigen verwenden, wird der [Ablauf für Kennwortberechtigungsnachweise von Ressourceneignern](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html) verwendet, um Zugriffs- und Identitätstoken bereitzustellen.


## Branding der App mit dem iOS-Swift-SDK
{: #branded-ui-ios-swift}

Wenn Cloud Directory aktiviert ist, können Sie mit dem iOS Swift-SDK eigene, an das Brand-Marketing Ihres Unternehmens angepasste Anzeigen aufrufen.
{: shortdesc}

</br>
**Anmelden**

1. Legen Sie auf der Registerkarte für Identitätsprovider in der GUI den Wert **Ein** für Cloud Directory fest. 
2. Rufen Sie das Anmeldewidget auf, um den Verarbeitungsablauf für die Anmeldung zu starten. Zugriffs- und Identitätstoken werden abgerufen, wenn ein Benutzer versucht, sich mit seinem Benutzernamen bzw. einer E-Mail-Adresse und einem Kennwort anzumelden. 
  ```swift
  class delegate : TokenResponseDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
      // Benutzer authentifiziert.
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
      // Ausnahmebedingung aufgetreten.
  			 }
  }

  AppID.sharedInstance.signinWithResourceOwnerPassword(username: username, password: password, delegate: delegate())
  ```
  {: pre}

</br>

**Registrieren**

1. Legen Sie auf der Registerkarte für Identitätsprovider in der GUI den Wert **Ein** für Cloud Directory fest. 
2. Legen Sie für **Benutzern die Registrierung und das Zurücksetzen ihres Kennworts ermöglichen** den Wert **Ein** in den Cloud Directory-Einstellungen fest. 
3. Rufen Sie das Anmeldewidget auf, um den Registrierungsablauf zu starten. 
  ```swift
  class delegate : AuthorizationDelegate {
    public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
       if accessToken == nil && identityToken == nil {
        // E-Mail-Verifizierung erforderlich.
        return
       }
     // Benutzer authentifiziert.
    }

    public func onAuthorizationCanceled() {
        // Registrierung vom Benutzer abgebrochen.
    }

    public func onAuthorizationFailure(error: AuthorizationError) {
        // Ausnahmebedingung aufgetreten.
  		}
  }

  AppID.sharedInstance.loginWidget?.launchSignUp(delegate: delegate())
  ```
  {: pre}

</br>

**Kennwort vergessen**

1. Legen Sie auf der Registerkarte für Identitätsprovider in der GUI den Wert **Ein** für Cloud Directory fest. 
2. Legen Sie für **Benutzern die Registrierung und das Zurücksetzen ihres Kennworts ermöglichen** den Wert **Ein** in den Cloud Directory-Einstellungen fest. 
3. Rufen Sie das Anmeldewidget auf, um den Verarbeitungsablauf für vergessene Kennwörter zu starten. 
  ```swift
  class delegate : AuthorizationDelegate {
     public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
        // Aktion für vergessenes Kennwort beendet, in diesem Fall sind Zugriffstoken und Identitätstoken null.
     }

     public func onAuthorizationCanceled() {
         // Aktion für vergessenes Kennwort vom Benutzer abgebrochen.
     }

     public func onAuthorizationFailure(error: AuthorizationError) {
         // Ausnahmebedingung aufgetreten.
  		 }
  }

  AppID.sharedInstance.loginWidget?.launchForgotPassword(delegate: delegate())
  ```
  {: pre}

</br>

**Details ändern**

1. Legen Sie auf der Registerkarte für Identitätsprovider in der GUI den Wert **Ein** für Cloud Directory fest. 
2. Legen Sie für **Benutzern die Registrierung und das Zurücksetzen ihres Kennworts ermöglichen** den Wert **Ein** in den Cloud Directory-Einstellungen fest. 
3. Rufen Sie das Anmeldewidget auf, um den Verarbeitungsablauf für das Ändern von Details zu starten. 
  ```swift
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
         // Benutzer authentifiziert, neue Token erhalten.
      }

      public func onAuthorizationCanceled() {
          // Aktion für Detailänderung vom Benutzer abgebrochen.
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          // Ausnahmebedingung aufgetreten.
  			 }
  }

   AppID.sharedInstance.loginWidget?.launchChangeDetails(delegate: delegate())
  ```
  {: pre}

</br>

**Kennwort ändern**

1. Legen Sie auf der Registerkarte für Identitätsprovider in der GUI den Wert **Ein** für Cloud Directory fest. 
2. Legen Sie für **Benutzern die Registrierung und das Zurücksetzen ihres Kennworts ermöglichen** den Wert **Ein** in den Cloud Directory-Einstellungen fest. 
3. Rufen Sie das Anmeldewidget auf, um den Verarbeitungsablauf für das Ändern von Details zu starten. 
  ```swift
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
          // Benutzer authentifiziert, neue Token erhalten.
      }

      public func onAuthorizationCanceled() {
          // Kennwortänderung vom Benutzer abgebrochen.
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
           // Ausnahmebedingung aufgetreten.
  			 }
   }

   AppID.sharedInstance.loginWidget?.launchChangePassword(delegate: delegate())
  ```
  {: pre}

</br>


## Branding der App mit dem Android-SDK
{: #branded-ui-android}

Wenn Cloud Directory aktiviert ist, können Sie mit dem Android-SDK angepasste Anzeigen aufrufen. Sie können die gewünschte Kombination der Anzeigen auswählen, mit denen die Benutzer interagieren sollen. <a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="blank">Lesen in diesem Blog <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> ein ausführliches Beispiel dazu!
{: shortdesc}

</br>

**Anmelden**

1. **Cloud Directory** als Identitätsprovider aktivieren (**Ein**).
2. Rufen Sie Zugriffs-, Identitäts- und Aktualisierungstoken ab, indem Sie Name und Kennwort des Endbenutzers übergeben. 
3. Rufen Sie das Anmeldewidget auf, um den Verarbeitungsablauf für die Anmeldung zu starten. 
  ```java
  AppID.getInstance().signinWithResourceOwnerPassword(getApplicationContext(), username, password, new TokenResponseListener() {
      @Override
      public void onAuthorizationFailure (AuthorizationException exception) {
          // Ausnahmebedingung aufgetreten.
  			 }

      @Override
      public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          // Benutzer authentifiziert.
          }
  });
  ```
  {: pre}

</br>

**Registrieren**

1. **Cloud Directory** als Identitätsprovider aktivieren (**Ein**).
2. Legen Sie für **Benutzern die Registrierung und das Zurücksetzen ihres Kennworts ermöglichen** den Wert **Ein** in den Cloud Directory-Einstellungen fest. 
3. Rufen Sie das Anmeldewidget auf, um den Registrierungsablauf zu starten. 
  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launchSignUp(this, new AuthorizationListener() {
      @Override
      public void onAuthorizationFailure (AuthorizationException exception) {
          // Ausnahmebedingung aufgetreten.
  			 }

      @Override
      public void onAuthorizationCanceled () {
          // Registrierung vom Benutzer abgebrochen
      }

      @Override
      public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          if (accessToken != null && identityToken != null) {
              // Benutzer authentifiziert.
          } else {
              // E-Mail-Verifizierung erforderlich.
          }
      }
  });
  ```
  {: pre}

</br>


**Kennwort vergessen**

1. **Cloud Directory** als Identitätsprovider aktivieren (**Ein**).
2. Legen Sie für **Benutzern die Registrierung und das Zurücksetzen ihres Kennworts ermöglichen** den Wert **Ein** in den Cloud Directory-Einstellungen fest. 
3. Rufen Sie das Anmeldewidget auf, um den Verarbeitungsablauf für vergessene Kennwörter zu starten. 
  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launchForgotPassword(this, new AuthorizationListener() {
      @Override
   	public void onAuthorizationFailure (AuthorizationException exception) {
          // Ausnahmebedingung aufgetreten.
  			 }

      @Override
      public void onAuthorizationCanceled () {
          // Aktion für vergessenes Kennwort vom Benutzer abgebrochen.  			
      }

      @Override
      public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          // Aktion für vergessenes Kennwort beendet, in diesem Fall sind Zugriffstoken und Identitätstoken null.
      }
  });
  ```
  {: pre}

</br>

**Details ändern**

1. **Cloud Directory** als Identitätsprovider aktivieren (**Ein**).
2. Legen Sie für **Benutzern die Registrierung und das Zurücksetzen ihres Kennworts ermöglichen** den Wert **Ein** in den Cloud Directory-Einstellungen fest. 
3. Rufen Sie das Anmeldewidget auf, um den Verarbeitungsablauf für das Ändern von Details zu starten. 
  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launchChangeDetails(this, new AuthorizationListener() {
      @Override
      public void onAuthorizationFailure (AuthorizationException exception) {
          // Ausnahmebedingung aufgetreten.
  			 }

      @Override
      public void onAuthorizationCanceled () {
          // Aktion für Detailänderung vom Benutzer abgebrochen.  			
      }

      @Override
      public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          // Benutzer authentifiziert, neue Token erhalten.
  			 }
  });
  ```
  {: pre}


</br>

**Kennwort ändern**

1. **Cloud Directory** als Identitätsprovider aktivieren (**Ein**).
2. Legen Sie für **Benutzern die Registrierung und das Zurücksetzen ihres Kennworts ermöglichen** den Wert **Ein** in den Cloud Directory-Einstellungen fest. 
3. Rufen Sie das Anmeldewidget auf, um den Verarbeitungsablauf für Kennwortänderung zu starten. 
  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launchChangePassword(this, new AuthorizationListener() {
      @Override
      public void onAuthorizationFailure (AuthorizationException exception) {
          // Ausnahmebedingung aufgetreten.
  			 }

      @Override
      public void onAuthorizationCanceled () {
          // Aktion für Kennwortänderung vom Benutzer abgebrochen.  			
      }

      @Override
      public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          // Benutzer authentifiziert, neue Token erhalten.
  			 }
  });
  ```
  {: pre}

</br>
</br>


## Branding der App mit dem Node.js-SDK
{: #branded-ui-nodejs}

Wenn Cloud Directory aktiviert ist, können Sie mit dem Node.js-SDK angepasste Anzeigen aufrufen.
{: shortdesc}

**Anmeldung**

Mithilfe von WebAppStrategy können Benutzer sich bei Ihren Web-Apps mit ihrem Benutzernamen und einem Kennwort anmelden. Nach der Anmeldung bei der App bleibt das Zugriffstoken der Benutzer in einer HTTP-Sitzung erhalten, bis die Sitzung endet. Nach dem Beenden oder Ablaufen der HTTP-Sitzung wird auch das Zugriffstoken gelöscht. 

1. Legen Sie in den Identitätsprovidereinstellungen den Wert **Ein** für Cloud Directory fest und geben Sie einen Callback-Endpunkt an. 
2. Fügen Sie eine POST-Route zu Ihrer App hinzu, die mit den Parametern für den Benutzernamen und das Kennwort aufgerufen werden kann, und melden Sie sich entsprechend dem für Ressourceneigner vorgesehenen Kennwortablauf an. 
  ```javascript
  app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true // Flash-Nachrichten zulassen.
  }));
  ```
  {: pre}
  <table>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="Symbol für weitere Informationen"/> Befehlsparameter</th>
    </thead>
    <tbody>
      <tr>
        <td><code>successRedirect</code></td>
        <td>Die URL, an die der Benutzer nach einer erfolgreichen Authentifizierung weitergeleitet werden soll. </td>
      </tr>
      <tr>
        <td><code>failureRedirect</code></td>
        <td>Die URL, an die der Benutzer weitergeleitet werden soll, wenn die Authentifizierung fehlschlägt. </td>
      </tr>
      <tr>
        <td><code>failureFlash</code></td>
        <td>Bei Angabe von <code>true</code> wird eine Fehlernachricht vom Cloud Directory-Service zurückgegeben. Standardwert: <code>false</code>. </td>
      </tr>
    </tbody>
  </table>

  1. Wenn Sie die Anforderung in einem HTML-Formular übergeben, können Sie die Middleware [body parser](https://www.npmjs.com/package/body-parser) verwenden. 
  2. Zum Abrufen der zurückgegebenen Fehlernachricht eignet sich [connect-flash](https://www.npmjs.com/package/connect-flash). Weitere Informationen finden Sie im Abschnitt zum [Beispiel für eine Web-App](https://github.com/ibm-cloud-security/appid-serversdk-nodejs/blob/master/samples/web-app-sample.js). {: tip}

</br>
**Registrierung**

1. Legen Sie in den Identitätsprovidereinstellungen den Wert **Ein** für Cloud Directory fest und geben Sie einen Callback-Endpunkt an. 
2. Legen Sie für **Benutzern die Registrierung und das Zurücksetzen ihres Kennworts ermöglichen** den Wert **Ein** in den Cloud Directory-Einstellungen fest. 
3. Legen Sie für **Benutzern Anmeldung ohne E-Mail-Verifizierung ermöglichen** den Wert **Nein** fest. Andernfalls können die Zugriffs- und Identitätstoken von {{site.data.keyword.appid_short_notm}} nicht abgerufen werden. 
4. Fügen Sie eine POST-Route zu Ihrer App hinzu, die mit den Parametern für den Benutzernamen und das Kennwort aufgerufen werden kann, und melden Sie sich entsprechend dem für Ressourceneigner vorgesehenen Kennwortablauf an. 
  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: pre}

</br>

**Kennwort vergessen**

1. Legen Sie in den Identitätsprovidereinstellungen den Wert **Ein** für Cloud Directory fest und geben Sie einen Callback-Endpunkt an. 
2. Legen Sie für **Benutzern die Registrierung und das Zurücksetzen ihres Kennworts ermöglichen** den Wert **Ein** in den Cloud Directory-Einstellungen fest. 
3. Legen Sie für **E-Mail für vergessenes Kennwort** den Wert **Ein** fest. 
4. Übergeben Sie die Eigenschaft *show* an `WebAppStrategy.FORGOT_PASSWORD`, um das Formular für ein vergessenes Kennwort aufzurufen. 
  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: pre}

</br>

**Details ändern**

1. Legen Sie in den Identitätsprovidereinstellungen den Wert **Ein** für Cloud Directory fest und geben Sie einen Callback-Endpunkt an. 
2. Legen Sie für **Benutzern die Registrierung und das Zurücksetzen ihres Kennworts ermöglichen** den Wert **Ein** in den Cloud Directory-Einstellungen fest. 
3. Stellen Sie sicher, dass eine Authentifizierung des Benutzers mit {{site.data.keyword.appid_short_notm}} erfolgt ist. 
4. Übergeben Sie die Eigenschaft *show* an `WebAppStrategy.CHANGE_DETAILS`, um das entsprechende Formular aufzurufen. 
  ```javascript
  app.get("/change_details", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_DETAILS
  }));
  ```
  {: pre}

</br>

## Branding der App mit der API
{: #branded-ui-api}

Sie können eigene angepasste Anzeigen anzeigen und die Authentifizierungs- und Berechtigungsfunktionen von {{site.data.keyword.appid_short_notm}} nutzen. Mit Cloud Directory als Identitätsprovider können die Benutzer mit Ihren Apps interagieren und benötigen deutlich weniger Unterstützung durch Sie. Die Benutzer können sich anmelden, sich registrieren, das Kennwort zurücksetzen und weitere Aktionen durchführen, ohne dass sie Unterstützung anfordern müssen.
{: shortdesc}

Um dies zu ermöglichen, stellt {{site.data.keyword.appid_short_notm}} die REST-APIs zur Verfügung. Sie können die REST-API verwenden, um einen Back-End-Server zu erstellen, der Ihren Web-Apps dient oder um mit einer mobilen App mit Ihren angepassten Anzeigen zu interagieren.

Die Verwaltungs-API wird mit Token geschützt, die von IBM Cloud Identity and Access Management generiert wurden. Das heißt, dass Kontoeigner angeben können, wer in ihrem Team über welche Zugriffsebene für die jeweilige Serviceinstanz verfügen soll. Weitere Informationen dazu, wie IAM und {{site.data.keyword.appid_short_notm}} zusammenarbeiten, finden Sie in [Servicezugriffsverwaltung](/docs/services/appid/iam.html).

Nach der Konfiguration der [Einstellungen](/docs/services/appid/cloud-directory.html) können Sie die folgenden Endpunkte aufrufen, um die einzelnen Anzeigen anzuzeigen. 


**Registrierung**
Mit dem Endpunkt `/sign_up` können Sie es Benutzern ermöglichen, sich bei Ihrer App zu registrieren.
Übergeben Sie die folgenden Daten im Anforderungshauptteil: 
  * Ihre Tenant-ID (tenantID).
  * Benutzerdaten des Cloudverzeichnisses. Weitere Details finden Sie in [SCIM Full User Representation](https://tools.ietf.org/html/rfc7643#section-8.2).
    * Ein Kennwortattribut `password`.
    * Im E-Mail-Bereich, bei dem für das primäre Attribut (`primary`) der Wert `true` festgelegt ist, müssen Sie über mindestens eine E-Mail-Adresse verfügen.

Abhängig von Ihren [E-Mail-Konfigurationen](/docs/services/appid/cloud-directory.html) erhält ein Benutzer möglicherweise die Anforderung für die Verifizierung oder eine Willkommens-E-Mail, wenn er sich für Ihre App registriert. Beide Typen von E-Mails werden ausgelöst, wenn ein Benutzer sich für Ihre App registriert. Die Verifizierungs-E-Mail enthält die Schaltfläche **Verifizieren**. Nach dem die Benutzer auf diese Schaltfläche geklickt und Ihre Identität bestätigt haben, wird von {{site.data.keyword.appid_short_notm}} eine Anzeige angezeigt, in der für die Verifizierung gedankt wird.  

Sie können eine eigene Seite angeben, die nach der Verifizierung angezeigt werden soll:

1. Navigieren Sie zu der Registerkarte für **Angepasste Landing-Pages** des {{site.data.keyword.appid_short_notm}}-Dashboards
2. Geben Sie die URL Ihrer Landing-Page im Feld für die **URL Ihrer angepassten Prüfseite für E-Mail-Adressen** ein.

Wenn dieser Wert bereitgestellt ist, ruft {{site.data.keyword.appid_short_notm}} die URL zusammen mit einer `Kontext`abfrage auf. Wenn Sie den Endpunkt `/sign_up/confirmation_result` aufrufen und die empfangenen `Kontext`parameter übergeben, können Sie im Ergebnis sehen, ob Ihr Benutzer das Konto verifiziert hat. Wurde das Konto verifiziert, können Sie jetzt Ihre angepasste Seite anzeigen.

</br>
**Kennwort vergessen**

Sie können den Endpunkt `/forgot_password` verwenden, um Benutzern zu ermöglichen, Ihr Kennwort wiederherzustellen, falls Sie es vergessen haben sollten.

Übergeben Sie die folgenden Daten im Anforderungshauptteil: 
  * Ihre Tenant-ID (tenantID)
  * Die E-Mail des Cloudverzeichnisbenutzers

Wenn der Endpunkt aufgerufen wird, wird die E-Mail zum Zurücksetzen des Kennworts an den Benutzer gesendet. Die E-Mail enthält die Schaltfläche **Zurücksetzen**. Nachdem die Benutzer auf diese Schaltfläche geklickt haben, wird von {{site.data.keyword.appid_short_notm}} eine Anzeige angezeigt, in der sie ihr Kennwort zurücksetzen können.

Sie können eine eigene Seite angeben, die nach dem Zurücksetzen des Kennworts angezeigt werden soll:

1. Navigieren Sie zu der Registerkarte für **Angepasste Landing-Pages** des {{site.data.keyword.appid_short_notm}}-Dashboards
2. Geben Sie die URL für Ihre Landing-Page im Feld für die **URL für die angepasste Seite zum Zurücksetzen des Kennworts** ein.  

Wenn dieser Wert bereitgestellt ist, ruft {{site.data.keyword.appid_short_notm}} die URL zusammen mit einer `Kontext`abfrage auf. Der `Kontext`parameter wird verwendet, um das Ergebnis zu empfangen, wenn `/forgot_password/confirmation_result` aufgerufen wird. Falls das Ergebnis erfolgreich war, können Sie Ihre angepasste Seite anzeigen.

Fügen Sie eine zufällige Zeichenfolge zur angepassten Seite für das Zurücksetzen des Kennworts hinzu und übergeben Sie sie an Ihr Back-End, wenn die Anforderung übergeben wird. Lassen Sie Ihren Handler die Zeichenfolge überprüfen und den Endpunkt `/change_password` nur dann aufrufen, wenn die Zeichenfolge gültig ist. Auf diese Weise, können Sie die Verletzlichkeit Ihres Back-End-Endpunkts zum Zurücksetzen des Kennworts verringern.
{: tip}

</br>
**Kennwort ändern**

Sie können den Endpunkt `/change_password` auf zwei Weisen verwenden. Wenn ein Benutzer eine Anforderung zum Zurücksetzen übergibt oder wenn ein Benutzer sich bei Ihrer App anmeldet und sein Kennwort aktualisieren möchte.

Übergeben Sie die folgenden Daten im Anforderungshauptteil, um das zugehörige Kennwort nach einer Anforderung zum Zurücksetzen zu aktualisieren: 
  * Ihre Tenant-ID (tenantID)
  * Das neue Kennwort des Benutzers
  * Die Cloudverzeichnisbenutzer-UUID
  * Optional: Die IP-Adresse, von der die Anforderung zum Zurücksetzen des Kennworts ausgeführt wurde. Wenn Sie auswählen, dass die IP-Adresse übergeben wird, dann ist der Platzhalter `%{passwordChangeInfo.ipAddress}` für die E-Mail-Vorlage zum Ändern des Kennworts verfügbar.

Abhängig von Ihrer Konfiguration sendet {{site.data.keyword.appid_short_notm}} beim Ändern des Kennworts möglicherweise eine E-Mail an den Benutzer und lässt diesen wissen, dass eine Änderung vorgenommen wurde.

</br>
Gehen Sie wie folgt vor, um Benutzern das Ändern ihres Kennworts zu ermöglichen, während sie sich bei Ihrer App anmelden:

Übergeben Sie die folgenden Daten im Anforderungshauptteil: 
  * Ihre Tenant-ID (tenantID)
  * Das neue Kennwort des Benutzers
  * Die Cloudverzeichnisbenutzer-UUID

Ihre Seite zum Ändern des Kennworts sollte den Benutzer auffordern, sein aktuelles Kennwort und sein neues Kennwort einzugeben.
{: tip}

Ihr Back-End validiert das aktuelle Kennwort des Benutzers mit der ROP-API und falls dieses gültig ist, wird der Endpunkt mit dem neuen Kennwort aufgerufen. Abhängig von Ihrer Konfiguration sendet {{site.data.keyword.appid_short_notm}} beim Ändern des Kennworts möglicherweise eine E-Mail an den Benutzer und lässt diesen wissen, dass eine Änderung vorgenommen wurde.

</br>
**Erneut senden**

Sie können den Endpunkt `/resend/{templateName}` verwenden, um eine E-Mail erneut zu senden, wenn ein Benutzer die E-Mail nicht erhalten haben sollte. 

Übergeben Sie die folgenden Daten im Anforderungshauptteil: 
  * Die Tenant-ID (tenantID)
  * Den Vorlagennamen
  * Die Cloudverzeichnisbenutzer-UUID


**Details ändern**

Wenn ein Benutzer bei Ihrer App angemeldet ist, kann er einige seiner Daten aktualisieren. Sie können `/Users/{userId}` verwenden, um seine Daten abzurufen und zu aktualisieren.

Wenn die Benutzerdetails aktualisiert werden, ruft der Endpunkt die aktualisierten Benutzerdaten im Anforderungshauptteil im [SCIM-Format](https://tools.ietf.org/html/rfc7643#section-8.2) ab. Stellen Sie sicher, dass Sie nur die relevanten Details ändern.

Die E-Mail-Adresse kann nicht geändert werden.
{: tip}
