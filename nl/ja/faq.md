---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}


# FAQ

この FAQ には、{{site.data.keyword.appid_full}} サービスに関する一般的な質問に対する答えがあります。
{: shortdesc}


## {{site.data.keyword.appid_short_notm}} の料金はどのように計算しますか?
{: #pricing}

{{site.data.keyword.appid_short_notm}} では、使用するリソースが増えるにつれて、支払いは少なくなります。
{: shortdesc}

累進階層方式のプランは、認証イベントの数と許可ユーザーの数の 2 つの部分で構成されています。 この 2 つの部分の合計に基づいて、毎月課金されます。 合計額は、数量にその階層の単価を乗算して計算する、各レベルの使用量の累積料金です。

### 認証イベント

認証イベントは、正規または匿名の新しいアクセス・トークンが発行されたときに発生します。識別されたユーザーの場合、新しいアクセス・トークンはそれぞれデフォルトで 1 時間有効になります (実際のユーザー認証による場合でもリフレッシュ・トークンを介した場合でも同じです)。匿名トークンは、デフォルトで 1 カ月有効です。 トークンの期限が切れた後に保護リソースにアクセスするには、新しいトークンを作成する必要があります。 {{site.data.keyword.appid_short_notm}} ダッシュボードの**「サインイン有効期限 (Sign-in Expiration)」**ページで、{{site.data.keyword.appid_short_notm}} トークンの有効期限を更新できます。

{{site.data.keyword.appid_short_notm}} をモバイル・アプリケーションで使用する場合、トークンは key-store または key-chain に保管され、以後のすべての要求に追加されます。トークンには、App ID Android または iOS SDK を使用してアクセスできます。{{site.data.keyword.appid_short_notm}} を Web アプリケーションで使用する場合は、トークンをアプリケーション・セッションの Cookie に保管することをお勧めします。


### 許可ユーザー

許可ユーザーとは、直接的または間接的にサービスにログインする固有のユーザーのことです。 各 ID プロバイダーから 1 人の新しいユーザー (匿名ユーザーを含む) がログインするたびに、1 人分の許可ユーザー料金が課金されます。 例えば、あるユーザーが Facebook でログインし、その後 Google を使用してログインした場合には、それらは 2 つの別個の許可ユーザーと見なされます。

累進階層方式の価格設定について詳しくは、[{{site.data.keyword.Bluemix_notm}} の価格設定の資料](/docs/billing-usage/how_charged.html#services)を参照してください。

</br>


## 暗号化は {{site.data.keyword.appid_short_notm}} でどのように機能しますか?
{: #encryption}

暗号化に関するよくある質問の答えは、以下の表を参照してください。

<table>
  <thead>
    <th colspan=2><img src="images/idea.png" alt="詳細情報アイコン"/>  </th>
  </thead>
  <tbody>
    <tr>
      <td>暗号化を使用のはなぜですか?</td>
      <td>このサービスでは、お客様の保存データの暗号化を行います。</td>
    </tr>
    <tr>
      <td>独自のアルゴリズムを作成したのですか？ どのアルゴリズムをコードで使用しますか?</td>
      <td>当社は独自のものを作成してはいません。このサービスでは、<code>AES</code> および <code>SHA-256</code> をソルト処理と共に使用します。</td>
    </tr>
    <tr>
      <td>公開済みまたはオープン・ソースの暗号化モジュールまたはプロバイダーを使用していますか? 暗号化機能を公開したことがありますか? </td>
      <td>このサービスでは <code>javax.crypto</code> Java ライブラリーを使用しますが、暗号化機能を公開したことはありません。</td>
    </tr>
    <tr>
      <td>鍵を格納するには、どのようにすればよいですか?</td>
      <td>鍵が生成されると、それぞれの領域に固有のマスター鍵を使用して暗号化された後に、ローカルに保管されます。マスター鍵は {{site.data.keyword.keymanagementserviceshort}} に格納されます。</td>
    </tr>
    <tr>
      <td>使用する鍵の強度は何ですか?</td>
      <td>サービスは 16 バイトを使用します。</td>
    </tr>
    <tr>
      <td>暗号化機能を公開するリモート API を呼び出していますか?</td>
      <td>いいえ、していません。</td>
    </tr>
  </tbody>
</table>

</br>

## {{site.data.keyword.appid_short_notm}} ではどのような SAML アサーションが求められますか?
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

</br>

## SAML 署名ではどのようなタイプのアルゴリズムがサポートされていますか?
{: #saml-signatures}

以下のいずれかのアルゴリズムを使用して XML デジタル署名を処理できます。

<table>
  <tr>
    <th> アルゴリズムのタイプ </th>
    <th> アルゴリズムのオプション </th>
  </tr>
  <tr>
    <td>正規化および変換アルゴリズム (コメントあり/なし)</td>
    <td><ul><li><a href="http://www.w3.org/TR/2001/REC-xml-c14n-20010315" target="_blank">正規化 <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></li>
    <li><a href="http://www.w3.org/2001/10/xml-exc-c14n#" target="_blank">排他的正規化 (コメントあり/なし) <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></li>
    <li><a href=" http://www.w3.org/2000/09/xmldsig#enveloped-signature" target="_blank">エンベロープ署名変換 <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></li></ul></td>
  </tr>
  <tr>
    <td>ハッシュ・アルゴリズム</td>
    <td><ul><li><a href="http://www.w3.org/2000/09/xmldsig#sha1" target="_blank">SHA1 ダイジェスト <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmlenc#sha256" target="_blank">SHA256 ダイジェスト <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmlenc#sha512" target="_blank">SHA512 ダイジェスト <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></li></ul></td>
  </tr>
  <tr>
    <td>署名アルゴリズム</td>
    <td><ul><li><a href="http://www.w3.org/2000/09/xmldsig#rsa-sha1" target="_blank">RSA-SHA1 <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmldsig-more#rsa-sha256" target="_blank">RSA-SHA256 <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmldsig-more#rsa-sha512" target="_blank">RSA-SHA512 <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></li>
    <li><a href="http://www.w3.org/2000/09/xmldsig#hmac-sha1" target="_blank">HMAC-SHA1 <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></li></ul></td>
  </tr>
</table>

SAML ID プロバイダーの使用について詳しくは、[エンタープライズ ID プロバイダーの構成](enterprise.html)を参照してください。
