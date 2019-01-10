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


# Acessando recursos protegidos por meio de aplicativos móveis
{: #access-backend}

É possível usar os SDKs do cliente {{site.data.keyword.appid_full}} para acessar terminais em seus aplicativos.
{: shortdesc}


## Acessando recursos protegidos com o SDK do Swift iOS
{: #accessing-swift}

É possível usar o SDK do iOS Swift do {{site.data.keyword.appid_short_notm}} para acessar terminais em seus aplicativos iOS Swift.
{: shortdesc}

1. Importe o BMSCore.
  ```swift
  import BMSCore
  ```
  {: codeblock}

2. Chame uma solicitação de recurso protegido.
  ```swift
  BMSClient.sharedInstance.initialize(bluemixRegion: AppID.<region>)
  BMSClient.sharedInstance.authorizationManager = AppIDAuthorizationManager(appid:AppID.sharedInstance)
  var request:Request =  Request(url: "<your protected resource url>")
  request.send(completionHandler: {(response:Response?, error:Error?) in
      //code handling the response here
  })
  ```
  {: codeblock}


## Acessando recursos protegidos com o SDK Android
{: #accessing-android}

É possível usar o SDK do Android do {{site.data.keyword.appid_short_notm}} para acessar terminais em seus aplicativos Android.
{: shortdesc}

1. Chame uma solicitação de recurso protegido.
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
