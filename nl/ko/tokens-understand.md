---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-11"

keywords: authentication, authorization, identity, app security, secure, access, tokens

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



# 토큰에 대한 정보
{: #tokens}

사용자가 정상적으로 인증되면 애플리케이션은 {{site.data.keyword.appid_short_notm}}에서 토큰을 받습니다. 이 서비스는 서로 다른 세 가지 유형의 토큰을 사용하여 인증 프로세스를 완료합니다.
{: shortdesc}


## 액세스 토큰
{: #access}

액세스 토큰은 권한을 나타내며 이를 사용하면 {{site.data.keyword.appid_short}}에 의해 설정된 권한 필터로 보호되는 [백엔드 리소스](/docs/services/appid?topic=appid-backend)와의 통신이 가능합니다. 토큰은 JOSE(JavaScript Object Signing and Encryption) 스펙을 준수합니다. 이 토큰은 RS256 알고리즘을 사용하는 JSON 웹 키로 서명된 <a href="https://jwt.io/introduction/" target="blank">JSON 웹 토큰 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>으로 형식화됩니다.

토큰 예제:
  ```
Header: {
    "alg": "RS256",
    "typ": "JWT",
    "kid": "appId-39a37f57-a227-4bfe-a044-93b6e6050a61-2018-08-02T11:57:43.401",
    "ver": 4
  }
  Payload:
  {
    "iss": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61",
    "exp": 1551903163,
    "aud": [
      "968c2306-9aef-4109-bc06-4f5ed6axi24a"
    ],
    "sub": "2b96cc04-eca5-4122-a8de-6e07d14c13a5",
    "email_verified": true,
    "amr": [
      "cloud_directory"
    ],
    "iat": 1551899553,
    "tenant": "39a37f57-a227-4bfe-a044-93b6e6050a61",
    "scope": "openid appid_default appid_readprofile appid_readuserattr appid_writeuserattr appid_authenticated"
  }
  ```
  {: screen}

## ID 토큰이 무엇입니까?
{: #identity}

ID 토큰은 인증을 나타내며 사용자에 대한 정보를 포함합니다. 이름, 이메일, 성 및 위치에 대한 정보를 제공합니다. 토큰은 사용자의 이미지에 대한 URL을 리턴할 수도 있습니다. 이 토큰은 RS256 알고리즘을 사용하는 JSON 웹 키로 서명된 <a href="https://jwt.io/introduction/" target="blank">JSON 웹 토큰 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>으로 형식화됩니다.

토큰 예제:
  ```
Header: {
    "alg": "RS256",
    "typ": "JWT",
    "kid": "appId-39a37f57-a227-4bfe-a044-93b6e6050a61-2018-08-02T11:57:43.401",
    "ver": 4
  }
  Payload:
  {
    "iss": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61",
    "aud": [
      "968c2306-9aef-4109-bc06-4f5ed6axi24a"
    ],
    "exp": 1551903163,
    "tenant": "39a37f57-a227-4bfe-a044-93b6e6050a61",
    "iat": 1551899553,
    "email": "appid155@mailinator.com",
    "name": "appid155@mailinator.com",
    "sub": "2b96cc04-eca5-4122-a8de-6e07d14c13a5",
    "email_verified": true,
    "identities": [
      {
        "provider": "cloud_directory",
        "id": "118c0278-3526-4954-876b-cf70eb88efa2"
      }
    ],
    "amr": [
      "cloud_directory"
    ]
  }
  ```
  {: screen}


ID 토큰에는 부분적인 사용자 정보만 포함됩니다. ID 제공자에서 제공되는 모든 정보를 확인하기 위해 [/userinfo 엔드포인트](/docs/services/appid?topic=appid-predefined-attributes#predefined-access-api)를 사용할 수 있습니다.

## 새로 고치기 토큰이 무엇입니까?
{: #refresh}

{{site.data.keyword.appid_short}}의 경우 <a href="http://openid.net/specs/openid-connect-core-1_0.html#RefreshTokens" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>에 정의된 것처럼 재인증 없이 새 액세스 및 ID 토큰을 획득하는 기능을 지원합니다. 새로 고치기 토큰은 사용자가 사인인하기 위해 어떤 조치(예: 인증 정보 제공)도 수행할 필요가 없도록 액세스 토큰을 갱신하기 위해 사용할 수 있습니다. 액세스 토큰과 마찬가지로 새로 고치기 토큰에도 {{site.data.keyword.appid_short_notm}}에서 권한 부여 여부를 판별할 수 있도록 해주는 데이터가 포함되어 있습니다. 하지만 이 토큰은 불투명합니다.

새로 고치기 토큰은 정규 액세스 토큰보다 수명이 더 길기 때문에 액세스 토큰이 만료되더라도 새로 고치기 토큰은 여전히 유효하며 액세스 토큰을 갱신하기 위해 사용할 수 있습니다. {{site.data.keyword.appid_short_notm}}의 새로 고치기 토큰은 1 - 90일 동안 지속되도록 구성할 수 있습니다. 새로 고치기 토큰을 완전히 활용하려면 전체 수명 기간 동안 또는 해당 토큰이 갱신될 때까지 토큰이 지속되도록 하십시오. 새로 고치기 토큰만 사용해서는 사용자가 리소스에 직접 액세스할 수 없으므로 액세스 토큰보다 더 오래 지속되더라도 안전합니다. 우수 사례의 경우 새로 고치기 토큰을 수신한 클라이언트에서 해당 토큰을 안전하게 저장한 후 해당 토큰을 발행한 권한 서버로만 전송해야 합니다.

추가적인 편의성을 위해 {{site.data.keyword.appid_short_notm}}는 액세스 토큰이 갱신될 때 새로 고치기 토큰 및 해당 만기 날짜도 갱신함으로써 현재 새로 고치기 토큰이 만료되기 이전 시점의 활성 상태인 한 사용자가 로그인 상태를 유지할 수 있도록 해줍니다. 다른 한편으로는 새로 고치기 토큰을 사용하면서도 사용자가 주기적으로 로그인하도록 강제하려는 경우 앱에서 사용자가 해당 인증 정보를 입력하여 로그인할 때 리턴된 새로 고치기 토큰만 사용할 수 있습니다. 하지만 <a href="https://tools.ietf.org/html/rfc6749#page-47" target="_blank">OAuth 2.0 스펙 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>에서 설명한 것처럼 항상 {{site.data.keyword.appid_short_notm}}에서 받은 최신 새로 고치기 토큰을 사용하는 것이 좋습니다.


이러한 토큰을 통해 로그인 프로세스를 간소화할 수 있지만 예를 들어 새로 고치기 토큰이 손상된 것으로 판단되는 경우 언제든지 해당 토큰을 취소할 수 있도록 앱이 토큰에 종속되어서는 안됩니다. 새로 고치기 토큰을 취소해야 하는 경우 새로 고치기 토큰을 취소하는 두 가지 방법이 있습니다. 새로 고치기 토큰이 있는 경우 <a href="https://tools.ietf.org/html/rfc7009#section-2" target="_blank">RFC7009 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>에 따라 해당 토큰을 취소할 수 있습니다. 또는 사용자 ID가 있는 경우 <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/" target="_blank">관리 API <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 사용하여 새로 고치기 토큰을 취소할 수 있습니다. 관리 API에 액세스하는 방법에 대한 자세한 정보는 [서비스 액세스 관리](/docs/services/appid?topic=appid-service-access-management#service-access-management)를 참조하십시오.

새로 고치기 토큰 관련 작업을 수행하는 예제 및 해당 예제를 사용하여 기억하기 기능을 구현하는 방법은 [시작하기 샘플](/docs/services/appid?topic=appid-getting-started#getting-started)을 참조하십시오.


## 토큰은 어디에서 제공됩니까?
{: #where}

토큰은 {{site.data.keyword.appid_short_notm}} OAuth 서버를 통해 발행되며 [JSON 웹 토큰(JWT)](https://jwt.io/introduction/)으로 형식화됩니다. 이 토큰은 RS256 알고리즘을 사용하는 [JSON 웹 키(JWK)](https://tools.ietf.org/html/rfc7517)로 서명되어 있습니다.

## 토큰에 포함된 정보는 어떻게 처리됩니까?
{: #contains}

액세스 토큰에는 표준 JWT 청구 세트 및 {{site.data.keyword.appid_short_notm}} 특정 청구 세트(예: 테넌트 ID)가 포함되어 있습니다. ID 토큰에는 사용자 특정 정보가 포함되어 있습니다. 토큰 내의 정보는 [사용자 프로파일](/docs/services/appid?topic=appid-user-profile#user-profile)의 일부인 청구로 저장됩니다.

## 토큰을 받는 방법은 무엇입니까?
{: #received}

토큰은 정상적인 인증 후 앱에서 수신합니다. 이 토큰을 사용하여 사용자 권한 및 인증에 대한 정보를 검색할 수 있습니다. 액세스 토큰은 리소스에 대한 요청을 전송하여 보호된 리소스에 대한 액세스 권한을 받기 위해 사용할 수 있습니다. 요청에서 액세스 토큰은 [전달자 인증 스킴](https://tools.ietf.org/html/rfc6750#page-5)에 설명되어 있습니다. 토큰을 추출하려면 앱에서 헤더를 구문 분석해야 합니다.

요청 예제:

  ```
  GET /resource HTTP/1.1
  Host: server.example.com
  Authorization: Bearer  mF_9.B5f-4.1JqM mF_9.B5f-4.1JqM
  ```
  {: screen}

## 토큰을 설정하는 방법은 무엇입니까?
{: #set}

토큰 구성은 {{site.data.keyword.appid_short_notm}} 대시보드를 통해 사용 및 사용 안함으로 설정할 수 있습니다. 구성 옵션에 대한 자세한 정보는 [토큰 관리](/docs/services/appid?topic=appid-managing-idp#managing-idp)를 참조하십시오.
