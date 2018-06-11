---

copyright:
  years: 2017, 2018
lastupdated: "2018-06-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}

# Configuring the SDKs
{: #configuring}


## Setting up the Android SDK
{: #android-setup}

Build your Android apps with the {{site.data.keyword.appid_short}} client SDK, initialize the SDK, authenticate users, and make requests to protected and unprotected resources.
{:shortdesc}


### Before you begin
{: #before-android}

You need the following information:
  * An instance of the {{site.data.keyword.appid_short_notm}} service.
  * Your tenant ID. In the **Service Credentials** tab of your service dashboard, click **View Credentials**. Your tenant ID is a unique identifier that is used to initialize your app.
  * Your {{site.data.keyword.Bluemix}} region. You can find your region by looking in the UI. The value is used for initializing your app.
    <table> <caption> Table 1. {{site.data.keyword.Bluemix_notm}} regions and corresponding SDK values </caption>
    <tr>
      <th>{{site.data.keyword.Bluemix}} Region</th>
      <th>SDK value</th>
    </tr>
    <tr>
      <td>US South</td>
      <td><code>AppID.REGION_US_SOUTH</code> </td>
    </tr>
    <tr>
      <td>Sydney</td>
      <td><code>AppID.REGION_SYDNEY</code></td>
    </tr>
    <tr>
      <td>United Kingdom</td>
      <td><code>AppID.REGION_UK</code></td>
    </tr>
    <tr>
      <td>Germany</td>
      <td><code>AppID.REGION_GERMANY</code></td>
    </tr>
  </table>

  * An <a href="https://developers.google.com/web/tools/setup/" target="_blank">Android Studio project<img src="../../icons/launch-glyph.svg" alt="External link icon"></a>, set up to work with Gradle.

### Installing the client SDK
{: #install-android}

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

6. Synchronize your project with Gradle. Click **Tools > Android > Sync Project with Gradle Files**.

### Initializing the client SDK
{: #initialize-android}

Initialize the client SDK by passing the context, tenant ID, and region parameters to the initialize method. A common, though not mandatory, place to put the initialization code is in the onCreate method of the main activity in your Android application.

  ```java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, AppID.REGION_UK);
  ```
  {: codeblock}

1. Replace *tenantId* with your service tenantId.
2. Replace the *AppID.REGION_UK* with your {{site.data.keyword.Bluemix_notm}} region.

For more information, see the <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">{{site.data.keyword.appid_short_notm}} Android GitHub repository<img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.

## Setting up the iOS Swift SDK
{: #ios-setup}

Build your Swift applications with the {{site.data.keyword.appid_short}} client SDK, initialize the SDK, authenticate users, and make requests to protected and unprotected resources.
{:shortdesc}


### Before you begin
{: #before-ios}

You need the following information:
  * An instance of {{site.data.keyword.appid_short_notm}}.
  * Your Tenant ID. In the **Service Credentials** tab of your service dashboard, click **View Credentials**. Your Tenant ID is a unique identifier that is used to initialize your app.
  * Your {{site.data.keyword.Bluemix_notm}} Region.
  You can find your region by looking in the UI. The value is used for initializing your app.
  <table> <caption> Table 1. {{site.data.keyword.Bluemix_notm}} regions and corresponding SDK values </caption>
    <tr>
      <th>{{site.data.keyword.Bluemix}} Region</th>
      <th>SDK value</th>
    </tr>
    <tr>
      <td>US South</td>
      <td><code>AppID.REGION_US_SOUTH</code></td>
    </tr>
    <tr>
      <td>Sydney</td>
      <td><code>AppID.REGION_SYDNEY</code></td>
    </tr>
    <tr>
      <td>United Kingdom</td>
      <td><code>AppID.REGION_UK</code></td>
    </tr>
    <tr>
      <td>Germany</td>
      <td><code>AppID.REGION_GERMANY</code></td>
    </tr>
  </table>

  * An Xcode project (version 9.0.1 or higher).
  * CocoaPods (version 1.1.0 or higher).


### Installing the client SDK
{: #install-ios}

The {{site.data.keyword.appid_short_notm}} client SDK is distributed with CocoaPods, a dependency manager for Swift and Objective-C Cocoa projects. CocoaPods downloads artifacts, and makes them available to your project.

1. Create an Xcode project, or open an existing project.
2. Open, or create, the podfile in the project's directory.
3. Following your project's target add a dependency for the 'BluemixAppID' pod and the `use_frameworks!` command.

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

6. Open your Xcode project and enable keychain sharing. Navigate to **Project Settings > Capabilities > Keychain Sharing** and select **Enable keychain sharing**.
7. Open **Project Settings > Info > URL Types**, and add a **URL Type**. Place `$(PRODUCT_BUNDLE_IDENTIFIER)` in both the **Identifier** and the **URL Scheme** text boxes.


### Initializing the client SDK
{: #initialize-ios}

1. Add the following import to your `AppDelegate` file.

  ```swift
  import BluemixAppID
  ```
  {: codeblock}

2. Initialize the client SDK by passing the tenant ID and region parameters to the initialize method. A common, though not mandatory, place to put the initialization code is in the `application:didFinishLaunchingWithOptions` method of the AppDelegate in your Swift application.

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, bluemixRegion: AppID.Region_UK"]),
      ]
  )
  ```
  {: codeblock}

2. For MacOS: When you build on the command line, all packages should include the following flags.
  ```
  swift build -Xlinker -L/usr/local/opt/openssl/lib -Xcc -I/usr/local/opt/openssl/include
  ```
  {: pre}

3. Use the following command when you create an xcodeproject:
  ```
  swift package generate-xcodeproj --xcconfig-overrides openssl.xcconfig
  ```
  {: pre}

  You can copy the openssl.xcconfig from the <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">{{site.data.keyword.appid_short_notm}} Swift GitHub <img src="../../icons/launch-glyph.svg" alt="External link icon"</a>
  {: tip}
