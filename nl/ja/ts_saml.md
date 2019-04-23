---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-10"

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

# ID プロバイダーの構成
{: #troubleshooting-idp}

{{site.data.keyword.appid_full}} と連携して使用する ID プロバイダーを構成中に問題が生じた場合は、ここに示すトラブルシューティング手法やヘルプの利用手法を検討してください。
{: shortdesc}


## ユーザーが ID プロバイダーにリダイレクトされない
{: #ts-saml-redirect}

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


## SAML の一般的な問題
{: #ts-common-saml}

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
      <td><code>SAML response body must contain the RelayState parameter.</code></td>
      <td>パラメーターが SAML 応答本文に含まれていませんでした。 {{site.data.keyword.appid_short_notm}} はこのパラメーターを要求の一部として ID プロバイダーに提供するため、正確なパラメーターが応答で返される必要があります。 このパラメーターが変更されている場合は、ID プロバイダー管理者に問い合わせてください。 </td>
    </tr>
    <tr>
      <td><code>SAML Configuration must have certificates, entityID and signInUrl of the IdP.</code></td>
      <td>SAML ID プロバイダーが<a href="/docs/services/appid?topic=appid-enterprise#enterprise" target="_blank">正しく構成</a>されていません。 構成を検証してください。</td>
    </tr>
    <tr>
      <td><code>Error in assertion validation. SAML Assertion signature check failed! Certificate .. may be invalid.</code></td>
      <td>有効な署名とダイジェストがアサーションに含まれている必要があります。 この署名は、SAML 構成で指定された証明書に関連付けられた秘密鍵を使用して作成する必要があります (2 次または 1 次のいずれかを使用できます)。 <strong>注</strong>: {{site.data.keyword.appid_short_notm}} では暗号化されたアサーションはサポートされません。 ID プロバイダーが SAML アサーションを暗号化する場合は、暗号化を無効にします。</td>
    </tr>
  </tbody>
</table>



## SAML 応答検証エラー
{: #ts-saml-response}

{{site.data.keyword.appid_short_notm}} では、アサーションのために以下の妥当性要件があります。 特に指定がない限り、すべての属性は必須の SAML 応答 XML ノードです。
{: shortdesc}


<table summary="表の行はすべて左から右に読みます。1 列目は応答エレメント、2 列目は説明です。">
  <thead>
    <th>応答エレメント</th>
    <th>説明</th>
  </thead>
  <tbody>
    <tr>
      <td><code>samlp:Response</code></td>
      <td>応答 XML には応答エレメントが含まれている必要があります。</td>
    </tr>
    <tr>
      <td><code>SAML version</code></td>
      <td>{{site.data.keyword.appid_short_notm}} は <code>SAML version 2.0</code> のみを受け入れます。</td>
    </tr>
    <tr>
      <td><code>InResponseTo</code></td>
      <td>{{site.data.keyword.appid_short_notm}} は、アサーションで返される応答エレメント <code>InResponseTo</code> が SAML 要求からの保存済み要求 ID と一致することを検証します。</td>
    </tr>
    <tr>
      <td><code>saml:issuer</code></td>
      <td>アサーションで指定されている発行者は、{{site.data.keyword.appid_short_notm}} ID プロバイダー構成で指定されている発行者と一致する必要があります。</td>
    </tr>
    <tr>
      <td><code>ds:Signature</code></td>
      <td>有効な署名とダイジェストがアサーションに含まれている必要があります。 この署名は、SAML 構成で指定された証明書に関連付けられている秘密鍵を使用して作成する必要があります。 ダイジェストは、指定された <code>CanonicalizationMethod</code> および <code>Transforms</code> を使用して検証されます。 <strong>注</strong>: {{site.data.keyword.appid_short_notm}} は証明書の有効期限を検証しません。 証明書の管理に役立つように、[証明書マネージャー](/docs/services/certificate-manager?topic=certificate-manager-getting-started#getting-started)を試してみてください。</td>
    </tr>
    <tr>
      <td><code>saml:subject</code></td>
      <td>アサーションのサブジェクトまたは <code>name_id</code> は、ユーザーの統合 E メールでなければなりません。</td>
    </tr>
    <tr>
      <td><code>saml:AttributeStatement</code></td>
      <td>特定の属性が特定の認証済みユーザーに関連付けられていることを表明します。</td>
    </tr>
    <tr>
      <td><code>saml:Conditions</code></td>
      <td><strong>オプション</strong>: アサーションに条件文が含まれる場合、有効なタイム・スタンプも含まれている必要があります。 {{site.data.keyword.appid_short_notm}} は、アサーションで指定された有効期間を受け入れます。 検証するために、このサービスは <code>NotBefore</code> 制約および <code>NotOnOrAfter</code> 制約を検索します。これらは定義されていて、有効になっている必要があります。</td>
    </tr>
  </tbody>
</table>

{{site.data.keyword.appid_short_notm}} では、暗号化されたアサーションはサポートしません。 ID プロバイダーでアサーションを暗号化するように設定されている場合は、それを無効にします。 アサーションは暗号化されていない形式でなければなりません。
{: tip}
