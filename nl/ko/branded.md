---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:tip: .tip}

# 앱 브랜드화
{: #branding}

사용자 정의된 화면을 표시하고 {{site.data.keyword.appid_full}}의 인증 및 권한 부여 기능을 활용할 수 있습니다. 클라우드 디렉토리를 ID 제공자로 사용하면 사용자는 도움을 받지 않고 앱과 상호 작용할 수 있습니다. 사용자는 도움을 요청하지 않고도 사인인, 등록 및 자체 비밀번호 변경 등을 수행할 수 있습니다.
{: shortdesc}

자체 화면을 사용하는 경우에는 [Resource Owner Password Credentials flow](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html)를 사용하여 액세스 및 ID 토큰을 제공할 수 있습니다.


## iOS Swift SDK로 앱 브랜드화
{: #branded-ui-ios-swift}

클라우드 디렉토리가 사용되는 경우에는 iOS Swift SDK로 자체 브랜드화된 화면을 호출할 수 있습니다.
{: shortdesc}

</br>
**사인인**

1. GUI의 ID 제공자 탭에서 클라우드 디렉토리를 **설정**으로 지정하십시오.
2. 로그인 위젯을 호출하여 사인인 플로우를 시작하십시오. 사용자가 자신의 사용자 이름 또는 이메일과 비밀번호를 사용하여 로그인을 시도할 때 액세스 및 ID 토큰을 가져옵니다. 
  ```swift
  class delegate : TokenResponseDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
      //User authenticated
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
      //Exception occurred
      }
  }

  AppID.sharedInstance.signinWithResourceOwnerPassword(username: username, password: password, delegate: delegate())
  ```
  {: pre}

</br>

**등록**

1. GUI의 ID 제공자 탭에서 클라우드 디렉토리를 **설정**으로 지정하십시오.
2. 클라우드 디렉토리 설정에서 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용**을 **설정**으로 지정하십시오. 
3. 로그인 위젯을 호출하여 등록 플로우를 시작하십시오.
  ```swift
  class delegate : AuthorizationDelegate {
    public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
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

1. GUI의 ID 제공자 탭에서 클라우드 디렉토리를 **설정**으로 지정하십시오.
2. 클라우드 디렉토리 설정에서 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용**을 **설정**으로 지정하십시오. 
3. 로그인 위젯을 호출하여 비밀번호 찾기 플로우를 시작하십시오.
  ```swift
  class delegate : AuthorizationDelegate {
     public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
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

**세부사항 변경**

1. GUI의 ID 제공자 탭에서 클라우드 디렉토리를 **설정**으로 지정하십시오.
2. 클라우드 디렉토리 설정에서 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용**을 **설정**으로 지정하십시오. 
3. 로그인 위젯을 호출하여 세부사항 변경 플로우를 시작하십시오.
  ```swift
class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
         //User authenticated, and fresh tokens received
      }

      public func onAuthorizationCanceled() {
          //changed details canceled by the user
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          //Exception occurred
      }
  }

   AppID.sharedInstance.loginWidget?.launchChangeDetails(delegate: delegate())
  ```
  {: pre}

</br>

**비밀번호 변경**

1. GUI의 ID 제공자 탭에서 클라우드 디렉토리를 **설정**으로 지정하십시오.
2. 클라우드 디렉토리 설정에서 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용**을 **설정**으로 지정하십시오. 
3. 로그인 위젯을 호출하여 세부사항 변경 플로우를 시작하십시오.
  ```swift
class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
          //User authenticated, and fresh tokens received
      }

      public func onAuthorizationCanceled() {
          //change password canceled by the user
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
           //Exception occurred
      }
   }

    AppID.sharedInstance.loginWidget?.launchChangePassword(delegate: delegate())
  ```
  {: pre}

</br>


## Android SDK로 앱 브랜드화
{: #branded-ui-android}

클라우드 디렉토리를 사용하면 Android SDK로 사용자 정의된 화면을 호출할 수 있습니다. 사용자가 상호 작용할 수 있는 화면의 조합을 선택할 수 있습니다. 세부 예제는 <a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="blank">Check out this blog<img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>의 내용을 참조하십시오.
{: shortdesc}

</br>

**사인인**

1. ID 제공자로서 **클라우드 디렉토리**를 **설정**으로 지정하십시오.
2. 일반 사용자의 사용자 이름 및 비밀번호를 제공하여 액세스 ID 및 새로 고치기 토큰을 가져오십시오.
3. 로그인 위젯을 호출하여 사인인 플로우를 시작하십시오.
  ```java
  AppID.getInstance().signinWithResourceOwnerPassword(getApplicationContext(), username, password,
         new TokenResponseListener() {
      @Override
          public void onAuthorizationFailure (AuthorizationException exception) {
          //Exception occurred
      }

      @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          //User authenticated
          }
  });
  ```
  {: pre}

</br>

**등록**

1. ID 제공자로서 **클라우드 디렉토리**를 **설정**으로 지정하십시오.
2. 클라우드 디렉토리 설정에서 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용**을 **설정**으로 지정하십시오. 
3. 로그인 위젯을 호출하여 등록 플로우를 시작하십시오.
  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launchSignUp(this, new AuthorizationListener() {
      @Override
          public void onAuthorizationFailure (AuthorizationException exception) {
          //Exception occurred
      }

      @Override
          public void onAuthorizationCanceled () {
          //Sign up canceled by the user
      }

      @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          if (accessToken != null && identityToken != null) {
              //User authenticated
          } else {
              //email verification is required
          }
      }
  });
  ```
  {: pre}

</br>


**비밀번호 찾기**

1. ID 제공자로서 **클라우드 디렉토리**를 **설정**으로 지정하십시오.
2. 클라우드 디렉토리 설정에서 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용**을 **설정**으로 지정하십시오. 
3. 로그인 위젯을 호출하여 비밀번호 찾기 플로우를 시작하십시오.
  ```java
    LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launchForgotPassword(this, new AuthorizationListener() {
      @Override
		public void onAuthorizationFailure(AuthorizationException exception) {
          //Exception occurred
      }

      @Override
          public void onAuthorizationCanceled () {
          // Forogt password canceled by the user
      }

      @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          // Forgot password finished, in this case accessToken and identityToken will be null.
      }
  });
  ```
  {: pre}

</br>

**세부사항 변경**

1. ID 제공자로서 **클라우드 디렉토리**를 **설정**으로 지정하십시오.
2. 클라우드 디렉토리 설정에서 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용**을 **설정**으로 지정하십시오. 
3. 로그인 위젯을 호출하여 세부사항 변경 플로우를 시작하십시오.
  ```java
   LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
   loginWidget.launchChangeDetails(this, new AuthorizationListener() {
      @Override
          public void onAuthorizationFailure (AuthorizationException exception) {
          //Exception occurred
          }

      @Override
          public void onAuthorizationCanceled () {
          // Changed details canceled by the user
      }

      @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          // User authenticated, and fresh tokens received
      }
  });
  ```
  {: pre}


</br>

**비밀번호 변경**

1. ID 제공자로서 **클라우드 디렉토리**를 **설정**으로 지정하십시오.
2. 클라우드 디렉토리 설정에서 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용**을 **설정**으로 지정하십시오. 
3. 로그인 위젯을 호출하여 비밀번호 변경 플로우를 시작하십시오.
  ```java
    LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launchChangePassword(this, new AuthorizationListener() {
      @Override
          public void onAuthorizationFailure (AuthorizationException exception) {
          //Exception occurred
          }

      @Override
          public void onAuthorizationCanceled () {
          // Change password canceled by the user
      }

      @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          // User authenticated, and fresh tokens received
      }
  });
  ```
  {: pre}

</br>
</br>


## Node.js SDK로 앱 브랜드화
{: #branded-ui-nodejs}

클라우드 디렉토리가 사용되는 경우에는 Node.js SDK로 사용자 정의된 화면을 호출할 수 있습니다.
{: shortdesc}

**사인인**

사용자는 WebAppStrategy를 사용하여 사용자 이름과 비밀번호로 웹 앱에 사인인할 수 있습니다. 사용자가 앱에 성공적으로 로그인하면 액세스 토큰이 활성 상태로 유지되는 한 HTTP 세션에서 지속됩니다. HTTP 세션이 닫히거나 만료되면 액세스 토큰도 영구 삭제됩니다.
    

1. ID 제공자 설정에서 클라우드 디렉토리를 **설정**으로 지정하고 콜백 엔드포인트를 지정하십시오.
2. 사용자 이름과 비밀번호 매개변수로 호출할 수 있는 사후 라우트를 앱에 추가하고 리소스 소유자 비밀번호 플로우를 사용하여 사인인하십시오.
  ```javascript
    app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
    	failureRedirect: ROP_LOGIN_PAGE_URL,
    	failureFlash : true // allow flash messages
    }));
  ```
  {: pre}
  <table>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="자세한 정보 아이콘"/> 명령 매개변수 </th>
    </thead>
    <tbody>
      <tr>
        <td><code>successRedirect</code></td>
        <td>인증에 성공한 후 사용자를 경로 재지정할 URL입니다.</td>
      </tr>
      <tr>
        <td><code>failureRedirect</code></td>
        <td>인증에 실패하는 경우 사용자를 경로 재지정할 URL입니다.</td>
      </tr>
      <tr>
        <td><code>failureFlash</code></td>
        <td><code>true</code>로 설정된 경우 클라우드 디렉토리 서비스에서 오류 메시지가 리턴됩니다. 기본적으로 이 값은 <code>false</code>로 설정됩니다.</td>
      </tr>
    </tbody>
  </table>

  1. HTML 양식으로 요청을 제출하는 경우 [본문 구문 분석기](https://www.npmjs.com/package/body-parser) 미들웨어를 사용할 수 있습니다.
  2. [connect-flash](https://www.npmjs.com/package/connect-flash)를 사용하여 리턴된 오류 메시지를 가져올 수 있습니다. 자세한 정보는 [웹 앱 샘플](https://github.com/ibm-cloud-security/appid-serversdk-nodejs/blob/master/samples/web-app-sample.js)을 참조하십시오.
  {: tip}

</br>
**등록**

1. ID 제공자 설정에서 클라우드 디렉토리를 **설정**으로 지정하고 콜백 엔드포인트를 지정하십시오.
2. 클라우드 디렉토리 설정에서 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용**을 **설정**으로 지정하십시오. 
3. **사용자가 이메일 검증 없이 사인인할 수 있도록 허용**을 **아니오**로 설정하십시오. 그렇지 않으면 {{site.data.keyword.appid_short_notm}} 액세스 및 ID 토큰을 검색할 수 없습니다.
4. 사용자 이름과 비밀번호 매개변수로 호출할 수 있는 사후 라우트를 앱에 추가하고 리소스 소유자 비밀번호 플로우를 사용하여 사인인하십시오.
  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: pre}

</br>

**비밀번호 찾기**

1. ID 제공자 설정에서 클라우드 디렉토리를 **설정**으로 지정하고 콜백 엔드포인트를 지정하십시오.
2. 클라우드 디렉토리 설정에서 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용**을 **설정**으로 지정하십시오. 
3. **비밀번호 이메일 찾기**를 **설정**으로 지정하십시오.
4. *show* 특성을 `WebAppStrategy.FORGOT_PASSWORD`에 전달하여 비밀번호 찾기 양식을 시작하십시오.
  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: pre}

</br>

**세부사항 변경**

1. ID 제공자 설정에서 클라우드 디렉토리를 **설정**으로 지정하고 콜백 엔드포인트를 지정하십시오.
2. 클라우드 디렉토리 설정에서 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용**을 **설정**으로 지정하십시오. 
3. 사용자가 이미 {{site.data.keyword.appid_short_notm}}로 인증되었는지 확인하십시오.
4. *show* 특성을 `WebAppStrategy.CHANGE_DETAILS`에 전달하여 비밀번호 찾기 양식을 시작하십시오.
  ```javascript
  app.get("/change_details", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_DETAILS
  }));
  ```
  {: pre}

</br>

## API로 앱 브랜드화
{: #branded-ui-api}

사용자 정의된 화면을 표시하고 {{site.data.keyword.appid_short_notm}}의 인증 및 권한 부여 기능을 활용할 수 있습니다. 클라우드 디렉토리를 ID 제공자로 사용하면 사용자는 도움을 받지 않고 앱과 상호 작용할 수 있습니다. 사용자는 도움을 요청하지 않고도 사인인, 등록 및 자체 비밀번호 재설정 등을 수행할 수 있습니다.
{: shortdesc}

이를 가능하게 하도록 {{site.data.keyword.appid_short_notm}}에서 REST API를 공개합니다. REST API를 사용하면 웹 앱을 서비스하는 백엔드 서버를 빌드하거나 자체 사용자 정의 화면에서 모바일 앱과 상호작용할 수 있습니다.

관리 API는 IBM Cloud IAM(Identity and Access Management) 생성 토큰으로 보호됩니다. 이는 계정 소유자가 자체 팀의 어떤 구성원이 각 서비스 인스턴스에 대해 어떤 액세스 레벨을 보유하는지를 지정할 수 있음을 의미합니다. IAM 및 {{site.data.keyword.appid_short_notm}}가 함께 작동되는 방법에 대한 자세한 정보는 [서비스 액세스 관리](/docs/services/appid/iam.html)를 참조하십시오.

[설정](/docs/services/appid/cloud-directory.html)을 구성한 후 다음 엔드포인트를 호출하여 각 화면을 표시할 수 있습니다.


**등록**
`/sign_up` 엔드포인트를 사용하면 사용자가 앱에 자신을 등록할 수 있도록 허용할 수 있습니다.
요청 본문에서 다음 데이터를 제공하십시오.
  * tenantID.
  * 클라우드 디렉토리 사용자 데이터. 세부사항은 [SCIM 전체 사용자 표시](https://tools.ietf.org/html/rfc7643#section-8.2)를 참조하십시오.
    * `password` 속성.
    * `true`로 설정된 `primary` 속성의 이메일 배열에서, 최소한 1개의 이메일 주소가 있어야 합니다.

[이메일 구성](/docs/services/appid/cloud-directory.html)에 따라 사용자는 확인 요청을 받거나 앱에 등록 시에 환영 이메일을 받을 수 있습니다. 두 가지 유형의 이메일 모두 사용자가 앱에 등록할 때 트리거됩니다. 확인 이메일에는 **확인** 단추가 포함되어 있습니다. 단추를 누르고 자체 ID를 확인한 후에는 확인에 대해 감사하는 화면이 {{site.data.keyword.appid_short_notm}}에 의해 표시됩니다.  

사후 확인 페이지를 제시할 수 있습니다.

1. {{site.data.keyword.appid_short_notm}} 대시보드의 **사용자 정의 랜딩 페이지** 탭으로 이동하십시오.
2. **사용자 정의 이메일 주소 확인 페이지의 URL**에서 랜딩 페이지의 URL을 입력하십시오.

이 값이 제공된 경우, {{site.data.keyword.appid_short_notm}}는 `context` 조회와 함께 URL을 호출합니다. `/sign_up/confirmation_result` 엔드포인트를 호출하고 수신된 `context` 매개변수를 전달하면 결과에서 사용자가 자체 계정을 확인했는지 여부를 알려줍니다. 해당되는 경우에는 사용자 정의 페이지를 표시할 수 있습니다.

</br>
**비밀번호 찾기**

`/forgot_password` 엔드포인트를 사용하면 사용자가 자체 비밀번호를 잊은 경우에 이를 복구하도록 허용할 수 있습니다.

요청 본문에서 다음 데이터를 제공하십시오.
  * tenantID.
  * 클라우드 디렉토리 사용자의 이메일.

엔드포인트가 호출된 경우에는 비밀번호 재설정 이메일이 사용자에게 발송됩니다. 이메일에는 **재설정** 단추가 포함되어 있습니다. 사용자가 단추를 누르면 {{site.data.keyword.appid_short_notm}}에 의해 화면이 표시되며, 이를 사용하여 자체 비밀번호를 재설정할 수 있습니다.

사후 비밀번호 재설정 페이지를 제시할 수 있습니다.

1. {{site.data.keyword.appid_short_notm}} 대시보드의 **사용자 정의 랜딩 페이지** 탭으로 이동하십시오.
2. **사용자 정의 비밀번호 재설정 페이지의 URL**에서 랜딩 페이지의 URL을 입력하십시오.  

이 값이 제공된 경우, {{site.data.keyword.appid_short_notm}}는 `context` 조회와 함께 URL을 호출합니다. `context` 매개변수를 사용하면 `/forgot_password/confirmation_result`가 호출될 때 결과를 수신할 수 있습니다. 결과가 성공적이면 사용자 정의 페이지를 표시할 수 있습니다.

랜덤 문자열을 사용자 정의 비밀번호 재설정 페이지에 추가하고 요청이 제출되면 이를 백엔드에 전달하십시오. 핸들러가 문자열을 유효성 검증하도록 하고, 유효한 경우에만 `/change_password` 엔드포인트를 호출하십시오. 이를 수행하면 백엔드 비밀번호 재설정 엔드포인트의 취약성을 낮출 수 있습니다.
{: tip}

</br>
**비밀번호 변경**

두 가지 방법으로 `/change_password` 엔드포인트를 사용할 수 있습니다. 사용자가 재설정 요청을 제출하는 경우 또는 사용자가 앱에 사인인하고 자체 비밀번호를 업데이트하고자 하는 경우입니다.

재설정 요청 후 비밀번호를 업데이트하려면 요청 본문에서 다음 데이터를 제공하십시오.
  * tenantID.
  * 사용자 새 비밀번호.
  * 클라우드 디렉토리 사용자 UUID.
  * 선택사항: 비밀번호 재설정이 수행된 IP 주소. IP 주소 전달을 선택한 경우에는 비밀번호 변경 이메일 템플리트에 대해 `%{passwordChangeInfo.ipAddress}`  플레이스홀더가 사용 가능합니다.

구성에 따라서는 비밀번호가 변경될 때 {{site.data.keyword.appid_short_notm}}에 변경사항이 있었음을 알려주는 이메일을 사용자에게 발송할 수 있습니다.

</br>
앱에 사인인한 동안 사용자가 자체 비밀번호를 변경할 수 있도록 허용하려면 다음을 수행하십시오.

요청 본문에서 다음 데이터를 제공하십시오.
  * tenantID.
  * 사용자 새 비밀번호.
  * 클라우드 디렉토리 사용자 UUID.

비밀번호 변경 페이지가 사용자에게 현재 비밀번호와 새 비밀번호를 입력하도록 프롬프트를 표시해야 합니다.
{: tip}

백엔드는 ROP API로 사용자의 현재 비밀번호를 유효성 검증하며, 유효한 경우에는 새 비밀번호를 사용하여 엔드포인트를 호출합니다. 구성에 따라서는 비밀번호가 변경될 때 {{site.data.keyword.appid_short_notm}}에 변경사항이 있었음을 알려주는 이메일을 사용자에게 발송할 수 있습니다.

</br>
**재발송**

사용자가 어떤 이유로 인해 이메일을 받지 못한 경우에는 `/resend/{templateName}`을 사용하여 이메일을 재발송할 수 있습니다. 

요청 본문에서 다음 데이터를 제공하십시오.
  * tenantID.
  * 템플리트 이름.
  * 클라우드 디렉토리 사용자 UUID.


**세부사항 변경**

사용자가 앱에 사인인한 경우에는 일부 자체 정보를 업데이트할 수 있습니다. `/Users/{userId}`를 사용하여 해당 정보를 가져오고 업데이트할 수 있습니다.

사용자 세부사항이 업데이트되는 경우, 엔드포인트는 [SCIM 형식](https://tools.ietf.org/html/rfc7643#section-8.2)으로 요청 본문의 업데이트된 사용자 데이터를 가져옵니다. 반드시 관련 세부사항만 변경하십시오.

사용자의 이메일 주소는 변경할 수 없습니다.
{: tip}
