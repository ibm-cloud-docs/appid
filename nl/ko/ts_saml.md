---

copyright:
  years: 2017, 2018
lastupdated: "2018-06-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tip: .tip}

# ID 제공자 구성
{: #troubleshooting-idp}

{{site.data.keyword.appid_full}}에 대해 작업하도록 ID 제공자를 구성하는 중에 문제점이 발생하는 경우 문제점을 해결하고 도움을 받기 위한 다음 기술을 고려하십시오.
{: shortdesc}


## 사인인 이후 앱으로 경로 재지정 없음
{: #signin-fail}

{: tsSymptoms}
사용자가 ID 제공자의 사인인 페이지를 통해 애플리케이션에 사인인하지만 아무 일도 발생하지 않거나 사인인에 실패합니다.

{: tsCauses}
다음 이유로 인해 사인인에 실패할 수 있습니다.

* 경로 재지정 URL이 [화이트리스트](identity-providers.html#redirect)에 제대로 추가되지 않았습니다.
* 사용자에게 권한이 부여되지 않습니다.
* 사용자가 잘못된 신임 정보로 사인인을 시도했습니다.

{: tsResolve}
경로 재지정이 발생하려면 다음을 수행하십시오.

* 경로 재지정 URL이 올바른지 확인하십시오. 경로 재지정이 발생하려면 이 URL이 정확해야 합니다.
* 사용자가 올바른 신임 정보로 사인인했는지 확인하십시오.
* 신임 정보가 ID 제공자 사용자 설정에서 구성되었는지 확인하십시오.


## SAML 관련 작업 시의 일반적인 문제
{: #common-saml}

SAML 관련 작업 시에 발생하는 가장 일반적인 문제에 대한 설명과 해결책은 다음 표를 살펴보십시오.

<table summary="표의 모든 행은 왼쪽에서 오른쪽으로 읽어야 합니다. 클러스터 단계는 1열에 있으며 설명은 2열에 있습니다. ">
  <thead>
    <th>메시지</th>
    <th>설명</th>
  </thead>
  <tbody>
    <tr>
      <td><code>Could not parse assertion xml.</code></td>
      <td>SAML의 응답 형식이 올바르지 않습니다.</td>
    </tr>
    <tr>
      <td><code>Invalid attribute without name. ID 제공자 관리자에게 문의하십시오. </code></td>
      <td>정의된 값이 없는 <code>&lt;saml:Attribute&gt;</code>가 있습니다. ID 제공자 관리자에게 문의하십시오.</td>
    </tr>
    <tr>
      <td><code>SAML response body must contain RelayState.</code></td>
      <td>RelayState 매개변수가 SAML 응답 본문에 포함되지 않았습니다. {{site.data.keyword.appid_short_notm}}는 요청의 일부로서 ID 제공자에게 매개변수를 제공하며, 정확한 매개변수가 응답에서 리턴되어야 합니다. 매개변수가 수정된 경우에는 ID 제공자 관리자에 문의할 수 있습니다. </td>
    </tr>
    <tr>
      <td><code>SAML Configuration must have certificates, entityID and signInUrl of the IdP.</code></td>
      <td>SAML ID 제공자가 올바르게 구성되지 않았습니다. 구성을 유효성 검증하십시오. 도움말은 <a href="enterprise.html#configuring-saml" target="_blank">외부 SAML ID 제공자로 작동하도록 앱 구성</a>을 참조하십시오.</td>
    </tr>
    <tr>
      <td><code>Error in assertion validation. SAML Assertion signature check failed! Certificate .. may be invalid.</code></td>
      <td>올바른 서명과 다이제스트가 어설션에 포함되어야 합니다. 서명은 SAML 구성에서 제공된 인증서와 연관된 개인 키를 사용하여 작성되어야 합니다. 2차 또는 1차가 사용될 수 있습니다. <strong>참고</strong>: {{site.data.keyword.appid_short_notm}}는 암호화된 어설션을 지원하지 않습니다. ID 제공자가 SAML 어설션에 대해 이를 수행하는 경우에는 암호화를 사용하지 마십시오.</td>
    </tr>
  </tbody>
</table>


## ID 제공자에 대한 경로 재지정이 없음
{: #saml-redirect}

{: tsSymptoms}
사용자가 애플리케이션에 사인인을 시도하지만 프롬프트가 표시될 때 사인인 페이지가 표시되지 않습니다.

{: tsCauses}
ID 제공자는 여러 이유로 인해 실패할 수 있습니다.

* 구성된 경로 재지정 URL이 올바르지 않습니다.
* ID 제공자가 인증 요청을 인식하지 않습니다.
* ID 제공자가 HTTP-POST 바인딩을 예상합니다.
* ID 제공자가 서명된 authnRequest를 예상합니다.

{: tsResolve}
다음 솔루션 중 일부를 시도할 수 있습니다.

* 사인인 URL을 업데이트합니다. 이 URL은 authnRequest의 일부로서 전송되며 정확해야 합니다.
* {{site.data.keyword.appid_short_notm}} 메타데이터가 ID 제공자 설정에서 올바르게 설정되었는지 확인합니다.
* HTTP 경로 재지정에서 authnRequest를 승인하도록 ID 제공자를 구성합니다.
* {{site.data.keyword.appid_short_notm}}가 서명 authnRequest를 지원하지 않습니다.

이 중에서 어떤 솔루션도 적용되지 않으면 연결에 문제가 있을 수 있습니다. {: tip}

## 속성이 잘못된 값을 표시함
{: #saml-attribute}

{: tsSymptoms}
속성 값이 사용자 프로파일에 존재하지만 올바른 속성에 연결되지 않았습니다.

{: tsCauses}
사용자 프로파일 속성이 올바르게 맵핑되지 않았습니다.

{: tsResolve}
ID 제공자 설정의 속성을 맵핑하십시오. {{site.data.keyword.appid_short_notm}}는 다음의 속성을 예상합니다.
* `name`
* `email`
* `locale`
* `picture`


