---

copyright:
  years: 2017
lastupdated: "2017-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


# Back-End-Ressourcen schützen

Mit den {{site.data.keyword.appid_short_notm}}-Server-SDKs können Sie Endpunkte in Ihren Apps schützen und den Zugriff darauf steuern. Darüber hinaus können Sie die Client-SDKs verwenden, um auf geschützte Ressourcen zuzugreifen.

**Hinweis**: Beim Aufrufen einer geschützten Ressource wird bei Bedarf das Anmelde-Widget gestartet. Wenn bereits ein gültiges Token angefordert wurde, wird das Anmelde-Widget nicht gestartet. Auf die Ressource kann dann direkt zugegriffen werden.

## Ressourcen in Liberty for Java schützen
{: #protecting-liberty}

Mit {{site.data.keyword.appid_short_notm}} können Sie Endpunkte in Ihren IBM Liberty for Java-Apps schützen. Liberty for Java bietet die integrierte Funktionalität für die Verarbeitung von Open ID Connect-Anforderungen (OIDC-Anforderungen).

Vorbereitungen:
* Sie benötigen eine vorhandene, nicht gebundene [IBM Liberty for Java-App](https://console.bluemix.net/catalog/starters/liberty-for-java). Anhand der [Dokumentation](/docs/runtimes/liberty/index.html) können Sie sich mit der Entwicklung von Liberty for Java-Apps vertraut machen.
* [Apache Maven](https://maven.apache.org/download.cgi) muss installiert sein.
* Machen Sie sich mit der Funktionsweise von OIDC mit Liberty for Java vertraut.

Schützen der Ressourcen:

1. Laden Sie das Liberty for Java-Beispiel von der Benutzerschnittstelle herunter. Das Beispiel enthält eine ZIP-Datei mit den Liberty-Standarddateien.
2. Öffnen Sie das Terminal in dem Verzeichnis, in dem Sie das Beispiel entpackt haben.
3. Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} über die Cloud Foundry-Befehlszeile an. Geben Sie Ihre Berechtigungsnachweise ein, wenn Sie dazu aufgefordert werden.

  ```
  cf login
  ```
  {: codeblock}

4. Stellen Sie die App bereit. Mit dem folgenden Befehl wird eine Liberty for Java-Instanz mit einem Namen erstellt, der der Tenant-ID zugeordnet ist.

  ```
  cf push
  ```
  {: codeblock}

5. Binden Sie die Serviceinstanz an die neue Liberty for Java-Instanz und stellen Sie die App erneut bereit.
6. Öffnen Sie die App in einem Browser und melden Sie sich mit Ihren Berechtigungsnachweisen an, um die Authentifizierungsaktivitäten zu überprüfen.

## Ressourcen in Node.js schützen
{: #protecting-resources-nodesdk}

Das {{site.data.keyword.appid_short_notm}}-Server-SDK stellt eine ApiStrategy-Passwort-Strategie zur Verfügung, die in Back-End-Apps verwendet werden, die in {{site.data.keyword.Bluemix_notm}} bereitgestellt werden. Zum Schutz Ihrer App gegen unbefugten Zugriff müssen Sie Ihren Node.js-Server mit ApiStrategy instrumentieren. Das NPM-Modul `appid-serversdk-nodejs` stellt die Passport-Strategie 'ApiStrategy' und eine Verifizierungsmethode bereit, um das von {{site.data.keyword.appid_short_notm}} ausgegebene Zugriffstoken und ID-Token zu validieren.

Das {{site.data.keyword.appid_short_notm}}-Server-SDK verwendet das <a href="http://passportjs.org/" target="_blank">Passport-Framework <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> zur Umsetzung der Berechtigung.

Das folgende Snippet demonstriert, wie `APIStrategy` in einer einfachen Express-App zum Schutz der GET-Methoden für den Endpunkt `/protected` verwendet wird.

  ```JavaScript

  var express = require('express');
  var passport = require('passport');
  var APIStrategy = require('bluemix-appid').APIStrategy;

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


## Mit dem iOS-Swift-SDK auf geschützte Ressourcen zugreifen
{: #requesting-swift}

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
