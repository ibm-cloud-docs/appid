---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}

# 일반 문제점 해결
{: #troubleshooting}

{{site.data.keyword.appid_full}} 관련 작업 중에 문제점이 있으면 문제점을 해결하고 도움을 받기 위한 다음 기술을 고려하십시오.
{: shortdesc}

## 도움 및 지원 받기
{: #gettinghelp}

정보를 검색하거나 포럼을 통해 질문하여 도움을 받을 수 있습니다. 또한 지원 티켓을 열 수도 있습니다. 포럼을 사용하여 질문하는 경우, {{site.data.keyword.Bluemix_notm}} 개발 팀이 볼 수 있도록 질문에 태그를 지정하십시오.
  * {{site.data.keyword.appid_short_notm}}에 대한 기술적 질문이 있으면 <a href="https://stackoverflow.com/search?q=ibm-appid" target="_blank">Stack Overflow <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>에 질문을 게시하고 질문에 "ibm-appid" 태그를 지정하십시오.
  * 서비스 및 시작하기 지시사항에 대한 질문이 있는 경우, <a href="https://developer.ibm.com/answers/topics/appid/" target="_blank"> developerWorks dW Answers <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a> 포럼을 사용하십시오. `appid` 태그를 포함하십시오.

지원을 받는 방법에 대한 자세한 정보는 [필요한 지원을 받는 방법은 무엇입니까?](/docs/get-support/howtogetsupport.html#getting-customer-support)를 참조하십시오.

</br>

## 사용자 정의 URL이 거부됨
{: #ts-custom-url}


{: tsSymptoms}
사용자 정의 URL 스킴을 사용하는 웹 경로 재지정 URL을 입력하는 경우 {{site.data.keyword.appid_short_notm}} 콘솔에서 해당 URL이 거부됩니다.

{: tsCauses}
다음과 같은 이유로 URL이 거부될 수 있습니다.

* URL이 `http` 또는 `https` 스킴을 준수하지 않음
* URL이 `://`로 종료됨
* URL에 오타가 있음

이 제한사항은 보안 용도로 사용됩니다.

{: tsResolve}
이 문제를 해결하려면 URL이 올바른지 확인하십시오. URL에서 요구사항을 충족하지 않을 경우 앱에서 HTTPS 엔드포인트를 작성하여 수신된 권한 코드를 사용자 정의 URL로 경로 재지정할 수 있습니다. {{site.data.keyword.appid_short_notm}} 콘솔에서 작성된 엔드포인트를 경로 재지정 URL로 지정하십시오.

</br>
