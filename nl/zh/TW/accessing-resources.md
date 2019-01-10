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


# 從行動應用程式存取受保護的資源
{: #access-backend}

您可以使用 {{site.data.keyword.appid_full}} 用戶端 SDK 來存取應用程式中的端點。
{: shortdesc}


## 使用 iOS Swift SDK 存取受保護資源
{: #accessing-swift}

您可以使用 {{site.data.keyword.appid_short_notm}} iOS Swift SDK 來存取 iOS Swift 應用程式中的端點。
{: shortdesc}

1. 匯入 BMSCore。
  ```swift
  import BMSCore
  ```
  {: codeblock}

2. 呼叫受保護的資源要求。
  ```swift
  BMSClient.sharedInstance.initialize(bluemixRegion: AppID.<region>)
  BMSClient.sharedInstance.authorizationManager = AppIDAuthorizationManager(appid:AppID.sharedInstance)
  var request:Request =  Request(url: "<your protected resource url>")
  request.send(completionHandler: {(response:Response?, error:Error?) in
      //code handling the response here
  })
  ```
  {: codeblock}


## 使用 Android SDK 存取受保護資源
{: #accessing-android}

您可以使用 {{site.data.keyword.appid_short_notm}} Android SDK 來存取 Android 應用程式中的端點。
{: shortdesc}

1. 呼叫受保護的資源要求。
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
