---

copyright:
  years: 2017, 2018
lastupdated: "2018-01-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


# 既存のアプリへの {{site.data.keyword.appid_short_notm}} の追加

既存のアプリケーションで {{site.data.keyword.appid_full}} を使用して、認証を行い、ユーザーに関するプロファイル情報を保管できます。


## 前提条件

* iOS Swift、Android、Node.js、Swift、Liberty for Java の既存のアプリケーション。
* {{site.data.keyword.appid_short_notm}} の既存のインスタンス。


## 既存の Android アプリへの {{site.data.keyword.appid_short_notm}} の追加
{: #existing-android}

既存の Android アプリケーションに {{site.data.keyword.appid_short_notm}} サービスを追加できます。

1. JitPack リポジトリーをルートの `build.gradle` ファイルに追加します。

  ```gradle
  allprojects {
      		repositories {
         	 ...
         	 maven { url 'https://jitpack.io' }
	    }
  }
  ```
  {: codeblock}

2. アプリケーションの `build.gradle` ファイルを開き、ファイルの従属関係セクションを見つけて、{{site.data.keyword.appid_short_notm}} Client SDK 用のコンパイル従属関係を追加します。

  ```gradle
  dependencies {
      compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:1.+'
   }
  ```
  {: codeblock}

3. defaultConfig セクションを見つけて、以下のコード行を追加します。

  ```gradle
  defaultConfig {
                         ...
            manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
  ```
  {: codeblock}

4. プロジェクトを Gradle と同期化します。
5. context、tenant ID、region パラメーターを initialize メソッドに渡して、Client SDK を初期化します。 初期化コードの配置場所として一般的な (必須ではありません) 場所は、Android アプリケーションのメイン・アクティビティーの onCreate メソッド内です。

  ```Java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, <AppID.REGION>);
  ```
  {: codeblock}

    <table>
    <caption> 表 1. コマンドのコンポーネントの説明 </caption>
      <tr>
        <th> コンポーネント </th>
        <th> 説明 </th>
      </tr>
      <tr>
        <td> <i> tenantID </i> </td>
        <td> この値を見つけるには、サービス・ダッシュボードの**「サービス資格情報」**タブで**「資格情報の表示」**をクリックします。 </td>
      </tr>
      <tr>
        <td> <i> AppID.REGION </i> </td>
        <td> 地域は UI に示されています。 オプションは、`AppID.REGION_US_SOUTH`、`AppID.REGION_UK`、または `AppID.REGION_Sydney` です。 </td>
      </tr>
    </table>

6. {{site.data.keyword.appid_short_notm}} Client SDK が初期化されたら、ログイン・ウィジェットを実行してユーザーを認証できるようになります。

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
    <caption> 表 2. コマンドのコンポーネントの説明 </caption>
      <tr>
        <th> コンポーネント </th>
        <th> 説明 </th>
      </tr>
      <tr>
        <td> <i> onAuthorizationFailure </i> </td>
        <td> 例外が発生しました。 </td>
      </tr>
      <tr>
        <td> <i> onAuthorizationCanceled </i> </td>
        <td> 認証プロセスは、ユーザーによって取り消されました。 </td>
      </tr>
      <tr>
        <td> <i> onAuthorizationSuccess </i> </td>
        <td> ユーザーは認証されました。 </td>
      </tr>
    </table>

## 既存の iOS アプリケーションへの {{site.data.keyword.appid_short_notm}} の追加
{: #existing-ios}

1. プロジェクトのディレクトリー内の podfile を開きます。
2. プロジェクトのターゲットの下に、「BluemixAppID」Pod の従属関係を追加します。 必ず、`use_frameworks!` コマンドもターゲットの下に置いてください。
3. `BluemixAppID` の従属関係をダウンロードするには、以下のコマンドを実行します。

  ```
  pod install --repo-update
  ```
  {: codeblock}

4. Xcode プロジェクトを開き、キーチェーン共有を使用可能にします。 **「Project Settings」**の下で、**「Capabilities」** > **「Keychain Sharing」**をクリックします。
5. **「Project Settings」** > **「Info」** > **「URL Types」**の下で、**「URL Type」**を追加します。 **「Identifier」**テキスト・ボックスと**「URL Scheme」**テキスト・ボックスの両方に、以下の値を入力します。

  ```
  $(PRODUCT_BUNDLE_IDENTIFIER)
  ```
  {: codeblock}

6. `AppDelegate.swift` ファイルに以下のインポートを追加します。

  ```swift
  import BluemixAppID
  import BMSCore
  ```
  {: codeblock}

7. tenant ID パラメーターと region パラメーターを initialize メソッドに渡して、Client SDK を初期化します。 初期化コードを入れる一般的な場所 (ただし、これは必須ではありません) は、アプリケーションの AppDelegate の application:didFinishLaunchingWithOptions: メソッド内です。

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, bluemixRegion: <AppID.Region>)
  ```
  {: codeblock}

    <table>
    <caption> 表 3. コマンドのコンポーネントの説明 </caption>
      <tr>
        <th> コンポーネント </th>
        <th> 説明 </th>
      </tr>
      <tr>
        <td> <i> tenantID </i> </td>
        <td> この値を見つけるには、サービス・ダッシュボードの**「サービス資格情報」**タブで**「資格情報の表示」**をクリックします。 </td>
      </tr>
      <tr>
        <td> <i> AppID.REGION </i> </td>
        <td> 地域は UI に示されています。 オプションは、`AppID.REGION_US_SOUTH`、`AppID.REGION_UK`、または `AppID.REGION_Sydney` です。 </td>
      </tr>
    </table>

8. 以下のコードを AppDelegate ファイルに追加します。

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
    <caption> 表 4. コマンドのコンポーネントの説明 </caption>
      <tr>
        <th> コンポーネント </th>
        <th> 説明 </th>
      </tr>
      <tr>
        <td> <i> onAuthorizationSuccess </i> </td>
        <td> ユーザーは認証されました。 </td>
      </tr>
      <tr>
        <td> <i> onAuthorizationCanceled </i> </td>
        <td> 認証プロセスは、ユーザーによって取り消されました。 </td>
      </tr>
      <tr>
        <td> <i> onAuthorizationFailure </i> </td>
        <td> 例外が発生しました。 </td>
      </tr>
    </table>

## 既存の Node.js Web アプリへの {{site.data.keyword.appid_short_notm}} の追加
{: #existing-node}

1. Node.js アプリケーションに `bluemix-appid` モジュールを追加します。

  ```javaScript
  npm install --save bluemix-appid
  ```
  {: codeblock}

2. まだインストールしていない場合、以下のモジュールをインストールします。

  ```javaScript
  npm install --save express
  npm install --save passport
  npm install --save express-session
  ```
  {: codeblock}

3. 次の目的で、`app.js` ファイルに以下のコードを追加します。
    * express-session ミドルウェアを使用するように Express アプリをセットアップする。 **注**: ミドルウェアには、実稼働環境用の適切なセッション・ストレージを構成する必要があります。 詳細については、<a href="https://github.com/expressjs/session" target="_blank">expressjs の資料 <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を参照してください。
    * passportjs にシリアライゼーションとデシリアライゼーションを構成する。 これは、複数の HTTP 要求にわたって認証済みセッション・パーシスタンスを維持するために必要です。 詳細については、<a href="http://passportjs.org/docs" target="_blank">passportjs の資料 <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を参照してください。  
    * コールバック URL で GET コマンドを実行して、{{site.data.keyword.appid_short_notm}} サービスからアクセス・トークンと識別トークンを取得する。

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

    **注**: サービスは、以下の順序でリダイレクトされます。
    1. `WebAppStrategy.ORIGINAL_URL` キーの下の HTTP セッションに永続する、認証プロセスを起動した要求の元の URL。
    2. 正常に実行されたリダイレクト (`passport.authenticate(name, {successRedirect: "...."})` で指定)。
    3. アプリケーションのルート (「/」)

4. アプリケーションを再デプロイします。


## 既存の Swift Web アプリケーションへの {{site.data.keyword.appid_short_notm}} の追加
{: #existing-swift}

1. Swift アプリのディレクトリーにある `Package.swift` ファイルを開き、`appid-serversdk-swift` 従属関係を追加します。
  以下に例を示します。

    ```swift
    import PackageDescription

    let package = Package(
      dependencies: [
           	.Package(url: "https://github.com/ibm-cloud-security/appid-serversdk-swift.git", majorVersion: 1)
      ]
    )
    ```
    {: codeblock}

2. 次の目的で、Swift アプリケーションに以下のコードを追加します。
    * session ミドルウェアを使用するように Kitura をセットアップする。 **注**: Kitura には、実稼働環境用の適切なセッション・ストレージを構成する必要があります。 詳細については、<a href="https://github.com/IBM-Swift/Kitura-Session" target="_blank">Kitura の資料 <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を参照してください。
    * コールバック URL で GET コマンドを実行して、{{site.data.keyword.appid_short_notm}} サービスからアクセス・トークンと識別トークンを取得する。

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
  <caption> 表 5. コマンドのコンポーネントの説明 </caption>
    <tr>
      <th> コンポーネント </th>
      <th> 説明 </th>
    </tr>
    <tr>
      <td> <i> var CALLBACK_URL </i> </td>
      <td> /ibm/bluemix/appid/callback </td>
    </tr>
    <tr>
      <td> <i> var LANDING_PAGE_URL </i> </td>
      <td> /index.html </td>
    </tr>
    </table>

5. アプリケーションを再デプロイします。



## 既存の Liberty for Java アプリケーションへの {{site.data.keyword.appid_short_notm}} の追加
{: #existing-liberty}

{{site.data.keyword.appid_short_notm}} で、既存の Liberty for Java Web アプリケーションを操作するための構成を行います。

1. <a href="https://www.ibm.com/support/knowledgecenter/en/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/twlp_config_oidc_rp.html" target="_blank">OpenID Connect 機能 <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を `server.xml` に追加します。

  ```xml
  <feature manager>
  <feature>appSecurity-2.0</feature>
  <feature>openidConnectClient-1.0</feature>  
  ```
  {: codeblock}

2. Open ID Connect Client 機能で以下のプレースホルダーを定義します。 プレースホルダーの値は、後で {{site.data.keyword.Bluemix_notm}} によって自動的に設定されます。 インスタンス名の変数は、{{site.data.keyword.appid_short_notm}} インスタンスの名前と一致していなければなりません。

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

  **注**: issuerIdentifier 変数は、地域によって変わります。 以下のいずれかの変数になります。
  * issuerIdentifier="appid-oauth.ng.bluemix.net"
  * issuerIdentifier="appid-oauth.eu-gb.bluemix.net"
  * issuerIdentifier="appid-oauth.au-syd.bluemix.net"</ul> </td>

3. 保護リソースを指定するための許可フィルターを定義します。 フィルターを<a href="https://www.ibm.com/support/knowledgecenter/en/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/rwlp_auth_filter.html" target="_blank">定義 <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> しない場合は、サービスによってすべてのリソースが保護されます。
  ```
  <authFilter id="myAuthFilter">
             <requestUrl id="myRequestUrl" urlPattern="/protected" matchType="contains"/>
    </authFilter>
  ```
  {: codeblock}

3. `server.xml` ファイルで、特殊対象タイプを ALL_AUTHENTICATED_USERS として定義します。

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

4. `<application-bnd>` 要素で、Web アプリケーションの `web.xml` のとおりに<a href="https://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_authorization.html?cp=SSAW57_8.5.5&cm_mc_uid=18498555367014888859884&cm_mc_sid_50200000=1494855872" target="_blank">役割を定義します <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a>。

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

5. 証明書を取得します。

    a. {{site.data.keyword.appid_short_notm}} ダッシュボードで「サービス資格情報」をクリックします。

    b. **「資格情報の表示」**をクリックして、`oauthServerUrl` をコピーします。

    c. URL に `/token` を追加します。 Firefox で出力の URL を参照して、証明書を取得します。 例えば、以下のような URL を使用できます。

    ```
    https://appid-oauth.eu-gb.bluemix.net/oauth/v3/5d12852e-b0a0-46a3-9547-67a4a33a7164/token
    ```
    {: screen}

    d. Firefox のアドレス・バーで、錠のアイコン > **右矢印** > **「詳細を表示」** > **「証明書を表示」**をクリックします。

    e. **「セキュリティー」**タブで**「証明書を表示」** > **「詳細」**をクリックします。

    f. 証明書をエクスポートして、ローカル・ドライブに PEM ファイルとして保存します。

6. 証明書を Liberty for Java の truststore.jks ファイルに追加します。そのために、<a href="https://www.ibm.com/support/knowledgecenter/SSYKE2_6.0.0/com.ibm.java.security.component.60.doc/security-component/keytoolDocs/keytool_overview.html" target="_blank">Liberty Keytool <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を使用し、証明書別名への参照を OIDC 要素に追加してください。 `.jks ファイル`は、サーバー・ディレクトリー (**resources** > **security** > **<i>トラストストア・ファイル名</i>** > **`.jks ファイル`**) にあります。 以下のいずれかのオプションを使用して、証明書をファイルに追加できます。

    * 端末で Liberty for Java セキュリティー・フォルダー (wlp > usr > servers > <i>サーバー名</i> > resources > security) に移動し、以下のコマンドを使用して証明書を追加します。

      ```
      keytool -importcert -keystore ./trust.jks -file ~/Documents/secbluemix.cer`
      ```
      {: codeblock}      

      **注**: `~/Documents/[certificatename].cer` は、ご使用のローカル・ドライブ上のファイルの場所です。

    * <a href="http://keystore-explorer.org/index.html" target="_blank">KeyStore Explorer <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を使用して証明書を追加します。 KeyStore Explorer を開いて、**「Open an existing KeyStore」**を選択します。

7. `manifest.yml` ファイルで {{site.data.keyword.appid_short_notm}} インスタンスを定義します。

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

    {{site.data.keyword.appid_short_notm}} に合わせて構成した `server.xml` ファイルのサンプルを以下に示します。

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

      
      <applicationManager autoExpand="true"/>

  </server>
  ```
  {: codeblock}



## {{site.data.keyword.Bluemix_notm}} 上で実行されない既存のアプリケーションへの {{site.data.keyword.appid_short_notm}} の追加
{: #existing}

{{site.data.keyword.Bluemix_notm}} 上で実行されない Node.js または Swift のアプリケーションがある場合、リモート側から作業するように WebAppStrategy または WebAppKituraCredentialsPlugin を構成できます。 Bluemix で実行しない Liberty for Java アプリケーションについては、OIDC 要素変数を構成してください。


Node.js アプリでは、`passport.use(new WebAppStrategy());` を以下のコードに置き換えます。

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

Swift アプリでは、`let webappKituraCredentialsPlugin = WebAppKituraCredentialsPlugin()` を以下のコードに置き換えます。

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
  <caption> 表 6. Swift アプリケーションと Node.js アプリケーションで使用するコマンドのコンポーネントの説明 </caption>
    <tr>
      <th> コンポーネント </th>
      <th> 説明 </th>
    </tr>
    <tr>
      <td> <i> tenantID </i> </br> <i> clientID </i> </br> <i> secret </i> </br> <i> oauth-server-url </i> </br> </td>
      <td> これらの値を見つけるには、サービス・ダッシュボードの**「サービス資格情報」**タブで**「資格情報の表示」**をクリックします。 </td>
    </tr>
    <tr>
      <td> <i> app-url </i> </td>
      <td> アプリケーションの URL。 </td>
    </tr>
    <tr>
      <td> <i> CALLBACK_URL </i> </td>
      <td> ログイン後にユーザーに表示されるページの URL。 </td>
    </tr>
  </table>

Liberty for Java アプリケーションで、[既存の Liberty for Java アプリケーションへの {{site.data.keyword.appid_short_notm}} の追加](/docs/services/appid/existing.html#existing-liberty)の手順を実行します。ただし、OIDC クライアント要素変数を以下のコードに置き換えてください。

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
  <caption> 表 7. Bluemix で実行しない Liberty for Java アプリケーションの OIDC 要素変数 </caption>
    <tr>
      <th> コンポーネント </th>
      <th> 説明 </th>
    </tr>
    <tr>
    <td> <i> clientID </i> </br> <i> secret </i> </br> <i> oauth-server-url </i> </br> </td>
    <td> これらの値を見つけるには、サービス・ダッシュボードの**「サービス資格情報」**タブで**「資格情報の表示」**をクリックします。 </td>
    </tr>
    <tr>
      <td> <i> authorizationEndpointURL </i> </td>
      <td> oauthServerURL の最後に `/authorization` を追加します。 </td>
    </tr>
    <tr>
      <td> <i> tokenEndpointUrl </i> </td>
      <td> oauthServerURL の最後に `/token` を追加します。 </td>
    </tr>
    <tr>
      <td> <i> jwkEndpointUrl </i> </td>
      <td> oauthServerURL の最後に `/publickeys` を追加します。 </td>
    </tr>
    <tr>
      <td> <i> issuerIdentifier </i> </td>
      <td> 地域によって変わります。 以下の値のいずれかです。 </br><ul><li> issuerIdentifier="appid-oauth.ng.bluemix.net" </br><li> issuerIdentifier="appid-oauth.eu-gb.bluemix.net" </br><li> issuerIdentifier="appid-oauth.au-syd.bluemix.net" </ul></td>
    </tr>
    <tr>
      <td> <i> tokenEndpointAuthMethod </i> </td>
      <td> "basic" を指定します。 </td>
    </tr>
    <tr>
      <td> <i> signatureAlgorithm </i> </td>
      <td> "RS256" を指定します。 </td>
    </tr>
    <tr>
      <td> <i> authFilterid </i> </td>
      <td> 保護するリソースのリスト。 </td>
    </tr>
    <tr>
      <td> <i> trustAliasName </i> </td>
      <td> トラストストア内の証明書の名前。 </td>
    </tr>
  </table>
