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

# SDK の構成
{: #configuring}


## Android SDK のセットアップ
{: #android-setup}

{{site.data.keyword.appid_short}} Client SDK を使用して Android アプリを構築し、SDK を初期化し、ユーザーを認証し、保護リソースや無保護リソースへの要求を実行します。
{:shortdesc}


### 開始する前に

以下の情報が必要です。
  * {{site.data.keyword.appid_short_notm}} サービスのインスタンス。
  * テナント ID。 サービスのダッシュボードの**「サービス資格情報」**タブの**「資格情報の表示」**をクリックします。 テナント ID は、アプリの初期化に使用される固有 ID です。
  * {{site.data.keyword.Bluemix}} 地域。 地域は UI に表示されています。 その値をアプリの初期化に使用します。
    <table> <caption> 表 1. {{site.data.keyword.Bluemix_notm}} 地域と対応する SDK 値 </caption>
    <tr>
      <th>{{site.data.keyword.Bluemix}} 地域</th>
      <th>SDK 値 </th>
    </tr>
    <tr>
      <td>米国南部 </td>
      <td><code>AppID.REGION_US_SOUTH</code> </td>
    </tr>
    <tr>
      <td>シドニー </td>
      <td><code>AppID.REGION_SYDNEY</code></td>
    </tr>
    <tr>
      <td>英国 </td>
      <td><code>AppID.REGION_UK</code></td>
    </tr>
    <tr>
      <td>ドイツ</td>
      <td><code>AppID.REGION_GERMANY</code></td>
    </tr>
  </table>

  * Gradle と連動して機能するようにセットアップされた <a href="https://developers.google.com/web/tools/setup/" target="_blank">Android Studio プロジェクト<img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a>。

### Client SDK のインストール

1. Android Studio プロジェクトを作成するか、既存のプロジェクトを開きます。
2. JitPack リポジトリーをルートの `build.gradle` ファイルに追加します。

  ```gradle
    allprojects {
	    repositories {
		    ...
		    maven { url 'https://jitpack.io' }
	    }
    }
  ```
  {: codeblock}

3. アプリケーションの `build.gradle` ファイルを開きます。

    **注**: プロジェクトの `build.gradle` ファイルではなくアプリのファイルを開いてください。
4. ファイルの従属関係セクションを見つけて、{{site.data.keyword.appid_short_notm}} Client SDK 用のコンパイル従属関係を追加します。

  ```gradle
   dependencies {
       compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:1.+'
   }
  ```
  {: codeblock}

5. `defaultConfig` セクションを見つけて、以下のコード行を追加します。

  ```gradle
  defaultConfig {
  ...
  manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
  ```
  {: codeblock}

6. プロジェクトを Gradle と同期化します。 **「ツール」>「Android」>「プロジェクトを Gradle ファイルと同期 (Sync Project with Gradle Files)」**とクリックします。

### Client SDK の初期化

context、tenant ID、region パラメーターを initialize メソッドに渡して、Client SDK を初期化します。 初期化コードの配置場所として一般的な (必須ではありません) 場所は、Android アプリケーションのメイン・アクティビティーの onCreate メソッド内です。

  ```java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, AppID.REGION_UK);
  ```
  {: codeblock}

1. *tenantId* をサービスの tenantId に置き換えます。
2. *AppID.REGION_UK* を、該当する {{site.data.keyword.Bluemix_notm}} 地域に置き換えます。

詳細については、<a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">{{site.data.keyword.appid_short_notm}} Android GitHub リポジトリー <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を参照してください。

## iOS Swift SDK のセットアップ
{: #ios-setup}

{{site.data.keyword.appid_short}} Client SDK を使用して Swift アプリケーションを構築し、SDK を初期化し、ユーザーを認証し、保護リソースや無保護リソースへの要求を実行します。
{:shortdesc}


### 開始する前に

以下の情報が必要です。
  * {{site.data.keyword.appid_short_notm}} のインスタンス。
  * テナント ID。 サービスのダッシュボードの**「サービス資格情報」**タブの**「資格情報の表示」**をクリックします。 テナント ID は、アプリの初期化に使用される固有 ID です。
  * {{site.data.keyword.Bluemix_notm}} 地域。
  地域は UI に表示されています。 その値をアプリの初期化に使用します。
  <table> <caption> 表 1. {{site.data.keyword.Bluemix_notm}} 地域と対応する SDK 値 </caption>
    <tr>
      <th>{{site.data.keyword.Bluemix}} 地域</th>
      <th>SDK 値 </th>
    </tr>
    <tr>
      <td>米国南部 </td>
      <td><code>AppID.REGION_US_SOUTH</code> </td>
    </tr>
    <tr>
      <td>シドニー </td>
      <td><code>AppID.REGION_SYDNEY</code></td>
    </tr>
    <tr>
      <td>英国 </td>
      <td><code>AppID.REGION_UK</code></td>
    </tr>
    <tr>
      <td>ドイツ</td>
      <td><code>AppID.REGION_GERMANY</code></td>
    </tr>
  </table>

  * Xcode プロジェクト (バージョン 9.0.1 以上)。
  * CocoaPods (バージョン 1.1.0 以上)。


### Client SDK のインストール

{{site.data.keyword.appid_short_notm}} Client SDK には、Swift プロジェクトと Objective-C Cocoa プロジェクト用の従属関係マネージャーである CocoaPods が付属しています。 CocoaPods は成果物をダウンロードし、プロジェクトで使用できるようにします。

1. Xcode プロジェクトを作成するか、既存のプロジェクトを開きます。
2. プロジェクトのディレクトリー内の podfile を開くか、このディレクトリー内に podfile を作成します。
3. プロジェクトのターゲットに続いて、「BluemixAppID」ポッドおよび `use_frameworks!` コマンドの従属関係を追加します。

  以下に例を示します。

  ```swift
  target '<yourTarget>' do
     use_frameworks!
     pod 'BluemixAppID'
  end
  ```
  {: codeblock}

4. `BluemixAppID` の従属関係をダウンロードするには、以下のコマンドを実行します。

  ```swift
  pod install --repo-update
  ```
  {: codeblock}

6. Xcode プロジェクトを開き、キーチェーン共有を使用可能にします。 **「Project Settings」>「Capabilities」>「Keychain Sharing」**に移動し、**「Enable keychain sharing」**を選択します。
7. **「Project Settings」>「Info」>「URL Types」**を開き、**「URL Type」**を追加します。**「Identifier」**と**「URL Scheme」**の両方のテキスト・ボックスに `$(PRODUCT_BUNDLE_IDENTIFIER)` を入力します。


### Client SDK の初期化

1. `AppDelegate` ファイルに以下のインポートを追加します。

  ```swift
  import BluemixAppID
  ```
  {: codeblock}

2. tenant ID パラメーターと region パラメーターを initialize メソッドに渡すことによって、Client SDK を初期化します。 初期化コードの配置場所として一般的な (必須ではありません) 場所は、Swift アプリケーションの AppDelegate の `application:didFinishLaunchingWithOptions` メソッド内です。

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, bluemixRegion: AppID.Region_UK)
  ```
  {: codeblock}

  * *tenantId* をサービスのテナント ID に置き換えます。
  * AppID.REGION_UK を、該当する {{site.data.keyword.appid_short_notm}} 地域に置き換えます。

3. 以下のコードを AppDelegate ファイルに追加します。

  ```swift
  func application(_ application: UIApplication, open url: URL, options :[UIApplicationOpenURLOptionsKey : Any]) -> Bool {
          return AppID.sharedInstance.application(application, open: url, options: options)
      }
  ```
  {: codeblock}

詳細については、<a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">{{site.data.keyword.appid_short_notm}} iOS GitHub リポジトリー <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を参照してください。

## Node.js SDK のセットアップ
{: #nodejs-setup}

### 開始する前に

* {{site.data.keyword.Bluemix_notm}} での Node.js アプリの開発に精通している必要があります。
* {{site.data.keyword.appid_short_notm}} Server SDK には、Node.js サーバーが <a href="http://expressjs.com/" target="_blank">Express フレームワーク<img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a>を使用して実装されていることが必要です。

**注**: その他のフレームワークは `Express` フレームワーク (LoopBack など) を使用します。 {{site.data.keyword.appid_short_notm}} Server SDK は、それらのどのフレームワークでも使用できます。


### Server SDK のインストール


1. コマンド・ラインを使用して、Node.js アプリのディレクトリーを開いてください。
2. 以下のコマンドを実行します。

  ```
  npm install -save express
  npm install -save passport
  npm install -save bluemix-appid
  ```
  {: codeblock}

詳細については、<a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">{{site.data.keyword.appid_short_notm}}Node.js GitHub リポジトリー <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を参照してください。

## Swift SDK のセットアップ
{: #swift-setup}

{{site.data.keyword.appid_short}} サーバー SDK を使用して、バックエンドと API を保護します。
{:shortdesc}


### 開始する前に

Swift SDK の作業を行う前に、以下の前提条件を満たす必要があります。

* MacOS または Linux のいずれか
* Linux では OpenSSL 1.0.2
* Swift 3.0.2 をインストールします
* Kitura 1.6 をインストールします


### SDK のインストール

1. Swift アプリのディレクトリーにある `Package.swift` ファイルを開き、`appid-serversdk-swift` 従属関係を追加します。 以下に例を示します。

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

2. MacOS の場合: コマンド・ラインでビルドする場合、すべてのパッケージに次のフラグが含まれている必要があります。
  ```
  swift build -Xlinker -L/usr/local/opt/openssl/lib -Xcc -I/usr/local/opt/openssl/include
  ```
  {: pre}

3. Xcode プロジェクトを作成する場合は、次のコマンドを使用します。
  ```
  swift package generate-xcodeproj --xcconfig-overrides openssl.xcconfig
  ```
  {: pre}

  openssl.xcconfig は <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">{{site.data.keyword.appid_short_notm}} Swift GitHub <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> からコピーできます。
  {: tip}
