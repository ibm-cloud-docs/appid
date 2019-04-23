---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

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

Security Assertion Markup Language (SAML) は、ユーザーの身分を表明する ID プロバイダーとユーザー ID 情報を取り込むサービス・プロバイダーの間で、認証データと許可データを交換するためのオープン・スタンダードです。
{: shortdesc}

{{site.data.keyword.appid_short_notm}} は、サービス・プロバイダーとして機能し、Active Directory Federation Services などのサード・パーティー・プロバイダーに対するシングル・サインオン (SSO) ログインを開始します。 <a href="http://saml.xml.org/saml-specifications" target="blank">SAML <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> プロトコルは、さまざまなプロファイルやバインド・オプションをサポートします。 {{site.data.keyword.appid_short_notm}} は、HTTP Post バインディングを使用して Web ブラウザー SSO プロファイルをサポートします。

特定の SAML ID プロバイダーの使用方法の手順については、{{site.data.keyword.appid_short_notm}} のセットアップ手順に関する、[Ping One ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-ping-one/)、[Azure Active Directory ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-azure-active-directory/)、または [Active Directory Federation Service ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-active-directory-federation-service/) のブログ投稿を参照してください。
{: tip}



## アサーションについて
{: #saml-assertions}

SAML アサーションは[ユーザー属性](/docs/services/appid?topic=appid-user-profile#user-profile)に似ています。ユーザーに関するステートメントつまり一片の情報であり、ユーザーがアプリに正常にログインすると ID プロバイダーによって {{site.data.keyword.appid_short_notm}} に返されます。アプリ構成と使用する ID プロバイダーによっては、ユーザー名や E メールなど、指定を求めるフィールドが情報に含まれる場合があります。
{: shortdesc}

アサーションが {{site.data.keyword.appid_short_notm}} に返されると、サービスはユーザー ID を統合します。以下のいずれかの OIDC クレームに SAML アサーションが対応している場合、その SAML アサーションは自動的に識別トークンに追加されます。これらの値の 1 つ以上がプロバイダー側で変更された場合、新しい値は、ユーザーが再びログインした後でないと使用できるようになりません。

 * `name`
 * `email`
 * `locale`
 * `picture`

どの標準名にも対応しないアサーションはデフォルトで無視されますが、SAML プロバイダーが他のアサーションを返す場合には、ユーザーがログインするときの情報を取得することが可能です。使用するアサーションの配列を作成することによって、[トークンに情報を注入する](/docs/services/appid?topic=appid-customizing-tokens#customizing-tokens)ことができます。 ただし、必要以上に情報をトークンに追加しないようにしてください。トークンは通常、http ヘッダー内で送信されますが、ヘッダーのサイズは制限されています。
{: tip}

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




## ID プロバイダーへのメタデータの提供
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
      <td>ID プロバイダーがアサーションのサブジェクトの中で送信する必要のある ID 形式を ID プロバイダーが判別する方法。 {{site.data.keyword.appid_short_notm}} がユーザーを識別する方法。</td>
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

## {{site.data.keyword.appid_short_notm}} へのメタデータの提供
{: #saml-provide-appid}

ID プロバイダーからデータを取得し、それを {{site.data.keyword.appid_short_notm}} に提供することができます。
{: shortdesc}

### GUI を使用したメタデータの提供
{: #saml-provide-gui}

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


### API を使用したメタデータの提供
{: #saml-provide-api}

1. [/getSamlMetadata API エンドポイント](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.get_saml_idp)に GET 要求を行って、SAML メタデータを取得します。

  サンプル・コード:
  ```
  <?xml version="1.0"?>
  <getSamlMetadata>
    <?xml version="1.0"?> <EntityDescriptor> <SPSSODescriptor> <NameIDFormat> </NameIDFormat> <AssertionConsumerService /> </SPSSODescriptor>
   </EntityDescriptor>
    </getSamlMetadata>
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
    },
    "validation_data": {
      "certificates": [
        {
          "certificate_index": 0,
          "expiration_timestamp": 1674473996,
          "warning": "Your certificate will expire in 18 days."
        }
      ]
    }
  }
  ```
  {: screen}

2. [/set_saml_idp API エンドポイント](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp)への POST 要求を構成します。

  1. 以下のメタデータの例で、各変数を各自固有の情報に置き換えます。

    ```
    Put {Management URI}/config/idps/saml
    Content-Type: application/json
    {
      "isActive": true,
      "config": {
        "entityID": "https://example.com/saml2/metadata/706634",
      "signInUrl": "https://example.com/saml2/sso-redirect/706634",
      "certificates": [
          "primary-certificate-example-pem-format"
        ],
        "displayName": "my saml example"
      }
    }
    ```
    {: codeblock}

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

  2. オプション: 証明書配列の中で、1 次証明書の後に 2 次証明書を追加します。 2 次証明書は、1 次証明書で署名検証が不合格になった場合に使用されます。 同じ署名鍵をそのまま使用する場合、証明書の認証が期限切れを理由に {{site.data.keyword.appid_short_notm}} でブロックされることはありません。

    例:
    ```
    {
      "isActive": true,
      "config": {
        ...
        "certificates": [
          "primary-certificate-example-pem-format",
          "secondary-certificate-example-pem-format"
        ],
        ...
      }
    }
    ```
    {: screen}
  {: #configuring-saml-new}
  3. オプション: クラス配列と比較ストリングをコードに追加することによって、認証コンテキストを追加します。 `class` パラメーターと `comparison` パラメーターの両方を、適切な値で更新してください。 認証コンテキストは、認証および SAML アサーションの品質を検証するために使用されます。

    例:
    ```
    {
      "isActive": true,
      "config": {
        ...
        "authnContext": {
          "class": [
            "urn:oasis:names:tc:SAML:2.0:ac:classes:YourChosenClassValue",
            "urn:oasis:names:tc:SAML:2.0:ac:classes:YourOtherChosenClassValue"
          ],
          "comparison": "sampleComparisonValue"
        }
      }
    }
    ```
    {: screen}

3. 要求を行います。 オプション値を追加することにした場合、要求は以下の例のようになります。

  ```
  Put {Management URI}/config/idps/saml
    Content-Type: application/json
    {
    "isActive": true,
    "config": {
      ...
      "authnContext": {
        "class": [
          "urn:oasis:names:tc:SAML:2.0:ac:classes:YourChosenClassValue",
            "urn:oasis:names:tc:SAML:2.0:ac:classes:YourOtherChosenClassValue"
        ],
        "comparison": "sampleComparisonValue"
      "entityID": "https://example.com/saml2/metadata/706634",
      "signInUrl": "https://example.com/saml2/sso-redirect/706634",
      "certificates": [
        "primary-certificate-example-pem-format"
        "secondary-certificate-example-pem-format"
      ],
        "displayName": "my saml example"
      }
  }
  ```
  {: codeblock}


## 構成のテスト
{: #saml-testing}

SAML ID プロバイダーと {{site.data.keyword.appid_short_notm}} の間で構成をテストできます。

1. 構成を保存したことを確認します。
2. {{site.data.keyword.appid_short_notm}} ダッシュボードの**「SAML 2.0」**タブに移動して、**「テスト」**をクリックします。 新しいタブが開きます。
3. ID プロバイダーによって既に認証されているユーザーを使用してログインします。
4. フォームの入力を完了すると、別のページにリダイレクトされます。
  * 認証に成功した場合: {{site.data.keyword.appid_short_notm}} と ID プロバイダーの間の接続は正常に機能しています。 ページには、有効な[アクセス・トークンと識別トークン](/docs/services/appid?topic=appid-tokens#tokens)が表示されます。
  * 認証に失敗した場合: 接続は切断されています。 ページには、エラーと SAML 応答 XML ファイルが表示されます。


問題が発生する場合は、 [ID プロバイダー構成のトラブルシューティング](/docs/services/appid?topic=appid-troubleshooting-idp#troubleshooting-idp)を参照してください。
{: tip}
