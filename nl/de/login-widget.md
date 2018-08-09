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


# Anmeldeerfahrung verwalten

{{site.data.keyword.appid_full}} stellt ein Anmeldewidget zur Verfügung, mit dem Sie Ihren Benutzern sichere Anmeldeoptionen bieten können.
{: shortdesc}

Wenn Ihre App für die Verwendung eines Identitätsproviders konfiguriert wurde, werden Besucher Ihrer App durch ein Anmeldewidget zur Anmeldeanzeige weitergeleitet. Falls nur ein Provider aktiviert ist, werden Besucher standardmäßig zur Authentifizierungsanzeige des Identitätsproviders weitergeleitet. Mit dem Anmeldewidget können Sie eine Standardanmeldeanzeige anzeigen oder bei Nutzung des Cloudverzeichnisses Ihre vorhandenen Benutzerschnittstellen wiederverwenden. 

Sie können Ihren Anmeldedatenfluss jederzeit aktualisieren, ohne Ihren Quellcode in irgendeiner Weise zu ändern.
{: tip}

Der Service verwendet OAuth2-Bewilligungstypen, um den Berechtigungsprozess zuzuordnen. Wenn Sie Social Media-Identitätsprovider wie z. B. Facebook konfigurieren, wird der [Oauth2-Berechtigungserteilungsablauf](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html) verwendet, um das Anmeldewidget aufzurufen. Wenn Sie Ihre eigenen Anzeigen der Benutzerschnittstelle verwenden, wird der [Ablauf für Kennwortberechtigungsnachweise von Ressourceneignern](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html) verwendet, um sich anzumelden und Zugriff und Identitätstoken zu erhalten. 


