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



# 取得記號
{: #obtain-tokens}

當使用者或後端服務與您的應用程式互動時，他們可能需要獲得授權才能執行特定動作。{{site.data.keyword.appid_short_notm}} 會驗證提出要求的實體已獲授權，並將存取權和身分記號傳回給您的應用程式。如果提出要求的實體是一般使用者，則記號可能包含使用者的相關資訊，例如其許可權的範圍及其名稱。如果是後端服務，則只會傳回存取記號。
{: shortdesc}


## 取得用戶端 ID 及密碼
{: #obtain-clientid-secret}

若要取得記號，您必須具有用戶端 ID 及密碼。認證是每一個應用程式所特有，用來協助識別及驗證可能獲指派記號的使用者。
{: shortdesc}


### 使用 GUI
{: #credentials-gui}

1. 導覽至 {{site.data.keyword.appid_short_notm}} 儀表板的**應用程式**標籤。

2. 如果您已經列出一組認證，則可以跳到步驟 3。如果沒有，請建立一組。
    1. 在**應用程式**標籤上，按一下**新增應用程式**。
    2. 給與應用程式名稱，然後按一下**儲存**，以回到已登錄應用程式的清單。應用程式的名稱不能超過 50 個字元。

3. 從已登錄應用程式的清單中，選取您要使用的應用程式。此列會展開以顯示您的認證。

4. 複製用戶端 ID 及密碼。


### 透過使用 API
{: #credentials-api}

1.  對 [`/management/v4/{tenantId}/applications` 端點](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Applications/mgmt.registerApplication)提出 POST 要求。

  要求：

  ```
  curl -X POST \  https://us-south.appid.cloud.ibm.com/management/v4/39a37f57-a227-4bfe-a044-93b6e6060b61/applications/ \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer IAM_TOKEN' \
  -d '{"name": "ApplicationName"}'
  ```
  {: codeblock}

  回應範例：

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

2. 複製用戶端 ID 及密碼。



## 取得存取權和身分記號
{: #obtain-access-id-tokens}

利用用戶端 ID 和密碼，您可以使用下列步驟來取得存取權和身分記號。
{: shortdesc}


### 使用 SDK 取得記號
{: obtain-token-sdk}

1. 從您的認證取得您的承租戶 ID、用戶端 ID、密碼和 OAuth 伺服器 URL。

2. 使用步驟 1 的資訊，更新下列程式碼 Snippet，並將它新增至您的應用程式。預設程式碼適用於 Node.js。如果您使用另一種語言，可以在本主題的開頭，選擇一個適合您的語言。

  Node：
  {: ph data-hd-programlang='javascript'}

  ```
  const config = {
    tenantId: "{tenant-id}",
    clientId: "{client-id}",
    secret: "{secret}",
    oauthServerUrl: "{oauth-server-url}"
  };

  const TokenManager = require('ibmcloud-appid').TokenManager;

  const tokenManager = new TokenManager(config);async function getAppIdentityToken() {
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

  Java：
  {: ph data-hd-programlang='java'}
  ```
  AppID.getInstance().signinWithResourceOwnerPassword(getApplicationContext(), username, password,
         new TokenResponseListener() {
         @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //Exception occurred
        }

        @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
            //User authenticated
        }
      });
  ```
  {: codeblock}
  {: ph data-hd-programlang='java'}

iOS Swift：
{: ph data-hd-programlang='swift'}

  ```
  class delegate : TokenResponseDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
    //User authenticated
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
      //Exception occurred
        }

        }

  AppID.sharedInstance.signinWithResourceOwnerPassword(username: username, password: password, delegate: delegate())
  ```
  {: codeblock}
  {: ph data-hd-programlang='swift'}

伺服器 Swift：
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

### 使用 API 取得記號
{: #obtain-tokens-api}

1. 從您的認證取得您的承租戶 ID、用戶端 ID、密碼和 OAuth 伺服器 URL。

2. 將用戶端 ID 及密碼編碼。

    1. 請使用前一節的步驟來複製用戶端 ID 及密碼。
    2. 使用 base64 編碼器來編碼您的授權資訊。
    3. 複製輸出。

3. 向 API 提出要求以取得記號。您的要求的資料區段會根據您使用的授權類型而有所不同。 

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

您用來取得記號的授權類型，可以根據您使用的授權類型而有所不同。如需詳細的選項清單，請參閱[Swagger 文件](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Authorization%20Server%20-%20Authorization%20Server%20V4/oauth-server.token)。
