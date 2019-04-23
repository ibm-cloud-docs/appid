---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

keywords: authentication, authorization, identity, app security, secure, custom, proprietary, private key, public key, jwt

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

# カスタム
{: #custom-identity}

認証時に独自のカスタム ID プロバイダーを使用できます。 {{site.data.keyword.appid_full}} で具体的にサポート対象となっていない、任意の認証メカニズムに準拠した ID プロバイダーを使用できます (専有のものを含む)。
{: shortdesc}

{{site.data.keyword.appid_short_notm}} が特定の ID プロバイダーを直接サポートしていない場合、{{site.data.keyword.appid_short_notm}} の既存の認証フローと認証プロトコルの間のブリッジとして、カスタム識別フローを使用することができます。 例えば、GitHub または LinkedIn を使用してユーザーにサインインを許可するとします。 ユーザー認証情報を容易に扱えるように ID プロバイダーの既存の SDK を使用してから、その情報をパッケージして {{site.data.keyword.appid_short_notm}} と交換することができます。 多くのエンタープライズ・シナリオでは、既存の ID プロバイダーで独自のカスタム認証プロトコルを使用しているとしても、{{site.data.keyword.appid_short_notm}} の機能も利用できると便利です。 こうした種類のシナリオで、カスタム ID フローは、ユーザーの資格情報を露出せずにユーザーを安全に認証するための、分離された手段となります。

## カスタム ID の構成
{: #custom-configure}

以下のステップに従って、{{site.data.keyword.appid_short_notm}} と連携するようにカスタム ID プロバイダーを構成できます。
{: shortdesc}

### 開始する前に
{: #custom-identity-before}

{{site.data.keyword.appid_short_notm}} とカスタム ID プロバイダーの間の信頼関係を確立するには、最小長 2048 の RSA PEM 鍵ペアが必要です。 実動用に使用する鍵は、必ず安全にバックアップしてください。

鍵の使用方法

- 秘密鍵は、JWT に署名するためにアプリまたは ID プロバイダーで使用されます。
- 公開鍵は、ユーザー情報を入れた JWT を検証するために {{site.data.keyword.appid_short_notm}} によって使用されます。

Open SSL を使用して RSA PEM 鍵ペアを生成するには、以下のコマンドを実行します。

```
$ openssl genpkey -algorithm RSA -out private_key.pem -pkeyopt rsa_keygen_bits:2048
$ openssl rsa -pubout -in private_key.pem -out public_key.pem
```
{: codeblock}

</br>

### GUI を使用した構成
{: #custom-identity-configure-gui}

1. {{site.data.keyword.cloud_notm}} アカウントにサインインし、{{site.data.keyword.appid_short_notm}} のインスタンスにナビゲートします。

2. **「管理」**タブで、**「カスタム ID プロバイダー (Custom Identity Provider)」**を**「オン」**に設定します。

3. 公開鍵を {{site.data.keyword.appid_short_notm}} に登録します。
  1. **「カスタム ID プロバイダー (Custom Identity Provider)」**タブにナビゲートします。
  2. 公開鍵を**「パブリック・キー」**ボックスに貼り付け、**「保存」**をクリックします。



### API を使用した構成
{: #custom-identity-configure-api}

[管理 API エンドポイント](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_custom_idp)への PUT 要求を行って、鍵を登録します。

```
Put {Management URI}/config/idps/custom
Content-Type: application/json
{
    isActive: true,
    config: {
        publicKey: <Your newline separated (\n) PEM public key>
    }
}
```
{: codeblock}

## 構成のテスト
{: #custom-identity-testing}

有効な公開鍵を使用して {{site.data.keyword.appid_short_notm}} インスタンスを構成した後、サービスで提供されているテスト・アプリケーションを使用して、構成が正しくセットアップされていることを確認することができます。 サンプル・アプリでは、標準サインイン・フローで返される、{{site.data.keyword.appid_short_notm}} のアクセス・トークンおよび識別トークンのペイロードを確認できます。

1. **「カスタム ID プロバイダー (Custom Identity Provider)」**タブで、**「テスト」**をクリックしてテスト・アプリケーションを開きます。

2. カスタム ID [プロトコル](https://jwt.io/)の後に [JWT.io](/docs/services/appid?topic=appid-custom-auth#generating-jwts) を使用して、サンプル JWT を作成します。

3. この JWT を、**「JSON Web トークン (JSON Web Token)」**というラベルが付いたボックスに貼り付け、**「テスト」**をクリックしてサンプル認証を実行します。

成功すると、標準のサインイン・フローにおいてアプリケーションで使用可能な、デコードされた {{site.data.keyword.appid_short_notm}} の識別トークンとアクセス・トークンを確認できるようになります。

## 次のステップ
{: #custom-identity-next}

カスタム ID プロバイダーが構成されたので、[それをアプリケーションに追加します](/docs/services/appid?topic=appid-custom-auth#custom-auth)。