## Standardanmeldeanzeige anpassen
{: #login-widget}

Sie können die vorkonfigurierte Anmeldeanzeige so anpassen, dass das Logo und die gewünschten Farben angezeigt werden.
{: shortdesc}

Anpassen der Anzeige:

1. Öffnen Sie das {{site.data.keyword.appid_short_notm}}-Service-Dashboard.
2. Wählen Sie den Abschnitt über die **Anpassung der Registrierung** aus. Sie können die Darstellung des Anmeldewidgets ändern, damit es zur Außendarstellung des Unternehmens passt. 
3. Laden Sie Ihr Unternehmenslogo hoch. Wählen Sie dazu eine PNG- oder JPG von Ihrem lokalen System aus. Die empfohlene Bildgröße ist 320 x 320 Pixel. Die maximale Dateigröße ist 100 KB.
4. Wählen Sie eine Headerfarbe für das Widget aus der Farbauswahl aus oder geben Sie den hexadezimalen Code für eine andere Farbe ein.
5. Prüfen Sie das Aussehen im Vorschaubereich und klicken Sie auf **Änderungen speichern**, wenn Sie mit den Anpassungen zufrieden sind. Eine Bestätigungsnachricht wird angezeigt.
6. Aktualisieren Sie die Anmeldeseite im Browser, um Ihre Änderungen zu überprüfen. 


## Standardanzeigen anzeigen
{: #default}

{{site.data.keyword.appid_short_notm}} stellt eine Standardanmeldeanzeige zur Verfügung, die Sie aufrufen können, wenn Sie keine eigenen Anzeigen der Benutzerschnittstellen haben.
{: shortdesc}

Abhängig von der Konfiguration des Identitätsproviders können sich die Anzeigen voneinander unterscheiden. Der Service stellt keine erweiterte Funktionalität für Social Media-Identitätsprovider zur Verfügung, da kein Zugriff auf die Benutzerkontoinformationen ermöglicht wird. Benutzer müssen sich an den Identitätsprovider wenden, um ihre Daten zu verwalten. Wenn jemand beispielsweise sein Kennwort für Facebook ändern möchte, muss er www.facebook.com aufrufen.

Überprüfen Sie die folgende Tabelle, um zu sehen, welche Anzeigen Sie für den jeweiligen Identitätsprovidertyp anzeigen können. 

<table>
  <thead>
    <tr>
      <th>Anzeigebildschirm</th>
      <th>Social Media-Identitätsprovider</th>
      <th>Unternehmensidentitätsprovider</th>
      <th>Cloudverzeichnis</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Anmelden</td>
      <td><img src="images/confirm.png" width="32" alt="Funktion verfügbar" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="Funktion verfügbar" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="Funktion verfügbar" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Registrieren</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Funktion verfügbar" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Kennwort vergessen</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Funktion verfügbar" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Kennwort ändern</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Funktion verfügbar" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Kontodetails</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Funktion verfügbar" style="width:32px;" /></td>
    </tr>
  </tbody>
</table>

Nachdem Sie Ihre Einstellungen für [Social Media-Identitätsprovider](/docs/services/appid/identity-providers.html) und [Cloudverzeichnis](/docs/services/appid/cloud-directory.html) konfiguriert haben, klicken Sie im folgenden Bild auf die gewünschte Sprache, um den Code zu implementieren. 


Klicken Sie im folgenden Bild auf die gewünschte Sprache, um mit dem Implementieren des Codes zu beginnen. 

<img usemap="#default-options-map" border="0" class="image" id="options" src="images/default-options.png" width="750" alt="Klicken Sie auf ein SDK-Sprachensymbol, um  in Ihren Apps mit dem Cloudverzeichnis zu beginnen." style="width:750px;" />
<map name="default-options-map" id="default-options-map">
<area href="login-widget.html#android" alt="Anmeldeschnittstelle mit dem Android-SDK verwalten" shape="rect" coords="113, 8, 224, 123" />
<area href="login-widget.html#ios-swift" alt="Anmeldeschnittstelle mit dem iOS Swift-SDK verwalten" shape="rect" coords="251, 12, 362, 127" />
<area href="login-widget.html#nodejs" alt="Anmeldeschnittstelle mit dem Node.js-SDK verwalten" shape="rect" coords="387, 10, 498, 125" />
<area href="login-widget.html#swift" alt="Anmeldeerfahrung mit dem Swift-SDK verwalten" shape="rect" coords="525, 10, 636, 125" />
</map>
</br>

### Standardanzeigen mit dem Android-SDK anzeigen
{: #android}

Sie können die vorkonfigurierten Anzeigen mit dem Android-SDK aufrufen.
{: shortdesc}

</br>

**Anmelden**
1. Fügen Sie den folgenden Befehl in den Code ein.
    ```java
    LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launch(this, new AuthorizationListener() {
          @Override
          public void onAuthorizationFailure (AuthorizationException exception) {
            //Ausnahmebedingung aufgetreten.
  			 }

          @Override
        public void onAuthorizationCanceled () {
            //Authentifizierung von Benutzer abgebrochen
        }

          @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
            //Benutzer authentifiziert.
          }
        });
    ```
  {: pre}

</br>
**Registrierung**

1. Für **Benutzern die Registrierung und das Zurücksetzen ihres Kennworts ermöglichen** den Wert **Aktiv** in den Cloud Directory-Einstellungen festlegen.
2. Rufen Sie das LoginWidget auf, um mit dem Registrierungsablauf zu beginnen.
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
**Kennwort vergessen**

1. Für **Benutzern die Registrierung und das Zurücksetzen ihres Kennworts ermöglichen** und **E-Mail für vergessenes Kennwort** den Wert **Aktiv** in den Cloud Directory-Einstellungen festlegen.
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
   			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
   			 }
   		 });
    ```
    {: pre}

</br>
**Kontodetails**

1. Für **Benutzern die Registrierung und das Zurücksetzen ihres Kennworts ermöglichen** den Wert **Aktiv** in den Cloud Directory-Einstellungen festlegen.
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
  			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
  			 }
  		 });
   ```
   {: pre}

</br>
**Kennwort ändern**

