---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}


# Accesso alle risorse protette dalle applicazioni mobili 
{: #access-backend}

Puoi utilizzare gli SDK client {{site.data.keyword.appid_full}} per accedere agli endpoint nelle tue applicazioni.
{: shortdesc}


## Accesso alle risorse protette con l'SDK iOS Swift
{: #accessing-swift}

Puoi utilizzare l'SDK {{site.data.keyword.appid_short_notm}} iOS Swift per accedere agli endpoint nelle tue applicazioni iOS Swift.
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
{: #accessing-android}

Puoi utilizzare l'SDK {{site.data.keyword.appid_short_notm}} Android per accedere agli endpoint nelle tue applicazioni Android.
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
