---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-09"

keywords: Authentication, authorization, identity, app security, secure, development, sign in, sign up, password, social, enterprise

subcollection: appid

---

{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}


# 로그인 위젯 사용
{: #login-widget}

{{site.data.keyword.appid_full}}를 사용할 경우 로그인 위젯이라는 기본 UI를 통해 애플리케이션 사용자가 사인인할 때 사용할 ID 제공자를 선택할 수 있습니다. Cloud Directory를 사용 중인 경우 로그인 위젯은 등록, 비밀번호 찾기, 다단계 인증 등의 추가 기능에 사용할 있는 UI도 추가로 제공합니다.
{: shortdesc}


## 로그인 위젯에 대한 정보
{: #widget-understanding}

로그인 위젯의 가장 뛰어난 부분 중 하나는 사용자가 자체 인증 UI를 구현하기 전에 {{site.data.keyword.appid_short_notm}}를 사용할 수 있다는 점입니다. 따라서 개발자의 온보딩 경험이 훨씬 쉬워집니다.

### 기본 로그인 위젯 동작은 무엇입니까?
{: #widget-default}

기본적으로 로그인 위젯에서는 Facebook, Google 및 Cloud Directory를 사용할 수 있습니다. 구성하려는 ID 제공자를 옵션으로 선택하여 언제든지 동작을 변경할 수 있습니다. 둘 이상의 ID 제공자가 사용으로 설정된 경우 로그인 위젯은 사용자가 자신의 ID 제공자를 선택할 수 있는 화면을 표시합니다. 그러나 하나의 제공자가 사용으로 설정된 경우 앞에서 언급한 선택 화면이 표시되지 않습니다. ID 제공자로 직접 이동되어 사인인 프로세스가 시작됩니다.

예를 들어 기본값(Facebook, Google, Cloud Directory)을 사용 중인 경우 사용자에게 화면이 표시됩니다. Facebook만 사용으로 설정할 경우 인증을 위해 Facebook으로 직접 이동됩니다.



### 각각의 제공자에 대해 표시할 수 있는 화면은 무엇입니까?
{: #widget-options}

Cloud Directory를 사용할 경우, {{site.data.keyword.appid_short_notm}}는 사용자 관리의 확장 기능을 제공할 수 있습니다. 확장 기능은 로그인 위젯 기능에도 적용됩니다. Cloud Directory에 저장된 사용자는 로그인 위젯에서 직접 등록 또는 비밀번호 재설정 등의 기능을 활용할 수 있습니다. 각 유형의 ID 제공자에 대해 표시할 수 있는 화면을 보려면 다음의 표를 체크아웃하십시오.

<table>
  <thead>
    <tr>
      <th>로그인 위젯 화면</th>
      <th>소셜 ID 제공자</th>
      <th>엔터프라이즈 ID 제공자</th>
      <th>Cloud Directory</th>
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


## 로그인 위젯 사용자 정의
{: #widget-customize}

로그인 위젯은 동적입니다. 룩앤필 또는 ID 제공자 구성을 사용자 정의할 수 있으며 변경사항은 즉시 적용됩니다. 애플리케이션 코드를 업데이트하거나 애플리케이션을 재배치하지 않아도 됩니다!
{: shortdesc}

로그인 위젯이 제공하는 것보다 더 많은 사용자 정의가 필요합니까? 사용자 사인인, 등록, 비밀번호 재설정 및 기타 플로우에 대해 완전히 사용자 정의된 사용자 고유의 UI를 구현하여 자신의 앱에 고유한 환경을 만들 수 있습니다. 시작하려면 [앱 브랜드화](/docs/services/appid?topic=appid-branded)를 확인하십시오.
{: tip}

화면을 사용자 정의하려면 다음을 수행하십시오.

1. {{site.data.keyword.appid_short_notm}} 서비스 대시보드를 여십시오.
2. **로그인 사용자 정의** 섹션을 선택하십시오. 회사의 브랜드에 맞추어 로그인 위젯의 모양을 수정할 수 있습니다.
3. 로컬 시스템에서 PNG 또는 JPG 파일을 선택하여 회사의 로고를 업로드하십시오. 권장하는 이미지 크기는 320 x 320픽셀입니다. 최대 파일 크기는 100KB입니다.
4. 색상 선택도구에서 위젯에 대한 헤더 색상을 선택하거나 다른 색상의 16진 코드를 입력하십시오.
5. 미리보기 분할창을 확인하고 사용자 정의 내용에 만족하면 **변경사항 저장**을 클릭하십시오. 확인 메시지가 표시됩니다.
6. 브라우저에서 로그인 페이지를 새로 고쳐서 변경사항을 확인하십시오.


## Android SDK를 사용하여 로그인 위젯 표시
{: #widget-display-android}

[Android 클라이언트 SDK](https://github.com/ibm-cloud-security/appid-clientsdk-android)를 사용하여 사전 구성된 화면을 호출할 수 있습니다.
{: shortdesc}

코드에 다음 명령을 입력하십시오.

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
{: codeblock}

</br>

### 등록
{: #widget-android-signup}

1. GUI에서 Cloud Directory [설정](/docs/services/appid?topic=appid-cloud-directory#cd-settings)을 구성하십시오. **사용자가 앱에 등록할 수 있도록 허용** 및 **사용자가 앱에서 해당 계정을 관리할 수 있도록 허용**을 둘 다 **켜기**로 설정하십시오.
2. 앱에 다음 코드를 추가하십시오. 사용자가 사용자 정의 화면에서 앱에 등록하면 등록 플로우가 시작됩니다. 다음 호출은 사용자를 등록할 뿐만 아니라 Cloud Directory 구성에 따라 등록을 완료하기 위한 검증 이메일도 발송합니다.

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
  {: codeblock}

</br>

### 비밀번호 찾기
{: #widget-android-forgot-password}

1. GUI에서 Cloud Directory [설정](/docs/services/appid?topic=appid-cloud-directory#cd-settings)을 구성하십시오. **사용자가 앱에서 해당 계정을 관리할 수 있도록 허용**을 **켜기**로 설정해야 합니다.
2. 서비스 대시보드의 **비밀번호 재설정** 탭에서 **비밀번호 찾기 이메일**이 **켜기**로 설정되어 있는지 확인하십시오.
3. 앱에 다음 코드를 추가하십시오. 사용자가 애플리케이션에서 "비밀번호 찾기"를 클릭하면 SDK에서 비밀번호 찾기 API를 호출하여 사용자에게 비밀번호를 재설정할 수 있도록 해주는 이메일을 발송합니다.

  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launchForgotPassword(this, new AuthorizationListener() {
      @Override
   	public void onAuthorizationFailure (AuthorizationException exception) {
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
  {: codeblock}

</br>

### 세부사항 변경
{: #widget-android-change-details}

1. GUI에서 Cloud Directory [설정](/docs/services/appid?topic=appid-cloud-directory#cd-settings)을 구성하십시오. **사용자가 앱에 등록할 수 있도록 허용** 및 **사용자가 앱에서 해당 계정을 관리할 수 있도록 허용**을 둘 다 **켜기**로 설정하십시오.
2. 서비스 대시보드의 **비밀번호 변경** 탭에서 **비밀번호 변경 이메일**을 켜기로 설정하십시오.
3. 로그인 위젯을 호출하여 세부사항 변경 플로우를 시작하십시오.

  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launchChangeDetails(this, new AuthorizationListener() {
      @Override
      public void onAuthorizationFailure (AuthorizationException exception) {
          // Exception occurred
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
  {: codeblock}

</br>

### 비밀번호 변경
{: #widget-android-change-password}

1. GUI에서 Cloud Directory [설정](/docs/services/appid?topic=appid-cloud-directory#cd-settings)을 구성하십시오. **사용자가 앱에 등록할 수 있도록 허용** 및 **사용자가 앱에서 해당 계정을 관리할 수 있도록 허용**을 둘 다 **켜기**로 설정하십시오.
2. 앱에 다음 코드를 배치하여 비밀번호 변경 플로우를 시작하십시오.

  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launchChangePassword(this, new AuthorizationListener() {
      @Override
      public void onAuthorizationFailure (AuthorizationException exception) {
          // Exception occurred
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
  {: codeblock}



## iOS Swift SDK를 사용하여 로그인 위젯 표시
{: #widget-display-ios-swift}

[iOS Swift 클라이언트 SDK](https://github.com/ibm-cloud-security/appid-clientsdk-swift)를 사용하여 사전 구성된 화면을 호출할 수 있습니다.
{: shortdesc}

코드에 다음 명령을 입력하십시오.

  ```swift
  import IBMCloudAppID
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
  {: codeblock}

</br>

### 등록
{: #widget-ios-signup}

1. GUI에서 Cloud Directory [설정](/docs/services/appid?topic=appid-cloud-directory#cd-settings)을 구성하십시오. **사용자가 앱에 등록할 수 있도록 허용** 및 **사용자가 앱에서 해당 계정을 관리할 수 있도록 허용**을 둘 다 **켜기**로 설정하십시오.
2. 애플리케이션에 다음 코드를 배치하십시오. 사용자가 애플리케이션에 등록하려고 시도하면 로그인 위젯이 호출되고 사용자 정의 등록 페이지가 표시됩니다.

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
  {: codeblock}

</br>

### 비밀번호 찾기
{: #widget-ios-forgot-password}

1. GUI에서 Cloud Directory [설정](/docs/services/appid?topic=appid-cloud-directory#cd-settings)을 구성하십시오. **사용자가 앱에서 해당 계정을 관리할 수 있도록 허용**을 **켜기**로 설정해야 합니다.
2. 서비스 대시보드의 **비밀번호 재설정** 탭에서 **비밀번호 찾기 이메일**이 **켜기**로 설정되어 있는지 확인하십시오.
3. 애플리케이션에 다음 코드를 배치하십시오. 앱 사용자 중 한 명이 비밀번호를 업데이트하도록 요청하면 로그인 위젯이 호출되고 프로세스가 시작됩니다.

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
  {: codeblock}

</br>

### 세부사항 변경
{: #widget-ios-change-details}

1. GUI에서 Cloud Directory [설정](/docs/services/appid?topic=appid-cloud-directory#cd-settings)을 구성하십시오. **사용자가 앱에 등록할 수 있도록 허용** 및 **사용자가 앱에서 해당 계정을 관리할 수 있도록 허용**을 둘 다 **켜기**로 설정하십시오.
2. 서비스 대시보드의 **비밀번호 변경** 탭에서 **비밀번호 변경 이메일**을 켜기로 설정하십시오.
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
  {: codeblock}

</br>

### 비밀번호 변경
{: #widget-ios-change-password}

1. GUI에서 Cloud Directory [설정](/docs/services/appid?topic=appid-cloud-directory#cd-settings)을 구성하십시오. **사용자가 앱에 등록할 수 있도록 허용** 및 **사용자가 앱에서 해당 계정을 관리할 수 있도록 허용**을 둘 다 **켜기**로 설정하십시오.
2. 앱에 다음 코드를 배치하여 비밀번호 변경 플로우를 시작하십시오.

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
  {: codeblock}


## Node.js SDK를 사용하여 로그인 위젯 표시
{: #widget-display-nodejs}

[Node.js 서버 SDK](https://github.com/ibm-cloud-security/appid-serversdk-nodejs)를 사용하여 사전 구성된 화면을 호출할 수 있습니다.
{: shortdesc}

사용자 이름과 비밀번호 매개변수로 호출할 수 있는 사후 라우트를 앱에 추가하고 리소스 소유자 비밀번호를 사용하여 로그인하십시오.

  ```javascript
  app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true // allow flash messages
  }));
  ```
  {: codeblock}

`WebAppStrategy`를 사용하여 사용자는 사용자 이름과 비밀번호로 웹 앱에 사인인할 수 있습니다. 로그인에 성공한 후에 사용자의 액세스 토큰은 HTTP 세션에 저장되며 세션 중에 사용 가능합니다. HTTP 세션이 영구 삭제되거나 만료되면 토큰이 유효하지 않게 됩니다.
{: tip}

</br>

### 등록
{: #widget-nodejs-signup}

1. GUI에서 Cloud Directory [설정](/docs/services/appid?topic=appid-cloud-directory#cd-settings)을 구성하십시오. **사용자가 앱에 등록할 수 있도록 허용** 및 **사용자가 앱에서 해당 계정을 관리할 수 있도록 허용**을 둘 다 **켜기**로 설정하십시오.
2. 애플리케이션에 다음 코드를 배치하십시오. 사용자가 애플리케이션에 등록하려고 시도하면 로그인 위젯이 호출되고 사용자 정의 등록 페이지가 표시됩니다.

  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: codeblock}

</br>

### 비밀번호 찾기
{: #widget-nodejs-forgot-password}

1. GUI에서 Cloud Directory [설정](/docs/services/appid?topic=appid-cloud-directory#cd-settings)을 구성하십시오. **사용자가 앱에서 해당 계정을 관리할 수 있도록 허용**을 **켜기**로 설정해야 합니다.
2. 서비스 대시보드의 **비밀번호 재설정** 탭에서 **비밀번호 찾기 이메일**이 **켜기**로 설정되어 있는지 확인하십시오.
3. 애플리케이션에 다음 코드를 배치하여 *show* 특성을 `WebAppStrategy.FORGOT_PASSWORD`에 전달하십시오. 사용자가 앱의 비밀번호를 업데이트하도록 요청하면 로그인 위젯이 호출되고 프로세스가 시작됩니다.

  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: codeblock}

</br>

### 세부사항 변경
{: #widget-nodejs-change-details}

1. GUI에서 Cloud Directory [설정](/docs/services/appid?topic=appid-cloud-directory#cd-settings)을 구성하십시오. **사용자가 앱에 등록할 수 있도록 허용** 및 **사용자가 앱에서 해당 계정을 관리할 수 있도록 허용**을 둘 다 **켜기**로 설정하십시오.
2. 서비스 대시보드의 **비밀번호 변경** 탭에서 **비밀번호 변경 이메일**을 켜기로 설정하십시오.
3. 애플리케이션에 다음 코드를 배치하여 *show* 특성을 `WebAppStrategy.FORGOT_PASSWORD`에 전달함으로써 세부사항 변경 양식을 실행하십시오.

  ```javascript
  app.get("/change_details", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_DETAILS
  }));
  ```
  {: codeblock}

</br>

### 비밀번호 변경
{: #widget-nodejs-change-password}

1. GUI에서 Cloud Directory [설정](/docs/services/appid?topic=appid-cloud-directory#cd-settings)을 구성하십시오. **사용자가 앱에 등록할 수 있도록 허용** 및 **사용자가 앱에서 해당 계정을 관리할 수 있도록 허용**을 둘 다 **켜기**로 설정하십시오.
2. 서비스 대시보드의 **비밀번호 변경** 탭에서 **비밀번호 변경 이메일**을 켜기로 설정하십시오.
3. 애플리케이션에 다음 코드를 배치하여 *show* 특성을 `WebAppStrategy.FORGOT_PASSWORD`에 전달함으로써 세부사항 변경 양식을 실행하십시오.

  ```javascript
  app.get("/change_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_PASSWORD
  }));
  ```
  {: codeblock}
