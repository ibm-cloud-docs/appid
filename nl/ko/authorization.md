---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}

# 권한 및 인증
{: #authorization}

{{site.data.keyword.appid_full}}를 사용하여 사용자는 토큰 및 권한 필터의 레버리지를 활용하여 앱이 보호되도록 보장할 수 있습니다. 사용자가 앱에 대한 권한 부여를 수행하려면 우선 ID 제공자가 해당 ID를 인증해야 합니다.
{: shortdesc}


## 핵심 개념
{: #key-concepts}

다음의 핵심 용어는 서비스에서 권한과 인증 프로세스를 분류하는 방식을 이해하는 데 도움이 될 수 있습니다.

<dl>
  <dt>OAuth 2</dt>
    <dd><a href="https://tools.ietf.org/html/rfc6749" target="_blank">OAuth 2 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>는 앱 권한을 제공하는 데 사용하는 개방형 표준 프로토콜입니다.</dd>
  <dt>OIDC(Open ID Connect)</dt>
    <dd><p><a href="http://openid.net/developers/specs/" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>는 OAuth 2에서 작동하는 인증 계층입니다.</p>
    <p>OIDC 및 {{site.data.keyword.appid_short_notm}}를 함께 사용하는 경우 서비스 신임 정보는 OAuth 엔드포인트를 구성하는 데 도움이 됩니다. SDK를 사용하는 경우 엔드포인트 URL이 자동으로 빌드됩니다. 그러나 서비스 신임 정보를 사용하여 자체적으로 URL을 빌드할 수도 있습니다. 다음 예제와 표에서 URL을 함께 배치하는 방법을 알아볼 수 있습니다.</p>
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
    <dd>서비스에서 세 가지 다른 유형의 토큰을 사용하여 인증을 제공합니다. 액세스 토큰은 권한을 나타내며 이를 사용하면 {{site.data.keyword.appid_short}}에 의해 설정된 권한 필터로 보호되는 [백엔드 리소스](/docs/services/appid/protecting-resources.html)와의 통신이 가능합니다. ID 토큰은 인증을 나타내며 사용자에 대한 정보를 포함합니다. 새로 고치기 토큰은 수명이 확장된 액세스 토큰입니다. 사용자는 새로 고치기 토큰을 사용하여 애플리케이션에서 정보를 기억하도록 허용할 수 있습니다. 이 방식으로 사인인된 상태를 유지할 수 있습니다.
  </dd>
  <dt>권한 헤더</dt>
    <dd><p>{{site.data.keyword.appid_short}}는 <a href="https://tools.ietf.org/html/rfc6750" target="blank">Token Bearer Specification<img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>을 준수하며 HTTP 권한 헤더로 전송된 액세스 및 ID 토큰의 조합을 사용합니다. 권한 헤더에는 세 개의 서로 다른 파트가 공백으로 구분되어 있습니다. 토큰은 base64로 인코딩되어 있습니다. ID 토큰은 선택사항입니다.</br>
    예:</p>
    <pre><code>Authorization=Bearer {access_token} [{id_token}]</pre></code></dd>
  <dt>API 전략</dt>
    <dd><p>API 전략은 요청에 올바른 액세스 토큰이 있는 권한 헤더가 포함될 것으로 예상합니다. 요청에도 ID 토큰이 포함될 수 있지만 필수는 아닙니다. 토큰이 올바르지 않거나 만료된 경우 API 전략에서 다음 HTTP 헤더로 구성된 HTTP 401 오류를 리턴합니다.</p> <pre><code>Www-Authenticate=Bearer scope="{scope}" error="{error}"</code></pre>
    <p>요청이 올바른 토큰을 리턴하는 경우, 제어가 다음 미들웨어에 전달되며 <code>appIdAuthorizationContext</code> 특성이 요청 오브젝트에 삽입됩니다. 이 특성에는 원래 액세스 및 ID 토큰, 일반 JSON 오브젝트로 디코딩된 페이로드 정보가 포함됩니다.</dd>
  <dt>웹 앱 전략</dt>
    <dd>웹 앱 전략에서 인증된 절차를 통해 보호된 자원에 액세스하려는 시도를 발견하면 사용자의 브라우저 경로를 {{site.data.keyword.appid_short}}에서 제공할 수 있는 인증 페이지로 자동 재지정합니다. 인증에 성공하면 사용자가 웹 앱의 콜백 URL로 리턴됩니다. 웹 앱 전략에서 액세스 및 ID 토큰을 확보한 후 <code>WebAppStrategy.AUTH_CONTEXT</code>의 HTTP 세션에 저장합니다. 앱 데이터베이스에서 액세스 및 ID 토큰을 저장할 것인지 여부는 사용자가 결정합니다.</dd>
  <dt>데이터 분리 및 암호화</dt>
    <dd><p>{{site.data.keyword.appid_short_notm}}는 사용자 프로파일 속성을 저장하고 암호화합니다. 다중 테넌트 서비스로서 모든 테넌트에는 지정된 암호화 키가 있으며 각 테넌트의 사용자 데이터는 해당 테넌트의 키로만 암호화됩니다.</p>
    <p>{{site.data.keyword.appid_short_notm}}는 개인 정보를 저장하기 전에 암호화되었는지 확인합니다.</p></dd>
</dl>

</br>

## 프로세스 작동 방식
{: #process}

앱을 코딩할 때 가장 큰 문제 중 하나는 보안입니다. 올바른 액세스 권한이 있는 사용자만 앱을 사용할 수 있도록 보장하는 방법은 무엇입니까? 권한 프로세스를 사용합니다. 대부분의 프로세스에서는 권한 부여와 인증이 함께 결합되어 있으므로 보안 정책과 ID 제공자의 변경이 복잡해질 수 있습니다. {{site.data.keyword.appid_short}}에서는 권한 부여와 인증이 개별 프로세스입니다.
{: shortdesc}

Facebook과 같은 소셜 ID 제공자를 구성할 때 [Authorization Grant flow](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html)를 사용하여 로그인 위젯을 호출합니다. 클라우드 디렉토리를 ID 제공자로 사용하면 [Resource Owner Password Credentials flow](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html)를 사용하여 액세스와 ID 토큰을 제공합니다.

![식별된 사용자가 되기 위한 경로.](/images/authenticationtrail.png)

사인인을 선택하는 경우, 해당 사용자는 식별된 사용자가 됩니다. ID 제공자에서 액세스 및 ID 토큰을 사용자에 대한 정보가 포함된 {{site.data.keyword.appid_short}}에 리턴합니다. 이 서비스에서는 제공된 토큰을 사용하고 사용자가 앱에 액세스하는 데 적절한 권한이 있는지 판별합니다. 토큰의 유효성이 검증되면 서비스가 사용자 액세스 권한을 부여합니다. 인증 정보는 권한 부여된 후에 사용자의 레코드와 연관됩니다. 동일한 ID로 인증하는 클라이언트에서 레코드와 그 속성에 다시 액세스할 수 있습니다.

### 점진적 인증

{{site.data.keyword.appid_short_notm}}에서는 익명의 사용자가 식별된 사용자가 되도록 선택할 수 있습니다.

어떻게 수행됩니까?

사용자가 즉시 사인인하지 않도록 선택하면 익명의 사용자로 간주됩니다. 예를 들어, 사용자는 사인인하지 않고 즉시 장바구니에 항목 추가를 시작할 수 있습니다. 익명의 사용자인 경우, {{site.data.keyword.appid_short_notm}}는 임시 사용자 레코드를 작성하고 익명 액세스 및 ID 토큰을 리턴하는 OAuth 로그인 API를 호출합니다. 해당 토큰을 사용하여 앱은 사용자 레코드에 저장된 속성을 작성, 읽기, 업데이트, 삭제할 수 있습니다.

![익명으로 시작할 때 식별된 사용자가 되기 위한 경로.](/images/anon-authenticationtrail.png)

익명의 사용자가 사인인하면 해당 액세스 토큰이 로그인 API에 전달됩니다. 서비스가 ID 제공자로 호출을 인증합니다. 서비스는 익명 레코드를 찾기 위해 액세스 토큰을 사용하고 ID를 익명 레코드에 연결합니다. 새 액세스 및 ID 토큰에는 ID 제공자가 공유한 공용 정보가 포함됩니다. 사용자가 식별된 후에 익명 토큰은 무효화됩니다. 그러나 새 액세스 토큰으로 속성에 액세스할 수 있으므로 사용자가 계속해서 속성에 액세스할 수 있습니다.

다른 사용자에게 아직 지정되지 않은 경우에만 익명 레코드에 ID를 지정할 수 있습니다.
{: tip}

ID가 다른 {{site.data.keyword.appid_short_notm}} 사용자와 이미 연관되어 있는 경우, 토큰에 그 사용자 레코드의 정보가 포함되며 속성에 대한 액세스를 제공합니다. 이전 익명 사용자 속성은 새 토큰을 통해 액세스할 수 없습니다. 토큰이 만료될 때까지는 익명 액세스 토큰을 통해 정보에 계속 액세스할 수 있습니다. 개발 중에 익명 속성을 알려진 사용자에 병합하는 방식을 선택할 수 있습니다.
