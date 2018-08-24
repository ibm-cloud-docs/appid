---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}

# 앱에 {{site.data.keyword.appid_short}} 추가
{: #configuring}

애플리케이션에서 서비스를 설정하여 {{site.data.keyword.appid_short}}를 시작하십시오.
{: shortdesc}


## Android SDK 설정
{: #android-setup}

{{site.data.keyword.appid_short}} 클라이언트 SDK를 사용하여 Android 앱을 빌드하고, SDK를 초기화하고, 사용자를 인증하고, 보호 및 비보호 리소스를 요청하십시오.
{:shortdesc}


### 시작하기 전에
{: #before-android}

다음 정보가 필요합니다.
  * {{site.data.keyword.appid_short_notm}} 서비스의 인스턴스.
  * 테넌트 ID. 테넌트 ID는 앱을 초기화하는 데 사용되는 고유 ID이며 서비스 대시보드의 **서비스 신임 정보** 탭에서 찾을 수 있습니다.
  * {{site.data.keyword.Bluemix}} 지역. UI에서 보고 지역을 찾을 수 있습니다. 이 값은 앱을 초기화하는 데 사용됩니다.
    <table><caption> 표 1. {{site.data.keyword.Bluemix_notm}} 지역 및 해당 SDK 값</caption>
    <tr>
      <th>{{site.data.keyword.Bluemix}} 지역</th>
      <th>SDK 값</th>
    </tr>
    <tr>
      <td>미국 남부</td>
      <td><code>AppID.REGION_US_SOUTH</code> </td>
    </tr>
    <tr>
      <td>시드니</td>
      <td><code>AppID.REGION_SYDNEY </code></td>
    </tr>
    <tr>
      <td>영국</td>
      <td><code>AppID.REGION_UK </code></td>
    </tr>
    <tr>
      <td>독일</td>
      <td><code>AppID.REGION_GERMANY</code></td>
    </tr>
  </table>

  * Gradle에서 작동하도록 설정된 <a href="https://developers.google.com/web/tools/setup/" target="_blank">Android Studio 프로젝트 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>.

### SDK 설치
{: #install-android}

1. Android Studio 프로젝트를 작성하거나 기존 프로젝트를 여십시오.
2. 루트 `build.gradle` 파일에 JitPack 저장소를 추가하십시오.

  ```gradle
    allprojects {
	    repositories {
		    ...
		    maven { url 'https://jitpack.io' }
	    }
    }
  ```
  {: codeblock}

3. 앱에 대한 `build.gradle` 파일의 종속성 섹션을 찾아서 {{site.data.keyword.appid_short_notm}} 클라이언트 SDK에 대한 컴파일 종속성을 추가하십시오. **참고**: 프로젝트 `build.gradle` 파일이 아니라, 반드시 사용자의 앱에 대한 파일을 여십시오.

  ```gradle
dependencies {
       compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:4.+'
   }
  ```
  {: codeblock}

5. `defaultConfig` 섹션을 찾아서 다음의 코드 행을 추가하십시오.

  ```gradle
defaultConfig {
  ...
  manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
  ```
  {: codeblock}

6. 프로젝트를 Gradle과 동기화하십시오. **도구 > Android > Gradle 파일과 프로젝트 동기화**를 클릭하십시오.

### SDK 초기화
{: #initialize-android}

initialize 메소드에 컨텍스트, 테넌트 ID 및 지역 매개변수를 전달하여 클라이언트 SDK를 초기화하십시오. 필수는 아니지만 일반적으로 초기화 코드를 넣는 위치는 Android 애플리케이션에서 기본 활동의 onCreate 메소드에 있습니다.

  ```java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, AppID.REGION_UK);
  ```
  {: codeblock}

  <table>
  <caption> 표. 명령 컴포넌트 설명 </caption>
    <tr>
      <th> 컴포넌트 </th>
      <th> 설명 </th>
    </tr>
    <tr>
      <td> <i> tenantID </i> </td>
      <td> 서비스 대시보드의 **서비스 신임 정보** 탭에서 **신임 정보 보기**를 클릭하여 이 값을 찾을 수 있습니다. </td>
    </tr>
    <tr>
      <td> <i> AppID.REGION </i> </td>
      <td> UI에서 지역을 찾을 수 있습니다. 옵션은 `AppID.REGION_US_SOUTH`, `AppID.REGION_UK`, `AppID.REGION_Sydney` 또는 `AppID.REGION_Germany`입니다. </td>
    </tr>
  </table>

이제 ID 제공자를 구성하고 사용자 인증을 시작할 준비가 되었습니다! 자세한 정보는 <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">{{site.data.keyword.appid_short_notm}} Android GitHub repository <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 참조하십시오.


</br>

## iOS Swift SDK 설정
{: #ios-setup}

{{site.data.keyword.appid_short}} 클라이언트 SDK를 사용하여 Swift 애플리케이션을 빌드하고, SDK를 초기화하고, 사용자를 인증하고, 보호 및 비보호 리소스를 요청하십시오.
{:shortdesc}


### 시작하기 전에
{: #before-ios}

다음 정보가 필요합니다.
  * {{site.data.keyword.appid_short_notm}}의 인스턴스.
  * 테넌트 ID. 테넌트 ID는 앱을 초기화하는 데 사용되는 고유 ID이며 서비스 대시보드의 **서비스 신임 정보** 탭에서 찾을 수 있습니다.
  * {{site.data.keyword.Bluemix_notm}} 지역.
  UI에서 보고 지역을 찾을 수 있습니다. 이 값은 앱을 초기화하는 데 사용됩니다.
  <table> <caption> 표. {{site.data.keyword.Bluemix_notm}} 지역 및 해당 SDK 값 </caption>
    <tr>
      <th>{{site.data.keyword.Bluemix}} 지역</th>
      <th>SDK 값</th>
    </tr>
    <tr>
      <td>미국 남부</td>
      <td><code>AppID.REGION_US_SOUTH </code></td>
    </tr>
    <tr>
      <td>시드니</td>
      <td><code>AppID.REGION_SYDNEY </code></td>
    </tr>
    <tr>
      <td>영국</td>
      <td><code>AppID.REGION_UK </code></td>
    </tr>
    <tr>
      <td>독일</td>
      <td><code>AppID.REGION_GERMANY</code></td>
    </tr>
  </table>

  * Xcode 프로젝트(버전 9.0.1 이상).
  * CocoaPods(버전 1.1.0 이상).


### SDK 설치
{: #install-ios}

{{site.data.keyword.appid_short_notm}} 클라이언트 SDK는 Swift 및 Objective-C Cocoa 프로젝트의 종속성 관리자인 CocoaPods를 사용하여 분배됩니다. CocoaPods는 아티팩트를 다운로드하고 프로젝트에서 아티팩트를 사용할 수 있게 합니다.

1. Xcode 프로젝트를 작성하거나 기존 프로젝트를 여십시오.
2. 프로젝트의 디렉토리에서 podfile을 열거나 작성하십시오.
3. 프로젝트의 대상에 따라 'IBMCloudAppID' 팟(Pod) 및 `use_frameworks!` 명령에 대한 종속성을 추가하십시오.

  ```swift
  target '<yourTarget>' do
     use_frameworks!
     pod 'IBMCloudAppID'
  end
  ```
  {: codeblock}

4. 'IBMCloudAppID' 종속성을 다운로드하십시오.

  ```swift
  pod install --repo-update
  ```
  {: codeblock}

6. Xcode 프로젝트에서 키 체인 공유를 사용으로 설정하십시오. **프로젝트 설정 > 기능 > 키 체인 공유**로 이동하고 **키 체인 공유 사용**을 선택하십시오.
7. **프로젝트 설정 > 정보 > URL 유형**을 열고 **URL 유형**을 추가하십시오. **Identifier** 및 **URL 스킴** 텍스트 상자 모두에 다음 값을 배치하십시오.
  ```
  $(PRODUCT_BUNDLE_IDENTIFIER)
  ```
  {: codeblock}


### SDK 초기화
{: #initialize-ios}

1. initialize 메소드에 테넌트 ID 및 지역 매개변수를 전달하여 클라이언트 SDK를 초기화하십시오. 필수는 아니지만 일반적으로 초기화 코드를 넣는 위치는 Swift 애플리케이션에서 AppDelegate의 `application:didFinishLaunchingWithOptions` 메소드에 있습니다.

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, region: AppID.Region_UK)
  ```
  {: codeblock}

  <table>
  <caption> 표. 명령 컴포넌트 설명 </caption>
    <tr>
      <th> 컴포넌트 </th>
      <th> 설명 </th>
    </tr>
    <tr>
      <td> <i> tenantID </i> </td>
      <td> 서비스 대시보드의 **서비스 신임 정보** 탭에서 **신임 정보 보기**를 클릭하여 이 값을 찾을 수 있습니다. </td>
    </tr>
    <tr>
      <td> <i> AppID.REGION </i> </td>
      <td> UI에서 지역을 찾을 수 있습니다. 옵션은 `AppID.REGION_US_SOUTH`, `AppID.REGION_UK`, `AppID.REGION_Sydney` 또는 `AppID.REGION_Germany`입니다. </td>
    </tr>
  </table>

2. `AppDelegate` 파일로 다음의 가져오기를 추가하십시오.

    ```swift
    import IBMCloudAppID
    ```
    {: codeblock}

3. AppDelegate 파일에 다음 코드를 추가하십시오.

  ```swift
  func application( application: UIApplication, open url: URL, options :[UIApplicationOpenURLOptionsKey : Any]) -> Bool {
          return AppID.sharedInstance.application(application, open: url, options: options)
      }
  ```
  {: codeblock}

이제 ID 제공자를 구성하고 사용자 인증을 시작할 준비가 되었습니다! iOS SDK에 대한 자세한 정보는 <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">{{site.data.keyword.appid_short_notm}} iOS GitHub repository <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 참조하십시오.

</br>

## Node.js SDK 설정
{: #nodejs-setup}

### 시작하기 전에
{: #before-nodejs}

다음 전제조건이 준비되어 있는지 확인하십시오.
1. [IBM Cloud CLI](../cli/index.html)를 설치하십시오.
2. Node.js 서버를 <a href="http://expressjs.com/" target="_blank">Express 프레임워크 <img src="../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>로 구현하십시오. Express 프레임워크를 설치하려면 명령행을 사용하여 Node.js 앱이 있는 디렉토리를 열고 다음 명령을 실행하십시오.
  ```
  npm install --save express
  ```
  {: codeblock}
3. Passport를 설치하십시오. 명령행을 사용하여 Node.js 앱이 있는 디렉토리를 열고 다음 명령을 실행하십시오.
  ```
  npm install --save passport
  ```
  {: codeblock}

**참고**: 다른 프레임워크는 `Express` 프레임워크(예: LoopBack)를 사용합니다. 이러한 프레임워크와 함께 {{site.data.keyword.appid_short_notm}} 서버 SDK를 사용할 수 있습니다.


### SDK 설치
{: #install-nodejs}

1. 명령행을 사용하여 Node.js 앱이 있는 디렉토리를 여십시오.
2. {{site.data.keyword.appid_short_notm}} 서비스를 설치하십시오.
  ```
  npm install --save ibmcloud-appid
  ```
  {: codeblock}

### SDK 초기화
{: #initialize}

1. 다음 `require` 정의를 `server.js` 파일에 추가하십시오.
    ```
    const express = require('express');
    const session = require('express-session')
    const passport = require('passport');
    const WebAppStrategy = require("ibmcloud-appid").WebAppStrategy;
    const CALLBACK_URL = "/ibm/cloud/appid/callback";
    ```
    {: codeblock}

2. express-session 미들웨어를 사용하도록 express 앱을 설정하십시오. **참고**: 프로덕션 환경에 적합한 세션 스토리지로 미들웨어를 구성해야 합니다. 자세한 정보는 <a href="https://github.com/expressjs/session" target="_blank">expressjs 문서 <img src="../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 참조하십시오.
    ```
    const app = express();
    app.use(session({
        secret: "123456",
        resave: true,
        saveUninitialized: true
        }));
    app.use(passport.initialize());
    app.use(passport.session());
    ```
    {: codeblock}

3. 테넌트 ID 및 신임 정보를 전달하여 SDK를 초기화하십시오.
    ```
  passport.use(new WebAppStrategy({
    	  tenantId: "{tenant-id}",
   	    clientId: "{client-id}",
      	secret: "{secret}",
      	oauthServerUrl: "{oauth-server-url}",
      	redirectUri: "{app-url}" + CALLBACK_URL
      }));
    ```
    {: codeblock}

 <table summary="명령 컴포넌트: Node.js 앱">
  <caption>Node.js 앱에 대한 명령 컴포넌트</caption>
    <tr>
      <th>컴포넌트</th>
      <th>설명</th>
    </tr>
    <tr>
      <td><i> tenantID </i></td>
      <td>테넌트 ID는 앱을 초기화하는 데 사용되는 고유 ID입니다. **서비스 신임 정보** 탭의 **신임 정보 보기**를 클릭하여 {{site.data.keyword.appid_short_notm}} 서비스 대시보드에서 값을 찾을 수 있습니다.</td>
    </tr>
    <tr>
      <td><i> clientID </i> </br> <i> secret </i> </br> <i> oauth-server-url </i> </br> </td>
      <td>서비스 대시보드의 **서비스 신임 정보** 탭에서 **신임 정보 보기**를 클릭하여 이러한 값을 찾을 수 있습니다. </td>
    </tr>
    <tr><td><i>redirectUri</i></td>
    <td>세 가지 방법으로 redirectUri 값을 제공할 수 있습니다.</br>
        1. 새 WebAppStrategy({redirectUri: "...."})에서 수동으로</br>
        2. `redirectUri`라는 환경 변수</br>
        3. 위의 값이 모두 제공되지 않으면 App ID SDK가 IBM Cloud에서 실행 중인 애플리케이션의 application_uri를 검색하고 기본 접미부 "/ibm/cloud/appid/callback"을 추가하려고 시도합니다.</td>
    </tr>
    <tr>
      <td><i> CALLBACK_URL </i></td>
      <td>사용자가 로그인한 후에 보는 페이지의 URL입니다. </td>
    </tr>
  </table>

4. 직렬화 및 직렬화 해제로 passport를 구성하십시오. 이 구성 단계는 HTTP 요청 전체에 걸쳐 인증된 세션 지속성에 필요합니다. 자세한 정보는 <a href="http://passportjs.org/docs" target="_blank">passport 문서 <img src="../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 참조하십시오.

  ```
  passport.serializeUser(function(user, cb) {
    cb(null, user);
    });

  passport.deserializeUser(function(obj, cb) {
    cb(null, obj);
    });
  ```
  {: codeblock}

5. 다음 코드를 `server.js` 파일에 추가하여 서비스 경로 재지정을 실행하십시오.
   ```
   app.get(CALLBACK_URL, passport.authenticate(WebAppStrategy.STRATEGY_NAME));
   app.get('/protected', passport.authenticate(WebAppStrategy.STRATEGY_NAME)), function(req, res)
        res.json(req.user);
   });
   ```
   {: codeblock}

   **참고**: 서비스는 다음 순서로 경로 재지정됩니다.
    1. `WebAppStrategy.ORIGINAL_URL` 키 아래에서 HTTP 세션에서 지속된 대로 인증 프로세스를 트리거한 요청의 원래 URL.
    2. `passport.authenticate(name, {successRedirect: "...."})`에 지정된 대로 성공적인 경로 재지정
    3. 애플리케이션 루트("/")

6. 애플리케이션을 재배치하십시오.

자세한 정보는 <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">{{site.data.keyword.appid_short_notm}} Node.js GitHub repository <img src="../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 참조하십시오.

## Swift SDK 설정
{: #swift-setup}

{{site.data.keyword.appid_short}} 서버 SDK로 백엔드 및 API를 보호합니다.
{:shortdesc}


### 시작하기 전에
{: #before-swift}

Swift SDK 관련 작업을 수행하려면 우선 다음의 전제조건이 필요합니다.

* MacOS 또는 Linux
* OpenSSL 1.0.2(Linux)
* Swift 3.0.2 설치
* Kitura 1.6 설치


### SDK 설치
{: #install-swift}

1. Swift 앱의 디렉토리에서 `Package.swift` 파일을 열고 `appid-serversdk-swift` 종속성을 추가하십시오.

  ```swift
  let package = Package(
      name: “myApp",
      dependencies: [
          .package(url: "https://github.com/ibm-cloud-security/appid-serversdk-swift.git", .upToNextMinor(from: “4.0.0")),
      ],
      targets: [
          .target(
              name: "myApp",
              dependencies: ["IBMCloudAppID"]),
      ]
  )
  ```
  {: codeblock}

2. MacOS의 경우: 명령행에서 빌드할 때 모든 패키지에는 다음 플래그가 포함되어야 합니다.
  ```
  swift build -Xlinker -L/usr/local/opt/openssl/lib -Xcc -I/usr/local/opt/openssl/include
  ```
  {: pre}

3. xcodeproject를 작성할 때 다음 명령을 사용하십시오.
  ```
  swift package generate-xcodeproj --xcconfig-overrides openssl.xcconfig
  ```
  {: pre}

  <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">{{site.data.keyword.appid_short_notm}} Swift GitHub <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>에서 openssl.xcconfig를 복사할 수 있습니다.
  {: tip}

4. 다음 코드를 Swift 애플리케이션에 추가하십시오.
    * 세션 미들웨어를 사용하도록 Kitura를 설정하십시오. **참고**: 프로덕션 환경에 적합한 세션 스토리지로 Kitura를 구성해야 합니다. 자세한 정보는 <a href="https://github.com/IBM-Swift/Kitura-Session" target="_blank">Kitura 문서 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 참조하십시오.
    * 콜백 URL에서 get 명령을 실행하여 {{site.data.keyword.appid_short_notm}} 서비스에서 액세스 및 ID 토큰을 검색하십시오.

    ```swift
    import Foundation
    import Kitura
    import KituraSession
    import Credentials
    import SwiftyJSON
    import IBMCloudAppID
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

5. 애플리케이션을 재배치하십시오.

</br>

## Liberty for Java SDK 설정
{: #lfj-setup}

Liberty for Java 웹 애플리케이션에서 작동하도록 {{site.data.keyword.appid_short_notm}}를 구성할 수 있습니다.
{:shortdesc}

1. <a href="https://www.ibm.com/support/knowledgecenter/en/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/twlp_config_oidc_rp.html" target="_blank">OpenID Connect feature <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 `server.xml`에 추가하십시오.

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

4. `server.xml` 파일에서 특수 주제 유형을 ALL_AUTHENTICATED_USERS로 정의하십시오.

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

5. `<application-bnd>` 요소에서, 웹 앱 `web.xml`에서 찾은 <a href="https://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_authorization.html?cp=SSAW57_8.5.5&cm_mc_uid=18498555367014888859884&cm_mc_sid_50200000=1494855872" target="_blank">역할을 정의 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>하십시오.

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

6. 인증서를 가져오십시오.

    a. {{site.data.keyword.appid_short_notm}} 대시보드에서 서비스 신임 정보를 클릭하십시오.

    b. **신임 정보 보기**를 클릭하고 `oauthServerUrl`을 복사하십시오.

    c. `/token`을 URL에 추가하십시오. Firefox를 사용하여 출력 URL을 찾아보고 인증서를 가져오십시오. 다음 URL을 예로 사용할 수 있습니다.

    ```
    https://appid-oauth.ng.bluemix.net/oauth/v3/5d12852e-b0a0-46a3-9547-67a4a33a7164/token
    ```
    {: screen}

    d. Firefox 주소 표시줄에서 잠금 아이콘 > **오른쪽 화살표** > **자세한 정보** > **인증서 보기**을 클릭하십시오.

    e. **보안** 탭에서 **인증서 보기** > **세부사항**을 클릭하십시오.

    f. 인증서를 내보내고 이를 PEM 파일로서 로컬 드라이브에 저장하십시오.

7. <a href="https://www.ibm.com/support/knowledgecenter/SSYKE2_6.0.0/com.ibm.java.security.component.60.doc/security-component/keytoolDocs/keytool_overview.html" target="_blank">Liberty Keytool <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>을 사용하여 Liberty for Java truststore.jks 파일에 인증서를 추가하고 OIDC 요소의 인증서 별명에 참조를 추가하십시오. 
`.jks file`은 서버 디렉토리: **리소스** > **보안** > **<i>신뢰 저장소 파일 이름</i>** > **`.jks file`**에 있습니다. 다음 옵션 중 하나를 사용하여 파일에 인증서를 추가하십시오.

    * 터미널에서 Liberty for Java 보안 폴더: wlp > usr > 서버 > <i>servername</i> > 리소스 > 보안으로 이동하고 다음 명령을 사용하여 인증서를 추가하십시오.

      ```
      keytool -importcert -keystore ./trust.jks -file ~/Documents/secbluemix.cer`
      ```
      {: codeblock}      

      **참고**: `~/Documents/[certificatename].cer`은 로컬 드라이브에서 파일 위치를 보여줍니다.

    * <a href="http://keystore-explorer.org/index.html" target="_blank">KeyStore 탐색기 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 사용하여 인증서를 추가할 수 있습니다. KeyStore 탐색기를 열고 **기존 KeyStore 열기**를 선택하십시오.

    **참고**: 신뢰 저장소를 새 인증서로 업데이트해야 하는 경우 인증서가 만료/변경될 수 있습니다.

8. `manifest.yml` 파일에서 {{site.data.keyword.appid_short_notm}} 인스턴스를 정의하십시오.

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

  ```
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
         authFilterid="myAuthFilter"/>
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
      <applicationManager autoExpand="true"/>
  </server>
  ```
  {: codeblock}



</br>

## {{site.data.keyword.Bluemix_notm}}에서 실행되지 않는 기존 애플리케이션에 {{site.data.keyword.appid_short_notm}} 추가
{: #existing}

{{site.data.keyword.Bluemix_notm}}에서 실행되지 않는 애플리케이션에 {{site.data.keyword.appid_short_notm}}를 추가할 수 있습니다. 이 주제에서 일부 예제를 볼 수 있지만 이러한 언어로만 서비스를 사용할 수 있는 것은 아닙니다.

</br>

**Node.js**

Node.js 앱에서 `passport.use(new WebAppStrategy());`을 다음 코드로 바꾸십시오.

  ```
  passport.use(new WebAppStrategy({
    	  tenantId: "{tenant-id}",
   	    clientId: "{client-id}",
      	secret: "{secret}",
      	oauthServerUrl: "{oauth-server-url}",
      	redirectUri: "{app-url}" + CALLBACK_URL
      }));
  ```
  {: codeblock}

  <table>
  <caption> 표. Node.js 앱에 대한 명령 컴포넌트 설명 </caption>
    <tr>
      <th> 컴포넌트 </th>
      <th> 설명 </th>
    </tr>
    <tr>
      <td><code>tenant-id</code> </br> <code> clientID </code> </br> <code> secret </code> </br> <code> oauth-server-url </code> </br></td>
      <td> 서비스 대시보드의 **서비스 신임 정보** 탭에서 **신임 정보 보기**를 클릭하여 이러한 값을 찾을 수 있습니다. </td>
    </tr>
    <tr>
      <td><code> app-url </code></td>
      <td>애플리케이션 URL입니다.</td>
    </tr>
    <tr>
      <td><code> CALLBACK_URL </code></td>
      <td> 사용자가 로그인한 후에 보는 페이지의 URL입니다. </td>
    </tr>
  </table>

</br>

**Swift**

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
  <caption>표. Swift 앱에 대한 명령 컴포넌트 설명</caption>
    <tr>
      <th> 컴포넌트 </th>
      <th> 설명 </th>
    </tr>
    <tr>
      <td><code>tenant-id</code> </br> <code> clientID </code> </br> <code> secret </code> </br> <code> oauth-server-url </code> </br></td>
      <td> 서비스 대시보드의 **서비스 신임 정보** 탭에서 **신임 정보 보기**를 클릭하여 이러한 값을 찾을 수 있습니다. </td>
    </tr>
    <tr>
      <td><code> app-url </code></td>
      <td>애플리케이션 URL입니다.</td>
    </tr>
    <tr>
      <td><code> CALLBACK_URL </code></td>
      <td> 사용자가 로그인한 후에 보는 페이지의 URL입니다. </td>
    </tr>
  </table>


</br>

**Liberty for Java**

Liberty for Java 앱에서 [Liberty for Java SDK 설정](#lfj-setup) 아래의 단계를 완료하십시오. 단, OIDC 클라이언트 요소 변수를 다음 코드로 대체하십시오.

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
  <caption>표. Liberty for Java 앱에 대한 OIDC 요소 변수 </caption>
    <tr>
      <th> 컴포넌트 </th>
      <th> 설명 </th>
    </tr>
    <tr>
    <td><code> clientID </code> </br> <code> secret </code> </br> <code> oauth-server-url </code> </br></td>
    <td>서비스 대시보드의 **서비스 신임 정보** 탭에서 **신임 정보 보기**를 클릭하여 이러한 값을 찾을 수 있습니다.</td>
    </tr>
    <tr>
      <td><code> authorizationEndpointURL </code></td>
      <td> oauthServerURL의 끝에 `/authorization`을 추가합니다.</td>
    </tr>
    <tr>
      <td><code> tokenEndpointUrl </code></td>
      <td>oauthServerURL의 끝에 `/token`을 추가합니다.</td>
    </tr>
    <tr>
      <td><code> jwkEndpointUrl </code></td>
      <td>oauthServerURL의 끝에 `/publickeys`를 추가합니다.</td>
    </tr>
    <tr>
      <td><code> issuerIdentifier </code></td>
      <td>사용자의 지역에 따라 다릅니다. 다음 중 하나일 수 있습니다. </br><ul><li>issuerIdentifier="appid-oauth.ng.bluemix.net" </br><li> issuerIdentifier="appid-oauth.eu-gb.bluemix.net" </br><li>issuerIdentifier="appid-oauth.au-syd.bluemix.net"</ul></td>
    </tr>
    <tr>
      <td><code> tokenEndpointAuthMethod </code></td>
      <td>"basic"으로 지정됩니다.</td>
    </tr>
    <tr>
      <td><code> signatureAlgorithm </code></td>
      <td>"RS256"으로 지정됩니다.</td>
    </tr>
    <tr>
      <td><code> authFilterid </code></td>
      <td>보호할 리소스의 목록입니다.</td>
    </tr>
    <tr>
      <td><code> trustAliasName </code></td>
      <td>신뢰 저장소 내에서 인증서의 이름입니다.</td>
    </tr>
  </table>
