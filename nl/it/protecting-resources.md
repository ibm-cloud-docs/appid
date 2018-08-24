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


# Protezione delle risorse di back-end
{: #secure-back-end}

Puoi utilizzare le SDK server {{site.data.keyword.appid_short_notm}} per proteggere gli endpoint di accesso alle tue applicazioni. Puoi anche utilizzare le SDK client per accedere alle risorse protette.
{: shortdesc}

Il richiamo di una risorsa protetta avvia il widget di accesso, se necessario. Se è già stato ottenuto un token valido, il widget di accesso non viene avviato e si accede direttamente alla risorsa.
{: tip}

## Protezione delle risorse in Liberty for Java
{: #protecting-liberty}

Puoi utilizzare {{site.data.keyword.appid_short_notm}} per proteggere gli endpoint nelle tue applicazioni IBM Liberty for Java. Liberty for Java ha la capacità integrata di gestire le richieste di Open ID Connect (OIDC).
{: shortdesc}



Prima di cominciare:
* Hai bisogno di un'<a href="https://console.bluemix.net/catalog/starters/liberty-for-java" target="_blank">applicazione {{site.data.keyword.Bluemix_notm}} Liberty for Java<img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> esistente non associata. Per acquisire familiarità con lo sviluppo delle applicazioni Liberty for Java, consulta [la documentazione](/docs/runtimes/liberty/index.html).
* Assicurati di aver installato <a href="https://maven.apache.org/download.cgi" target="_blank">Apache Maven <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>.
* Impara come OIDC funziona con Liberty for Java.



Per proteggere le tue risorse:

1. Scarica l'esempio Liberty for Java dalla IU. L'esempio contiene un file compresso con i file Liberty standard.
2. Segui le istruzioni fornite nell'IU per distribuire l'applicazione a IBM Cloud.
3. Apri la tua applicazione in un browser e accedi utilizzando le tue credenziali per verificare le attività di autenticazione.

## Protezione di risorse in Node.js
{: #protecting-resources-nodesdk}

L'SDK server {{site.data.keyword.appid_short_notm}} fornisce una strategia passport ApiStrategy utilizzata nella applicazioni di back-end distribuite in {{site.data.keyword.Bluemix_notm}}. Per proteggere la tua applicazione da accessi non autorizzati devi strumentare il tuo server Node.js con ApiStrategy. Il `modulo npm appid-serversdk-nodejs` fornisce la strategia passport ApiStrategy e il metodo di verifica per convalidare il token di accesso e il token ID emessi da {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

L'SDK server {{site.data.keyword.appid_short_notm}} utilizza il framework <a href="http://passportjs.org/" target="_blank">Passport <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> per implementare l'autorizzazione.

Il seguente frammento di codice illustra come utilizzare `APIStrategy` in un'applicazione Express semplice per proteggere i metodi GET dell'endpoint `/protected`.
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


## Protezione delle risorse con Swift SDK
{: #protecting-swift}

Puoi utilizzare {{site.data.keyword.appid_short_notm}} per proteggere le tue risorse lato server utilizzando l'SDK Swift.
{: shortdesc}

L'SDK server Swift {{site.data.keyword.appid_short_notm}} fornisce un plug-in middleware di protezione dell'API utilizzato per proteggere le tue applicazioni di back-end. Associando le tue API al middleware, puoi proteggere la tua applicazione da accessi non autorizzati. Dopo che l'API è protetta, il middleware garantisce che i token generati da {{site.data.keyword.appid_short_notm}} siano convalidati. Puoi quindi modificare il comportamento dell'API in base ai risultati della convalida.

Vedi il seguente frammento di codice per un esempio di come proteggere l'API `/protectedendpoint`.

```Swift
import Foundation
import Kitura              // server
import Credentials         // middleware
import IBMCloudAppID       // SDK

// setup routes
let router = Router()

// mandatory option to be passed in if app not deployed on IBM Cloud
let options = [
    "oauthServerUrl": "https://appid-oauth.ng.bluemix.net/oauth/v3/d8438de6-c325-4956-ad34-abd49194affd",
]
let apiCreds = Credentials()

// Minimum macOS version required
if #available(OSX 10.12, *) {

    // setup API protection
    let apiKituraCredentialsPlugin = APIKituraCredentialsPlugin(options: options)
    apiCreds.register(plugin: apiKituraCredentialsPlugin)

    // associate route with API protection
    router.all(middleware: apiCreds)

    // create protected API
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

    // Start server
    Kitura.addHTTPServer(onPort: 8090, with: router)

    Kitura.run()  
}
```


## Accesso alle risorse protette con l'SDK iOS Swift
{: #requesting-swift}

Puoi utilizzare {{site.data.keyword.appid_short_notm}} per proteggere gli endpoint nelle tue applicazioni iOS Swift.
{: shortdesc}

1. Importa BMSCore.
  ```swift
  import BMSCore
  ```
  {: codeblock}

2. Richiama una richiesta della risorsa protetta.
  ```swift
  BMSClient.sharedInstance.initialize(bluemixRegion: AppID.<region>)
  BMSClient.sharedInstance.authorizationManager = AppIDAuthorizationManager(appid:AppID.sharedInstance)
  var request:Request =  Request(url: "<your protected resource url>")
  request.send(completionHandler: {(response:Response?, error:Error?) in
      //il codice gestisce la risposta qui
  })
  ```
  {: codeblock}


## Accesso alle risorse protette con l'SDK Android
{: #requesting-android}

Puoi utilizzare {{site.data.keyword.appid_short_notm}} per proteggere gli endpoint nelle tue applicazioni Android.
{: shortdesc}

1. Richiama una richiesta della risorsa protetta.
  ```java
  BMSClient bmsClient = BMSClient.getInstance();
  bmsClient.initialize(getApplicationContext(), AppID.REGION_UK);

  AppIDAuthorizationManager appIdAuthMgr = new AppIDAuthorizationManager(AppID.getInstance())
  bmsClient.setAuthorizationManager(appIdAuthMgr);

  Request request = new Request("<your protected resource url>", Request.GET);
  request.send(this, new ResponseListener() {
  @Override
		public void onSuccess (Response response) {
     //il codice gestisce la risposta qui
  }
  @Override
		public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
      //il codice gestisce la risposta qui
  });
  ```
  {: codeblock}
