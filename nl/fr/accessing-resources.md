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


# Accès aux ressources protégées à partir d'applications mobiles
{: #access-backend}

Vous pouvez utiliser les SDK client {{site.data.keyword.appid_full}} pour accéder aux noeuds finaux dans vos applications.
{: shortdesc}


## Accès aux ressources protégées avec le logiciel SDK Swift iOS
{: #accessing-swift}

Vous pouvez utiliser le SDK Swift iOS {{site.data.keyword.appid_short_notm}} pour accéder aux noeuds finaux dans vos applications Swift iOS.
{: shortdesc}

1. Importez BMSCore.
  ```swift
  import BMSCore
  ```
  {: codeblock}

2. Appelez une demande de ressource protégée.
  ```swift
  BMSClient.sharedInstance.initialize(bluemixRegion: AppID.<region>)
  BMSClient.sharedInstance.authorizationManager =
AppIDAuthorizationManager(appid:AppID.sharedInstance)
  var request:Request =  Request(url: "<your protected resource url>")
  request.send(completionHandler: {(response:Response?, error:Error?) in
      //code handling the response here
  })
  ```
  {: codeblock}


## Accès aux ressources protégées avec le logiciel SDK Android
{: #accessing-android}

Vous pouvez utiliser le SDK Android {{site.data.keyword.appid_short_notm}} pour accéder aux noeuds finaux dans vos applications Android.
{: shortdesc}

1. Appelez une demande de ressource protégée.
  ```java
  BMSClient bmsClient = BMSClient.getInstance();
  bmsClient.initialize(getApplicationContext(), AppID.REGION_UK);

  AppIDAuthorizationManager appIdAuthMgr = new AppIDAuthorizationManager(AppID.getInstance())
  bmsClient.setAuthorizationManager(appIdAuthMgr);

  Request request = new Request("<your protected resource url>", Request.GET);
  request.send(this, new ResponseListener() {
  @Override
		public void onSuccess (Response response) {
     //code handling the response here
  }
  @Override
		public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
      //code handling the failure here
  });
  ```
  {: codeblock}
