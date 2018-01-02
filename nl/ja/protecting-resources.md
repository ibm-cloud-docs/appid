---

copyright:
  years: 2017
lastupdated: "2017-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


# バックエンド・リソースの保護

{{site.data.keyword.appid_short_notm}} Server SDK を使用して、アプリ内のエンドポイントを保護したりアクセスしたりすることができます。Client SDK を使用して保護リソースにアクセスすることもできます。

**注**: 必要な場合は、保護リソースの呼び出しによってログイン・ウィジェットが開始します。有効なトークンが既に取得されている場合、ログイン・ウィジェットは開始されず、リソースに直接アクセスします。

## Liberty for Java のリソースの保護
{: #protecting-liberty}

{{site.data.keyword.appid_short_notm}} を使用して、IBM Liberty for Java アプリケーションのエンドポイントを保護できます。 Liberty for Java には、Open ID Connect (OIDC) 要求を処理するための組み込み機能があります。

開始前に、以下のことを行います。
* まだバインドしていない既存の [IBM Liberty for Java アプリ](https://console.bluemix.net/catalog/starters/liberty-for-java)が必要です。Liberty for Java アプリケーションの開発の詳細については、[この資料](/docs/runtimes/liberty/index.html)を参照してください。
* [Apache Maven](https://maven.apache.org/download.cgi) がインストールされていることを確認してください。
* OIDC と Liberty for Java の連係動作を確認してください。

リソースを保護するには、以下のようにします。

1. UI から Liberty for Java サンプルをダウンロードします。 サンプルには、標準の Liberty ファイルを格納した zip ファイルが入っています。
2. 端末を開いて、サンプルを解凍したディレクトリーに移動します。
3. Cloud Foundry コマンド・ラインを使用して {{site.data.keyword.Bluemix_notm}} にログインします。 資格情報のプロンプトが表示されたら、入力してください。

  ```
  cf login
  ```
  {: codeblock}

4. アプリをデプロイします。以下のコマンドを実行すると、tenantid に関連した名前で Liberty for Java インスタンスが作成されます。

  ```
  cf push
  ```
  {: codeblock}

5. サービス・インスタンスを新しい Liberty for Java インスタンスにバインドして、アプリを再デプロイします。
6. ブラウザーでアプリを開き、自分の資格情報でログインして、認証アクティビティーを確認します。

## Node.js のリソースの保護
{: #protecting-resources-nodesdk}

{{site.data.keyword.appid_short_notm}} Server SDK には、{{site.data.keyword.Bluemix_notm}} にデプロイされたバックエンド・アプリで使用する ApiStrategy パスポート戦略が用意されています。ご使用のアプリを無許可アクセスから保護するには、Node.js サーバーに ApiStrategy を装備する必要があります。 `appid-serversdk-nodejs npm モジュール`には、ApiStrategy パスポート戦略の他に、{{site.data.keyword.appid_short_notm}} から発行されたアクセス・トークンと ID トークンを検証するための検証メソッドも用意されています。

{{site.data.keyword.appid_short_notm}} Server SDK は、<a href="http://passportjs.org/" target="_blank">Passport フレームワーク <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を使用して許可を実施します。

以下のスニペットは、`APIStrategy` を単純な Express アプリで使用して、`/protected` エンドポイント GET メソッドを保護する方法を示しています。

  ```JavaScript

  var express = require('express');
  var passport = require('passport');
  var APIStrategy = require('bluemix-appid').APIStrategy;

  passport.use(new APIStrategy());
  var app = express();
  app.use(passport.initialize());

  app.get('/protected', passport.authenticate('APIStrategy.STRATEGY_NAME', {session: false }),
      function(request, response){
          console.log("Securty context", request.securityContext)    
          response.send(200, "Success!");
      }
  );

  app.listen(process.env.PORT);
  ```
  {: codeblock}


## iOS Swift SDK を使用した保護リソースへのアクセス
{: #requesting-swift}

1. BMSCore をインポートします。

  ```swift
  import BMSCore
  ```
  {: codeblock}

2. 保護リソース要求を呼び出します。

  ```swift
  BMSClient.sharedInstance.initialize(bluemixRegion: AppID.<region>)
  BMSClient.sharedInstance.authorizationManager = AppIDAuthorizationManager(appid:AppID.sharedInstance)
  var request:Request =  Request(url: "<your protected resource url>")
  request.send(completionHandler: {(response:Response?, error:Error?) in
      //応答処理コードをここに記述
  })
  ```
  {: codeblock}


## Android SDK を使用した保護リソースへのアクセス
{: #requesting-android}

1. 保護リソース要求を呼び出します。

  ```java
  BMSClient bmsClient = BMSClient.getInstance();
  bmsClient.initialize(getApplicationContext(), AppID.REGION_UK);

  AppIDAuthorizationManager appIdAuthMgr = new AppIDAuthorizationManager(AppID.getInstance())
  bmsClient.setAuthorizationManager(appIdAuthMgr);

  Request request = new Request("<your protected resource url>", Request.GET);
  request.send(this, new ResponseListener() {
  @Override
		public void onSuccess (Response response) {
     //応答処理コードをここに記述
  }
  @Override
		public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
      //エラー処理コードをここに記述
  });
  ```
  {: codeblock}
