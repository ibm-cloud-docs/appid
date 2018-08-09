---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}

# SDK 구성
{: #configuring}


## Android SDK 설정
{: #android-setup}

{{site.data.keyword.appid_short}} 클라이언트 SDK를 사용하여 Android 앱을 빌드하고, SDK를 초기화하고, 사용자를 인증하고, 보호 및 비보호 리소스를 요청하십시오.
{:shortdesc}


### 시작하기 전에

다음 정보가 필요합니다.
  * {{site.data.keyword.appid_short_notm}} 서비스의 인스턴스.
  * 테넌트 ID. 서비스 대시보드의 **서비스 신임 정보** 탭에서 **신임 정보 보기**를 클릭하십시오. 테넌트 ID는 앱을 초기화하는 데 사용되는 고유한 ID입니다. 
  * {{site.data.keyword.Bluemix}} 지역. UI에서 보고 지역을 찾을 수 있습니다. 이 값은 앱을 초기화하는 데 사용됩니다.
    <table> <caption> 표 1. {{site.data.keyword.Bluemix_notm}} 지역 및 해당 SDK 값 </caption>
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

### 클라이언트 SDK 설치

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

3. 사용자의 애플리케이션에 대한 `build.gradle` 파일을 여십시오.

    **참고**: 프로젝트 `build.gradle` 파일이 아니라, 반드시 사용자의 앱에 대한 파일을 여십시오.
4. 파일의 종속성 섹션을 찾아서 {{site.data.keyword.appid_short_notm}} 클라이언트 SDK에 대한 컴파일 종속성을 추가하십시오.

  ```gradle
dependencies {
       compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:1.+'
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

### 클라이언트 SDK 초기화

initialize 메소드에 컨텍스트, 테넌트 ID 및 지역 매개변수를 전달하여 클라이언트 SDK를 초기화하십시오. 필수는 아니지만 일반적으로 초기화 코드를 넣는 위치는 Android 애플리케이션에서 기본 활동의 onCreate 메소드에 있습니다.

  ```java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, AppID.REGION_UK);
  ```
  {: codeblock}

1. *tenantId*를 서비스 tenantId로 바꾸십시오.
2. *AppID.REGION_UK*를 사용자의 {{site.data.keyword.Bluemix_notm}} 지역으로 바꾸십시오.

자세한 정보는 <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">{{site.data.keyword.appid_short_notm}} Android GitHub 저장소 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 참조하십시오.

## iOS Swift SDK 설정
{: #ios-setup}

{{site.data.keyword.appid_short}} 클라이언트 SDK를 사용하여 Swift 애플리케이션을 빌드하고, SDK를 초기화하고, 사용자를 인증하고, 보호 및 비보호 리소스를 요청하십시오.
{:shortdesc}


### 시작하기 전에

다음 정보가 필요합니다.
  * {{site.data.keyword.appid_short_notm}}의 인스턴스.
  * 테넌트 ID. 서비스 대시보드의 **서비스 신임 정보** 탭에서 **신임 정보 보기**를 클릭하십시오. 테넌트 ID는 앱을 초기화하는 데 사용되는 고유한 ID입니다. 
  * {{site.data.keyword.Bluemix_notm}} 지역.
  UI에서 보고 지역을 찾을 수 있습니다. 이 값은 앱을 초기화하는 데 사용됩니다.
  <table> <caption> 표 1. {{site.data.keyword.Bluemix_notm}} 지역 및 해당 SDK 값 </caption>
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

  * Xcode 프로젝트(버전 9.0.1 이상).
  * CocoaPods(버전 1.1.0 이상).


### 클라이언트 SDK 설치

{{site.data.keyword.appid_short_notm}} 클라이언트 SDK는 Swift 및 Objective-C Cocoa 프로젝트의 종속성 관리자인 CocoaPods를 사용하여 분배됩니다. CocoaPods는 아티팩트를 다운로드하고 프로젝트에서 아티팩트를 사용할 수 있게 합니다.

1. Xcode 프로젝트를 작성하거나 기존 프로젝트를 여십시오.
2. 프로젝트의 디렉토리에서 podfile을 열거나 작성하십시오.
3. 프로젝트의 대상에 따라 `use_frameworks!` 명령 및 'BluemixAppID' 팟(Pod)에 대한 종속성을 추가하십시오. 

  예를 들면 다음과 같습니다.

  ```swift
  target '<yourTarget>' do
     use_frameworks!
     pod 'BluemixAppID'
  end
  ```
  {: codeblock}

4. `BluemixAppID` 종속성을 다운로드하려면 다음 명령을 실행하십시오.

  ```swift
  pod install --repo-update
  ```
  {: codeblock}

6. Xcode 프로젝트를 열고 키 체인 공유를 사용 설정하십시오. **프로젝트 설정 > 기능 > 키 체인 공유**로 이동하고 **키 체인 공유 사용**을 선택하십시오. 
7. **프로젝트 설정 > 정보 > URL 유형**을 열고 **URL 유형**을 추가하십시오. **ID** 및 **URL 스킴** 텍스트 상자 모두에 `$(PRODUCT_BUNDLE_IDENTIFIER)`를 두십시오. 


### 클라이언트 SDK 초기화

1. `AppDelegate` 파일로 다음의 가져오기를 추가하십시오. 

  ```swift
  import BluemixAppID
  ```
  {: codeblock}

2. initialize 메소드에 테넌트 ID 및 지역 매개변수를 전달하여 클라이언트 SDK를 초기화하십시오. 필수는 아니지만 일반적으로 초기화 코드를 넣는 위치는 Swift 애플리케이션에서 AppDelegate의 `application:didFinishLaunchingWithOptions` 메소드에 있습니다.

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, bluemixRegion: AppID.Region_UK)
  ```
  {: codeblock}

  * *tenantId*를 사용자의 서비스에 대한 테넌트 ID로 바꾸십시오.
  * AppID.REGION_UK를 {{site.data.keyword.appid_short_notm}} 지역으로 바꾸십시오.

3. AppDelegate 파일에 다음 코드를 추가하십시오.

  ```swift
  func application(_ application: UIApplication, open url: URL, options :[UIApplicationOpenURLOptionsKey : Any]) -> Bool {
          return AppID.sharedInstance.application(application, open: url, options: options)
      }
  ```
  {: codeblock}

자세한 정보는 <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">{{site.data.keyword.appid_short_notm}} iOS GitHub 저장소 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 참조하십시오.

## Node.js SDK 설정
{: #nodejs-setup}

### 시작하기 전에

* {{site.data.keyword.Bluemix_notm}}에서 Node.js 앱 개발에 익숙해지십시오. 
* {{site.data.keyword.appid_short_notm}} 서버 SDK를 사용하려면 Node.js 서버를 <a href="http://expressjs.com/" target="_blank">Express 프레임워크 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>로 구현해야 합니다.

**참고**: 다른 프레임워크는 `Express` 프레임워크(예: LoopBack)를 사용합니다. 이러한 프레임워크와 함께 {{site.data.keyword.appid_short_notm}} 서버 SDK를 사용할 수 있습니다.


### 서버 SDK 설치


1. 명령행을 사용하여 Node.js 앱이 있는 디렉토리를 여십시오.
2. 다음 명령을 실행하십시오.

  ```
  npm install -save express
  npm install -save passport
  npm install -save bluemix-appid
  ```
  {: codeblock}

자세한 정보는 <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">{{site.data.keyword.appid_short_notm}} Node.js GitHub 저장소 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 참조하십시오.

## Swift SDK 설정
{: #swift-setup}

{{site.data.keyword.appid_short}} 서버 SDK로 백엔드 및 API를 보호합니다.
{:shortdesc}


### 시작하기 전에

Swift SDK 관련 작업을 수행하려면 우선 다음의 전제조건이 필요합니다. 

* MacOS 또는 Linux
* OpenSSL 1.0.2(Linux)
* Swift 3.0.2 설치
* Kitura 1.6 설치


### SDK 설치

1. Swift 앱의 디렉토리에서 `Package.swift` 파일을 열고 `appid-serversdk-swift` 종속성을 추가하십시오. 예를 들면 다음과 같습니다.

  ```swift
  let package = Package(
      name: “myApp",
      dependencies: [
          .package(url: "https://github.com/ibm-cloud-security/appid-serversdk-swift.git", .upToNextMinor(from: “4.0.0")),
      ],
      targets: [
          .target(
              name: "myApp",
              dependencies: ["BluemixAppID"]),
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
