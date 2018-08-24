---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-09"

---

{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:pre: .pre}
{:new_window: target="blank"}
{:shortdesc: .shortdesc}


# Standardanzeigen anzeigen
{: #default}

{{site.data.keyword.appid_full}} stellt ein Anmeldewidget zur Verfügung, mit dem Sie Ihren Benutzern sichere Anmeldeoptionen bieten können.
{: shortdesc}

Wenn Ihre App für die Verwendung eines Identitätsproviders konfiguriert wurde, werden Besucher Ihrer App durch ein Anmeldewidget zur Anmeldeanzeige weitergeleitet. Wenn nur ein einziger Provider aktiviert (**Ein**) ist, werden Besucher standardmäßig zur Authentifizierungsanzeige des betreffenden Identitätsproviders weitergeleitet. Mit dem Anmeldewidget können Sie eine Standardanmeldeanzeige anzeigen oder bei Nutzung des Cloudverzeichnisses Ihre vorhandenen Benutzerschnittstellen wiederverwenden. Zusätzlich interessant ist hierbei, dass Sie Ihren Anmeldedatenfluss jederzeit aktualisieren können, ohne Ihren Quellcode in irgendeiner Weise zu ändern!



Der Service verwendet OAuth2-Bewilligungstypen, um den Berechtigungsprozess zuzuordnen. Wenn Sie Social Media-Identitätsprovider wie z. B. Facebook konfigurieren, wird der [Oauth2-Berechtigungserteilungsablauf](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html) verwendet, um das Anmeldewidget aufzurufen.

Wollen Sie eine Benutzererfahrung kreieren, durch die sich Ihre App von anderen abhebt? Sie können [Ihre eigenen Anzeigen einbringen](/docs/services/appid/branded.html)!
{: tip}


## Standardanmeldeanzeige anpassen
{: #login-widget}

Sie können die vorkonfigurierte Anmeldeanzeige so anpassen, dass das Logo und die gewünschten Farben angezeigt werden.
{: shortdesc}

Anpassen der Anzeige:

1. Öffnen Sie das {{site.data.keyword.appid_short_notm}}-Service-Dashboard.
2. Wählen Sie den Abschnitt über die **Anpassung der Registrierung** aus. Sie können die Darstellung des Anmeldewidgets ändern, damit es zur Außendarstellung des Unternehmens passt.
3. Laden Sie Ihr Unternehmenslogo hoch. Wählen Sie dazu eine PNG- oder JPG-Datei von Ihrem lokalen System aus. Die empfohlene Bildgröße ist 320 x 320 Pixel. Die maximale Dateigröße ist 100 KB.
4. Wählen Sie eine Headerfarbe für das Widget aus der Farbauswahl aus oder geben Sie den hexadezimalen Code für eine andere Farbe ein.
5. Prüfen Sie das Aussehen im Vorschaubereich und klicken Sie auf **Änderungen speichern**, wenn Sie mit den Anpassungen zufrieden sind. Eine Bestätigungsnachricht wird angezeigt.
6. Aktualisieren Sie die Anmeldeseite im Browser, um Ihre Änderungen zu überprüfen.


## Anzeigen planen
{: #plan}

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
      <th>Cloud Directory</th>
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

Nachdem Sie Ihre Einstellungen für [Social Media-Identitätsprovider](/docs/services/appid/identity-providers.html) und [Cloudverzeichnis](/docs/services/appid/cloud-directory.html) konfiguriert haben, klicken Sie in der folgenden Abbildung auf die gewünschte Sprache, um den Code zu implementieren.


Klicken Sie auf die Abbildung, um eines der bereitgestellten SDKs oder die APIs zu verwenden. Vergessen Sie nicht, dass Sie App ID auch mit anderen Sprachen nutzen können. Mithilfe unserer APIs können Sie in jeder App ein Cloudverzeichnis einrichten. Wenn Sie Hilfe für Sprachen benötigen, die nicht in der Abbildung enthalten sind, informieren Sie sich anhand <a href="https://www.ibm.com/blogs/bluemix/tag/app-id/" target="_blank">unserer Blogs<img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> über mögliche Lösungen.
{: shortdesc}

</br>

## Standardanzeigen mit dem Android-SDK anzeigen
{: #android}

Sie können die vorkonfigurierten Anzeigen mit dem Android-SDK aufrufen.
{: shortdesc}

</br>

**Anmelden**
1. Den folgenden Befehl in den Code einfügen.
    ```java
    LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launch(this, new AuthorizationListener() {
          @Override
          public void onAuthorizationFailure (AuthorizationException exception) {
            // Ausnahmebedingung aufgetreten.
     			 }

          @Override
          public void onAuthorizationCanceled () {
            // Authentifizierung vom Benutzer abgebrochen
          }

          @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
            // Benutzer authentifiziert.
          }
        });
    ```
  {: pre}

</br>
**Registrierung**

1. Für **Benutzern die Registrierung und das Zurücksetzen ihres Kennworts ermöglichen** den Wert **Ein** in den Cloud Directory-Einstellungen festlegen.
2. Das Anmeldewidget aufrufen, um den Registrierungsablauf zu starten. 
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

1. Für **Benutzern die Registrierung und das Zurücksetzen ihres Kennworts ermöglichen** und **E-Mail für vergessenes Kennwort** den Wert **Ein** in den Cloud Directory-Einstellungen festlegen.
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

1. Für **Benutzern die Registrierung und das Zurücksetzen ihres Kennworts ermöglichen** den Wert **Ein** in den Cloud Directory-Einstellungen festlegen.
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

1. Für **Benutzern die Registrierung und das Zurücksetzen ihres Kennworts ermöglichen** den Wert **Ein** in den Cloud Directory-Einstellungen festlegen.
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

## Standardanzeigen mit dem iOS Swift-SDK anzeigen
{: #ios-swift}

Sie können die vorkonfigurierten Anzeigen mit dem iOS Swift-SDK aufrufen.
{: shortdesc}

</br>
**Anmelden**

1. Den folgenden Befehl in den Code einfügen.
  ```swift
  import BluemixAppID
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, refreshToken: RefreshToken?) {
          // Benutzer authentifiziert
      }

      public func onAuthorizationCanceled() {
          // Authentifizierung vom Benutzer abgebrochen
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          // Ausnahmebedingung aufgetreten.
  			 }
  }

  AppID.sharedInstance.loginWidget?.launch(delegate: delegate())
  ```
  {: pre}


</br>
**Registrierung**

1. Für **Benutzern die Registrierung und das Zurücksetzen ihres Kennworts ermöglichen** den Wert **Ein** in den Cloud Directory-Einstellungen festlegen.
2. Das Anmeldewidget aufrufen, um den Registrierungsablauf zu starten. 
  ```swift
  class delegate : AuthorizationDelegate {
    public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?) {
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

1. Für **Benutzern die Registrierung und das Zurücksetzen ihres Kennworts ermöglichen** und **E-Mail für vergessenes Kennwort** den Wert **Ein** in den Cloud Directory-Einstellungen festlegen.
2. Das Anmeldewidget aufrufen, um den Ablauf beim Vergessen eines Kennworts zu starten.
  ```swift
  class delegate : AuthorizationDelegate {
     public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?) {
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
**Kontodetails**

1. Für **Benutzern die Registrierung und das Zurücksetzen ihres Kennworts ermöglichen** den Wert **Ein** in den Cloud Directory-Einstellungen festlegen.
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

1. Für **Benutzern die Registrierung und das Zurücksetzen ihres Kennworts ermöglichen** den Wert **Ein** in den Cloud Directory-Einstellungen festlegen.
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

## Standardanzeige mit dem Node.js-SDK anzeigen
{: #nodejs}

Sie können die vorkonfigurierten Anzeigen mit dem Node.js-SDK aufrufen.
{: shortdesc}

</br>
**Anmelden**
1. In den Identitätsprovidereinstellungen den Wert **Ein** für Cloud Directory festlegen und einen Callback-Endpunkt angeben.
2. Eine POST-Route zu Ihrer App hinzufügen, die mit den Parametern für den Benutzernamen und das Kennwort aufgerufen werden kann, und mit dem Kennwort des Ressourceneigners anmelden.
    ```javascript
    app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
    	successRedirect: LANDING_PAGE_URL,
    	failureRedirect: ROP_LOGIN_PAGE_URL,
    	failureFlash : true // allow flash messages
    }));
    ```
    {: pre}
    `WebAppStrategy` ermöglicht es Benutzern, sich bei Ihren Web-Apps mit einem Benutzernamen und einem Kennwort anzumelden. Nach einer erfolgreichen Registrierung wird das Zugriffstoken eines Benutzers in der HTTP-Sitzung gespeichert und ist während der Sitzung verfügbar. Sobald die HTTP-Sitzung gelöscht wird oder abgelaufen ist, ist das Token nicht mehr gültig.
    {: tip}

</br>
**Registrierung**

1. Für **Benutzern die Registrierung und das Zurücksetzen ihres Kennworts ermöglichen** den Wert **Ein** in den Cloud Directory-Einstellungen festlegen. Falls diese Einstellung nicht aktiviert ist, wird der Prozess beendet, ohne dass Zugriffs- und Identitätstoken abgerufen werden.
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

1. Für **Benutzern die Registrierung und das Zurücksetzen ihres Kennworts ermöglichen** und **E-Mail für vergessenes Kennwort** den Wert **Ein** in den Cloud Directory-Einstellungen festlegen. Falls diese Einstellung nicht aktiviert ist, wird der Prozess beendet, ohne dass Zugriffs- und Identitätstoken abgerufen werden.
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
1. Für **Benutzern die Registrierung und das Zurücksetzen ihres Kennworts ermöglichen** den Wert **Ein** in den Cloud Directory-Einstellungen festlegen.
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
1. Für **Benutzern die Registrierung und das Zurücksetzen ihres Kennworts ermöglichen** den Wert **Ein** in den Cloud Directory-Einstellungen festlegen.
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

## Standardanzeigen mit dem Swift-SDK anzeigen
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

  // Callback zum Beenden des Berechtigungsprozesses. Ruft Zugriffs- und Identitätstoken von AppID ab
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

  // HTTP-Server hinzufügen und mit Router verbinden
  Kitura.addHTTPServer(onPort: port, with: router)

  // Start des Kitura-Runloops (Aufruf wird nie zurückgegeben)
  Kitura.run()
  ```
  {: codeblock}
</br>
</br>



