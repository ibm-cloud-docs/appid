---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-29"

keywords: authentication, authorization, identity, app security, secure, access management, roles, attributes, users

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
{:java: .ph data-hd-programlang='java'}
{:javascript: .ph data-hd-programlang='javascript'}
{:swift: .ph data-hd-programlang='swift'}
{:curl: .ph data-hd-programlang='curl'}



# トークンの取得
{: #obtain-tokens}

ユーザーまたはバックエンド・サービスがアプリと対話するときには、特定のアクションを実行するために許可が必要になる場合があります。 {{site.data.keyword.appid_short_notm}} は、要求を行ったエンティティーが許可されていることを検証し、アクセス・トークンと識別トークンをアプリに返します。 要求したエンティティーがエンド・ユーザーである場合は、通常、トークンにはユーザーに関する情報 (権限の範囲や名前など) が含まれています。 バックエンド・サービスである場合は、アクセス・トークンのみが返されます。
{: shortdesc}


## クライアント ID とシークレットを取得する
{: #obtain-clientid-secret}

トークンを取得するには、クライアント ID とシークレットが必要です。 これらの資格情報は各アプリケーションに固有のものであり、これを使用して、トークンが割り当てられるユーザーを識別して検証することができます。 
{: shortdesc}


### GUI を使用する場合
{: #credentials-gui}

1. {{site.data.keyword.appid_short_notm}} ダッシュボードの**「アプリケーション」**タブにナビゲートします。

2. 資格情報のセットが既にリストされている場合は、手順 3 にスキップできます。リストされていない場合は、作成します。
    1. **「アプリケーション」**タブで、**「アプリケーションの追加」**をクリックします。
    2. アプリケーションに名前を付け、**「保存」**をクリックして、登録済みアプリのリストに戻ります。 アプリケーションの名前は 50 文字を超えてはなりません。

3. 登録済みアプリのリストから、作業対象のアプリケーションを選択します。 行が展開され、資格情報が表示されます。

4. クライアント ID とシークレットをコピーします。


### API を使用する場合
{: #credentials-api}

1.  [`/management/v4/{tenantId}/applications` エンドポイント](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Applications/mgmt.registerApplication)に対して POST 要求を行います。

  要求:

  ```
  curl -X POST \  https://us-south.appid.cloud.ibm.com/management/v4/39a37f57-a227-4bfe-a044-93b6e6060b61/applications/ \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer IAM_TOKEN' \
  -d '{"name": "ApplicationName"}'
  ```
  {: codeblock}

  応答例:

  ```
  {
    "clientId": "c90830bf-11b0-4b65-bffe-9773f8703bad",
    "tenantId": "b42f7429-fc24-48ds-b4f9-616bcc31cfd5",
    "secret": "YWQyNjdkZjMtMGRhZC00ZWRkLThiOTQtN2E3ODEyZjhkOWQz",
    "name": "testing",
    "oAuthServerUrl": "https://us-south.appid.cloud.ibm.com/oauth/v4/b42f7429-fc24-48ds-b4f9-616bcb31cfd5",
    "profilesUrl": "https://us-south.appid.cloud.ibm.com",
    "discoveryEndpoint": "https://us-south.appid.cloud.ibm.com/oauth/v4/b42f7429-fc24-48ds-b4f9-616bcb31cfd5/.well-known/openid-configuration"
  }
  ```
  {: screen}

2. クライアント ID とシークレットをコピーします。



## アクセス・トークンと識別トークンの取得
{: #obtain-access-id-tokens}

クライアント ID とシークレットを取得したら、以下の手順でアクセス・トークンと識別トークンを取得できます。
{: shortdesc}


### SDK を使用したトークンの取得
{: obtain-token-sdk}

1. 資格情報からテナント ID、クライアント ID、シークレット、および OAuth サーバー URL を取得します。

2. 手順 1 の情報を使用して、以下のコード・スニペットを更新し、アプリケーションに追加します。 デフォルトのコードは Node.js 用です。 別の言語を使用している場合は、このトピックの最初に、該当する言語を選択できます。

  Node:
  {: ph data-hd-programlang='javascript'}

  ```
  const config = {
    tenantId: "{tenant-id}",
    clientId: "{client-id}",
    secret: "{secret}",
    oauthServerUrl: "{oauth-server-url}"
  };

  const TokenManager = require('ibmcloud-appid').TokenManager;

  const tokenManager = new TokenManager(config);

  async function getAppIdentityToken() {
    try {
        const tokenResponse = await tokenManager.getApplicationIdentityToken();
        console.log('Token response : ' + JSON.stringify(tokenResponse));

        //the token response contains the access_token, expires_in, token_type
    } catch (err) {
        console.log('err obtained : ' + err);
    }
  }
  ```
  {: codeblock}
  {: ph data-hd-programlang='javascript'}

  Java:
  {: ph data-hd-programlang='java'}
  ```
  AppID.getInstance().signinWithResourceOwnerPassword(getApplicationContext(), username, password,
         new TokenResponseListener() {
    @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
        //例外の発生
    }

    @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
        //ユーザーの認証
        }
  });
  ```
  {: codeblock}
  {: ph data-hd-programlang='java'}

iOS Swift:
{: ph data-hd-programlang='swift'}

  ```
  class delegate : TokenResponseDelegate {
    public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
    //ユーザーの認証
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
    //例外の発生
    }
  }

  AppID.sharedInstance.signinWithResourceOwnerPassword(username: username, password: password, delegate: delegate())
  ```
  {: codeblock}
  {: ph data-hd-programlang='swift'}

サーバー Swift:
{: ph data-hd-programlang='swift'}

  ```
  let options = [
    "clientId": "{client-id}",
  	"secret": "{secret}",
  	"tenantId": "{tenant-id}",
  	"oauthServerUrl": "{oauth-server-url}",
  	"redirectUri": "{app-url}" + CALLBACK_URL
  ]
  let webappKituraCredentialsPlugin = WebAppKituraCredentialsPlugin(options: options)
  let kituraCredentials = Credentials()
  kituraCredentials.register(plugin: webappKituraCredentialsPlugin)
  ```
  {: codeblock}
  {: ph data-hd-programlang='swift'}


</br>

### API を使用したトークンの取得
{: #obtain-tokens-api}

1. 資格情報からテナント ID、クライアント ID、シークレット、および OAuth サーバー URL を取得します。

2. クライアント ID とシークレットをエンコードします。

    1. 前のセクションの手順を使用して、クライアント ID とシークレットをコピーします。
    2. Base64 エンコーダーを使用して、許可情報をエンコードします。
    3. 出力をコピーします。

3. トークンを取得するための API に要求を発行します。 要求のデータ・セクションは、使用する付与タイプに応じて異なります。 

  ```
  curl -X POST \
  https://{region}.appid.cloud.ibm.com/oauth/v4/{tenant_id}/token \
  -H 'Authorization: Basic base64Encoded{{client-ID}:{client-secret}}' \
  -H 'Content-Type: application/x-www-form-urlencoded' \
  -H `Accept: application/json` \
  -F grant_type=password \
  -F username=testuser@test.com \
  -F password=testuser
  ```
  {: codeblock}

トークンを取得するために使用する付与タイプは、使用している許可のタイプに応じて異なります。 オプションの詳細なリストについては、[Swagger の資料](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Authorization%20Server%20-%20Authorization%20Server%20V4/oauth-server.token)を参照してください。
