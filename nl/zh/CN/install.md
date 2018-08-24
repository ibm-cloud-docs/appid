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

# 将 {{site.data.keyword.appid_short}} 添加到您的应用程序
{: #configuring}

通过在应用程序中设置服务来开始使用 {{site.data.keyword.appid_short}}。
{: shortdesc}


## 设置 Android SDK
{: #android-setup}

使用 {{site.data.keyword.appid_short}} 客户端 SDK 构建 Android 应用程序，初始化该 SDK，认证用户，然后对受保护和不受保护的资源发起请求。
{:shortdesc}


### 开始之前
{: #before-android}

您需要以下信息：
  * {{site.data.keyword.appid_short_notm}} 服务的实例。
  * 您的租户标识。您的租户标识是用于初始化应用程序的唯一标识，可在服务仪表板的**服务凭证**选项卡中找到。
  * 您所在的 {{site.data.keyword.Bluemix}} 区域。您可以通过查看 UI 来找到您所在的区域。此值用于初始化应用程序。
    <table><caption> 表 1. {{site.data.keyword.Bluemix_notm}} 区域及对应的 SDK 值</caption>
    <tr>
      <th>{{site.data.keyword.Bluemix}} 区域</th>
      <th>SDK 值</th>
    </tr>
    <tr>
      <td>美国南部</td>
      <td><code>AppID.REGION_US_SOUTH</code> </td>
    </tr>
    <tr>
      <td>悉尼</td>
      <td><code>AppID.REGION_SYDNEY</code></td>
    </tr>
    <tr>
      <td>英国</td>
      <td><code>AppID.REGION_UK</code></td>
    </tr>
    <tr>
      <td>德国</td>
      <td><code>AppID.REGION_GERMANY</code></td>
    </tr>
  </table>

  * <a href="https://developers.google.com/web/tools/setup/" target="_blank">Android Studio 项目 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>，设置为使用 Gradle。

### 安装 SDK
{: #install-android}

1. 创建 Android Studio 项目或打开现有项目。
2. 将 JitPack 存储库添加到根 `build.gradle` 文件。

  ```gradle
    allprojects {
	    repositories {
		    ...
		    maven { url 'https://jitpack.io' }
	    }
    }
  ```
  {: codeblock}

3. 找到应用程序的`build.gradle` 文件的 dependencies 部分，并为 {{site.data.keyword.appid_short_notm}} 客户端 SDK 添加编译依赖项。**注：**请确保打开应用程序的这一文件，而不是项目的 `build.gradle` 文件。


  ```gradle
   dependencies {
       compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:4.+'
   }
  ```
  {: codeblock}

5. 找到 `defaultConfig` 部分，并添加以下代码行。

  ```gradle
  defaultConfig {
  ...
  manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
  ```
  {: codeblock}

6. 使用 Gradle 同步项目。单击**工具 > Android > 使用 Gradle 文件同步项目**。

### 初始化 SDK
{: #initialize-android}

通过将上下文、租户标识和区域参数传递到 initialize 方法来初始化客户端 SDK。在 Android 应用程序中，通常会将初始化代码放置在主活动的 onCreate 方法中，但这不是强制性的。

  ```java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, AppID.REGION_UK);
  ```
  {: codeblock}

  <table>
  <caption> 表. 命令组成部分说明</caption>
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
      <td> 可以在 UI 中找到您所在的区域。选项为 `AppID.REGION_US_SOUTH`、`AppID.REGION_UK`、`AppID.REGION_Sydney` 或 `AppID.REGION_Germany`。</td>
    </tr>
  </table>

现在，您已准备好配置身份提供者并开始认证用户！有关更多信息，请参阅 <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">{{site.data.keyword.appid_short_notm}} Android GitHub 存储库 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>。


</br>

## 设置 iOS Swift SDK
{: #ios-setup}

使用 {{site.data.keyword.appid_short}} 客户端 SDK 构建 Swift 应用程序，初始化该 SDK，认证用户，然后对受保护和不受保护的资源发起请求。
{:shortdesc}


### 开始之前
{: #before-ios}

您需要以下信息：
  * {{site.data.keyword.appid_short_notm}} 的实例。
  * 您的租户标识。您的租户标识是用于初始化应用程序的唯一标识，可在服务仪表板的**服务凭证**选项卡中找到。
  * 您所在的 {{site.data.keyword.Bluemix_notm}} 区域。您可以通过查看 UI 来找到您所在的区域。此值用于初始化应用程序。
    
  <table> <caption> 表. {{site.data.keyword.Bluemix_notm}} 区域及对应的 SDK 值</caption>
    <tr>
      <th>{{site.data.keyword.Bluemix}} 区域</th>
      <th>SDK 值</th>
    </tr>
    <tr>
      <td>美国南部</td>
      <td><code>AppID.REGION_US_SOUTH</code></td>
    </tr>
    <tr>
      <td>悉尼</td>
      <td><code>AppID.REGION_SYDNEY</code></td>
    </tr>
    <tr>
      <td>英国</td>
      <td><code>AppID.REGION_UK</code></td>
    </tr>
    <tr>
      <td>德国</td>
      <td><code>AppID.REGION_GERMANY</code></td>
    </tr>
  </table>

  * Xcode 项目（V9.0.1 或更高版本）。
  * CocoaPods（V1.1.0 或更高版本）。


### 安装 SDK
{: #install-ios}

{{site.data.keyword.appid_short_notm}} 客户端 SDK 通过 CocoaPods 进行分发；CocoaPods 是用于 Swift 和 Objective-C Cocoa 项目的依赖项管理器。CocoaPods 会下载工件，并将其提供给项目使用。

1. 创建 Xcode 项目或打开现有项目。
2. 在项目的目录中打开或创建 podfile。
3. 在项目的目标后，添加“IBMCloudAppID”pod 的依赖项和 `use_frameworks!` 命令。

  ```swift
  target '<yourTarget>' do
     use_frameworks!
     pod 'IBMCloudAppID'
  end
  ```
  {: codeblock}

4. 下载“IBMCloudAppID”依赖项。

  ```swift
  pod install --repo-update
  ```
  {: codeblock}

6. 在 Xcode 项目中启用密钥链共享。浏览到**项目设置> 功能 > 密钥链共享**并选择**启用密钥链共享**。
7. 打开**项目设置 > 信息 > URL 类型**，并添加 **URL 类型**。将以下值放在**标识**和
**URL 方案**文本框中。
  ```
  $(PRODUCT_BUNDLE_IDENTIFIER)
  ```
  {: codeblock}


### 初始化 SDK
{: #initialize-ios}

1. 通过将租户标识和区域参数传递到 initialize 方法来初始化客户端 SDK。在 Swift 应用程序中，通常会将初始化代码放置在 AppDelegate 的 `application:didFinishLaunchingWithOptions` 方法中，但这不是强制性的。

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, region: AppID.Region_UK)
  ```
  {: codeblock}

  <table>
  <caption> 表. 命令组成部分说明</caption>
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
      <td> 可以在 UI 中找到您所在的区域。选项为 `AppID.REGION_US_SOUTH`、`AppID.REGION_UK`、`AppID.REGION_Sydney` 或 `AppID.REGION_Germany`。</td>
    </tr>
  </table>

2. 将以下导入项添加到 `AppDelegate` 文件。

    ```swift
    import IBMCloudAppID
    ```
    {: codeblock}

3. 将以下代码添加到 AppDelegate 文件中。

  ```swift
  func application( application: UIApplication, open url: URL, options :[UIApplicationOpenURLOptionsKey : Any]) -> Bool {
          return AppID.sharedInstance.application(application, open: url, options: options)
      }
  ```
  {: codeblock}

现在，您已准备好配置身份提供者并开始认证用户！有关 iOS SDK 的更多信息，请参阅 <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">{{site.data.keyword.appid_short_notm}} iOS GitHub 存储库 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>。

</br>

## 设置 Node.js SDK
{: #nodejs-setup}

### 开始之前
{: #before-nodejs}

请确保您已准备好以下先决条件，可以：
1. 安装 [IBM Cloud CLI](../cli/index.html)。
2. 使用 <a href="http://expressjs.com/" target="_blank">Express 框架 <img src="../icons/launch-glyph.svg" alt="外部链接图标"></a> 实施 Node.js 服务器。要安装 Express 框架，请使用命令行以打开包含 Node.js 应用程序的目录，然后运行以下命令：
  ```
  npm install --save express
  ```
  {: codeblock}
3. 安装 Passport。使用命令行以打开包含 Node.js 应用程序的目录，然后运行以下命令：
  ```
  npm install --save passport
  ```
  {: codeblock}

**注**：其他框架会使用 `Express` 框架，例如 LoopBack。可以将 {{site.data.keyword.appid_short_notm}} 服务器 SDK 与其中任意框架一起使用。


### 安装 SDK
{: #install-nodejs}

1. 使用命令行打开包含 Node.js 应用程序的目录。
2. 安装 {{site.data.keyword.appid_short_notm}} 服务。
  ```
  npm install --save ibmcloud-appid
  ```
  {: codeblock}

### 初始化 SDK
{: #initialize}

1. 将以下 `require` 定义添加到 `server.js` 文件。
    ```
    const express = require('express');
    const session = require('express-session')
    const passport = require('passport');
    const WebAppStrategy = require("ibmcloud-appid").WebAppStrategy;
    const CALLBACK_URL = "/ibm/cloud/appid/callback";
    ```
    {: codeblock}

2. 将 express 应用程序设置为使用 express-session 中间件。**注**：必须针对生产环境为中间件配置合适的会话存储量。有关更多信息，请参阅 <a href="https://github.com/expressjs/session" target="_blank">expressjs 文档 <img src="../icons/launch-glyph.svg" alt="外部链接图标"></a>。
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

3. 传递租户标识和凭证以初始化 SDK。
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

 <table summary="命令组成部分：Node.js 应用程序">
  <caption>Node.js 应用程序的命令组成部分</caption>
    <tr>
      <th>组成部分</th>
      <th>描述</th>
    </tr>
    <tr>
      <td><i>tenantID</i></td>
      <td>租户标识是用于初始化应用程序的唯一标识。您可以通过单击**服务凭证**选项卡中的**查看凭证**在 {{site.data.keyword.appid_short_notm}} 服务中查找值。</td>
    </tr>
    <tr>
      <td><i>clientID</i></br> <i>secret</i></br> <i>oauth-server-url</i></br> </td>
      <td>可以通过单击服务仪表板的**服务凭证**选项卡中的**查看凭证**来找到这些值。</td>
    </tr>
    <tr><td><i>redirectUri</i></td>
    <td>可通过以下三种方式提供 redirectUri 值：</br>
        1. 在 WebAppStrategy({redirectUri: "...."}) 中手动提供</br>
        2. 作为名为 `redirectUri` 的环境变量提供</br>
        3. 如果未提供以上任何一项，那么 App ID SDK 将尝试检索正在 IBM Cloud 上运行的应用程序的 application_uri 并附加缺省后缀“/ibm/cloud/appid/callback”</td>
    </tr>
    <tr>
      <td><i>CALLBACK_URL</i></td><td>用户登录后看到的页面的 URL。</td>
    </tr>
  </table>

4. 使用序列化和反序列化来配置 passport。此配置对于跨 HTTP 请求的已认证会话持久性是必需的。有关更多信息，请参阅 <a href="http://passportjs.org/docs" target="_blank">passport 文档 <img src="../icons/launch-glyph.svg" alt="外部链接图标"></a>。

  ```
  passport.serializeUser(function(user, cb) {
    cb(null, user);
    });

    passport.deserializeUser(function(obj, cb) {
      cb(null, obj);
    });
  ```
  {: codeblock}

5. 向 `server.js` 文件添加以下代码以发出服务重定向：
   ```
   app.get(CALLBACK_URL, passport.authenticate(WebAppStrategy.STRATEGY_NAME));
   app.get('/protected', passport.authenticate(WebAppStrategy.STRATEGY_NAME)), function(req, res)
        res.json(req.user);
   });
   ```
   {: codeblock}

   **注**：服务将按以下顺序重定向：
    1. 触发认证流程的请求的原始 URL，此 URL 持久存储在 HTTP 会话中的 `WebAppStrategy.ORIGINAL_URL` 键下。
    2. 成功重定向，如 `passport.authenticate(name, {successRedirect: "...."}).`
    3. 应用程序根目录（“/”）

6. 重新部署应用程序。

有关更多信息，请参阅 <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">{{site.data.keyword.appid_short_notm}} Node.js GitHub 存储库 <img src="../icons/launch-glyph.svg" alt="外部链接图标"></a>。

## 设置 Swift SDK
{: #swift-setup}

使用 {{site.data.keyword.appid_short}} 服务器 SDK 保护后端和 API。
{:shortdesc}


### 开始之前
{: #before-swift}

在使用 Swift SDK 之前，您必须满足以下先决条件：

*  MacOS 或 Linux
* OpenSSL 1.0.2 (Linux)
* 安装 Swift 3.0.2
* 安装 Kitura 1.6


### 安装 SDK
{: #install-swift}

1. 打开 Swift 应用程序目录中的 `Package.swift` 文件，并添加 `appid-serversdk-swift` 依赖项。

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

2. 对于 MacOS：在命令行上构建时，所有软件包都应包含以下标志。
  ```
  swift build -Xlinker -L/usr/local/opt/openssl/lib -Xcc -I/usr/local/opt/openssl/include
  ```
  {: pre}

3. 创建 xcodeproject 时，请使用以下命令：
  ```
  swift package generate-xcodeproj --xcconfig-overrides openssl.xcconfig
  ```
  {: pre}

  您可以从 <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">{{site.data.keyword.appid_short_notm}} Swift GitHub <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>复制openssl.xcconfig
  {: tip}

4. 将以下代码添加到 Swift 应用程序中，以便：
    * 将 Kitura 设置为使用会话中间件。**注**：必须针对生产环境为 Kitura 配置合适的会话存储量。有关更多信息，请参阅 <a href="https://github.com/IBM-Swift/Kitura-Session" target="_blank">Kitura 文档 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>。
    * 通过对回调 URL 运行 get 命令，从 {{site.data.keyword.appid_short_notm}} 服务中检索访问令牌和身份令牌。

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

5. 重新部署应用程序。

</br>

## 设置 Liberty for Java SDK
{: #lfj-setup}

可以将 {{site.data.keyword.appid_short_notm}} 配置为与 Liberty for Java Web 应用程序一起运作。{:shortdesc}

1. 向 `server.xml` 中添加 <a href="https://www.ibm.com/support/knowledgecenter/en/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/twlp_config_oidc_rp.html" target="_blank">OpenID Connect 功能 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>。

  ```xml
  <feature manager>
  <feature>appSecurity-2.0</feature>
  <feature>openidConnectClient-1.0</feature>  
  ```
  {: codeblock}

2. 在 OpenID Connect 客户机功能中，定义以下占位符。这些占位符以后会由 {{site.data.keyword.Bluemix_notm}} 自动填充。实例名称变量必须与您的 {{site.data.keyword.appid_short_notm}} 实例名称完全匹配。

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

  **注**：issuerIdentifier 变量会根据您的区域而变化。可以是以下其中一个变量：
  * issuerIdentifier="appid-oauth.ng.bluemix.net"
  * issuerIdentifier="appid-oauth.eu-gb.bluemix.net"
  * issuerIdentifier="appid-oauth.au-syd.bluemix.net"</ul> </td>

3. 定义授权过滤器以指定受保护资源。如果未<a href="https://www.ibm.com/support/knowledgecenter/en/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/rwlp_auth_filter.html" target="_blank">定义 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 过滤器，那么服务将保护所有资源。
  ```
  <authFilter id="myAuthFilter">
             <requestUrl id="myRequestUrl" urlPattern="/protected" matchType="contains"/>
    </authFilter>
  ```
  {: codeblock}

4. 在 `server.xml` 文件中，将特殊主体类型定义为 ALL_AUTHENTICATED_USERS。

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

5. 在 `<application-bnd>` 元素中，<a href="https://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_authorization.html?cp=SSAW57_8.5.5&cm_mc_uid=18498555367014888859884&cm_mc_sid_50200000=1494855872" target="_blank">定义角色 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>，如 Web 应用程序 `web.xml` 中所示。

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

6. 获取证书。

    a. 在 {{site.data.keyword.appid_short_notm}} 仪表板中，单击“服务凭证”。

    b. 单击**查看凭证**，然后复制 `oauthServerUrl`。

    c. 向 URL 中添加 `/token`。使用 Firefox 来浏览输出 URL 并获取证书。例如，可以使用以下 URL。

    ```
    https://appid-oauth.ng.bluemix.net/oauth/v3/5d12852e-b0a0-46a3-9547-67a4a33a7164/token
    ```
    {: screen}

    d. 在 Firefox 地址栏中，单击“锁定”图标 > **右箭头** > **更多信息** > **查看证书**。

    e. 在**安全**选项卡中，单击**查看证书** > **详细信息**。

    f. 导出证书，并将其作为 PEM 文件保存在本地驱动器上。

7. 使用 <a href="https://www.ibm.com/support/knowledgecenter/SSYKE2_6.0.0/com.ibm.java.security.component.60.doc/security-component/keytoolDocs/keytool_overview.html" target="_blank">Liberty Keytool <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 将证书添加到 Liberty for Java truststore.jks 文件中，然后在 OIDC 元素中添加对该证书别名的引用。`.jks 文件`位于服务器目录中：**resources** > **security** > **<i>truststore file name</i>** > **`.jks 文件`**。可以使用以下其中一个选项将证书添加到该文件中。

    * 在终端中，转至 Liberty for Java security 文件夹 (wlp > usr > servers > <i>servername</i> > resources > security)，然后使用以下命令添加证书。

      ```
      keytool -importcert -keystore ./trust.jks -file ~/Documents/secbluemix.cer`
      ```
      {: codeblock}      

      **注**：`~/Documents/[certificatename].cer` 指示本地驱动器上的文件位置。

    * 可以使用 <a href="http://keystore-explorer.org/index.html" target="_blank">KeyStore Explorer <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 来添加证书。打开 KeyStore Explorer，然后选择**打开现有密钥库**。

    **注**：证书可能已到期/更改，在此情况下，应使用新证书更新信任库。

8. 在 `manifest.yml` 文件中，定义 {{site.data.keyword.appid_short_notm}} 实例。

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

    下面是为 {{site.data.keyword.appid_short_notm}} 配置的示例 `server.xml` 文件：

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

## 向不在 {{site.data.keyword.Bluemix_notm}} 上运行的现有应用程序添加 {{site.data.keyword.appid_short_notm}}
{: #existing}

您可以向不在 {{site.data.keyword.Bluemix_notm}} 上运行的应用程序添加 {{site.data.keyword.appid_short_notm}}。您可以在本主题中看到一些示例，但并非只有这些语言可使用此服务。

</br>

**Node.js**

在 Node.js 应用程序中，将 `passport.use(new WebAppStrategy());` 替换为以下代码。

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
  <caption> 表.  Node.js 应用程序的命令组成部分说明</caption>
    <tr>
      <th> 组成部分</th>
      <th> 描述</th>
    </tr>
    <tr>
      <td><code>tenant-id</code> </br> <code>clientID</code></br> <code>secret</code></br> <code>oauth-server-url</code></br></td>
      <td> 可以通过单击服务仪表板的**服务凭证**选项卡中的**查看凭证**来找到这些值。</td>
    </tr>
    <tr>
      <td><code>app-url</code></td><td>应用程序 URL。</td>
    </tr>
    <tr>
      <td><code>CALLBACK_URL</code></td><td> 用户登录后看到的页面的 URL。</td>
    </tr>
  </table>

</br>

**Swift**

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
  {: codeblock}

  <table>
  <caption>表.  Swift 应用程序的命令组成部分说明</caption>
    <tr>
      <th> 组成部分</th>
      <th> 描述</th>
    </tr>
    <tr>
      <td><code>tenant-id</code> </br> <code>clientID</code></br> <code>secret</code></br> <code>oauth-server-url</code></br></td>
      <td> 可以通过单击服务仪表板的**服务凭证**选项卡中的**查看凭证**来找到这些值。</td>
    </tr>
    <tr>
      <td><code>app-url</code></td><td>应用程序 URL。</td>
    </tr>
    <tr>
      <td><code>CALLBACK_URL</code></td><td> 用户登录后看到的页面的 URL。</td>
    </tr>
  </table>


</br>

**Liberty for Java**

在 Liberty for Java 应用程序中，完成[设置 Liberty for Java SDK](#lfj-setup) 之下的步骤，但是将 OIDC 客户机元素变量替换为以下代码。

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
  <caption>表. Liberty for Java 应用程序的 OIDC 元素变量</caption>
    <tr>
      <th> 组成部分</th>
      <th> 描述</th>
    </tr>
    <tr>
    <td><code>clientID</code></br> <code>secret</code></br> <code>oauth-server-url</code></br></td>
    <td>可以通过单击服务仪表板的**服务凭证**选项卡中的**查看凭证**来找到这些值。</td>
    </tr>
    <tr>
      <td><code>authorizationEndpointURL</code></td><td> 将 `/authorization` 添加到 oauthServerURL 的末尾。</td>
    </tr>
    <tr>
      <td><code>tokenEndpointUrl</code></td><td>将 `/token` 添加到 oauthServerURL 的末尾。</td>
    </tr>
    <tr>
      <td><code>jwkEndpointUrl</code></td><td>将 `/publickeys` 添加到 oauthServerURL 的末尾。</td>
    </tr>
    <tr>
      <td><code>issuerIdentifier</code></td><td>该变量会根据您的区域而变化。可以是以下其中一项：</br><ul><li>issuerIdentifier="appid-oauth.ng.bluemix.net"</br><li> issuerIdentifier="appid-oauth.eu-gb.bluemix.net"</br><li>issuerIdentifier="appid-oauth.au-syd.bluemix.net"</ul></td>
    </tr>
    <tr>
      <td><code>tokenEndpointAuthMethod</code></td><td>被指定为“basic”。</td>
    </tr>
    <tr>
      <td><code>signatureAlgorithm</code></td><td>被指定为“RS256”。</td>
    </tr>
    <tr>
      <td><code>authFilterid</code></td><td>要保护的资源的列表。</td>
    </tr>
    <tr>
      <td><code>trustAliasName</code></td><td>信任库中证书的名称。</td>
    </tr>
  </table>
