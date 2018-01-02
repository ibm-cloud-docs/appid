---

copyright:
  years: 2017
lastupdated: "2017-12-12"

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


누진 계층 가격 책정에 대한 자세한 정보는 [{{site.data.keyword.Bluemix_notm}} 가격 책정 문서](/docs/pricing/index.html#pricing)를 참조하십시오.
