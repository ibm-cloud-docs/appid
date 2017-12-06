---
copyright:
  years: 2017
lastupdated: "2017-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Configuring the SDKs
{: #configuring}


## Setting up the Android SDK
{: #android-setup}

Build your Android apps with the {{site.data.keyword.appid_short}} client SDK, initialize the SDK, authenticate users, and make requests to protected and unprotected resources.
{:shortdesc}


### Before you begin

You need the following information:
  * An instance of the {{site.data.keyword.appid_short_notm}} service.
  * Your tenant ID. In the **Service Credentials** tab of your service dashboard, click **View Credentials**. Your tenant ID is displayed in the **tenantID** field. This is a unique identifier that is used to initialize your app.
  * Your {{site.data.keyword.Bluemix}} region. You can find your region by looking in the UI. The value is used for initializing your app.
    <table> <caption> Table 1. {{site.data.keyword.Bluemix_notm}} regions and corresponding SDK values </caption>
    <tr>
      <th> Bluemix Region </th>
      <th> SDK value </th>
    </tr>
    <tr>
      <td> US South </td>
      <td> AppID.REGION_US_SOUTH </td>
    </tr>
    <tr>
      <td> Sydney </td>
      <td> AppID.REGION_SYDNEY </td>
    </tr>
    <tr>
      <td> United Kingdom </td>
      <td> AppID.REGION_UK </td>
    </tr>
  </table>

  * An <a href="https://developers.google.com/web/tools/setup/" target="_blank">Android Studio project<img src="../../icons/launch-glyph.svg" alt="External link icon"></a>, set up to work with Gradle.

### Installing the client SDK

1. Create an Android Studio project, or open an existing project.
2. Add the JitPack repository to your root `build.gradle` file.

  ```gradle
    allprojects {
	    repositories {
		    ...
		    maven { url 'https://jitpack.io' }
	    }
    }
  ```
  {: codeblock}

3. Open the `build.gradle` file for your application.

    **Note**: Be sure to open the file for your app, not the project `build.gradle` file.
4. Find the dependencies section of the file and add a compile dependency for the {{site.data.keyword.appid_short_notm}} client SDK.

  ```gradle
   dependencies {
       compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:1.+'
   }
  ```
  {: codeblock}

5. Find the `defaultConfig` section and add the following lines of code.

  ```gradle
  defaultConfig {
  ...
  manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
  ```
  {: codeblock}

6. Synchronize your project with Gradle. Click **Tools** > **Android** > **Sync Project with Gradle Files**.

### Initializing the client SDK

Initialize the client SDK by passing the context, tenant ID, and region parameters to the initialize method. A common, though not mandatory, place to put the initialization code is in the onCreate method of the main activity in your Android application.

  ```java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, AppID.REGION_UK);
  ```
  {: codeblock}

1. Replace *tenantId* with your service tenantId.
2. Replace the *AppID.REGION_UK* with your {{site.data.keyword.Bluemix_notm}} region.

For more information, see the <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">{{site.data.keyword.appid_short_notm}} Android GitHub repository <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.

## Setting up the iOS Swift SDK
{: #ios-setup}

Build your Swift applications with the {{site.data.keyword.appid_short}} client SDK, initialize the SDK, authenticate users, and make requests to protected and unprotected resources.
{:shortdesc}


### Before you begin

You need the following information:
  * An instance of {{site.data.keyword.appid_short_notm}}.
  * Your Tenant ID. In the **Service Credentials** tab of your service dashboard, click **View Credentials**. Your Tenant ID is displayed in the **TenantID** field. This is a unique identifier that is used to initialize your app.
  * Your {{site.data.keyword.Bluemix_notm}} Region.
  You can find your region by looking in the UI. The value is used for initializing your app.
    <table> <caption> Table 1. {{site.data.keyword.Bluemix_notm}} regions and corresponding SDK values </caption>
    <tr>
      <th> Bluemix Region </th>
      <th> SDK value </th>
    </tr>
    <tr>
      <td> US South </td>
      <td> AppID.REGION_US_SOUTH </td>
    </tr>
    <tr>
      <td> Sydney </td>
      <td> AppID.REGION_SYDNEY </td>
    </tr>
    <tr>
      <td> United Kingdom </td>
      <td> AppID.REGION_UK </td>
    </tr>
  </table>

  * An Xcode project (version 8.1 or higher).
  * CocoaPods (version 1.1.0 or higher).


### Installing the client SDK

The {{site.data.keyword.appid_short_notm}} client SDK is distributed with CocoaPods, a dependency manager for Swift and Objective-C Cocoa projects. CocoaPods downloads artifacts, and makes them available to your project.

1. Create an Xcode project, or open an existing project.
2. Open, or create, the podfile in the project's directory.
3. Under your project's target add a dependency for the 'BluemixAppID' pod. Make sure the `use_frameworks!` command is also under your target.

  For example:

  ```swift
  target '<yourTarget>' do
     use_frameworks!
     pod 'BluemixAppID'
  end
  ```
  {: codeblock}

4. To download the `BluemixAppID` dependency, run the following command.

  ```swift
  pod install --repo-update
  ```
  {: codeblock}

6. Open your Xcode project and enable keychain sharing. Under **Project Settings**, click **Capabilities > Keychain Sharing**.
7. Under **Project Settings > Info > URL Types**, add a **URL Type**. Fill both the **Identifier** text box and the **URL Scheme** text box with this value: `$(PRODUCT_BUNDLE_IDENTIFIER)`


### Initializing the client SDK

1. Add the following import to your `AppDelegate.swift` file.

  ```swift
  import BluemixAppID
  ```
  {: codeblock}

2. Initialize the client SDK by passing the tenant ID and region parameters to the initialize method. A common, though not mandatory, place to put the initialization code is in the `application:didFinishLaunchingWithOptions` method of the AppDelegate in your Swift application.

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, bluemixRegion: AppID.Region_UK)
  ```
  {: codeblock}

  * Replace *tenantId* with the tenant ID for your service.
  * Replace AppID.REGION_UK with your {{site.data.keyword.appid_short_notm}} region.

3. Add the following code to your AppDelegate file.

  ```swift
  func application(_ application: UIApplication, open url: URL, options :[UIApplicationOpenURLOptionsKey : Any]) -> Bool {
          return AppID.sharedInstance.application(application, open: url, options: options)
      }
  ```
  {: codeblock}

For more information, see the <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">{{site.data.keyword.appid_short_notm}} iOS GitHub repository <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.

## Setting up the Node.js SDK
{: #nodejs-setup}

### Before you begin

* Be familiar with developing Node.js applications on {{site.data.keyword.Bluemix_notm}}.
* The {{site.data.keyword.appid_short_notm}} server SDK requires that your Node.js server is implemented with the <a href="http://expressjs.com/" target="_blank">Express framework <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.

**Note**: Other frameworks use `Express` frameworks, such as LoopBack. You can use the {{site.data.keyword.appid_short_notm}} server SDK with any of these frameworks.


### Installing the server SDK


1. Using the command line, open the directory with your Node.js app.
2. Run the following commands.

  ```
  npm install -save express
  npm install -save passport
  npm install -save bluemix-appid
  ```
  {: codeblock}

For more information, see the <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">{{site.data.keyword.appid_short_notm}} Node.js GitHub repository <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.

## Setting up the Swift SDK
{: #swift-setup}

### Before you begin

* Be familiar with developing Swift applications on {{site.data.keyword.Bluemix}}.
* Install Swift 3.0.2
* Install Kitura 1.6


### Installing the SDK

1. Open the `Package.swift` file in the directory of your Swift app and add the `appid-serversdk-swift` dependency. For example:

  ```swift
  import PackageDescription

  let package = Package(
      dependencies: [
          .Package(url: "https://github.com/ibm-cloud-security/appid-serversdk-swift.git", majorVersion: 1)
      ]
  )
  ```
  {: codeblock}

For more information see the <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">{{site.data.keyword.appid_short_notm}} Swift GitHub repository <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.
