---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:faq: data-hd-content-type='faq'}


# FAQ
{: #faq}

이 FAQ에서는 {{site.data.keyword.appid_full}} 서비스에 대한 일반적인 질문의 답을 제공합니다.
{: shortdesc}


## {{site.data.keyword.appid_short_notm}}의 가격 계산 방법
{: #pricing}
{: faq}

{{site.data.keyword.appid_short_notm}}를 사용하면 더 많은 리소스를 좀 더 적은 비용으로 이용할 수 있습니다.
{: shortdesc}

누진 계층 플랜은 세 가지 부분(인증 이벤트 수, 정규 및 고급 보안, 권한 부여된 사용자 수)으로 구성되어 있습니다. 두 부분의 요약을 기반으로 매월 비용이 청구됩니다. 총 비용은 각 사용 레벨의 누적 요금으로 해당 계층의 단가와 수량을 곱한 값으로 구성됩니다.

첫 1000개의 인증 이벤트 및 첫 1000명의 권한 부여된 사용자는 고급 보안 이벤트를 제외하고 매월 무료로 사용할 수 있습니다. 고급 보안 이벤트의 경우 추가 비용이 발생합니다.

### 인증 이벤트

새 액세스 토큰(일반 또는 익명)이 발행될 때 인증 이벤트가 발생합니다. 토큰은 사용자가 시작하거나 사용자를 대신하여 앱이 시작하는 사인인 요청에 대한 응답으로 발행할 수 있습니다. 기본적으로 액세스 토큰은 한 시간 동안 유효하며, 익명 토큰은 30일 동안 유효합니다. 토큰이 만료된 후 보호된 리소스에 액세스하려면 새 토큰을 작성해야 합니다. 서비스 대시보드의 **사인인 만기** 페이지에서 {{site.data.keyword.appid_short_notm}} 토큰의 만기 시간을 업데이트할 수 있습니다.

#### 고급 보안 기능

고급 보안 기능은 애플리케이션의 보안을 강화하는 기능을 제공합니다.
{: shortdesc}

<table>
  <tr>
    <th>기능</th>
    <th>이점</th>
  </tr>
  <tr>
    <td>다단계 인증</td>
    <td>[클라우드 디렉토리용 MFA](mfa.html)는 사용자가 이메일 및 비밀번호를 입력하는 것은 물론 해당 이메일로 발송되는 일회성 패스코드도 입력하도록 요구하여 사용자의 ID를 확인합니다.</td>
  </tr>
  <tr>
    <td>비밀번호 정책 관리</td>
    <td>계정 소유자의 경우 사용자 비밀번호에서 준수해야 하는 규칙 세트를 구성하여 클라우드 디렉토리에 추가적인 보안이 설정된 비밀번호를 적용합니다. 예를 들면 잠금 전 사인인 시도 횟수, 만기 시간, 비밀번호 업데이트 사이의 최소 기간 또는 비밀번호를 반복할 수 없는 횟수 등이 있습니다. 옵션 및 설정 정보에 대한 전체 목록은 [고급 비밀번호 관리](cloud-directory.html#advanced-password)를 참조하십시오.</td>
  </tr>
</table>

기본적으로 고급 보안 기능은 사용 안함으로 설정되어 있습니다. 다단계 인증 또는 비밀번호 정책 관리를 켜는 경우 추가 비용이 발생합니다. 고급 기능을 모두 사용 안함으로 설정하는 경우 저비용 정책으로 되돌려집니다. 예를 들어 10,000개의 액세스 토큰을 받았습니다. 그런 다음 MFA 및 비밀번호 정책 관리를 켜고 추가로 10,000개를 받았습니다. 이 경우 20,000개의 인증 이벤트 및 10,000개의 고급 보안 이벤트에 대한 비용을 지불하게 됩니다.

이러한 기능은 2018년 3월 15일 이후에 작성되었으며 누진 가격 플랜이 적용된 인스턴스에서만 사용할 수 있습니다.
{: note}

### 권한이 부여된 사용자

권한 부여된 사용자는 익명 사용자를 포함하여 직간접적으로 서비스를 통해 사인인하는 고유 사용자입니다. 익명 사용자를 포함하여 새 사용자가 애플리케이션에 사인인할 때마다 한 명의 권한 부여된 사용자에 대해 비용이 청구됩니다. 예를 들어 사용자가 Facebook을 통해 사인인한 후 나중에 Google을 사용하여 사인인하는 경우 두 명의 별도로 권한 부여된 사용자인 것으로 간주됩니다.

{{site.data.keyword.appid_short_notm}}에 대한 최신 가격 정보는 [가격 계산기](https://console.cloud.ibm.com/pricing/configure/service/AdvancedMobileAccess-d6aece47-d840-45b0-8ab9-ad15354deeea)를 참조하십시오.
{: important}

</br>


## 내 경로 재지정 URL을 화이트리스트에 지정해야 하는 이유가 무엇입니까?
{: #redirect}
{: faq}

경로 재지정 URL은 앱의 콜백 엔드포인트입니다. 피싱 공격을 차단하기 위해 {{site.data.keyword.appid_short_notm}}는 경로 재지정 URL의 화이트리스트에 대해 URL을 유효성 검증합니다. 피싱이 발생하는 경우 공격자가 사용자 토큰에 대한 액세스 권한을 얻을 기회가 존재합니다.

URL을 화이트리스트에 추가하려면 다음을 수행하십시오.

1. **ID 제공자 > 관리**로 이동하십시오.
2. **웹 경로 재지정 URL 추가** 필드에서 URL을 입력하고 **+**를 클릭하십시오.

URL에 조회 매개변수를 포함하지 마십시오. 이는 유효성 검증 프로세스에서 무시됩니다. 예제 URL: `http://host:[port]/path`
{: tip}

</br>

## {{site.data.keyword.appid_short_notm}}에서 암호화가 어떻게 작동합니까?
{: #encryption}
{: faq}

암호화에 대한 자주 묻는 질문의 답변은 다음 표를 확인하십시오.

<table>
  <thead>
    <th colspan=2><img src="images/idea.png" alt="자세한 정보 아이콘"/>  </th>
  </thead>
  <tbody>
    <tr>
      <td>암호화를 사용하는 이유는 무엇입니까?</td>
      <td>사용자 정보를 보호하는 방법 중 하나는 고객의 저장 데이터를 암호화하는 것입니다. 이 서비스는 테넌트 키별로 고객의 저장 데이터를 암호화합니다.</td>
    </tr>
    <tr>
      <td>고유 알고리즘을 빌드했습니까? 코드에서 어떤 알고리즘을 사용합니까?</td>
      <td>고유 알고리즘을 빌드하지 않았습니다. 서비스에서 솔트(salt)와 함께 <code>AES</code> 및 <code>SHA-256</code>을 사용합니다.</td>
    </tr>
    <tr>
      <td>공용 또는 오픈 소스 암호화 모듈이나 제공자를 사용합니까? 암호화 기능을 노출한 적이 있습니까? </td>
      <td>서비스에서 <code>javax.crypto</code> Java 라이브러리를 사용하지만 암호화 기능을 노출하지 않습니다.</td>
    </tr>
    <tr>
      <td>키를 어떻게 저장합니까?</td>
      <td>키는 생성되어 각각의 지역에 특정한 마스터 키로 암호화된 후 로컬로 저장됩니다. 마스터 키는 {{site.data.keyword.keymanagementserviceshort}}에 저장됩니다. 스토리지 및 미들웨어 레벨의 경우 서비스 레벨 암호화가 존재합니다(모든 고객에 대해 하나의 키가 존재함). 앱 레벨의 경우 각각의 고객에게 고유한 암호화 키가 있습니다.</td>
    </tr>
    <tr>
      <td>사용자는 키 등급은 무엇입니까?</td>
      <td>서비스에서는 16바이트를 사용합니다.</td>
    </tr>
    <tr>
      <td>암호화 기능을 노출하는 원격 API를 호출합니까?</td>
      <td>아니오, 호출하지 않습니다.</td>
    </tr>
  </tbody>
</table>

</br>

## {{site.data.keyword.appid_short_notm}}가 SAML 어설션의 형태를 어떻게 예상합니까?
{: #saml-example}
{: faq}

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

</br>

## SAML 서명에 지원되는 알고리즘의 유형
{: #saml-signatures}
{: faq}

다음 알고리즘을 사용하여 XML 디지털 서명을 처리할 수 있습니다.

<table>
  <tr>
    <th> 알고리즘 유형 </th>
    <th> 알고리즘 옵션 </th>
  </tr>
  <tr>
    <td>정규화 및 변환 알고리즘(주석 포함/미포함)</td>
    <td><ul><li><a href="http://www.w3.org/TR/2001/REC-xml-c14n-20010315" target="_blank">Canonicalization <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></li>
    <li><a href="http://www.w3.org/2001/10/xml-exc-c14n#" target="_blank">Exclusive Canonicalization with and without comments <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></li>
    <li><a href=" http://www.w3.org/2000/09/xmldsig#enveloped-signature" target="_blank">Enveloped Signature transform <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></li></ul></td>
  </tr>
  <tr>
    <td>해싱 알고리즘</td>
    <td><ul><li><a href="http://www.w3.org/2000/09/xmldsig#sha1" target="_blank">SHA1 digests <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmlenc#sha256" target="_blank">SHA256 digests <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmlenc#sha512" target="_blank">SHA512 digests <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></li></ul></td>
  </tr>
  <tr>
    <td>서명 알고리즘</td>
    <td><ul><li><a href="http://www.w3.org/2000/09/xmldsig#rsa-sha1" target="_blank">RSA-SHA1 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmldsig-more#rsa-sha256" target="_blank">RSA-SHA256 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmldsig-more#rsa-sha512" target="_blank">RSA-SHA512 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></li>
    <li><a href="http://www.w3.org/2000/09/xmldsig#hmac-sha1" target="_blank">HMAC-SHA1 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></li></ul></td>
  </tr>
</table>

SAML ID 제공자 사용에 대한 자세한 정보는 [엔터프라이즈 ID 제공자 구성](enterprise.html)을 참조하십시오.
