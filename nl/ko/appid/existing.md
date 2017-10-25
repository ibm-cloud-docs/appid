---

copyright:
  years: 2017
lastupdated: "2017-06-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# 기존 앱에 {{site.data.keyword.appid_short_notm}} 추가

사용자에 대한 프로파일 정보를 인증하고 저장하기 위해 기존 애플리케이션과 함께 {{site.data.keyword.appid_full}}를 사용할 수 있습니다.


## 전제조건

* 기존 iOS Swift, Android, Node.js 또는 Swift 애플리케이션.
* {{site.data.keyword.appid_short_notm}}의 기존 인스턴스. 


## 기존 Android 앱에 {{site.data.keyword.appid_short_notm}} 추가

앱 ID 서비스를 기존 Android 애플리케이션에 추가할 수 있습니다.

1. 루트 build.gradle 파일에 JitPack 저장소를 추가하십시오.

  ```gradle
    allprojects {
	    repositories {
		    ...
         	 maven { url 'https://jitpack.io' }
	    }
    }
  ```
  {: pre}

2. 사용자의 애플리케이션에 해당하는 build.gradle 파일을 열고 파일의 종속성 섹션을 찾아서 {{site.data.keyword.appid_short_notm}} 클라이언트 SDK에 대한 컴파일 종속성을 추가하십시오. 

  ```gradle
   dependencies {
       compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:1.+'
   }
  ```
  {: pre}

3. defaultConfig 섹션을 찾아서 다음의 코드 행을 추가하십시오. 

  ```gradle
  defaultConfig {
  ...
            manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
  ```
  {: pre}

4. 프로젝트를 Gradle과 동기화하십시오. 
5. initialize 메소드에 컨텍스트, 테넌트 ID 및 지역 매개변수를 전달하여 클라이언트 SDK를 초기화하십시오. 필수는 아니지만 일반적으로 초기화 코드를 넣는 위치는 Android 애플리케이션에서 기본 활동의 onCreate 메소드에 있습니다. 

  ```Java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, <AppID.REGION>);
  ```
  {: pre}

  <table>
  <caption> 표 1. 명령 컴포넌트 설명</caption>
    <tr>
      <th> 컴포넌트</th>
      <th> 설명 </th>
    </tr>
    <tr>
      <td> <i> tenantID </i> </td>
      <td> 서비스 대시보드의 **서비스 신임 정보** 탭에서 **신임 정보 보기**를 클릭하여 이 값을 찾을 수 있습니다. </td>
    </tr>
    <tr>
      <td> <i> AppID.REGION </i> </td>
      <td> UI에서 지역을 찾을 수 있습니다. 옵션은 `AppID.REGION_US_SOUTH`, `AppID.REGION_UK` 또는 `AppID.REGION_Sydney`입니다. </td>
    </tr>
  </table>

6. {{site.data.keyword.appid_short_notm}} 클라이언트 SDK가 초기화된 후에 로그인 위젯을 실행하여 사용자를 인증할 수 있습니다. 

  ```Java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launch(this, new AuthorizationListener() {
          @Override
          public void onAuthorizationFailure (AuthorizationException exception) {
          }

          @Override
          public void onAuthorizationCanceled () {
          }

          @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
          }
        });
  ```
  {: pre}

  <table>
  <caption> 표 2. 명령 컴포넌트 설명</caption>
    <tr>
      <th> 컴포넌트</th>
      <th> 설명 </th>
    </tr>
    <tr>
      <td> <i> onAuthorizationFailure </i> </td>
      <td> 예외가 발생했습니다. </td>
    </tr>
    <tr>
      <td> <i> onAuthorizationCanceled </i> </td>
      <td> 사용자가 인증 프로세스를 취소했습니다. </td>
    </tr>
    <tr>
      <td> <i> onAuthorizationSuccess </i> </td>
      <td> 사용자가 인증되었습니다. </td>
    </tr>
  </table>

