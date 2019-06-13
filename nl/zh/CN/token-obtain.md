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



# 获取令牌
{: #obtain-tokens}

用户或后端服务与应用程序交互时，可能需要获得授权才能执行特定操作。{{site.data.keyword.appid_short_notm}} 会验证发出请求的实体是否已获得授权，并将访问令牌和身份令牌返回给应用程序。如果发出请求的实体是最终用户，那么令牌可能包含有关用户的信息，例如用户的许可权作用域和用户名。如果发出请求的是后端服务，那么仅返回访问令牌。
{: shortdesc}


## 获取客户端标识和私钥
{: #obtain-clientid-secret}

为了获取令牌，您必须具有客户端标识和私钥。凭证特定于每个应用程序，用于帮助识别和验证可能向其分配了令牌的用户。
{: shortdesc}


### 使用 GUI
{: #credentials-gui}

1. 导航至 {{site.data.keyword.appid_short_notm}} 仪表板的**应用程序**选项卡。

2. 如果已列出一组凭证，那么可以跳至步骤 3。如果没有列出，请创建凭证。
    1. 在**应用程序**选项卡上，单击**添加应用程序**。
    2. 为应用程序提供名称，然后单击**保存**以返回到已注册应用程序的列表。应用程序的名称不能超过 50 个字符。

3. 从已注册应用程序的列表中，选择要使用的应用程序。相应行将展开以显示凭证。

4. 复制客户端标识和私钥。


### 使用 API
{: #credentials-api}

1.  对 [`/management/v4/{tenantId}/applications` 端点](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Applications/mgmt.registerApplication)发出 POST 请求。

  请求：

  ```
  curl -X POST \  https://us-south.appid.cloud.ibm.com/management/v4/39a37f57-a227-4bfe-a044-93b6e6060b61/applications/ \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer IAM_TOKEN' \
  -d '{"name": "ApplicationName"}'
  ```
  {: codeblock}

  示例响应：

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

2. 复制客户端标识和私钥。



## 获取访问令牌和身份令牌
{: #obtain-access-id-tokens}

可以使用以下步骤通过客户端标识和私钥来获取访问令牌和身份令牌。
{: shortdesc}


### 使用 SDK 获取令牌
{: obtain-token-sdk}

1. 从凭证中获取租户标识、客户端标识、私钥和 OAuth 服务器 URL。

2. 使用步骤 1 中的信息更新以下代码片段，然后将其添加到应用程序中。缺省代码是针对 Node.js 的。如果要使用其他语言，可以在本主题开始位置选择适用于您的语言。

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

服务器 Swift：
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

### 使用 API 获取令牌
{: #obtain-tokens-api}

1. 从凭证中获取租户标识、客户端标识、私钥和 OAuth 服务器 URL。

2. 对您的客户端标识和私钥进行编码。

    1. 使用上一部分中的步骤来复制客户端标识和私钥。
    2. 使用 Base64 编码器对这些授权信息进行编码。
    3. 复制输出。

3. 对 API 发出请求以获取令牌。请求的数据部分根据使用的授权类型而有所不同。 

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

用于获取令牌的授权类型根据使用的权限类型而有所不同。有关选项的详细列表，请查看 [Swagger 文档](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Authorization%20Server%20-%20Authorization%20Server%20V4/oauth-server.token)。