1. Für **Benutzern die Registrierung und das Zurücksetzen ihres Kennworts ermöglichen** den Wert **Aktiv** in den Cloud Directory-Einstellungen festlegen.
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
   			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
   			 }
   		 });
   ```
   {: pre}
</br>
</br>

### Standardanzeigen mit dem iOS Swift-SDK anzeigen
{: #ios-swift}

Sie können die vorkonfigurierten Anzeigen mit dem iOS Swift-SDK aufrufen.
{: shortdesc}

</br>
**Anmelden**

1. Fügen Sie den folgenden Befehl in den Code ein.
  ```swift
  import BluemixAppID
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, refreshToken: RefreshToken?) {
          //Benutzer authentifiziert
      }

      public func onAuthorizationCanceled() {
          //Authentifizierung von Benutzer abgebrochen
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          //Ausnahmebedingung aufgetreten.
  			 }
  }

  AppID.sharedInstance.loginWidget?.launch(delegate: delegate())
  ```
  {: pre}


</br>
**Registrierung**

1. Für **Benutzern die Registrierung und das Zurücksetzen ihres Kennworts ermöglichen** den Wert **Aktiv** in den Cloud Directory-Einstellungen festlegen.
2. Rufen Sie das LoginWidget auf, um mit dem Registrierungsablauf zu beginnen. 
  ```swift
  class delegate : AuthorizationDelegate {
    public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?) {
       if accessToken == nil && identityToken == nil {
        //E-Mail-Verifizierung erforderlich.
        return
       }
     //Benutzer authentifiziert.
    }

    public func onAuthorizationCanceled() {
        //Registrierung vom Benutzer abgebrochen.
    }

    public func onAuthorizationFailure(error: AuthorizationError) {
        //Ausnahmebedingung aufgetreten.
  			 }
  }

  AppID.sharedInstance.loginWidget?.launchSignUp(delegate: delegate())
  ```
  {: pre}

</br>
**Kennwort vergessen**

1. Für **Benutzern die Registrierung und das Zurücksetzen ihres Kennworts ermöglichen** und **E-Mail für vergessenes Kennwort** den Wert **Aktiv** in den Cloud Directory-Einstellungen festlegen.
2. Das Anmeldewidget aufrufen, um den Ablauf beim Vergessen eines Kennworts zu starten.
  ```swift
  class delegate : AuthorizationDelegate {
     public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?) {
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
  {: pre}

</br>
**Kontodetails**

1. Für **Benutzern die Registrierung und das Zurücksetzen ihres Kennworts ermöglichen** den Wert **Aktiv** in den Cloud Directory-Einstellungen festlegen.
2. Das Anmeldewidget aufrufen, um den Ablauf für das Ändern von Details zu starten.
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
**Kennwort ändern**

1. Für **Benutzern die Registrierung und das Zurücksetzen ihres Kennworts ermöglichen** den Wert **Aktiv** in den Cloud Directory-Einstellungen festlegen.
2. Das Anmeldewidget aufrufen, um den Ablauf für das Ändern des Kennworts zu starten.
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

### Standardanzeige mit dem Node.js-SDK anzeigen
{: #nodejs}

Sie können die vorkonfigurierten Anzeigen mit dem Node.js-SDK aufrufen.
{: shortdesc}

</br>
**Anmelden**
1. In den Identitätsprovidereinstellungen den Wert **Aktiv** für Cloud Directory festlegen und einen Callback-Endpunkt angeben.
2. Eine POST-Route zu Ihrer App hinzufügen, die mit den Parametern für den Benutzernamen und das Kennwort aufgerufen werden kann, und mit dem Kennwort des Ressourceneigners anmelden.
    ```javascript
    app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
    	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true // Flash-Nachrichten zulassen.
  }));
    ```
    {: pre}
    `WebAppStrategy` ermöglicht es Benutzern, sich bei Ihren Web-Apps mit einem Benutzernamen und einem Kennwort anzumelden. Nach einer erfolgreichen Registrierung wird das Zugriffstoken eines Benutzers in der HTTP-Sitzung gespeichert und ist während der Sitzung verfügbar. Sobald die HTTP-Sitzung gelöscht wird oder abgelaufen ist, ist das Token nicht mehr gültig. {: tip}

</br>
**Registrierung**

1. Für **Benutzern die Registrierung und das Zurücksetzen ihres Kennworts ermöglichen** den Wert **Aktiv** in den Cloud Directory-Einstellungen festlegen. Falls diese Einstellung nicht aktiviert ist, wird der Prozess beendet, ohne dass Zugriffs- und Identitätstoken abgerufen werden. 
2. Die WebAppStrategy-Eigenschaft `show` übergeben und `WebAppStrategy.SIGN_UP` dafür festlegen.
  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: pre}

</br>
**Kennwort vergessen**

1. Für **Benutzern die Registrierung und das Zurücksetzen ihres Kennworts ermöglichen** und **E-Mail für vergessenes Kennwort** den Wert **Aktiv** in den Cloud Directory-Einstellungen festlegen. Falls diese Einstellung nicht aktiviert ist, wird der Prozess beendet, ohne dass Zugriffs- und Identitätstoken abgerufen werden. 
2. Die WebAppStrategy-Eigenschaft `show` übergeben und `WebAppStrategy.FORGOT_PASSWORD` dafür festlegen.
  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: pre}

