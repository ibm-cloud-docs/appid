---

copyright:
  years: 2017
lastupdated: "2017-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Anmeldeschnittstelle verwalten
Mit dem Anmeldewidget können Sie in wenigen Minuten einen Anmeldeablauf einrichten und betriebsbereit machen. Sie können das Widget oder Motiv zu jedem beliebigen Zeitpunkt aktualisieren, ohne dass Anmeldequellcode hinzugefügt, entfernt oder geändert werden muss.
{: shortdesc}



## Anmelde-Widget anpassen
{: #login-widget}

Sie können das Anmelde-Widget so konfigurieren, dass das jeweilige Logo in den gewünschten Farben angezeigt wird.
{: shortdesc}

Wenn der {{site.data.keyword.appid_short}}-Service mit zwei oder mehreren Identitätsprovidern konfiguriert wird, kann der Benutzer einen Identitätsprovider im Anmelde-Widget auswählen. Führen Sie die folgenden Schritte aus, um Ihr Anmelde-Widget anzupassen:

1. Öffnen Sie das {{site.data.keyword.appid_short_notm}}-Service-Dashboard.
2. Wählen Sie den Abschnitt **Anpassung der Anmeldung**, in dem Sie das Aussehen des Anmelde-Widgets an Ihre Unternehmensmarke anpassen können.
3. Laden Sie Ihr Unternehmenslogo hoch. Wählen Sie dazu eine PNG- oder JPG von Ihrem lokalen System aus. Die empfohlene Bildgröße ist 320 x 320 Pixel. Die maximale Dateigröße ist 100 KB.
4. Wählen Sie eine Headerfarbe für das Widget aus der Farbauswahl aus oder geben Sie den hexadezimalen Code für eine andere Farbe ein.
5. Prüfen Sie das Aussehen im Vorschaubereich und klicken Sie auf **Änderungen speichern**, wenn Sie mit den Anpassungen zufrieden sind. Eine Bestätigungsnachricht wird angezeigt.

**Hinweis**: Sie müssen Ihre Anwendung nicht neu erstellen. Das Bild wird in der {{site.data.keyword.appid_short}}-Datenbank gespeichert und bei der nächsten Anmeldung angezeigt.

## Anmeldewidget mit dem Android-SDK ausführen
{: #authenticate-android}

Wenn Sie mehr als einen Identitätsprovider konfigurieren, wird den Benutzern ein Anmeldewidget angezeigt, sobald sie Ihre App aufrufen. Wenn Sie nur einen Identitätsprovider konfigurieren, wird der Benutzer standardmäßig zur Authentifizierungsanzeige des konfigurierten Identitätsproviders weitergeleitet.


Nach der Initialisierung des {{site.data.keyword.appid_short_notm}}-Client-SDK können Sie Benutzer authentifizieren, indem Sie das Anmelde-Widget ausführen.

  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launch(this, new AuthorizationListener() {
        @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //Ausnahmebedingung aufgetreten
        }

        @Override
        public void onAuthorizationCanceled () {
          //Authentifizierung von Benutzer abgebrochen
        }

        @Override
        public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
          //Benutzer authentifiziert
        }
      });
  ```
  {: codeblock}

## Anmeldewidget mit dem iOS-SDK ausführen
{: #authenticate-ios}

Wenn Sie mehr als einen Identitätsprovider konfigurieren, wird den Benutzern ein Anmeldewidget angezeigt, sobald sie Ihre App aufrufen. Wenn Sie nur einen Identitätsprovider konfigurieren, wird der Benutzer standardmäßig zur Authentifizierungsanzeige des konfigurierten Identitätsproviders weitergeleitet.


1. Fügen Sie den folgenden Import zu der Datei hinzu, in der das SDK verwendet werden soll.

  ```swift
  import BluemixAppID
  ```
  {: codeblock}

2. Führen Sie den folgenden Befehl aus, um das Widget zu starten:

  ```swift
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, response:Response?) {
          //Benutzer authentifiziert
      }

      public func onAuthorizationCanceled() {
          //Authentifizierung von Benutzer abgebrochen
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          //Ausnahmebedingung aufgetreten
      }
  }

  AppID.sharedInstance.loginWidget?.launch(delegate: delegate())
  ```
  {: codeblock}

## Anmeldewidget mit dem Node.js-SDK ausführen
{: #authenticate-nodejs}

Mit `WebAppStrategy` können Sie die Ressourcen von Webanwendungen schützen.

  ```JavaScript

  var express = require('express');
  var passport = require('passport');
  var WebAppStrategy = require('bluemix-appid').WebAppStrategy;
  ```
  {: codeblock}


## Anmeldewidget mit dem Swift-SDK ausführen
{: #authenticate-swift}

Das WebAppKituraCredentialsPlugin basiert auf dem Grant-Ablauf des OAuth2-Berechtigungscodes und muss für Webanwendungen verwendet werden, die Browser nutzen. Das Plug-in enthält Tools, um Authentifizierungs- und Berechtigungsabläufe zu implementieren. Das Plug-in stellt außerdem Mechanismen zur Verfügung, um nicht authentifizierte Versuche aufzudecken, auf geschützte Ressourcen zuzugreifen, und leitet einen Benutzerbrowser zur Authentifizierungsseite weiter. Nach einer erfolgreichen Authentifizierung wird der Benutzer zur Callback-URL der Webanwendung weitergeleitet, die das Plug-in verwendet, um Zugriff und Identitätstoken von {{site.data.keyword.appid_short_notm}} zu erhalten. Nach Erhalt dieser Token werden diese vom Plug-in in einer HTTP-Sitzung unter WebAppKituraCredentialsPlugin.AuthContext gespeichert.

Der folgende Code demonstriert, wie WebAppKituraCredentialsPlugin in einer Kitura-Anwendung verwendet wird, um den Endpunkt `/protected` zu schützen.

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
