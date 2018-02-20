---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-01"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# 권한 및 인증
{: authorization}

{{site.data.keyword.appid_full}}를 사용하면 토큰 및 권한 필터를 활용하여 앱이 보호되는지 확인할 수 있습니다. ID 제공자가 사용자의 ID를 인증해야 사용자가 권한을 부여할 수 있습니다.
{: shortdesc}


## 핵심 개념
{: key-concepts}

서비스에서 권한과 인증 프로세스를 분류하는 방식을 확실히 이해하려면 몇 가지 핵심 개념을 이해해야 합니다.

<dl>
  <dt>OAuth 2</dt>
    <dd><a href="https://tools.ietf.org/html/rfc6749" target="_blank">OAuth 2 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>는 앱 권한을 제공하는 데 사용하는 개방형 표준 프로토콜입니다.</dd>
  <dt>OIDC(Open ID Connect)</dt>
    <dd><a href="http://openid.net/developers/specs/" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>는 OAuth 2에서 작동하는 인증 계층입니다.</dd>
  <dt>액세스 토큰</dt>
    <dd><p>액세스 토큰은 권한을 나타내며 해당 토큰을 사용하면 {{site.data.keyword.appid_short}}를 통해 설정한 권한 필터로 보호되는 [백엔드 리소스](/docs/services/appid/protecting-resources.html)와의 통신이 가능합니다. 토큰은 JOSE(JavaScript Object Signing and Encryption) 스펙을 준수합니다. 토큰은 <a href="https://jwt.io/introduction/" target="blank">JSON Web Tokens <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>로 형식화됩니다.</br>
    예:</p>
    <pre><code>Header: {
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
    </code></pre></dd>
  <dt>ID 토큰</dt>
    <dd><p>ID 토큰은 인증을 나타내며 사용자에 대한 정보를 포함합니다. 이름, 이메일, 성 및 위치에 대한 정보를 제공합니다. 토큰은 사용자의 이미지에 대한 URL을 리턴할 수도 있습니다.</br>
    예:</p>
    <pre><code>Header: {
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
    </pre></code></dd>
  <dt>권한 헤더</dt>
    <dd><p>{{site.data.keyword.appid_short}}는 <a href="https://tools.ietf.org/html/rfc6750" target="blank">토큰 전달자 사양 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>을 준수하며 HTTP 권한 헤더로 전송된 액세스 및 ID 토큰의 조합을 사용합니다. 권한 헤더에는 세 개의 서로 다른 파트가 공백으로 구분되어 있습니다. 토큰은 base64로 인코딩되어 있습니다. ID 토큰은 선택사항입니다.</br>
    예:</p>
    <pre><code>Authorization=Bearer {access_token} [{id_token}]</pre></code></dd>
  <dt>API 전략</dt>
    <dd><p>API 전략은 요청에 올바른 액세스 토큰이 있는 권한 헤더가 포함될 것으로 예상합니다. 요청에도 ID 토큰이 포함될 수 있지만 필수는 아닙니다. 토큰이 올바르지 않거나 만료된 경우 API 전략에서 다음 HTTP 헤더로 구성된 HTTP 401 오류를 리턴합니다.</p> <pre><code>Www-Authenticate=Bearer scope="{scope}" error="{error}"</code></pre>
    <p>요청이 올바른 토큰을 리턴하는 경우, 제어가 다음 미들웨어에 전달되며 <code>appIdAuthorizationContext</code> 특성이 요청 오브젝트에 삽입됩니다. 이 특성에는 원래 액세스 및 ID 토큰, 일반 JSON 오브젝트로 디코딩된 페이로드 정보가 포함됩니다.</dd>
  <dt>웹 앱 전략</dt>
    <dd>웹 앱 전략에서 인증된 절차를 통해 보호된 자원에 액세스하려는 시도를 발견하면 사용자의 브라우저 경로를 {{site.data.keyword.appid_short}}에서 제공할 수 있는 인증 페이지로 자동 재지정합니다. 인증에 성공하면 사용자가 웹 앱의 콜백 URL로 리턴됩니다. 웹 앱 전략에서 액세스 및 ID 토큰을 확보한 후 <code>WebAppStrategy.AUTH_CONTEXT</code>의 HTTP 세션에 저장합니다. 앱 데이터베이스에서 액세스 및 ID 토큰을 저장할 것인지 여부는 사용자가 결정합니다.</dd>
</dl>

</br>

## 프로세스 작동 방식
{: #process}

앱을 코딩할 때 가장 큰 문제 중 하나는 보안입니다. 올바른 액세스 권한이 있는 사용자만 앱을 사용하는지 확인할 수 있는 방법은 무엇입니까? 권한 프로세스를 사용합니다. 대부분의 애플리케이션에서는 권한과 인증 프로세스가 결합됩니다. 보안 정책과 ID 제공자를 변경하는 작업은 복잡합니다. {{site.data.keyword.appid_short}}에서는 권한 부여와 인증이 개별 프로세스입니다.
{: shortdesc}

Facebook과 같은 소셜 ID 제공자를 구성할 때 [Oauth2 권한 부여 플로우](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html)를 사용하여 로그인 위젯을 호출합니다. 클라우드 디렉토리를 ID 제공자로 사용하면 [리소스 소유자 비밀번호 비밀번호 신임 정보 플로우](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html)를 사용하여 액세스와 ID 토큰을 제공합니다.

![식별된 사용자가 되기 위한 경로.](/images/authenticationtrail.png)

사용자가 사인인하도록 선택하면 해당 사용자는 식별된 사용자가 됩니다. 사인인할 때 사용한 ID 제공자에서 사용자에 대한 정보를 얻습니다. ID 제공자에서 액세스 및 ID 토큰을 사용자에 대한 정보가 포함된 {{site.data.keyword.appid_short}}에 리턴합니다. 이 서비스에서는 제공된 토큰을 사용하고 사용자가 앱에 액세스하는 데 적절한 권한이 있는지 판별합니다. 토큰의 유효성이 검증되면 서비스에서 사용자에게 액세스 권한을 부여합니다. 사용자에게 권한이 부여되고 나면 인증 정보가 사용자 레코드와 연관됩니다. 동일한 ID로 인증하는 클라이언트에서 레코드와 그 속성에 다시 액세스할 수 있습니다.

### 점진적 인증

{{site.data.keyword.appid_short_notm}}에서는 익명의 사용자가 식별된 사용자가 되도록 선택할 수 있습니다.

어떻게 수행됩니까?

사용자가 즉시 사인인하지 않도록 선택하면 익명의 사용자로 간주됩니다. 예를 들어 사용자가 사인인하지 않고 장바구니에 즉시 항목을 추가하기 시작할 수 있습니다. {{site.data.keyword.appid_short_notm}}에서는 익명의 사용자에 대해 임시 사용자 레코드를 작성하고 익명 액세스 및 ID 토큰을 리턴하는 OAuth 로그인 API를 호출합니다. 해당 토큰을 사용하여 앱은 사용자 레코드에 저장된 속성을 작성, 읽기, 업데이트, 삭제할 수 있습니다.

![익명으로 시작할 때 식별된 사용자가 되기 위한 경로.](/images/anon-authenticationtrail.png)

익명의 사용자가 사인인하면 익명 액세스 토큰이 로그인 API에 전달됩니다. 서비스가 ID 제공자로 호출을 인증합니다. 서비스는 익명 레코드를 찾기 위해 액세스 토큰을 사용하고 ID를 익명 레코드에 연결합니다. 새 액세스 및 ID 토큰에는 ID 제공자가 공유한 공용 정보가 포함됩니다. 사용자가 식별된 후 익명 토큰은 올바르지 않은 상태가 됩니다. 그러나 새 액세스 토큰으로 속성에 액세스할 수 있으므로 사용자가 계속해서 속성에 액세스할 수 있습니다.

**참고**: ID가 다른 사용자에게 아직 지정되지 않은 경우 익명 레코드에만 ID를 지정할 수 있습니다. ID가 다른 {{site.data.keyword.appid_short_notm}} 사용자와 이미 연관되어 있는 경우, 토큰에 그 사용자 레코드의 정보가 포함되며 속성에 대한 액세스를 제공합니다. 이전 익명 사용자 속성은 새 토큰을 통해 액세스할 수 없습니다. 토큰이 만료될 때까지는 익명 액세스 토큰을 통해 정보에 계속 액세스할 수 있습니다. 개발 중에 익명 속성을 알려진 사용자에 병합하는 방식을 선택할 수 있습니다.
