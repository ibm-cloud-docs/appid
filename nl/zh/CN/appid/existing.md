---

copyright:
  years: 2017
lastupdated: "2017-06-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# 向现有应用程序添加 {{site.data.keyword.appid_short_notm}}

可以将 {{site.data.keyword.appid_full}} 用于现有应用程序以认证和存储有关用户的概要文件信息。


## 先决条件

* 现有 iOS Swift、Android、Node.js 或 Swift 应用程序。
* 现有 {{site.data.keyword.appid_short_notm}} 实例。


## 向现有 Android 应用程序添加 {{site.data.keyword.appid_short_notm}}

可以将 App ID 服务添加到现有 Android 应用程序。

1. 将 JitPack 存储库添加到根 build.gradle 文件。

  ```gradle
  allprojects {
      		repositories {
		    ...
         	 maven { url 'https://jitpack.io' }
	    }
    }
  ```
  {: pre}

2. 打开应用程序的 build.gradle 文件，找到该文件的 dependencies 部分，并为 {{site.data.keyword.appid_short_notm}} 客户端 SDK 添加编译依赖项。

  ```gradle
  dependencies {
      compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:1.+'
   }
  ```
  {: pre}

3. 找到 defaultConfig 部分，并添加以下代码行。

  ```gradle
  defaultConfig {
                         ...
            manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
  ```
  {: pre}

4. 使用 Gradle 同步项目。
5. 通过将上下文、租户标识和区域参数传递到 initialize 方法来初始化客户端 SDK。在 Android 应用程序中，通常会将初始化代码放置在主活动的 onCreate 方法中，但这不是强制性的。

  ```Java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, <AppID.REGION>);
  ```
  {: pre}

  <table>
  <caption> 表 1. 命令组成部分说明</caption>
    <tr>
      <th> 组成部分</th>
      <th> 描述</th>
    </tr>
    <tr>
      <td> <i>tenantID</i></td>
      <td> 可以通过单击服务仪表板的**服务凭证**选项卡中的**查看凭证**来找到此值。</td>
    </tr>
    <tr>
      <td> <i>AppID.REGION</i></td>
      <td> 可以在 UI 中找到您所在的区域。选项为 `AppID.REGION_US_SOUTH`、`AppID.REGION_UK` 或 `AppID.REGION_Sydney`。</td>
    </tr>
  </table>

6. 初始化 {{site.data.keyword.appid_short_notm}} 客户端 SDK 后，可以通过运行登录窗口小部件来对用户进行认证。

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
  {: pre}

  <table>
  <caption> 表 2. 命令组成部分说明</caption>
    <tr>
      <th> 组成部分</th>
      <th> 描述</th>
    </tr>
    <tr>
      <td> <i>onAuthorizationFailure</i></td>
      <td> 发生了异常。</td>
    </tr>
    <tr>
      <td> <i>onAuthorizationCanceled</i></td>
      <td> 认证流程已被用户取消。</td>
    </tr>
    <tr>
      <td> <i>onAuthorizationSuccess</i></td>
      <td> 已对用户进行认证。</td>
    </tr>
  </table>

## 向现有 iOS Swift 应用程序添加 {{site.data.keyword.appid_short_notm}}

1. 在项目的目录中打开 podfile。
2. 在项目的目标下，添加“BluemixAppID”pod 的依赖项。确保 `use_frameworks!` 命令也位于目标下。
3. 要下载 `BluemixAppID` 依赖项，请运行以下命令。

  ```
  pod install --repo-update
  ```
  {: pre}

4. 打开 Xcode 项目并启用密钥链共享。在**项目设置**下，单击**功能** > **密钥链共享**。
5. 在**项目设置** > **信息** > **URL 类型**下，添加 **URL 类型**。使用以下值填充**标识**文本框和 **URL 方案**文本框。

  ```
  $(PRODUCT_BUNDLE_IDENTIFIER)
  ```
  {: pre}

6. 将以下 import 语句添加到 AppDelegate.swift 文件中。

  ```swift
  import BluemixAppID
  import BMSCore
  ```
  {: pre}

