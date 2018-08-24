---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# 정보
{: #about}

애플리케이션 보안은 상당히 복잡할 수 있습니다. 대부분의 개발자에게 이는 앱 작성의 가장 어려운 부분 중 하나입니다. 사용자의 정보가 보호되는지 어떻게 보장할 수 있습니까? {{site.data.keyword.appid_full}}를 앱에 통합하여 리소스를 보호하고 인증을 추가할 수 있습니다. 이는 보안 경험이 많지 않은 경우에도 해당됩니다.
{:shortdesc}


## 서비스 사용 이유
{: #reasons}

{{site.data.keyword.appid_short_notm}}는 개발자가 몇 개의 코드 행으로 쉽게 웹 및 모바일 앱에 인증을 추가하고 {{site.data.keyword.Bluemix_notm}}의 클라우드 고유 애플리케이션 및 서비스를 보호하도록 도움을 줍니다. 사용자가 앱에 사인인하도록 요구함으로써 공개 소셜 프로파일의 정보 또는 앱 환경 설정 등의 사용자 데이터를 저장한 후에 해당 데이터를 활용하여 앱 내의 각 사용자 환경을 사용자 정의할 수 있습니다. {{site.data.keyword.appid_short_notm}}에서 로그인 프레임워크를 제공하지만 클라우드 디렉토리에 사용할 자체 브랜드화된 사인인 화면을 가져올 수도 있습니다.
{: shortdesc}

{{site.data.keyword.appid_short_notm}}를 사용하는 이유는 무엇입니까? 다음의 시나리오를 체크아웃하여 이 중에서 적용되는 시나리오가 있는지 여부를 확인할 수 있습니다.

<table>
  <tr>
    <th>시나리오</th>
    <th>솔루션</th>
  </tr>
  <tr>
    <td>[권한 및 인증](/docs/services/appid/authorization.html)을 모바일 및 웹 앱에 추가해야 하지만 안전한 백그라운드를 갖추고 있지 않습니다.</td>
    <td>{{site.data.keyword.appid_short_notm}}를 사용하면 앱에 대한 인증 단계의 추가가 쉬워집니다. API, SDK, 사전 빌드된 UI 또는 자체 브랜드화된 UI를 사용하여 이메일 또는 사용자 이름 사인인, 소셜 사인인, 엔터프라이즈 사인인을 앱에 추가할 수 있습니다.</td>
  </tr>
  <tr>
    <td>앱 및 백엔드 리소스에 대한 액세스를 제한하려고 합니다.</td>
    <td>{{site.data.keyword.appid_short_notm}}에서 제공되는 표준 기반 인증을 사용하여 앱, 백엔드 리소스 및 API를 쉽게 보호할 수 있습니다.</td>
  </tr>
  <tr>
    <td>사용자에 맞는 개인화된 앱 환경을 구축하려고 합니다.</td>
    <td>{{site.data.keyword.appid_short_notm}}를 사용하여 앱 환경 설정 또는 공개 소셜 프로파일의 정보와 같은 [사용자 데이터를 저장](/docs/services/appid/user-profile.html)한 다음 해당 데이터를 사용하여 앱의 각 환경을 사용자 정의할 수 있습니다.</td>
  </tr>
  <tr>
    <td>확장 가능한 방식으로 사용자를 관리하려고 합니다.</td>
    <td> {{site.data.keyword.appid_short_notm}}를 사용하면 등록 및 사인인을 앱에 추가할 수 있도록 허용하는 [클라우드 디렉토리](/docs/services/appid/cloud-directory.html)를 작성할 수 있습니다. 클라우드 디렉토리에서는 사용자 기반으로 스케일링할 수 있는 사용자 레지스트리를 유지보수하는 프레임워크를 제공합니다. 이메일 검증 및 비밀번호 재설정과 같이 사전 빌드된 셀프 서비스 기능을 사용하여 앱에서 사용자를 안전하게 인증하는지 확인할 수 있습니다.</td>
  </tr>
</table>


## 통합
{: #integrations}

{{site.data.keyword.appid_short_notm}}를 기타 {{site.data.keyword.Bluemix_notm}} 오퍼링에서 사용할 수 있습니다.
{:shortdesc}


<dl>
  <dt>{{site.data.keyword.containerlong_notm}}</dt>
    <dd>표준 클러스터에서 Ingress를 구성하면 클러스터 레벨에서 앱을 보호할 수 있습니다. 시작하려면 <a href="/docs/containers/cs_annotations.html#appid-auth">{{site.data.keyword.appid_short_notm}} authentication Ingress annotation</a> 또는 <a href="https://www.ibm.com/blogs/bluemix/2018/05/announcing-app-id-integration-ibm-cloud-kubernetes-service/">Announcing App ID integration to IBM Cloud Kubernetes Service<img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a> 블로그 게시물을 확인하십시오.</dd>
  <dt>{{site.data.keyword.openwhisk}} 및 API Connect</dt>
    <dd>[{{site.data.keyword.openwhisk_short}}](/docs/openwhisk/index.html) 및 [API Connect](/docs/apis/management/manage_apis.html)로 API를 작성하면 앱 코드에서가 아니라 게이트웨이에서 애플리케이션을 보호할 수 있습니다. 조치에서 통합을 보려면 <a href="https://www.youtube.com/watch?v=Fa9YD2NGZiE" target="_blank">Simple and fast social login OAUTH with APIC and {{site.data.keyword.appid_short_notm}}<img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 참조하십시오.</dd>
  <dt>Cloud Foundry</dt>
    <dd>제공된 샘플 Cloud Foundry 앱 중 하나를 실행해 보면 {{site.data.keyword.appid_short_notm}}를 앱에 통합하는 방법을 볼 수 있습니다.</dd>
  <dt>iOS Programming Guide</dt>
    <dd>Apple용 앱을 개발하십니까? <a href="https://console.bluemix.net/docs/swift/index.html#overview" target="_blank">iOS Programming Guide<img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 실행해 보면 {{site.data.keyword.Bluemix_notm}}에서 기존 iOS 앱을 학습하고 실험하며 개선할 수 있습니다. </dd>
  <dt>{{site.data.keyword.cloudaccesstrailshort}}</dt>
    <dd>[{{site.data.keyword.cloudaccesstrailshort}} 서비스](/docs/services/cloud-activity-tracker/index.html)를 사용하여 대시보드 구성 변경사항과 같이 {{site.data.keyword.appid_short_notm}}에서 작성된 관리 활동을 모니터할 수 있습니다.</dd>
  <dt>Node.js Programming Guide</dt>
    <dd>Node.js에서 앱을 개발하십니까? <a href="https://console.bluemix.net/docs/node/index.html#getting-started-tutorial" target="_blank">Node.js Programming Guide<img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 실행해 보면 {{site.data.keyword.Bluemix_notm}}에서 기존 Node.js 앱을 학습하고 실험하며 개선할 수 있습니다. </dd>
</dl>


## 아키텍처
{: #architecture}

{{site.data.keyword.appid_short_notm}}을 사용하면 사용자에게 사인인을 요구하여 앱에 보안 레벨을 추가할 수 있습니다. 서버 SDK 또는 API를 사용하여 백엔드 리소스를 보호할 수도 있습니다.
{: shortdesc}

![{{site.data.keyword.appid_short_notm}} 아키텍처 다이어그램](/images/appid_architecture1.png)

<dl>
  <dt>애플리케이션</dt>
    <dd><strong>서버 SDK</strong>: 서버 SDK를 사용하여 웹 앱 및 {{site.data.keyword.Bluemix_notm}}에 호스팅된 백엔드 리소스를 보호할 수 있습니다. 서버 SDK는 요청에서 액세스 토큰을 추출하고 {{site.data.keyword.appid_short_notm}}로 해당 토큰의 유효성을 검증합니다. </br>
    <strong>클라이언트 SDK</strong>: Android 또는 iOS 클라이언트 SDK로 모바일 앱을 보호할 수 있습니다. 권한 부여 인증 확인을 발견하는 경우, 클라이언트 SDK는 인증 프로세스를 시작하도록 클라우드 리소스와 통신합니다.</dd>
  <dt>{{site.data.keyword.Bluemix_notm}}</dt>
    <dd><strong>{{site.data.keyword.appid_short_notm}}</strong>: 인증에 성공한 후에 {{site.data.keyword.appid_short_notm}}는 액세스 및 ID 토큰을 앱에 리턴합니다.</br>
    <strong>클라우드 디렉토리</strong>: 사용자는 자신의 이메일과 비밀번호로 서비스에 등록할 수 있습니다. 그런 다음 UI를 통해 목록 보기에 있는 사용자를 관리할 수 있습니다. 클라우드 디렉토리로 {{site.data.keyword.appid_short_notm}}는 ID 제공자의 기능을 수행합니다.</dd>
  <dt>외부(써드파티)</dt>
    <dd><strong>소셜 및 엔터프라이즈 ID 제공자</strong>: {{site.data.keyword.appid_short_notm}}는 Facebook, Google+ 및 SAML 2.0 연합을 ID 제공자 옵션으로 지원합니다. 서비스는 ID 제공자에 대한 경로 재지정을 배열하고 리턴된 인증 토큰을 확인합니다. 토큰이 올바르지 않은 경우, 서비스는 실제 비밀번호 문구에 액세스하지 않고도 앱에 대한 액세스 권한을 부여합니다.</dd>
</dl>


## 요청 플로우
{: #request}

요청 플로우는 애플리케이션 구성에 따라 다를 수 있지만 App ID에 대해 작업하는 동안 발생할 수 있는 세 가지 기본 플로우가 있습니다. 모바일 앱 플로우, 웹 앱 플로우를 작성하거나 다른 플로우로 리소스를 보호할 수 있습니다. 앱을 구성할 때 그 위치에서 시작할 수 있는지 알아보려면 몇 가지 예제 플로우를 확인하십시오.
{: shortdesc}

### 웹 앱 요청 플로우
{: #web-flow}

![{{site.data.keyword.appid_short_notm}} 요청 플로우](/images/web_flow1.png)

1. 사용자가 브라우저를 사용하여 App ID SDK에 대한 요청을 트리거하는 조치를 수행합니다.
2. 사용자에게 권한이 없는 경우 App ID로의 경로 재지정이 시작됩니다.
3. App ID가 웹 위젯을 실행하여 브라우저에 전송합니다.
4. 사용자가 인증할 ID 제공자를 선택하고 사인인 프로세스를 완료합니다.
5. ID 제공자가 ID 토큰을 사용하여 App ID SDK로 다시 경로 재지정합니다.
6. App ID SDK가 App ID 서비스에서 액세스 토큰을 가져옵니다.
7. App ID SDK가 토큰을 저장하고 경로 재지정이 발생합니다.
8. 사용자에게 애플리케이션에 대한 권한이 부여됩니다.

### 모바일 요청 플로우
{: #mobile-flow}

![{{site.data.keyword.appid_short_notm}} 요청 플로우](/images/mobile_flow.png)

1. 사용자가 App ID SDK에 대한 클라이언트 애플리케이션의 요청을 트리거하는 조치를 수행합니다.
2. 사용자에게 올바른 액세스 토큰이 없는 경우 App ID SDK가 권한 부여 프로세스를 시작합니다.
3. 로그인 위젯이 사용자에게 표시됩니다.
4. 사용자가 구성된 ID 제공자 중 하나를 사용하여 인증합니다.
5. 사용자에게 ID 토큰이 있으면 SDK가 App ID 서비스에서 액세스 토큰를 가져옵니다.
6. 두 토큰을 모두 사용하여 SDK가 요청을 다시 수행합니다.
7. 토큰이 올바른 경우 사용자에게 애플리케이션에 대한 액세스 권한이 부여됩니다.

### 보호된 리소스 요청 플로우
{: #pr-flow}

![{{site.data.keyword.appid_short_notm}} 요청 플로우](/images/pr_flow.png)

1. 리소스에 대한 요청을 작성하기 전에 클라이언트 애플리케이션에 공개 키 세트가 있어야 합니다.
2. 공개 키를 사용하여 클라이언트 애플리케이션에서 요청을 작성합니다.
3. 올바른 액세스 토큰이 없으면 애플리케이션이 오류를 수신합니다.
4. 올바른 토큰을 얻은 후 클라이언트 앱이 다시 요청할 수 있습니다. 그러나 이때 토큰을 포함하십시오.
5. 애플리케이션이 액세스 토큰에서 부여된 권한의 유효성을 검증할 수 있는 경우 애플리케이션에 보호된 리소스에 대한 액세스 권한이 부여됩니다.
