---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# 시작하기 튜토리얼
{: #gettingstarted}

{{site.data.keyword.appid_full}}는 사용자가 모바일 및 웹 앱에 인증을 추가할 수 있도록 도와주며 백엔드 리소스를 보호합니다.
{: shortdesc}

## 서비스 인스턴스 작성
{: #create}

{{site.data.keyword.appid_short_notm}}의 인스턴스를 작성하여 시작합니다.
{: shortdesc}

1. {{site.data.keyword.Bluemix}} 카탈로그에서 {{site.data.keyword.appid_short_notm}}를 선택하십시오. 서비스 구성 화면이 열립니다.
2. 서비스 인스턴스에 이름을 제공하거나 사전 설정된 이름을 사용하십시오.
3. 인스턴스를 바인드하려면 **연결 대상** 메뉴에서 앱을 선택하십시오. **바인딩되지 않은 상태로 두기**를 선택하면 나중에 서비스 인스턴스를 바인드할 수 있습니다.
4. 가격 책정 플랜을 선택하고 **작성**을 클릭하십시오.

## 샘플 앱 구성
{: #sample-app}

사전 구성된 샘플 앱 중 하나를 사용하여 서비스 작업을 익힐 수 있습니다.
{: shortdesc}

바로 사용할 수 있는 샘플 앱은 두 개의 ID 제공자와 인증 검토 기능으로 구성됩니다. 로그인 위젯 기능을 사용하여 사인인 페이지를 사용자 정의하고 업데이트한 사항이 앱에 얼마나 신속하게 표시되는지 확인할 수 있습니다.

GUI에서 샘플 앱을 구성하려면 다음을 수행하십시오.

1. 서비스 인스턴스를 작성한 후 작업하기에 편한 언어로 된 샘플 앱을 선택할 수 있습니다. iOS Swift, Android, Node.js 및 Java에서 선택할 수 있습니다. SDK를 사용하고 싶지 않으십니까? <a href="https://github.com/mnsn/appid-python-flask-example" target="_blank">Python과 같은 다른 언어로 {{site.data.keyword.appid_short_notm}} 사용 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>에 대한 블로그를 확인하십시오.
2. GUI의 단계를 따라 샘플 앱을 **빌드 및 실행**하십시오. 각 언어는 약간 다르게 구성되므로, 드롭 다운에서 다운로드한 앱의 언어를 선택하십시오. 앱이 구성되고 나면 브라우저에서 연 다음 신임 정보를 사용하여 로그인할 수 있습니다.
  **참고**: 작업하는 데 사용할 언어에 맞는 필수 소프트웨어가 설치되어 있는지 확인하십시오.
  <dl>
    <dt> Android </dt>
      <dd><ul><li> Android API 25 이상 </li><li> Java 8.x </li><li> Android SDK 도구 25.2.5+ </li><li> Android SDK 플랫폼 도구 25.0.3+ </li><li> Android 빌드 도구 버전 25.0.2</li></ul></dd>
    <dt> iOS Swift </dt>
      <dd><ul><li> CocoaPods(버전 1.1.0 이상) </li><li> iOS 9 이상 </li><li> MacOS 10.11.5 </li><li> Xcode 8.1 25.0.3+ </li></ul></dd>
    <dt> Node.js </dt>
      <dd><ul><li> Cloud Foundry CLI </li></ul></dd>
    <dt> Java </dt>
      <dd><ul><li>  Cloud Foundry CLI </li><li> Maven </li></ul></dd>
  </dl>
3. **활동 검토**를 클릭하여 발생한 인증 이벤트를 확인하십시오. 로그인한 경우 이벤트가 하나 이상 표시되어야 합니다.
4. 로그인 환경을 사용자 정의하십시오. 로고와 헤더 색상 등의 이미지를 선택할 수 있습니다. 색상 옵션 중 하나를 선택하거나 16진 값을 삽입할 수 있습니다. 미리보기 내용에 만족하면 **변경사항 저장**을 클릭하십시오. 다음 이미지에서 샘플 사인인 환경의 예를 볼 수 있습니다.
5. 브라우저에서 로그인 페이지를 새로 고치십시오. 이전 단계에서 변경한 내용은 이미 표시됩니다.
