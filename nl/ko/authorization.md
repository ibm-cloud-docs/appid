---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-21"

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

# 핵심 개념
{: #key-concepts}

권한과 인증 간의 차이점에 대해 혼란스러우십니까? 당신만 그런 것이 아닙니다. 이 페이지의 정보를 참조하여 특정 용어, 프로세스 및 서비스에서 토큰을 사용하는 방법에 대해 학습하십시오.
{: shortdesc}

권한 부여 및 인증의 기본 개념에 대해 자세히 알고 싶으십니까? 그렇다면 더 이상 찾으실 필요가 없습니다. 다음 동영상에서 OAuth 2.0, 권한 부여 유형, OIDC 등에 대해 학습할 수 있습니다. 

<iframe class="embed-responsive-item" id="about-appid-basics" title="{{site.data.keyword.appid_short_notm}} 정보" type="text/html" width="640" height="390" src="//www.youtube.com/embed/ndlk-ZhKGXM?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>


## 용어
{: #terms}

다음의 핵심 용어는 서비스에서 권한과 인증 프로세스를 분류하는 방식을 이해하는 데 도움이 될 수 있습니다.

### OAuth 2
{: #term-oauth}
<a href="https://tools.ietf.org/html/rfc6749" target="_blank">OAuth 2 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>는 앱 권한을 제공하는 데 사용하는 개방형 표준 프로토콜입니다.


### OIDC(Open ID Connect)
{: #term-oidc}

<a href="https://openid.net/developers/specs/" target="_blank">OIDC<img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>는 OAuth 2를 기반으로 작동하는 인증 계층입니다. OIDC와 {{site.data.keyword.appid_short_notm}}를 함께 사용할 경우 애플리케이션 인증 정보로 OAuth 엔드포인트를 구성하는 데 도움이 됩니다. SDK를 사용하는 경우 엔드포인트 URL이 자동으로 빌드됩니다. 그러나 서비스 인증 정보를 사용하여 자체적으로 URL을 빌드할 수도 있습니다. URL의 형식은 {{site.data.keyword.appid_short_notm}} 서비스 엔드포인트 + "/oauth/v4" + /tenantID입니다.

    예:

```
{
  "clientId": "7eba72ef-b913-47b0-b3b6-54358bb69035",
  "tenantId": "8f5aa500-357e-443a-aab6-bf878f852b5a",
  "secret": "OWEzZGM4M2UtZjhlYS00MDI2LTkwNGItNDJmYzViMmU2YzIz",
  "name":testing",
  "oAuthServerUrl": "https://us-south.appid.cloud.ibm.com/oauth/v4/8f5aa500-357e-443a-aab6-bf878f852b5a",
  "profilesUrl": "https://us-south.appid.cloud.ibm.com",
  "discoveryEndpoint": "https://us-south.appid.ibm.cloud.com/oauth/v4/8f5aa500-357e-443a-aab6-bf878f852b5a/.well-known/openid-configuration"
}
```
{: screen}

이 예제를 사용하는 경우 URL은 `https://us-south.appid.cloud.ibm.com/oauth/v4/3x176051-a23x-40y4-9645-804943z660q0`이 됩니다. 이제 요청을 작성할 대상 엔드포인트를 추가할 수 있습니다. 다음 표에서 몇 가지 엔드포인트 예제를 참조하십시오.

<table>
  <tr>
    <th>엔드포인트</th>
    <th>형식</th>
  </tr>
  <tr>
    <td>권한</td>
    <td>{oauthServerUrl}/authorization</td>
  </tr>
  <tr>
    <td>토큰</td>
    <td>{oauthServerUrl}/token</td>
  </tr>
  <tr>
    <td>사용자 정보</td>
    <td>{oauthServerUrl}/userinfo</td>
  </tr>
  <tr>
    <td>JWKS</td>
    <td>{oauthServerUrl}/publickeys</td>
  </tr>
</table>

SDK를 사용하는 경우 엔드포인트 URL이 자동으로 빌드됩니다.
{: note}

### 토큰
{: #term-token}

이 서비스는 서로 다른 세 가지 유형의 토큰을 사용합니다. 액세스 토큰은 권한을 나타내며 이를 사용하면 {{site.data.keyword.appid_short}}에 의해 설정된 권한 필터로 보호되는 [백엔드 리소스](/docs/services/appid?topic=appid-backend)와의 통신이 가능합니다. ID 토큰은 인증을 나타내며 사용자에 대한 정보를 포함합니다. 새로 고치기 토큰은 사용자를 재인증하지 않고 새 액세스 토큰을 얻기 위해 사용할 수 있습니다. 사용자는 새로 고치기 토큰을 사용하여 애플리케이션에서 정보를 기억하도록 허용할 수 있습니다. 이 방식으로 사인인된 상태를 유지할 수 있습니다. 토큰은 {{site.data.keyword.appid_short}} 대시보드의 **ID 제공자 > 관리**에서 설정됩니다. 토큰 및 {{site.data.keyword.appid_short}}에서 해당 토큰을 사용하는 방법에 대한 자세한 정보는 [토큰 관리](/docs/services/appid?topic=appid-tokens#tokens)를 참조하십시오.

### 권한 헤더
{: #term-auth-header}

{{site.data.keyword.appid_short}}는 <a href="https://tools.ietf.org/html/rfc6750" target="blank">Token Bearer Specification <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>을 준수하며 HTTP 권한 헤더로 전송된 액세스 및 ID 토큰의 조합을 사용합니다. 권한 헤더에는 세 개의 서로 다른 파트가 공백으로 구분되어 있습니다. 토큰은 base64로 인코딩되어 있습니다. ID 토큰은 선택사항입니다.

    예:

```
Authorization=Bearer {access_token} [{id_token}]
```
{: screen}


### API 전략
{: #term-api-strategy}

API 전략은 요청에 올바른 액세스 토큰이 있는 권한 헤더가 포함될 것으로 예상합니다. 요청에도 ID 토큰이 포함될 수 있지만 필수는 아닙니다. 토큰이 올바르지 않거나 만료된 경우 API 전략에서 다음 HTTP 헤더로 구성된 HTTP 401 오류를 리턴합니다.
```
Www-Authenticate=Bearer scope="{scope}" error="{error}"
```
{: screen}

요청이 올바른 토큰을 리턴하는 경우, 제어가 다음 미들웨어에 전달되며 `appIdAuthorizationContext` 특성이 요청 오브젝트에 삽입됩니다. 이 특성에는 원래 액세스 및 ID 토큰, 일반 JSON 오브젝트로 디코딩된 페이로드 정보가 포함됩니다.

### 웹 앱 전략
{: #term-web-strategy}

웹 앱 전략에서 인증된 절차를 통해 보호된 리소스에 액세스하려는 시도를 발견하면 사용자의 브라우저 경로를 {{site.data.keyword.appid_short}}에서 제공할 수 있는 인증 페이지로 자동 재지정합니다. 인증에 성공하면 사용자가 웹 앱의 콜백 URL로 리턴됩니다. 웹 앱 전략에서 액세스 및 ID 토큰을 확보한 후 `WebAppStrategy.AUTH_CONTEXT`의 HTTP 세션에 저장합니다. 앱 데이터베이스에서 액세스 및 ID 토큰을 저장할 것인지 여부는 사용자가 결정합니다.

### 데이터 분리 및 암호화
{: #term-data-encryption}

{{site.data.keyword.appid_short_notm}}는 사용자 프로파일 속성을 저장하고 암호화합니다. 다중 테넌트 서비스로서 모든 테넌트에는 지정된 암호화 키가 있으며 각 테넌트의 사용자 데이터는 해당 테넌트의 키로만 암호화됩니다.

{{site.data.keyword.appid_short_notm}}는 개인 정보를 저장하기 전에 암호화되었는지 확인합니다.
{: note}


### 경로 재지정 URI
{: #term-redirect}

{{site.data.keyword.appid_short_notm}}는 앱과 상호작용한 후 승인된 완전한 URI 목록을 사용하여 사용자를 경로 재지정합니다. 예를 들어 사용자가 정상적으로 사인인되는 경우 {{site.data.keyword.appid_short_notm}}는 해당 사용자를 앱의 홈 페이지 또는 지정된 다른 페이지로 경로 재지정합니다. URI의 형식은 애플리케이션에 따라 변경될 수 있습니다. 자세한 정보는 [경로 재지정 URI 추가](/docs/services/appid?topic=appid-managing-idp#add-redirect-uri)를 참조하십시오.


### JWKS(JSON Web Key Set)
{: #term-jwks}

JWKS는 암호 키 세트를 나타냅니다. {{site.data.keyword.appid_short_notm}}는 JWKS를 사용하여 서비스에서 생성되는 토큰의 신뢰성을 확인합니다. 키 ID를 사용하여 서명을 확인함으로써 신뢰할 수 있는 소스인 {{site.data.keyword.appid_short_notm}}에서 토큰이 발행되었으며 토큰 내의 정보가 변경된 적이 없음을 확인할 수 있습니다.


