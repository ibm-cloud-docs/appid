---

copyright:
  years: 2017
lastupdated: "2017-11-02"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Liberty for Java リソースの保護
{: #protecting-liberty}

{{site.data.keyword.appid_short_notm}} を使用して、IBM Liberty for Java アプリケーションのエンドポイントを保護できます。Liberty for Java には、Open ID Connect (OIDC) 要求を処理するための組み込み機能があります。

## 開始する前に
{: #begin}

* まだバインドしていない既存の [IBM Liberty for Java アプリケーション](https://console.bluemix.net/catalog/starters/liberty-for-java)が必要です。Liberty for Java アプリケーションの開発の詳細については、[この資料](/docs/runtimes/liberty/index.html)を参照してください。
* [Apache Maven](https://maven.apache.org/download.cgi) がインストールされていることを確認してください。
* OIDC と Liberty for Java の連係動作を確認してください。

## Liberty for Java のリソースの保護
{: #protecting-liberty}

1. UI から Liberty for Java サンプルをダウンロードします。サンプルには、標準の Liberty ファイルを格納した zip ファイルが入っています。

2. 端末を開いて、サンプルを解凍したディレクトリーに移動します。

3. Cloud Foundry コマンド・ラインを使用して {{site.data.keyword.Bluemix_notm}} にログインします。資格情報のプロンプトが表示されたら、入力してください。

  ```
  cf login
  ```
  {: codeblock}

4. アプリケーションをデプロイします。以下のコマンドを実行すると、tenantid に関連した名前で Liberty for Java インスタンスが作成されます。

  ```
  cf push
  ```
  {: codeblock}

5. サービス・インスタンスを新しい Liberty for Java インスタンスにバインドして、アプリケーションを再デプロイします。

6. ブラウザーでアプリケーションを開き、自分の資格情報でログインして、認証アクティビティーを確認します。


## Liberty for Java サンプルの更新
{: #updating-liberty}

サンプル・アプリケーションを更新する場合は、以下の手順を実行してください。

1. jsp と html のサーブレットを作成します。
2. 保護リソースを定義して、許可フィルター `web.xml` と `server.xml` に追加します。
3. WAR ファイルを作成して Liberty for Java にデプロイします。

アプリケーションの更新の詳細については、[既存のアプリケーションへの {{site.data.keyword.appid_short_notm}} の追加](/docs/services/appid/existing.html#existing-liberty)を参照してください。
