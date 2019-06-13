---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-21"

keywords: authentication, authorization, identity, app security, secure, development, idp, troubleshooting, redirected, validation

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

# トラブルシューティング: SAML
{: #troubleshooting-idp}

{{site.data.keyword.appid_full}} で使用する SAML を構成中に問題が生じた場合は、ここに示すトラブルシューティングの方法やヘルプの利用を検討してください。
{: shortdesc}


## 一般的な構成の問題
{: #ts-common-saml}

SAML フレームワークは、複数のプロファイル、フロー、および構成をサポートしています。そのため、ID プロバイダー構成を正しく構成することが重要です。SAML を使用する場合によく起きる問題のいくつかについて、解決に役立つトピックを以下に記載します。
{: shortdesc}


ID プロバイダーの特定のエラー・コードおよびメッセージがこのページに記載されていない場合は、[SAML 仕様](http://docs.oasis-open.org/security/saml/Post2.0/sstc-saml-tech-overview-2.0.html)で詳細な情報を検索できます。必要な情報が見つからない場合は、ID プロバイダー管理者に詳しい情報を問い合わせてください。
{: note}



### `RelayState` パラメーターの欠落
{: #ts-saml-relaystate}

**現象**

`RelayState` パラメーターが認証応答にない。


**現象の理由**

{{site.data.keyword.appid_short_notm}} は、`RelayState` と呼ばれる不透明なパラメーターを認証要求の一部として送信します。このパラメーターが応答に含まれていない場合は、ID プロバイダーがこのパラメーターを正しく返すように構成されていない可能性があります。`RelayState` の形式は次のとおりです。

```
https://idp.example.org/SAML2/SSO/Redirect?SAMLRequest=request&RelayState=token
```
{: screen}

**修正方法**

`RelayState` パラメーターを変更せずに {{site.data.keyword.appid_short_notm}} に返すように、SAML プロバイダーが構成されていることを確認してください。


### NameID フィールドの欠落または誤り
{: #ts-saml-nameid}

**現象**

認証要求を送信すると、`NameID` に関するエラーを受け取る。

**現象の理由**

{{site.data.keyword.appid_short_notm}} は、サービス・プロバイダーとして、サービスおよび ID プロバイダーによるユーザーの識別方法を定義します。{{site.data.keyword.appid_short_notm}} では、ユーザーは `NameID` 認証要求において以下の例に示す `NameID` フィールドで識別されます。

```
<NameIDFormat>urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress</NameIDFormat>
```
{: screen}

**修正方法**

この問題を解決するには、ID プロバイダーの `NameID` の形式が E メール・アドレスに設定されていることを確認してください。ID プロバイダー・レジストリー内のすべてのユーザーが有効な E メール・アドレス形式であることを確認してください。次に、レジストリー内のユーザーに複数の E メールが設定されている場合でも、常に有効な E メールが返されるように、`NameID` フィールドが適切に定義されていることを確認します。



### 応答署名の失敗
{: #ts-saml-response-sign-fail}

**現象**

認証要求を送信すると、以下のエラー・メッセージを受け取る。

```
Could not verify SAML assertion signature. Ensure {{site.data.keyword.appid_short_notm}} is configurated with your SAML provider's signing certificate.
```
{: screen}

**現象の理由**

{{site.data.keyword.appid_short_notm}} は、応答内のすべての SAML アサーションに署名が付いていることを予期します。このサービスが応答内で署名を検出または検証できない場合、エラーが返されます。

**修正方法**

この問題を解決するには、次のようにします。

* ID プロバイダーのメタデータ XML ファイルから署名証明書を抽出したことを確認します。`<KeyDescriptor use="signing">` を指定して鍵を使用していることを確認してください。
* 応答署名アルゴリズムを XXX に設定したことを確認します。 





### 応答の復号の失敗
{: #ts-saml-decrypt-fail}

**現象**

認証要求への応答として、以下のいずれかのエラー・メッセージを受け取る。

エラー・メッセージ 1:

```
Unexpectedly received an encrypted assertion. Please enable response encryption in your {{site.data.keyword.appid_short_notm}} SAML configuration.
```
{: screen}

エラー・メッセージ 2: 

```
Could not decrypt SAML assertion. Ensure your SAML provider is configured with the {{site.data.keyword.appid_short_notm}} encryption 
```
{: screen}


**現象の理由**

ID プロバイダーが暗号化するように構成されている場合は、SAML 認証要求 (AuthnRequest) に署名するように {{site.data.keyword.appid_short_notm}} を構成する必要があります。そして、対応する構成を予期するように ID プロバイダーを構成する必要があります。これらのエラーは、以下のいずれかの理由で受け取る可能性があります。

- ID プロバイダーの SAML 応答が暗号化されていることを予期するように、{{site.data.keyword.appid_short_notm}} が構成されていない。
- {{site.data.keyword.appid_short_notm}} がアサーションを正しく復号できない。


**修正方法**

エラー・メッセージ 1 を受け取った場合は、暗号化された応答を予期するように SAML 構成が設定されていることを確認します。デフォルトでは、{{site.data.keyword.appid_short_notm}} は暗号化された応答を予期しません。暗号化を構成するには、[API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp) を使用して `encryptResponse` パラメーターを **true** に設定してください。

エラー・メッセージ 2 を受け取った場合は、証明書が正しいことを確認してください。署名証明書は、{{site.data.keyword.appid_short_notm}} メタデータ XML ファイルから取得できます。`<KeyDescriptor use="signing">` を指定して鍵を使用していることを確認してください。署名アルゴリズムとして `` を使用するように ID プロバイダーが構成されていることを確認してください。 


### レスポンダー・エラー・コード
{: #ts-saml-responder}

**現象**

認証要求を送信すると、以下の一般エラー・メッセージを受け取る。

```
urn:oasis:names:tc:SAML:2.0:status:Responder
```
{: screen}

**現象の理由**

{{site.data.keyword.appid_short_notm}} が初期認証要求を送信しますが、ID プロバイダーはユーザー認証を実行して応答を返す必要があります。ID プロバイダーがこのエラー・メッセージをスローする理由としては、いくつかの理由が考えられます。

このメッセージは、ID プロバイダーが以下の場合に表示されることがあります。 

* ユーザー名を見つけられない、または、検証できない。
* 認証要求 (`AuthnRequest`) に定義されている `NameID` 形式をサポートしていない。
* 認証コンテキストをサポートしていない。
* 署名された認証要求を必要とする。または、固有の署名アルゴリズムを使用している。

**修正方法**

この問題を解決するには、構成とユーザー名を確認します。正しい認証コンテキストおよび変数が定義されていることを確認してください。特定の方法で要求に署名する必要があるかどうかを確認してください。




### サポートされない認証要求
{: #ts-saml-unsupported-request}

**現象**

サポートされない認証要求に関するメッセージを受け取る。

**現象の理由**

{{site.data.keyword.appid_short_notm}} は、認証要求を生成するときに、認証コンテキストを使用して、認証および SAML アサーションの品質を要求できます。

**修正方法**

この問題を解決するには、認証コンテキストを更新します。デフォルトでは、{{site.data.keyword.appid_short_notm}} は認証クラス `urn: oasis: names: tc: SAML: 2.0: ac: classes: PasswordProtectedTransport` と比較 `exact` を使用します。API を使用して、ユース・ケースに合うようにコンテキスト・パラメーターを更新できます。




### SAML 要求署名の失敗
{: #ts-saml-request-sign-fail}

**現象**

認証要求を検証できないことを示すエラーを受け取る。

**現象の理由**

SAML 認証要求 (`AuthNRequest`) に署名するように {{site.data.keyword.appid_short_notm}} を構成できますが、対応する構成を予期するように ID プロバイダーを構成する必要があります。

**修正方法**

この問題を解決するには、次のようにします。

* [SAML IdP 設定 API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp) を使用して `signRequest` パラメーターを `true` に設定することで、認証要求に署名するように {{site.data.keyword.cloud_notm}} を構成します。認証要求が署名されているかどうかを確認するには、要求 URL を調べます。署名は照会パラメーターとして組み込まれます。例: `https://idp.example.org/SAML2/SSO/Redirect?SAMLRequest=request&SigAlg=value&Signature=value&RelayState=token`

* 正しい証明書を使用して ID プロバイダーが構成されていることを確認します。署名証明書を取得するには、{{site.data.keyword.cloud_notm}} ダッシュボードからダウンロードした {{site.data.keyword.cloud_notm}} メタデータ XML ファイルを確認してください。`<KeyDescriptor use="signing">` を指定して鍵を使用していることを確認してください。

* 署名アルゴリズムとして `` を使用するように ID プロバイダーが構成されていることを確認します。



## 接続のデバッグ
{: #ts-saml-debug-connection}

構成は正しいのに、まだバグがありますか? 以下の有用なヒントをいくつか確認して、SAML 接続をデバッグしてください。
{: shortdesc}


### SAML 認証の要求と応答をキャプチャーするには、どのようにすればよいですか?
{: #ts-saml-capture}

SAML 要求および応答をキャプチャーするために使用できる [Firefox](https://addons.mozilla.org/en-US/firefox/addon/saml-tracer/) や [Chrome](https://chrome.google.com/webstore/detail/saml-tracer/mpdajninpobndbfcldcmbpnnbhibjmch?hl=en) などのブラウザーのプラグインのオプションがいくつかあります。プラグインは使用したくありませんか? 問題ありません。 Atlassian に、[手動で抽出する方式](https://confluence.atlassian.com/jirakb/how-to-view-a-saml-responses-in-your-browser-for-troubleshooting-872129244.html)が説明されています。


### メッセージを理解できません。どうすれば解読できますか?
{: #ts-saml-decode-messages}

SAML デバッグ・ツールを使用しても問題が解決しない場合は、[SAML 開発者ツール](https://www.samltool.com/online_tools.php)を使用して、メッセージを解読してください。注意: SAML メッセージをインターセプトした場所によっては、[URL でエンコードされた](https://www.samltool.com/online_tools.php)要求、[base 64 でエンコードされ、圧縮された](https://www.samltool.com/decode.php)要求、または[暗号化された](https://www.samltool.com/decrypt.php)要求が取得されることがあります。

SAML 応答などの SAML メッセージをオンライン・ツールで復号しないでください。情報を復号するためには、ツールに暗号化の秘密鍵を提供する必要があります。鍵は機密を維持し、アクセスを制御する必要があります。このセクションで紹介した復号ツールは、デバッグ目的でのみ使用してください。
{: important}