## 기존 iOS Swift 앱에 {{site.data.keyword.appid_short_notm}} 추가

1. 프로젝트의 디렉토리에서 podfile을 여십시오. 
2. 프로젝트의 대상 아래에 'BluemixAppID' 팟(pod)에 대한 종속성을 추가하십시오. `use_frameworks!` 명령도 대상 아래에 있는지 확인하십시오. 
3. `BluemixAppID` 종속성을 다운로드하려면 다음 명령을 실행하십시오. 

  ```
  pod install --repo-update
  ```
  {: pre}

4. Xcode 프로젝트를 열고 키 체인 공유를 사용 설정하십시오. **프로젝트 설정** 아래에서 **기능** > **키 체인 공유**를 클릭하십시오.
5. **프로젝트 설정** > **정보** > **URL 유형** 아래에 **URL 유형**을 추가하십시오. **ID** 텍스트 상자 및 **URL 체계** 텍스트 상자를 모두 다음 값으로 채우십시오. 

  ```
  $(PRODUCT_BUNDLE_IDENTIFIER)
  ```
  {: pre}

6. AppDelegate.swift 파일에 다음 가져오기를 추가하십시오.

  ```swift
  import BluemixAppID
  import BMSCore
  ```
  {: pre}

7. initialize 메소드에 테넌트 ID 및 지역 매개변수를 전달하여 클라이언트 SDK를 초기화하십시오. 필수는 아니지만 일반적으로 초기화 코드를 넣는 위치는 application:didFinishLaunchingWithOptions: 사용자의 애플리케이션에서 AppDelegate의 메소드에 있습니다. 

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, bluemixRegion: <AppID.Region>)
  ```
  {: pre}

  <table>
  <caption> 표 3. 명령 컴포넌트 설명</caption>
    <tr>
      <th> 컴포넌트</th>
      <th> 설명 </th>
    </tr>
    <tr>
      <td> <i> tenantID </i> </td>
      <td> 서비스 대시보드의 **서비스 신임 정보** 탭에서 **신임 정보 보기**를 클릭하여 이 값을 찾을 수 있습니다. </td>
    </tr>
    <tr>
      <td> <i> AppID.REGION </i> </td>
      <td> UI에서 지역을 찾을 수 있습니다. 옵션은 `AppID.REGION_US_SOUTH`, `AppID.REGION_UK` 또는 `AppID.REGION_Sydney`입니다. </td>
    </tr>
  </table>

8. AppDelegate 파일에 다음 코드를 추가하십시오. 

  ```swift
  func application(_ application: UIApplication, open url: URL, options :[UIApplicationOpenURLOptionsKey : Any]) -> Bool {
          return AppID.sharedInstance.application(application, open: url, options: options)
      }
  class delegate : AuthorizationDelegate {
     public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, response:Response?) {
     }

     public func onAuthorizationCanceled() {
     }

     public func onAuthorizationFailure(error: AuthorizationError) {
     }
  }

  AppID.sharedInstance.loginWidget?.launch(delegate: delegate())
  ```
  {: pre}
  <table>
  <caption> 표 4. 명령 컴포넌트 설명</caption>
    <tr>
      <th> 컴포넌트</th>
      <th> 설명 </th>
    </tr>
    <tr>
      <td> <i> onAuthorizationSuccess </i> </td>
      <td> 사용자가 인증되었습니다. </td>
    </tr>
    <tr>
      <td> <i> onAuthorizationCanceled </i> </td>
      <td> 사용자가 인증 프로세스를 취소했습니다. </td>
    </tr>
    <tr>
      <td> <i> onAuthorizationFailure </i> </td>
      <td> 예외가 발생했습니다. </td>
    </tr>
  </table>

## 기존 Node.js 앱에 {{site.data.keyword.appid_short_notm}} 추가

1. `bluemix-appid` 모듈을 Node.js 애플리케이션에 추가하십시오. 

  ```javaScript
  npm install --save bluemix-appid
  ```
  {: pre}

2. 다음 모듈이 아직 설치되지 않은 경우 설치하십시오. 

  ```javaScript
  npm install --save express
  npm install --save passport
  npm install --save express-session
  ```
  {: pre}

3. 다음 코드를 app.js 파일에 추가하십시오. 
    * express-session 미들웨어를 사용하도록 express 앱을 설정하십시오. **참고**: 프로덕션 환경에 적합한 세션 스토리지로 미들웨어를 구성해야 합니다. 자세한 정보는 [expressjs 문서](https://github.com/expressjs/session)를 참조하십시오.
    * 직렬화 및 직렬화 해제로 passportjs를 구성하십시오. 이는 HTTP 요청 전체에 걸쳐 인증된 세션 지속성에 필요합니다. 자세한 정보는 [passportjs 문서](http://passportjs.org/docs)를 참조하십시오.
    * 콜백 URL에서 get 명령을 실행하여 앱 ID 서비스에서 액세스 및 ID 토큰을 검색하십시오.

  ```javaScript
  const express = require("express");
  const session = require("express-session");
  const passport = require("passport");
  const WebAppStrategy = require("bluemix-appid").WebAppStrategy;
  const app = express();
  const CALLBACK_URL = "/ibm/bluemix/appid/callback";
  app.use(session({
      secret: "123456",
      resave: true,
      saveUninitialized: true
    }));
  app.use(passport.initialize());
    app.use(passport.session());

    passport.use(new WebAppStrategy());
  passport.serializeUser(function(user, cb) {
      cb(null, user);
    });

    passport.deserializeUser(function(obj, cb) {
      cb(null, obj);
    });
  app.get(CALLBACK_URL, passport.authenticate(WebAppStrategy.STRATEGY_NAME));
  app.get("/protected", passport.authenticate(WebAppStrategy.STRATEGY_NAME), function(req, res)
    		res.json(req.user);
    });
  ```
  {: pre}

    **참고**: 서비스는 다음 순서로 경로 재지정됩니다. 
    1. `WebAppStrategy.ORIGINAL_URL` 키 아래에서 HTTP 세션에서 지속된 대로 인증 프로세스를 트리거한 요청의 원래 URL.
    2. `passport.authenticate(name, {successRedirect: "...."})`에 지정된 대로 성공적인 경로 재지정
    3. 애플리케이션 루트("/")

4. 애플리케이션을 재배치하십시오. 


## 기존 Swift 웹 애플리케이션에 {{site.data.keyword.appid_short_notm}} 추가

1. Swift 앱의 디렉토리에서 `Package.swift` 파일을 열고 `appid-serversdk-swift` 종속성을 추가하십시오. 예를 들면 다음과 같습니다. 

    ```swift
  import PackageDescription

  let package = Package(
      dependencies: [
          .Package(url: "https://github.com/ibm-cloud-security/appid-serversdk-swift.git", majorVersion: 1)
      ]
  )
    ```
    {: pre}

2. 다음 코드를 Swift 애플리케이션에 추가하십시오. 
    * 세션 미들웨어를 사용하도록 Kitura를 설정하십시오. **참고**: 프로덕션 환경에 적합한 세션 스토리지로 Kitura를 구성해야 합니다. 자세한 정보는 [Kitura 문서](https://github.com/IBM-Swift/Kitura-Session)를 참조하십시오.
    * 콜백 URL에서 get 명령을 실행하여 앱 ID 서비스에서 액세스 및 ID 토큰을 검색하십시오.

  ```swift
  import Foundation
  import Kitura
  import KituraSession
  import Credentials
  import SwiftyJSON
  import BluemixAppID
  let router = Router()
  let session = Session(secret: "Some secret")
  router.all(middleware: session)
  let webappKituraCredentialsPlugin = WebAppKituraCredentialsPlugin()
  let kituraCredentials = Credentials()
  kituraCredentials.register(plugin: webappKituraCredentialsPlugin)
  router.get(CALLBACK_URL,
    handler: kituraCredentials.authenticate(credentialsType: webappKituraCredentialsPlugin.name,
      successRedirect: LANDING_PAGE_URL,
      failureRedirect: LANDING_PAGE_URL
      ))
  router.get("/protected", handler: kituraCredentials.authenticate(credentialsType: webappKituraCredentialsPlugin.name), { (request, response, next) in
    let appIdAuthContext:JSON? = request.session?[WebAppKituraCredentialsPlugin.AuthContext]
      let identityTokenPayload:JSON? = appIdAuthContext?["identityTokenPayload"]
    guard appIdAuthContext?.dictionary != nil, identityTokenPayload?.dictionary != nil else {
      response.status(.unauthorized)
          return next()
      }

      response.send(json: identityTokenPayload!)
      next()
  })
  ```
  {: pre}

  <table>
  <caption> 표 6. 명령 컴포넌트 설명</caption>
    <tr>
      <th> 컴포넌트</th>
      <th> 설명 </th>
    </tr>
    <tr>
      <td> <i> var CALLBACK_URL </i> </td>
      <td> /ibm/bluemix/appid/callback </td>
    </tr>
    <tr>
      <td> <i> var LANDING_PAGE_URL </i> </td>
      <td> /index.html </td>
    </tr>
    </table>

5. 애플리케이션을 재배치하십시오. 



## {{site.data.keyword.Bluemix_notm}}에서 실행되지 않는 기존 애플리케이션에 {{site.data.keyword.appid_short_notm}} 추가


Bluemix에서 실행되지 않는 Node.js 또는 Swift 애플리케이션이 있는 경우, 원격에서 작업하도록 WebAppStrategy 또는 WebAppKituraCredentialsPlugin을 구성할 수 있습니다.


Node.js 앱에서 `passport.use(new WebAppStrategy());`을 다음 코드로 바꾸십시오. 

  ```javaScript
  passport.use(new WebAppStrategy({
    	  tenantId: "{tenant-id}",
   	    clientId: "{client-id}",
      	secret: "{secret}",
      	oauthServerUrl: "{oauth-server-url}",
      	redirectUri: "{app-url}" + CALLBACK_URL
      }));
  ```
{: pre}

Swift 앱에서 `let webappKituraCredentialsPlugin = WebAppKituraCredentialsPlugin()`를 다음 코드로 바꾸십시오.

  ```swift
  let options = [
        "clientId": "{client-id}",
  	"secret": "{secret}",
  	"tenantId": "{tenant-id}",
  	"oauthServerUrl": "{oauth-server-url}",
  	"redirectUri": "{app-url}" + CALLBACK_URL
  ]
  let webappKituraCredentialsPlugin = WebAppKituraCredentialsPlugin(options: options)
  ```
  {: pre}

<table>
<caption> Table 7. Swift 및 Node.js 앱에 대한 명령 컴포넌트 설명 </caption>
  <tr>
    <th> 컴포넌트</th>
    <th> 설명 </th>
  </tr>
  <tr>
    <td> <i> tenantID </i> </br> <i> clientID </i> </br> <i> secret </i> </br> <i> oauth-server-url </i> </br> </td>
    <td> 서비스 대시보드의 **서비스 신임 정보** 탭에서 **신임 정보 보기**를 클릭하여 이러한 값을 찾을 수 있습니다. </td>
  </tr>
  <tr>
    <td> <i> app-url </i> </td>
    <td> 애플리케이션 URL입니다. </td>
  </tr>
  <tr>
    <td> <i> CALLBACK_URL </i> </td>
    <td> 사용자가 로그인한 후에 보는 페이지의 URL입니다. </td>
  </tr>
</table>
