---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-20"

keywords: authentication, authorization, identity, app security, secure, development,

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

# 시작하기 튜토리얼
{: #getting-started}

애플리케이션 보안은 상당히 복잡할 수 있습니다. 대부분의 개발자에게 이는 앱 작성의 가장 어려운 부분 중 하나입니다. 사용자 정보가 보호되는지 어떻게 보장할 수 있습니까? {{site.data.keyword.appid_full}}를 앱에 통합하여 리소스를 보호하고 인증을 추가할 수 있습니다. 이는 보안 경험이 많지 않은 경우에도 해당됩니다.
{: shortdesc}

사용자가 앱에 사인인하도록 요구함으로써 공개 소셜 프로파일의 정보 또는 앱 환경 설정 등의 사용자 데이터를 저장한 후에 해당 데이터를 사용하여 앱의 각 환경(experience)을 사용자 정의할 수 있습니다. {{site.data.keyword.appid_short_notm}}에서 프레임워크를 제공하지만 Cloud Directory에서 작동하는 경우 고유 브랜드 사인인 화면을 가져올 수도 있습니다.

귀하의 피드백과 질문을 듣고 싶습니다!
* {{site.data.keyword.appid_short_notm}}에 대한 기술적 질문이 있는 경우 <a href="https://stackoverflow.com" target="_blank">스택 오버플로우 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>에 질문을 게시하고 해당 질문에 `ibm-appid` 태그를 지정하십시오.
* 서비스 및 시작하기 지시사항에 대한 질문이 있는 경우, <a href="https://developer.ibm.com" target="_blank"> developerWorks dW Answers <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a> 포럼을 사용하십시오. `appid` 태그를 포함하십시오.

## 서비스 인스턴스 작성
{: #create}

시작하려면 {{site.data.keyword.appid_short_notm}}의 인스턴스를 작성하고 이를 앱에 바인드하십시오.
{: shortdesc}

1. {{site.data.keyword.cloud_notm}} 카탈로그에서 {{site.data.keyword.appid_short_notm}}를 선택하십시오. 서비스 구성 화면이 열립니다.
2. 서비스 인스턴스에 이름을 제공하거나 사전 설정된 이름을 사용하십시오.
3. 가격 플랜을 선택하고 **작성**을 클릭하십시오.
4. {{site.data.keyword.appid_short_notm}}의 인스턴스를 바인드하십시오.
    1. 서비스 인스턴스에 바인드할 수 있는 앱의 목록을 보려면 **연결**을 클릭하십시오.
    2. **연결 작성**을 클릭하십시오. 바인드할 옵션이 있는 모든 앱으로 페이지가 열립니다.
    3. 바인드할 앱에서 **연결**을 클릭하십시오.
    4. **다시 스테이징**을 클릭하여 변경사항을 적용하십시오.

이제 됐습니다! 애플리케이션 설정의 구성을 시작할 준비를 마쳤습니다.

## 샘플 앱 구성
{: #sample-app}

사전 구성된 샘플 앱 중 하나를 사용하여 서비스 작업을 익힐 수 있습니다.
{: shortdesc}

바로 사용할 수 있는 샘플 앱은 두 개의 ID 제공자와 인증 검토 기능으로 구성됩니다. 샘플 앱은 `iOS Swift`, `Android`, `Node.js` 및 `Java` 형식으로 제공됩니다. 원하는 언어가 표시되지 않더라도 걱정하지 마십시오! 제공된 API를 사용하여 {{site.data.keyword.appid_short_notm}}를 고유한 샘플 애플리케이션에 통합할 수 있습니다.

샘플 앱을 빌드하려면 다음 작업을 수행하십시오.

1. **샘플 다운로드**를 클릭하십시오.
2. 원하는 언어를 클릭하여 샘플을 다운로드하십시오.
  찾고 있는 언어가 표시되지 않았습니까? 걱정하지 마십시오! API를 통해 {{site.data.keyword.appid_short_notm}}를 활용할 수 있습니다. <a href="https://www.ibm.com/blogs/bluemix/tag/app-id/" target="_blank">IBM Cloud 블로그 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 확인하여 다른 언어로 추가 도움을 받을 수 있습니다.
  {: tip}
3. 전제조건이 설치되었거나 완료되었는지 확인하십시오.
4. **빌드 및 실행** 단계를 수행하여 {{site.data.keyword.appid_short_notm}}에서 샘플을 설정하십시오.
5. **활동 검토**를 클릭하여 발생한 인증 이벤트를 확인하십시오. 유형에 관계 없이 사인인이 발생하면 이 페이지에 표시되는 이벤트가 작성됩니다.
6. 사인인 위젯을 사용자 정의하십시오.
  1. **선택**을 클릭한 후 이미지를 업로드할 로컬 시스템을 찾아서 브랜드 로고 등의 이미지를 추가하십시오.
  2. 색상 옵션 중 하나를 선택하거나 16진 값으로 지정하여 색상 스킴을 선택하십시오.
  3. 웹과 모바일 사이에서 변경하여 각각의 디바이스에서 색상 스킴이 표시되는 방식을 확인하십시오.
  4. 선택사항이 만족스러운 경우 **변경사항 저장**을 클릭하십시오.
7. 브라우저에서 로그인 페이지를 새로 고치십시오. 이전 단계에서 변경한 내용은 이미 표시됩니다.


## 다음 단계
{: #next}

자체 앱을 시작할 준비가 되었습니까? [앱에 서비스를 추가](/docs/services/appid?topic=appid-web-apps#web-apps)하여 시작하십시오. 이 서비스는 대부분의 언어를 위한 SDK를 제공하지만 앱이 작성된 언어용 SDK가 없더라도 API를 사용하여 {{site.data.keyword.appid_short_notm}}를 활용할 수 있습니다.
