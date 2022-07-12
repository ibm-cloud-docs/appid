---

copyright:
  years: 2017, 2022
lastupdated: "2022-05-17"

keywords: secure mobile app, android, ios, authenticate users,  authorization grant, client sdk, trusted client, native app, personalized, custom app, devices, identity flow, app security

subcollection: appid

---

{:codeblock: .codeblock}
{:screen: .screen}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:gif: data-image-type='gif'}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:tip: .tip}
{:preview: .preview}
{:deprecated: .deprecated}
{:beta: .beta}
{:term: .term}
{:shortdesc: .shortdesc}
{:script: data-hd-video='script'}
{:support: data-reuse='support'}
{:table: .aria-labeledby="caption"}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:help: data-hd-content-type='help'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:java: .ph data-hd-programlang='java'}
{:javascript: .ph data-hd-programlang='javascript'}
{:swift: .ph data-hd-programlang='swift'}
{:curl: .ph data-hd-programlang='curl'}
{:video: .video}
{:step: data-tutorial-type='step'}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:cli: .ph data-hd-interface='cli'}
{:api: .ph data-hd-interface='api'}
{:release-note: data-hd-content-type='release-note'}

# Mobile apps
{: #mobile-apps}

With {{site.data.keyword.appid_full}}, you can quickly construct an authentication layer for your native or hybrid mobile app.
{: shortdesc}

## Understanding the flow
{: #understanding-mobile}

A mobile flow is useful when you are developing an app that is to be installed on a user's device (a native application). By using this flow, you can securely authenticate users on your app to provide personalized user experiences across devices.

### What is the flow's technical basis?
{: #mobile-technical-flow}

Since native applications are installed directly on a user's device, private user information and application credentials can be extracted by third-parties with relative ease. By default, these types of applications are known as untrusted clients as they cannot store global credentials or user refresh tokens. As a result, untrusted clients require users to input their credentials every time their access tokens expire.

To convert your application into a trusted client, {{site.data.keyword.appid_short_notm}} uses [Dynamic Client Registration](https://datatracker.ietf.org/doc/html/rfc6749){: external}. Before an application instance begins authenticating users, it first registers as an OAuth2 client with {{site.data.keyword.appid_short_notm}}. Because of client registration, your application receives an installation-specific client ID that can be digitally signed and used to authorize requests with {{site.data.keyword.appid_short_notm}}. Since {{site.data.keyword.appid_short_notm}} stores your application's corresponding public key, it can validate your request signature that allows your application to be viewed as a confidential client. This process minimizes your application's risk of exposing credentials indefinitely and greatly improves the user experience by allowing automatic token refresh.

Following registration, your users authenticate by using either the OAuth2 `authorization code` or `resource owner password` [authorization grant](https://datatracker.ietf.org/doc/html/rfc6749#section-1.3){: external} flows to authenticate users.


### Dynamic client registration
{: #mobile-dynamic}

1. A user performs an action that triggers a request by the client application to the {{site.data.keyword.appid_short_notm}} SDK.
2. If your app is not registered as a mobile client yet, the SDK initiates a dynamic registration flow.
3. On a successful registration, {{site.data.keyword.appid_short_notm}} returns your installation-specific client ID.

### Authorization flow
{: #mobile-auth-flow}

![{{site.data.keyword.appid_short_notm}} mobile request flow](images/mobile-flow.svg){: caption="Figure 1. {{site.data.keyword.appid_short_notm}} mobile request flow" caption-side="bottom"}

1. The {{site.data.keyword.appid_short_notm}} SDK starts the authorization process by using the {{site.data.keyword.appid_short_notm}} `/authorization` endpoint.
2. The login widget is displayed to the user.
3. The user authenticates by using one of the configured identity providers.
4. {{site.data.keyword.appid_short_notm}} returns an authorization grant.
5. The authorization grant is exchanged for access, identity, and refresh tokens from the {{site.data.keyword.appid_short_notm}} `/token` endpoint.


## Configuring your mobile app with the {{site.data.keyword.appid_short}} SDKs
{: #configuring-mobile}

Get started with the {{site.data.keyword.appid_short_notm}} SDKs.
{: shortdesc}

### Before you begin
{: #mobile-before-begin}

You need the following information:

* An {{site.data.keyword.appid_short_notm}} instance
* Your instance's tenant ID. This can be found in the **Service Credentials** tab of your service dashboard.
* Your instance's deployment {{site.data.keyword.cloud_notm}} region. You can find your region by looking at the console.

   | {{site.data.keyword.cloud_notm}} Region | SDK value |
   | ---------------- | --------- |
   | US South | `AppID.REGION_US_SOUTH` |
   | Sydney | `AppID.REGION_SYDNEY` |
   | United Kingdom | `AppID.REGION_UK` |
   | Germany | `AppID.REGION_GERMANY` |
   {: caption="Table 1. {{site.data.keyword.cloud_notm}} regions and corresponding SDK values" caption-side="top"}

## Authenticating with the Android SDK
{: #mobile-android}

Protect your mobile applications by using the {{site.data.keyword.appid_short_notm}} client SDK.
{: shortdesc}

### Before you begin
{: #mobile-android-before}

You must have the following prerequisites before you can get started:

* API 27 or higher
* Java 8.x
* Android SDK Tools 26.1.1+
* Android SDK Platform Tools 27.0.1+
* Android Build Tools version 27.0.0+


### Installing the SDK
{: #mobile-android-install}

1. Create an Android Studio project or open an existing project.

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

3. Find your application's `build.gradle` file. **Note**: Be sure to open the file for your app, not the project `build.gradle` file.

   1. Add the {{site.data.keyword.appid_short_notm}} client SDK to the dependencies section.

      ```gradle
      dependencies {
         compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:4.+'
      }
      ```
      {: codeblock}

   2. In the `defaultConfig` section, configure the redirect scheme.

      ```gradle
      defaultConfig {
      ...
      manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
      }
      ```
      {: codeblock}

4. Synchronize your project with Gradle. Click **Tools > Android > Sync Project with Gradle Files**.

</br>

### Initializing the SDK
{: #mobile-android-initialize}


1. Pass the context, tenant ID, and region parameters to the initialize method to configure the SDK.

   A common, though not mandatory, place to put the initialization code is in the `onCreate` method of the main activity in your Android application.
   {: tip}

   ```java
   AppID.getInstance().initialize(getApplicationContext(), <tenantID>, <region>);
   ```
   {: codeblock}



## Authenticating with the iOS Swift SDK
{: #mobile-ios}

Protect your mobile applications by using the {{site.data.keyword.appid_short_notm}} client SDK.
{: shortdesc}

### Before you begin
{: #mobile-ios-before}

You must have the following prerequisites before you get started:

* Xcode 9.0 or higher
* CocoaPods 1.1.0 or higher
* iOS 10.0 or higher



### Installing the SDK
{: #mobile-ios-install}

The {{site.data.keyword.appid_short_notm}} client SDK is distributed with CocoaPods, a dependency manager for Swift and Objective-C Cocoa projects. CocoaPods downloads artifacts, and makes them available to your project.

1. Create an Xcode project or open an existing one.

2. Create a new or open your existing `Podfile` in the project's directory.

3. Add the `IBMCloudAppID` pod and `use_frameworks!` command to your target's dependencies

   ```swift
   target '<yourTarget>' do
      use_frameworks!
      pod 'IBMCloudAppID'
   end
   ```
   {: codeblock}

4. Install your dependencies from the command line within your project directory.

   ```swift
   pod install --repo-update
   ```
   {: codeblock}

5. After installation, open the `{your app}.xcworkspace` file that contains your Xcode project and your linked dependencies

6. Enable keychain sharing in your Xcode project. Navigate to **Project Settings > Capabilities > Keychain Sharing** and select **Enable keychain sharing**.

7. Open **Project Settings > Info > URL Types**, and add a **URL Type**. Place the following value in both the **Identifier** and the **URL Scheme** text boxes.

   ```swift
   (PRODUCT_BUNDLE_IDENTIFIER)
   ```
   {: codeblock}



### Initializing the SDK
{: #mobile-ios-initialize}

1. Initialize the client SDK by passing the tenant ID and region parameters to the initialize method.

   ```swift
      AppID.sharedInstance.initialize(tenantId: <tenantID>, region: <region>)
   ```
   {: codeblock}

   A common, though not mandatory, place to put the initialization code is in the `application:didFinishLaunchingWithOptions` method of the AppDelegate file of your Swift application.
   {: tip}

2. Import the {{site.data.keyword.appid_short_notm}} SDK to your `AppDelegate` file.

   ```swift
   import IBMCloudAppID
   ```
   {: codeblock}

3. Configure your application to process redirects through {{site.data.keyword.appid_short_notm}}.

   ```swift
   func application(_ application: UIApplication, open url: URL, options :[UIApplication.OpenURLOptionsKey : Any]) -> Bool {
         return AppID.sharedInstance.application(application, open: url, options: options)
      }
   ```
   {: codeblock}


## Accessing protected APIs
{: #mobile-accessing-apis}

After a successful login flow, you can use your access and identity tokens to invoke protected backend resources that use the SDK or a networking library of your choice.


### With the Swift SDK
{: #mobile-access-api-swift}

1. Add the following imports to the file in which you want to invoke a protected resource request:

   ```swift
   import BMSCore
   import IBMCloudAppID
   ```
   {: codeblock}

2. Invoke your protected resource

   ```swift
   BMSClient.sharedInstance.initialize(region: <region>)
   BMSClient.sharedInstance.authorizationManager = AppIDAuthorizationManager(appid: AppID.sharedInstance)

   let request =  Request(url: "{your protected resource url}")

   request.send { (response: Response?, error: Error?) in

      guard let response = response, error == null else {
            print("An error occurred invoking a protected resources", error?.localizedDescription ?? "No response was received")
            return;
      }
      // use your response object
   })
   ```
   {: codeblock}


### With the Android SDK
{: #mobile-access-api-android}

1. Add the following imports to the file in which you want to invoke a protected resource request:

   ```java
   import com.ibm.mobilefirstplatform.clientsdk.android.core.api.BMSClient;
   import com.ibm.cloud.appid.android.api.AppIDAuthorizationManager;
   ```

2. Invoke your protected resource

   ```java
   BMSClient bmsClient = BMSClient.getInstance();
   bmsClient.initialize(getApplicationContext(), <region>);

   AppIDAuthorizationManager appIdAuthMgr = new AppIDAuthorizationManager(AppID.getInstance())
   bmsClient.setAuthorizationManager(appIdAuthMgr);

   Request request = new Request("{your protected resource url}", Request.GET);
   request.send(this, new ResponseListener() {

   @Override
   public void onSuccess (Response response) {
         Log.d("My app", "onSuccess :: " + response.getResponseText());
   }

   @Override
   public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
         if (null != t) {
            Log.d("My app", "onFailure :: " + t.getMessage());
         } else if (null != extendedInfo) {
            Log.d("My app", "onFailure :: " + extendedInfo.toString());
         } else {
            Log.d("My app", "onFailure :: " + response.getResponseText());
            }
         }
   });
   ```
   {: codeblock}


### Without an SDK
{: #mobile-access-api-nosdk}

With the library of your choice, set your `Authorization` request header to use the `Bearer` authentication scheme to transmit the access token.

Example request format:

   ```sh
   GET /resource HTTP/1.1
   Host: server.example.com
   Authorization: Bearer <accessToken> <optionalIdentityToken>
   ```
   {: screen}


## Next steps
{: #mobile-next}

With {{site.data.keyword.appid_short_notm}} installed in your application, you're almost ready to start authenticating users! Try doing one of the following activities next:

* Configure your [identity providers](/docs/appid?topic=appid-social)
* Customize and configure [the Login Widget](/docs/appid?topic=appid-login-widget)
* Learn more about the [Android SDK](https://github.com/ibm-cloud-security/appid-clientsdk-android){: external}
* Learn more about the [iOS Swift SDK](https://github.com/ibm-cloud-security/appid-clientsdk-swift){: external}


