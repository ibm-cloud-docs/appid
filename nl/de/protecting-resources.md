---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}


# Back-End-Ressourcen schützen
{: #secure-back-end}

Mit den {{site.data.keyword.appid_short_notm}}-Server-SDKs können Sie Endpunkte in Ihren Apps schützen und den Zugriff darauf steuern. Darüber hinaus können Sie die Client-SDKs verwenden, um auf geschützte Ressourcen zuzugreifen.
{: shortdesc}

Das Aufrufen geschützter Ressourcen startet bei Bedarf das Anmeldewidget. Wenn bereits ein gültiges Token angefordert wurde, wird das Anmelde-Widget nicht gestartet. Auf die Ressource kann dann direkt zugegriffen werden.
{: tip}

## Ressourcen in Liberty for Java schützen
{: #protecting-liberty}

Mit {{site.data.keyword.appid_short_notm}} können Sie Endpunkte in Ihren IBM Liberty for Java-Apps schützen. Liberty for Java bietet die integrierte Funktionalität für die Verarbeitung von Open ID Connect-Anforderungen (OIDC-Anforderungen).
{: shortdesc}



Vorbereitungen:
* Sie benötigen eine vorhandene, nicht gebundene <a href="https://console.bluemix.net/catalog/starters/liberty-for-java" target="_blank">{{site.data.keyword.Bluemix_notm}} Liberty for Java-App <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>. Anhand der [Dokumentation](/docs/runtimes/liberty/index.html) können Sie sich mit der Entwicklung von Liberty for Java-Apps vertraut machen.
* Stellen Sie sicher, dass Sie <a href="https://maven.apache.org/download.cgi" target="_blank">Apache Maven <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> installiert haben.
* Machen Sie sich mit der Funktionsweise von OIDC mit Liberty for Java vertraut.



Schützen der Ressourcen:

1. Laden Sie das Liberty for Java-Beispiel von der Benutzerschnittstelle herunter. Das Beispiel enthält eine komprimierte Datei mit den Liberty-Standarddateien.
2. Stellen Sie Ihre Anwendung wie in der Benutzerschnittstelle beschrieben in IBM Cloud bereit. 
3. Öffnen Sie die App in einem Browser und melden Sie sich mit Ihren Berechtigungsnachweisen an, um die Authentifizierungsaktivitäten zu überprüfen.

## Ressourcen in Node.js schützen
{: #protecting-resources-nodesdk}

Das {{site.data.keyword.appid_short_notm}}-Server-SDK stellt eine ApiStrategy-Passwort-Strategie zur Verfügung, die in Back-End-Apps verwendet werden, die in {{site.data.keyword.Bluemix_notm}} bereitgestellt werden. Zum Schutz Ihrer App gegen unbefugten Zugriff müssen Sie Ihren Node.js-Server mit ApiStrategy instrumentieren. Das NPM-Modul `appid-serversdk-nodejs` stellt die Passport-Strategie 'ApiStrategy' und eine Verifizierungsmethode bereit, um das von {{site.data.keyword.appid_short_notm}} ausgegebene Zugriffstoken und ID-Token zu validieren.
{: shortdesc}

Das {{site.data.keyword.appid_short_notm}}-Server-SDK verwendet das <a href="http://passportjs.org/" target="_blank">Passport-Framework <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> zur Umsetzung der Berechtigung.

Das folgende Snippet demonstriert, wie `APIStrategy` in einer einfachen Express-App zum Schutz der GET-Methoden für den Endpunkt `/protected` verwendet wird.
  ```JavaScript

  var express = require('express');
  var passport = require('passport');
  var APIStrategy = require('ibmcloud-appid').APIStrategy;

  passport.use(new APIStrategy());
  var app = express();
  app.use(passport.initialize());

  app.get('/protected', passport.authenticate('APIStrategy.STRATEGY_NAME', {session: false }),
      function(request, response){
          console.log("Securty context", request.securityContext)
          response.send(200, "Success!");
      }
  );

  app.listen(process.env.PORT);
  ```
  {: codeblock}


## Ressourcen mit dem Swift-SDK schützen
{: #protecting-swift}

Sie können {{site.data.keyword.appid_short_notm}} verwenden, um Ihre Ressourcen auf der Serverseite mithilfe des Swift-SDK zu schützen.
{: shortdesc}

Das {{site.data.keyword.appid_short_notm}} Swift-Server-SDK stellt ein Middleware-Plug-in für den API-Schutz zur Verfügung, das zum Schutz Ihrer Back-End-Apps verwendet wird. Durch die Zuordnung Ihrer APIs zur Middleware können Sie Ihre App vor unbefugtem Zugriff schützen. Nachdem die API geschützt ist, stellt die Middleware sicher, dass die Token, die von {{site.data.keyword.appid_short_notm}} generiert wurden, validiert werden. Sie können dann das Verhalten der API abhängig von den Validierungsergebnissen ändern.

Das folgende Code-Snippet ist ein Beispiel für den Schutz der `/protectedendpoint`-API.

```Swift
import Foundation
import Kitura              // Server
import Credentials         // Middleware
import IBMCloudAppID       // SDK

// Routen einrichten
let router = Router()

// Obligatorische Option, die übergeben wird, wenn die App nicht in IBM Cloud bereitgestellt wird.
let options = [
    "oauthServerUrl": "https://appid-oauth.ng.bluemix.net/oauth/v3/d8438de6-c325-4956-ad34-abd49194affd",
]
let apiCreds = Credentials()

// Mindestens erforderliche macOS-Version
if #available(OSX 10.12, *) {

    // API-Schutz einrichten
    let apiKituraCredentialsPlugin = APIKituraCredentialsPlugin(options: options)
    apiCreds.register(plugin: apiKituraCredentialsPlugin)

    // Route zu API-Schutz zuordnen.
    router.all(middleware: apiCreds)

    // Geschützte API erstellen.
    router.get("/protectedendpoint") { request, response, next in

        response.headers["Content-Type"] = "text/html; charset=utf-8"
        do {
            if let userProfile = request.userProfile  {
                try response.status(.OK).send(
                    "<!DOCTYPE html><html><body>" +
                        "Welcome " + userProfile.displayName  +
                        "! You are logged in with " + userProfile.provider + ".
" +
                    "</body></html>\n\n").end()
                next()
                return
            }
            try response.status(.unauthorized).send(
                "<!DOCTYPE html><html><body>” + “You are not authorized!" +
                "</body></html>\n\n").end()
        }
        catch {}
        next()
    }

    // Server starten
    Kitura.addHTTPServer(onPort: 8090, with: router)

    Kitura.run()  
}
```


## Mit dem iOS-Swift-SDK auf geschützte Ressourcen zugreifen
{: #requesting-swift}

Mit {{site.data.keyword.appid_short_notm}} können Sie Endpunkte in Ihren iOS Swift-Apps schützen.
{: shortdesc}

1. Importieren Sie BMSCore.
  ```swift
  import BMSCore
  ```
  {: codeblock}

2. Rufen Sie eine Anforderung für die geschützte Ressource auf.
  ```swift
  BMSClient.sharedInstance.initialize(bluemixRegion: AppID.<region>)
  BMSClient.sharedInstance.authorizationManager = AppIDAuthorizationManager(appid:AppID.sharedInstance)
  var request:Request =  Request(url: "<your protected resource url>")
  request.send(completionHandler: {(response:Response?, error:Error?) in
      //Code-Handling der Antwort hier
  })
  ```
  {: codeblock}


## Mit dem Android-SDK auf geschützte Ressourcen zugreifen
{: #requesting-android}

Mit {{site.data.keyword.appid_short_notm}} können Sie Endpunkte in Ihren Android-Apps schützen.
{: shortdesc}

1. Rufen Sie eine Anforderung für die geschützte Ressource auf.
  ```java
  BMSClient bmsClient = BMSClient.getInstance();
  bmsClient.initialize(getApplicationContext(), AppID.REGION_UK);

  AppIDAuthorizationManager appIdAuthMgr = new AppIDAuthorizationManager(AppID.getInstance())
  bmsClient.setAuthorizationManager(appIdAuthMgr);

  Request request = new Request("<your protected resource url>", Request.GET);
  request.send(this, new ResponseListener() {
  @Override
	public void onSuccess (Response response) {
     //Code-Handling der Antwort hier
  }
  @Override
	public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
      //Code-Handling des Fehlers hier
  });
  ```
  {: codeblock}
