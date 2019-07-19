---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-18"

keywords: Authentication, authorization, identity, app security, secure, application identity, app to app, access token, activity

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


# {{site.data.keyword.cloudaccesstrailshort}} 이벤트
{: #at-events}

{{site.data.keyword.cloudaccesstrailshort}} 서비스를 사용하여 {{site.data.keyword.appid_full}} 서비스 인스턴스에서 작성된 사용자가 시작하는 활동을 확인, 관리 및 분석할 수 있습니다.
{: shortdesc}





서비스가 작동하는 방식에 대한 자세한 정보는 [{{site.data.keyword.cloudaccesstrailshort}} 문서](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started)를 참조하십시오.






## 관리 이벤트 보기
{: #at-monitor-admin}

{{site.data.keyword.at_short}} 서비스를 사용하여 {{site.data.keyword.appid_short_notm}} 인스턴스에서 작성된 구성 활동을 확인, 관리 및 분석할 수 있습니다.
{: shortdesc}

관리 활동을 모니터링하려면 다음을 수행하십시오.

1. {{site.data.keyword.cloud_notm}} 계정에 로그인하십시오.
2. 카탈로그에서 {{site.data.keyword.appid_short_notm}} 인스턴스와 동일한 계정의 {{site.data.keyword.cloudaccesstrailshort}} 서비스 인스턴스를 프로비저닝하십시오.
3. {{site.data.keyword.cloudaccesstrailshort}} 대시보드에서 **관리** 탭을 클릭하십시오.
4. 드롭 다운 목록에서 다음 구성을 작성하여 {{site.data.keyword.appid_short_notm}}에서 생성된 이벤트를 검색하십시오.
    * **로그 보기**에서 **계정 로그**를 선택하십시오.
    * **검색**에서 **target.Management**를 선택하십시오.
    * **필터**에 `appid`를 입력하십시오.
5. **필터**를 클릭하십시오.

</br>

## 관리 이벤트 목록
{: #at-events-admin}

{{site.data.cloudaccesstrailshort}}에 전송되는 이벤트의 목록을 보려면 다음 표를 확인하십시오.

<table>
  <tr>
    <th>조치</th>
    <th>설명</th>
    <th>UI 위치</th>
  </tr>
  <tr>
    <td><code>read.recentActivity</code></td>
    <td>최근 활동을 봅니다.</td>
    <td><strong>개요</strong> 탭의 <strong>활동 로그</strong> 상자에서 찾을 수 있습니다.</td>
  </tr>
  <tr>
    <td><code>read.idpConfig</code></td>
    <td>ID 제공자 구성을 봅니다.</td>
    <td><strong>ID 제공자 > 관리</strong> 탭에서 찾을 수 있습니다.</td>
  </tr>
  <tr>
    <td><code>update.idpConfig</code></td>
    <td>ID 제공자 구성을 업데이트합니다.</td>
    <td><strong>ID 제공자 > 관리</strong> 탭에서 업데이트할 수 있습니다.</td>
  </tr>
  <tr>
    <td><code>read.tokensConfig</code></td>
    <td>토큰 만기 구성을 봅니다.</td>
    <td><strong>ID 제공자 > 토큰 만기</strong> 탭에서 찾을 수 있습니다.</td>
  </tr>
  <tr>
    <td><code>read.isProfilesActive</code></td>
    <td>사용자 프로파일 스토리지 구성을 봅니다.</td>
    <td><strong>개요</strong> 탭의 <strong>활동 로그</strong>에서 찾을 수 있습니다.</td>
  </tr>
  <tr>
    <td><code>update.isProfilesActive</code></td>
    <td>사용자 프로파일 스토리지 구성을 업데이트합니다.</td>
    <td><strong>프로파일</strong> 탭에서 찾을 수 있습니다.</td>
  </tr>
  <tr>
    <td><code>read.themeColor</code></td>
    <td>로그인 위젯 헤더의 테마 색상을 봅니다.</td>
    <td><strong>로그인 사용자 정의</strong> 탭에서 찾을 수 있습니다.</td>
  </tr>
  <tr>
    <td><code>update.themeColor</code></td>
    <td>로그인 위젯 헤더의 테마 색상을 업데이트합니다.</td>
    <td><strong>로그인 사용자 정의</strong> 탭에서 업데이트할 수 있습니다.</td>
  </tr>
  <tr>
    <td><code>read.media</code></td>
    <td>로그인 위젯에 표시되는 이미지를 확인합니다.</td>
    <td><strong>로그인 사용자 정의</strong> 탭에서 찾을 수 있습니다.</td>
  </tr>
  <tr>
    <td><code>update.media</code></td>
    <td>로그인 위젯에 표시되는 이미지를 업데이트합니다.</td>
    <td><strong>로그인 사용자 정의</strong> 탭에서 업데이트할 수 있습니다.</td>
  </tr>
  <tr>
    <td><code>read.uiConfiguration</code></td>
    <td>헤더 색상 및 이미지를 포함한 로그인 위젯 UI 구성을 확인합니다.</td>
    <td><strong>로그인 사용자 정의</strong> 탭에서 찾을 수 있습니다.</td>
  </tr>
  <tr>
    <td><code>read.uiLanguages</code></td>
    <td>지원되는 언어 목록을 봅니다.</td>
    <td>API에서 확인해야 합니다.</td>
  </tr>
  <tr>
    <td><code>update.uiLanguages</code></td>
    <td>지원되는 언어를 업데이트합니다.</td>
    <td>API를 통해 업데이트해야 합니다.</td>
  </tr>
  <tr>
    <td><code>read.samlMetadata</code></td>
    <td>{{site.data.keyword.appid_short_notm}} SAML 메타데이터를 확인합니다.</td>
    <td><strong>ID 제공자 > SAML 2.0 연합</strong> 탭에서 찾을 수 있습니다.</td>
  </tr>
  <tr>
    <td><code>read.cloudDirectoryUser</code></td>
    <td>Cloud Directory 사용자를 봅니다.</td>
    <td><strong>사용자</strong> 탭에서 찾을 수 있습니다.</td>
  </tr>
  <tr>
    <td><code>update.cloudDirectoryUser</code></td>
    <td>Cloud Directory 사용자를 업데이트합니다.</td>
    <td><strong>사용자</strong> 탭에서 업데이트할 수 있습니다.</td>
  </tr>
  <tr>
    <td><code>delete.cloudDirectoryUser</code></td>
    <td>Cloud Directory 사용자를 삭제합니다.</td>
    <td><strong>사용자</strong> 탭에서 삭제할 수 있습니다.</td>
  </tr>
  <tr>
    <td><code>read.cloudDirectoryUsers</code></td>
    <td>Cloud Directory 사용자 목록을 봅니다.</td>
    <td><strong>사용자</strong> 탭에서 찾을 수 있습니다.</td>
  </tr>
  <tr>
    <td><code>update.cloudDirectoryUsers</code></td>
    <td>Cloud Directory 사용자 목록을 업데이트합니다.</td>
    <td><strong>사용자</strong> 탭에서 업데이트할 수 있습니다.</td>
  </tr>
  <tr>
    <td><code>delete.cloudDirectoryUsers</code></td>
    <td>Cloud Directory 사용자 목록을 삭제합니다.</td>
    <td><strong>사용자</strong> 탭에서 삭제할 수 있습니다.</td>
  </tr>
  <tr>
    <td><code>read.emailTemplate</code></td>
    <td>이메일 템플리트를 봅니다.</td>
    <td><strong>ID 제공자 > Cloud Directory > 템플리트</strong> 탭에서 찾을 수 있습니다.</td>
  </tr>
  <tr>
    <td><code>update.emailTemplate</code></td>
    <td>이메일 템플리트를 업데이트합니다.</td>
    <td><strong>ID 제공자 > Cloud Directory > 템플리트</strong> 탭에서 찾을 수 있습니다.</td>
  </tr>
  <tr>
    <td><code>delete.emailTemplate</code></td>
    <td>기본값으로 재설정하기 위해 이메일 템플리트를 삭제합니다.</td>
    <td><strong>ID 제공자 > Cloud Directory > 템플리트</strong> 탭에서 찾을 수 있습니다.</td>
  </tr>
  <tr>
    <td><code>read.senderDetails</code></td>
    <td>발신인 세부사항을 봅니다.</td>
    <td><strong>ID 제공자 > Cloud Directory > 설정</strong> 탭에서 찾을 수 있습니다.</td>
  </tr>
  <tr>
    <td><code>update.senderDetails</code></td>
    <td>발신인 세부사항을 업데이트합니다.</td>
    <td><strong>ID 제공자 > Cloud Directory > 설정</strong> 탭에서 찾을 수 있습니다.</td>
  </tr>
  <tr>
    <td><code>update.resendNotification</code></td>
    <td>사용자 알림을 다시 보냅니다.</td>
    <td><strong>ID 제공자 > Cloud Directory > 설정</strong> 탭에서 찾을 수 있습니다.</td>
  </tr>
  <tr>
    <td><code>update.selfForgotPassword</code></td>
    <td>비밀번호 찾기 프로세스를 업데이트합니다.</td>
    <td><strong>ID 제공자 > Cloud Directory > 설정</strong> 탭에서 찾을 수 있습니다.</td>
  </tr>
  <tr>
    <td><code>update.forgotPasswordResult</code></td>
    <td>비밀번호 찾기 확인 결과를 봅니다.</td>
    <td>API를 통해 수행해야 합니다.</td>
  </tr>
  <tr>
    <td><code>update.selfSignUp</code></td>
    <td>등록 프로세스를 업데이트합니다.</td>
    <td><strong>ID 제공자 > Cloud Directory > 설정</strong> 탭에서 찾을 수 있습니다.</td>
  </tr>
  <tr>
    <td><code>update.signUpResult</code></td>
    <td>등록 결과 확인을 확인합니다.</td>
    <td>API를 통해 수행해야 합니다.</td>
  </tr>
  <tr>
    <td><code>read.action_url</code></td>
    <td>조치가 수행될 때 호출되는 사용자 정의 URL을 봅니다.</td>
    <td><strong>ID 제공자 > Cloud Directory > 사용자 정의 랜딩 페이지</strong> 탭에서 찾을 수 있습니다.</td>
  </tr>
  <tr>
    <td><code>update.action_url</code></td>
    <td>조치가 수행될 때 호출되는 사용자 정의 URL을 업데이트합니다.</td>
    <td><strong>ID 제공자 > Cloud Directory > 설정</strong> 탭에서 찾을 수 있습니다.</td>
  </tr>
  <tr>
    <td><code>update.changePassword</code></td>
    <td>Cloud Directory 사용자 비밀번호를 변경합니다.</td>
    <td><strong>ID 제공자 > Cloud Directory > 설정</strong> 탭에서 찾을 수 있습니다.</td>
  </tr>
  <tr>
    <td><code>read.loginWidgetConfig</code></td>
    <td>로그인 위젯 구성을 봅니다.</td>
    <td><strong>로그인 사용자 정의</strong> 탭에서 찾을 수 있습니다.</td>
  </tr>
  <tr>
    <td><code>update.loginWidgetConfig</code></td>
    <td>로그인 위젯 구성을 업데이트합니다.</td>
    <td><strong>로그인 사용자 정의</strong> 탭에서 업데이트할 수 있습니다.</td>
  </tr>
</table>



