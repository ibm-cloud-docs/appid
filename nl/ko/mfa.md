---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}


# 다단계 인증
{: #mfa}

다단계 인증(MFA)은 사용자가 누구인지 확인하기 위해 알고 있는 것 뿐만 아니라 보유하고 있는 것도 사용하도록 요구하여 사용자의 ID를 확인하는 방법입니다. 예를 들어 {{site.data.keyword.appid_full}}를 사용하는 경우 사용자가 이메일 및 비밀번호를 입력한 후 해당 이메일로 전송된 일회성 코드를 입력하도록 할 수 있습니다.
{: shortdesc}

MFA는 클라우드 디렉토리 사용자만 사용할 수 있습니다. SAML 2.0 또는 소셜 로그인을 통한 엔터프라이즈 사인인을 사용하는 경우 사용 중인 ID 제공자에서 MFA를 사용으로 설정할 수 있습니다.
{: note}

MFA가 사용으로 설정되면 새 사용자가 사인인하려고 시도할 때마다 로그인 위젯에서 MFA를 요구합니다. 사용자가 정상적으로 인증 정보를 입력하면 자신의 계정을 작성할 때 등록한 이메일 주소로 일회성 패스코드가 발송됩니다. 각각의 코드는 6자이며 만기는 5분입니다. 사용자가 해당 코드를 수신하지 않을 경우 다른 코드를 발송하도록 요청할 수 있지만 만기 시간은 재설정되지 않습니다. 코드가 만료되면 사용자는 강제로 전체 로그인 프로세스를 반복해야 합니다.

등록 시 아직 관리 API 또는 이메일 검증을 통해 사용자 이메일이 확인되지 않은 경우 MFA 코드 검증이 정상적으로 완료될 때 확인됩니다. 사용자의 이메일 주소를 변경해야 하는 경우 관리자는 [관리 API](https://appid-management.ng.bluemix.net/swagger-ui/#!/Cloud_Directory_Users/updateCloudDirectoryUser)를 사용할 수 있습니다.

MFA는 [누진 계층 가격 플랜](faq.html#pricing)에 있는 {{site.data.keyword.appid_short_notm}}의 해당 인스턴스에 대해 사용할 수 있습니다.
{: note}

## 플로우에 대한 정보
{: #understanding}



1. 앱 사용자에게 {{site.data.keyword.appid_short_notm}}의 기본 사인인 UI가 표시됩니다.

2. 사용자는 해당 클라우드 디렉토리 사용자 인증 정보(예: 이메일 또는 사용자 이름 및 비밀번호)를 입력합니다.

3. 인증 정보가 유효성 검증되고 MFA 양식이 리턴됩니다. 이 양식에서는 사용자에게 이메일을 통해 발송된 코드를 붙여넣도록 요청합니다.

4. 사용자는 해당 이메일 주소로 일회성 패스코드를 수신한 후 기본 MFA UI에 입력합니다.

5. MFA 코드가 유효성 검증되고 권한 코드가 포함된 클라이언트 앱으로 경로 재지정된 후 OAuth 2 플로우로 계속 진행됩니다.


</br>

## MFA 구성
{: #configuration}

{{site.data.keyword.appid_short_notm}} MFA는 로그인 위젯을 통해 클라우드 디렉토리 사용자에 대한 OAuth 2.0 권한 코드 플로우의 일부로 지원됩니다.
{: shortdesc}

GUI를 통해 MFA를 구성하려면 [클라우드 디렉토리](cloud-directory.html)를 참조하십시오.
{: note}

### API를 사용하여 구성

관리 API를 사용하여 MFA를 구성할 수 있습니다.
{: shortdesc}

**시작하기 전에**

다음과 같은 전제조건이 준비되어 있어야 합니다.

* {{site.data.keyword.appid_short_notm}} 인스턴스의 테넌트 ID. 이 ID는 대시보드의 **서비스 인증 정보** 섹션에서 찾을 수 있습니다.
* IAM(Identity and Access Management) 토큰. IAM 토큰을 얻는 방법에 대한 도움말은 [IAM 문서](/docs/iam/apikey_iamtoken.html)를 참조하십시오.


1. MFA 구성이 포함된 `/config/mfa` 엔드포인트에 대한 PUT 요청을 작성하여 `isActive`를 `true`로 설정함으로써 MFA를 사용으로 설정하십시오.

  헤더:
  ```
  PUT {management-url}/management/v4/{tenantId}/config/mfa
       Host: <management-server-url>
       Authorization: Bearer <IAM_TOKEN>
       Content-Type: application/json
  ```
  {: pre}

  본문:
  ```
   {
       "isActive": true
   }
  ```
  {: pre}

  요청 예제:
  ```
  $ curl -X PUT
    --header 'Content-Type: application/json'
    --header 'Accept: application/json'
    --header 'Authorization: Bearer <IAM_TOKEN>'
    -d '{
          "isActive": true
      }'
    }'
    '{management-url}/management/v4/{tenantId}/config/mfa'
  ```
  {: screen}

2. MFA 구성이 포함된 `/mfa/channels/{channelType}` 엔드포인트에 대한 PUT 요청을 작성하여 MFA 채널을 사용으로 설정하십시오. `isActive`를 `true`로 설정하면 MFA 채널이 사용으로 설정됩니다.

  헤더:
  ```
  PUT /management/v4/{tenantId}/mfa/channels/{channelType}
       Host: <management-server-url>
       Authorization: Bearer <IAM_TOKEN>
       Content-Type: application/json
  ```
  {: pre}

  <table>
    <thead>
      <th colspan=3>지원되는 채널 유형</th>
    </thead>
    <tbody>
      <tr>
        <td>`email`</td>
      </tr>
    </tbody>
  </table>

  본문:
  ```
   {
       "isActive": true
   }
  ```
  {: pre}

  요청 예제:
  ```
  $ curl -X PUT
    --header 'Content-Type: application/json'
    --header 'Accept: application/json'
    --header 'Authorization: Bearer <IAM_TOKEN>'
    -d '{
          "isActive": true
      }'
    }'
    '{management-url}/management/v4/{tenantId}/mfa/channels/{channelType}'
  ```
  {: screen}

</br>
