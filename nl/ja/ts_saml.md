---

copyright:
  years: 2017, 2018
lastupdated: "2018-06-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tip: .tip}

# ID プロバイダーの構成
{: #troubleshooting-idp}

{{site.data.keyword.appid_full}} を使用して ID プロバイダーを構成中に問題が生じた場合は、ここに示すトラブルシューティング手法やヘルプの利用手法を検討してください。
{: shortdesc}


## サインイン後にアプリにリダイレクトされない
{: #signin-fail}

{: tsSymptoms}
ユーザーが ID プロバイダーのサインイン・ページ経由でアプリケーションにサインインすると、何も起こらないかサインインが失敗します。

{: tsCauses}
以下の理由でサインインに失敗している可能性があります。

* リダイレクト URL が[ホワイトリスト](identity-providers.html#redirect)に正しく追加されていない。
* ユーザーが許可されていない。
* ユーザーが誤った資格情報でサインインしようとした。

{: tsResolve}
リダイレクトが行われるようにするには、以下のようにします。

* リダイレクト URL が正しいことを確認してください。 これが正確でないとリダイレクトが機能しません。
* ユーザーが正しい資格情報でサインインしているか確認してください。
* ID プロバイダーのユーザー設定で各ユーザーが構成されているか確認してください。


## SAML の操作時によく発生する問題
{: #common-saml}

以下の表で、SAML の操作時によく発生する問題の説明と解決法を確認してください。

<table summary="表の行はすべて左から右に読みます。1 列目はクラスターの状態、2 列目は説明です。">
  <thead>
    <th>メッセージ</th>
    <th>説明</th>
  </thead>
  <tbody>
    <tr>
      <td><code>Could not parse assertion xml.</code></td>
      <td>SAML からの応答の形式が誤っていました。</td>
    </tr>
    <tr>
      <td><code>Invalid attribute without name. Contact your identity provider administrator.</code></td>
      <td>定義された値を持たない <code>&lt;saml:Attribute&gt;</code> があります。 ID プロバイダー管理者に問い合わせてください。</td>
    </tr>
    <tr>
      <td><code>SAML response body must contain RelayState.</code></td>
      <td>RelayState パラメーターが SAML 応答本文に含まれていませんでした。 {{site.data.keyword.appid_short_notm}} はこのパラメーターを要求の一部として ID プロバイダーに提供するため、正確なパラメーターが応答で返される必要があります。 このパラメーターが変更されている場合は、ID プロバイダー管理者に問い合わせてください。 </td>
    </tr>
    <tr>
      <td><code>SAML Configuration must have certificates, entityID and signInUrl of the IdP.</code></td>
      <td>SAML ID プロバイダーが正しく構成されていません。 構成を検証してください。 詳しくは、<a href="enterprise.html#configuring-saml" target="_blank">外部 SAML ID プロバイダーと連動するようにアプリを構成する</a>を参照してください。</td>
    </tr>
    <tr>
      <td><code>Error in assertion validation. SAML Assertion signature check failed! Certificate .. may be invalid.</code></td>
      <td>有効な署名とダイジェストがアサーションに含まれている必要があります。 この署名は、SAML 構成で指定された証明書に関連付けられた秘密鍵を使用して作成する必要があります (2 次または 1 次のいずれかを使用できます)。 <strong>注</strong>: {{site.data.keyword.appid_short_notm}} では暗号化されたアサーションはサポートされません。 ご使用の ID プロバイダーが SAML アサーションを暗号化する場合は、暗号化を無効にしてください。</td>
    </tr>
  </tbody>
</table>


## ID プロバイダーにリダイレクトされない
{: #saml-redirect}

{: tsSymptoms}
ユーザーがアプリケーションにサインインしようとして要求を出しても、サインイン・ページが表示されません。

{: tsCauses}
ID プロバイダーが以下のような理由で失敗している可能性があります。

* 構成済みのリダイレクト URL が正しくない。
* ID プロバイダーが認証要求を認識しない。
* ID プロバイダーが HTTP-POST バインディングを必要としている。
* ID プロバイダーが署名済み authnRequest を必要としている。

{: tsResolve}
以下のような解決法を試行できます。

* サインイン URL を更新します。 この URL は authnRequest の一部として送信されるため、正確でなければなりません。
* {{site.data.keyword.appid_short_notm}} メタデータが ID プロバイダー設定で正しく設定されていることを確認します。
* HTTP リダイレクトで authnRequest を受け入れるように ID プロバイダーを構成します。
* {{site.data.keyword.appid_short_notm}} では、authnRequest の署名はサポートされていません。

これらの方法で解決できない場合は、接続の問題がある可能性があります。
{: tip}

## 属性に誤った値が表示される
{: #saml-attribute}

{: tsSymptoms}
ユーザー・プロファイルに属性値がありますが、正しい属性に接続されていません。

{: tsCauses}
ユーザー・プロファイル属性が正しくマップされていません。

{: tsResolve}
ID プロバイダー設定で属性をマップします。 {{site.data.keyword.appid_short_notm}} は以下の属性を必要としています。
* `name`
* `email`
* `locale`
* `picture`


