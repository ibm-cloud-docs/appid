---

copyright:
  years: 2017
lastupdated: "2017-11-09"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


# 정보
{: #about}

{{site.data.keyword.appid_full}}는 사용자 친화적인 방식으로 애플리케이션에 대한 액세스를 관리하는 기능을 제공합니다.
{:shortdesc}


## 서비스 사용 이유
{: #reasons}

{{site.data.keyword.appid_short_notm}}를 사용하는 이유는 무엇입니까? 다음의 시나리오를 검토하여 이 중에서 자신에 적합한 시나리오가 있는지 확인하십시오.
{: shortdesc}

<table>
  <tr>
    <th> 시나리오</th>
    <th> 이유</th>
  </tr>
  <tr>
    <td> 모바일 및 웹 애플리케이션에 보안을 추가하려고 합니다. </td>
    <td> {{site.data.keyword.appid_short_notm}}를 사용하면 애플리케이션에 대한 인증 단계의 추가가 쉬워집니다. 이 서비스를 사용하여 ID 제공자와 통신함으로써 애플리케이션에 대한 액세스를 관리할 수 있습니다. </td>
  </tr>
  <tr>
    <td> 앱 및 백엔드 리소스에 대한 액세스를 제한하려고 합니다. </td>
    <td> 이 서비스는 인증된 사용자와 익명 사용자 모두에 대해 리소스를 보호하는 기능을 제공합니다. </td>
  </tr>
  <tr>
    <td> 사용자에 맞는 개인화된 앱 환경을 구축하려고 합니다. </td>
    <td> {{site.data.keyword.appid_short_notm}}를 사용하면 공용 소셜 프로파일의 정보 또는 앱 환경 설정 등의 사용자 데이터를 저장할 수 있습니다. 해당 데이터를 사용하면 사용자가 자신에 맞게 사용자 정의된 환경을 보유하는지 확인할 수 있습니다. </td>
  </tr>
</table>

**참고**: 구현된 프로토콜은 OIDC(OpenID Connect)를 완전히 준수합니다.


## 아키텍처
{: #architecture}

{{site.data.keyword.appid_short_notm}}에서 사용자에게 사인인하도록 요구하여 애플리케이션에 보안 레벨을 추가할 수 있습니다. 서버 SDK를 사용하여 백엔드 리소스를 보호할 수도 있습니다. 

다음 다이어그램은 {{site.data.keyword.appid_short_notm}} 서비스가 작동하는 방식에 대한 개요를 보여줍니다. 


![{{site.data.keyword.appid_short_notm}} 아키텍처 다이어그램](/images/appid_architecture2.png)

그림 1. {{site.data.keyword.appid_short_notm}} 아키텍처 다이어그램



<dl>
  <dt> 애플리케이션</dt>
    <dd> 클라이언트 SDK는 클라우드 리소스와 통신하기 위한 요청 클래스를 제공합니다. 권한 부여 인증 확인을 발견하는 경우, 클라이언트 SDK는 자동으로 인증 프로세스를 시작합니다. </dd>
  <dt> {{site.data.keyword.Bluemix_notm}} </dt>
    <dd>  서버 SDK는 요청에서 액세스 토큰을 추출하고 {{site.data.keyword.appid_short_notm}}로 해당 토큰의 유효성을 검증합니다. 인증에 성공하면 {{site.data.keyword.appid_short_notm}}가 액세스 및 ID 토큰을 애플리케이션에 리턴합니다. </dd>
  <dt> ID 제공자</dt>
    <dd> 서비스는 ID 제공자에 대한 경로 재지정을 배열하고 애플리케이션에 대한 액세스를 제공하기 위한 인증을 확인합니다. {{site.data.keyword.appid_short_notm}}는 실제 비밀번호 문구에 액세스하지 않고도 신임 정보를 확인합니다. </dd>
</dl>


## 요청 플로우
{: #request}

다음 다이어그램은 클라이언트 SDK에서 백엔드 애플리케이션 및 ID 제공자로 요청이 어떻게 이동되는지 설명합니다. 

![{{site.data.keyword.appid_short_notm}} 요청 플로우](/images/appidrequestflow.png)

그림 2. {{site.data.keyword.appid_short_notm}} 요청 플로우


* {{site.data.keyword.appid_short_notm}} 서버 SDK로 보호된 백엔드 리소스에 대한 요청을 작성하는 {{site.data.keyword.appid_short_notm}} 클라이언트 SDK. 
* {{site.data.keyword.appid_short_notm}} 서버 SDK가 권한이 없는 요청을 발견하고 HTTP 401 및 권한 범위를 리턴합니다. 
* 클라이언트 SDK가 자동으로 HTTP 401을 발견하고 인증 프로세스를 시작합니다. 
* 클라이언트 SDK가 서비스에 접속하면 둘 이상의 ID 제공자가 구성되어 있는 경우 서버 SDK는 로그인 위젯을 리턴합니다. {{site.data.keyword.appid_short_notm}}는 ID 제공자를 호출하고 해당 제공자에 대한 로그인 양식을 표시하거나, ID 제공자가 구성되지 않은 경우 인증할 수 있는 승인 코드를 리턴합니다. 
* {{site.data.keyword.appid_short_notm}}는 인증 확인 방식을 제공함으로써 인증하도록 클라이언트 앱에 요청합니다. 
* 사용자가 로그인할 때 ID 제공자가 구성된 경우에는 인증이 개별 OAuth 플로우에 의해 처리됩니다. 
* 동일한 승인 코드로 인증이 종료되는 경우 토큰 엔드포인트에 코드가 전송됩니다. 엔드포인트는 두 가지 토큰(액세스 토큰과 ID 토큰)을 리턴합니다. 이 시점부터 클라이언트 SDK로 작성된 모든 요청은 권한 헤더를 새로 획득합니다. 
* 클라이언트 SDK가 권한 플로우를 트리거한 원래 요청을 자동으로 재전송합니다. 
* 서버 SDK는 요청에서 권한 헤더를 추출하고 서비스를 사용하여 해당 헤더의 유효성을 검증하고 백엔드 리소스에 액세스를 부여합니다. 


## 컴포넌트
{: #components}

서비스는 다음 컴포넌트로 구성되어 있습니다. 

<dl>
  <dt> 대시보드</dt>
    <dd> 서비스 대시보드에서는 온보딩 샘플을 다운로드하고 활동 로그를 보며 인증 및 ID 제공자를 구성할 수 있습니다. </dd>
  <dt> 클라이언트 SDK</dt>
    <dd> 모바일 및 웹 앱에서 클라이언트 SDK를 사용하여 사용자 인증을 구현할 수 있습니다. </br></br>
    Android의 필수 소프트웨어:
    <ul><ul><li> API 25 이상 </li>
    <li> Java 8.x</li>
    <li> Android SDK 도구 25.2.5 이상 </li>
    <li> Android SDK 플랫폼 도구 25.0.3 이상 </li>
    <li> Android Build Tools 버전 25.0.2 이상 </li></ul></ul></br>
    iOS의 필수 소프트웨어:
    </br>
    <ul><ul><li> iOS9 이상 </li>
    <li> MacOS 10.11.5</li>
    <li>Xcode 8.2 </li></ul></ul></dd>
  <dt> 서버 SDK </dt>
    <dd> {{site.data.keyword.Bluemix_notm}}에서 호스팅되는 백엔드 리소스를 보호할 수 있습니다. </br>
    지원되는 런타임:
    <ul><ul><li> Node.js</li>
    <li> Liberty for Java </li>
    <li> Swift

 </li></ul></ul></dd>
</dl>
