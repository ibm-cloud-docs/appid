---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-10"

keywords: authentication, authorization, identity, app security, secure, development, idp, troubleshooting, redirected, validation

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
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}

# ID 제공자 구성
{: #troubleshooting-idp}

{{site.data.keyword.appid_full}}에서 작동하도록 ID 제공자를 구성할 때 문제점이 발생하는 경우 문제점을 해결하고 도움을 받기 위해 다음과 같은 기술을 고려하십시오.
{: shortdesc}


## 사용자가 ID 제공자로 경로 재지정되지 않음
{: #ts-saml-redirect}

{: tsSymptoms}
사용자가 애플리케이션에 사인인하려고 시도하지만 프롬프트가 표시될 때 사인인 페이지가 표시되지 않습니다.

{: tsCauses}
ID 제공자는 여러 이유로 인해 실패할 수 있습니다.

* 구성된 경로 재지정 URL이 올바르지 않습니다.
* ID 제공자가 인증 요청을 인식하지 않습니다.
* ID 제공자가 HTTP-POST 바인딩을 예상합니다.
* ID 제공자가 서명된 authnRequest를 예상합니다.

{: tsResolve}
다음 솔루션 중 일부를 시도할 수 있습니다.

* 사인인 URL을 업데이트하십시오. 이 URL은 authnRequest의 일부로서 전송되며 정확해야 합니다.
* {{site.data.keyword.appid_short_notm}} 메타데이터가 ID 제공자 설정에서 올바르게 설정되었는지 확인합니다.
* HTTP 경로 재지정에서 authnRequest를 승인하도록 ID 제공자를 구성합니다.
* {{site.data.keyword.appid_short_notm}}가 서명 authnRequest를 지원하지 않습니다.

이 중에서 어떤 솔루션도 적용되지 않으면 연결에 문제가 있을 수 있습니다.
{: tip}


## 일반적인 SAML 문제
{: #ts-common-saml}

다음 표에서 SAML 관련 작업을 수행할 때 발생하는 가장 일반적인 문제에 대한 설명 및 해결책을 검토하십시오.

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
      <td><code>Invalid attribute without name. Contact your identity provider administrator.</code></td>
      <td>정의된 값이 없는 <code>&lt;saml:Attribute&gt;</code>가 있습니다. ID 제공자 관리자에게 문의하십시오.</td>
    </tr>
    <tr>
      <td><code>SAML response body must contain the RelayState parameter.</code></td>
      <td>SAML 응답 본문에 매개변수가 포함되지 않았습니다. {{site.data.keyword.appid_short_notm}}는 요청의 일부로서 ID 제공자에게 매개변수를 제공하며, 정확한 매개변수가 응답에서 리턴되어야 합니다. 매개변수가 수정된 경우에는 ID 제공자 관리자에 문의할 수 있습니다. </td>
    </tr>
    <tr>
      <td><code>SAML Configuration must have certificates, entityID and signInUrl of the IdP.</code></td>
      <td>SAML ID 제공자가 <a href="/docs/services/appid?topic=appid-enterprise#enterprise" target="_blank">올바르게 구성</a>되지 않았습니다. 구성을 유효성 검증하십시오.</td>
    </tr>
    <tr>
      <td><code>Error in assertion validation. SAML Assertion signature check failed! Certificate .. may be invalid.</code></td>
      <td>올바른 서명과 다이제스트가 어설션에 포함되어야 합니다. 서명은 SAML 구성에서 제공되는 인증서와 연관된 개인 키를 사용하여 작성해야 하며, 보조 또는 기본 키를 사용할 수 있습니다. <strong>참고</strong>: {{site.data.keyword.appid_short_notm}}는 암호화된 어설션을 지원하지 않습니다. ID 제공자가 SAML 어설션을 암호화하는 경우 암호화를 사용 안함으로 설정하십시오.</td>
    </tr>
  </tbody>
</table>



## SAML 응답 유효성 검증 오류
{: #ts-saml-response}

{{site.data.keyword.appid_short_notm}}의 경우 어설션에 대한 다음과 같은 유효성 요구사항이 적용됩니다. 별도로 지정되지 않는 한 모든 속성이 필수 SAML 응답 XML 노드입니다.
{: shortdesc}


<table summary="모든 행은 왼쪽에서 오른쪽으로 읽어야 합니다. 1열에는 응답 요소가 있고 2열에는 설명이 있습니다.">
  <thead>
    <th>응답 요소</th>
    <th>설명</th>
  </thead>
  <tbody>
    <tr>
      <td><code>samlp:Response</code></td>
      <td>이 응답 요소는 응답 XML에 반드시 포함되어야 합니다.</td>
    </tr>
    <tr>
      <td><code>SAML version</code></td>
      <td>{{site.data.keyword.appid_short_notm}}의 경우 <code>SAML 버전 2.0</code>만 허용됩니다.</td>
    </tr>
    <tr>
      <td><code>InResponseTo</code></td>
      <td>{{site.data.keyword.appid_short_notm}}는 어설션에서 리턴되는 응답 요소인 <code>InResponseTo</code>가 SALM 요청의 저장된 요청 ID와 일치하는지 확인합니다.</td>
    </tr>
    <tr>
      <td><code>saml:issuer</code></td>
      <td>어설션에서 지정된 발행자가 {{site.data.keyword.appid_short_notm}} ID 제공자 구성에서 지정된 발행자와 일치해야 합니다.</td>
    </tr>
    <tr>
      <td><code>ds:Signature</code></td>
      <td>올바른 서명과 다이제스트가 어설션에 포함되어야 합니다. 서명은 SAML 구성에서 제공되는 인증서와 연관된 개인 키를 사용하여 작성해야 합니다. 다이제스트는 지정된 <code>CanonicalizationMethod</code> 및 <code>Transforms</code>를 사용하여 유효성 검증합니다. <strong>참고</strong>: {{site.data.keyword.appid_short_notm}}는 인증서 만기를 유효성 검증하지 않습니다. 인증서 관리를 지원하기 위해 [인증서 관리자](/docs/services/certificate-manager?topic=certificate-manager-getting-started#getting-started)를 사용해 보십시오.</td>
    </tr>
    <tr>
      <td><code>saml:subject</code></td>
      <td>어설션의 제목 또는 <code>name_id</code>는 사용자의 연합 이메일이어야 합니다.</td>
    </tr>
    <tr>
      <td><code>saml:AttributeStatement</code></td>
      <td>특정 속성이 인증된 특정 사용자와 연관되어 있음을 나타냅니다.</td>
    </tr>
    <tr>
      <td><code>saml:Conditions</code></td>
      <td><strong>선택사항</strong>: 어설션에 조건 명령문이 포함되는 경우 올바른 시간소인도 포함되어야 합니다. {{site.data.keyword.appid_short_notm}}는 어설션에서 지정된 유효 기간을 준수합니다. 확인을 위해 이 서비스는 정의되어 있고 유효한 <code>NotBefore</code> 및 <code>NotOnOrAfter</code> 제한조건을 검색합니다.</td>
    </tr>
  </tbody>
</table>

{{site.data.keyword.appid_short_notm}}는 암호화된 어설션을 지원하지 않습니다. ID 제공자가 어설션을 암호화하도록 설정된 경우 암호화를 사용 안함으로 설정하십시오. 어설션은 암호화되지 않은 형식이어야 합니다.
{: tip}
