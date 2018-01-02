---

copyright:
  years: 2017
lastupdated: "2017-12-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Cloud Directory verwalten
{: #cd}

Sie können {{site.data.keyword.appid_short_notm}} so konfigurieren, dass Cloud Directory als Identitätsprovider verwendet wird. Wenn sich Benutzer mit ihrer E-Mail-Adresse und einem Kennwort anmelden, werden sie zu Ihrem Verzeichnis hinzugefügt und Sie können die Benutzer über die grafische Benutzerschnittstelle des Service verwalten.
{: shortdesc}

<!--- What is a cloud directory? --->

## Verzeichniseinstellungen verwalten

Sie können die Benachrichtigungen und den Grad der Benutzersteuerung für Ihre App konfigurieren. Auf der Registerkarte **Verzeichniseinstellungen** der grafischen Benutzerschnittstelle können Sie festlegen, in welchem Umfang die Benutzer Self-Service-Operationen vornehmen können.

1. Wenn Sie zulassen möchten, dass sich Benutzer mit einer E-Mail-Adresse anmelden können, müssen Sie für die Option **Benutzern die Anmeldung und das Zurücksetzen ihres Kennworts ermöglichen** die Einstellung **Ein** festlegen. Wenn für die Option der Wert **Aus** festgelegt ist, können Sie dennoch Benutzer über die Konsole hinzufügen, jedoch nur zu Entwicklungszwecken.
2. Konfigurieren Sie die Absenderdetails. Geben Sie die E-Mail-Adresse an, von der aus die Nachrichten gesendet werden sollen, die als Absender angezeigt wird und an die Benutzer Antworten senden können. **Hinweis**: Stellen Sie beim Konfigurieren der Aktions-URL sicher, dass der festgelegte Zeitraum für das Klicken auf den Link ausreicht. Ein Benutzer muss seine E-Mail-Adresse verifizieren, damit ihm bestimmte Optionen zur Verfügung stehen, wie z. B. die Möglichkeit, das Zurücksetzen des Kennworts anzufordern.
3. Bestimmen Sie die E-Mail-Typen, die ein Benutzer erhält, sowie die Absenderinformationen.



## Nachrichten verwalten

Eine Vorlage ist ein Beispiel für eine E-Mail-Nachricht, die Sie an die Benutzer senden können. Sie können die Vorlage anpassen, indem Sie den Inhalt und das Layout der Nachricht aktualisieren. Sie können für diese Nachrichten die Einstellung **Ein** oder **Aus** auf der Registerkarte mit den Verzeichniseinstellungen festlegen.

1. Wählen Sie einen **Nachrichtentyp** aus.
2. Passen Sie die Nachricht an, indem Sie den Inhalt und das Design der Nachricht ändern. Sie können Parameter verwenden, um die Nachrichten zu personalisieren. Denken Sie daran, die Änderungen zu speichern!

### Nachrichtentypen

<dl>
  <dt> Begrüßung</dt>
    <dd>Sie können einen Benutzer per E-Mail bei Ihrer Anwendung begrüßen, nachdem dieser eine Registrierung durchgeführt hat. Gestalten Sie die Nachrichten so attraktiv wie möglich, um die Benutzer zu begrüßen und zu binden.<table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> Parameter, die in jedem beliebigen Nachrichtentyp verwendet werden können</th>
      </thead>
      <tbody>
        <tr>
          <td> %{display.logo} </td>
          <td> Zeigt das Bild an, das Sie für das Anmeldewidget konfiguriert haben. </td>
        </tr>
	 <tr>
          <td> %{display.headerColor} </td>
          <td> Zeigt die Headerfarbe an, das Sie für das Anmeldewidget konfiguriert haben. </td>
        </tr>
        <tr>
          <td> %{user.displayName} </td>
          <td> Zeigt den Anzeigenamen an, den ein Benutzer für die Interaktion mit der App ausgewählt hat. </td>
        </tr>
        <tr>
          <td> %{user.email} </td>
          <td> Zeigt die registrierte E-Mail-Adresse des Benutzers an. </td>
        </tr>
        <tr>
          <td> %{user.firstName} </td>
          <td> Zeigt den angegebenen Vornamen des Benutzers an. </td>
        </tr>
        <tr>
          <td> %{user.formattedName} </td>
          <td> Zeigt den vollständigen Namen des Benutzers an. </td>
        </tr>
        <tr>
          <td> %{user.lastName} </td>
          <td> Zeigt den angegebenen Nachnamen des Benutzers an. </td>
        </tr>
      </tbody>
    </table>

    **Hinweis**: Wenn ein Benutzer die vom Parameter abgefragte Information nicht angibt, wird im entsprechenden Feld kein Wert angezeigt. </dd>
  <dt> Kennwort vergessen</dt>
    <dd> Wenn ein Benutzer das Kennwort vergisst oder es aus einem anderen Grund aktualisieren möchte, kann er ein Zurücksetzen des Kennworts anfordern. Sie können die E-Mail-Antwort auf diese Anforderung anpassen. Wenn ein Benutzer eine Änderung anfordert, wird das Kennwort erst geändert, wenn er auf den Link in dieser E-Mail klickt.

    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> Parameter für Nachrichten zur Kennwortänderung</th>
      </thead>
      <tbody>
        <tr>
          <td> %{linkExpiration.hours} </td>
          <td> Zeigt die Anzahl der Stunden an, die der Link gültig ist. </td>
        </tr>
        <tr>
          <td> %{linkExpiration.minutes} </td>
          <td> Zeigt die Anzahl der Minuten an, die der Link gültig ist. </td>
        </tr>
        <tr>
          <td> %{resetPassword.code} </td>
          <td> Zeigt einen einmaligen Kenncode als Teil der URL an. Dies bedeutet, dass jeder Person ein anderer Code zugeordnet ist. Beispiel: <code>https://appid-wfm.bluemix.net/verify/6574839563478</code>. </td>
        </tr>
        <tr>
          <td> %{resetPassword.link} </td>
          <td> Zeigt den Link an, auf den ein Benutzer klicken muss, um sein Kennwort zu ändern. </td>
        </tr>
       </tbody>
    </table></dd>
  <dt> Verifizierung</dt>
    <dd> Sie können festlegen, dass ein Benutzer sein Konto per E-Mail verifizieren muss. Indem Sie eine Verifizierung anfordern, begrenzen Sie die Anzahl der gefälschten Konten, die sich bei Ihrer App anmelden können. Sie können den Zugriff auf Ihre App einschränken, bis ein Benutzer seine E-Mail-Adresse verifiziert hat, oder Sie können auf diese Weise die Erstellung von Profilen für bestimmte Benutzer verwalten.
<table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> Parameter für Verifizierungsnachrichten </th>
      </thead>
      <tbody>
        <tr>
          <td> %{linkExpiration.hours} </td>
          <td> Zeigt die Anzahl der Stunden an, die der Link gültig ist. </td>
        </tr>
        <tr>
          <td> %{linkExpiration.minutes} </td>
          <td> Zeigt die Anzahl der Minuten an, die der Link gültig ist. </td>
        </tr>
        <tr>
          <td> %{verify.code} </td>
          <td> Zeigt eine einmalige Verifizierungs-URL an. </td>
        </tr>
        <tr>
          <td> %{verify.link} </td>
          <td> Zeigt die Aktions-URL an, die Sie in den Einstellungen angegeben haben. </td>
        </tr>
      </tbody>
    </table></dd>
  <dt> Kennwortänderung </dt>
    <dd> Sie können einen Benutzer über die Kennwortaktualisierung benachrichtigen. Dies ist nützlich, wenn die Anforderung zur Kennwortänderung nicht vom Benutzer ausging. So können die Benutzer die erforderlichen Schritte unternehmen, um ihr Konto erneut zu schützen.

    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> Parameter für Nachrichten zur Kennwortänderung</th>
      </thead>
      <tbody>
        <tr>
          <td> %{passwordChangeInfo.time} </td>
          <td> Zeigt den Zeitpunkt an, an dem ein neues Kennwort gültig wurde. </td>
        </tr>
        <tr>
          <td> %{passwordChangeInfo.ipAddress} </td>
          <td> Zeigt die IP-Adresse an, von der aus die Kennwortänderung angefordert wurde. </td>
        </tr>
      </tbody>
    </table></dd>
</dl>



## Cloud Directory mit dem Android-SDK verwalten
{: #managing-android}

Zur Verwendung der folgenden APIs muss für **Cloud Directory-Identitätsprovider** die Einstellung **Ein** festgelegt werden.

### Mit dem Ressourceneignerkennwort anmelden
Sie können ein Zugriffs- und ein Identitätstoken abrufen, indem Sie den Benutzernamen und das Kennwort des Endbenutzers verwenden. 

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

### Anmeldung

Für **Benutzern die Anmeldung und das Zurücksetzen ihres Kennworts ermöglichen** muss in den Einstellungen für Cloud Directory der Wert **Ein** festgelegt werden.

 Verwenden Sie die Klasse 'LoginWidget', um den Anmeldeablauf zu starten.
 ```java
 LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
 loginWidget.launchSignUp(this, new AuthorizationListener() {
			 @Override
			 public void onAuthorizationFailure (AuthorizationException exception) {
				 //Ausnahmebedingung aufgetreten.
   		}

			 @Override
			 public void onAuthorizationCanceled () {
				 //Anmeldung vom Benutzer abgebrochen.
			 }

			 @Override
			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
				 if (accessToken != null && identityToken != null) {
				     //Benutzer authentifiziert.
				 } else {
				     //E-Mail-Verifizierung erforderlich.
				 }

			 }
		 });
 ```
 {: codeblock}

### Kennwort vergessen
Für **Benutzern die Anmeldung und das Zurücksetzen ihres Kennworts ermöglichen** und **E-Mail für vergessenes Kennwort** muss in den Einstellungen für Cloud Directory der Wert **Ein** festgelegt werden.

Verwenden Sie die Klasse 'LoginWidget', um den Verarbeitungsablauf für das vergessene Kennwort zu starten.
  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launchForgotPassword(this, new AuthorizationListener() {
 			 @Override
 			 public void onAuthorizationFailure (AuthorizationException exception) {
 				 //Ausnahmebedingung aufgetreten.
 			 }

 			 @Override
 			 public void onAuthorizationCanceled () {
 				 //Aktion für vergessenes Kennwort vom Benutzer abgebrochen.
 			 }

 			 @Override
 			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
 				 //Aktion für vergessenes Kennwort beendet, in diesem Fall sind Zugriffstoken und Identitätstoken null.

 			 }
 		 });
  ```
  {: codeblock}

### Details ändern
Für **Benutzern die Anmeldung und das Zurücksetzen ihres Kennworts ermöglichen** muss in den Einstellungen für Cloud Directory der Wert **Ein** festgelegt werden. Verwenden Sie die Klasse 'LoginWidget', um den Verarbeitungsablauf für das Ändern von Details zu starten. Diese API kann nur verwendet werden, wenn der Benutzer Cloud Directory als Identitätsprovider für die Anmeldung verwendet.
   ```java
   LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
   loginWidget.launchChangeDetails(this, new AuthorizationListener() {
  			 @Override
  			 public void onAuthorizationFailure (AuthorizationException exception) {
  				 //Ausnahmebedingung aufgetreten.
  			 }

  			 @Override
        public void onAuthorizationCanceled () {
  				 //Detailänderung vom Benutzer abgebrochen.
  			 }

  			 @Override
  			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
  				 //Benutzer authentifiziert, neue Token erhalten.
  			 }
  		 });
   ```
   {: codeblock}

### Kennwortänderung
Für **Benutzern die Anmeldung und das Zurücksetzen ihres Kennworts ermöglichen** muss in den Einstellungen für Cloud Directory der Wert **Ein** festgelegt werden.

Verwenden Sie die Klasse 'LoginWidget', um den Verarbeitungsablauf für die Kennwortänderung zu starten. Diese API kann nur verwendet werden, wenn der Benutzer Cloud Directory als Identitätsprovider für die Anmeldung verwendet.

   ```java
    LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launchChangePassword(this, new AuthorizationListener() {
   			 @Override
   			 public void onAuthorizationFailure (AuthorizationException exception) {
   				 //Ausnahmebedingung aufgetreten.
   			 }

   			 @Override
        public void onAuthorizationCanceled () {
   				 //Kennwortänderung vom Benutzer abgebrochen.
   			 }

   			 @Override
   			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
   				   //Benutzer authentifiziert, neue Token erhalten.
   			 }
   		 });
   ```
   {: codeblock}

## Cloud Directory mit dem iOS-Swift-SDK verwalten


### Mit dem Ressourceneignerkennwort anmelden

Sie können ein Zugriffs- und ein Identitätstoken abrufen, indem Sie den Benutzernamen und das Kennwort des Endbenutzers verwenden. 
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

### Anmeldung

Für **Benutzern die Anmeldung und das Zurücksetzen ihres Kennworts ermöglichen** muss in den Einstellungen für Cloud Directory der Wert **Ein** festgelegt werden.

Verwenden Sie die Klasse 'LoginWidget', um den Anmeldeablauf zu starten.
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

### Kennwort vergessen
Für **Benutzern die Anmeldung und das Zurücksetzen ihres Kennworts ermöglichen** und **E-Mail für vergessenes Kennwort** muss in den Einstellungen für Cloud Directory der Wert **Ein** festgelegt werden.

Verwenden Sie die Klasse 'LoginWidget', um den Verarbeitungsablauf für das vergessene Kennwort zu starten.
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

### Details ändern

Für **Benutzern die Anmeldung und das Zurücksetzen ihres Kennworts ermöglichen** muss in den Einstellungen für Cloud Directory der Wert **Ein** festgelegt werden.

Verwenden Sie die Klasse 'LoginWidget', um den Verarbeitungsablauf für das Ändern von Details zu starten. Diese API kann nur verwendet werden, wenn der Benutzer Cloud Directory als Identitätsprovider für die Anmeldung verwendet.
  ```swift

   class delegate : AuthorizationDelegate {
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
          //Benutzer authentifiziert, neue Token erhalten.
       }

       public func onAuthorizationCanceled() {
           //Detailänderung vom Benutzer abgebrochen.
       }

       public func onAuthorizationFailure(error: AuthorizationError) {
           //Ausnahmebedingung aufgetreten.
       }
   }

   AppID.sharedInstance.loginWidget?.launchChangeDetails(delegate: delegate())
  ```
  {: codeblock}

### Kennwortänderung

Für **Benutzern die Anmeldung und das Zurücksetzen ihres Kennworts ermöglichen** muss in den Einstellungen für Cloud Directory der Wert **Ein** festgelegt werden.

Verwenden Sie die Klasse 'LoginWidget', um den Verarbeitungsablauf für die Kennwortänderung zu starten. Diese API kann nur verwendet werden, wenn der Benutzer Cloud Directory als Identitätsprovider für die Anmeldung verwendet.
  ```swift
   class delegate : AuthorizationDelegate {
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
           //Benutzer authentifiziert, neue Token erhalten.
       }

       public func onAuthorizationCanceled() {
           //Kennwortänderung vom Benutzer abgebrochen.
       }

       public func onAuthorizationFailure(error: AuthorizationError) {
            //Ausnahmebedingung aufgetreten.
       }
    }

    AppID.sharedInstance.loginWidget?.launchChangePassword(delegate: delegate())
  ```
  {: codeblock}


## Cloud Directory mit dem Node.js-SDK verwalten
Stellen Sie sicher, dass für den Cloud Directory-Identitätsprovider die Einstellung **Ein** festgelegt ist, und geben Sie den Callback-Endpunkt an.

### Ablauf für die Anmeldung mit dem Ressourceneignerkennwort
WebAppStrategy ermöglicht Benutzern die Anmeldung bei Ihrer Webanwendung mithilfe eines Benutzernamens und eines Kennwort.
Nach einer erfolgreichen Anmeldung wird das Zugriffstoken des Benutzers in der HTTP-Sitzung gespeichert und ist verfügbar, solange die HTTP-Sitzung aktiv bleibt. Wenn die Sitzung gelöscht wird oder abgelaufen ist, wird auch das Token gelöscht.

Wenn Sie den Benutzern die Anmeldung mit einem Benutzernamen und einem Kennwort ermöglichen möchten, fügen Sie zu Ihrer App eine POST-Route hinzu, die mit den Parametern für den Benutzernamen und das Kennwort aufgerufen wird.

  ```javascript
  app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true // Flash-Nachrichten zulassen.
  }));
  ```
  {: codeblock}

  <table>
    <thead>
      <th colspan=2><img src="images/idea.png"/> Erläuterung der Komponenten dieses Befehls </th>
    </thead>
    <tbody>
      <tr>
        <td><code> successRedirect </code></td>
        <td> Legen Sie für diesen Wert die URL fest, an die ein Benutzer nach einer erfolgreichen Authentifizierung weitergeleitet werden soll. Der Standardwert ist die ursprüngliche Anforderungs-URL. Beispiel: <code>/form/submit</code>. </td>
      </tr>
      <tr>
        <td><code> failureRedirect </code></td>
        <td> Legen Sie für diesen Wert die URL fest, an die ein Benutzer nach einer fehlgeschlagenen Authentifizierung weitergeleitet werden soll. Der Standardwert ist die ursprüngliche Anforderungs-URL. </td>
      </tr>
      <tr>
        <td><code> failureFlash </code></td>
        <td> Legen Sie für diesen Wert <code>true</code> fest, um eine von Cloud Directory zurückgegebene Fehlernachricht zu erhalten. Der Standardwert ist 'false'.</td>
      </tr>
     </tbody>
  </table>


**Hinweis**:
  * Wenn Sie die Anforderung mithilfe eines HTML-Formulars übergeben, verwenden Sie die Middleware [body-parser](https://www.npmjs.com/package/body-parser).
  * Verwenden Sie [connect-flash](https://www.npmjs.com/package/connect-flash) zum Empfangen der zurückgegebenen Fehlernachricht. Siehe `web-app-sample-server.js`.

### Anmeldung
Zum Starten des {{site.data.keyword.appid_short_notm}}-Anmeldeformulars übergeben Sie die WebAppStrategy-Eigenschaft "show" und legen Sie den Wert `WebAppStrategy.SIGN_UP` dafür fest.
  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: codeblock}

    **Hinweis**:
    * Wenn in den Cloud Directory-Einstellungen für **Benutzern die Anmeldung ohne E-Mail-Verifizierung ermöglichen** der Wert **Nein** festgelegt ist, wird der Prozess beendet, ohne dass {{site.data.keyword.appid_short_notm}}-Zugriffs- und -Identitätstokens abgerufen werden.
    * Für **Benutzern die Anmeldung und das Zurücksetzen ihres Kennworts ermöglichen** muss in den Einstellungen für Cloud Directory der Wert **Ein** festgelegt werden. 


### Kennwort vergessen
Zum Starten des {{site.data.keyword.appid_short_notm}}-Formulars für ein vergessenes Kennwort übergeben Sie die WebAppStrategy-Eigenschaft `show` und legen Sie den Wert `WebAppStrategy.FORGOT_PASSWORD` dafür fest.
  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: codeblock}

**Hinweis**:
* Wenn in den Cloud Directory-Einstellungen für **Benutzern die Anmeldung ohne E-Mail-Verifizierung ermöglichen** der Wert **Nein** festgelegt ist, wird der Prozess beendet, ohne dass {{site.data.keyword.appid_short_notm}}-Zugriffs- und -Identitätstokens abgerufen werden.
* Für **Benutzern die Anmeldung und das Zurücksetzen ihres Kennworts ermöglichen** und **E-Mail für vergessenes Kennwort** muss in den Einstellungen für Cloud Directory der Wert **Ein** festgelegt werden.

### Details ändern
Zum Starten des {{site.data.keyword.appid_short_notm}}-Formulars für das Ändern von Details übergeben Sie die WebAppStrategy-Eigenschaft `show` und legen Sie den Wert `WebAppStrategy.CHANGE_DETAILS` dafür fest.
  ```javascript
  app.get("/change_details", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_DETAILS
  }));
  ```
  {: codeblock}

**Hinweis**:
* Ein Benutzer muss authentifiziert werden, indem Cloud Directory als Identitätsprovider verwendet wird.
* Für **Benutzern die Anmeldung und das Zurücksetzen ihres Kennworts ermöglichen** muss in den Einstellungen für Cloud Directory der Wert **Ein** festgelegt werden. 


### Kennwortänderung
Zum Starten des {{site.data.keyword.appid_short_notm}}-Formulars für die Kennwortänderung übergeben Sie die WebAppStrategy-Eigenschaft `show` und legen Sie den Wert `WebAppStrategy.CHANGE_PASSWORD` dafür fest.
  ```javascript
  app.get("/change_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_PASSWORD
  }));
  ```
  {: codeblock}

**Hinweis**:
* Ein Benutzer muss authentifiziert werden, indem Cloud Directory als Identitätsprovider verwendet wird.
* Für **Benutzern die Anmeldung und das Zurücksetzen ihres Kennworts ermöglichen** muss in den Einstellungen für Cloud Directory der Wert **Ein** festgelegt werden. 
