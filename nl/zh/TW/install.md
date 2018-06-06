---
copyright:
  years: 2017, 2018
lastupdated: "2018-01-02"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# 配置 SDK
{: #configuring}


## 設定 Android SDK
{: #android-setup}

使用 {{site.data.keyword.appid_short}} 用戶端 SDK 建置 Android 應用程式、起始設定 SDK、鑑別使用者，以及對受保護資源及未受保護資源提出要求。
{:shortdesc}


### 開始之前

您需要下列資訊：
  * {{site.data.keyword.appid_short_notm}} 服務的實例。
  * 您的承租戶 ID。在服務儀表板的**服務認證**標籤中，按一下**檢視認證**。您的承租戶 ID 會顯示在 **tenantID** 欄位中。這是用來起始設定您應用程式的唯一 ID。
  * 您的 {{site.data.keyword.Bluemix}} 地區。您可以在使用者介面中尋找，以找到您的地區。此值用於起始設定應用程式。
    <table> <caption> 表 1. {{site.data.keyword.Bluemix_notm}} 地區及對應的 SDK 值</caption>
    <tr>
      <th> Bluemix 地區</th>
      <th> SDK 值</th>
    </tr>
    <tr>
      <td> 美國南部</td>
      <td> AppID.REGION_US_SOUTH </td>
    </tr>
    <tr>
      <td> 雪梨</td>
      <td> AppID.REGION_SYDNEY </td>
    </tr>
    <tr>
      <td> 英國</td>
      <td> AppID.REGION_UK </td>
    </tr>
  </table>

  * 設定成使用 Gradle 的 <a href="https://developers.google.com/web/tools/setup/" target="_blank">Android Studio 專案 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。

### 安裝用戶端 SDK

1. 建立 Android Studio 專案，或開啟現有專案。
2. 將 JitPack 儲存庫新增至根 `build.gradle` 檔案。

  ```gradle
    allprojects {
	    repositories {
		    ...
		    maven { url 'https://jitpack.io' }
	    }
    }
  ```
  {: codeblock}

3. 開啟應用程式的 `build.gradle` 檔案。

    **附註**：請務必開啟您應用程式的檔案，而非專案 `build.gradle` 檔案。
4. 尋找檔案的 dependencies 區段，並新增 {{site.data.keyword.appid_short_notm}} 用戶端 SDK 的編譯相依關係。

  ```gradle
   dependencies {
       compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:1.+'
   }
  ```
  {: codeblock}

5. 尋找 `defaultConfig` 區段，並新增下列這幾行程式碼。

  ```gradle
  defaultConfig {
  ...
  manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
  ```
  {: codeblock}

6. 將專案與 Gradle 同步化。按一下**工具** > **Android** > **將專案與 Gradle 檔案同步化**。

### 起始設定用戶端 SDK

將環境定義、承租戶 ID 及地區參數傳遞給起始設定方法，以起始設定用戶端 SDK。放置起始設定碼的一般（但非強制）位置是在 Android 應用程式中主要活動的 onCreate 方法。

  ```java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, AppID.REGION_UK);
  ```
  {: codeblock}

1. 將 *tenantId* 取代為您的服務承租戶 ID。
2. 將 *AppID.REGION_UK* 取代為您的 {{site.data.keyword.Bluemix_notm}} 地區。

如需相關資訊，請參閱 <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">{{site.data.keyword.appid_short_notm}} Android GitHub 儲存庫 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。

## 設定 iOS Swift SDK
{: #ios-setup}

使用 {{site.data.keyword.appid_short}} 用戶端 SDK 建置 Swift 應用程式、起始設定 SDK、鑑別使用者，以及對受保護資源及未受保護資源提出要求。
{:shortdesc}


### 開始之前

您需要下列資訊：
  * {{site.data.keyword.appid_short_notm}} 的實例。
  * 您的承租戶 ID。在服務儀表板的**服務認證**標籤中，按一下**檢視認證**。您的「承租戶 ID」會顯示在 **TenantID** 欄位中。這是用來起始設定您應用程式的唯一 ID。
  * 您的 {{site.data.keyword.Bluemix_notm}} 地區。
  您可以在使用者介面中尋找，以找到您的地區。此值用於起始設定應用程式。
    <table> <caption> 表 1. {{site.data.keyword.Bluemix_notm}} 地區及對應的 SDK 值</caption>
    <tr>
      <th> Bluemix 地區</th>
      <th> SDK 值</th>
    </tr>
    <tr>
      <td> 美國南部</td>
      <td> AppID.REGION_US_SOUTH </td>
    </tr>
    <tr>
      <td> 雪梨</td>
      <td> AppID.REGION_SYDNEY </td>
    </tr>
    <tr>
      <td> 英國</td>
      <td> AppID.REGION_UK </td>
    </tr>
  </table>

  * Xcode 專案（8.1 版或更新版本）。
  * CocoaPods（1.1.0 版或更新版本）。


### 安裝用戶端 SDK

{{site.data.keyword.appid_short_notm}} 用戶端 SDK 是使用 CocoaPods（Swift 及 Objective-C Cocoa 專案的相依關係管理程式）進行配送。CocoaPods 會下載構件，並讓它們可供您的專案使用。

1. 建立 Xcode 專案，或開啟現有專案。
2. 在專案的目錄中，開啟或建立 podfile。
3. 在專案的目標下，新增 'BluemixAppID' 欄的相依關係。請確定，您的目標下也有 `use_frameworks!` 指令。
  

  例如：

  ```swift
  target '<yourTarget>' do
     use_frameworks!
     pod 'BluemixAppID'
  end
  ```
  {: codeblock}

4. 若要下載 `BluemixAppID` 相依關係，請執行下列指令。

  ```swift
  pod install --repo-update
  ```
  {: codeblock}

6. 開啟 Xcode 專案，並啟用金鑰鏈共用。在**專案設定**下，按一下**功能 > 金鑰鏈共用**。
7. 在**專案設定 > 資訊 > URL 類型**下，新增 **URL 類型**。請將下列值填入 **ID** 文字框及 **URL 架構**文字框：`$(PRODUCT_BUNDLE_IDENTIFIER)`


### 起始設定用戶端 SDK

1. 將下列 import 新增至 `AppDelegate.swift` 檔案。

  ```swift
  import BluemixAppID
  ```
  {: codeblock}

2. 將承租戶 ID 及地區參數傳遞給起始設定方法，以起始設定用戶端 SDK。放置起始設定碼的一般（但非強制）位置是在 Swift 應用程式中 AppDelegate 的 `application:didFinishLaunchingWithOptions` 方法。

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, bluemixRegion: AppID.Region_UK)
  ```
  {: codeblock}

  * 將 *tenantId* 取代為服務的承租戶 ID。
  * 將 AppID.REGION_UK 取代為 {{site.data.keyword.appid_short_notm}} 地區。

3. 將下列程式碼新增至 AppDelegate 檔案。

  ```swift
  func application(_ application: UIApplication, open url: URL, options :[UIApplicationOpenURLOptionsKey : Any]) -> Bool {
          return AppID.sharedInstance.application(application, open: url, options: options)
      }
  ```
  {: codeblock}

如需相關資訊，請參閱 <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">{{site.data.keyword.appid_short_notm}} iOS GitHub 儲存庫 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。

## 設定 Node.js SDK
{: #nodejs-setup}

### 開始之前

* 熟悉如何在 {{site.data.keyword.Bluemix_notm}} 上開發 Node.js 應用程式。
* {{site.data.keyword.appid_short_notm}} 伺服器 SDK 需要使用 <a href="http://expressjs.com/" target="_blank">Express 架構 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 來實作 Node.js 伺服器。

**附註**：其他架構使用 `Express` 架構（例如 LoopBack）。您可以搭配使用 {{site.data.keyword.appid_short_notm}} 伺服器 SDK 與任何這些架構。


### 安裝伺服器 SDK


1. 使用指令行，開啟具有 Node.js 應用程式的目錄。
2. 執行下列指令。

  ```
  npm install -save express
  npm install -save passport
  npm install -save bluemix-appid
  ```
  {: codeblock}

如需相關資訊，請參閱 <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">{{site.data.keyword.appid_short_notm}} Node.js GitHub 儲存庫 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。

## 設定 Swift SDK
{: #swift-setup}

### 開始之前

* 熟悉如何在 {{site.data.keyword.Bluemix}} 上開發 Swift 應用程式。
* 安裝 Swift 3.0.2
* 安裝 Kitura 1.6


### 安裝 SDK

1. 開啟 Swift 應用程式的目錄中的 `Package.swift` 檔案，並新增 `appid-serversdk-swift` 相依關係。例如：

  ```swift
  import PackageDescription

  let package = Package(
      dependencies: [
          .Package(url: "https://github.com/ibm-cloud-security/appid-serversdk-swift.git", majorVersion: 1)
      ]
  )
  ```
  {: codeblock}

如需相關資訊，請參閱 <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">{{site.data.keyword.appid_short_notm}} Swift GitHub 儲存庫 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。