7. 通过将租户标识和区域参数传递到 initialize 方法来初始化客户端 SDK。在应用程序中，通常会将初始化代码放置在 AppDelegate 的 application:didFinishLaunchingWithOptions: 方法中，但这不是强制性的。

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, bluemixRegion: <AppID.Region>)
  ```
  {: pre}

  <table>
  <caption> 表 3. 命令组成部分说明</caption>
    <tr>
      <th> 组成部分</th>
      <th> 描述</th>
    </tr>
    <tr>
      <td> <i>tenantID</i></td>
      <td> 可以通过单击服务仪表板的**服务凭证**选项卡中的**查看凭证**来找到此值。</td>
    </tr>
    <tr>
      <td> <i>AppID.REGION</i></td>
      <td> 可以在 UI 中找到您所在的区域。选项为 `AppID.REGION_US_SOUTH`、`AppID.REGION_UK` 或 `AppID.REGION_Sydney`。</td>
    </tr>
  </table>

8. 将以下代码添加到 AppDelegate 文件中。

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
  {: pre}
  <table>
  <caption> 表 4. 命令组成部分说明</caption>
    <tr>
      <th> 组成部分</th>
      <th> 描述</th>
    </tr>
    <tr>
      <td> <i>onAuthorizationSuccess</i></td>
      <td> 已对用户进行认证。</td>
    </tr>
    <tr>
      <td> <i>onAuthorizationCanceled</i></td>
      <td> 认证流程已被用户取消。</td>
    </tr>
    <tr>
      <td> <i>onAuthorizationFailure</i></td>
      <td> 发生了异常。</td>
    </tr>
  </table>

## 向现有 Node.js Web 应用程序添加 {{site.data.keyword.appid_short_notm}}

1. 将 `bluemix-appid` 模块添加到 Node.js 应用程序。

  ```javaScript
  npm install --save bluemix-appid
  ```
  {: pre}

2. 如果尚未安装以下模块，请进行安装。

  ```javaScript
  npm install --save express
  npm install --save passport
  npm install --save express-session
  ```
  {: pre}

3. 将以下代码添加到 app.js 文件中，以便：
    * 将 express 应用程序设置为使用 express-session 中间件。**注**：必须针对生产环境为中间件配置合适的会话存储量。有关更多信息，请参阅 [expressjs 文档](https://github.com/expressjs/session)。
    * 使用序列化和反序列化来配置 passportjs。这对于跨 HTTP 请求的已认证会话持久性是必需的。有关更多信息，请参阅 [passportjs 文档](http://passportjs.org/docs)。
    * 通过在回调 URL 上运行 get 命令，从 App ID 服务中检索访问令牌和身份令牌。

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
  app.get("/protected", passport.authenticate(WebAppStrategy.STRATEGY_NAME), function(req, res)
    		res.json(req.user);
    });
  ```
  {: pre}

    **注**：服务将按以下顺序重定向：
    1. 触发认证流程的请求的原始 URL，此 URL 持久存储在 HTTP 会话中的 `WebAppStrategy.ORIGINAL_URL` 键下。
    2. 成功重定向，如 `passport.authenticate(name, {successRedirect: "...."})` 中所指定。
    3. 应用程序根目录（“/”）

4. 重新部署应用程序。


## 向现有 Swift Web 应用程序添加 {{site.data.keyword.appid_short_notm}}

1. 打开 Swift 应用程序目录中的 `Package.swift` 文件，并添加 `appid-serversdk-swift` 依赖项。例如：


    ```swift
    import PackageDescription

    let package = Package(
      dependencies: [
          .Package(url: "https://github.com/ibm-cloud-security/appid-serversdk-swift.git", majorVersion: 1)
      ]
  )
    ```
    {: pre}

2. 将以下代码添加到 Swift 应用程序中，以便：
    * 将 Kitura 设置为使用会话中间件。**注**：必须针对生产环境为 Kitura 配置合适的会话存储量。有关更多信息，请参阅 [Kitura 文档](https://github.com/IBM-Swift/Kitura-Session)。
    * 通过在回调 URL 上运行 get 命令，从 App ID 服务中检索访问令牌和身份令牌。

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
  {: pre}

  <table>
  <caption> 表 6. 命令组成部分说明</caption>
    <tr>
      <th> 组成部分</th>
      <th> 描述</th>
    </tr>
    <tr>
      <td> <i>var CALLBACK_URL</i></td>
      <td> /ibm/bluemix/appid/callback</td>
    </tr>
    <tr>
      <td> <i>var LANDING_PAGE_URL</i></td>
      <td> /index.html</td>
    </tr>
    </table>

5. 重新部署应用程序。



## 向不在 {{site.data.keyword.Bluemix_notm}} 上运行的现有应用程序添加 {{site.data.keyword.appid_short_notm}}


如果您有一个不在 Bluemix 上运行的 Node.js 或 Swift 应用程序，那么可以将 WebAppStrategy 或 WebAppKituraCredentialsPlugin 配置为远程工作。


在 Node.js 应用程序中，将 `passport.use(new WebAppStrategy());` 替换为以下代码。

  ```javaScript
  passport.use(new WebAppStrategy({
    	  tenantId: "{tenant-id}",
   	    clientId: "{client-id}",
      	secret: "{secret}",
      	oauthServerUrl: "{oauth-server-url}",
      	redirectUri: "{app-url}" + CALLBACK_URL
      }));
  ```
{: pre}

在 Swift 应用程序中，将 `let webappKituraCredentialsPlugin = WebAppKituraCredentialsPlugin()` 替换为以下代码。

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
  {: pre}

<table>
<caption> 表 7. Swift 和 Node.js 应用程序的命令组成部分说明</caption>
  <tr>
    <th> 组成部分</th>
    <th> 描述</th>
  </tr>
  <tr>
    <td> <i>tenantID</i></br> <i>clientID</i></br> <i>secret</i></br> <i>oauth-server-url</i></br> </td>
    <td> 可以通过单击服务仪表板的**服务凭证**选项卡中的**查看凭证**来找到这些值。</td>
  </tr>
  <tr>
    <td> <i>app-url</i></td>
    <td> 应用程序 URL。</td>
  </tr>
  <tr>
    <td> <i>CALLBACK_URL</i></td>
    <td> 用户登录后看到的页面的 URL。</td>
  </tr>
</table>
