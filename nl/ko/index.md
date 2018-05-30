---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:tip: .tip}

# 시작하기 튜토리얼
{: #gettingstarted}

애플리케이션 보안은 상당히 복잡할 수 있습니다. 대부분의 개발자에게 이는 앱 작성의 가장 어려운 부분 중 하나입니다. 사용자 정보가 보호되는지 어떻게 보장할 수 있습니까? IBM® Cloud App ID를 앱에 통합하여 리소스를 보호하고 인증을 추가할 수 있습니다. 이는 보안 경험이 많지 않은 경우에도 해당됩니다.
{: shortdesc}

사용자가 앱에 사인인하도록 요구함으로써 공개 소셜 프로파일의 정보 또는 앱 환경 설정 등의 사용자 데이터를 저장한 후에 해당 데이터를 사용하여 앱의 각 환경을 사용자 정의할 수 있습니다. App ID에서 로그인 프레임워크를 제공하지만, 클라우드 디렉토리 관련 작업 시에 자체 브랜드화된 사인인 화면을 가져올 수도 있습니다. 


계정 소유자로서 이제 팀 구성원이 {{site.data.keyword.appid_short_notm}}의 인스턴스와 상호작용할 수 있는 방법을 정의하는 정책을 설정할 수 있습니다. 서비스의 인스턴스를 작성, 업데이트 및 삭제할 수 있는 사용자를 결정할 수 있습니다. 자세한 정보는 [서비스 액세스 관리](/docs/services/appid/iam.html)를 참조하십시오.
{:tip}

## 서비스 인스턴스 작성
{: #create}

시작하려면 {{site.data.keyword.appid_short_notm}}의 인스턴스를 작성하고 이를 앱에 바인드하십시오.
{: shortdesc}

1. {{site.data.keyword.Bluemix}} 카탈로그에서 {{site.data.keyword.appid_short_notm}}를 선택하십시오. 서비스 구성 화면이 열립니다.
2. 서비스 인스턴스에 이름을 제공하거나 사전 설정된 이름을 사용하십시오.
3. 가격 책정 플랜을 선택하고 **작성**을 클릭하십시오.
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

바로 사용할 수 있는 샘플 앱은 두 개의 ID 제공자와 인증 검토 기능으로 구성됩니다. 로그인 위젯 기능을 사용하여 사인인 페이지를 사용자 정의하고 업데이트한 사항이 앱에 얼마나 신속하게 표시되는지 확인할 수 있습니다.

GUI에서 샘플 앱을 구성하려면 다음을 수행하십시오.

1. 서비스의 인스턴스가 작성된 후에는 작업하기에 편리한 언어로 샘플 앱을 선택할 수 있습니다. iOS Swift, Android, Node.js 및 Java에서 선택할 수 있습니다. SDK를 사용하고 싶지 않으십니까? <a href="https://github.com/mnsn/appid-python-flask-example" target="_blank">Python 등의 기타 언어로 {{site.data.keyword.appid_short_notm}} 사용 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>을 시작하려면 이 예제를 체크아웃하십시오. 
2. GUI의 단계를 따라 샘플 앱을 **빌드 및 실행**하십시오. 각 언어는 약간 다르게 구성되므로, 드롭 다운에서 다운로드한 앱의 언어를 선택하십시오. 앱이 구성되고 나면 브라우저에서 연 다음 신임 정보를 사용하여 로그인할 수 있습니다. 앱 언어의 필수 소프트웨어가 설치되었는지 확인하십시오. 
  <dl>
    <dt> Android </dt>
      <dd><ul><li> Android API 25 이상 </li><li> Java 8.x </li><li> Android SDK 도구 25.2.5+ </li><li> Android SDK 플랫폼 도구 25.0.3+ </li><li> Android 빌드 도구 버전 25.0.2 </li></ul></dd>
    <dt> iOS Swift </dt>
      <dd><ul><li> CocoaPods(버전 1.1.0 이상) </li><li> iOS 9 이상 </li><li> MacOS 10.11.5 </li><li> Xcode(버전 9.0.1 이상)</li></ul></dd>
    <dt> Node.js </dt>
      <dd><ul><li>  Cloud Foundry CLI </li></ul></dd>
    <dt> Java </dt>
      <dd><ul><li>  Cloud Foundry CLI </li><li> Maven </li></ul></dd>
  </dl>
3. **활동 검토**를 클릭하여 발생한 인증 이벤트를 보십시오. 로그인 후에는 이벤트를 볼 수 있습니다. 
4. 로그인 환경을 사용자 정의하십시오. 로고와 헤더 색상 등의 이미지를 선택할 수 있습니다. 색상 옵션 중 하나를 선택하거나 16진 값을 삽입할 수 있습니다. 미리보기 내용에 만족하면 **변경사항 저장**을 클릭하십시오.
5. 브라우저에서 로그인 페이지를 새로 고치십시오. 이전 단계에서 변경한 내용은 이미 표시됩니다.
