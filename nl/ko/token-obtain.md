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



# 토큰 얻기
{: #obtain-tokens}

사용자 또는 백엔드 서비스가 앱과 상호작용할 때 특정 조치를 수행하려면 이들에게 권한이 부여되어야 합니다. {{site.data.keyword.appid_short_notm}}는 요청을 작성하는 엔티티에 권한이 부여되었으며 이 엔티티가 액세스 및 ID 토큰을 앱에 리턴하는지 확인합니다. 요청을 작성하는 엔티티가 일반 사용자일 경우 사용자 권한의 범위 및 사용자 이름과 같은 사용자 정보가 토큰에 포함될 수 있습니다. 백엔드 서비스일 경우 액세스 토큰만 리턴됩니다.
{: shortdesc}


## 클라이언트 ID 및 시크릿 가져오기
{: #obtain-clientid-secret}

토큰을 얻으려면 클라이언트 ID와 시크릿이 있어야 합니다. 인증 정보는 각 애플리케이션에 국한되며, 토큰이 지정될 수 있는 사용자를 식별하고 해당 사용자의 유효성을 검증하는 데 사용됩니다. 
{: shortdesc}


### GUI 사용
{: #credentials-gui}

1. {{site.data.keyword.appid_short_notm}} 대시보드의 **애플리케이션** 탭으로 이동하십시오.

2. 나열된 인증 정보 세트가 이미 있는 경우 3단계로 건너뛸 수 있고, 없는 경우 인증 정보를 작성하십시오.
    1. **애플리케이션** 탭에서 **애플리케이션 추가**를 클릭하십시오.
    2. 애플리케이션 이름을 제공한 후 **저장**을 클릭하여 등록된 앱 목록으로 돌아가십시오. 애플리케이션 이름은 50자를 초과할 수 없습니다.

3. 등록된 앱 목록에서 작업할 애플리케이션을 선택하십시오. 해당 행이 펼쳐지면서 인증 정보가 표시됩니다.

4. 클라이언트 ID와 시크릿을 복사하십시오.


### API 사용
{: #credentials-api}

1.  [`/management/v4/{tenantId}/applications` 엔드포인트](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Applications/mgmt.registerApplication)에 대한 POST 요청을 작성하십시오.

  요청:

  ```
  curl -X POST \  https://us-south.appid.cloud.ibm.com/management/v4/39a37f57-a227-4bfe-a044-93b6e6060b61/applications/ \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer IAM_TOKEN' \
  -d '{"name": "ApplicationName"}'
  ```
  {: codeblock}

  응답 예제:

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

2. 클라이언트 ID와 시크릿을 복사하십시오.



## 액세스 및 ID 토큰 얻기
{: #obtain-access-id-tokens}

클라이언트 ID와 시크릿을 사용할 경우 다음 단계를 수행하여 액세스 및 ID 토큰을 얻을 수 있습니다.
{: shortdesc}


### SDK를 사용하여 토큰 얻기
{: obtain-token-sdk}

1. 인증 정보에서 테넌트 ID, 클라이언트 ID, 시크릿 및 OAuth 서버 URL을 얻으십시오.

2. 1단계의 정보를 사용하여 다음 코드 스니펫을 업데이트한 후 이를 애플리케이션에 추가하십시오. 기본 코드는 Node.js용입니다. 다른 언어로 작업하는 경우 이 주제의 시작 부분에서 자신에게 해당하는 언어를 선택할 수 있습니다.

  노드:
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
  AppID.getInstance().signinWithResourceOwnerPassword(getApplicationContext(), username, password, new TokenResponseListener() {
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

iOS Swift:
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

서버 Swift:
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

### API를 사용하여 토큰 얻기
{: #obtain-tokens-api}

1. 인증 정보에서 테넌트 ID, 클라이언트 ID, 시크릿 및 OAuth 서버 URL을 얻으십시오.

2. 클라이언트 ID 및 시크릿을 인코딩하십시오.

    1. 앞 절의 단계를 사용하여 클라이언트 ID와 시크릿을 복사하십시오.
    2. Base-64 인코더를 사용하여 권한 정보를 인코딩하십시오.
    3. 출력을 복사하십시오.

3. API를 요청하여 토큰을 얻으십시오. 사용 중인 권한 부여 유형에 따라 요청의 데이터 섹션이 달라집니다. 

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

토큰을 얻을 때 사용하는 권한 부여 유형은 작업 중인 권한 유형에 따라 달라질 수 있습니다. 자세한 옵션 목록은 [swagger 문서](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Authorization%20Server%20-%20Authorization%20Server%20V4/oauth-server.token)를 확인하십시오.
