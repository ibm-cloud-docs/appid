---

copyright:
  years: 2017, 2018
lastupdated: "2018-04-27"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 정보
{: #about}

{{site.data.keyword.appid_full}}를 사용하여 인증을 앱에 추가하고 백엔드 리소스를 보호할 수 있습니다.
{:shortdesc}

## 서비스 사용 이유
{: #reasons}

{{site.data.keyword.appid_short_notm}}를 사용하는 이유는 무엇입니까? 다음의 시나리오를 체크아웃하여 이 중에서 적용되는 시나리오가 있는지 여부를 확인할 수 있습니다.
{: shortdesc}

<table>
  <tr>
    <th> 시나리오 </th>
    <th> 이유 </th>
  </tr>
  <tr>
    <td> [권한 및 인증](/docs/services/appid/authorization.html)을 모바일 및 웹 앱에 추가해야 하지만 안전한 백그라운드를 갖추고 있지 않습니다. </td>
    <td> {{site.data.keyword.appid_short_notm}}를 사용하면 앱에 대한 인증 단계의 추가가 쉬워집니다. 이 서비스를 사용하여 [ID 제공자](/docs/services/appid/identity-providers.html)와 통신함으로써 앱에 대한 액세스를 관리할 수 있습니다. </td>
  </tr>
  <tr>
    <td> 앱 및 백엔드 리소스에 대한 액세스를 제한하려고 합니다. </td>
    <td> 이 서비스는 인증된 사용자와 익명 사용자 모두의 [리소스 보호](/docs/services/appid/protecting-resources.html)에 대한 기능을 제공합니다. </td>
  </tr>
  <tr>
    <td> 사용자에 맞는 개인화된 앱 환경을 구축하려고 합니다. </td>
    <td> {{site.data.keyword.appid_short_notm}}를 사용하여 앱 환경 설정 또는 공개 소셜 프로파일의 정보와 같은 [사용자 데이터를 저장](/docs/services/appid/user-profile.html)한 다음 해당 데이터를 사용하여 앱의 각 환경을 사용자 정의할 수 있습니다. </td>
  </tr>
  <tr>
    <td> 이메일과 비밀번호를 사용하여 앱에 대한 액세스 권한을 얻는 기능을 제공하고자 합니다. </td>
    <td> {{site.data.keyword.appid_short_notm}}를 사용하면 등록 및 사인인을 앱에 추가할 수 있도록 허용하는 [클라우드 디렉토리](/docs/services/appid/cloud-directory.html)를 작성할 수 있습니다. 클라우드 디렉토리에서는 사용자 기반으로 스케일링할 수 있는 사용자 레지스트리를 유지보수하는 프레임워크를 제공합니다. 이메일 검증 및 비밀번호 재설정과 같이 사전 빌드된 셀프 서비스 기능을 사용하여 앱에서 사용자를 안전하게 인증하는지 확인할 수 있습니다. </td>
  </tr>
</table>


## 통합
{: #integrations}

{{site.data.keyword.appid_short_notm}}를 기타 {{site.data.keyword.Bluemix_notm}} 오퍼링에서 사용할 수 있습니다.
{:shortdesc}


<dl>
  <dt>{{site.data.keyword.containerlong_notm}}</dt>
    <dd>표준 클러스터에서 Ingress를 구성하면 클러스터 레벨에서 앱을 보호할 수 있습니다. 시작하려면 {{site.data.keyword.appid_short_notm}} 인증 Ingress 어노테이션을 체크아웃하십시오. </dd>
  <dt>{{site.data.keyword.openwhisk}} 및 API Connect</dt>
    <dd>[{{site.data.keyword.openwhisk_short}}](/docs/openwhisk/index.html) 및 [API Connect](/docs/apis/management/manage_apis.html)로 API를 작성하면 앱 코드에서가 아니라 게이트웨이에서 애플리케이션을 보호할 수 있습니다. 조치에서 통합을 보려면 <a href="https://www.youtube.com/watch?v=Fa9YD2NGZiE" target="_blank">APIC 및 {{site.data.keyword.appid_short_notm}}를 사용한 단순하고 빠른 소셜 로그인 OAUTH <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 참조하십시오. </dd>
  <dt>Cloud Foundry</dt>
    <dd>샘플 Cloud Foundry 앱 중 하나를 실행해 보면 앱 id를 앱에 통합하는 방법을 볼 수 있습니다. </dd>
  <dt>iOS 프로그래밍 안내서</dt>
    <dd>Apple용 앱을 개발하십니까? <a href="https://console.bluemix.net/docs/swift/index.html#overview" target="_blank">iOS 프로그래밍 안내서 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 실행해 보면 {{site.data.keyword.Bluemix_notm}}에서 기존 iOS 앱을 학습하고 실험하며 개선할 수 있습니다. </dd>
</dl>


## 아키텍처
{: #architecture}

{{site.data.keyword.appid_short_notm}}을 사용하면 사용자에게 사인인을 요구하여 앱에 보안 레벨을 추가할 수 있습니다. 서버 SDK를 사용하여 백엔드 리소스를 보호할 수도 있습니다.
{: shortdesc}

![{{site.data.keyword.appid_short_notm}} 아키텍처 다이어그램](/images/appid_architecture.png)

<dl>
  <dt> 애플리케이션 </dt>
    <dd><strong>서버 SDK</strong>: 서버 SDK를 사용하여 웹 앱 및 {{site.data.keyword.Bluemix_notm}}에 호스팅된 백엔드 리소스를 보호할 수 있습니다. 서버 SDK는 요청에서 액세스 토큰을 추출하고 {{site.data.keyword.appid_short_notm}}로 해당 토큰의 유효성을 검증합니다. </br>
    <strong>클라이언트 SDK</strong>: Android 또는 iOS 클라이언트 SDK로 모바일 앱을 보호할 수 있습니다. 권한 부여 인증 확인을 발견하는 경우, 클라이언트 SDK는 인증 프로세스를 시작하도록 클라우드 리소스와 통신합니다.</dd>
  <dt>{{site.data.keyword.Bluemix_notm}}</dt>
    <dd><strong>{{site.data.keyword.appid_short_notm}}</strong>: 인증에 성공한 후에 {{site.data.keyword.appid_short_notm}}는 액세스 및 ID 토큰을 앱에 리턴합니다. </br>
    <strong>클라우드 디렉토리</strong>: 사용자는 자신의 이메일과 비밀번호로 서비스에 등록할 수 있습니다. 그런 다음 UI를 통해 목록 보기에 있는 사용자를 관리할 수 있습니다. 클라우드 디렉토리로 {{site.data.keyword.appid_short_notm}}는 ID 제공자의 기능을 수행합니다. </dd>
  <dt>외부(써드파티)</dt>
    <dd><strong>소셜 및 엔터프라이즈 ID 제공자</strong>:{{site.data.keyword.appid_short_notm}}는 2개의 소셜 ID 제공자(Facebook 및 Google+)와 1개의 엔터프라이즈 ID 제공자(SAML 2.0 연합)를 지원합니다. 서비스는 ID 제공자에 대한 경로 재지정을 배열하고 리턴된 인증 토큰을 확인합니다. 토큰이 올바르지 않은 경우, 서비스는 실제 비밀번호 문구에 액세스하지 않고도 앱에 대한 액세스 권한을 부여합니다. </dd>
</dl>


## 요청 플로우
{: #request}

다음 다이어그램은 클라이언트 SDK에서 백엔드 리소스 및 ID 제공자로 요청이 어떻게 이동되는지 설명합니다.
{: shortdesc}

![{{site.data.keyword.appid_short_notm}} 요청 플로우](/images/appidrequestflow.png)


* {{site.data.keyword.appid_short_notm}} 클라이언트 SDK는 {{site.data.keyword.appid_short_notm}} 서버 SDK로 보호되는 백엔드 리소스에 대한 요청을 작성합니다. 
* {{site.data.keyword.appid_short_notm}} 서버 SDK가 권한이 없는 요청을 발견하고 HTTP 401 및 권한 범위를 리턴합니다.
* 클라이언트 SDK가 자동으로 HTTP 401을 발견하고 인증 프로세스를 시작합니다.
* 클라이언트 SDK가 서비스에 접속하면 둘 이상의 ID 제공자가 구성되어 있는 경우 서버 SDK는 로그인 위젯을 리턴합니다. {{site.data.keyword.appid_short_notm}}는 ID 제공자를 호출하고 해당 제공자에 대한 로그인 양식을 표시하거나, ID 제공자가 구성되지 않은 경우 인증할 수 있는 승인 코드를 리턴합니다.
* {{site.data.keyword.appid_short_notm}}는 인증 확인 방식을 제공함으로써 인증하도록 클라이언트 앱에 요청합니다.
* 사용자가 로그인할 때 ID 제공자가 구성된 경우에는 인증이 개별 OAuth 플로우에 의해 처리됩니다.
* 동일한 승인 코드로 인증이 종료되는 경우 토큰 엔드포인트에 코드가 전송됩니다. 엔드포인트는 두 가지 토큰(액세스 토큰과 ID 토큰)을 리턴합니다. 이 시점부터 클라이언트 SDK로 작성된 모든 요청은 권한 헤더를 새로 획득합니다.
* 클라이언트 SDK가 권한 플로우를 트리거한 원래 요청을 자동으로 재전송합니다.
* 서버 SDK는 요청에서 권한 헤더를 추출하고 서비스를 사용하여 해당 헤더의 유효성을 검증하고 백엔드 리소스에 액세스를 부여합니다.

**참고**: 구현된 프로토콜은 OIDC(OpenID Connect)를 완전히 준수합니다.
