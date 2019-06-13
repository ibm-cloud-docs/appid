---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-20"

keywords: authentication, authorization, identity, app security, secure, custom, service provider, identity provider, enterprise, assertions

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

# SAML
{: #enterprise}

SAML 기반 ID 제공자가 있는 경우, 서드파티 제공자에 대한 싱글 사인온(SSO) 로그인을 시작하는 서비스 제공자 역할을 하도록 {{site.data.keyword.appid_short_notm}}를 구성할 수 있습니다. 사인인 플로우 중 사용자는 쉽게 인증받고 {{site.data.keyword.appid_short_notm}} 보안 토큰을 얻을 수 있으므로 자신의 앱과 보호된 API에 액세스할 수 있습니다.
{: shortdesc}

 
특정 ID 제공자에서 작동합니까? [Ping One ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/cloud/blog/setting-ibm-cloud-app-id-ping-one), [Azure Active Directory ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/cloud/blog/setting-ibm-cloud-app-id-azure-active-directory) 또는 [Active Directory Federation Service ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/cloud/blog/setting-ibm-cloud-app-id-active-directory-federation-service)를 사용한 {{site.data.keyword.appid_short_notm}} 설정에 대한 블로그 게시물 중 하나를 확인하십시오.
{: tip}


## SAML 이해
{: #saml-understanding}

SAML(Security Assertion Markup Language)은 사용자 ID를 어설션하는 ID 제공자와 사용자 ID 정보를 이용하는 서비스 제공자 간의 인증 및 권한 데이터를 교환하기 위한 개방형 표준입니다.
{: shortdesc}

<a href="http://saml.xml.org/saml-specifications" target="blank">SAML <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a> 프로토콜은 다양한 프로파일 및 바인드 옵션을 지원합니다. {{site.data.keyword.appid_short_notm}}는 HTTP POST 바인딩과 함께 웹 브라우저 SSO 프로파일을 지원합니다.

### 플로우의 기술적 기반은 무엇입니까? 
{: #saml-tech-basis}

SAML 2.0은 인증 및 권한 부여 표준에 대한 가장 대표적인 프레임워크 중 하나로서, 서비스 제공자({{site.data.keyword.appid_short_notm}})와 ID 제공자 간 XML 기반 프로토콜입니다. ID 제공자가 사용자를 인증하면 사용자에 대한 어설션 또는 명령문이 포함된 SAML 토큰이 작성됩니다. 명령문에는 다음이 포함될 수 있습니다. 

- 사용자 인증 방법과 같은 인증 정보 - 비밀번호, MFA 등...
- 사용자와 연관된 속성 - 사용자가 속한 그룹
- 사용자가 특정 리소스에 대해 특정 조치를 수행할 수 있는지 여부를 기술하는 권한 부여 결정

어설션이 {{site.data.keyword.appid_short_notm}}에 리턴되면 서비스가 사용자 ID를 연합하고 해당 토큰이 생성됩니다. SAML 어설션이 다음 OIDC 청구 중 하나에 해당하는 경우 자동으로 ID 토큰에 추가됩니다.  제공자 측에서 해당 값 중 하나 이상이 변경되는 경우 사용자가 다시 로그인한 후에만 새 값을 사용할 수 있습니다.

 * `name`
 * `email`
 * `locale`
 * `picture`

표준 이름에 해당되지 않는 어설션은 기본적으로 무시되지만 SAML 제공자가 다른 어설션을 리턴하는 경우 사용자가 로그인할 때 해당 정보를 얻을 수 있습니다. 사용할 어설션의 배열을 작성하여 [토큰에 정보를 삽입](/docs/services/appid?topic=appid-customizing-tokens#customizing-tokens)할 수 있습니다. 하지만 토큰에 필요한 정보보다 더 많은 정보를 추가하지 않도록 하십시오. 토큰은 일반적으로 http 헤더로 전송되며 헤더에는 크기 제한이 있습니다.
{: tip}

### 이 플로우의 형태는 어떻습니까?
{: #saml-flow}

{{site.data.keyword.appid_short_notm}}와 ID 제공자는 SAML 프레임워크를 사용하여 사용자를 인증하지만, {{site.data.keyword.appid_short_notm}}는 최신 OAuth 2.0/OIDC 프레임워크를 사용하여 애플리케이션과 보안 토큰을 교환합니다. 자세한 정보 플로우를 보려면 다음 이미지를 확인하십시오. 

![SAML 엔터프라이즈 인증 플로우](/images/ibmid-flow.png)

1. 사용자가 자신의 애플리케이션에서 로그인 페이지 또는 제한된 리소스에 액세스합니다. 그러면 {{site.data.keyword.appid_short_notm}} SDK 또는 API를 통해 {{site.data.keyword.appid_short_notm}} `/authorization` 엔드포인트에 대한 요청이 시작됩니다. 권한이 없는 사용자일 경우 {{site.data.keyword.appid_short_notm}}로 경로 재지정되면서 인증 플로우가 시작됩니다. 
2. {{site.data.keyword.appid_short_notm}}에서 SAML 인증 요청(AuthNRequest)을 생성하고 브라우저에서 사용자가 SAML ID 제공자로 자동 경로 재지정됩니다. 
3. ID 제공자가 SAML 요청을 구문 분석하고 사용자를 인증하며 해당 어설션을 사용하여 SAML 응답을 생성합니다. 
4. ID 제공자가 SAML 응답을 사용하여 사용자와 응답을 다시 {{site.data.keyword.appid_short_notm}}로 경로 재지정합니다. 
5. 인증에 성공하면 {{site.data.keyword.appid_short_notm}}에서 사용자의 권한 부여 및 인증을 나타내는 액세스 및 ID 토큰을 작성한 후 이를 앱에 리턴합니다. 인증에 실패하면 {{site.data.keyword.appid_short_notm}}에서 ID 제공자 오류 코드를 앱에 리턴합니다. 
6. 사용자에게 앱 또는 보호된 리소스에 대한 액세스 권한이 부여됩니다. 



### SSO의 경우 플로우가 변경됩니까? 
{: #saml-sso-flow}

{{site.data.keyword.appid_short_notm}}가 구현하는 웹 브라우저 SSO 프로파일은 서비스 제공자를 통해 시작됩니다. 즉, {{site.data.keyword.appid_short_notm}}가 SAML 요청을 ID 제공자에게 전송하여 인증 세션을 시작해야 합니다.  

{{site.data.keyword.appid_short_notm}}는 현재 ID 제공자를 통해 시작된 플로우를 지원하지 않으므로 현재 이 플로우를 서비스와 함께 사용하면 안됩니다.
{: note}

ID 제공자가 SSO를 지원할 경우 SAML 인증 시 이미 설정된 SSO 세션을 사용하여 사용자를 인증할 수 있습니다. 지원하지 않을 경우 사용자가 로그인 페이지로 경로 재지정됩니다. ID 제공자가 SSO를 설정하는 데 사용되는 요구사항과 {{site.data.keyword.cloud_notm}} 인증 요청에 정의된 인증 요구사항을 일치시킬 수 없는 경우 사용자가 경로 재지정될 수 있습니다. 예를 들어 ID 제공자가 생체인식을 사용하여 사용자 SSO 세션을 설정하는 경우, {{site.data.keyword.appid_short_notm}}의 기본 인증 컨텍스트를 변경해야 합니다. 기본적으로 {{site.data.keyword.appid_short_notm}}에서는 사용자 인증이 HTTPS를 통해 비밀번호를 사용하여 수행될 것으로 예상합니다. `urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport`.



## {{site.data.keyword.appid_short_notm}}와 함께 작동하도록 SAML 구성
{: #saml-configure}

{{site.data.keyword.appid_short_notm}}의 메타데이터는 ID 제공자에게 제공하고 ID 제공자의 메타데이터는 {{site.data.keyword.appid_short_notm}}에 제공하여 SAML이 {{site.data.keyword.appid_short_notm}}와 함께 작동하도록 구성할 수 있습니다. 



### ID 제공자에 메타데이터 제공
{: #saml-provide-idp}

앱을 구성하려면 SAML 호환 가능 ID 제공자에 정보를 제공해야 합니다. 정보는 신뢰 구축에 사용되는 구성 데이터도 포함된 메타데이터 XML 파일을 통해 교환됩니다.
{: shortdesc}

ID 제공자로 구성한 후에는 SAML을 사용으로 설정할 수 없습니다.
{: tip}

1. {{site.data.keyword.appid_short_notm}} 대시보드의 **관리** 탭에서 **SAML** 행의 **편집**을 클릭하여 설정을 구성하십시오.
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
      <td>어설션의 주제에서 전송해야 하는 ID 형식을 ID 제공자가 파악하는 방법 및 {{site.data.keyword.appid_short_notm}}에서 사용자를 식별하는 방법입니다. ID 형식은 다음과 같습니다. <code><saml:NameID Format="urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress"/></code></td>
    </tr>
    <tr>
      <td><code>WantAssertionsSigned</code></td>
      <td>어설션에 서명해야 하는지 여부를 파악하기 위해 ID 제공자가 확인하는 방법입니다. 서비스는 어설션의 서명을 예상하지만 암호화된 어설션을 지원하지는 않습니다.</td>
    </tr>
  </table>

3. ID 제공자에 데이터를 제공하십시오. ID 제공자가 메타데이터 파일의 업로드를 지원하면 이를 수행할 수 있습니다. 그렇지 않으면 수동으로 특성을 구성하십시오. 모든 ID 제공자가 동일한 특성을 사용하지는 않으므로 모든 ID 제공자를 사용하지 않을 수도 있습니다.

  특성 이름은 ID 제공자 간에 서로 다를 수 있습니다.
  {: tip}

4. **SAML 2.0 연합**을 **사용**으로 전환하십시오.



### {{site.data.keyword.appid_short_notm}}에 메타데이터 제공
{: #saml-provide-appid}

ID 제공자로부터 데이터를 받아서 {{site.data.keyword.appid_short_notm}}에 제공할 수 있습니다.
{: shortdesc}

**GUI를 사용하여 메타데이터 제공** 

1. {{site.data.keyword.appid_short_notm}} 대시보드의 **SAML 2.0** 탭으로 이동하십시오. **SAML IdP의 메타데이터 제공** 섹션에 다음과 같이 ID 제공자로부터 얻은 메타데이터를 입력하십시오.
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

인증 컨텍스트를 설정하시겠습니까? API를 통해 해당 작업을 수행할 수 있습니다.
{: tip}

</br>

**API를 사용하여 메타데이터 제공**

1. [`/saml` API 엔드포인트](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.get_saml_idp)에 대한 GET 요청을 작성하여 인증 컨텍스트 및 인증을 포함한 현재 SAML 구성을 확인하십시오.


  코드 예제:
  ```
  curl --request GET \
  https://us-south.appid.cloud.ibm.com/management/v4/<tenant-ID>/config/idps/saml \
  --header `Accept: application/json`
  ```
  {: codeblock}

  출력 예:
  ```
  {
    "isActive": true,
    "config": {
      "entityID": "https://example.com/saml2/metadata/706634",
      "signInUrl": "https://example.com/saml2/sso-redirect/706634",
      "certificates": [
        "certificate-example-pem-format"
      ],
      "displayName": "my saml example",
      "authnContext": {
        "class": [
          "urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport"
        ],
        "comparison": "exact"
      }
    }
  }
  ```
  {: screen}

2. 다음 예의 값을 제공자가 제공한 정보로 대체하여 SAML 구성을 작성하십시오. 예에 표시된 값은 필수지만, 표에 표시된 추가 정보를 포함하도록 선택할 수 있습니다. 

  ```
  "config": {
    "authnContext": {
      "class": [
        "urn:oasis:names:tc:SAML:2.0:ac:classes:YourChosenClassValue",
          "urn:oasis:names:tc:SAML:2.0:ac:classes:YourOtherChosenClassValue"
      ],
      "comparison": "sampleComparisonValue"}
    "entityID": "https://example.com/saml2/metadata/706634",
    "signInUrl": "https://example.com/saml2/sso-redirect/706634",
    "certificates": [
      "primary-certificate-example-pem-format"
        "secondary-certificate-example-pem-format"
    ],
    "displayName": "my saml example",
  }
  ```
  {: codeblock}
  {: #configuring-saml-new}

  <table>
    <tr>
      <th> 변수 </th>
      <th> 설명 </th>
    </tr>
    <tr>
      <td><code>signInUrl</code></td>
      <td>인증을 위해 사용자가 경로 재지정되는 URL입니다. 이는 SAML ID 제공자에 의해 호스팅됩니다.</td>
    </tr>
    <tr>
      <td><code>entityID</code></td>
      <td>SAML ID 제공자의 글로벌한 고유 이름입니다.</td>
    </tr>
    <tr>
      <td><code>displayName</code></td>
      <td>SAML 구성에 지정한 이름입니다. </td>
    </tr>
    <tr>
      <td><code>primary-certificate-example-pem-format</code></td>
      <td>SAML ID 제공자가 발행한 인증서입니다. 이는 SAML 어설션을 서명하고 유효성 검증하는 데 사용됩니다. 모든 제공자가 서로 다르지만, ID 제공자로부터 서명 인증서의 다운로드가 가능합니다. 인증서는 <code>.pem</code> 형식이어야 합니다.</td>
    </tr>
    <tr>
      <td>선택사항: <code>secondary-certificate-example-pem-format</code></td>
      <td>SAML ID 제공자가 발행한 백업 인증서입니다. 기본 인증서의 서명 유효성 검증이 실패할 경우에 사용됩니다. <strong>고</strong>: 서명 키가 동일하게 유지되면 {{site.data.keyword.appid_short_notm}}는 만료된 인증서에 대한 인증을 차단하지 않습니다. </td>
    </tr>
    <tr>
      <td>선택사항: <code>authnContext</code></td>
      <td>인증 컨텍스트는 인증 및 SAML 어설션의 품질을 확인하는 데 사용됩니다. 코드에 클래스 배열 및 비교 문자열을 추가하여 인증 컨텍스트를 추가할 수 있습니다. <code>class</code> 및 <code>comparison</code> 매개변수를 둘 다 사용자의 고유한 값으로 업데이트해야 합니다. 예를 들어 <code>class</code> 매개변수는 <code>urn:oasis:names:tc:SAML:2.0:ac:classes:YourChosenClassValue</code>와 유사할 수 있습니다. </td>
    </tr>
  </table>

3. [`/saml` API 엔드포인트](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp)에 대해 PUT 요청을 작성하여 2단계에서 작성한 구성을 {{site.data.keyword.appid_short_notm}}에 제공하십시오. 사용자의 요청을 살펴보려면 다음 예를 확인하십시오. 

  ```
  curl --request PUT \
  https://us-south.appid.cloud.ibm.com/management/v4/<tenant-ID>/config/idps/saml \
  --header `Accept: application/json` \
  --data \
  {
    "isActive": true,
    "config": {
      "entityID": "https://example.com/saml2/metadata/706634",
      "signInUrl": "https://example.com/saml2/sso-redirect/706634",
      "certificates": [
        "primary-certificate-example-pem-format"
      ],
      "displayName": "my saml example",
    }
  }
  ```
  {: screen}



## 구성 테스트
{: #saml-testing}

SAML ID 제공자 및 {{site.data.keyword.appid_short_notm}} 간의 구성을 테스트할 수 있습니다.

1. 구성을 저장했는지 확인하십시오.
2. {{site.data.keyword.appid_short_notm}} 대시보드의 **SAML 2.0** 탭으로 이동하고 **테스트**를 클릭하십시오. 새 탭이 열립니다.
3. ID 제공자가 이미 인증한 사용자로 로그인하십시오.
4. 양식이 완료되면 다른 페이지로 경로 재지정됩니다.
  * 성공적 인증: {{site.data.keyword.appid_short_notm}} 및 ID 제공자 간의 연결이 정상적으로 작동 중입니다. 올바른 [액세스 및 ID 토큰](/docs/services/appid?topic=appid-tokens#tokens)이 페이지에 표시됩니다.
  * 실패한 인증: 연결이 끊겼습니다. 오류 및 SAML 응답 XML 파일이 페이지에 표시됩니다.


문제점이 발견되었습니까? [문제점 해결: SAML](/docs/services/appid?topic=appid-troubleshooting-idp#troubleshooting-idp)을 확인하십시오.
{: tip}




## SAML FAQ
{: #saml-assertions}

SAML 어설션은 여러 가지 방식으로 리턴될 수 있습니다. {{site.data.keyword.appid_short_notm}}의 응답 형식화 방식을 살펴보려면 다음 예를 확인하십시오.
{: shortdesc}


### {{site.data.keyword.appid_short_notm}}가 SAML 어설션의 형태를 어떻게 예상합니까?
{: #saml-example}

서비스는 SAML 어설션의 형태가 다음 예제와 유사하다고 예상합니다.

```
<samlp:Response xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol" ID="s2202bbbbafa9d270d1c15990b738f4ab36139d463" InResponseTo="_e4a78780-35da-012e-8ea7-0050569200d8" Version="2.0" IssueInstant="2011-03-21T11:22:02Z" Destination="https://example.example.com/">
  <saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">idp_entityId</saml:Issuer>
  <samlp:Status xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <samlp:StatusCode  xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol"Value="urn:oasis:names:tc:SAML:2.0:status:Success"/>
  </samlp:Status>
  <saml:Assertion xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="2.0" ID="pfx539c9774-de5c-5f52-0c3f-b1c2e2697a89" IssueInstant="2018-01-29T13:02:58Z" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <saml:Issuer>idp_entityId</saml:Issuer>
    <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      <ds:SignedInfo>
        <ds:CanonicalizationMethod Algorithm="one_of_supported_algo"/>
        <ds:SignatureMethod Algorithm="one_of_supported_algo"/>
        <ds:Reference URI="#pfx539c9774-de5c-5f52-0c3f-b1c2e2697a89">
          <ds:Transforms>
            <ds:Transform Algorithm="one_of_supported_algo"/>
            <ds:Transform Algorithm="one_of_supported_algo"/>
          </ds:Transforms>
          <ds:DigestMethod Algorithm="one_of_supported_algo"/>
          <ds:DigestValue>huywDPPfOEGyyzE7d5hjOG97p7FDdGrjoSfes6RB19g=</ds:DigestValue>
        </ds:Reference>
      </ds:SignedInfo>
 <ds:SignatureValue>BAwNZFgWF2oxD1ux0WPfeHnzL+IWYqGhkM9DD28nI9v8XtPN8tqmIb5y4bomaYknmNpWYn7TgNO2Rn/XOq+N9fTZXO2RybaC49iF+zWibRIcNwFKCCpDL6H6jA5eqJX2YKBR+K6Yt2JPoUIRLmqdgm2lMr4Nwq1KYcSzQ/yoV5W0SN/V5t8EfctFoaXVPdtfHVXkwqHeufo+L4gobFt9NRTzXB0SQEClA1L8hQ+/LhY4l46k1D0c34iWjVLZr+ecQyubf7rekOG/R7DjWCFMTke822dR+eJTPWFsHGSPWCDDHFYqB4QMinTvUnsngjY3AssPqIOjeUxjL3p+GXn8IQ==</ds:SignatureValue>
    </ds:Signature>
    <saml:Subject>
      <saml:NameID Format="urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress">JohnDoe@gmail.com</saml:NameID>
    </saml:Subject>
    <saml:Conditions NotBefore="2018-01-29T12:59:58Z" NotOnOrAfter="2018-01-29T13:05:58Z">
    </saml:Conditions>
</samlp:Response>
```
{: screen}


### {{site.data.keyword.appid_short_notm}}에서 지원되는 알고리즘의 유형은 무엇입니까?
{: #saml-signatures}

{{site.data.keyword.appid_short_notm}}는 <a href="http://www.w3.org/2001/04/xmldsig-more#rsa-sha256" target="_blank">RSA-SHA256 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a> 알고리즘을 사용하여 XML 디지털 서명을 처리합니다.

