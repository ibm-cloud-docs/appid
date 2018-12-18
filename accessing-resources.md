---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-18"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}


# Accessing protected resources from mobile apps
{: #access-backend}

You can use the {{site.data.keyword.appid_full}} client SDKs to access endpoints in your apps.
{: shortdesc}


## Accessing protected resources with the iOS Swift SDK
{: #accessing-swift}

You can use the {{site.data.keyword.appid_short_notm}} iOS Swift SDK to access endpoints in your iOS Swift apps.
{: shortdesc}

1. Import BMSCore.
  ```swift
  import BMSCore
  ```
  {: codeblock}

2. Invoke a protected resource request.
  ```swift
  BMSClient.sharedInstance.initialize(region: AppID.<region>)
  BMSClient.sharedInstance.authorizationManager = AppIDAuthorizationManager(appid:AppID.sharedInstance)
  var request:Request =  Request(url: "<your protected resource url>")
  request.send(completionHandler: {(response:Response?, error:Error?) in
      //code handling the response here
  })
  ```
  {: codeblock}


## Accessing protected resources with the Android SDK
{: #accessing-android}

You can use the {{site.data.keyword.appid_short_notm}} Android SDK to access endpoints in your Android apps.
{: shortdesc}

1. Invoke a protected resource request.
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
