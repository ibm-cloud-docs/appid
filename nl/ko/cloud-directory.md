---

copyright:
  years: 2017
lastupdated: "2017-12-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# 클라우드 디렉토리 관리
{: #cd}

{{site.data.keyword.appid_short_notm}}를 구성하여 ID 제공자로 클라우드 디렉토리를 사용할 수 있습니다. 사용자가 이메일 및 비밀번호로 사인인하는 경우 디렉토리에 추가되고 서비스 GUI에서 사용자를 관리할 수 있습니다.
{: shortdesc}

<!--- What is a cloud directory? --->

## 디렉토리 설정 관리

앱에 대한 알림 및 사용자 제어의 레벨을 관리할 수 있습니다. GUI의 **디렉토리 설정** 탭에서 사용자가 수행할 셀프 서비스의 레벨을 결정할 수 있습니다. 

1. 사용자가 등록하는 데 이메일을 사용하도록 허용하려면 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용**을 **설정**으로 설정해야 합니다. **끄기**로 설정된 경우 콘솔을 통해 계속해서 사용자를 추가할 수 있으나, 이는 개발 목적으로만 가능합니다. 
2. 발신인 세부사항을 구성하십시오. 메시지를 전송할 이메일, 발신인으로 표시되는 사용자 및 사용자가 응답할 수 있는 대상을 지정하십시오. **참고**: 사용자가 링크를 클릭하는 데 충분한 시간을 지정하도록 조치 URL을 구성하는 시기를 확인하십시오. 사용자는 이메일에 비밀번호 재설정을 요청하는 기능과 같은 특정 옵션이 있는지 확인해야 합니다. 
3. 사용자가 수신하는 이메일의 유형 및 발신인 정보의 유형을 결정하십시오. 



## 메시지 관리

템플리트는 사용자에게 전송할 수 있는 이메일 메시지의 예제입니다. 메시지의 컨텐츠 및 레이아웃을 업데이트하여 템플리트를 사용자 정의할 수 있습니다. 디렉토리 설정 탭에서 이 메시지를 **설정** 또는 **해제**로 설정할 수 있습니다.

1. **메시지 유형**을 선택하십시오.
2. 메시지의 컨텐츠 및 디자인을 변경하여 메시지를 사용자 정의하십시오. 매개변수를 사용하여 메시지를 개인화할 수 있습니다. 변경사항을 저장하십시오!

### 메시지 유형

<dl>
  <dt> 환영 </dt>
    <dd>사용자가 애플리케이션에 등록한 후 이메일을 통해 사용자를 환영할 수 있습니다. 사용자를 환영하거나 보류하려면 최대한 메시지를 관련시키십시오. <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> 모든 유형의 메시지에 사용할 수 있는 매개변수 </th>
      </thead>
      <tbody>
        <tr>
          <td> %{display.logo} </td>
          <td> 로그인 위젯에 대해 구성한 이미지를 표시합니다. </td>
        </tr>
	 <tr>
          <td> %{display.headerColor} </td>
          <td> 로그인 위젯에 대해 구성한 헤더 색상을 표시합니다. </td>
        </tr>
        <tr>
          <td> %{user.displayName} </td>
          <td> 사용자가 앱과 상호작용할 때 사용하도록 선택한 화면 이름을 표시합니다. </td>
        </tr>
        <tr>
          <td> %{user.email} </td>
          <td> 사용자의 등록된 이메일 주소를 표시합니다. </td>
        </tr>
        <tr>
          <td> %{user.firstName} </td>
          <td> 사용자의 지정된 이름을 표시합니다. </td>
        </tr>
        <tr>
          <td> %{user.formattedName} </td>
          <td> 사용자의 전체 이름을 표시합니다. </td>
        </tr>
        <tr>
          <td> %{user.lastName} </td>
          <td> 사용자의 지정된 성을 표시합니다. </td>
        </tr>
      </tbody>
    </table>

    **참고**: 사용자가 매개변수로 수집된 정보를 제공하지 않는 경우 공백으로 표시됩니다. </dd>
  <dt> 비밀번호 찾기 </dt>
    <dd> 어떠한 이유로든 잊어버린 비밀번호를 재설정해야 하는지 또는 업데이트해야 하는지를 물어볼 수 있습니다. 요청에 대한 이메일 응답을 사용자 정의할 수 있습니다. 사용자가 변경을 요청한 경우 이메일의 링크를 클릭할 때까지 비밀번호는 변경되지 않습니다.

    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> 비밀번호 변경 매개변수 </th>
      </thead>
      <tbody>
        <tr>
          <td> %{linkExpiration.hours} </td>
          <td> 링크가 유효한 기간(시)을 표시합니다. </td>
        </tr>
        <tr>
          <td> %{linkExpiration.minutes} </td>
          <td> 링크가 유효한 기간(분)을 표시합니다. </td>
        </tr>
        <tr>
          <td> %{resetPassword.code} </td>
          <td> URL의 일부로 일회성 패스코드를 표시합니다. 이는 각 개인이 서로 다른 코드를 보유함을 의미합니다. 예를 들면, <code>https://appid-wfm.bluemix.net/verify/6574839563478</code>입니다. </td>
        </tr>
        <tr>
          <td> %{resetPassword.link} </td>
          <td> 비밀번호를 재설정하기 위해 사용자가 클릭하는 링크를 표시합니다. </td>
        </tr>
       </tbody>
    </table></dd>
  <dt> 검증 </dt>
    <dd> 사용자가 이메일을 통해 검증하도록 요청할 수 있습니다. 검증을 요청하여 앱에 등록할 수 있는 허위 계정의 수를 제한할 수 있습니다. 사용자가 이메일을 검증할 때까지 앱에 대한 액세스를 제한하거나 프로파일을 작성하는 사용자를 관리하는 방법으로 이를 사용할 수 있습니다. <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> 메시지 매개변수 검증 </th>
      </thead>
      <tbody>
        <tr>
          <td> %{linkExpiration.hours} </td>
          <td> 링크가 유효한 기간(시)을 표시합니다. </td>
        </tr>
        <tr>
          <td> %{linkExpiration.minutes} </td>
          <td> 링크가 유효한 기간(분)을 표시합니다. </td>
        </tr>
        <tr>
          <td> %{verify.code} </td>
          <td> 일회성 확인 URL을 표시합니다. </td>
        </tr>
        <tr>
          <td> %{verify.link} </td>
          <td> 설정에 지정한 조치 URL을 표시합니다. </td>
        </tr>
      </tbody>
    </table></dd>
  <dt> 비밀번호 변경 </dt>
    <dd> 비밀번호가 업데이트될 때 사용자에게 알릴 수 있습니다. 비밀번호 변경을 요청하지 않은 경우 유용합니다. 계정의 보안을 재설정하기 위한 적절한 단계를 수행할 수 있습니다. <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> 비밀번호 변경 매개변수 </th>
      </thead>
      <tbody>
        <tr>
          <td> %{passwordChangeInfo.time} </td>
          <td> 새 비밀번호가 적용된 시간을 표시합니다. </td>
        </tr>
        <tr>
          <td> %{passwordChangeInfo.ipAddress} </td>
          <td> 비밀번호 변경이 요청된 IP 주소를 표시합니다. </td>
        </tr>
      </tbody>
    </table></dd>
</dl>



## Android SDK로 클라우드 디렉토리 관리
{: #managing-android}

다음 API를 사용할 때 **클라우드 디렉토리 ID 제공자**를 **설정**으로 설정해야 합니다. 

### 리소스 소유자 비밀번호를 사용하여 로그인
일반 사용자의 사용자 이름 및 비밀번호를 제공하여 액세스 권한 및 ID 토큰을 얻을 수 있습니다. 

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

### 등록

클라우드 디렉토리의 설정에서 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용**을 **설정**으로 설정해야 합니다. 

 LoginWidget 클래스를 사용하여 등록 플로우를 시작하십시오. 
 ```java
 LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
 loginWidget.launchSignUp(this, new AuthorizationListener() {
			 @Override
		public void onAuthorizationFailure(AuthorizationException exception) {
			//Exception occurred
		}
	@Override
			 public void onAuthorizationCanceled () {
				 //Sign up canceled by the user
			 }

			 @Override
			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
				 if (accessToken != null && identityToken != null) {
				     //User authenticated
				 } else {
				     //email verification is required
				 }

			 }
		 });
 ```
 {: codeblock}

### 비밀번호 찾기
클라우드 디렉토리의 설정에서 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용** 및 **비밀번호 이메일 찾기**를 **설정**으로 설정해야 합니다. 

LoginWidget 클래스를 사용하여 비밀번호 찾기 플로우를 시작하십시오. 
  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launchForgotPassword(this, new AuthorizationListener() {
 			 @Override
 			 public void onAuthorizationFailure (AuthorizationException exception) {
 				 //Exception occurred
 			 }

 			 @Override
 			 public void onAuthorizationCanceled () {
 				 //forogt password canceled by the user
 			 }

 			 @Override
 			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
 				 //forgot password finished, in this case accessToken and identityToken will be null.

 			 }
 		 });
  ```
  {: codeblock}

### 세부사항 변경
클라우드 디렉토리의 설정에서 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용**을 **설정**으로 설정해야 합니다. LoginWidget 클래스를 사용하여 세부사항 변경 플로우를 시작하십시오. 사용자가 ID 제공자로 클라우드 디렉토리를 사용하여 로그인하는 경우에만 이 API를 사용할 수 있습니다. 
   ```java
   LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
   loginWidget.launchChangeDetails(this, new AuthorizationListener() {
  			 @Override
  			 public void onAuthorizationFailure (AuthorizationException exception) {
  				 //Exception occurred
  			 }

  			 @Override
  			 public void onAuthorizationCanceled () {
  				 //changed details canceled by the user
  			 }

  			 @Override
  			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
  				 //User authenticated, and fresh tokens received
  			 }
  		 });
   ```
   {: codeblock}

### 비밀번호 변경
클라우드 디렉토리의 설정에서 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용**을 **설정**으로 설정해야 합니다. 

LoginWidget 클래스를 사용하여 비밀번호 변경 플로우를 시작하십시오. 사용자가 ID 제공자로 클라우드 디렉토리를 사용하여 로그인하는 경우에만 이 API를 사용할 수 있습니다. 

   ```java
    LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launchChangePassword(this, new AuthorizationListener() {
   			 @Override
   			 public void onAuthorizationFailure (AuthorizationException exception) {
   				 //Exception occurred
   			 }

   			 @Override
   			 public void onAuthorizationCanceled () {
   				 //change password canceled by the user
   			 }

   			 @Override
   			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
   				   //User authenticated, and fresh tokens received
   			 }
   		 });
   ```
   {: codeblock}

## iOS Swift SDK로 클라우드 디렉토리 관리


### 리소스 소유자 비밀번호를 사용하여 로그인

일반 사용자의 사용자 이름 및 비밀번호를 제공하여 액세스 권한 및 ID 토큰을 얻을 수 있습니다. 
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

### 등록

클라우드 디렉토리의 설정에서 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용**을 **설정**으로 설정해야 합니다. 

LoginWidget 클래스를 사용하여 등록 플로우를 시작하십시오. 
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

### 비밀번호 찾기
클라우드 디렉토리의 설정에서 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용** 및 **비밀번호 이메일 찾기**를 **설정**으로 설정해야 합니다. 

LoginWidget 클래스를 사용하여 비밀번호 찾기 플로우를 시작하십시오. 
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

### 세부사항 변경

클라우드 디렉토리의 설정에서 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용**을 **설정**으로 설정해야 합니다. 

LoginWidget 클래스를 사용하여 세부사항 변경 플로우를 시작하십시오. 사용자가 ID 제공자로 클라우드 디렉토리를 사용하여 로그인하는 경우에만 이 API를 사용할 수 있습니다. 
  ```swift

   class delegate : AuthorizationDelegate {
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
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

### 비밀번호 변경

클라우드 디렉토리의 설정에서 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용**을 **설정**으로 설정해야 합니다. 

LoginWidget 클래스를 사용하여 비밀번호 변경 플로우를 시작하십시오. 사용자가 ID 제공자로 클라우드 디렉토리를 사용하여 로그인하는 경우에만 이 API를 사용할 수 있습니다. 
  ```swift
   class delegate : AuthorizationDelegate {
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
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


## Node.js SDK로 클라우드 디렉토리 관리
클라우드 디렉토리 ID 제공자가 **설정**으로 설정되어 있고 콜백 엔드포인트를 포함하는지 확인하십시오.

### 리소스 소유자 비밀번호 플로우를 사용하여 로그인
WebAppStrategy를 통해 사용자는 사용자 이름 및 비밀번호를 사용하여 웹 애플리케이션에 로그인할 수 있습니다.
로그인 후 사용자의 액세스 토큰이 HTTP 세션에서 지속되고 HTTP 세션이 활성 상태인 경우 사용 가능합니다. HTTP 세션이 영구 삭제되거나 만료되면 토큰도 영구 삭제됩니다. 

사용자가 사용자 이름 및 비밀번호를 사용하여 로그인할 수 있으려면 사용자 이름 및 비밀번호 매개변수로 호출할 사후 라우트에 앱을 추가하십시오. 

  ```javascript
  app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true // allow flash messages
  }));
  ```
  {: codeblock}

  <table>
    <thead>
      <th colspan=2><img src="images/idea.png"/> 이 명령 컴포넌트 이해</th>
    </thead>
    <tbody>
      <tr>
        <td><code> successRedirect </code></td>
        <td> 인증 후 사용자를 경로 재지정할 URL로 이 값을 설정하십시오. 기본값은 원래의 요청 URL입니다. 예를 들면, <code>/form/submit</code>입니다. </td>
      </tr>
      <tr>
        <td><code> failureRedirect </code></td>
        <td> 인증에 실패한 경우 사용자를 경로 재지정할 URL로 이 값을 설정하십시오. 기본값은 원래의 요청 URL입니다. </td>
      </tr>
      <tr>
        <td><code> failureFlash </code></td>
        <td> 클라우드 디렉토리에서 리턴된 오류 메시지를 수신하려면 이 값을 <code>true</code>로 설정하십시오. 기본값은 false입니다. </td>
      </tr>
     </tbody>
  </table>


**참고**:
  * HTML 양식을 사용하여 요청을 제출하는 경우 [body-parser](https://www.npmjs.com/package/body-parser) 미들웨어를 사용하십시오. 
  * 리턴된 오류 메시지를 가져오려면 [connect-flash](https://www.npmjs.com/package/connect-flash)를 사용하십시오. `web-app-sample-server.js`를 참조하십시오.

### 등록
{{site.data.keyword.appid_short_notm}} 등록 양식을 실행하려면 WebAppStrategy "show" 특성을 전달하고 `WebAppStrategy.SIGN_UP`으로 설정하십시오.
  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: codeblock}

    **참고**:
    * 클라우드 디렉토리 설정에서 **이메일 검증 없이 사용자가 사인인할 수 있도록 허용**을 **아니오**로 설정한 경우 {{site.data.keyword.appid_short_notm}} 액세스 권한 및 ID 토큰을 검색하지 않고 프로세스가 종료됩니다. 
    * 클라우드 디렉토리 설정에서 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용**을 **설정**으로 설정해야 합니다. 


### 비밀번호 찾기
{{site.data.keyword.appid_short_notm}} 비밀번호 찾기 양식을 실행하려면 WebAppStrategy `show` 특성을 전달하고 `WebAppStrategy.FORGOT_PASSWORD`로 설정하십시오.
  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: codeblock}

**참고**:
* 클라우드 디렉토리 설정에서 **이메일 검증 없이 사용자가 사인인할 수 있도록 허용**을 **아니오**로 설정한 경우 {{site.data.keyword.appid_short_notm}} 액세스 권한 및 ID 토큰을 검색하지 않고 프로세스가 종료됩니다. 
* 클라우드 디렉토리 설정에서 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용** 및 **비밀번호 이메일 찾기**를 **설정**으로 설정해야 합니다. 

### 세부사항 변경
{{site.data.keyword.appid_short_notm}} 세부사항 변경 양식을 실행하려면 WebAppStrategy `show` 특성을 전달하고 `WebAppStrategy.CHANGE_DETAILS`로 설정하십시오.
  ```javascript
  app.get("/change_details", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_DETAILS
  }));
  ```
  {: codeblock}

**참고**:
* ID 제공자로 클라우드 디렉토리를 사용하여 사용자를 인증해야 합니다. 
* 클라우드 디렉토리 설정에서 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용**을 **설정**으로 설정해야 합니다. 


### 비밀번호 변경
{{site.data.keyword.appid_short_notm}} 비밀번호 변경 양식을 실행하려면 WebAppStrategy `show` 특성을 전달하고 `WebAppStrategy.CHANGE_PASSWORD`로 설정하십시오.
  ```javascript
  app.get("/change_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_PASSWORD
  }));
  ```
  {: codeblock}

**참고**:
* ID 제공자로 클라우드 디렉토리를 사용하여 사용자를 인증해야 합니다. 
* 클라우드 디렉토리 설정에서 **사용자가 등록하고 비밀번호를 재설정할 수 있도록 허용**을 **설정**으로 설정해야 합니다. 
