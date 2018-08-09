---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:tip: .tip}

# 사인인 환경 브랜드화
{: #branding}

사용자 정의된 화면을 표시하고 {{site.data.keyword.appid_full}}의 인증 및 권한 부여 기능을 활용할 수 있습니다. 클라우드 디렉토리를 ID 제공자로 사용하면 지원을 덜 받으면서 사용자가 앱과 상호 작용할 수 있습니다. 사용자는 도움을 요청하지 않고도 사인인할 수 있습니다.
{: shortdesc}

자체 화면을 사용하는 경우에는 [Resource Owner Password Credentials flow](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html)를 사용하여 액세스 및 ID 토큰을 제공할 수 있습니다. 


## Android SDK로 사용자 정의된 화면 표시
{: #branded-ui-android}

클라우드 디렉토리를 사용하면 Android SDK로 사용자 정의된 화면을 호출할 수 있습니다.  <a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="blank">이 블로그를 체크아웃하십시오! <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>
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
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
            //User authenticated
          }
         });
  ```
  {: pre}

</br>
</br>

## iOS Swift SDK로 사용자 정의된 화면 표시
{: #branded-ui-ios-swift}

클라우드 디렉토리가 사용되는 경우에는 iOS Swift SDK로 사용자 정의된 화면을 호출할 수 있습니다.
{: shortdesc}

</br>
**사인인**

1. GUI의 ID 제공자 탭에서 클라우드 디렉토리를 **설정**으로 지정하십시오.
2. 리소스 소유자 비밀번호를 사용하여 로그인하십시오. 액세스 및 ID 토큰은 사용자가 자신의 사용자 이름과 비밀번호를 사용하여 로그인을 시도할 때 가져옵니다. 
  ```swift
  class delegate : TokenResponseDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
      //User authenticated
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
      //Exception occurred
      }
  }

  AppID.sharedInstance.obtainTokensWithROP(username: username, password: password, delegate: delegate())
  ```
  {: pre}


</br>
</br>

## Node.js SDK로 사용자 정의된 화면 표시
{: #branded-ui-nodejs}

클라우드 디렉토리를 사용하면 Node.js SDK로 사용자 정의된 화면을 호출할 수 있습니다. 
{: shortdesc}

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

