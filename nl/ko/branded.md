---

copyright:
  years: 2017, 2018
lastupdated: "2018-10-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:tip: .tip}

# 앱 브랜드화
{: #branding}

고유한 사용자 정의 화면을 표시하고 고유한 사인인 플로우를 사용하여 {{site.data.keyword.appid_full}}의 인증 및 권한 기능을 활용할 수 있습니다. 사용자는 클라우드 디렉토리를 ID 제공자로 사용하여 더 적은 도움을 받으면서 앱과 상호작용할 수 있습니다. 사용자는 도움을 요청하지 않고도 사인인, 등록 및 자체 비밀번호 변경 등을 수행할 수 있습니다.
{: shortdesc}

**고유한 화면을 표시하는 이유가 무엇입니까?**

기존 UI를 재사용하는 경우 앱에 대한 일관성 있는 사인인 플로우를 작성할 수 있습니다. 동일한 이미지, 색상 및 브랜드를 사용하면 사용자가 앱과 직접 상호작용하지 않는 경우에도 더 쉽게 브랜드를 인식할 수 있습니다.

</br>

**고유한 화면을 표시하기 위해 어떤 유형의 구성이 필요합니까?**

고유한 UI를 표시하려면 [클라우드 디렉토리(/docs/services/appid/cloud-directory.html)]를 ID 제공자로 사용해야 합니다. 클라우드 디렉토리를 [구성](cloud-directory.html)할 수 있는 몇 가지 서로 다른 방법이 존재합니다. 전송할 메시지의 유형을 결정하고 컨텐츠 및 디자인을 사용자 정의할 수 있습니다. 어떤 메시지를 전송할지 모르시겠습니까? 문제 없습니다. GUI에 사용 가능한 예제 메시지가 있습니다.

영어 이외의 [언어](cloud-directory.html#languages)를 사용하시겠습니까? 자체 번역 컨텐츠를 표시하기 위해 <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/updateLocalization" target="_blank">언어 관리 API <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 사용하여 다른 언어를 선택할 수 있습니다.
{: tip}

</br>



**기술적으로 이 플로우가 어떻게 다릅니까?**

이 서비스는 OAuth2 권한 부여 플로우를 사용하여 권한 프로세스를 맵핑합니다. Facebook 등의 소셜 ID 제공자를 구성하는 경우 <a href="https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html" target="_blank">권한 부여 플로우 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 사용하여 로그인 위젯을 호출합니다. 고유 화면을 사용하는 경우 <a href="https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html" target="_blank">리소스 소유자 비밀번호 인증 정보 플로우 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 사용하여 사인인 화면을 호출할 수 있도록 해주는 액세스 및 ID 토큰을 제공합니다.

</br>

**작동 방법을 보여주는 예제 앱이 있습니까?**

예! 작동 중에 클라우드 디렉토리를 확인하려면 다음 예제를 참조하십시오.

* <a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="_blank">Use your own branded UI for user sign-in with {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>
* <a href="https://www.ibm.com/blogs/bluemix/2018/06/use-ui-flows-user-sign-sign-app-id/" target="_blank">Use your own UI and Flows for User Sign-Up and Sign-in with with {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>
* <a href="https://www.ibm.com/blogs/bluemix/2018/06/custom-login-page-app-id-integration/" target="_blank">Use a custom login page with  {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>

</br>
</br>

## Android SDK로 앱 브랜드화
{: #branded-ui-android}

클라우드 디렉토리를 사용하면 Android SDK로 사용자 정의된 화면을 호출할 수 있습니다. 사용자가 상호 작용할 수 있는 화면의 조합을 선택할 수 있습니다. 세부 예제는 <a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="blank">Check out this blog<img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>의 내용을 참조하십시오.
{: shortdesc}

</br>

**사인인**

1. GUI에서 클라우드 디렉토리 [설정](cloud-directory.html#cd-settings)을 구성하십시오. 
2. 애플리케이션에 다음 코드를 추가하십시오. 사용자가 사용자 정의 화면에서 사인인을 클릭하면 사인인 플로우가 트리거됩니다. 일반 사용자의 사용자 이름 및 비밀번호를 제공하여 액세스, ID 및 새로 고치기 토큰을 받을 수 있습니다.

  ```java
  AppID.getInstance().signinWithResourceOwnerPassword(getApplicationContext(), username, password, new TokenResponseListener() {
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

## iOS Swift SDK로 앱 브랜드화
{: #branded-ui-ios-swift}

클라우드 디렉토리가 사용으로 설정되어 있는 경우 [iOS Swift SDK](https://github.com/ibm-cloud-security/appid-clientsdk-swift)를 통해 고유한 브랜드의 화면을 호출할 수 있습니다.
{: shortdesc}

</br>

**사인인**

1. GUI에서 클라우드 디렉토리 [설정](cloud-directory.html#cd-settings)을 구성하십시오. 
2. 애플리케이션에 다음 코드를 배치하십시오. 사용자가 사인인하려고 시도하면 사인인 화면이 호출되고 사용자 정의된 사인인 페이지를 통해 권한 및 인증 프로세스가 시작됩니다.

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
  {: codeblock}

</br>
</br>

## Node.js SDK로 앱 브랜드화
{: #branded-ui-nodejs}

클라우드 디렉토리가 사용되는 경우에는 Node.js SDK로 사용자 정의된 화면을 호출할 수 있습니다.
{: shortdesc}

**사인인**

사용자는 WebAppStrategy를 사용하여 사용자 이름과 비밀번호로 웹 앱에 사인인할 수 있습니다. 사용자가 앱에 성공적으로 로그인하면 액세스 토큰이 활성 상태로 유지되는 한 HTTP 세션에서 지속됩니다. HTTP 세션이 닫히거나 만료되면 액세스 토큰도 영구 삭제됩니다.


1. GUI에서 클라우드 디렉토리 [설정](cloud-directory.html#cd-settings)을 구성하십시오. 
2. 애플리케이션에 다음 코드를 배치하십시오. 사용자가 사인인하려고 시도하면 사인인 화면이 호출되고 사용자 정의된 사인인 페이지를 통해 권한 및 인증 프로세스가 시작됩니다.

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

**참고**: HTML 형식으로 요청을 제출하는 경우 <a href="https://www.npmjs.com/package/body-parser" target="blank">본문 구문 분석기 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a> 미들웨어를 사용할 수 있습니다. 리턴되는 오류 메시지를 확인하려는 경우 <a href="https://www.npmjs.com/package/connect-flash" target="blank">connect-flash <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 사용할 수 있습니다. 작동 중에 확인하려면 <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs/blob/master/samples/web-app-sample.js" target="blank">웹 앱 샘플 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>을 참조하십시오.

</br>
</br>

## API로 앱 브랜드화
{: #branded-ui-api}

사용자 정의된 화면을 표시하고 {{site.data.keyword.appid_short_notm}}의 인증 및 권한 부여 기능을 활용할 수 있습니다. 클라우드 디렉토리를 ID 제공자로 사용하면 사용자는 도움을 받지 않고 앱과 상호 작용할 수 있습니다. 사용자는 도움을 요청하지 않고도 사인인, 등록 및 자체 비밀번호 재설정 등을 수행할 수 있습니다.
{: shortdesc}

이를 가능하게 하도록 {{site.data.keyword.appid_short_notm}}에서 REST API를 공개합니다. REST API를 사용하여 웹 앱을 서비스하는 백엔드 서버를 빌드하거나 고유한 사용자 정의 화면을 통해 모바일 앱과 상호작용할 수 있습니다.

관리 API는 IBM Cloud IAM(Identity and Access Management) 생성 토큰으로 보호됩니다. 이는 계정 소유자가 자체 팀의 어떤 구성원이 각 서비스 인스턴스에 대해 어떤 액세스 레벨을 보유하는지를 지정할 수 있음을 의미합니다. IAM 및 {{site.data.keyword.appid_short_notm}}가 함께 작동되는 방법에 대한 자세한 정보는 [서비스 액세스 관리](/docs/services/appid/iam.html)를 참조하십시오.

[설정](/docs/services/appid/cloud-directory.html)을 구성한 후 다음 엔드포인트를 호출하여 각 화면을 표시할 수 있습니다.

**등록**

`/sign_up` 엔드포인트를 사용하여 사용자가 직접 앱에 등록하도록 허용할 수 있습니다.
요청 본문에서 다음 데이터를 제공하십시오.
  * tenantID.
  * 클라우드 디렉토리 사용자 데이터. 세부사항은 [SCIM 전체 사용자 표시](https://tools.ietf.org/html/rfc7643#section-8.2)를 참조하십시오.
    * `password` 속성.
    * `true`로 설정된 `primary` 속성의 이메일 배열에서, 최소한 1개의 이메일 주소가 있어야 합니다.

[이메일 구성](/docs/services/appid/cloud-directory.html)에 따라 사용자가 검증 요청을 수신하거나, 앱에 등록 시 환영하는 이메일을 수신하거나, 또는 둘 다 수신할 수 있습니다. 두 가지 유형의 이메일 모두 사용자가 앱에 등록할 때 트리거됩니다. 검증 이메일에는 사용자가 해당 ID를 확인하기 위해 클릭할 수 있는 링크가 포함되어 있으며, 검증을 수행한 것에 감사하거나 검증이 완료되었음을 확인하는 화면이 표시됩니다.  

고유한 사후 검증 페이지를 표시하려면 다음 작업을 수행하십시오.

1. {site.data.keyword.appid_short_notm}} 대시보드에서 클라우드 디렉토리 ID 제공자로 이동하십시오.
2. **이메일 검증** 탭을 클릭하십시오.
3. **사용자 정의 검증 페이지 URL**에서 랜딩 페이지의 URL을 입력하십시오.

이 값이 제공된 경우, {{site.data.keyword.appid_short_notm}}는 `context` 조회와 함께 URL을 호출합니다. `/sign_up/confirmation_result` 엔드포인트를 호출하고 수신된 `context` 매개변수를 전달하면 결과에서 사용자가 자체 계정을 확인했는지 여부를 알려줍니다. 해당되는 경우에는 사용자 정의 페이지를 표시할 수 있습니다.

</br>
**비밀번호 찾기**

`/forgot_password` 엔드포인트를 사용하면 사용자가 자체 비밀번호를 잊은 경우에 이를 복구하도록 허용할 수 있습니다.

요청 본문에서 다음 데이터를 제공하십시오.
  * tenantID.
  * 클라우드 디렉토리 사용자의 이메일.

엔드포인트가 호출된 경우에는 비밀번호 재설정 이메일이 사용자에게 발송됩니다. 이메일에는 **재설정** 단추가 포함되어 있습니다. 사용자가 단추를 누르면 {{site.data.keyword.appid_short_notm}}에 의해 화면이 표시되며, 이를 사용하여 자체 비밀번호를 재설정할 수 있습니다.

사후 비밀번호 재설정 페이지를 제시할 수 있습니다.

1. GUI에서 클라우드 디렉토리 [설정](cloud-directory.html#cd-settings)을 구성하십시오. **사용자가 앱에서 해당 계정을 관리할 수 있도록 허용**을 **켜기**로 설정해야 합니다.
2. 서비스 대시보드의 **비밀번호 재설정** 탭에서 **비밀번호 찾기 이메일**이 **켜기**로 설정되어 있는지 확인하십시오.
3. **사용자 정의 비밀번호 재설정 페이지의 URL**에서 랜딩 페이지의 URL을 입력하십시오.  

이 값이 제공된 경우, {{site.data.keyword.appid_short_notm}}는 `context` 조회와 함께 URL을 호출합니다. `context` 매개변수를 사용하면 `/forgot_password/confirmation_result`가 호출될 때 결과를 수신할 수 있습니다. 결과가 성공적이면 사용자 정의 페이지를 표시할 수 있습니다.

랜덤 문자열을 사용자 정의 비밀번호 재설정 페이지에 추가하고 요청이 제출되면 이를 백엔드에 전달하십시오. 핸들러가 문자열을 유효성 검증하도록 하고, 유효한 경우에만 `/change_password` 엔드포인트를 호출하십시오. 이를 수행하면 백엔드 비밀번호 재설정 엔드포인트의 취약성을 낮출 수 있습니다.
{: tip}

</br>
**비밀번호 변경**

두 가지 방법으로 `/change_password` 엔드포인트를 사용할 수 있습니다. 사용자가 재설정 요청을 제출하는 경우 또는 사용자가 앱에 사인인하고 자체 비밀번호를 업데이트하고자 하는 경우입니다.

재설정 요청 후 비밀번호를 업데이트하려면 요청 본문에서 다음 데이터를 제공하십시오.
  * tenantID.
  * 사용자 새 비밀번호.
  * 클라우드 디렉토리 사용자의 UUID.
  * 선택사항: 비밀번호 재설정이 수행된 IP 주소. IP 주소 전달을 선택한 경우에는 비밀번호 변경 이메일 템플리트에 대해 `%{passwordChangeInfo.ipAddress}` 플레이스홀더가 사용 가능합니다.

구성에 따라서는 비밀번호가 변경될 때 {{site.data.keyword.appid_short_notm}}에 변경사항이 있었음을 알려주는 이메일을 사용자에게 발송할 수 있습니다.

</br>
앱에 사인인한 동안 사용자가 자체 비밀번호를 변경할 수 있도록 허용하려면 다음을 수행하십시오.

요청 본문에서 다음 데이터를 제공하십시오.
  * tenantID.
  * 사용자 새 비밀번호.
  * 클라우드 디렉토리 사용자의 UUID.

비밀번호 변경 페이지가 사용자에게 현재 비밀번호와 새 비밀번호를 입력하도록 프롬프트를 표시해야 합니다.
{: tip}

백엔드는 ROP API로 사용자의 현재 비밀번호를 유효성 검증하며, 유효한 경우에는 새 비밀번호를 사용하여 엔드포인트를 호출합니다. 구성에 따라서는 비밀번호가 변경될 때 {{site.data.keyword.appid_short_notm}}에 변경사항이 있었음을 알려주는 이메일을 사용자에게 발송할 수 있습니다.

</br>
**재발송**

사용자가 어떤 이유로 인해 이메일을 받지 못한 경우에는 `/resend/{templateName}`을 사용하여 이메일을 재발송할 수 있습니다.

요청 본문에서 다음 데이터를 제공하십시오.
  * tenantID.
  * 템플리트 이름.
  * 클라우드 디렉토리 사용자의 UUID.

**세부사항 변경**

사용자가 앱에 사인인한 경우에는 일부 자체 정보를 업데이트할 수 있습니다. `/Users/{userId}`를 사용하여 해당 정보를 가져오고 업데이트할 수 있습니다.

사용자 세부사항이 업데이트되는 경우, 엔드포인트는 [SCIM 형식](https://tools.ietf.org/html/rfc7643#section-8.2)으로 요청 본문의 업데이트된 사용자 데이터를 가져옵니다. 반드시 관련 세부사항만 변경하십시오.

사용자의 이메일 주소는 변경할 수 없습니다.
{: tip}
