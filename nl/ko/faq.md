---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-17"

keywords: authentication, authorization, identity, app security, secure

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
{:faq: data-hd-content-type='faq'}


# FAQ
{: #faq}

이 FAQ에서는 {{site.data.keyword.appid_full}} 서비스에 대한 일반적인 질문의 답을 제공합니다.
{: shortdesc}


## {{site.data.keyword.appid_short_notm}}의 가격 계산 방법
{: #faq-pricing}
{: faq}

{{site.data.keyword.appid_short_notm}}를 사용하면 더 많은 리소스를 좀 더 적은 비용으로 이용할 수 있습니다.
{: shortdesc}

누진 계층 플랜은 세 가지 부분(인증 이벤트 수, 정규 및 고급 보안, 권한 부여된 사용자 수)으로 구성되어 있습니다. 두 부분의 요약을 기반으로 매월 비용이 청구됩니다. 총 비용은 각 사용 레벨의 누적 요금으로 해당 계층의 단가와 수량을 곱한 값으로 구성됩니다.

첫 1000개의 인증 이벤트 및 첫 1000명의 권한 부여된 사용자는 고급 보안 이벤트를 제외하고 매월 무료로 사용할 수 있습니다. 고급 보안 이벤트의 경우 추가 비용이 발생합니다.

### 인증 이벤트
{: #faq-authentication}

새 액세스 토큰(일반 또는 익명)이 발행될 때 인증 이벤트가 발생합니다. 토큰은 사용자가 시작하거나 사용자를 대신하여 앱이 시작하는 사인인 요청에 대한 응답으로 발행할 수 있습니다. 기본적으로 액세스 토큰은 한 시간 동안 유효하며, 익명 토큰은 30일 동안 유효합니다. 토큰이 만료된 후 보호된 리소스에 액세스하려면 새 토큰을 작성해야 합니다. 서비스 대시보드의 **ID 제공자 > 관리 > 인증 설정** 페이지에서 {{site.data.keyword.appid_short_notm}} 토큰의 만기 시간을 업데이트할 수 있습니다.

#### 고급 보안 기능

고급 보안 기능은 애플리케이션의 보안을 강화하는 기능을 제공합니다.
{: shortdesc}

<table>
  <tr>
    <th>기능</th>
    <th>이점</th>
  </tr>
  <tr>
    <td>다단계 인증(MFA)</td>
    <td>[Cloud Directory용 MFA](/docs/services/appid?topic=appid-cd-mfa#cd-mfa)는 사용자가 이메일 및 비밀번호를 입력하는 것은 물론 해당 이메일로 발송되는 일회성 패스코드도 입력하도록 요구하여 사용자의 ID를 확인합니다.</td>
  </tr>
  <tr>
    <td>비밀번호 정책 관리</td>
    <td>계정 소유자의 경우 사용자 비밀번호에서 준수해야 하는 규칙 세트를 구성하여 Cloud Directory에 추가적인 보안이 설정된 비밀번호를 적용합니다. 예를 들면 잠금 전 사인인 시도 횟수, 만기 시간, 비밀번호 업데이트 사이의 최소 기간 또는 비밀번호를 반복할 수 없는 횟수 등이 있습니다. 옵션 및 설정 정보에 대한 전체 목록은 [고급 비밀번호 관리](/docs/services/appid?topic=appid-cd-strength#cd-advanced-password)를 참조하십시오.</td>
  </tr>
</table>

기본적으로 고급 보안 기능은 사용 안함으로 설정되어 있습니다. MFA 또는 비밀번호 정책 관리를 켜는 경우 추가 비용이 발생합니다. 고급 기능을 모두 사용 안함으로 설정하는 경우 계정이 저비용 정책으로 되돌려집니다. 예를 들어 10,000개의 액세스 토큰을 받았습니다. 그런 다음 비밀번호 정책 관리를 켜고 추가로 10,000개를 받았습니다. 이 경우 20,000개의 인증 이벤트 및 10,000개의 고급 보안 이벤트에 대한 비용을 지불하게 됩니다.

이러한 기능은 2018년 3월 15일 이후에 작성되었으며 누진 계층 가격 플랜이 적용된 인스턴스에서만 사용할 수 있습니다.
{: note}

### 권한이 부여된 사용자
{: #faq-authorized}

권한 부여된 사용자는 익명 사용자를 포함하여 직간접적으로 서비스를 통해 사인인하는 고유 사용자입니다. 익명 사용자를 포함하여 새 사용자가 애플리케이션에 사인인할 때마다 한 명의 권한 부여된 사용자에 대해 비용이 청구됩니다. 예를 들어 사용자가 Facebook을 통해 사인인한 후 나중에 Google을 사용하여 사인인하는 경우 두 명의 별도로 권한 부여된 사용자인 것으로 간주됩니다.

최신 가격 정보의 경우 [{{site.data.keyword.cloud_notm}} 카탈로그](https://cloud.ibm.com/catalog/services/app-id)의 {{site.data.keyword.appid_short_notm}} 섹션에서 **견적서에 추가**를 클릭하여 비용 견적서를 작성할 수 있습니다.
{: tip}



## 내 경로 재지정 URI를 화이트리스트에 지정해야 하는 이유가 무엇입니까?
{: #faq-redirect}
{: faq}

경로 재지정 URI는 앱의 콜백 엔드포인트입니다. {{site.data.keyword.appid_short_notm}}는 피싱 공격을 차단하기 위해 경로 재지정 URI의 화이트리스트에 대해 URI를 유효성 검증합니다. 피싱이 발생하는 경우 공격자가 사용자의 토큰에 대한 액세스 권한을 얻을 가능성이 존재합니다. 경로 재지정 URI에 대한 자세한 정보는 [경로 재지정 URI 추가](/docs/services/appid?topic=appid-managing-idp#add-redirect-uri)를 참조하십시오.

URL에 조회 매개변수를 포함하지 마십시오. 이는 유효성 검증 프로세스에서 무시됩니다. 예제 URL: `http://host:[port]/path`
{: tip}



## {{site.data.keyword.appid_short_notm}}에서 암호화가 어떻게 작동합니까?
{: #faq-encryption}
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
      <td>이 서비스에서는 <code>javax.crypto</code> Java 라이브러리를 사용하지만 암호화 기능을 노출하지 않습니다.</td>
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



## {{site.data.keyword.appid_short_notm}}와 Keycloak 간의 차이점은 무엇입니까?
{:# faq-keycloak}

{{site.data.keyword.appid_short_notm}}와 Keycloak은 모두 애플리케이션에 인증을 추가하고 서비스를 보안 설정하는 데 사용할 수 있습니다. 두 오퍼링 간의 주요한 차이점은 패키징 방식입니다.
{: shortdesc}

Keycloak은 소프트웨어로 패키징됩니다. 즉, 사용자가 다운로드한 이후에 제품 기능을 유지보수할 책임은 개발자에게 있습니다. 호스팅, 고가용성, 준수, 백업, DDoS 보호, 로드 밸런싱, 웹 방화벽, 데이터베이스에 대한 책임은 사용자에게 있습니다.

{{site.data.keyword.appid_short_notm}}는 "서비스로" 제공되는 완전히 관리되는 오퍼링입니다. 즉, IBM에서 서비스 운영을 담당하고, 준수, 여러 구역의 가용성 및 SLA 등을 처리합니다. {{site.data.keyword.appid_short_notm}}는 또한 {{site.data.keyword.containershort_notm}}, {{site.data.keyword.openwhisk_short}}, {{site.data.keyword.cloudaccesstrailshort}} 등의 기본 런타임 및 서비스로 구성된, {{site.data.keyword.cloud_notm}} 플랫폼을 제공하는 즉시 사용 가능한 통합 환경도 제공합니다.
