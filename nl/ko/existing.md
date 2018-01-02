---

copyright:
  years: 2017
lastupdated: "2017-12-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


# 기존 앱에 {{site.data.keyword.appid_short_notm}} 추가

사용자에 대한 프로파일 정보를 인증하고 저장하기 위해 기존 애플리케이션과 함께 {{site.data.keyword.appid_full}}를 사용할 수 있습니다.


## 전제조건

* 기존 iOS Swift, Android, Node.js, Swift 또는 Liberty for Java 애플리케이션. 
* {{site.data.keyword.appid_short_notm}}의 기존 인스턴스. 


## 기존 Android 앱에 {{site.data.keyword.appid_short_notm}} 추가
{: #existing-android}

기존 Android 애플리케이션에 {{site.data.keyword.appid_short_notm}} 서비스를 추가할 수 있습니다. 

1. 루트 `build.gradle` 파일에 JitPack 저장소를 추가하십시오.

  ```gradle
  allprojects {
      		repositories {
		    ...
         	 maven { url 'https://jitpack.io' }
	    }
    }
  ```
  {: codeblock}

2. 사용자의 애플리케이션에 해당하는 `build.gradle` 파일을 열고 파일의 종속성 섹션을 찾아서 {{site.data.keyword.appid_short_notm}} 클라이언트 SDK에 대한 컴파일 종속성을 추가하십시오. 

  ```gradle
dependencies {
compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:1.+'
   }
  ```
  {: codeblock}

3. defaultConfig 섹션을 찾아서 다음의 코드 행을 추가하십시오. 

  ```gradle
defaultConfig {
...
            manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
  ```
  {: codeblock}

4. 프로젝트를 Gradle과 동기화하십시오. 
5. initialize 메소드에 컨텍스트, 테넌트 ID 및 지역 매개변수를 전달하여 클라이언트 SDK를 초기화하십시오. 필수는 아니지만 일반적으로 초기화 코드를 넣는 위치는 Android 애플리케이션에서 기본 활동의 onCreate 메소드에 있습니다. 

  ```Java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, <AppID.REGION>);
  ```
  {: codeblock}

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
  {: codeblock}

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
{: #existing-ios}

1. 프로젝트의 디렉토리에서 podfile을 여십시오. 
2. 프로젝트의 대상 아래에 'BluemixAppID' 팟(pod)에 대한 종속성을 추가하십시오. `use_frameworks!` 명령도 대상 아래에 있는지 확인하십시오. 
3. `BluemixAppID` 종속성을 다운로드하려면 다음 명령을 실행하십시오. 

  ```
  pod install --repo-update
  ```
  {: codeblock}

4. Xcode 프로젝트를 열고 키 체인 공유를 사용 설정하십시오. **프로젝트 설정** 아래에서 **기능** > **키 체인 공유**를 클릭하십시오.
5. **프로젝트 설정** > **정보** > **URL 유형** 아래에 **URL 유형**을 추가하십시오. **ID** 텍스트 상자 및 **URL 체계** 텍스트 상자를 모두 다음 값으로 채우십시오. 

  ```
  $(PRODUCT_BUNDLE_IDENTIFIER)
  ```
  {: codeblock}

6. `AppDelegate.swift` 파일에 다음과 같이 가져오기를 추가하십시오. 

  ```swift
  import BluemixAppID
  import BMSCore
  ```
  {: codeblock}

7. initialize 메소드에 테넌트 ID 및 지역 매개변수를 전달하여 클라이언트 SDK를 초기화하십시오. 필수는 아니지만 일반적으로 초기화 코드를 넣는 위치는 application:didFinishLaunchingWithOptions: 사용자의 애플리케이션에서 AppDelegate의 메소드에 있습니다. 

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, bluemixRegion: <AppID.Region>)
  ```
  {: codeblock}

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
  {: codeblock}

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
{: #existing-node}

1. `bluemix-appid` 모듈을 Node.js 애플리케이션에 추가하십시오. 

  ```javaScript
  npm install --save bluemix-appid
  ```
  {: codeblock}

2. 다음 모듈이 아직 설치되지 않은 경우 설치하십시오. 

  ```javaScript
  npm install --save express
  npm install --save passport
  npm install --save express-session
  ```
  {: codeblock}

3. 다음 코드를 `app.js` 파일에 추가하십시오. 
    * express-session 미들웨어를 사용하도록 express 앱을 설정하십시오. **참고**: 프로덕션 환경에 적합한 세션 스토리지로 미들웨어를 구성해야 합니다. 자세한 정보는 <a href="https://github.com/expressjs/session" target="_blank">expressjs 문서 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 참조하십시오. 
    * 직렬화 및 직렬화 해제로 passportjs를 구성하십시오. 이는 HTTP 요청 전체에 걸쳐 인증된 세션 지속성에 필요합니다. 자세한 정보는 <a href="http://passportjs.org/docs" target="_blank">passportjs 문서 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 참조하십시오.   
    * 콜백 URL에서 get 명령을 실행하여 {{site.data.keyword.appid_short_notm}} 서비스에서 액세스 및 ID 토큰을 검색하십시오. 

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
  app.get("/protected", passport.authenticate(WebAppStrategy.STRATEGY_NAME)), function(req, res)
    		res.json(req.user);
    });
  ```
  {: codeblock}

    **참고**: 서비스는 다음 순서로 경로 재지정됩니다. 
    1. `WebAppStrategy.ORIGINAL_URL` 키 아래에서 HTTP 세션에서 지속된 대로 인증 프로세스를 트리거한 요청의 원래 URL.
    2. `passport.authenticate(name, {successRedirect: "...."})`에 지정된 대로 성공적인 경로 재지정
    3. 애플리케이션 루트("/")

4. 애플리케이션을 재배치하십시오. 


## 기존 Swift 웹 애플리케이션에 {{site.data.keyword.appid_short_notm}} 추가
{: #existing-swift}

1. Swift 앱의 디렉토리에서 `Package.swift` 파일을 열고 `appid-serversdk-swift` 종속성을 추가하십시오. 예를 들면 다음과 같습니다. 

    ```swift
    import PackageDescription

    let package = Package(
      dependencies: [
          .Package(url: "https://github.com/ibm-cloud-security/appid-serversdk-swift.git", majorVersion: 1)
      ]
  )
    ```
    {: codeblock}

2. 다음 코드를 Swift 애플리케이션에 추가하십시오. 
    * 세션 미들웨어를 사용하도록 Kitura를 설정하십시오. **참고**: 프로덕션 환경에 적합한 세션 스토리지로 Kitura를 구성해야 합니다. 자세한 정보는 <a href="https://github.com/IBM-Swift/Kitura-Session" target="_blank">Kitura 문서 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 참조하십시오. 
    * 콜백 URL에서 get 명령을 실행하여 {{site.data.keyword.appid_short_notm}} 서비스에서 액세스 및 ID 토큰을 검색하십시오. 

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
  {: codeblock}

  <table>
  <caption> 표 5. 명령 컴포넌트 설명</caption>
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



## 기존 Liberty for Java 앱에 {{site.data.keyword.appid_short_notm}} 추가
{: #existing-liberty}

기존 Liberty for Java 웹 애플리케이션에서 작동하도록 {{site.data.keyword.appid_short_notm}}를 구성할 수 있습니다. 

1. <a href="https://www.ibm.com/support/knowledgecenter/en/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/twlp_config_oidc_rp.html" target="_blank">OpenID Connect 기능 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>을 `server.xml`에 추가하십시오. 

  ```xml
  <feature manager>
  <feature>appSecurity-2.0</feature>
  <feature>openidConnectClient-1.0</feature>  
  ```
  {: codeblock}

2. Open ID Connect 클라이언트 기능에서 다음 플레이스홀더를 정의하십시오. 나중에 {{site.data.keyword.Bluemix_notm}}에서 이를 자동으로 채웁니다. 인스턴스 이름 변수는 {{site.data.keyword.appid_short_notm}} 인스턴스 이름과 정확히 일치해야 합니다. 

  ```
  clientId='${cloud.services.AppID-Instance-Name.credentials.clientId}'
  clientSecret='${cloud.services.AppID-Instance-Name.credentials.clientSecret}'
  authorizationEndpointUrl='${cloud.services.AppID-Instance-Name.credentials.authorizationEndpointUrl}'
  tokenEndpointUrl='${cloud.services.AppID-Instance-Name.credentials.tokenEndpointUrl}'
  jwkEndpointUrl='${cloud.services.AppID-Instance-Name.credentials.jwkEndpointUrl}'
  issuerIdentifier='appid-oauth.ng.bluemix.net'
  tokenEndpointAuthMethod="basic"
  signatureAlgorithm="RS256"
  authFilterid="myAuthFilter"
  ```
  {: codeblock}

  **참고**: issuerIdentifier 변수는 사용자의 지역에 따라 변경됩니다. 이는 다음 변수 중 하나일 수 있습니다. 
  * issuerIdentifier="appid-oauth.ng.bluemix.net"
  * issuerIdentifier="appid-oauth.eu-gb.bluemix.net"
  * issuerIdentifier="appid-oauth.au-syd.bluemix.net"</ul> </td>

3. 보호된 리소스를 지정하기 위한 권한 필터를 정의하십시오. 필터가 <a href="https://www.ibm.com/support/knowledgecenter/en/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/rwlp_auth_filter.html" target="_blank">정의되지 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a> 않은 경우에는 서비스가 모든 리소스를 보호합니다. 
  ```
  <authFilter id="myAuthFilter">
             <requestUrl id="myRequestUrl" urlPattern="/protected" matchType="contains"/>
    </authFilter>
  ```
  {: codeblock}

3. `server.xml` 파일에서 특수 주제 유형을 ALL_AUTHENTICATED_USERS로 정의하십시오. 

  ```xml
  <application type="war" id="ProtectedServlet" context-root="/appidSample"
  location="${server.config.dir}/apps/libertySample-1.0.0.war">
    <application-bnd>
        <security-role name="myrole">
        <special-subject type="ALL_AUTHENTICATED_USERS"/>
        </security-role>
            </application-bnd>
        </application>
  ```
  {: codeblock}

4. `<application-bnd>` 요소에서, 웹 앱 `web.xml`에서 찾은 <a href="https://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_authorization.html?cp=SSAW57_8.5.5&cm_mc_uid=18498555367014888859884&cm_mc_sid_50200000=1494855872" target="_blank">역할을 정의 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>하십시오. 

  ```xml
  <security-role>
  <role-name>myrole</role-name>
  </security-role>

  <security-constraint>
  <web-resource-collection>
  <web-resource-name>ProtectedServlet</web-resource-name>
  <url-pattern>/ProtectedServlet/*</url-pattern>
  <http-method>GET</http-method>
  <http-method>PUT</http-method>
  <http-method>POST</http-method>
  <http-method>DELETE</http-method>
  </web-resource-collection>

  <auth-constraint>
  <role-name>myrole</role-name>
  </auth-constraint>
  <user-data-constraint>
  <transport-guarantee>NONE</transport-guarantee>
  </user-data-constraint>
  </security-constraint>
  ```
  {: codeblock}

5. 인증서를 가져오십시오. 

    a. {{site.data.keyword.appid_short_notm}} 대시보드에서 서비스 신임 정보를 클릭하십시오. 

    b. **신임 정보 보기**를 클릭하고 `oauthServerUrl`을 복사하십시오. 

    c. `/token`을 URL에 추가하십시오. Firefox를 사용하여 출력 URL을 찾아보고 인증서를 가져오십시오. 다음 URL을 예로 사용할 수 있습니다. 

    ```
    https://appid-oauth.eu-gb.bluemix.net/oauth/v3/5d12852e-b0a0-46a3-9547-67a4a33a7164/token
    ```
    {: screen}

    d. Firefox 주소 표시줄에서 잠금 아이콘 > **오른쪽 화살표** > **자세한 정보** > **인증서 보기**을 클릭하십시오. 

    e. **보안** 탭에서 **인증서 보기** > **세부사항**을 클릭하십시오. 

    f. 인증서를 내보내고 이를 PEM 파일로서 로컬 드라이브에 저장하십시오. 

6. <a href="https://www.ibm.com/support/knowledgecenter/SSYKE2_6.0.0/com.ibm.java.security.component.60.doc/security-component/keytoolDocs/keytool_overview.html" target="_blank">Liberty Keytool <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>을 사용하여 Liberty for Java truststore.jks 파일에 인증서를 추가하고 OIDC 요소의 인증서 별명에 참조를 추가하십시오. 
`.jks 파일`은 서버 디렉토리: **리소스** > **보안** > **<i>신뢰 저장소 파일 이름</i>** > **`.jks 파일`**에 있습니다. 다음 옵션 중 하나를 사용하여 파일에 인증서를 추가하십시오. 

    * 터미널에서 Liberty for Java 보안 폴더: wlp > usr > 서버 > <i>servername</i> > 리소스 > 보안으로 이동하고 다음 명령을 사용하여 인증서를 추가하십시오. 

      ```
      keytool -importcert -keystore ./trust.jks -file ~/Documents/secbluemix.cer`
      ```
      {: codeblock}      

      **참고**: `~/Documents/[certificatename].cer`은 로컬 드라이브에서 파일 위치를 보여줍니다. 

    * <a href="http://keystore-explorer.org/index.html" target="_blank">KeyStore 탐색기 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 사용하여 인증서를 추가할 수 있습니다. KeyStore 탐색기를 열고 **기존 KeyStore 열기**를 선택하십시오. 

7. `manifest.yml` 파일에서 {{site.data.keyword.appid_short_notm}} 인스턴스를 정의하십시오. 

  ```yml
  services:
  - <appid service name>

  Manifest.yml file example:
  applications:
  - name: LibertyExampl
  buildpack: liberty-for-java
  instances: 1
  random-route: true
  memory: 512M
  disk_quota: 1024M
  timeout: 180
  services:
  - AppID-Instance-Name
  ```
  {: codeblock}

    {{site.data.keyword.appid_short_notm}}용으로 구성된 예제 `server.xml` 파일: 

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
<server description="sample server">

      <featureManager>
        <feature>ssl-1.0</feature>
        <feature>servlet-3.1</feature>
        <feature>appSecurity-2.0</feature>
        <feature>openidConnectClient-1.0</feature>  
      </featureManager>

      <openidConnectClient id="MyDefaultRP"
         clientId='${cloud.services.AppID-Instance-Name.credentials.clientId}'
         clientSecret='${cloud.services.AppID-Instance-Name.credentials.clientSecret}'
         authorizationEndpointUrl='${cloud.services.AppID-Instance-Name.credentials.authorizationEndpointUrl}'
         tokenEndpointUrl='${cloud.services.AppID-Instance-Name.credentials.tokenEndpointUrl}'
         jwkEndpointUrl='${cloud.services.AppID-Instance-Name.credentials.jwkEndpointUrl}'
         issuerIdentifier='${cloud.services.AppID-Instance-Name.credentials.appid-oauth.ng.bluemix.net}'
         tokenEndpointAuthMethod="basic"
         signatureAlgorithm="RS256"
         authFilterid="myAuthFilter"
         trustAliasName="my.bluemix.certificate "
      />
      <authFilter id="myAuthFilter">
               <requestUrl id="myRequestUrl" urlPattern="/protected" matchType="contains"/>
      </authFilter>

      <application type="war" id="ProtectedServlet" context-root="/appidSample" location="${server.config.dir}/apps/libertySample-1.0.0.war">
          <application-bnd>
              <security-role name="myrole">
                  <special-subject type="ALL_AUTHENTICATED_USERS" />
              </security-role>
          </application-bnd>
      </application>

   <applicationManager autoExpand="true"/>

  <keyStore id="defaultKeyStore" password="Password"/>
  <keyStore id="defaulttrustore" password="Liberty" location="<FileContainingCertificated>.jks"/>

  <ssl id="defaultSSLSettings" keyStoreRef="defaultKeyStore" trustStoreRef="defaulttrustore"/>
  <sslDefault sslRef="defaultSSLSettings"/>

      <httpEndpoint id="defaultHttpEndpoint" httpPort="9080" host="*" httpsPort="9443" />

      <!-- Automatically expand WAR files and EAR files -->
      <applicationManager autoExpand="true"/>

  </server>
  ```
  {: codeblock}



## {{site.data.keyword.Bluemix_notm}}에서 실행되지 않는 기존 애플리케이션에 {{site.data.keyword.appid_short_notm}} 추가
{: #existing}

{{site.data.keyword.Bluemix_notm}}에서 실행되지 않는 Node.js 또는 Swift 애플리케이션이 있는 경우, 원격에서 작업하도록 WebAppStrategy 또는 WebAppKituraCredentialsPlugin을 구성할 수 있습니다.  Bluemix에서 실행되지 않는 Liberty for Java 앱의 경우에는 OIDC 요소 변수를 구성하십시오. 


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
  {: codeblock}

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
  {: codeblock}

  <table>
  <caption> 표 6. Swift 및 Node.js 앱에 대한 명령 컴포넌트 설명 </caption>
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

Liberty for Java 앱에서 [기존 Liberty for Java 앱에 {{site.data.keyword.appid_short_notm}} 추가](/docs/services/appid/existing.html#existing-liberty) 아래의 단계를 완료하되, OIDC 클라이언트 요소 변수를 다음 코드로 대체하십시오. 

  ```
  clientId='App ID client_ID'
  clientSecret='App Id Secret'      
  authorizationEndpointUrl='oauthServerUrl/authorization'       
  tokenEndpointUrl='oauthServerUrl/token'
  jwkEndpointUrl='oauthServerUrl/publickeys'
  issuerIdentifier='Changed according to the region'
  tokenEndpointAuthMethod="basic"
  signatureAlgorithm="RS256"
  authFilterid="myAuthFilter"
  trustAliasName="my.bluemix.certificate"
  ```
  {: codeblock}

  <table>
  <caption> 표 7. Bluemix에서 실행되지 않는 Liberty for Java 앱에 대한 OIDC 요소 변수</caption>
    <tr>
      <th> 컴포넌트 </th>
      <th> 설명 </th>
    </tr>
    <tr>
    <td> <i> clientID </i> </br> <i> secret </i> </br> <i> oauth-server-url </i> </br> </td>
    <td> 서비스 대시보드의 **서비스 신임 정보** 탭에서 **신임 정보 보기**를 클릭하여 이러한 값을 찾을 수 있습니다. </td>
    </tr>
    <tr>
      <td> <i> authorizationEndpointURL </i> </td>
      <td> oauthServerURL의 끝에 `/authorization`을 추가합니다. </td>
    </tr>
    <tr>
      <td> <i> tokenEndpointUrl </i> </td>
      <td> oauthServerURL의 끝에 `/token`을 추가합니다. </td>
    </tr>
    <tr>
      <td> <i> jwkEndpointUrl </i> </td>
      <td> oauthServerURL의 끝에 `/publickeys`를 추가합니다. </td>
    </tr>
    <tr>
      <td> <i> issuerIdentifier </i> </td>
      <td> 사용자의 지역에 따라 다릅니다. 다음 중 하나일 수 있습니다.</br><ul><li> issuerIdentifier="appid-oauth.ng.bluemix.net" </br><li> issuerIdentifier="appid-oauth.eu-gb.bluemix.net" </br><li> issuerIdentifier="appid-oauth.au-syd.bluemix.net" </ul></td>
    </tr>
    <tr>
      <td> <i> tokenEndpointAuthMethod </i> </td>
      <td> "basic"으로 지정됩니다. </td>
    </tr>
    <tr>
      <td> <i> signatureAlgorithm </i> </td>
      <td> "RS256"으로 지정됩니다. </td>
    </tr>
    <tr>
      <td> <i> authFilterid </i> </td>
      <td> 보호할 리소스의 목록입니다. </td>
    </tr>
    <tr>
      <td> <i> trustAliasName </i> </td>
      <td> 신뢰 저장소 내에서 인증서의 이름입니다. </td>
    </tr>
  </table>
