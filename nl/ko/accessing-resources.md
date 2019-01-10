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


# 모바일 앱에서 보호된 리소스에 액세스
{: #access-backend}

{{site.data.keyword.appid_full}} 클라이언트 SDK를 사용하여 앱의 엔드포인트에 액세스할 수 있습니다.
{: shortdesc}


## iOS Swift SDK로 보호된 리소스에 액세스
{: #accessing-swift}

{{site.data.keyword.appid_short_notm}} iOS Swift SDK를 사용하여 iOS Swift 앱의 엔드포인트에 액세스할 수 있습니다.
{: shortdesc}

1. BMSCore를 가져오십시오.
  ```swift
  import BMSCore
  ```
  {: codeblock}

2. 보호된 리소스 요청을 호출하십시오.
  ```swift
  BMSClient.sharedInstance.initialize(bluemixRegion: AppID.<region>)
  BMSClient.sharedInstance.authorizationManager = AppIDAuthorizationManager(appid:AppID.sharedInstance)
  var request:Request =  Request(url: "<your protected resource url>")
  request.send(completionHandler: {(response:Response?, error:Error?) in
      //code handling the response here
  })
  ```
  {: codeblock}


## Android SDK로 보호된 리소스에 액세스
{: #accessing-android}

{{site.data.keyword.appid_short_notm}} Android SDK를 사용하여 Android 앱의 엔드포인트에 액세스할 수 있습니다.
{: shortdesc}

1. 보호된 리소스 요청을 호출하십시오.
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
