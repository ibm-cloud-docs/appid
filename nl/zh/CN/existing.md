---

copyright:
  years: 2017
lastupdated: "2017-12-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


# 向现有应用程序添加 {{site.data.keyword.appid_short_notm}}

可以将 {{site.data.keyword.appid_full}} 用于现有应用程序以认证和存储有关用户的概要文件信息。


## 先决条件

* 现有 iOS Swift、Android、Node.js、Swift 或 Liberty for Java 应用程序。
* 现有 {{site.data.keyword.appid_short_notm}} 实例。


## 向现有 Android 应用程序添加 {{site.data.keyword.appid_short_notm}}
{: #existing-android}

可以将 {{site.data.keyword.appid_short_notm}} 服务添加到现有 Android 应用程序。

1. 将 JitPack 存储库添加到根 `build.gradle` 文件。

  ```gradle
  allprojects {
      		repositories {
		    ...
         	 maven { url 'https://jitpack.io' }
	    }
    }
  ```
  {: codeblock}

2. 打开应用程序的 `build.gradle` 文件，找到该文件的 dependencies 部分，并为 {{site.data.keyword.appid_short_notm}} 客户端 SDK 添加编译依赖项。

  ```gradle
  dependencies {
      compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:1.+'
   }
  ```
  {: codeblock}

3. 找到 defaultConfig 部分，并添加以下代码行。

  ```gradle
  defaultConfig {
                         ...
            manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
  ```
  {: codeblock}

4. 使用 Gradle 同步项目。
5. 通过将上下文、租户标识和区域参数传递到 initialize 方法来初始化客户端 SDK。在 Android 应用程序中，通常会将初始化代码放置在主活动的 onCreate 方法中，但这不是强制性的。

  ```Java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, <AppID.REGION>);
  ```
  {: codeblock}

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
  {: codeblock}

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
{: #existing-ios}

1. 在项目的目录中打开 podfile。
2. 在项目的目标下，添加“BluemixAppID”pod 的依赖项。确保 `use_frameworks!` 命令也位于目标下。
3. 要下载 `BluemixAppID` 依赖项，请运行以下命令。

  ```
  pod install --repo-update
  ```
  {: codeblock}

4. 打开 Xcode 项目并启用密钥链共享。在**项目设置**下，单击**功能** > **密钥链共享**。
5. 在**项目设置** > **信息** > **URL 类型**下，添加 **URL 类型**。使用以下值填充**标识**文本框和 **URL 方案**文本框。

  ```
  $(PRODUCT_BUNDLE_IDENTIFIER)
  ```
  {: codeblock}

6. 将以下 import 语句添加到 `AppDelegate.swift` 文件中。

  ```swift
  import BluemixAppID
  import BMSCore
  ```
  {: codeblock}

7. 通过将租户标识和区域参数传递到 initialize 方法来初始化客户端 SDK。在应用程序中，通常会将初始化代码放置在 AppDelegate 的 application:didFinishLaunchingWithOptions: 方法中，但这不是强制性的。

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, bluemixRegion: <AppID.Region>)
  ```
  {: codeblock}

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
  {: codeblock}

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
{: #existing-node}

1. 将 `bluemix-appid` 模块添加到 Node.js 应用程序。

  ```javaScript
  npm install --save bluemix-appid
  ```
  {: codeblock}

2. 如果尚未安装以下模块，请进行安装。

  ```javaScript
  npm install --save express
  npm install --save passport
  npm install --save express-session
  ```
  {: codeblock}

3. 将以下代码添加到 `app.js` 文件中，以便：
    * 将 express 应用程序设置为使用 express-session 中间件。**注**：必须针对生产环境为中间件配置合适的会话存储量。有关更多信息，请参阅 <a href="https://github.com/expressjs/session" target="_blank">expressjs 文档 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>。
    * 使用序列化和反序列化来配置 passportjs。这对于跨 HTTP 请求的已认证会话持久性是必需的。有关更多信息，请参阅 <a href="http://passportjs.org/docs" target="_blank">passportjs 文档 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>。  
    * 通过对回调 URL 运行 get 命令，从 {{site.data.keyword.appid_short_notm}} 服务中检索访问令牌和身份令牌。

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

    **注**：服务将按以下顺序重定向：
    1. 触发认证流程的请求的原始 URL，此 URL 持久存储在 HTTP 会话中的 `WebAppStrategy.ORIGINAL_URL` 键下。
    2. 成功重定向，如 `passport.authenticate(name, {successRedirect: "...."}).`
    3. 应用程序根目录（“/”）

4. 重新部署应用程序。


## 向现有 Swift Web 应用程序添加 {{site.data.keyword.appid_short_notm}}
{: #existing-swift}

1. 打开 Swift 应用程序目录中的 `Package.swift` 文件，并添加 `appid-serversdk-swift` 依赖项。例如：


    ```swift
    import PackageDescription

    let package = Package(
      dependencies: [
          .Package(url: "https://github.com/ibm-cloud-security/appid-serversdk-swift.git", majorVersion: 1)
      ]
  )
    ```
    {: codeblock}

2. 将以下代码添加到 Swift 应用程序中，以便：
    * 将 Kitura 设置为使用会话中间件。**注**：必须针对生产环境为 Kitura 配置合适的会话存储量。有关更多信息，请参阅 <a href="https://github.com/IBM-Swift/Kitura-Session" target="_blank">Kitura 文档 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>。
    * 通过对回调 URL 运行 get 命令，从 {{site.data.keyword.appid_short_notm}} 服务中检索访问令牌和身份令牌。

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
  <caption> 表 5. 命令组成部分说明</caption>
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



## 向现有 Liberty for Java 应用程序添加 {{site.data.keyword.appid_short_notm}}
{: #existing-liberty}

可以将 {{site.data.keyword.appid_short_notm}} 配置为与现有 Liberty for Java Web 应用程序一起运作。

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

3. 在 `server.xml` 文件中，将特殊主体类型定义为 ALL_AUTHENTICATED_USERS。

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

4. 在 `<application-bnd>` 元素中，<a href="https://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_authorization.html?cp=SSAW57_8.5.5&cm_mc_uid=18498555367014888859884&cm_mc_sid_50200000=1494855872" target="_blank">定义角色 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>，如 Web 应用程序 `web.xml` 中所示。

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

5. 获取证书。

    a. 在 {{site.data.keyword.appid_short_notm}} 仪表板中，单击“服务凭证”。

    b. 单击**查看凭证**，然后复制 `oauthServerUrl`。

    c. 向 URL 中添加 `/token`。使用 Firefox 来浏览输出 URL 并获取证书。例如，可以使用以下 URL。

    ```
    https://appid-oauth.eu-gb.bluemix.net/oauth/v3/5d12852e-b0a0-46a3-9547-67a4a33a7164/token
    ```
    {: screen}

    d. 在 Firefox 地址栏中，单击“锁定”图标 > **右箭头** > **更多信息** > **查看证书**。

    e. 在**安全**选项卡中，单击**查看证书** > **详细信息**。

    f. 导出证书，并将其作为 PEM 文件保存在本地驱动器上。

6. 使用 <a href="https://www.ibm.com/support/knowledgecenter/SSYKE2_6.0.0/com.ibm.java.security.component.60.doc/security-component/keytoolDocs/keytool_overview.html" target="_blank">Liberty Keytool <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 将证书添加到 Liberty for Java truststore.jks 文件中，然后在 OIDC 元素中添加对该证书别名的引用。`.jks 文件`位于服务器目录中：**resources** > **security** > **<i>truststore file name</i>** > **`.jks 文件`**。可以使用以下其中一个选项将证书添加到该文件中。

    * 在终端中，转至 Liberty for Java security 文件夹 (wlp > usr > servers > <i>servername</i> > resources > security)，然后使用以下命令添加证书。

      ```
      keytool -importcert -keystore ./trust.jks -file ~/Documents/secbluemix.cer`
      ```
      {: codeblock}      

      **注**：`~/Documents/[certificatename].cer` 指示本地驱动器上的文件位置。

    * 可以使用 <a href="http://keystore-explorer.org/index.html" target="_blank">KeyStore Explorer <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 来添加证书。打开 KeyStore Explorer，然后选择**打开现有密钥库**。

7. 在 `manifest.yml` 文件中，定义 {{site.data.keyword.appid_short_notm}} 实例。

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



## 向不在 {{site.data.keyword.Bluemix_notm}} 上运行的现有应用程序添加 {{site.data.keyword.appid_short_notm}}
{: #existing}

如果您有一个不在 {{site.data.keyword.Bluemix_notm}} 上运行的 Node.js 或 Swift 应用程序，那么可以将 WebAppStrategy 或 WebAppKituraCredentialsPlugin 配置为远程工作。对于不在 Bluemix 上运行的 Liberty for Java 应用程序，请配置 OIDC 元素变量。


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
  {: codeblock}

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
  <caption> 表 6. Swift 和 Node.js 应用程序的命令组成部分说明</caption>
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

在 Liberty for Java 应用程序中，完成[向现有 Liberty for Java 应用程序添加 {{site.data.keyword.appid_short_notm}}](/docs/services/appid/existing.html#existing-liberty) 之下的步骤，但要将 OIDC 客户机元素变量替换为以下代码。

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
  <caption> 表 7. 不在 Bluemix 上运行的 Liberty for Java 应用程序的 OIDC 元素变量</caption>
    <tr>
      <th> 组成部分</th>
      <th> 描述</th>
    </tr>
    <tr>
    <td> <i>clientID</i></br> <i>secret</i></br> <i>oauth-server-url</i></br> </td>
    <td> 可以通过单击服务仪表板的**服务凭证**选项卡中的**查看凭证**来找到这些值。</td>
    </tr>
    <tr>
      <td> <i>authorizationEndpointURL</i></td>
      <td> 将 `/authorization` 添加到 oauthServerURL 的末尾。</td>
    </tr>
    <tr>
      <td> <i>tokenEndpointUrl</i></td>
      <td> 将 `/token` 添加到 oauthServerURL 的末尾。</td>
    </tr>
    <tr>
      <td> <i>jwkEndpointUrl</i></td>
      <td> 将 `/publickeys` 添加到 oauthServerURL 的末尾。</td>
    </tr>
    <tr>
      <td> <i>issuerIdentifier</i></td>
      <td> 该变量会根据您的区域而变化。可以是以下其中一项：</br><ul><li> issuerIdentifier="appid-oauth.ng.bluemix.net"</br><li> issuerIdentifier="appid-oauth.eu-gb.bluemix.net"</br><li> issuerIdentifier="appid-oauth.au-syd.bluemix.net"</ul></td>
    </tr>
    <tr>
      <td> <i>tokenEndpointAuthMethod</i></td>
      <td> 被指定为“basic”。</td>
    </tr>
    <tr>
      <td> <i>signatureAlgorithm</i></td>
      <td> 被指定为“RS256”。</td>
    </tr>
    <tr>
      <td> <i>authFilterid</i></td>
      <td> 要保护的资源的列表。</td>
    </tr>
    <tr>
      <td> <i>trustAliasName</i></td>
      <td> 信任库中证书的名称。</td>
    </tr>
  </table>
