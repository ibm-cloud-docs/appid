---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# 서비스 액세스 관리
{: #service-access-management}

계정 소유자는 {{site.data.keyword.appid_full}} 및 {{site.data.keyword.Bluemix_notm}} IAM(Identity and Access Management)을 사용하여 해당 계정에서 사용자 액세스를 관리할 수 있습니다.
{: shortdesc}

계정 소유자로서 서로 다른 사용자에 대해 서로 다른 액세스 레벨을 작성하도록 계정 내에서 정책을 설정할 수 있습니다. 예를 들어, 특정 사용자가 하나의 인스턴스에 대해 **읽기 전용** 액세스 권한을 보유하지만 다른 인스턴스에 대해 **쓰기** 액세스 권한을 보유할 수 있습니다. {{site.data.keyword.appid_short_notm}}의 인스턴스를 작성, 업데이트 및 삭제할 수 있는 사용자를 결정할 수 있습니다.

IAM에 대한 자세한 정보는 [IAM 액세스](/docs/iam/users_roles.html)를 참조하십시오.

## 사용자 역할
{: #roles}

액세스 정책의 범위는 사용자 지정 역할을 기반으로 합니다.
{: shortdesc}

정책을 사용하면 다양한 레벨에서 액세스 권한 부여가 가능합니다. 일부 옵션에는 다음이 포함됩니다.
<ul><ul>
  <li>계정의 모든 서비스 인스턴스에 액세스</li>
  <li>계정의 개별 서비스 인스턴스에 액세스</li>
  <li>인스턴스 내의 특정 리소스에 액세스</li>
  <li>계정의 모든 IAM 사용 서비스에 액세스</li>
</ul></ul>

플랫폼 관리 역할을 사용하여 사용자는 플랫폼 레벨에서 서비스 리소스에 대한 태스크를 수행할 수 있습니다. 예를 들어, 역할을 지정하여 ID 작성이나 삭제, 인스턴스 작성 및 앱에 인스턴스 바인드를 수행할 수 있는 사용자를 판별할 수 있습니다. 다음 표에서는 플랫폼 관리 역할과 연관될 때의 조치에 대해 자세히 설명합니다.

<table>
  <tr>
    <th>플랫폼 역할</th>
    <th>권한</th>
    <th>예제 조치</th>
  </tr>
  <tr>
    <td><i>검토자</i></td>
    <td>{{site.data.keyword.appid_short_notm}} 인스턴스를 봅니다.</td>
    <td>클라우드 디렉토리 사용자의 데이터 또는 ID 제공자 구성을 볼 수 있습니다.</td>
  </tr>
  <tr>
    <td><i>편집자</i></td>
    <td>{{site.data.keyword.appid_short_notm}} 인스턴스를 보고 바인드합니다.</td>
    <td>애플리케이션을 {{site.data.keyword.appid_short_notm}}의 인스턴스에 바인드할 수 있습니다.</td>
  </tr>
  <tr>
    <td><i>운영자</i></td>
    <td>{{site.data.keyword.appid_short_notm}} 인스턴스의 작성, 삭제, 편집, 일시중단, 재개, 보기 또는 바인드를 수행할 수 있습니다.</td>
    <td>카탈로그에서 {{site.data.keyword.appid_short_notm}} 인스턴스를 작성하거나 삭제할 수 있습니다.</td>
  </tr>
  <tr>
    <td><i>관리자</i></td>
    <td>계정의 모든 서비스에 대한 모든 관리 조치를 수행합니다.</td>
    <td>기타 사용자에게 정책을 지정하는 기능 및 모든 운영자 조치를 수행할 수 있습니다.</td>
  </tr>
</table>

</br>
</br>
다음 표에서는 서비스 액세스 역할에 맵핑된 조치에 대해 자세히 설명합니다. 서비스 액세스 역할을 사용하여 사용자는 {{site.data.keyword.appid_short_notm}} API 호출 기능은 물론 {{site.data.keyword.appid_short_notm}}에 액세스할 수 있습니다.


<table>
  <tr>
    <th>서비스 역할</th>
    <th>권한</th>
    <th>예제 조치</th>
  </tr>
  <tr>
    <td><i>독자</i></td>
    <td>{{site.data.keyword.appid_short_notm}} 인스턴스 데이터를 봅니다.</td>
    <td>사용자 데이터 또는 ID 제공자 정보 등 서비스 인스턴스의 세부사항을 볼 수 있습니다.</td>
  </tr>
  <tr>
    <td> <i>작성자 또는 관리자</i></td>
    <td>{{site.data.keyword.appid_short_notm}} 인스턴스를 보고 변경합니다.</td>
    <td>모든 독자 조치를 수행하고 서비스 인스턴스를 편집(예: ID 제공자 구성 편집)할 수 있습니다. </li></ul></td>
  </tr>
</table>

UI에서 사용자 역할 지정에 대한 자세한 정보는 [IAM 액세스 관리](/docs/iam/mngiam.html#iammanidaccser)를 참조하십시오.


## {{site.data.keyword.appid_short_notm}} 액세스 정책
{: #access}

계정에서 {{site.data.keyword.appid_short_notm}} 서비스에 액세스하는 모든 사용자에게는 IAM 사용자 역할이 정의된 액세스 정책이 지정되어야 합니다. 해당 정책은 선택된 인스턴스 또는 서비스의 컨텍스트 내에서 사용자가 수행할 수 있는 조치를 판별합니다.
{: shortdesc}

조치는 서비스에서 수행되도록 허용된 조작으로서 {{site.data.keyword.Bluemix_notm}} 서비스에 의해 정의되고 사용자 정의됩니다. 그리고 조치는 IAM 사용자 역할에 맵핑됩니다. 수행된 조치 중 일부는 {{site.data.keyword.cloudaccesstrailshort}} 서비스를 사용하여 추적할 수 있습니다. 다음 표에는 {{site.data.keyword.appid_short_notm}}에 대한 조치와 필수 권한이 맵핑되어 있습니다.

<table>
  <tr>
    <th>조치</th>
    <th>설명</th>
    <th>필수 역할</th>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-redirect-uris</code></td>
    <td>사후-인증 경로 재지정 URL을 봅니다.</td>
    <td>독자, 작성자, 관리자</td>
  </tr>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-redirect-uris</code></td>
    <td>사후-인증 경로 재지정 URL을 추가하거나 업데이트합니다.</td>
    <td>작성자, 관리자</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-idps</code></td>
    <td>ID 제공자 구성을 업데이트합니다.</td>
    <td>작성자, 관리자</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-idps</code></td>
    <td>ID 제공자 구성을 봅니다.</td>
    <td>독자, 작성자, 관리자</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-recent-activities</code></td>
    <td>목록으로서 최신 인증 이벤트를 봅니다.</td>
    <td>독자, 작성자, 관리자</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-ui-config</code></td>
    <td>로고 및 색상 등의 로그인 위젯 구성을 봅니다.</td>
    <td>독자, 작성자, 관리자</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-ui-config</code></td>
    <td>로그인 위젯 구성을 업데이트합니다.</td>
    <td>작성자, 관리자</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-user-profile-config</code></td>
    <td>사용자 프로파일 구성을 봅니다.</td>
    <td>독자, 작성자, 관리자</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-user-profile-config</code></td>
    <td>사용자 프로파일 구성을 변경합니다.</td>
    <td>작성자, 관리자</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-cd-users</code></td>
    <td>사용자 프로파일 구성을 봅니다.</td>
    <td>독자, 작성자, 관리자</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-add-cd-user</code></td>
    <td>클라우드 디렉토리에 새 사용자를 추가합니다.</td>
    <td>작성자, 관리자</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-cd-user</code></td>
    <td>클라우드 디렉토리 사용자의 세부사항을 업데이트합니다.</td>
    <td>작성자, 관리자</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-delete-cd-user</code></td>
    <td>클라우드 디렉토리에서 사용자를 삭제합니다.</td>
    <td>작성자, 관리자</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-email-template</code></td>
    <td>클라우드 디렉토리 이메일 템플리트를 봅니다.</td>
    <td>독자, 작성자, 관리자</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-update-email-template</code></td>
    <td>자체 컨텐츠로 이메일 템플리트를 업데이트합니다.</td>
    <td>작성자, 관리자</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-delete-email-template</code></td>
    <td>클라우드 디렉토리 이메일 템플리트를 삭제합니다.</td>
    <td>작성자, 관리자</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-saml-metadata</code></td>
    <td>클라우드 디렉토리의 SAML 서비스 제공자(SP) 메타데이터를 봅니다.</td>
    <td>독자, 작성자, 관리자</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-post-saml-logo</code></td>
    <td>SAML ID 제공자에 대한 로그인 위젯의 이미지를 설정하거나 업데이트합니다.</td>
    <td>작성자, 관리자</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-send-email-cd</code></td>
    <td>템플리트를 기반으로 사용자에게 이메일을 발송합니다.</td>
    <td>작성자, 관리자</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-sender-details-cd</code></td>
    <td>이메일에 대한 발신인 세부사항을 봅니다.</td>
    <td>독자, 작성자, 관리자</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-sender-details-cd</code></td>
    <td>발신인 세부사항을 업데이트합니다.</td>
    <td>작성자, 관리자</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-revoke-refresh-token</code></td>
    <td>사용자의 새로 고치기 토큰을 해당 사용자 ID로 새로 고칩니다.</td>
    <td>작성자, 관리자</td>
  </tr>
</table>

</br>

## 예제: {{site.data.keyword.appid_short_notm}}의 인스턴스에 대해 다른 사용자 액세스 부여
{: #example}

이 시나리오에서 관리자는 {{site.data.keyword.appid_short_notm}}의 인스턴스를 작성했으며 다른 팀 구성원에 대해 뷰어 액세스를 부여해야 합니다.
{: shortdesc}

시작하기 전에:
* [{{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/index.html)를 설치하십시오.

액세스 권한을 업데이트하기 위해 관리자는 다음 단계를 완료합니다.

1. {{site.data.keyword.Bluemix_notm}} 콘솔에 로그인하십시오.
2. [IAM 문서](/docs/iam/mngiam.html)에 제시된 단계에 따라 직원 보기 액세스를 부여하십시오.
3. {{site.data.keyword.appid_short_notm}} 대시보드의 **서비스 인증 정보** 탭으로 이동하십시오. 
**인증 정보 보기**를 클릭하고 **tentantID**를 복사하십시오.
4. 터미널에서 {{site.data.keyword.Bluemix_notm}} CLI로 사인인하십시오.
    ```
    ibmcloud login -a api.<region>.bluemix.net
    ```
    {: codeblock}
5. IAM 토큰을 가져오고 이를 기록하십시오.
    ```
    ibmcloud iam oauth-tokens
    ```
    {: codeblock}
6. 팀 구성원이 변경사항을 작성할 수 없는지 확인하십시오.
    ```
    curl -X PUT --header 'Content-Type: application/json' \
    --header 'Accept: application/json' \
    --header 'Authorization: <IAM token value>' \
    -d '{
     "isActive": false,
     "config": {
       "idpId": "appID",
       "secret": "appsecret"
     }
    }' \
    'https://appid-management.ng.bluemix.net/management/v4/<tenantId>/config/idps/facebook'
    ```
    {: codeblock}

    결과로 403 권한 없음 메시지가 생성됩니다.

CLI에서 {{site.data.keyword.appid_short_notm}} 구성을 보기 위해 팀 구성원은 다음 단계를 완료합니다.

1. 터미널에서 {{site.data.keyword.Bluemix_notm}} CLI를 사용하여 사인인하십시오.
    ```
    ibmcloud login -a api.<region>.bluemix.net
    ```
    {: codeblock}
2. IAM 토큰을 가져오고 이를 기록하십시오.
    ```
    ibmcloud iam oauth-tokens
    ```
    {: codeblock}
3. cURL을 사용하여 Facebook에 대한 ID 제공자 구성을 보십시오.
    ```
    curl -X GET --header 'Accept: application/json' --header 'Authorization: <IAM token value>' \  'https://appid-management.ng.bluemix.net/management/v4/<tenantId>/config/idps/facebook'
    ```
    {: codeblock}
    결과로 ID 제공자 정보가 포함된 200 메시지가 생성됩니다.
