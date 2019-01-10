---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}




# 핵심 개념
{: #key-concepts}

권한과 인증 간의 차이점에 대해 혼란스러우십니까? 당신만 그런 것이 아닙니다. 이 페이지의 정보를 참조하여 특정 용어, 프로세스 및 서비스에서 토큰을 사용하는 방법에 대해 학습하십시오.
{: shortdesc}


## 용어
{: #terms}


다음의 핵심 용어는 서비스에서 권한과 인증 프로세스를 분류하는 방식을 이해하는 데 도움이 될 수 있습니다.

<dl>
  <dt>OAuth 2</dt>
    <dd><a href="https://tools.ietf.org/html/rfc6749" target="_blank">OAuth 2 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>는 앱 권한을 제공하는 데 사용하는 개방형 표준 프로토콜입니다.</dd>
  <dt>OIDC(Open ID Connect)</dt>
    <dd><p><a href="http://openid.net/developers/specs/" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>는 OAuth 2에서 작동하는 인증 계층입니다.</p>
    <p>OIDC 및 {{site.data.keyword.appid_short_notm}}를 함께 사용하는 경우 서비스 인증 정보는 OAuth 엔드포인트를 구성하는 데 도움이 됩니다. SDK를 사용하는 경우 엔드포인트 URL이 자동으로 빌드됩니다. 그러나 서비스 인증 정보를 사용하여 자체적으로 URL을 빌드할 수도 있습니다. 다음 예제와 표에서 URL을 함께 배치하는 방법을 알아볼 수 있습니다.</p>
    <pre class="codeblock">
    <code>{
      "version": 3,
      "clientId": "e8ac1132-5151-4d8a-934e-0141de8e2b34",
      "secret": "XYZ5ZYXzXYZtNyz5Yi00YzQ2LXYwMZctXyM5ODA4NjFhYxYZ",
      "tenantId": "3x176051-a23x-40y4-9645-804943z660q0",
      "oauthServerUrl": "https://appid-oauth.ng.bluemix.net/oauth/v3/3x176051-a23x-40y4-9645-804943z660q0",
      "profilesUrl": "https://appid-profiles.ng.bluemix.net/"
    }</code></pre>
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
    <p><strong>참고</strong>: SDK를 사용하는 경우 엔드포인트 URL이 자동으로 빌드됩니다.</p></dd>
  <dt>토큰</dt>
    <dd>이 서비스는 서로 다른 세 가지 유형의 토큰을 사용합니다. 액세스 토큰은 권한을 나타내며 이를 사용하면 {{site.data.keyword.appid_short}}에 의해 설정된 권한 필터로 보호되는 [백엔드 리소스](/docs/services/appid/backend-apps.html)와의 통신이 가능합니다. ID 토큰은 인증을 나타내며 사용자에 대한 정보를 포함합니다. 새로 고치기 토큰은 사용자를 재인증하지 않고 새 액세스 토큰을 얻기 위해 사용할 수 있습니다. 사용자는 새로 고치기 토큰을 사용하여 애플리케이션에서 정보를 기억하도록 허용할 수 있습니다. 이 방식으로 사인인된 상태를 유지할 수 있습니다. 토큰 및 {{site.data.keyword.appid_short}}에서 해당 토큰을 사용하는 방법에 대한 자세한 정보는 [토큰 유효성 검증](tokens.html#remote-validation)을 참조하십시오.
  </dd>
  <dt>권한 헤더</dt>
    <dd><p>{{site.data.keyword.appid_short}}는 <a href="https://tools.ietf.org/html/rfc6750" target="blank">Token Bearer Specification <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>을 준수하며 HTTP 권한 헤더로 전송된 액세스 및 ID 토큰의 조합을 사용합니다. 권한 헤더에는 세 개의 서로 다른 파트가 공백으로 구분되어 있습니다. 토큰은 base64로 인코딩되어 있습니다. ID 토큰은 선택사항입니다.</br>
    예:</p>
    <pre><code>Authorization=Bearer {access_token} [{id_token}]</pre></code></dd>
  <dt>API 전략</dt>
    <dd><p>API 전략은 요청에 올바른 액세스 토큰이 있는 권한 헤더가 포함될 것으로 예상합니다. 요청에도 ID 토큰이 포함될 수 있지만 필수는 아닙니다. 토큰이 올바르지 않거나 만료된 경우 API 전략에서 다음 HTTP 헤더로 구성된 HTTP 401 오류를 리턴합니다.</p> <pre><code>Www-Authenticate=Bearer scope="{scope}" error="{error}"</code></pre>
    <p>요청이 올바른 토큰을 리턴하는 경우, 제어가 다음 미들웨어에 전달되며 <code>appIdAuthorizationContext</code> 특성이 요청 오브젝트에 삽입됩니다. 이 특성에는 원래 액세스 및 ID 토큰, 일반 JSON 오브젝트로 디코딩된 페이로드 정보가 포함됩니다.</dd>
  <dt>웹 앱 전략</dt>
    <dd>웹 앱 전략에서 인증된 절차를 통해 보호된 리소스에 액세스하려는 시도를 발견하면 사용자의 브라우저 경로를 {{site.data.keyword.appid_short}}에서 제공할 수 있는 인증 페이지로 자동 재지정합니다. 인증에 성공하면 사용자가 웹 앱의 콜백 URL로 리턴됩니다. 웹 앱 전략에서 액세스 및 ID 토큰을 확보한 후 <code>WebAppStrategy.AUTH_CONTEXT</code>의 HTTP 세션에 저장합니다. 앱 데이터베이스에서 액세스 및 ID 토큰을 저장할 것인지 여부는 사용자가 결정합니다.</dd>
  <dt>데이터 분리 및 암호화</dt>
    <dd><p>{{site.data.keyword.appid_short_notm}}는 사용자 프로파일 속성을 저장하고 암호화합니다. 다중 테넌트 서비스로서 모든 테넌트에는 지정된 암호화 키가 있으며 각 테넌트의 사용자 데이터는 해당 테넌트의 키로만 암호화됩니다.</p>
    <p>{{site.data.keyword.appid_short_notm}}는 개인 정보를 저장하기 전에 암호화되었는지 확인합니다.</p></dd>
</dl>

</br>
</br>


## 토큰에 대한 정보
{: #tokens}

사용자가 정상적으로 인증되면 애플리케이션은 {{site.data.keyword.appid_short_notm}}에서 토큰을 받습니다. 이 서비스는 서로 다른 세 가지 유형의 토큰을 사용하여 인증 프로세스를 완료합니다.
{: shortdesc}


**액세스 토큰이 무엇입니까?**

액세스 토큰은 권한을 나타내며 이를 사용하면 {{site.data.keyword.appid_short}}에 의해 설정된 권한 필터로 보호되는 [백엔드 리소스](/docs/services/appid/backend-apps.html)와의 통신이 가능합니다. 토큰은 JOSE(JavaScript Object Signing and Encryption) 스펙을 준수합니다. 이 토큰은 RS256 알고리즘을 사용하는 JSON 웹 키로 서명된 <a href="https://jwt.io/introduction/" target="blank">JSON 웹 토큰 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>으로 형식화됩니다.

토큰 예제:
  ```
Header: {
      "typ": "JOSE",
    "alg": "RS256",
}
Payload: {
      "iss": "appid-oauth.ng.bluemix.net",
      "exp": "1495562664",
      "aud": "a3b87400-f03b-4956-844e-a52103ef26ba",
      "amr": ["facebook"],
      "sub": "de6a17d2-693d-4a43-8ea2-2140afd56a22",
      "iat": "1495559064",
      "tenant": "9781974b-6a1c-46c3-aebf-32b7e9bbbaee",
      "scope": "appid_default appid_readprofile appid_readuserattr appid_writeuserattr",
  ```
  {: screen}

**ID 토큰이 무엇입니까?**

ID 토큰은 인증을 나타내며 사용자에 대한 정보를 포함합니다. 이름, 이메일, 성 및 위치에 대한 정보를 제공합니다. 토큰은 사용자의 이미지에 대한 URL을 리턴할 수도 있습니다. 이 토큰은 RS256 알고리즘을 사용하는 JSON 웹 키로 서명된 <a href="https://jwt.io/introduction/" target="blank">JSON 웹 토큰 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>으로 형식화됩니다.

토큰 예제:
  ```
Header: {
      "typ": "JOSE",
    "alg": "RS256",
}
Payload: {
      "iss": "appid-oauth.ng.bluemix.net",
      "aud": "a3b87400-f03b-4956-844e-a52103ef26ba",
      "exp: "1495562664",
      "tenant": "9781974b-6a1c-46c3-aebf-32b7e9bbbaee",
      "iat": "1495559064",
      "name": "John Smith",
      "email": "js@mail.com",
      "gender", "male",
      "locale": "en",
      "picture": "<URL-to-photo>",
      "sub": "de6a17d2-693d-4a43-8ea2-2140afd56a22",
      "identities": [
          "provider": "facebook"
        "id": "377440159275659"
      ],
    "amr": ["facebook"],
    "oauth_client":{
        "name": "BluemixApp",
      "type": "serverapp",
      "software_id": "cb638f8f-e24b-41d3-b770-23be158dd8e6.2b94e6bb-bac4-4455-8712-a43fa804d5cc.a3b87400-f03b-4956-844e-a52103ef26ba",
      "software_version": "1.0.0",
    }
  }
  ```
  {: screen}

ID 토큰에는 부분적인 사용자 정보만 포함됩니다. ID 제공자에서 제공되는 모든 정보를 확인하려는 경우 [사용자 정보 엔드포인트](/docs/services/appid/predefined.html#api)를 사용할 수 있습니다.

**새로 고치기 토큰이 무엇입니까?**

{{site.data.keyword.appid_short}}의 경우 <a href="http://openid.net/specs/openid-connect-core-1_0.html#RefreshTokens" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>에 정의된 것처럼 재인증 없이 새 액세스 및 ID 토큰을 획득하는 기능을 지원합니다. 새로 고치기 토큰은 사용자가 사인인하기 위해 어떤 조치(예: 인증 정보 제공)도 수행할 필요가 없도록 액세스 토큰을 갱신하기 위해 사용할 수 있습니다. 액세스 토큰과 마찬가지로 새로 고치기 토큰에도 {{site.data.keyword.appid_short_notm}}에서 권한 부여 여부를 판별할 수 있도록 해주는 데이터가 포함되어 있습니다. 하지만 이 토큰은 불투명합니다.

새로 고치기 토큰은 정규 액세스 토큰보다 수명이 더 길기 때문에 액세스 토큰이 만료되더라도 새로 고치기 토큰은 여전히 유효하며 액세스 토큰을 갱신하기 위해 사용할 수 있습니다. {{site.data.keyword.appid_short_notm}}의 새로 고치기 토큰은 1 - 90일 동안 지속되도록 구성할 수 있습니다. 새로 고치기 토큰을 완전히 활용하려면 전체 수명 기간 동안 또는 해당 토큰이 갱신될 때까지 토큰이 지속되도록 하십시오. 새로 고치기 토큰만 사용해서는 사용자가 리소스에 직접 액세스할 수 없으므로 액세스 토큰보다 더 오래 지속되더라도 안전합니다. 우수 사례의 경우 새로 고치기 토큰을 수신한 클라이언트에서 해당 토큰을 안전하게 저장한 후 해당 토큰을 발행한 권한 서버로만 전송해야 합니다.

추가적인 편의성을 위해 {{site.data.keyword.appid_short_notm}}는 액세스 토큰이 갱신될 때 새로 고치기 토큰 및 해당 만기 날짜도 갱신함으로써 현재 새로 고치기 토큰이 만료되기 이전 시점의 활성 상태인 한 사용자가 로그인 상태를 유지할 수 있도록 해줍니다. 다른 한편으로는 새로 고치기 토큰을 사용하면서도 사용자가 주기적으로 로그인하도록 강제하려는 경우 앱에서 사용자가 해당 인증 정보를 입력하여 로그인할 때 리턴된 새로 고치기 토큰만 사용할 수 있습니다. 하지만 <a href="https://tools.ietf.org/html/rfc6749#page-47" target="_blank">Oauth 스펙 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>에서 설명한 것처럼 항상 App ID로부터 수신된 가장 최근의 새로 고치기 토큰을 사용하는 것이 좋습니다.


이러한 토큰을 통해 로그인 프로세스를 간소화할 수 있지만 예를 들어 새로 고치기 토큰이 손상된 것으로 판단되는 경우 언제든지 해당 토큰을 취소할 수 있도록 앱이 토큰에 종속되어서는 안됩니다. 새로 고치기 토큰을 취소해야 하는 경우 새로 고치기 토큰을 취소하는 두 가지 방법이 있습니다. 새로 고치기 토큰이 있는 경우 <a href="https://tools.ietf.org/html/rfc7009#section-2" target="_blank">RFC7009 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>에 따라 해당 토큰을 취소할 수 있습니다. 또는 사용자 ID가 있는 경우 <a href="https://appid-management.ng.bluemix.net/swagger-ui/" target="_blank">관리 API <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 사용하여 새로 고치기 토큰을 취소할 수 있습니다. 관리 API에 액세스하는 방법에 대한 자세한 정보는 [서비스 액세스 관리](iam.html#service-access-management)를 참조하십시오.

새로 고치기 토큰 관련 작업을 수행하는 예제 및 해당 예제를 사용하여 기억하기 기능을 구현하는 방법은 [시작하기 샘플](index.html)을 참조하십시오.


**토큰은 어디에서 제공됩니까?**

토큰은 {{site.data.keyword.appid_short_notm}} OAuth 서버를 통해 발행되며 [JSON 웹 토큰(JWT)](https://jwt.io/introduction/)으로 형식화됩니다. 이 토큰은 RS256 알고리즘을 사용하는 [JSON 웹 키(JWK)](https://tools.ietf.org/html/rfc7517)로 서명되어 있습니다.

**토큰에 포함된 정보는 어떻게 처리됩니까?**

액세스 토큰에는 표준 JWT 청구 세트 및 {{site.data.keyword.appid_short_notm}} 특정 청구 세트(예: 테넌트 ID)가 포함되어 있습니다. ID 토큰에는 사용자 특정 정보가 포함되어 있습니다. 토큰 내의 정보는 [사용자 프로파일](/docs/services/appid/user-profile.html)의 일부인 청구로 저장됩니다.

**토큰을 받는 방법은 무엇입니까?**

토큰은 정상적인 인증 후 앱에서 수신합니다. 이 토큰을 사용하여 사용자 권한 및 인증에 대한 정보를 검색할 수 있습니다. 액세스 토큰은 리소스에 대한 요청을 전송하여 보호된 리소스에 대한 액세스 권한을 받기 위해 사용할 수 있습니다. 요청에서 액세스 토큰은 [전달자 인증 스킴](https://tools.ietf.org/html/rfc6750#page-5)에 설명되어 있습니다. 토큰을 추출하려면 앱에서 헤더를 구문 분석해야 합니다.

요청 예제:

  ```
  GET /resource HTTP/1.1
  Host: server.example.com
  Authorization: Bearer  mF_9.B5f-4.1JqM mF_9.B5f-4.1JqM
  ```
  {: screen}

</br>
</br>
