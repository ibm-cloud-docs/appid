---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-21"

keywords: authentication, authorization, identity, app security, secure, troubleshooting, help, support, requests, uri

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

# 문제점 해결: 일반
{: #troubleshooting}

{{site.data.keyword.appid_full}} 관련 작업 중에 문제점이 있으면 문제점을 해결하고 도움을 받기 위한 다음 기술을 고려하십시오.
{: shortdesc}

## 도움 및 지원 받기
{: #ts-gettinghelp}

정보를 검색하거나 포럼을 통해 질문하여 도움을 받을 수 있습니다. 또한 지원 티켓을 열 수도 있습니다. 포럼을 사용하여 질문하는 경우, {{site.data.keyword.cloud_notm}} 개발 팀이 볼 수 있도록 질문에 태그를 지정하십시오.
  * {{site.data.keyword.appid_short_notm}}에 대한 기술적 질문이 있으면 <a href="https://stackoverflow.com/" target="_blank">Stack Overflow <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>에 질문을 게시하고 질문에 "ibm-appid" 태그를 지정하십시오.
  * 서비스 및 시작하기 지시사항에 대한 질문이 있는 경우, <a href="https://developer.ibm.com/" target="_blank"> developerWorks dW Answers <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a> 포럼을 사용하십시오. `appid` 태그를 포함하십시오.

지원을 받는 방법에 대한 자세한 정보는 [필요한 지원을 받는 방법은 무엇입니까?](/docs/get-support?topic=get-support-getting-customer-support#getting-customer-support)를 참조하십시오.


## 사인인 후 사용자가 앱으로 경로 재지정되지 않음
{: #ts-signin-fail}

{: tsSymptoms}
사용자가 ID 제공자의 사인인 페이지를 통해 애플리케이션에 사인인해도 아무 일도 발생하지 않거나 사인인에 실패합니다.

{: tsCauses}
다음 이유로 인해 사인인에 실패할 수 있습니다.

* 경로 재지정 URL이 [화이트리스트](/docs/services/appid?topic=appid-faq#faq-redirect)에 제대로 추가되지 않았습니다.
* 사용자에게 권한이 부여되지 않습니다.
* 사용자가 잘못된 인증 정보로 사인인을 시도했습니다.

{: tsResolve}
경로 재지정이 발생하려면 다음을 수행하십시오.

* 경로 재지정 URL이 올바른지 확인하십시오. 경로 재지정이 발생하려면 이 URL이 정확해야 합니다.
* 사용자가 올바른 인증 정보로 사인인했는지 확인하십시오.
* 인증 정보가 ID 제공자 사용자 설정에서 구성되었는지 확인하십시오.



## 사용자 정의 URI가 거부됨
{: #ts-custom-uri}

{: tsSymptoms}
사용자 정의 URL 스킴을 사용하는 웹 경로 재지정 URL을 입력하는 경우 {{site.data.keyword.appid_short_notm}} 콘솔에서 해당 URL이 거부됩니다.

{: tsCauses}
다음과 같은 이유로 URL이 거부될 수 있습니다.

* URL이 `http` 또는 `https` 스킴을 준수하지 않음
* URL이 `://`로 종료됨
* URL에 오타가 있음

이 제한사항은 보안 용도로 사용됩니다.

{: tsResolve}
이 문제를 해결하려면 URL이 올바른지 확인하십시오. URL에서 요구사항을 충족하지 않을 경우 앱에서 HTTPS 엔드포인트를 작성하여 수신된 권한 코드를 사용자 정의 URL로 경로 재지정할 수 있습니다. {{site.data.keyword.appid_short_notm}} 콘솔에서 작성된 엔드포인트를 경로 재지정 URL로 지정하십시오. 경로 재지정 URI에 대한 자세한 정보는 [경로 재지정 URI 추가](/docs/services/appid?topic=appid-managing-idp#add-redirect-uri)를 참조하십시오.

## 사용자가 ID 제공자로 경로 재지정되지 않음
{: #ts-redirect}

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


## 속성이 잘못된 값을 표시함
{: #ts-saml-attribute}

{: tsSymptoms}
사용자 프로파일에 속성 값이 존재하지만 올바른 속성과 연관되지 않았습니다.

{: tsCauses}
사용자 프로파일 속성이 올바르게 맵핑되지 않았습니다.

{: tsResolve}
ID 제공자 설정의 속성을 맵핑하십시오. {{site.data.keyword.appid_short_notm}}는 다음의 속성을 예상합니다.
* `name`
* `email`
* `locale`
* `picture`



## 오류: 요청이 너무 많음
{: #ts-requests}

{: tsSymptoms}
앱의 홈 페이지를 표시하려고 시도하지만 다음과 같은 오류가 수신됩니다.

```
{"error_code":"too many requests","error_description":"too many requests"}
```
{: screen}

{: tsCauses}
한 명의 가상 사용자만으로 자동화된 테스트를 수행하는 경우 "요청이 너무 많음" 오류가 수신될 수 있습니다. 각각의 사용자는 1분 범위 내에 5번의 사인인을 시도할 수 있도록 제한되어 있습니다. 무차별 대입공격 강제 실행 DDOS 및 기타 유사한 유형의 공격을 차단하기 위해 사인인 시도가 제한되어 있습니다.

{: tsResolve}
문제를 해결하려면 테스트를 수행할 때 복수의 가상 사용자를 사용하십시오.
</br>
