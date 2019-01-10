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


# 通过移动应用程序访问受保护资源
{: #access-backend}

您可以使用 {{site.data.keyword.appid_full}} 客户端 SDK 来访问应用程序中的端点。
{: shortdesc}


## 使用 iOS Swift SDK 访问受保护资源
{: #accessing-swift}

您可以使用 {{site.data.keyword.appid_short_notm}} iOS Swift SDK 来访问 iOS Swift 应用程序中的端点。
{: shortdesc}

1. 导入 BMSCore。
  ```swift
  import BMSCore
  ```
  {: codeblock}

2. 调用受保护资源请求。
  ```swift
  BMSClient.sharedInstance.initialize(bluemixRegion: AppID.<region>)
  BMSClient.sharedInstance.authorizationManager = AppIDAuthorizationManager(appid:AppID.sharedInstance)
  var request:Request =  Request(url: "<your protected resource url>")
  request.send(completionHandler: {(response:Response?, error:Error?) in
      //code handling the response here
  })
  ```
  {: codeblock}


## 使用 Android SDK 访问受保护资源
{: #accessing-android}

您可以使用 {{site.data.keyword.appid_short_notm}} Android SDK 来访问 Android 应用程序中的端点。
{: shortdesc}

1. 调用受保护资源请求。
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
