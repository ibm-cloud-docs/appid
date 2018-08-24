---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}

# 엔터프라이즈 ID 제공자 구성
{: #enterprise}

이미 내부 시스템에 대해 사용자를 인증하는 인증 방법과 기존 사용자 저장소가 있으면 엔터프라이즈 ID 제공자를 사용하도록 {{site.data.keyword.appid_full}} 서비스를 구성할 수 있습니다.
{: shortdesc}

## SAML 알아보기
{: #saml}

SAML은 사용자 ID를 어설션하는 ID 제공자 및 사용자 ID 정보를 이용하는 서비스 제공자 간의 인증 및 권한 부여 데이터를 교환하기 위한 개방형 표준입니다.
{: shortdesc}

작동 방식

{{site.data.keyword.appid_short_notm}}는 서비스 제공자로서 작동하며 Active Directory Federation Services 등의 써드파티 제공자에 대한 싱글 사인온(SSO) 로그인을 시작합니다. <a href="http://saml.xml.org/saml-specifications" target="_blank">SAML <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a> 프로토콜은 다양한 프로파일 및 바인드 옵션을 지원합니다. {{site.data.keyword.appid_short_notm}}는 HTTP POST 바인딩과 함께 웹 브라우저 SSO 프로파일을 지원합니다.

### SAML 어설션 및 ID 토큰 클레임

SAML 어설션은 하나 이상의 명령문이 포함된 정보의 패키지입니다. 어설션에는 권한 부여 의사결정이 포함되어 있으며, 사용자에 대한 ID 정보가 포함될 수 있습니다.

사용자가 ID 제공자로 사인인하는 경우에 해당 제공자는 어설션을 {{site.data.keyword.appid_short_notm}}에 전송합니다. {{site.data.keyword.appid_short_notm}}는 SAML 어설션에서 리턴된 사용자 ID 정보를 OIDC 토큰 청구로서 앱에 전파합니다. SAML 속성은 ID 토큰에 추가되는 다음의 OIDC 청구 중 하나에 대응되어야 합니다.

다음의 청구가 추가될 수 있습니다.
* `name`
* `email`
* `locale`
* `picture`

표준 이름에 대응되지 않는 나머지 SAML 속성 요소는 무시됩니다. 제공자 측에서 해당 값 중 하나 이상이 변경된 경우 사용자가 다시 로그인해야만 새 값을 사용할 수 있습니다.

## 외부 SAML ID 제공자로 작동하도록 앱 구성
{: #configuring-saml}

SAML(Security Assertion Markup Language) ID 제공자를 사용하도록 {{site.data.keyword.appid_short_notm}} 서비스를 구성할 수 있습니다.
{: shortdesc}

특정 SAML ID 제공자를 사용하는 방법에 대한 단계는 [Ping One ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-ping-one/), [Azure Active Directory ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-azure-active-directory/) 또는 [Active Directory Federation Service ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-active-directory-federation-service/)를 통한 {{site.data.keyword.appid_short_notm}} 설정에 대한 블로그 게시물을 확인하십시오.
{: tip}

### ID 제공자에 메타데이터 제공

앱을 구성하려면 SAML 호환 가능 ID 제공자에 정보를 제공해야 합니다. 정보는 신뢰 구축에 사용되는 구성 데이터도 포함된 메타데이터 XML 파일을 통해 교환됩니다.

1. {{site.data.keyword.appid_short_notm}} 대시보드의 **관리** 탭에서 **SAML 2.0**을 **켜기**로 설정하십시오. 그리고 **편집**을 클릭하여 SAML 설정을 구성하십시오.
2. **SAML 메타데이터 파일 다운로드**를 클릭하십시오. ID 제공자는 파일에서 다음 정보를 예상합니다.
  <table>
    <tr>
      <th> 변수 </th>
      <th> 설명 </th>
    </tr>
    <tr>
      <td><code>EntityID</code></td>
      <td>{{site.data.keyword.appid_short_notm}}에서 SAML 요청을 발행했음을 ID 제공자가 알 수 있도록 허용하는 ID입니다.</td>
    </tr>
    <tr>
      <td><code>Location URL</code></td>
      <td>사용자 인증에 성공한 후에 ID 제공자가 SAML 어설션을 전송하는 위치입니다.</td>
    </tr>
    <tr>
      <td><code>Binding</code></td>
      <td>ID 제공자가 SAML 응답을 전송해야 하는 방법에 대한 지시사항입니다.</td>
    </tr>
    <tr>
      <td><code>NameID Format</code></td>
      <td>어설션의 주제에서 전송해야 하는 ID 형식을 ID 제공자가 파악하는 방법입니다. {{site.data.keyword.appid_short_notm}}가 사용자를 식별하는 방법입니다.</td>
    </tr>
    <tr>
      <td><code>WantAssertionsSigned</code></td>
      <td>어설션에 서명해야 하는지 여부를 파악하기 위해 ID 제공자가 확인하는 방법입니다. 서비스는 어설션의 서명을 예상하지만 암호화된 어설션을 지원하지는 않습니다.</td>
    </tr>
  </table>

3. ID 제공자에 데이터를 제공하십시오. ID 제공자가 메타데이터 파일의 업로드를 지원하면 이를 수행할 수 있습니다. 그렇지 않으면 수동으로 특성을 구성하십시오. 모든 ID 제공자가 동일한 특성을 사용하지는 않으므로, 이를 모두 사용하지 않아도 상관 없습니다.

특성 이름은 ID 제공자 간에 서로 다를 수 있습니다.
{: tip}

### {{site.data.keyword.appid_short_notm}}에 메타데이터 제공

ID 제공자로부터 데이터를 가져오고 이를 {{site.data.keyword.appid_short_notm}}에 제공해야 합니다.

1. {{site.data.keyword.appid_short_notm}} 대시보드의 **SAML 2.0** 탭으로 이동하십시오. **SAML IdP의 메타데이터 제공** 섹션에서 ID 제공자로부터 가져온 다음의 메타데이터를 입력하십시오.
  <table>
    <tr>
      <th> 변수 </th>
      <th> 설명 </th>
    </tr>
    <tr>
      <td><code>Sign-in URL</code></td>
      <td>인증을 위해 사용자가 경로 재지정되는 URL입니다. 이는 SAML ID 제공자에 의해 호스팅됩니다.</td>
    </tr>
    <tr>
      <td><code>Entity ID</code></td>
      <td>SAML ID 제공자의 글로벌한 고유 이름입니다.</td>
    </tr>
    <tr>
      <td><code>Signing certificate</code></td>
      <td>SAML ID 제공자가 발행한 인증서입니다. 이는 SAML 어설션을 서명하고 유효성 검증하는 데 사용됩니다. 모든 제공자가 서로 다르지만, ID 제공자로부터 서명 인증서의 다운로드가 가능합니다. 인증서는 <code>.pem</code> 형식이어야 합니다.</td>
    </tr>
  </table>

2. 선택사항: 기본 인증서에서 서명 유효성 검증이 실패하는 경우에 사용되는 **보조 인증서**를 제공하십시오. 서명 키가 동일하게 유지되면 {{site.data.keyword.appid_short_notm}}는 만료된 인증서에 대해 인증을 차단하지 않습니다.

3. **제공자 이름**을 업데이트하고 **저장**을 클릭하십시오. 기본 이름은 SAML입니다.


### 구성 테스트

SAML ID 제공자 및 {{site.data.keyword.appid_short_notm}} 간의 구성을 테스트할 수 있습니다.

1. 구성을 저장했는지 확인하십시오.
2. {{site.data.keyword.appid_short_notm}} 대시보드의 **SAML 2.0** 탭으로 이동하고 **테스트**를 클릭하십시오. 새 탭이 열립니다.
3. ID 제공자가 이미 인증한 사용자로 로그인하십시오.
4. 양식이 완료되면 다른 페이지로 경로 재지정됩니다.
  * 성공적 인증: {{site.data.keyword.appid_short_notm}} 및 ID 제공자 간의 연결이 정상적으로 작동 중입니다. 올바른 [액세스 및 ID 토큰](/docs/services/appid/authorization.html#key-concepts)이 페이지에 표시됩니다.
  * 실패한 인증: 연결이 끊겼습니다. 오류 및 SAML 응답 XML 파일이 페이지에 표시됩니다.
