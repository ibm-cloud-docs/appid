---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-18"

keywords: Authentication, authorization, identity, app security, secure, compliance, high availability, ha, disaster recover, dr, protocols, oauth, oidc

subcollection: appid

---

{:external: target="_blank" .external}
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

# {{site.data.keyword.appid_short_notm}}에 대한 정보
{: #about}

애플리케이션 보안은 상당히 복잡할 수 있습니다. 대부분의 개발자에게 이는 앱 작성의 가장 어려운 부분 중 하나입니다. 사용자의 정보가 보호되는지 어떻게 보장할 수 있습니까? {{site.data.keyword.appid_full}}를 앱에 통합하여 리소스에 보안을 적용하고 인증을 추가할 수 있습니다. 이는 보안 경험이 많지 않은 경우에도 해당됩니다.
{: shortdesc}



## 서비스 사용 이유
{: #about-reasons}

{{site.data.keyword.appid_short_notm}}는 개발자가 몇 개의 코드 행으로 쉽게 웹 및 모바일 앱에 인증을 추가하고 {{site.data.keyword.cloud_notm}}의 클라우드 고유 애플리케이션 및 서비스를 보호하도록 도움을 줍니다. 사용자가 앱에 사인인하도록 요구함으로써 공개 소셜 프로파일의 정보 또는 앱 환경 설정 등의 사용자 데이터를 저장한 후에 해당 데이터를 활용하여 앱 내의 각 사용자 환경(experience)을 사용자 정의할 수 있습니다. {{site.data.keyword.appid_short_notm}}에서 로그인 프레임워크를 제공하지만 Cloud Directory에서 사용할 고유 브랜드 화면을 가져올 수도 있습니다.
{: shortdesc}

Cloud Directory의 용도는 무엇입니까? 이 동영상을 참조하여 서비스를 사용하는 다양한 방법에 대한 자세한 정보를 확인한 후 다음 표에서 다른 시나리오에 대한 자세한 정보를 읽어보십시오.

<iframe class="embed-responsive-item" id="about-appid" title="{{site.data.keyword.appid_short_notm}} 정보" type="text/html" width="640" height="390" src="//www.youtube.com/embed/XlrCjHdK43Q?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

<table>
  <tr>
    <th>시나리오</th>
    <th>솔루션</th>
  </tr>
  <tr>
    <td>[권한 및 인증](/docs/services/appid?topic=appid-key-concepts)을 모바일 및 웹 앱에 추가해야 하지만 안전한 백그라운드를 갖추고 있지 않습니다.</td>
    <td>{{site.data.keyword.appid_short_notm}}를 사용하면 앱에 대한 인증 단계의 추가가 쉬워집니다. API, SDK, 사전 빌드된 UI 또는 고유 브랜드 UI를 사용하여 앱에 이메일, 사용자 이름, 소셜 또는 엔터프라이즈 사인인을 추가할 수 있습니다.</td>
  </tr>
  <tr>
    <td>앱 및 백엔드 리소스에 대한 액세스를 제한하려고 합니다.</td>
    <td>{{site.data.keyword.appid_short_notm}}에서 제공되는 표준 기반 인증을 사용하여 앱, 백엔드 리소스 및 API에 간단히 보안을 적용할 수 있습니다.</td>
  </tr>
  <tr>
    <td>사용자에 맞는 개인화된 앱 환경을 구축하려고 합니다.</td>
    <td>{{site.data.keyword.appid_short_notm}}를 사용하여 앱 환경 설정 또는 공개 소셜 프로파일의 정보와 같은 [사용자 데이터를 저장](/docs/services/appid?topic=appid-profiles)한 다음 해당 데이터를 사용하여 앱의 각 환경을 사용자 정의할 수 있습니다.</td>
  </tr>
  <tr>
    <td>확장 가능한 방식으로 사용자를 관리하려고 합니다.</td>
    <td> {{site.data.keyword.appid_short_notm}}를 사용하는 경우 앱에 사용자 등록 및 사인인을 추가할 수 있도록 해주는 [Cloud Directory](/docs/services/appid?topic=appid-cloud-directory)를 작성할 수 있습니다. Cloud Directory에서는 사용자 기반으로 스케일링할 수 있는 사용자 레지스트리를 유지보수하는 프레임워크를 제공합니다. 이메일 검증 및 비밀번호 재설정과 같이 사전 빌드된 셀프 서비스 기능을 사용하여 앱에서 사용자를 안전하게 인증하는지 확인할 수 있습니다.</td>
  </tr>
</table>


## 작동 방식
{: #about-how-it-works}

{{site.data.keyword.appid_short_notm}}을 사용하면 사용자에게 사인인을 요구하여 앱에 보안 레벨을 추가할 수 있습니다. 서버 SDK 또는 API를 사용하여 백엔드 리소스를 보호할 수도 있습니다.
{: shortdesc}

![{{site.data.keyword.appid_short_notm}} 아키텍처 다이어그램](images/appid_architecture1.png)

<dl>
  <dt>애플리케이션</dt>
    <dd><strong>서버 SDK</strong>: 서버 SDK를 사용하여 웹 앱 및 {{site.data.keyword.cloud_notm}}에 호스팅된 백엔드 리소스를 보호할 수 있습니다. 서버 SDK는 요청에서 액세스 토큰을 추출하고 {{site.data.keyword.appid_short_notm}}로 해당 토큰의 유효성을 검증합니다.</br>
    <strong>클라이언트 SDK</strong>: Android 또는 iOS 클라이언트 SDK로 모바일 앱을 보호할 수 있습니다. 권한 부여 인증 확인을 발견하는 경우, 클라이언트 SDK는 인증 프로세스를 시작하도록 클라우드 리소스와 통신합니다.</dd>
  <dt>{{site.data.keyword.cloud_notm}}</dt>
    <dd><strong>{{site.data.keyword.appid_short_notm}}</strong>: 인증에 성공한 후에 {{site.data.keyword.appid_short_notm}}는 액세스 및 ID 토큰을 앱에 리턴합니다. </br>
    <strong>Cloud Directory</strong>: 사용자는 이메일 및 비밀번호를 사용하여 서비스에 등록할 수 있습니다. 그런 다음 UI를 통해 목록 보기에 있는 사용자를 관리할 수 있습니다. Cloud Directory를 사용하는 경우 {{site.data.keyword.appid_short_notm}}가 ID 제공자로 작동합니다.</dd>
  <dt>외부(서드파티)</dt>
    <dd><strong>소셜 및 엔터프라이즈 ID 제공자</strong>: {{site.data.keyword.appid_short_notm}}는 Facebook, Google+ 및 SAML 2.0 연합을 ID 제공자 옵션으로 지원합니다. 서비스는 ID 제공자에 대한 경로 재지정을 배열하고 리턴된 인증 토큰을 확인합니다. 토큰이 올바르지 않은 경우, 서비스는 실제 비밀번호 문구에 액세스하지 않고도 앱에 대한 액세스 권한을 부여합니다.</dd>
</dl>


## 통합
{: #about-integrations}

{{site.data.keyword.appid_short_notm}}를 기타 {{site.data.keyword.cloud_notm}} 오퍼링에서 사용할 수 있습니다.
{:shortdesc}

<dl>
  <dt>{{site.data.keyword.containershort_notm}}</dt>
    <dd>표준 클러스터에서 Ingress를 구성하면 클러스터 레벨에서 앱을 보호할 수 있습니다. 시작하려면 <a href="/docs/containers?topic=containers-ingress_annotation#appid-auth">{{site.data.keyword.appid_short_notm}} authentication Ingress annotation</a> 또는 <a href="https://www.ibm.com/cloud/blog/announcing-app-id-integration-ibm-cloud-kubernetes-service">Announcing {{site.data.keyword.appid_short_notm}} integration to {{site.data.keyword.containerlong_notm}} <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a> 블로그 게시물을 확인하십시오.</dd>
  <dt>{{site.data.keyword.openwhisk_short}} 및 {site.data.keyword.apiconnect_short}}</dt>
    <dd>[{{site.data.keyword.openwhisk_short}}](/docs/openwhisk?topic=cloud-functions-getting-started) 및 [API Connect](/docs/services/apiconnect?topic=apiconnect-getting-started)로 API를 작성하면 앱 코드에서가 아니라 게이트웨이에서 애플리케이션을 보호할 수 있습니다. 작동 중인 통합을 확인하려면 <a href="https://www.youtube.com/watch?v=Fa9YD2NGZiE" target="_blank">API Connect 및 {{site.data.keyword.appid_short_notm}}를 사용한 단순하고 빠른 소셜 로그인 OAauth <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 시청하십시오.</dd>
  <dt>Cloud Foundry</dt>
    <dd>제공된 샘플 Cloud Foundry 앱 중 하나를 실행해 보면 {{site.data.keyword.appid_short_notm}}를 앱에 통합하는 방법을 볼 수 있습니다.</dd>
  <dt>{{site.data.keyword.cloudaccesstrailshort}}</dt>
    <dd>[{{site.data.keyword.cloudaccesstrailshort}} 문서](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started)를 사용하여 대시보드 구성 변경사항과 같이 {{site.data.keyword.appid_short_notm}}에서 작성된 관리 활동을 모니터링할 수 있습니다.</dd>
  <dt>iOS Programming Guide</dt>
    <dd>Apple용 앱을 개발하십니까? {{site.data.keyword.cloud_notm}}에서 기존 iOS 앱을 학습, 실험 및 개선하려면 [iOS 프로그래밍 안내서](/docs/swift?topic=swift-getting-started)를 사용해 보십시오.</dd>
  <dt>Node.js Programming Guide</dt>
    <dd>Node.js에서 앱을 개발하십니까? {{site.data.keyword.cloud_notm}}에서 기존 Node.js 앱을 학습, 실험 및 개선하려면 [Node.js 프로그래밍 안내서](/docs/node?topic=nodejs-getting-started)를 사용해 보십시오.</dd>
</dl>


## 규제 준수 및 표준
{: #about-compliance}

{{site.data.keyword.appid_short_notm}}의 경우 여러 인증, 감사 및 표준이 정상적으로 갖추어져 있습니다. 
{: shortdesc}

{{site.data.keyword.appid_short_notm}}는 엔터프라이즈 및 이용자가 모두 사용하는 애플리케이션인 OAuth 2.0 Authorization Framework 및 Open ID Connect에서 자주 발견되는 유명한 업계 표준 프로토콜 및 스펙 세트를 기반으로 합니다. OAuth 2.0은 보호된 리소스에 액세스하기 위한 권한을 획득하고 검증하기 위해 사용됩니다. 또한 Open ID Connect는 애플리케이션에 인증 및 ID 보호 계층을 추가합니다.

[인증](https://www.ibm.com/software/reports/compatibility/clarity-reports/report/html/softwareReqsForProduct?deliverableId=BF31C8008D7C11E59F9AD7336D7D0FFB){: external}의 전체 목록을 검토하려면 {{site.data.keyword.appid_short_notm}} 소프트웨어 제품 호환성 보고서의 5.4절을 참조하십시오. {{site.data.keyword.appid_short_notm}}는 해당 인증 외에도 OAuth 2.0, OpenID Connect, JWT(JSON Web Token), JWS(JSON Web Signature), SCIM(System for Cross-domain Identity Management) 등의 스펙을 준수합니다. 


## 지역별 고가용성
{: #ha-dr}

{{site.data.keyword.appid_short_notm}}는 복수의 지역에서 실행되는 고가용성의 지역 서비스입니다.
{: shortdesc}

지원되는 각각의 다중 지역에서 모든 지역에는 몇 개의 작업자 노드가 포함된 고유한 {{site.data.keyword.containerlong_notm}} 클러스터가 있습니다. 각각의 작업자 노드는 {{site.data.keyword.appid_short_notm}} 컴포넌트에 대한 몇 가지 인스턴스를 실행합니다. 각각의 지역은 글로벌 로드 밸런서 및 웹 애플리케이션 방화벽과 마주하고 있습니다.

{{site.data.keyword.appid_short_notm}}에 저장되는 데이터는 암호화되어 가용성 지역에 분산되어 있는 데이터베이스 클러스터에서 지속됩니다. 또한 이 데이터는 별도의 암호화된 오브젝트 스토리지에 백업됩니다.

{{site.data.keyword.appid_short_notm}}는 지역 서비스이기 때문에 자동화된 교차 지역 장애 복구 또는 교차 지역 재해 복구를 제공하지 않습니다. 그러나 {{site.data.keyword.appid_short_notm}}에서는 개발자가 해당 서비스 구성을 {{site.data.keyword.appid_short_notm}}의 다른 인스턴스와 수동으로 동기화하기 위해 사용할 수 있는 [광범위한 API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/){: external}를 제공합니다.

