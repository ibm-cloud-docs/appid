---

copyright:
  years: 2017, 2018
lastupdated: "2018-01-02"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


# Protezione delle risorse di back-end 

Puoi utilizzare le SDK server {{site.data.keyword.appid_short_notm}} per proteggere gli endpoint di accesso alle tue applicazioni. Puoi anche utilizzare le SDK client per accedere alle risorse protette. 

**Nota**: il richiamo di una risorsa protetta avvia il widget di accesso, se necessario. Se è già stato ottenuto un token valido, il widget di accesso non viene avviato e si accede direttamente alla risorsa.

## Protezione delle risorse in Liberty for Java
{: #protecting-liberty}

Puoi utilizzare {{site.data.keyword.appid_short_notm}} per proteggere gli endpoint nelle tue applicazioni IBM Liberty for Java. Liberty for Java ha incorporata la capacità di gestire le richieste Open ID Connect (OIDC).

Prima di cominciare:
* Hai bisogno di un'[applicazione IBM Liberty for Java](https://console.bluemix.net/catalog/starters/liberty-for-java) non associata ed esistente. Per acquisire familiarità con lo sviluppo delle applicazioni Liberty for Java, consulta [la documentazione](/docs/runtimes/liberty/index.html).
* Assicurati che [Apache Maven](https://maven.apache.org/download.cgi) sia installato.
* Impara come OIDC funziona con Liberty for Java.

Per proteggere le tue risorse: 

1. Scarica l'esempio Liberty for Java dalla IU. L'esempio contiene un file zip con i file Liberty standard.
2. Apri il terminale nella directory in cui hai estratto l'esempio.
3. Accedi a {{site.data.keyword.Bluemix_notm}} utilizzando la riga di comando Cloud Foundry. Quando richiesto, immetti le tue credenziali.

  ```
  cf login
  ```
  {: codeblock}

4. Distribuisci l'applicazione. Immettendo il seguente comando crei un'istanza Liberty for Java con un nome correlato al tenantid.

  ```
  cf push
  ```
  {: codeblock}

5. Associa la tua istanza del servizio alla nuova istanza Liberty for Java e ridistribuisci l'applicazione. 
6. Apri la tua applicazione in un browser e accedi utilizzando le tue credenziali per verificare le attività di autenticazione. 

## Protezione di risorse in Node.js
{: #protecting-resources-nodesdk}

L'SDK server {{site.data.keyword.appid_short_notm}} fornisce una strategia passport ApiStrategy utilizzata nella applicazioni di back-end distribuite in {{site.data.keyword.Bluemix_notm}}. Per proteggere la tua applicazione da accessi non autorizzati devi strumentare il tuo server Node.js con ApiStrategy. Il `modulo npm appid-serversdk-nodejs` fornisce la strategia passport ApiStrategy e il metodo di verifica per convalidare il token di accesso e il token ID emessi da {{site.data.keyword.appid_short_notm}}.

L'SDK server {{site.data.keyword.appid_short_notm}} utilizza il framework <a href="http://passportjs.org/" target="_blank">Passport <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> per implementare l'autorizzazione.

Il seguente frammento di codice illustra come utilizzare `APIStrategy` in un'applicazione Express semplice per proteggere i metodi GET dell'endpoint `/protected`. 

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


## Accesso alle risorse protette con l'SDK Swift iOS 
{: #requesting-swift}

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