</br>
**Kontodetails**
1. Für **Benutzern die Registrierung und das Zurücksetzen ihres Kennworts ermöglichen** den Wert **Aktiv** in den Cloud Directory-Einstellungen festlegen.
2. Die WebAppStrategy-Eigenschaft `show` übergeben und `WebAppStrategy.CHANGE_DETAILS` dafür festlegen.
  ```javascript
  app.get("/change_details", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_DETAILS
  }));
  ```
  {: pre}

</br>
**Kennwort ändern**
1. Für **Benutzern die Registrierung und das Zurücksetzen ihres Kennworts ermöglichen** den Wert **Aktiv** in den Cloud Directory-Einstellungen festlegen.
2. Die WebAppStrategy-Eigenschaft `show` übergeben und `WebAppStrategy.CHANGE_PASSWORD` dafür festlegen.
  ```javascript
  app.get("/change_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_PASSWORD
  }));
  ```
  {: pre}

</br>
</br>
### Standardbenutzerschnittstelle mit dem Swift-SDK anzeigen
{: #swift}

Wenn die Social Media-Identitätsprovider aktiviert sind, können Sie die vorkonfigurierte Anmeldeanzeige mit dem Swift-SDK aufrufen.
{: shortdesc}

1. Der folgende Code demonstriert, wie WebAppKituraCredentialsPlugin in einer Kitura-App verwendet wird, um den Endpunkt `/protected` zu schützen. 

  ```swift
  import Foundation
  import Kitura
  import KituraSession
  import Credentials
  import SwiftyJSON
  import BluemixAppID

  // Folgende URLs werden für AppID OAuth-Abläufe genutzt
  var LOGIN_URL = "/ibm/bluemix/appid/login"
  var CALLBACK_URL = "/ibm/bluemix/appid/callback"
  var LOGOUT_URL = "/ibm/bluemix/appid/logout"
  var LANDING_PAGE_URL = "/index.html"

  // Setup von Kitura zur Nutzung von Sitzungs-Middleware
  // Muss mit korrektem Sitzungsspeicher für Produktionsumgebungen
  // konfiguriert werden. Siehe https://github.com/IBM-Swift/Kitura-Session für
  // weitere Dokumentationen
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

  // Expliziter Anmelde-Endpunkt
  router.get(LOGIN_URL,
  		   handler: kituraCredentials.authenticate(credentialsType: webappKituraCredentialsPlugin.name,
  												   successRedirect: LANDING_PAGE_URL,
  												   failureRedirect: LANDING_PAGE_URL
  ))

  // Callback zum Beenden des Berechtigungsprozesses. Ruft Zugriffs- und Identitätstokens von AppID ab
  router.get(CALLBACK_URL,
  		   handler: kituraCredentials.authenticate(credentialsType: webappKituraCredentialsPlugin.name,
  												   successRedirect: LANDING_PAGE_URL,
  												   failureRedirect: LANDING_PAGE_URL
  ))

  // Abmelde-Endpunkt. Löscht Authentifizierungsinformationen aus Sitzung
  router.get(LOGOUT_URL, handler:  { (request, response, next) in
  	kituraCredentials.logOut(request: request)
  	webappKituraCredentialsPlugin.logout(request: request)
  	_ = try? response.redirect(LANDING_PAGE_URL)
  })

  // Geschützter Bereich
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

  //HTTP-Server hinzufügen und mit Router verbinden
  Kitura.addHTTPServer(onPort: port, with: router)

  // Start des Kitura-Runloops (Aufruf wird nie zurückgegeben)
  Kitura.run()
  ```
  {: codeblock}
</br>
</br>


### Angepasste Anzeigen mit dem Android-SDK aufrufen
{: #branded-ui-android}

Wenn Cloud Directory aktiviert ist, können Sie mit dem Android-SDK angepasste Anzeigen aufrufen. Sie können die gewünschte Kombination der Anzeigen auswählen, mit denen die Benutzer interagieren sollen. <a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="blank">Lesen in diesem Blog <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> ein ausführliches Beispiel dazu!
{: shortdesc}

</br>
**Anmelden**

1. **Cloud Directory** als Identitätsprovider **aktivieren**.
2. Fügen Sie den folgenden Befehl in den Code ein.
  ```java
  AppID.getInstance().signinWithResourceOwnerPassword(getApplicationContext(), username, password,
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
  {: pre}

</br>
</br>

### Angepasste Anzeigen mit dem iOS Swift-SDK aufrufen
{: #branded-ui-ios-swift}

Wenn Cloud Directory aktiviert ist, können Sie mit dem iOS Swift-SDK angepasste Anzeigen aufrufen.
{: shortdesc}

</br>
**Anmelden**

1. Auf der Registerkarte für den Identitätsprovider in der GUI den Wert **Aktiv** für Cloud Directory festlegen.
2. Mit dem Kennwort des Ressourceneigners anmelden. Zugriffs- und Identitätstoken werden abgerufen, wenn ein Benutzer versucht, sich mit seinem Benutzernamen und Kennwort anzumelden. 
  ```swift
  class delegate : TokenResponseDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
      //Benutzer authentifiziert.
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
      //Ausnahmebedingung aufgetreten.
  			 }
  }

  AppID.sharedInstance.signinWithResourceOwnerPassword(username: username, password: password, delegate: delegate())
  ```
  {: pre}
</br>
</br>

### Angepasste Anzeigen mit dem Node.js-SDK aufrufen
{: #branded-ui-nodejs}

Wenn Cloud Directory aktiviert ist, können Sie mit dem Node.js-SDK angepasste Anzeigen aufrufen. Sie können die gewünschte Kombination der Anzeigen auswählen, mit denen die Benutzer interagieren sollen. Wenn Sie einen Node.js-Back-End auswählen, können Sie Ihr Self-Service-Modul im {{site.data.keyword.appid_short_notm}} Node.js-SDK (Link) verwenden.
{: shortdesc}

**Anmelden**
1. In den Identitätsprovidereinstellungen den Wert **Aktiv** für Cloud Directory festlegen und einen Callback-Endpunkt angeben.
2. Eine POST-Route zu Ihrer App hinzufügen, die mit den Parametern für den Benutzernamen und das Kennwort aufgerufen werden kann, und mit dem Kennwort des Ressourceneigners anmelden.
    ```javascript
    app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
    	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true // Flash-Nachrichten zulassen.
  }));
    ```
    {: pre}
    `WebAppStrategy` ermöglicht es Benutzern, sich bei Ihren Web-Apps mit einem Benutzernamen und einem Kennwort anzumelden. Nach einer erfolgreichen Registrierung wird das Zugriffstoken eines Benutzers in der HTTP-Sitzung gespeichert und ist während der Sitzung verfügbar. Sobald die HTTP-Sitzung gelöscht wird oder abgelaufen ist, ist das Token nicht mehr gültig. {: tip}

</br>
</br>

## Angepasste Anzeigen mit der API anzeigen
{: #branding}

Sie können eigene angepasste Anzeigen anzeigen und die Authentifizierungs- und Berechtigungsfunktionen von {{site.data.keyword.appid_short_notm}} nutzen. Mit Cloud Directory als Identitätsprovider können die Benutzer mit Ihren Apps interagieren und benötigen deutlich weniger Unterstützung durch Sie. Die Benutzer können sich anmelden, sich registrieren, das Kennwort zurücksetzen und weitere Aktionen durchführen, ohne dass sie Unterstützung anfordern müssen.
{: shortdesc}

Um dies zu ermöglichen, hat {{site.data.keyword.appid_short_notm}} die REST-APIs zur Verfügung gestellt. Sie können die REST-API verwenden, um einen Back-End-Server zu erstellen, der Ihren Web-Apps dient oder um mit einer mobilen App mit Ihren angepassten Anzeigen zu interagieren. 

Die Verwaltungs-API ist mit IBM Cloud Identity und von Access Management generierten Tokens gesichert. Das heißt, dass Kontoeigner angeben können, wer in ihrem Team über welche Zugriffsebene für die jeweilige Serviceinstanz verfügen soll. Weitere Informationen dazu, wie IAM und {{site.data.keyword.appid_short_notm}} zusammenarbeiten, finden Sie in [Servicezugriffsverwaltung](/docs/services/appid/iam.html).

Wenn ein Benutzer in Ihren angepassten Anzeigen auf Anmelden klickt, wird der[ Ablauf für Kennwortberechtigungsnachweise von Ressourceneignern](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html) verwendet, um Zugriffs- und Identitätstoken von Ihren Web-Apps oder von Ihren mobilen Apps zu erhalten. 

Nach der Konfiguration Ihrer [Einstellungen](/docs/services/appid/cloud-directory.html), führen Sie folgende Schritte aus.


**Registrierung**
Sie können den Endpunkt `/sign_up` verwenden, um Benutzern zu ermöglichen, sich bei Ihrer App zu registrieren.
Stellen Sie die folgenden Daten im Anforderungshauptteil zur Verfügung: 
  * Ihre Tenant-ID (tenantID).
  * Benutzerdaten des Cloudverzeichnisses. Weitere Details finden Sie in [SCIM Full User Representation](https://tools.ietf.org/html/rfc7643#section-8.2). 
    * Ein Kennwortattribut `password`. 
    * Im E-Mail-Bereich, bei dem für das primäre Attribut (`primary`) der Wert `true` festgelegt ist, müssen Sie über mindestens eine E-Mail-Adresse verfügen. 

Abhängig von Ihren [E-Mail-Konfigurationen](/docs/services/appid/cloud-directory.html) erhält ein Benutzer möglicherweise die Anforderung für die Verifizierung oder eine Willkommens-E-Mail, wenn er sich für Ihre App registriert. Beide Typen von E-Mails werden ausgelöst, wenn ein Benutzer sich für Ihre App registriert. Die Verifizierungs-E-Mail enthält die Schaltfläche **Verifizieren**. Nach dem die Benutzer auf diese Schaltfläche geklickt und Ihre Identität bestätigt haben, wird von {{site.data.keyword.appid_short_notm}} eine Anzeige angezeigt, in der für die Verifizierung gedankt wird.   

Sie können Ihre eigene Seite darstellen, die nach der Verifizierung angezeigt werden soll. 

1. Navigieren Sie zu der Registerkarte für **Angepasste Landing-Pages** des {{site.data.keyword.appid_short_notm}}-Dashboards
2. Geben Sie die URL Ihrer Landing-Page im Feld für die **URL Ihrer angepassten Prüfseite für E-Mail-Adressen** ein.

Wenn dieser Wert bereitgestellt ist, ruft {{site.data.keyword.appid_short_notm}} die URL zusammen mit einer `Kontext`abfrage auf. Wenn Sie den Endpunkt `/sign_up/confirmation_result` aufrufen und die empfangenen `Kontext`parameter übergeben, können Sie im Ergebnis sehen, ob Ihr Benutzer das Konto verifiziert hat. Wurde das Konto verifiziert, können Sie jetzt Ihre angepasste Seite anzeigen. 

</br>
**Kennwort vergessen**

Sie können den Endpunkt `/forgot_password` verwenden, um Benutzern zu ermöglichen, Ihr Kennwort wiederherzustellen, falls Sie es vergessen haben sollten. 

Stellen Sie die folgenden Daten im Anforderungshauptteil zur Verfügung: 
  * Ihre Tenant-ID (tenantID).
  * Die E-Mail des Cloudverzeichnisbenutzers. 

Wenn der Endpunkt aufgerufen wird, wird die E-Mail zum Zurücksetzen des Kennworts an den Benutzer gesendet. Die E-Mail enthält die Schaltfläche **Zurücksetzen**. Nachdem die Benutzer auf diese Schaltfläche geklickt haben, wird von {{site.data.keyword.appid_short_notm}} eine Anzeige angezeigt, in der sie ihr Kennwort zurücksetzen können. 

Sie können Ihre eigene Seite darstellen, die nach dem Zurücksetzen des Kennworts angezeigt werden soll. 

1. Navigieren Sie zu der Registerkarte für **Angepasste Landing-Pages** des {{site.data.keyword.appid_short_notm}}-Dashboards
2. Geben Sie die URL für Ihre Landing-Page im Feld für die **URL für die angepasste Seite zum Zurücksetzen des Kennworts** ein.  

Wenn dieser Wert bereitgestellt ist, ruft {{site.data.keyword.appid_short_notm}} die URL zusammen mit einer `Kontext`abfrage auf. Der `Kontext`parameter wird verwendet, um das Ergebnis abzurufen, wenn `/forgot_password/confirmation_result` aufgerufen wird. Falls das Ergebnis erfolgreich war, können Sie Ihre angepasste Seite anzeigen. 

Fügen Sie eine zufällige Zeichenfolge zur angepassten Seite für das Zurücksetzen des Kennworts hinzu und übergeben Sie sie an Ihr Back-End, wenn die Anforderung übergeben wird. Lassen Sie Ihren Handler die Zeichenfolge überprüfen und den Endpunkt `/change_password` nur dann aufrufen, wenn die Zeichenfolge gültig ist. Auf diese Weise, können Sie die Verletzlichkeit Ihres Back-End-Endpunkts zum Zurücksetzen des Kennworts verringern.
{: tip}

</br>
**Kennwort ändern**

Sie können den Endpunkt `/change_password` auf zwei Weisen verwenden. Wenn ein Benutzer eine Anforderung zum Zurücksetzen übergibt oder wenn ein Benutzer sich bei Ihrer App anmeldet und sein Kennwort aktualisieren möchte. 

Gehen Sie wie folgt vor, um ein Kennwort nach der Anforderung zum Zurücksetzen zu aktualisieren: 

Stellen Sie folgende Daten im Anforderungshauptteil zur Verfügung: 
  * Ihre Tenant-ID (tenantID).
  * Das neue Kennwort des Benutzers. 
  * Die Cloudverzeichnisbenutzer-UUID
  * Optional: Die IP-Adresse, von der die Anforderung zum Zurücksetzen des Kennworts ausgeführt wurde. Wenn Sie auswählen, dass die IP-Adresse übergeben wird, dann ist der Platzhalter `%{passwordChangeInfo.ipAddress}` für die E-Mail-Vorlage zum Ändern des Kennworts verfügbar. 

Abhängig von Ihrer Konfiguration sendet {{site.data.keyword.appid_short_notm}} beim Ändern des Kennworts möglicherweise eine E-Mail an den Benutzer und lässt diesen wissen, dass eine Änderung vorgenommen wurde. 

</br>
Gehen Sie wie folgt vor, um Benutzern das Ändern ihres Kennworts zu ermöglichen, während sie sich bei Ihrer App anmelden: 

Stellen Sie folgende Daten im Anforderungshauptteil zur Verfügung: 
  * Ihre Tenant-ID (tenantID).
  * Das neue Kennwort des Benutzers. 
  * Die Cloudverzeichnisbenutzer-UUID

Ihre Seite zum Ändern des Kennworts sollte den Benutzer auffordern, sein aktuelles Kennwort und sein neues Kennwort einzugeben.
{: tip}

Ihr Back-End validiert das aktuelle Kennwort des Benutzers mit der ROP-API und falls dieses gültig ist, wird der Endpunkt mit dem neuen Kennwort aufgerufen. Abhängig von Ihrer Konfiguration sendet {{site.data.keyword.appid_short_notm}} beim Ändern des Kennworts möglicherweise eine E-Mail an den Benutzer und lässt diesen wissen, dass eine Änderung vorgenommen wurde. 

</br>
**Erneut senden**

Sie können den Endpunkt `/resend/{templateName}` verwenden, um eine E-Mail erneut zu senden, wenn ein Benutzer diese aus einem bestimmten Grund nicht erhalten hat. 

Stellen Sie folgende Daten im Anforderungshauptteil zur Verfügung: 
  * Die Tenant-ID (tenantID).
  * Den Vorlagennamen. 
  * Die Cloudverzeichnisbenutzer-UUID


**Details ändern**

Wenn ein Benutzer bei Ihrer App angemeldet ist, kann er einige seiner Daten aktualisieren. Sie können `/Users/{userId}` verwenden, um seine Daten abzurufen und zu aktualisieren. 

Wenn die Benutzerdetails aktualisiert werden, ruft der Endpunkt die aktualisierten Benutzerdaten im Anforderungshauptteil im [SCIM-Format](https://tools.ietf.org/html/rfc7643#section-8.2) ab. Stellen Sie sicher, dass Sie nur die relevanten Details ändern.

Die E-Mail-Adresse kann nicht geändert werden.
{: tip}
