---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-02"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# FAQ

이 FAQ에서는 {{site.data.keyword.appid_full}} 서비스에 대한 일반적인 질문의 답을 제공합니다.
{: shortdesc}


## {{site.data.keyword.appid_short_notm}}의 가격 책정 계산 방법
{: #pricing}

{{site.data.keyword.appid_short_notm}}를 사용하면 더 많은 리소스를 좀 더 적은 비용으로 이용할 수 있습니다.
{: shortdesc}

누진 계층 가격 책정은 인증 이벤트 수 및 권한이 부여된 사용자의 수인 두 부분으로 구성됩니다. 두 부분의 요약을 기반으로 매월 비용이 청구됩니다. 총 비용은 각 사용 레벨의 누적 요금으로 해당 계층의 단가와 수량을 곱한 값으로 구성됩니다.

### 인증 이벤트

새 {{site.data.keyword.appid_short_notm}} 토큰이 발행될 때 인증 이벤트가 발생합니다. 식별된 사용자의 경우 각 새 토큰이 한 시간 동안 유효합니다. 익명 사용자의 경우 토큰이 한 달 동안 유효합니다. 토큰이 만료된 후 보호된 리소스에 액세스하려면 새 토큰을 작성해야 합니다. 모바일 인증을 위해 앱 ID를 사용하는 경우 사용자 토큰이 `key-store/key-chain`에 저장되고 이후 모든 요청에 추가됩니다. {{site.data.keyword.appid_short_notm}} Android 또는 iOS Swift SDK를 사용하여 토큰에 액세스할 수 있습니다. 웹 인증을 위해 서비스를 사용하는 경우 세션 쿠키에서 <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">사용자 토큰 저장 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>을 수행하십시오.

### 권한이 부여된 사용자

권한이 부여된 사용자는 직간접적으로 서비스를 사용하여 로그인하는 고유 사용자입니다. 익명의 사용자를 포함하여 새 사용자가 각 ID 제공자에서 로그인할 때마다 권한이 부여된 사용자에 대한 비용이 청구됩니다. 예를 들어, 사용자가 Facebook으로 로그인하고 이후에 Google을 사용하여 로그인한 경우 권한이 부여된 두 명의 개별 사용자로 간주됩니다.

누진 계층 가격 책정에 대한 자세한 정보는 [{{site.data.keyword.Bluemix_notm}} 가격 책정 문서](/docs/billing-usage/how_charged.html#services)를 참조하십시오.

</br>

## 앱 ID를 통해 모니터하는 활동의 유형은 무엇입니까?
{: #activity-monitor}

서비스 인스턴스에 바인딩된 앱에 생성된 활동을 추적할 수 있습니다. 활동 트래커 서비스를 사용하여 앱 ID별로 수행한 관리 활동도 모니터할 수 있습니다.

앱에서 생성한 활동을 보려면 다음을 수행하십시오.

1. IBM Cloud 계정에 로그인합니다.
2. 대시보드에서 앱 ID의 인스턴스를 선택합니다.
3. **개요** 탭을 클릭합니다.
4. **활동 로그**에 나열된 활동을 봅니다.

</br>
관리 활동을 모니터하려면 다음을 수행하십시오.

1. IBM Cloud 계정에 로그인합니다. 앱 ID의 인스턴스가 프로비저닝된 조직과 영역으로 이동합니다.
2. 카탈로그에서 활동 트래커 서비스의 인스턴스를 프로비저닝합니다. 앱 ID의 인스턴스와 동일한 영역에 있는지 확인합니다.
3. 활동 트래커 대시보드에서 **관리** 탭을 클릭합니다.
4. 드롭 다운 목록에서 다음 구성을 선택하여 앱 ID를 통해 생성한 이벤트를 검색합니다.
<table>
  <tr>
    <th> 필드 </th>
    <th> 구성 </th>
  </tr>
  <tr>
    <td><i>로그 보기</i></td>
    <td><b>영역 로그</b></td>
  </tr>
  <tr>
    <td><i>검색</i></td>
    <td><b>target.name</b></td>
  </tr>
  <tr>
    <td>필터</td>
    <td>appid</td>
  </tr>
</table>
5. **필터**를 클릭하십시오.

서비스 작동 방식에 대한 자세한 정보는 [활동 트래커 문서](/docs/services/cloud-activity-tracker/index.html)를 확인하십시오.
