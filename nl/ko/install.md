---
copyright:
  years: 2017, 2018
lastupdated: "2018-01-02"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# SDK 구성
{: #configuring}


## Android SDK 설정
{: #android-setup}

{{site.data.keyword.appid_short}} 클라이언트 SDK를 사용하여 Android 앱을 빌드하고, SDK를 초기화하고, 사용자를 인증하고, 보호 및 비보호 리소스를 요청하십시오.
{:shortdesc}


### 시작하기 전에

다음 정보가 필요합니다.
  * {{site.data.keyword.appid_short_notm}} 서비스의 인스턴스.
  * 테넌트 ID. 서비스 대시보드의 **서비스 신임 정보** 탭에서 **신임 정보 보기**를 클릭하십시오. 테넌트 ID가 **tenantID** 필드에 표시됩니다. 이는 앱을 초기화하는 데 사용되는 고유한 ID입니다.
  * {{site.data.keyword.Bluemix}} 지역. UI에서 보고 지역을 찾을 수 있습니다. 이 값은 앱을 초기화하는 데 사용됩니다.
    <table> <caption> 표 1. {{site.data.keyword.Bluemix_notm}} 지역 및 해당 SDK 값 </caption>
    <tr>
      <th> Bluemix 지역 </th>
      <th> SDK 값 </th>
    </tr>
    <tr>
      <td> 미국 남부 </td>
      <td> AppID.REGION_US_SOUTH </td>
    </tr>
    <tr>
      <td> 시드니 </td>
      <td> AppID.REGION_SYDNEY </td>
    </tr>
    <tr>
      <td> 영국 </td>
      <td> AppID.REGION_UK </td>
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

6. 프로젝트를 Gradle과 동기화하십시오. **도구** > **Android** > **Gradle 파일과 프로젝트 동기화**를 클릭하십시오.

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
  * 테넌트 ID. 서비스 대시보드의 **서비스 신임 정보** 탭에서 **신임 정보 보기**를 클릭하십시오. 테넌트 ID가 **TenantID** 필드에 표시됩니다. 이는 앱을 초기화하는 데 사용되는 고유한 ID입니다.
  * {{site.data.keyword.Bluemix_notm}} 지역.
  UI에서 보고 지역을 찾을 수 있습니다. 이 값은 앱을 초기화하는 데 사용됩니다.
    <table> <caption> 표 1. {{site.data.keyword.Bluemix_notm}} 지역 및 해당 SDK 값 </caption>
    <tr>
      <th> Bluemix 지역 </th>
      <th> SDK 값 </th>
    </tr>
    <tr>
      <td> 미국 남부 </td>
      <td> AppID.REGION_US_SOUTH </td>
    </tr>
    <tr>
      <td> 시드니 </td>
      <td> AppID.REGION_SYDNEY </td>
    </tr>
    <tr>
      <td> 영국 </td>
      <td> AppID.REGION_UK </td>
    </tr>
  </table>

  * Xcode 프로젝트(버전 8.1 이상).
  * CocoaPods(버전 1.1.0 이상).


### 클라이언트 SDK 설치

{{site.data.keyword.appid_short_notm}} 클라이언트 SDK는 Swift 및 Objective-C Cocoa 프로젝트의 종속성 관리자인 CocoaPods를 사용하여 분배됩니다. CocoaPods는 아티팩트를 다운로드하고 프로젝트에서 아티팩트를 사용할 수 있게 합니다.

1. Xcode 프로젝트를 작성하거나 기존 프로젝트를 여십시오.
2. 프로젝트의 디렉토리에서 podfile을 열거나 작성하십시오.
3. 프로젝트의 대상 아래에 'BluemixAppID' 팟(pod)에 대한 종속성을 추가하십시오. `use_frameworks!` 명령도 대상 아래에 있는지 확인하십시오.

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

6. Xcode 프로젝트를 열고 키 체인 공유를 사용 설정하십시오. **프로젝트 설정** 아래에서 **기능 > 키 체인 공유**를 클릭하십시오.
7. **프로젝트 설정 > 정보 > URL 유형** 아래에서 **URL 유형**을 추가하십시오. **ID** 텍스트 상자 및 **URL 체계** 텍스트 상자를 모두 `$(PRODUCT_BUNDLE_IDENTIFIER)` 값으로 채우십시오.


### 클라이언트 SDK 초기화

1. `AppDelegate.swift` 파일에 다음과 같이 가져오기를 추가하십시오.

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

* {{site.data.keyword.Bluemix_notm}}에서 Node.js 애플리케이션 개발에 익숙해지십시오.
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

### 시작하기 전에

* {{site.data.keyword.Bluemix}}에서 Swift 애플리케이션 개발에 익숙해지십시오.
* Swift 3.0.2 설치
* Kitura 1.6 설치


### SDK 설치

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

자세한 정보는 <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">{{site.data.keyword.appid_short_notm}} Swift GitHub 저장소 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 참조하십시오.
