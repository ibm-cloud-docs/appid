---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}


# FAQ

이 FAQ에서는 {{site.data.keyword.appid_full}} 서비스에 대한 일반적인 질문의 답을 제공합니다.
{: shortdesc}


## {{site.data.keyword.appid_short_notm}}의 가격 책정 계산 방법
{: #pricing}

{{site.data.keyword.appid_short_notm}}를 사용하면 더 많은 리소스를 좀 더 적은 비용으로 이용할 수 있습니다.
{: shortdesc}

누진 계층 가격 책정은 인증 이벤트 수 및 권한이 부여된 사용자의 수인 두 부분으로 구성됩니다. 두 부분의 요약을 기반으로 매월 비용이 청구됩니다. 총 비용은 각 사용 레벨의 누적 요금으로 해당 계층의 단가와 수량을 곱한 값으로 구성됩니다.

### 인증 이벤트

새 액세스 토큰(일반 또는 익명)이 발행될 때 인증 이벤트가 발생합니다. 식별된 사용자의 경우 각각의 새 토큰은 1시간 동안 유효합니다(실제 사용자 인증 또는 새로 고치기 토큰을 통해 유효하게 됨). 익명 토큰은 기본적으로 1개월 동안 유효합니다. 토큰이 만료된 후 보호된 리소스에 액세스하려면 새 토큰을 작성해야 합니다. {{site.data.keyword.appid_short_notm}} 대시보드의 **사인인 만기** 페이지에서 {{site.data.keyword.appid_short_notm}} 토큰의 만기 시간을 업데이트할 수 있습니다.

모바일 애플리케이션에서 {{site.data.keyword.appid_short_notm}}를 사용하는 경우 토큰이 key-store 또는 key-chain에 저장되며 이후의 모든 요청에 추가됩니다. App ID Android 또는 iOS SDK를 사용하여 토큰에 액세스할 수 있습니다. 웹 애플리케이션에서 {{site.data.keyword.appid_short_notm}}를 사용하는 경우 애플리케이션 세션 쿠키에 토큰을 저장하도록 권장합니다.


### 권한이 부여된 사용자

권한이 부여된 사용자는 직간접적으로 서비스를 사용하여 로그인하는 고유 사용자입니다. 익명의 사용자를 포함하여 새 사용자가 각 ID 제공자에서 로그인할 때마다 권한이 부여된 사용자에 대한 비용이 청구됩니다. 예를 들어, 사용자가 Facebook으로 로그인하고 이후에 Google을 사용하여 로그인한 경우 권한이 부여된 두 명의 개별 사용자로 간주됩니다.

누진 계층 가격 책정에 대한 자세한 정보는 [{{site.data.keyword.Bluemix_notm}} 가격 책정 문서](/docs/billing-usage/how_charged.html#services)를 참조하십시오.

</br>


## {{site.data.keyword.appid_short_notm}}에서 암호화가 어떻게 작동합니까?
{: #encryption}

암호화에 대한 자주 묻는 질문의 답변은 다음 표를 확인하십시오.

<table>
  <thead>
    <th colspan=2><img src="images/idea.png" alt="자세한 정보 아이콘"/>  </th>
  </thead>
  <tbody>
    <tr>
      <td>암호화를 사용하는 이유는 무엇입니까?</td>
      <td>서비스가 고객의 저장 데이터를 암호화합니다.</td>
    </tr>
    <tr>
      <td>고유 알고리즘을 빌드했습니까? 코드에서 어떤 알고리즘을 사용합니까?</td>
      <td>고유 알고리즘을 빌드하지 않았습니다. 서비스에서 솔트(salt)와 함께 <code>AES</code> 및 <code>SHA-256</code>을 사용합니다.</td>
    </tr>
    <tr>
      <td>공용 또는 오픈 소스 암호화 모듈이나 제공자를 사용합니까? 암호화 기능을 노출한 적이 있습니까?</td>
      <td>서비스에서 <code>javax.crypto</code> Java 라이브러리를 사용하지만 암호화 기능을 노출하지 않습니다.</td>
    </tr>
    <tr>
      <td>키를 어떻게 저장합니까?</td>
      <td>키가 생성된 다음 각 지역에 특정한 마스터 키를 사용하여 암호화된 후 로컬로 저장됩니다. 마스터 키는 {{site.data.keyword.keymanagementserviceshort}}에 저장됩니다.</td>
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
