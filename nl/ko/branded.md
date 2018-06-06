---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 사인인 환경 브랜드화
{: #branding}

{{site.data.keyword.appid_full}}의 인증 및 권한 부여 기능을 활용하면서 사용자 정의된 고유 UI를 표시할 수 있습니다. 클라우드 디렉토리를 ID 제공자로 사용하면 지원을 덜 받으면서 사용자가 앱과 상호 작용할 수 있습니다. 도움을 요청하지 않고도 사인인, 등록, 비밀번호 변경 등의 작업을 수행할 수 있습니다.
{: shortdesc}

클라우드 디렉토리를 ID 제공자로 사용하면 [리소스 소유자 비밀번호 비밀번호 신임 정보 플로우](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html)를 사용하여 액세스와 ID 토큰을 제공합니다.

**참고**: 클라우드 디렉토리가 구성된 유일한 옵션인 경우에만 사용자 정의된 사인인 페이지를 가져올 수 있습니다. 다른 ID 제공자가 **설정**으로 지정된 경우 사전 구성된 사인인 화면이 표시됩니다.

## Android SDK로 사용자 정의된 화면 표시
{: #branded-ui-android}

클라우드 디렉토리를 사용하면 Android SDK로 사용자 정의된 화면을 호출할 수 있습니다. 사용자가 상호 작용할 수 있게 할 화면 조합을 선택할 수 있습니다. <a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="blank">블로그를 확인하십시오! <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>
{: shortdesc}

</br>
**사인인**

1. ID 제공자로서 **클라우드 디렉토리**를 **설정**으로 지정하십시오.
2. 코드에 다음 명령을 두십시오.
  ```java
  AppID.getInstance().obtainTokensWithROP(getApplicationContext(), username, password,
         new TokenResponseListener() {
         @Override
          public void onAuthorizationFailure (AuthorizationException exception) {
             //Exception occurred
          }

          @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
            //User authenticated
          }
         });
  ```
  {: codeblock}

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
  		 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
  			 if (accessToken != null && identityToken != null) {
  			 } else {
  			 }

  		 }
  	 });
  ```
  {: codeblock}

</br>
**비밀번호 찾기**

1. 클라우드 디렉토리 설정에서 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용** 및 **비밀번호 이메일 찾기**를 **설정**으로 지정하십시오.
2. LoginWidget을 사용하여 비밀번호 찾기 플로우를 시작하십시오.
    ```java
    LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launchForgotPassword(this, new AuthorizationListener() {
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
    {: codeblock}

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
  			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
  			 }
  		 });
   ```
   {: codeblock}

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
   			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
   			 }
   		 });
   ```
   {: codeblock}

</br>
</br>

## iOS Swift SDK로 사용자 정의된 화면 표시
{: #branded-ui-ios-swift}

클라우드 디렉토리를 사용하면 ios Swift SDK로 사용자 정의된 화면을 호출할 수 있습니다. 사용자가 상호 작용할 수 있게 할 화면 조합을 선택할 수 있습니다.
{: shortdesc}

</br>
**사인인**

1. GUI의 ID 제공자 탭에서 클라우드 디렉토리를 **설정**으로 지정하십시오.
2. 리소스 소유자 비밀번호를 사용하여 로그인하십시오. 일반 사용자의 사용자 이름 및 비밀번호를 제공하여 액세스 권한 및 ID 토큰을 얻을 수 있습니다.
  ```swift
  class delegate : TokenResponseDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
      //User authenticated
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
      //Exception occurred
      }
  }

  AppID.sharedInstance.obtainTokensWithROP(username: username, password: password, delegate: delegate())
  ```
  {: codeblock}

</br>
**등록**

1. 클라우드 디렉토리 설정에서 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용**을 **설정**으로 지정하십시오.
2. LoginWidget을 호출하여 등록 플로우를 시작하십시오.
  ```swift
  class delegate : AuthorizationDelegate {
    public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
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
  {: codeblock}

</br>
**비밀번호 찾기**

1. 클라우드 디렉토리 설정에서 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용** 및 **비밀번호 이메일 찾기**를 **설정**으로 지정하십시오.
2. LoginWidget을 사용하여 비밀번호 찾기 플로우를 시작하십시오.
  ```swift
  class delegate : AuthorizationDelegate {
     public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
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
  {: codeblock}

</br>
**계정 세부사항**

1. 클라우드 디렉토리 설정에서 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용**을 **설정**으로 지정하십시오.
2. LoginWidget을 호출하여 세부사항 변경 플로우를 시작하십시오.
  ```swift

   class delegate : AuthorizationDelegate {
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
       }

       public func onAuthorizationCanceled() {
       }

       public func onAuthorizationFailure(error: AuthorizationError) {
       }
   }

   AppID.sharedInstance.loginWidget?.launchChangeDetails(delegate: delegate())
  ```
  {: codeblock}

</br>
**비밀번호 변경**

1. 클라우드 디렉토리 설정에서 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용**을 **설정**으로 지정하십시오.
2. LoginWidget을 호출하여 비밀번호 변경 플로우를 시작하십시오.
  ```swift
   class delegate : AuthorizationDelegate {
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
       }

       public func onAuthorizationCanceled() {
       }

       public func onAuthorizationFailure(error: AuthorizationError) {
       }
    }

    AppID.sharedInstance.loginWidget?.launchChangePassword(delegate: delegate())
  ```
  {: codeblock}

</br>

## Node.js SDK로 사용자 정의된 화면 표시
{: #branded-ui-nodejs}

클라우드 디렉토리를 사용하면 Node.js SDK로 사용자 정의된 화면을 호출할 수 있습니다. 사용자가 상호 작용할 수 있게 할 화면 조합을 선택할 수 있습니다.
{: shortdesc}

**사인인**
1. ID 제공자 설정에서 클라우드 디렉토리를 **설정**으로 지정하고 콜백 엔드포인트를 지정하십시오.
2. 사용자 이름과 비밀번호 매개변수로 호출할 수 있는 사후 라우트를 앱에 추가하고 리소스 소유자 비밀번호를 사용하여 로그인하십시오.
    **참고**: `WebAppStrategy`를 사용하면 사용자 이름과 비밀번호로 웹 앱에 로그인할 수 있습니다. 성공적으로 로그인하고 나면 사용자의 액세스 토큰이 HTTP 세션에 저장되고 세션 기간 동안 사용 가능합니다. HTTP 세션이 영구 삭제되거나 만료되면 토큰이 더 이상 유효하지 않습니다.
    ```javascript
    app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
    	successRedirect: LANDING_PAGE_URL,
    	failureRedirect: ROP_LOGIN_PAGE_URL,
    	failureFlash : true // allow flash messages
    }));
    ```
    {: codeblock}

</br>
**등록**

1. 클라우드 디렉토리 설정에서 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용**을 **설정**으로 지정하십시오. 아니오로 설정되면 액세스와 ID 토큰을 검색하지 않고 프로세스가 종료됩니다.
2. WebAppStrategy `show` 특성을 전달하고 `WebAppStrategy.SIGN_UP`으로 설정하십시오.
  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: codeblock}

</br>
**비밀번호 찾기**

1. 클라우드 디렉토리 설정에서 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용** 및 **비밀번호 이메일 찾기**를 **설정**으로 지정하십시오. 아니오로 설정되면 액세스와 ID 토큰을 검색하지 않고 프로세스가 종료됩니다.
2. WebAppStrategy `show` 특성을 전달하고 `WebAppStrategy.FORGOT_PASSWORD`로 설정하십시오.
  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: codeblock}

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
  {: codeblock}

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
  {: codeblock}
