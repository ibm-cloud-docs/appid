---

copyright:
  years: 2017, 2018
lastupdated: "2018-01-02"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


# 백엔드 리소스 보안 설정

{{site.data.keyword.appid_short_notm}} 서버 SDK를 사용하여 앱의 엔드포인트에 액세스하고 이를 보호할 수 있습니다. 또한 클라이언트 SDK를 사용하여 보호된 리소스에 액세스할 수도 있습니다.

**참고**: 필요한 경우에 보호된 리소스 호출로 로그인 위젯을 시작합니다. 올바른 토큰이 이미 확보된 경우, 로그인 위젯이 시작되지 않으며 리소스에 직접 액세스합니다.

## Liberty for Java의 리소스 보호
{: #protecting-liberty}

{{site.data.keyword.appid_short_notm}}를 사용하여 IBM Liberty for Java 앱에서 엔드포인트를 보호할 수 있습니다. Liberty for Java에는 OIDC(Open ID Connect) 요청을 처리하기 위한 내장 기능이 있습니다.

시작하기 전에:
* 기존의 바인드 해제된 [IBM Liberty for Java 앱](https://console.bluemix.net/catalog/starters/liberty-for-java)이 필요합니다. 
Liberty for Java 앱 개발에 친숙해지려면 [앱](/docs/runtimes/liberty/index.html)을 참조하십시오.
* [Apache Maven](https://maven.apache.org/download.cgi)이 설치되어 있는지 확인하십시오.
* Liberty for Java에서 OIDC가 작동하는 방법을 학습하십시오.

리소스 보호:

1. UI에서 Liberty for Java 샘플을 다운로드하십시오. 샘플에는 표준 Liberty 파일의 Zip 파일이 포함되어 있습니다.
2. 샘플의 압축이 풀린 디렉토리에서 터미널을 여십시오.
3. Cloud Foundry 명령행을 사용하여 {{site.data.keyword.Bluemix_notm}}에 로그인하십시오. 프롬프트가 나타나면 신임 정보를 입력하십시오.

  ```
  cf login
  ```
  {: codeblock}

4. 앱을 배치하십시오. 다음 명령을 실행하면 tenantid와 관련된 이름의 Liberty for Java 인스턴스가 작성됩니다.

  ```
  cf push
  ```
  {: codeblock}

5. 서비스 인스턴스를 새 Liberty for Java 인스턴스에 바인드하고 앱을 재배치하십시오.
6. 브라우저에서 앱을 열고 신임 정보를 사용하여 로그인하여 인증 활동을 검토하십시오.

## Node.js의 리소스 보호
{: #protecting-resources-nodesdk}

{{site.data.keyword.appid_short_notm}} 서버 SDK는 {{site.data.keyword.Bluemix_notm}}에 배치된 백엔드 앱에 사용된 ApiStrategy 패스포트 전략을 제공합니다. 권한이 없는 액세스에서 앱을 보호하려면 ApiStrategy로 Node.js 서버를 인스트루먼트해야 합니다. `appid-serversdk-nodejs npm module`은 {{site.data.keyword.appid_short_notm}}에서 발행한 액세스 토큰 및 ID 토큰의 유효성을 검증하도록 검증 방법과 ApiStrategy 패스포트 전략을 제공합니다.

{{site.data.keyword.appid_short_notm}} 서버 SDK는 <a href="http://passportjs.org/" target="_blank">Passport 프레임워크 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 사용하여 권한 부여를 실행합니다.

다음 스니펫은 `/protected` 엔드포인트 GET 메소드를 보호하기 위해
단순 Express 앱에서 `APIStrategy`를 사용하는 방법을 보여줍니다.

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


## iOS Swift SDK로 보호된 리소스에 액세스
{: #requesting-swift}

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
{: #requesting-android}

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
