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


# Acceso a recursos protegidos desde apps móviles
{: #access-backend}

Puede utilizar el SDK del cliente de {{site.data.keyword.appid_full}} para acceder a los puntos finales de sus apps.
{: shortdesc}


## Acceso a recursos protegidos con el SDK de Swift de iOS
{: #accessing-swift}

Puede utilizar el SDK de iOS Swift de {{site.data.keyword.appid_short_notm}} para acceder a puntos finales de las apps de iOS Swift.
{: shortdesc}

1. Importe BMSCore.
  ```swift
  import BMSCore
  ```
  {: codeblock}

2. Invoque una solicitud de recurso protegido.
  ```swift
  BMSClient.sharedInstance.initialize(bluemixRegion: AppID.<region>)
  BMSClient.sharedInstance.authorizationManager = AppIDAuthorizationManager(appid:AppID.sharedInstance)
  var request:Request =  Request(url: "<your protected resource url>")
  request.send(completionHandler: {(response:Response?, error:Error?) in
      //el código maneja la respuesta aquí
  })
  ```
  {: codeblock}


## Acceso a recursos protegidos con el SDK de Android
{: #accessing-android}

Puede utilizar el SDK de Android de {{site.data.keyword.appid_short_notm}} para acceder a los puntos finales de sus apps de Android.
{: shortdesc}

1. Invoque una solicitud de recurso protegido.
  ```java
  BMSClient bmsClient = BMSClient.getInstance();
  bmsClient.initialize(getApplicationContext(), AppID.REGION_UK);

  AppIDAuthorizationManager appIdAuthMgr = new AppIDAuthorizationManager(AppID.getInstance())
  bmsClient.setAuthorizationManager(appIdAuthMgr);

  Request request = new Request("<your protected resource url>", Request.GET);
  request.send(this, new ResponseListener() {
  @Override
		public void onSuccess (Response response) {
     //el código maneja la respuesta aquí
  }
  @Override
		public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
      //el código maneja el error aquí
  });
  ```
  {: codeblock}
