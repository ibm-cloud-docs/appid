---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-14"

keywords: authentication, authorization, identity, app security, secure, troubleshooting, help, support, requests, uri

subcollection: appid

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}

# 一般的なトラブルシューティング
{: #troubleshooting}

{{site.data.keyword.appid_full}} の操作中に問題が生じた場合は、ここに示すトラブルシューティング手法やヘルプの利用手法を検討してください。
{: shortdesc}

## ヘルプとサポートの入手
{: #ts-gettinghelp}

情報を検索したり、フォーラムで質問したりして、ヘルプを利用することができます。 また、サポート・チケットを開くことができます。 フォーラムを使用して質問するときは、{{site.data.keyword.cloud_notm}} 開発チームの目に止まるように、質問にタグを付けてください。
  * {{site.data.keyword.appid_short_notm}} についての技術的な質問がある場合は、質問を<a href="https://stackoverflow.com/search?q=ibm-appid" target="_blank">スタック・オーバーフロー <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a>に投稿し、質問に「ibm-appid」のタグを付けてください。
  * サービスや開始手順についての質問は、<a href="https://developer.ibm.com/answers/topics/appid/" target="_blank">dW Answers <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> フォーラムをご利用ください。 `appid` のタグを付けてください。

サポートについて詳しくは、[必要なサポートを利用するには](/docs/get-support?topic=get-support-getting-customer-support#getting-customer-support)を参照してください。



## サインイン後にユーザーがアプリにリダイレクトされない
{: #ts-signin-fail}

{: tsSymptoms}
ユーザーが ID プロバイダーのサインイン・ページ経由でアプリケーションにサインインすると、何も起こらないかサインインが失敗します。

{: tsCauses}
以下の理由でサインインに失敗している可能性があります。

* リダイレクト URL が[ホワイトリスト](/docs/services/appid?topic=appid-faq#faq-redirect)に正しく追加されていない。
* ユーザーが許可されていない。
* ユーザーが誤った資格情報でサインインしようとした。

{: tsResolve}
リダイレクトが行われるようにするには、以下のようにします。

* リダイレクト URL が正しいことを確認してください。 これが正確でないとリダイレクトが機能しません。
* ユーザーが正しい資格情報でサインインしているか確認してください。
* ID プロバイダーのユーザー設定で各ユーザーが構成されているか確認してください。



## カスタム URI が拒否される
{: #ts-custom-uri}

{: tsSymptoms}
カスタム URL スキームを使用する Web リダイレクト URL を入力すると、それが {{site.data.keyword.appid_short_notm}} コンソールによって拒否されます。

{: tsCauses}
以下の理由で URL が拒否される可能性があります。

* URL が `http` または `https` のスキームに従っていない
* URL の末尾が `://` となっている
* URL にタイプミスがある

この制限事項はセキュリティーのために課されています。

{: tsResolve}
この問題を解決するには、URL が正しいことを確認します。 URL が要件を満たしていない場合は、アプリに HTTPS エンドポイントを作成して、受信した付与コードをカスタム URL にリダイレクトできます。 作成したエンドポイントを、{{site.data.keyword.appid_short_notm}} コンソールでリダイレクト URL として指定します。 リダイレクト URI について詳しくは、[リダイレクト URI の追加](/docs/services/appid?topic=appid-managing-idp#add-redirect-uri)を参照してください。



## 属性に誤った値が表示される
{: #ts-saml-attribute}

{: tsSymptoms}
ユーザー・プロファイルに属性値がありますが、正しい属性に関連付けられていません。

{: tsCauses}
ユーザー・プロファイル属性が正しくマップされていません。

{: tsResolve}
ID プロバイダー設定で属性をマップします。 {{site.data.keyword.appid_short_notm}} は以下の属性を必要としています。
* `name`
* `email`
* `locale`
* `picture`



## エラー: 要求が多すぎます
{: #ts-requests}

{: tsSymptoms}
アプリのホーム・ページを表示しようとしたら、次のようなエラー・メッセージを受け取ります。

```
{"error_code":"too many requests","error_description":"too many requests"}
```
{: screen}

{: tsCauses}
「要求が多すぎます」エラーは、仮想ユーザー 1 人だけで自動テストを実行した場合に受け取ることがあります。各ユーザーが許可されるサインインの試行回数は 1 分間に 5 回に限られています。サインインの試行回数が限定されているのは、ブルート・フォース DDOS 攻撃 (総当たり攻撃) やその他の似たようなタイプの攻撃を防止するためです。

{: tsResolve}
この問題を解決するには、テストを行うときに複数の仮想ユーザーを使用するようにしてください。
</br>
