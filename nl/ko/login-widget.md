---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-09"

---

{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:pre: .pre}
{:new_window: target="blank"}
{:shortdesc: .shortdesc}


# 기본 화면 표시
{: #default}

{{site.data.keyword.appid_full}}는 사용자에게 안전한 사인인 옵션을 제공할 수 있도록 하는 로그인 위젯을 제공합니다.
{: shortdesc}

ID 제공자를 사용하도록 앱이 구성된 경우, 앱 방문자는 로그인 위젯에 의해 사인인 화면으로 경로 지정됩니다. 기본적으로, 하나의 제공자만 **설정**으로 지정된 경우에는 방문자가 해당 ID 제공자 인증 화면으로 경로 재지정됩니다. 로그인 위젯으로 기본 사인인 화면을 표시하거나, 클라우드 디렉토리로 기존 UI의 화면을 재사용할 수 있습니다. 이와 더불어 어떤 방식으로든 소스 코드를 변경하지 않고도 언제든지 사인인 플로우를 업데이트할 수 있습니다!


서비스는 OAuth 2 권한 부여 유형을 사용하여 권한 부여 프로세스를 맵핑합니다. Facebook 등의 소셜 ID 제공자를 구성할 때는 [Oauth2 Authorization Grant flow](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html)를 사용하여 로그인 위젯을 호출합니다.

앱에 고유한 환경을 작성하고 싶으십니까? [사용자 고유의 화면을 가져올](/docs/services/appid/branded.html) 수 있습니다!
{: tip}


## 기본 사인인 화면의 사용자 정의
{: #login-widget}

선택한 로고와 색상을 표시하도록 사전 구성된 사인인 화면을 사용자 정의할 수 있습니다.
{: shortdesc}

화면을 사용자 정의하려면 다음을 수행하십시오.

1. {{site.data.keyword.appid_short_notm}} 서비스 대시보드를 여십시오.
2. **로그인 사용자 정의** 섹션을 선택하십시오. 회사의 브랜드에 맞추어 로그인 위젯의 모양을 수정할 수 있습니다.
3. 로컬 시스템에서 PNG 또는 JPG 파일을 선택하여 회사의 로고를 업로드하십시오. 권장하는 이미지 크기는 320 x 320픽셀입니다. 최대 파일 크기는 100KB입니다.
4. 색상 선택도구에서 위젯에 대한 헤더 색상을 선택하거나 다른 색상의 16진 코드를 입력하십시오.
5. 미리보기 분할창을 확인하고 사용자 정의 내용에 만족하면 **변경사항 저장**을 클릭하십시오. 확인 메시지가 표시됩니다.
6. 브라우저에서 로그인 페이지를 새로 고쳐서 변경사항을 확인하십시오.


## 표시할 화면 계획
{: #plan}

{{site.data.keyword.appid_short_notm}}는 표시할 자체 UI 화면이 없을 때 호출할 수 있는 기본 로그인 화면을 제공합니다.
{: shortdesc}

ID 제공자 구성에 따라 표시 가능한 화면은 서로 다릅니다. 사용자 계정 정보에 대한 액세스 권한이 없으므로, 서비스는 소셜 ID 제공자에 대한 고급 기능을 제공하지 않습니다. 사용자는 ID 제공자로 이동하여 자체 정보를 관리해야 합니다. 예를 들어, 자체 Facebook 비밀번호를 변경하려는 경우에 사용자는 www.facebook.com으로 이동해야 합니다.

각 유형의 ID 제공자에 대해 표시할 수 있는 화면을 보려면 다음의 표를 체크아웃하십시오.

<table>
  <thead>
    <tr>
      <th>표시 화면</th>
      <th>소셜 ID 제공자</th>
      <th>엔터프라이즈 ID 제공자</th>
      <th>클라우드 디렉토리</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>사인인</td>
      <td><img src="images/confirm.png" width="32" alt="사용 가능한 기능" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="사용 가능한 기능" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="사용 가능한 기능" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>등록</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="사용 가능한 기능" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>비밀번호 찾기</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="사용 가능한 기능" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>비밀번호 변경</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="사용 가능한 기능" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>계정 세부사항</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="사용 가능한 기능" style="width:32px;" /></td>
    </tr>
  </tbody>
</table>

[소셜 ID 제공자](/docs/services/appid/identity-providers.html) 및 [클라우드 디렉토리](/docs/services/appid/cloud-directory.html)에 대한 설정을 구성한 후에는 다음 이미지에서 원하는 언어를 클릭하여 코드 구현을 시작하십시오.


제공된 SDK 또는 API 중 하나를 사용하려면 이미지를 클릭하십시오. 잊지 마십시오. 다른 언어로도 App ID를 활용할 수 있습니다. API를 사용하여 앱에서 클라우드 디렉토리를 설정할 수 있습니다. 이미지에 나열되지 않은 언어에 대한 도움을 받으려면
<a href="https://www.ibm.com/blogs/bluemix/tag/app-id/" target="_blank">IBM Cloud 블로그 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 확인하십시오.
{: shortdesc}

</br>

## Android SDK로 기본 화면 표시
{: #android}

Android SDK로 사전 구성된 화면을 호출할 수 있습니다.
{: shortdesc}

</br>

**사인인**
1. 코드에 다음 명령을 두십시오.
    ```java
    LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launch(this, new AuthorizationListener() {
          @Override
          public void onAuthorizationFailure (AuthorizationException exception) {
            //Exception occurred
     }

          @Override
          public void onAuthorizationCanceled () {
            //Authentication canceled by the user
          }

@Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
            //User authenticated
          }
        });
    ```
  {: pre}

</br>
**등록**

1. 클라우드 디렉토리 설정에서 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용**을 **설정**으로 지정하십시오.
2. LoginWidget을 호출하여 등록 플로우를 시작하십시오.
  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launchSignUp(this, new AuthorizationListener() {
  		 @Override
  		 public void onAuthorizationFailure (AuthorizationException exception) {
  		 }

  		 @Override
  		 public void onAuthorizationCanceled () {
  		 }

  		 @Override
  		 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
  			 if (accessToken != null && identityToken != null) {
  			 } else {
  			 }

  		 }
  	 });
  ```
  {: pre}

</br>
**비밀번호 찾기**

1. 클라우드 디렉토리 설정에서 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용** 및 **비밀번호 이메일 찾기**를 **설정**으로 지정하십시오.
2. LoginWidget을 사용하여 비밀번호 찾기 플로우를 시작하십시오.
    ```java
    LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launchForgotPassword(this, new AuthorizationListener() {
   			 @Override
		public void onAuthorizationFailure(AuthorizationException exception) {
   			 }

   			 @Override
		public void onAuthorizationCanceled() {
   			 }

   			 @Override
   			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
   			 }
   		 });
    ```
    {: pre}

</br>
**계정 세부사항**

1. 클라우드 디렉토리 설정에서 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용**을 **설정**으로 지정하십시오.
2. LoginWidget을 호출하여 세부사항 변경 플로우를 시작하십시오.
   ```java
   LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
   loginWidget.launchChangeDetails(this, new AuthorizationListener() {
  			 @Override
  			 public void onAuthorizationFailure (AuthorizationException exception) {
  			 }

  			 @Override
  			 public void onAuthorizationCanceled () {
  			 }

  			 @Override
  			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
  			 }
  		 });
   ```
   {: pre}

</br>
**비밀번호 변경**

1. 클라우드 디렉토리 설정에서 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용**을 **설정**으로 지정하십시오.
2. LoginWidget을 호출하여 비밀번호 변경 플로우를 시작하십시오.
   ```java
    LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launchChangePassword(this, new AuthorizationListener() {
   			 @Override
   			 public void onAuthorizationFailure (AuthorizationException exception) {
   			 }

   			 @Override
   			 public void onAuthorizationCanceled () {
   			 }

   			 @Override
   			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
   			 }
   		 });
   ```
   {: pre}
</br>
</br>

## iOS Swift SDK로 기본 화면 표시
{: #ios-swift}

iOS Swift SDK로 사전 구성된 화면을 호출할 수 있습니다.
{: shortdesc}

</br>
**사인인**

1. 코드에 다음 명령을 두십시오.
  ```swift
  import BluemixAppID
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, refreshToken: RefreshToken?) {
          //User authenticated
      }

      public func onAuthorizationCanceled() {
          //Authentication canceled by the user
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          //Exception occurred
      }
  }

  AppID.sharedInstance.loginWidget?.launch(delegate: delegate())
  ```
  {: pre}


</br>
**등록**

1. 클라우드 디렉토리 설정에서 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용**을 **설정**으로 지정하십시오.
2. LoginWidget을 호출하여 등록 플로우를 시작하십시오.
  ```swift
  class delegate : AuthorizationDelegate {
    public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?) {
       if accessToken == nil && identityToken == nil {
        //email verification is required
        return
       }
     //User authenticated
    }

    public func onAuthorizationCanceled() {
        //Sign up canceled by the user
    }

    public func onAuthorizationFailure(error: AuthorizationError) {
        //Exception occurred
    }
  }

  AppID.sharedInstance.loginWidget?.launchSignUp(delegate: delegate())
  ```
  {: pre}

</br>
**비밀번호 찾기**

1. 클라우드 디렉토리 설정에서 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용** 및 **비밀번호 이메일 찾기**를 **설정**으로 지정하십시오.
2. LoginWidget을 사용하여 비밀번호 찾기 플로우를 시작하십시오.
  ```swift
  class delegate : AuthorizationDelegate {
     public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?) {
        //forgot password finished, in this case accessToken and identityToken will be null.
     }

     public func onAuthorizationCanceled() {
         //forgot password canceled by the user
     }

     public func onAuthorizationFailure(error: AuthorizationError) {
         //Exception occurred
     }
  }

  AppID.sharedInstance.loginWidget?.launchForgotPassword(delegate: delegate())
  ```
  {: pre}

</br>
**계정 세부사항**

1. 클라우드 디렉토리 설정에서 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용**을 **설정**으로 지정하십시오.
2. LoginWidget을 호출하여 세부사항 변경 플로우를 시작하십시오.
  ```swift

   class delegate : AuthorizationDelegate {
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?) {
       }

       public func onAuthorizationCanceled() {
       }

       public func onAuthorizationFailure(error: AuthorizationError) {
       }
   }

   AppID.sharedInstance.loginWidget?.launchChangeDetails(delegate: delegate())
  ```
  {: pre}

</br>
**비밀번호 변경**

1. 클라우드 디렉토리 설정에서 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용**을 **설정**으로 지정하십시오.
2. LoginWidget을 호출하여 비밀번호 변경 플로우를 시작하십시오.
  ```swift
   class delegate : AuthorizationDelegate {
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?) {
       }

       public func onAuthorizationCanceled() {
       }

       public func onAuthorizationFailure(error: AuthorizationError) {
       }
    }

    AppID.sharedInstance.loginWidget?.launchChangePassword(delegate: delegate())
  ```
  {: pre}
</br>
</br>

## Node.js SDK로 기본 화면 표시
{: #nodejs}

Node.js SDK로 사전 구성된 화면을 호출할 수 있습니다.
{: shortdesc}

</br>
**사인인**
1. ID 제공자 설정에서 클라우드 디렉토리를 **설정**으로 지정하고 콜백 엔드포인트를 지정하십시오.
2. 사용자 이름과 비밀번호 매개변수로 호출할 수 있는 사후 라우트를 앱에 추가하고 리소스 소유자 비밀번호를 사용하여 로그인하십시오.
    ```javascript
    app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
    	successRedirect: LANDING_PAGE_URL,
    	failureRedirect: ROP_LOGIN_PAGE_URL,
    	failureFlash : true // allow flash messages
    }));
    ```
    {: pre}
    `WebAppStrategy`를 사용하여 사용자는 사용자 이름과 비밀번호로 웹 앱에 로그인할 수 있습니다. 로그인에 성공한 후에 사용자의 액세스 토큰은 HTTP 세션에 저장되며 세션 중에 사용 가능합니다. 일단 HTTP 세션이 영구 삭제되거나 만료되면 토큰이 더 이상 유효하지 않습니다.
    {: tip}

</br>
**등록**

1. 클라우드 디렉토리 설정에서 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용**을 **설정**으로 지정하십시오. '아니오'로 설정되면 액세스 및 ID 토큰을 검색하지 않고 프로세스가 종료됩니다.
2. WebAppStrategy `show` 특성을 전달하고 `WebAppStrategy.SIGN_UP`으로 설정하십시오.
  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: pre}

</br>
**비밀번호 찾기**

1. 클라우드 디렉토리 설정에서 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용** 및 **비밀번호 이메일 찾기**를 **설정**으로 지정하십시오. '아니오'로 설정되면 액세스 및 ID 토큰을 검색하지 않고 프로세스가 종료됩니다.
2. WebAppStrategy `show` 특성을 전달하고 `WebAppStrategy.FORGOT_PASSWORD`로 설정하십시오.
  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: pre}

</br>
**계정 세부사항**
1. 클라우드 디렉토리 설정에서 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용**을 **설정**으로 지정하십시오.
2. WebAppStrategy `show` 특성을 전달하고 `WebAppStrategy.CHANGE_DETAILS`로 설정하십시오.
  ```javascript
  app.get("/change_details", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_DETAILS
  }));
  ```
  {: pre}

</br>
**비밀번호 변경**
1. 클라우드 디렉토리 설정에서 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용**을 **설정**으로 지정하십시오.
2. WebAppStrategy `show` 특성을 전달하고 `WebAppStrategy.CHANGE_PASSWORD`로 설정하십시오.
  ```javascript
  app.get("/change_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_PASSWORD
  }));
  ```
  {: pre}

</br>
</br>

## Swift SDK로 기본 화면 표시
{: #swift}

소셜 ID 제공자가 사용되는 경우에는 Swift SDK로 사전 구성된 사인인 화면을 호출할 수 있습니다.
{: shortdesc}

1. 다음의 코드는 Kitura 앱에서 WebAppKituraCredentialsPlugin을 사용하여 `/protected` 엔드포인트를 보호하는 방법을 보여줍니다.

  ```swift
  import Foundation
  import Kitura
  import KituraSession
  import Credentials
  import SwiftyJSON
  import BluemixAppID

  // The following URLs will be used for AppID OAuth flows
  var LOGIN_URL = "/ibm/bluemix/appid/login"
  var CALLBACK_URL = "/ibm/bluemix/appid/callback"
  var LOGOUT_URL = "/ibm/bluemix/appid/logout"
  var LANDING_PAGE_URL = "/index.html"

  // Setup Kitura to use session middleware
  // Must be configured with proper session storage for production
  // environments. See https://github.com/IBM-Swift/Kitura-Session for
  // additional documentation
  let router = Router()
  let session = Session(secret: "Some secret")
  router.all(middleware: session)

  let options = [
  	"clientId": "{client-id}",
  	"secret": "{secret}",
  	"tenantId": "{tenant-id}",
  	"oauthServerUrl": "{oauth-server-url}",
  	"redirectUri": "{app-url}" + CALLBACK_URL
  ]
  let webappKituraCredentialsPlugin = WebAppKituraCredentialsPlugin(options: options)
  let kituraCredentials = Credentials()
  kituraCredentials.register(plugin: webappKituraCredentialsPlugin)

  // Explicit login endpoint
  router.get(LOGIN_URL,
  		   handler: kituraCredentials.authenticate(credentialsType: webappKituraCredentialsPlugin.name,
  												   successRedirect: LANDING_PAGE_URL,
  												   failureRedirect: LANDING_PAGE_URL
  ))

  // Callback to finish the authorization process. Will retrieve access and identity tokens from AppID
  router.get(CALLBACK_URL,
  		   handler: kituraCredentials.authenticate(credentialsType: webappKituraCredentialsPlugin.name,
  												   successRedirect: LANDING_PAGE_URL,
  												   failureRedirect: LANDING_PAGE_URL
  ))

  // Logout endpoint. Clears authentication information from session
  router.get(LOGOUT_URL, handler:  { (request, response, next) in
  	kituraCredentials.logOut(request: request)
  	webappKituraCredentialsPlugin.logout(request: request)
  	_ = try? response.redirect(LANDING_PAGE_URL)
  })

  // Protected area
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
  var port = 3000
  if let portString = ProcessInfo.processInfo.environment["PORT"]{
      port = Int(portString)!
  }
  print("Starting on \(port)")

  // Add an HTTP server and connect it to the router
  Kitura.addHTTPServer(onPort: port, with: router)

  // Start the Kitura runloop (this call never returns)
  Kitura.run()
  ```
  {: codeblock}
</br>
</br>



