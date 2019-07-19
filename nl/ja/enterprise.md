---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-20"

keywords: authentication, authorization, identity, app security, secure, custom, service provider, identity provider, enterprise, assertions

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

# SAML
{: #enterprise}

SAML ベースの ID プロバイダーがある場合、サード・パーティー・プロバイダーへのシングル・サインオン (SSO) ログインを開始するサービス・プロバイダーとして機能するように {{site.data.keyword.appid_short_notm}} を構成できます。 サインイン・フローの中で、ユーザーは簡単に認証を受け、アプリや保護 API にアクセスするための {{site.data.keyword.appid_short_notm}} セキュリティー・トークンを取得できます。
{: shortdesc}

 
特定の SAML ID プロバイダーと連携しますか? [Ping One ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/cloud/blog/setting-ibm-cloud-app-id-ping-one)、[Azure Active Directory ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/cloud/blog/setting-ibm-cloud-app-id-azure-active-directory)、または [Active Directory Federation Service ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/cloud/blog/setting-ibm-cloud-app-id-active-directory-federation-service) と連携する {{site.data.keyword.appid_short_notm}} のセットアップ方法についてのブログ投稿を参照してください。
{: tip}


## SAML についての説明
{: #saml-understanding}

Security Assertion Markup Language (SAML) は、ユーザーの身分を表明する ID プロバイダーとユーザー ID 情報を取り込むサービス・プロバイダーの間で、認証データと許可データを交換するためのオープン・スタンダードです。
{: shortdesc}

<a href="http://saml.xml.org/saml-specifications" target="blank">SAML <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> プロトコルは、さまざまなプロファイルやバインド・オプションをサポートします。 {{site.data.keyword.appid_short_notm}} は、HTTP Post バインディングを使用して Web ブラウザー SSO プロファイルをサポートします。

### フローの技術基盤
{: #saml-tech-basis}

SAML 2.0 は、認証と許可の標準として最も確立されたフレームワークの 1 つです。 これは、サービス・プロバイダー ({{site.data.keyword.appid_short_notm}}) と ID プロバイダーの間の XML ベースのプロトコルです。 ID プロバイダーは、ユーザーを認証すると、そのユーザーに関するアサーションまたはステートメントを含む SAML トークンを作成します。 一般にはステートメントには以下が含まれます。

- ユーザーの認証に使用した方法などの認証情報 - パスワードや MFA など。
- ユーザーに関連付けられた属性 - ユーザーが属するグループ。
- 特定のリソースに対する特定のアクションの実行をユーザーに許可するかどうかを示す許可決定。

アサーションが {{site.data.keyword.appid_short_notm}} に返されると、サービスはユーザー ID を統合し、適切なトークンが生成されます。 以下のいずれかの OIDC クレームに SAML アサーションが対応している場合、その SAML アサーションは自動的に識別トークンに追加されます。  これらの値の 1 つ以上がプロバイダー側で変更された場合、新しい値は、ユーザーが再びログインした後でないと使用できるようになりません。

 * `name`
 * `email`
 * `locale`
 * `picture`

どの標準名にも対応しないアサーションはデフォルトで無視されますが、SAML プロバイダーが他のアサーションを返す場合には、ユーザーがログインすると情報を取得することが可能となります。 使用するアサーションの配列を作成することによって、[トークンに情報を注入する](/docs/services/appid?topic=appid-customizing-tokens#customizing-tokens)ことができます。 ただし、必要以上に情報をトークンに追加しないようにしてください。 トークンは通常、http ヘッダー内で送信されますが、ヘッダーのサイズは制限されています。
{: tip}

### フローの概要
{: #saml-flow}

{{site.data.keyword.appid_short_notm}} と ID プロバイダーは SAML フレームワークを使用してユーザーを認証しますが、{{site.data.keyword.appid_short_notm}} は、より新しい OAuth 2.0/OIDC フレームワークを使用してアプリケーションとセキュリティー・トークンを交換します。 次の図を参照して、情報の詳しいフローを確認してください。

![SAML エンタープライズ認証フロー](/images/ibmid-flow.png)

1. ユーザーが、アプリケーション上のログイン・ページまたは制限付きリソースにアクセスします。これにより、{{site.data.keyword.appid_short_notm}} SDK または API を介して `{{site.data.keyword.appid_short_notm}}/authorization` エンドポイントへの要求が開始されます。 ユーザーが許可されていない場合、認証フローは {{site.data.keyword.appid_short_notm}} へのリダイレクトから始まります。
2. {{site.data.keyword.appid_short_notm}} が SAML 認証要求 (AuthNRequest) を生成し、ブラウザーはユーザーを SAML ID プロバイダーに自動的にリダイレクトします。
3. ID プロバイダーが SAML 要求を解析し、ユーザーを認証し、そのユーザーのアサーションを含む SAML 応答を生成します。
4. ID プロバイダーが、SAML 応答と一緒にユーザーと応答を {{site.data.keyword.appid_short_notm}} にリダイレクトします。
5. 認証が成功した場合、{{site.data.keyword.appid_short_notm}} は、ユーザーの許可と認証を表すアクセス・トークンと識別トークンを作成し、それらをアプリに返します。 認証が失敗した場合、{{site.data.keyword.appid_short_notm}} は ID プロバイダーのエラー・コードをアプリに返します。
6. アプリまたは保護リソースへのアクセスがユーザーに許可されます。



### SSO を使用するとフローが変わるか?
{: #saml-sso-flow}

{{site.data.keyword.appid_short_notm}} が実装している Web ブラウザー SSO プロファイルは、サービス・プロバイダーから開始されます。つまり、認証セッションを開始するためには {{site.data.keyword.appid_short_notm}} が SAML 要求を ID プロバイダーに送信する必要があります。 

現在、{{site.data.keyword.appid_short_notm}} は ID プロバイダーから開始されるフローをサポートしていないので、現時点ではこのようなフローをこのサービスで使用してはいけません。
{: note}

ID プロバイダーが SSO をサポートしている場合は、既に確立された SSO セッションを SAML 認証で使用してユーザーを認証することが可能です。 サポートしていない場合は、ユーザーはログイン・ページにリダイレクトされます。 {{site.data.keyword.cloud_notm}} の認証要求に定義されている認証要件と、SSO を確立するために ID プロバイダーが使用するものを、ID プロバイダーが対応付けられない場合、ユーザーはリダイレクトされることがあります。 例えば、ID プロバイダーが生体認証を使用してユーザーの SSO セッションを確立する場合は、{{site.data.keyword.appid_short_notm}} のデフォルトの認証コンテキストを変更する必要があります。 デフォルトでは、{{site.data.keyword.appid_short_notm}} は、HTTPS を介してパスワードでユーザーが認証されること (`urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport`) を予期します。



## {{site.data.keyword.appid_short_notm}} と連携する SAML の構成
{: #saml-configure}

{{site.data.keyword.appid_short_notm}} から ID プロバイダーにメタデータを提供し、ID プロバイダーから {{site.data.keyword.appid_short_notm}} にメタデータを提供することで、{{site.data.keyword.appid_short_notm}} と連携するように SAML を構成できます。



### ID プロバイダーへのメタデータの提供
{: #saml-provide-idp}

アプリを構成するには、SAML 互換の ID プロバイダーに情報を提供する必要があります。 その情報はメタデータ XML ファイルを介して交換されます。そこには、信頼関係の確立に使用される構成データも含まれています。
{: shortdesc}

SAML は ID プロバイダーとして構成されるまで有効にすることはできません。
{: tip}

1. {{site.data.keyword.appid_short_notm}} ダッシュボードの**「管理」**タブで、**「SAML」**行の**「編集」**をクリックして、設定を構成できるようにします。
2. **「SAML メタデータ・ファイルのダウンロード (Download SAML Metadata file)」**をクリックします。 ID プロバイダーは、以下の情報がファイルにあることを想定しています。
  <table>
    <tr>
      <th> 変数 </th>
      <th> 説明 </th>
    </tr>
    <tr>
      <td><code>EntityID</code></td>
      <td>{{site.data.keyword.appid_short_notm}} が SAML 要求を発行したことを ID プロバイダーに通知するための ID。</td>
    </tr>
    <tr>
      <td><code>Location URL</code></td>
      <td>ユーザーの認証が正常に終了した後に ID プロバイダーが SAML アサーションを送る場所。</td>
    </tr>
    <tr>
      <td><code>Binding</code></td>
      <td>ID プロバイダーが SAML 応答を送信する方法についての指示。</td>
    </tr>
    <tr>
      <td><code>NameID Format</code></td>
      <td>アサーションのサブジェクトで送信する必要がある ID 形式と {{site.data.keyword.appid_short_notm}} がユーザーを識別する方法を ID プロバイダーが認識する手段。 ID の形式は <code><saml:NameID Format="urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress"/></code> にする必要があります。</td>
    </tr>
    <tr>
      <td><code>WantAssertionsSigned</code></td>
      <td>アサーションに署名する必要があるかどうかを ID プロバイダーが検査する方法。 このサービスはアサーションが署名されていることを想定していますが、暗号化されたアサーションはサポートしていません。</td>
    </tr>
  </table>

3. ID プロバイダーにデータを提供します。 ID プロバイダーがメタデータ・ファイルのアップロードをサポートしている場合は、そうすることができます。 サポートしていない場合は、プロパティーを手動で構成してください。 すべての ID プロバイダーが同じプロパティーを使用するとは限らないため、必ずしもそれらをすべて使用するわけではありません。

  プロパティーの名前は ID プロバイダーの間で異なることがあります。
  {: tip}

4. **「SAML 2.0 フェデレーション (SAML 2.0 Federation)」**を**「有効」**に切り替えます。



### {{site.data.keyword.appid_short_notm}} へのメタデータの提供
{: #saml-provide-appid}

ID プロバイダーからデータを取得し、それを {{site.data.keyword.appid_short_notm}} に提供することができます。
{: shortdesc}

**GUI を使用したメタデータの提供** 

1. {{site.data.keyword.appid_short_notm}} ダッシュボードの**「SAML 2.0」**タブに移動します。 ID プロバイダーから取得した以下のメタデータを**「SAML IdP からのメタデータの提供 (Provide Metadata from SAML IdP)」**セクションに入力します。
  <table>
    <tr>
      <th> 変数 </th>
      <th> 説明 </th>
    </tr>
    <tr>
      <td><code>Sign-in URL</code></td>
      <td>認証のためにユーザーがリダイレクトされる URL。 SAML ID プロバイダーによってホストされます。</td>
    </tr>
    <tr>
      <td><code>Entity ID</code></td>
      <td>SAML ID プロバイダーのグローバルな固有名。</td>
    </tr>
    <tr>
      <td><code>Signing certificate</code></td>
      <td>SAML ID プロバイダーによって発行された証明書。 SAML アサーションの署名と検証のために使用されます。 プロバイダーごとに異なりますが、署名証明書を ID プロバイダーからダウンロードできる可能性があります。 証明書は <code>.pem</code> 形式でなければなりません。</td>
    </tr>
  </table>

2. オプション: 1 次証明書で署名検証に失敗した場合に使用される**「2 次証明書 (Secondary certificate)」**を入力します。 同じ署名鍵をそのまま使用する場合、証明書の認証が期限切れを理由に {{site.data.keyword.appid_short_notm}} でブロックされることはありません。
3. **「プロバイダー名 (Provider Name)」**を更新して、**「保存」**をクリックします。 デフォルト名は SAML です。

認証コンテキストを設定する必要がありますか? API を使用して行うことができます。
{: tip}

</br>

**API を使用したメタデータの提供**

1. [`/saml` API エンドポイント](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.get_saml_idp)に GET 要求を行い、認証コンテキストと証明書を含む現在の SAML 構成を表示します。

  サンプル・コード:
  ```
  curl --request GET \
  https://us-south.appid.cloud.ibm.com/management/v4/<tenant-ID>/config/idps/saml \
  --header `Accept: application/json`
  ```
  {: codeblock}

  出力例:
  ```
  {
    "isActive": true,
    "config": {
      "entityID": "https://example.com/saml2/metadata/706634",
      "signInUrl": "https://example.com/saml2/sso-redirect/706634",
      "certificates": [
        "certificate-example-pem-format"
      ],
      "displayName": "my saml example",
      "authnContext": {
        "class": [
          "urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport"
        ],
        "comparison": "exact"
      }
    }
  }
  ```
  {: screen}

2. 次の例の値をプロバイダーの情報に置き換えて、SAML 構成を作成します。 この例に示している値は必須ですが、表に示すように、より多くの情報を含めることもできます。

  ```
  "config": {
    "authnContext": {
      "class": [
        "urn:oasis:names:tc:SAML:2.0:ac:classes:YourChosenClassValue",
            "urn:oasis:names:tc:SAML:2.0:ac:classes:YourOtherChosenClassValue"
      ],
      "comparison": "sampleComparisonValue"}
    "entityID": "https://example.com/saml2/metadata/706634",
    "signInUrl": "https://example.com/saml2/sso-redirect/706634",
    "certificates": [
      "primary-certificate-example-pem-format"
        "secondary-certificate-example-pem-format"
    ],
    "displayName": "my saml example",
  }
  ```
  {: codeblock}
  {: #configuring-saml-new}

  <table>
    <tr>
      <th> 変数 </th>
      <th> 説明 </th>
    </tr>
    <tr>
      <td><code>signInUrl</code></td>
      <td>認証のためにユーザーがリダイレクトされる URL。 SAML ID プロバイダーによってホストされます。</td>
    </tr>
    <tr>
      <td><code>entityID</code></td>
      <td>SAML ID プロバイダーのグローバルな固有名。</td>
    </tr>
    <tr>
      <td><code>displayName             </code></td>
      <td>SAML 構成に割り当てる名前。</td>
    </tr>
    <tr>
      <td><code>primary-certificate-example-pem-format</code></td>
      <td>SAML ID プロバイダーによって発行された証明書。 SAML アサーションの署名と検証のために使用されます。 プロバイダーごとに異なりますが、署名証明書を ID プロバイダーからダウンロードできる可能性があります。 証明書は <code>.pem</code> 形式でなければなりません。</td>
    </tr>
    <tr>
      <td>オプション: <code>secondary-certificate-example-pem-format</code></td>
      <td>SAML ID プロバイダーから発行されたバックアップ証明書。 1 次証明書で署名検証に失敗した場合に使用されます。 <strong>注</strong>: 同じ署名鍵をそのまま使用する場合、証明書の認証が期限切れを理由に {{site.data.keyword.appid_short_notm}} でブロックされることはありません。</td>
    </tr>
    <tr>
      <td>オプション: <code>authnContext</code></td>
      <td>認証コンテキストは、認証および SAML アサーションの品質を検証するために使用されます。 認証コンテキストを追加するには、クラス配列と比較ストリングをコードに追加します。 <code>class</code> パラメーターと <code>comparison</code> パラメーターの両方を、適切な値で更新してください。 例えば、<code>class</code> パラメーターは <code>urn:oasis:names:tc:SAML:2.0:ac:classes:YourChosenClassValue</code> のようになります。</td>
    </tr>
  </table>

3. [`/saml` API エンドポイント](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp)に PUT 要求を行い、ステップ 2 で作成した構成を {{site.data.keyword.appid_short_notm}} に設定します。 次の例を参照して、どのような要求になるかを確認してください。

  ```
  curl --request PUT \
  https://us-south.appid.cloud.ibm.com/management/v4/<tenant-ID>/config/idps/saml \
  --header `Accept: application/json` \
  --data \
  {
    "isActive": true,
    "config": {
      "entityID": "https://example.com/saml2/metadata/706634",
      "signInUrl": "https://example.com/saml2/sso-redirect/706634",
      "certificates": [
        "primary-certificate-example-pem-format"
      ],
      "displayName": "my saml example",
    }
  }
  ```
  {: screen}



## 構成のテスト
{: #saml-testing}

SAML ID プロバイダーと {{site.data.keyword.appid_short_notm}} の間で構成をテストできます。

1. 構成を保存したことを確認します。
2. {{site.data.keyword.appid_short_notm}} ダッシュボードの**「SAML 2.0」**タブに移動して、**「テスト」**をクリックします。 新しいタブが開きます。
3. ID プロバイダーによって既に認証されているユーザーを使用してログインします。
4. フォームの入力を完了すると、別のページにリダイレクトされます。
  * 認証に成功した場合: {{site.data.keyword.appid_short_notm}} と ID プロバイダーの間の接続は正常に機能しています。 ページには、有効な[アクセス・トークンと識別トークン](/docs/services/appid?topic=appid-tokens#tokens)が表示されます。
  * 認証に失敗した場合: 接続は切断されています。 ページには、エラーと SAML 応答 XML ファイルが表示されます。


問題が発生する場合は、 [トラブルシューティング: SAML](/docs/services/appid?topic=appid-troubleshooting-idp#troubleshooting-idp) を参照してください。
{: tip}




## SAML FAQ
{: #saml-assertions}

さまざまな方法で SAML アサーションを返すことができます。 次の例を参照して、{{site.data.keyword.appid_short_notm}} が予期する応答の形式を確認してください。
{: shortdesc}


### {{site.data.keyword.appid_short_notm}} ではどのような SAML アサーションが求められますか?
{: #saml-example}

このサービスでは、次の例のような SAML アサーションが求めれます。

```
<samlp:Response xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol" ID="s2202bbbbafa9d270d1c15990b738f4ab36139d463" InResponseTo="_e4a78780-35da-012e-8ea7-0050569200d8" Version="2.0" IssueInstant="2011-03-21T11:22:02Z" Destination="https://example.example.com/">
  <saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">idp_entityId</saml:Issuer>
  <samlp:Status xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <samlp:StatusCode  xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol"Value="urn:oasis:names:tc:SAML:2.0:status:Success"/>
  </samlp:Status>
  <saml:Assertion xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="2.0" ID="pfx539c9774-de5c-5f52-0c3f-b1c2e2697a89" IssueInstant="2018-01-29T13:02:58Z" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <saml:Issuer>idp_entityId</saml:Issuer>
    <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      <ds:SignedInfo>
        <ds:CanonicalizationMethod Algorithm="one_of_supported_algo"/>
        <ds:SignatureMethod Algorithm="one_of_supported_algo"/>
        <ds:Reference URI="#pfx539c9774-de5c-5f52-0c3f-b1c2e2697a89">
          <ds:Transforms>
            <ds:Transform Algorithm="one_of_supported_algo"/>
            <ds:Transform Algorithm="one_of_supported_algo"/>
          </ds:Transforms>
          <ds:DigestMethod Algorithm="one_of_supported_algo"/>
          <ds:DigestValue>huywDPPfOEGyyzE7d5hjOG97p7FDdGrjoSfes6RB19g=</ds:DigestValue>
        </ds:Reference>
      </ds:SignedInfo>
 <ds:SignatureValue>BAwNZFgWF2oxD1ux0WPfeHnzL+IWYqGhkM9DD28nI9v8XtPN8tqmIb5y4bomaYknmNpWYn7TgNO2Rn/XOq+N9fTZXO2RybaC49iF+zWibRIcNwFKCCpDL6H6jA5eqJX2YKBR+K6Yt2JPoUIRLmqdgm2lMr4Nwq1KYcSzQ/yoV5W0SN/V5t8EfctFoaXVPdtfHVXkwqHeufo+L4gobFt9NRTzXB0SQEClA1L8hQ+/LhY4l46k1D0c34iWjVLZr+ecQyubf7rekOG/R7DjWCFMTke822dR+eJTPWFsHGSPWCDDHFYqB4QMinTvUnsngjY3AssPqIOjeUxjL3p+GXn8IQ==</ds:SignatureValue>
    </ds:Signature>
    <saml:Subject>
      <saml:NameID Format="urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress">JohnDoe@gmail.com</saml:NameID>
    </saml:Subject>
    <saml:Conditions NotBefore="2018-01-29T12:59:58Z" NotOnOrAfter="2018-01-29T13:05:58Z">
    </saml:Conditions>
</samlp:Response>
```
{: screen}


### どのようなタイプのアルゴリズムが {{site.data.keyword.appid_short_notm}} でサポートされていますか?
{: #saml-signatures}

{{site.data.keyword.appid_short_notm}} は、<a href="http://www.w3.org/2001/04/xmldsig-more#rsa-sha256" target="_blank">RSA-SHA256 <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> アルゴリズムを使用して、XML デジタル署名を処理します。

