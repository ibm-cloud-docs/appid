---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-10"

keywords: Authentication, authorization, identity, app security, secure, directory, registry, passwords, languages, lockout

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

# 이메일 사용자 정의
{: #cd-types}

사용자가 애플리케이션과 상호작용할 때 응답을 전송하거나 검증을 요청할 수 있습니다. {{site.data.keyword.appid_short_notm}}는 상호작용에 사용할 수 있는 기본 템플리트를 제공합니다. 또한 템플리트를 안내서로 사용하여 브랜드에 맞게 메시징을 사용자 정의할 수 있습니다.
{: shortdesc}

{{site.data.keyword.appid_short_notm}}는 <a href="https://www.sendgrid.com" target="_blank">SendGrid <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 메일 전달 서비스로 사용합니다. 모든 이메일은 단일 SendGrid 계정으로 발송됩니다.
{: note}

## 이메일 템플리트
{: #cd-messages}

사용자에게 메시지를 전송하는 경우 다음과 같은 템플리트의 조합을 사용할 수 있습니다. 또는 템플리트를 편집하여 메시지를 사용자 정의할 수 있습니다.
{: shortdesc}

다음 메시지 유형 이외에 [SSO](/docs/services/appid?topic=appid-cd-sso#cd-sso) 및 [MFA](/docs/services/appid?topic=appid-cd-mfa#cd-mfa) 템플리트도 활용할 수 있습니다.
{: tip}

추가로 사용자 정의하려면 메시지에 매개변수를 사용할 수 있습니다. 모든 메시지 유형에서 사용할 수 있는 매개변수를 확인하려면 다음 표를 참조하십시오.

<table>
  <tr>
    <th colspan=2><img src="images/idea.png" alt="자세한 정보 아이콘"/> 모든 메시지 매개변수 </th>
  </tr>
  <tr>
    <td><code>%{display.logo}</code></td>
    <td> 로그인 위젯에 대해 구성한 이미지를 표시합니다.</td>
  </tr>
  <tr>
    <td><code>%{user.displayName}</code></td>
    <td> 사용자가 앱과 상호작용할 때 사용하도록 선택한 화면 이름을 표시합니다.</td>
  </tr>
  <tr>
    <td><code>%{user.email}</code></td>
    <td> 사용자의 등록된 이메일 주소를 표시합니다.</td>
  </tr>
  <tr>
    <td><code>%{user.username}</code></td>
    <td> 인증 방법이 사용자 이름 및 비밀번호로 설정된 경우 사용자의 지정된 사용자 이름을 표시합니다. </td>
  </tr>
  <tr>
    <td><code>%{user.firstName}</code></td>
    <td> 사용자의 지정된 이름을 표시합니다. </td>
  </tr>
  <tr>
    <td><code>%{user.formattedName}</code></td>
    <td> 사용자의 전체 이름을 표시합니다. </td>
  </tr>
  <tr>
    <td><code>%{user.lastName}</code></td>
    <td> 사용자의 지정된 성을 표시합니다. </td>
  </tr>
</table>


### 이메일: 환영
{: #cd-messages-welcome}

사용자가 애플리케이션에 등록할 때 해당 사용자가 앱을 사용하게 된 것을 환영하는 메시지를 발송할 수 있습니다. 
{: shortdesc}

1. 서비스 대시보드의 **워크플로우 템플리트 > 환영 이메일** 탭으로 이동하십시오.

2. **환영 이메일**을 **사용**으로 설정하십시오.

3. 메시지의 컨텐츠를 사용자 정의하십시오. UI를 사용하여 매개변수를 추가하고 이미지를 삽입할 수 있습니다. 메시지의 [언어](/docs/services/appid?topic=appid-cd-messages#cd-languages)를 변경하기 위해 <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">API <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 사용하여 언어를 설정할 수 있습니다. 하지만 메시지의 컨텐츠 및 번역은 사용자의 책임입니다. 메시지에서 사용할 수 있는 표의 목록 및 발송할 수 있는 기타 모든 메시지를 확인하려면 다음 표를 참조하십시오. 사용자가 해당 매개변수를 통해 가져오는 정보를 제공하지 않을 경우 공백으로 표시됩니다.

4. **저장**을 클릭하십시오.


### 이메일: 검증
{: #cd-messages-verification}

사용자가 이메일을 사용하여 애플리케이션에 등록할 때 해당 사용자에게 ID를 확인하도록 요청하는 이메일을 발송할 수 있습니다. 검증을 요청하여 앱에 등록할 수 있는 허위 계정의 수를 제한할 수 있습니다. 사용자가 이메일을 검증할 때까지 앱에 대한 액세스를 제한하거나 프로파일을 작성하는 사용자를 관리하는 방법으로 사용할 수 있습니다.
{: shortdesc}

{{site.data.keyword.appid_short_notm}} 대시보드 또는 사용자 작성 API를 통해 수동으로 추가된 사용자의 경우 이 이메일을 자동으로 수신하지 않습니다.
{: note}


1. 서비스 대시보드의 **워크플로우 템플리트 > 이메일 검증** 탭으로 이동하십시오.

2. **이메일 검증**을 **사용**으로 설정하십시오.

3. **사용자가 먼저 해당 이메일 주소를 확인하지 않고 앱에 사인인할 수 있도록 허용**을 **예**로 설정하십시오. 예로 설정하면 사용자가 등록한 후 해당 이메일 주소를 확인하기 전에 애플리케이션과 상호작용할 수 있습니다. 기본 설정은 아니오입니다.

4. 메시지의 컨텐츠를 사용자 정의하십시오. UI를 사용하여 매개변수를 추가하고 이미지를 삽입할 수 있습니다. 메시지의 [언어](/docs/services/appid?topic=appid-cd-messages#cd-languages)를 변경하기 위해 <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">API <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 사용하여 언어를 설정할 수 있습니다. 하지만 메시지의 컨텐츠 및 번역은 사용자의 책임입니다. 메시지에서 사용할 수 있는 다양한 매개변수를 확인하려면 다음 표를 참조하십시오. 사용자가 해당 매개변수를 통해 가져오는 정보를 제공하지 않을 경우 공백으로 표시됩니다.

  <table>
    <tr>
      <th colspan=2><img src="images/idea.png" alt="자세한 정보 아이콘"/> 메시지 매개변수 검증</th>
    </tr>
    <tr>
      <td><code>%{linkExpiration.hours}</code></td>
      <td> 링크가 유효한 기간(시)을 표시합니다. </td>
    </tr>
    <tr>
      <td><code>%{linkExpiration.minutes}</code></td>
      <td> 링크가 유효한 기간(분)을 표시합니다. </td>
    </tr>
    <tr>
      <td><code>%{verify.code}</code></td>
      <td> 일회성 확인 URL을 표시합니다. </td>
    </tr>
    <tr>
      <td><code>%{verify.link}</code></td>
      <td> 설정에 지정한 조치 URL을 표시합니다. </td>
    </tr>
  </table>

  [환영 메시지](/docs/services/appid?topic=appid-cd-messages#cd-messages-welcome) 섹션에 나열된 메시지 매개변수를 사용할 수도 있습니다.
  {: tip}

5. 조치 URL의 만기 시간을 정의하십시오. URL 만기는 검증 링크가 만료되기 전에 사용자가 조치를 완료해야 하는 분 단위의 시간입니다. 이 설정은 비밀번호 재설정 링크가 유효한 기간에도 영향을 미칩니다.
 
6. **감사 페이지 URL** 상자에 사용자가 해당 이메일을 확인한 후에 표시할 페이지의 URL을 입력하십시오. 이 필드를 공백으로 두도록 선택하는 경우 {{site.data.keyword.appid_short_notm}} 기본 페이지가 표시됩니다.

7. **저장**을 클릭하십시오. 


### 이메일: 비밀번호 재설정
{: #cd-messages-reset}

사용자가 앱과 상호작용할 때 비밀번호를 잊어버리거나 비밀번호를 업데이트해야 할 수도 있습니다. 요청에 대한 이메일 응답을 사용자 정의할 수 있습니다. 사용자가 비밀번호 변경을 요청하는 경우 이 이메일의 링크를 클릭할 때까지 해당 비밀번호가 변경되지 않고 유지됩니다.
{: shortdesc}


1. 서비스 대시보드의 **워크플로우 템플리트 > 비밀번호 재설정** 탭으로 이동하십시오.

2. **비밀번호 찾기 이메일**을 **사용**으로 설정하십시오.

3. 메시지의 컨텐츠를 사용자 정의하십시오. UI를 사용하여 매개변수를 추가하고 이미지를 삽입할 수 있습니다. 메시지의 [언어](/docs/services/appid?topic=appid-cd-messages#cd-languages)를 변경하기 위해 <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">API <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 사용하여 언어를 설정할 수 있습니다. 하지만 메시지의 컨텐츠 및 번역은 사용자의 책임입니다. 메시지에서 사용할 수 있는 다양한 매개변수를 확인하려면 다음 표를 참조하십시오. 사용자가 해당 매개변수를 통해 가져오는 정보를 제공하지 않을 경우 공백으로 표시됩니다.

  <table>
    <tr>
      <th colspan=2><img src="images/idea.png" alt="자세한 정보 아이콘"/> 비밀번호 찾기 매개변수</th>
    </tr>
    <tr>
      <td><code>%{linkExpiration.hours}</code></td>
      <td> 링크가 유효한 기간(시)을 표시합니다.</td>
    </tr>
    <tr>
      <td><code>%{linkExpiration.minutes}</code></td>
      <td>링크가 유효한 기간(분)을 표시합니다.</td>
    </tr>
    <tr>
      <td><code>%{resetPassword.code}</code></td>
      <td> URL의 일부로 일회성 패스코드를 표시합니다. 이는 각 개인이 서로 다른 코드를 보유함을 의미합니다. 예: `https://us-south.appid.cloud.ibm.com/wfm/verify/6574839563478`</td>
    </tr>
    <tr>
      <td><code>%{resetPassword.link}</code></td>
      <td> 비밀번호를 재설정하기 위해 사용자가 클릭하는 링크를 표시합니다.</td>
    </tr>
  </table>

  [환영 메시지](/docs/services/appid?topic=appid-cd-messages#cd-messages-welcome) 섹션에 나열된 메시지 매개변수를 사용할 수도 있습니다.
  {: tip}

4. 조치 URL의 만기 시간을 정의하십시오. URL 만기는 검증 링크가 만료되기 전에 사용자가 조치를 완료해야 하는 분 단위의 시간입니다. 이 설정은 비밀번호 재설정 링크가 유효한 기간에도 영향을 미칩니다.
 
5. **비밀번호 재설정 페이지 URL** 상자에 사용자가 해당 이메일을 확인한 후에 표시할 페이지의 URL을 입력하십시오. 이 필드를 공백으로 두도록 선택하는 경우 {{site.data.keyword.appid_short_notm}} 기본 페이지가 표시됩니다.

6. **저장**을 클릭하십시오.


### 이메일: 비밀번호 변경
{: #cd-messages-password-change}

비밀번호가 업데이트되면 사용자에게 알릴 수 있습니다. 알림은 사용자가 비밀번호 변경을 요청하지 않은 경우에 유용합니다. 계정의 보안을 재설정하기 위한 적절한 단계를 수행할 수 있습니다.
{: shortdesc}

1. 서비스 대시보드의 **워크플로우 템플리트 > 비밀번호 변경** 탭으로 이동하십시오.

2. **비밀번호 변경 이메일**을 **사용**으로 설정하십시오.

3. 메시지의 컨텐츠를 사용자 정의하십시오. UI를 사용하여 매개변수를 추가하고 이미지를 삽입할 수 있습니다. 메시지의 [언어](/docs/services/appid?topic=appid-cd-messages#cd-languages)를 변경하기 위해 <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">API <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 사용하여 언어를 설정할 수 있습니다. 하지만 메시지의 컨텐츠 및 번역은 사용자의 책임입니다. 메시지에서 사용할 수 있는 다양한 매개변수를 확인하려면 다음 표를 참조하십시오. 사용자가 해당 매개변수를 통해 가져오는 정보를 제공하지 않을 경우 공백으로 표시됩니다.

  <table>
    <tr>
      <th colspan=2><img src="images/idea.png" alt="자세한 정보 아이콘"/> 비밀번호 변경 매개변수</th>
    </tr>
    <tr>
      <td><code>%{passwordChangeInfo.time}</code></td>
      <td> 새 비밀번호가 적용된 시간을 표시합니다. </td>
    </tr>
    <tr>
      <td><code>%{passwordChangeInfo.ipAddress}</code></td>
      <td> 비밀번호 변경이 요청된 IP 주소를 표시합니다. </td>
    </tr>
  </table>

  [환영 메시지](/docs/services/appid?topic=appid-cd-messages#cd-messages-welcome) 섹션에 나열된 메시지 매개변수를 사용할 수도 있습니다.
  {: tip}

4. **저장**을 클릭하십시오.




## 사용자 정의 이메일 발신인 사용
{: #cd-custom-email}

{{site.data.keyword.appid_short_notm}}를 사용하는 경우 사용자 정의 확장점을 정의하여 Cloud Directory 이메일 메시지를 발송할 수 있습니다. 확장점을 정의하여 이메일이 발송되는 방법을 완전히 제어하고 고유한 도메인 이름을 사용할 수 있습니다. 기본적으로 {{site.data.keyword.appid_short_notm}}에서는 <a href="https://www.sendgrid.com" target="_blank">SendGrid <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 메일 전달 서비스로 사용합니다.
 {: shortdesc}

다음과 같은 이유로 사용자 정의 이메일 발신인을 사용할 수 있습니다.

- **개인화된 도메인**
사용자 정의 이메일 디스패처를 사용하여 이메일 메시지가 발송되는 방법을 완전히 제어할 수 있습니다. 특히 이메일 도메인을 사용자 정의할 수 있습니다. 그러면 이메일이 스팸으로 필터링되는 확률을 줄일 수 있습니다. 또한 앱 사용자의 브랜드 경험을 더욱 향상시킬 수 있습니다.

- **인사이트 및 문제점 해결**
이메일 제공자로부터 이메일을 연 사용자 수 또는 전달되지 않은 메시지 등의 인사이트를 얻을 수 있습니다. 개별 메시지를 추적하고 전체적인 통계를 확인할 수 있기 때문에 이 인사이트를 통해 문제를 해결할 수 있습니다.

확장점이 구성되면 이메일 메시지를 발송해야 할 때마다 {{site.data.keyword.appid_short_notm}}에서 해당 확장점을 호출합니다. 확장점에는 이메일 본문의 최종 컨텐츠를 포함하여 메시지에 대한 모든 정보가 포함되어 있습니다.



### 사용자 정의 발신인 구성
{: #cd-messages-configure-custom-sender}

사용자 정의 이메일 발신인을 구성하려면 Cloud Directory <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.set_cloud_directory_email_dispatcher" target="_blank">관리 API</a>를 사용해야 합니다.


1. URL을 제공하십시오. 추가적으로 권한 정보를 제공할 수 있습니다. 지원되는 권한 유형은 `기본 권한` 또는 `상수 권한 헤더 값`입니다.

  올바른 구성 예제는 다음과 같습니다.
  ```
  {
    "custom": {
      "url": "https://example.com/send_mail"
    }
  }
  ```
  {: screen}

  ```
  {
    "custom": {
      "url": "https://example.com/send_mail",
      "authorization": {
        "type": "basic",
        "username": "username",
        "password": "password"
      }
    }
  }
  ```
  {: screen}

  ```
  {
    "custom": {
      "url": "https://example.com/send_mail",
      "authorization": {
        "type": "value",
        "value": "myApiKey"
      }
    }
  }
  ```
  {: screen}

2. 요청을 게시하기 위해 청취할 수 있는 확장점을 구성하십시오. 이 엔드포인트에서는 {{site.data.keyword.appid_short_notm}}로부터 수신되는 페이로드를 읽어들이고 사용자 정의 이메일 발신인을 사용하여 이메일을 발송할 수 있어야 합니다.

3. {{site.data.keyword.appid_short_notm}}에서 발송하는 본문의 형식은 `{"jws": "jws-format-string"}`입니다. 페이로드를 디코딩 및 확인한 후에는 해당 컨텐츠가 JSON 문자열이 됩니다.

  ```
  {
    "tenant": "tenant-id",
      "iss" : "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61",
      "iat": 1539173126,
      "jti": "uniq-id",
      "message": {
        "to": "your@mail.com",
          "from": {
            "name": "My Awesome Service",
              "address": "no-reply@company.com"
        },
          "replyTo": {
            "name": "My Awesome Service",
              "address": "yes-reply@company.com"
        },
          "subject": "Welcome to My Awesome Service",
          "body": "<p>Hello<p><br/><p>Thanks for signing up John Doe</p>"
    }
  }
  ```
  {: screen}

  <table>
    <tr>
      <th>변수</th>
      <th>설명</th>
    </tr>
    <tr>
      <td><code> tenant </code></td>
      <td>{{site.data.keyword.appid_short_notm}} 인스턴스의 테넌트 ID입니다.</td>
    </tr>
    <tr>
      <td><code> iat </code></td>
      <td>전송된 메시지의 시간소인입니다.</td>
    </tr>
    <tr>
      <td><code> iss </code></td>
      <td>JWS 토큰을 발행한 프린시펄 또는 {{site.data.keyword.appid_short_notm}} 인스턴스입니다.</td>
    </tr>
    <tr>
      <td><code>jti</code></td>
      <td>고유 트랜잭션 ID입니다.</td>
    </tr>
    <tr>
      <td><code>message: to</code></td>
      <td>메시지 수신인의 이메일 주소입니다.</td>
    </tr>
    <tr>
      <td><code>message: from</code> </br><code>name</code> </br><code>address</code></td>
      <td></br>메시지 발신인의 이름입니다. </br>발신인의 이메일 주소입니다.</td>
    </tr>
    <tr>
      <td><code>선택사항: message: reply to</code></br><code>name</code></br><code>address</code></td>
      <td></br>응답 이메일 주소에 첨부되는 이름입니다. </br>사용자가 응답할 수 있는 이메일 주소입니다.</td>
    </tr>
  </table>

  응답 상태 코드를 검사하여 요청이 정상적으로 완료되었는지 확인할 수 있습니다. 200 - 299 범위의 값은 모두 성공으로 간주됩니다. 다른 응답을 수신하는 경우 다시 요청을 시도하십시오.
  {: tip}

4. {{site.data.keyword.appid_short_notm}}에서 발송되는 모든 HTTP 페이로드는 비대칭 키 쌍을 사용하여 JWS 표준에 따라 자동으로 서명됩니다.
모든 {{site.data.keyword.appid_short_notm}} 인스턴스에 대해 다른 인스턴스에서 공유되지 않는 개인 및 공개 키가 생성됩니다. 개인 키는 HTTP 페이로드에 서명하기 위해 사용되며, 공개 키를 사용하여 해당 페이로드가 {{site.data.keyword.appid_short_notm}}에서 생성되고 서드파티에 의해 변경되지 않았는지 확인할 수 있습니다(<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#!/Authorization_Server_V4/publicKeys" target="_blank">공개 키 엔드포인트</a>).

5. 확장점 코드 예제(JavaScript)
  ```
  const sgMail = require('@sendgrid/mail');
  const {promisify} = require('bluebird');
  const request = promisify(require('request'));
  const jwtVerify = promisify(require('jsonwebtoken').verify);
  const jwtDecode = require('jsonwebtoken').decode;
  const jwkToPem = require('jwk-to-pem');

  async function obtainPublicKeys() {
  	// Your {{site.data.keyword.appid_short_notm}} instance tenant ID
  	const tenantId = '<TENANT-ID>';

  	// Send request to {{site.data.keyword.appid_short_notm}}'s public keys endpoint
  	const keysOptions = {
  		method: 'GET',
  		url: `https://<REGION>.appid.cloud.ibm.com/oauth/v4/${tenantId}/publickeys`
  	};
  	const keysResponse = await request(keysOptions);
  	return JSON.parse(keysResponse.body).keys;
  }

  async function verifySignature(keysArray, kid, jws) {
  	const keyJson = keysArray.find(key => key.kid === kid);
  	if (keyJson) {
  		const pem = jwkToPem(keyJson);
  		await jwtVerify(jws, pem);
  		return;
  	}
  	throw new Error ("Unable to verify signature");
  }

  async function verifyAndSendMail(jws) {
  	// The API key for Sendgrid
  	const sgApiKey = '<SENDGRID-API-KEY>';

  	// Init Sendgrind
  	sgMail.setApiKey(sgApiKey);

  	// Decode message to get information
  	const data = jwtDecode(jws, {complete: true});

  	// Extract kid from header
  	const kid = data.header.kid;

  	const keysArray = await obtainPublicKeys();

  	// Verify the signature of the payload with the public keys
  	await verifySignature(keysArray, kid ,jws);

  	// Send the email with Your Sendgrid account
  	const message = data.payload.message;
  	const msg = {
  		to: message.to,
  		from: message.from.address,
  		subject: message.subject,
  		html: message.body,
  	};
  	console.log(`Sending email to ${message.to}`);
  	let sendgridResponse = await sgMail.send(msg);

  	return {result : 'email_sent',sendgridResponse};
  }
  ```
  {: screen}

6. 이메일 디스패처를 테스트하여 구성이 올바르게 설정되었는지 확인하십시오. <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Config/post_email_dispatcher_test" target="_blank">테스트 API</a>를 사용하여 구성된 사용자 정의 이메일 발신인에 대한 요청을 트리거하십시오.

완전하게 작동하는 예는 <a href="https://www.ibm.com/cloud/blog/use-ibm-cloud-app-id-and-your-email-provider-to-brand-mails-sent-to-app-users" target="_blank">{{site.data.keyword.appid_full}}를 통해 발송되는 메일에 대해 고유한 제공자 사용</a>을 참조하십시오. 



## 지원되는 언어
{: #cd-languages}

<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">언어 관리 API <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 사용하여 사용자 통신이 작성될 수 있는 언어를 설정할 수 있습니다. 그러나 영어만 즉시 사용할 수 있습니다. 사용자는 메시지를 번역할 책임이 있습니다. API를 사용하여 구성을 설정한 후 템플리트 텍스트를 변경할 수 있도록 GUI가 업데이트됩니다.
{: shortdesc}

<table>
  <col width="20%">
  <col width="25%">
  <col width="35%">
  <tr>
    <th>코드</th>
    <th>언어</th>
    <th>Region</th>
  </tr>
  <tr>
    <td><code>af-ZA</code></td>
    <td>아프리칸스어</td>
    <td>남아프리카</td>
  </tr>
  <tr>
    <td><code>sq-AL</code></td>
    <td>알바니아어</td>
    <td>알바니아</td>
  </tr>
  <tr>
    <td><code>am-ET</code></td>
    <td>암하라어</td>
    <td>에티오피아</td>
  </tr>
  <tr>
    <td><code>ar-DZ</code></td>
    <td>아랍어</td>
    <td>알제리</td>
  </tr>
  <tr>
    <td><code>ar-BH</code></td>
    <td>아랍어</td>
    <td>바레인</td>
  </tr>
  <tr>
    <td><code>ar-EG</code></td>
    <td>아랍어</td>
    <td>이집트</td>
  </tr>
  <tr>
    <td><code>ar-IQ</code></td>
    <td>아랍어</td>
    <td>이라크</td>
  </tr>
  <tr>
    <td><code>ar-JO</code></td>
    <td>아랍어</td>
    <td>요르단</td>
  </tr>
  <tr>
    <td><code>ar-KW</code></td>
    <td>아랍어</td>
    <td>쿠웨이트</td>
  </tr>
  <tr>
    <td><code>ar-LB</code></td>
    <td>아랍어</td>
    <td>레바논</td>
  </tr>
  <tr>
    <td><code>ar-LY</code></td>
    <td>아랍어</td>
    <td>리비아</td>
  </tr>
  <tr>
    <td><code>ar-MR</code></td>
    <td>아랍어</td>
    <td>모리타니아</td>
  </tr>
  <tr>
    <td><code>ar-MA</code></td>
    <td>아랍어</td>
    <td>모로코</td>
  </tr>
  <tr>
    <td><code>ar-OM</code></td>
    <td>아랍어</td>
    <td>오만</td>
  </tr>
  <tr>
    <td><code>ar-QA</code></td>
    <td>아랍어</td>
    <td>카타르</td>
  </tr>
  <tr>
    <td><code>ar-SA</code></td>
    <td>아랍어</td>
    <td>사우디아라비아</td>
  </tr>
  <tr>
    <td><code>ar-SY</code></td>
    <td>아랍어</td>
    <td>시리아</td>
  </tr>
  <tr>
    <td><code>ar-YE</code></td>
    <td>아랍어</td>
    <td>튀니지</td>
  </tr>
  <tr>
    <td><code>ar-AE</code></td>
    <td>아랍어</td>
    <td>아랍에미리트</td>
  </tr>
  <tr>
    <td><code>ar-YE</code></td>
    <td>아랍어</td>
    <td>예멘</td>
  </tr>
  <tr>
    <td><code>hy-AM</code></td>
    <td>아르메니아어</td>
    <td>아르메니아</td>
  </tr>
  <tr>
    <td><code>as-IN</code></td>
    <td>아삼어</td>
    <td>인도</td>
  </tr>
  <tr>
    <td><code>az-AZ</code></td>
    <td>아제르바이잔어</td>
    <td>아제르바이잔</td>
  </tr>
  <tr>
    <td><code>eu-ES</code></td>
    <td>바스크어</td>
    <td>스페인</td>
  </tr>
  <tr>
    <td><code>be-BY</code></td>
    <td>벨라루스어</td>
    <td>벨라루스</td>
  </tr>
  <tr>
    <td><code>bn-BD</code></td>
    <td>벵골어</td>
    <td>방글라데시</td>
  </tr>
  <tr>
    <td><code>be-BY</code></td>
    <td>벨라루스어</td>
    <td>벨라루스</td>
  </tr>
  <tr>
    <td><code>bn-BD</code></td>
    <td>벵골어</td>
    <td>방글라데시</td>
  </tr>
  <tr>
    <td><code>bn-IN</code></td>
    <td>벵골어</td>
    <td>인도</td>
  </tr>
  <tr>
    <td><code>bs-Latn-BA</code></td>
    <td>보스니아어</td>
    <td>보스니아</td>
  </tr>
  <tr>
    <td><code>bg-BG</code></td>
    <td>불가리아어</td>
    <td>불가리아</td>
  </tr>
  <tr>
    <td><code>my-MM</code></td>
    <td>버마어</td>
    <td>미얀마</td>
  </tr>
  <tr>
    <td><code>ca-ES</code></td>
    <td>카탈로니아어</td>
    <td>스페인</td>
  </tr>
  <tr>
    <td><code>zh-Hans-CN</code></td>
    <td>중국어</td>
    <td>중국</td>
  </tr>
  <tr>
    <td><code>zh-Hans-SG</code></td>
    <td>중국어</td>
    <td>싱가포르</td>
  </tr>
  <tr>
    <td><code>zh-Hant-HK</code></td>
    <td>대만어</td>
    <td>홍콩 특별 행정구</td>
  </tr>
  <tr>
    <td><code>zh-Hant-MO</code></td>
    <td>대만어</td>
    <td>중국의 마카오 S.A.R.</tr>
  <tr>
    <td><code>zh-Hant-TW</code></td>
    <td>대만어</td>
    <td>대만</td>
  </tr>
  <tr>
    <td><code>hr-HR</code></td>
    <td>크로아티아어</td>
    <td>크로아티아</td>
  </tr>
  <tr>
    <td><code>cs-CZ</code></td>
    <td>체코어</td>
    <td>체코 공화국</td>
  </tr>
  <tr>
    <td><code>da-DK</code></td>
    <td>덴마크어</td>
    <td>덴마크</td>
  </tr>
  <tr>
    <td><code>nl-BE</code></td>
    <td>네덜란드어</td>
    <td>벨기에</td>
  </tr>
  <tr>
    <td><code>nl-NL</code></td>
    <td>네덜란드어</td>
    <td>네덜란드</td>
  </tr>
  <tr>
    <td><code>en-AU</code></td>
    <td>영어</td>
    <td>오스트레일리아</td>
  </tr>
  <tr>
    <td><code>eu-BE</code></td>
    <td>영어</td>
    <td>벨기에</td>
  </tr>
  <tr>
    <td><code>en-CM</code></td>
    <td>영어</td>
    <td>카메룬</td>
  </tr>
  <tr>
    <td><code>eu-CA</code></td>
    <td>영어</td>
    <td>캐나다</td>
  </tr>
  <tr>
    <td><code>en-GH</code></td>
    <td>영어</td>
    <td>가나</td>
  </tr>
  <tr>
    <td><code>eu-HK</code></td>
    <td>영어</td>
    <td>홍콩 특별 행정구</td>
  </tr>
  <tr>
    <td><code>en-IN</code></td>
    <td>영어</td>
    <td>인도</td>
  </tr>
  <tr>
    <td><code>en-IE</code></td>
    <td>영어</td>
    <td>아일랜드</td>
  </tr>
  <tr>
    <td><code>en-KE</code></td>
    <td>영어</td>
    <td>케냐</td>
  </tr>
  <tr>
    <td><code>en-MU</code></td>
    <td>영어</td>
    <td>모리셔스</td>
  </tr>
  <tr>
    <td><code>en-NZ</code></td>
    <td>영어</td>
    <td>뉴질랜드</td>
  </tr>
  <tr>
    <td><code>en-NG</code></td>
    <td>영어</td>
    <td>나이지리아</td>
  </tr>
  <tr>
    <td><code>en-PH</code></td>
    <td>영어</td>
    <td>필리핀</td>
  </tr>
  <tr>
    <td><code>en-SG</code></td>
    <td>영어</td>
    <td>싱가포르</td>
  </tr>
  <tr>
    <td><code>en-ZA</code></td>
    <td>영어</td>
    <td>남아프리카</td>
  </tr>
  <tr>
    <td><code>en-TZ</code></td>
    <td>영어</td>
    <td>탄자니아</td>
  </tr>
  <tr>
    <td><code>en-GB</code></td>
    <td>영어</td>
    <td>영국</td>
  </tr>
  <tr>
    <td><code>en-US</code></td>
    <td>영어</td>
    <td>미국</td>
  </tr>
  <tr>
    <td><code>en-ZM</code></td>
    <td>영어</td>
    <td>잠비아</td>
  </tr>
  <tr>
    <td><code>en</code></td>
    <td>영어</td>
    <td> </td>
  </tr>
  <tr>
    <td><code>et-EE</code></td>
    <td>에스토니아어</td>
    <td>에스토니아</td>
  </tr>
  <tr>
    <td><code>fil-PH</code></td>
    <td>필리핀어</td>
    <td>필리핀</td>
  </tr>
  <tr>
    <td><code>fi-FI</code></td>
    <td>핀란드어</td>
    <td>핀란드</td>
  </tr>
  <tr>
    <td><code>fr-DZ</code></td>
    <td>프랑스어</td>
    <td>알제리</td>
  </tr>
  <tr>
    <td><code>fr-CM</code></td>
    <td>프랑스어</td>
    <td>카메룬</td>
  </tr>
  <tr>
    <td><code>fr-CD</code></td>
    <td>프랑스어</td>
    <td>콩고민주공화국</td>
  </tr>
  <tr>
    <td><code>fr-BE</code></td>
    <td>프랑스어</td>
    <td>벨기에</td>
  </tr>
  <tr>
    <td><code>fr-CA</code></td>
    <td>프랑스어</td>
    <td>캐나다</td>
  </tr>
  <tr>
    <td><code>fr-FR</code></td>
    <td>프랑스어</td>
    <td>프랑스</td>
  </tr>
  <tr>
    <td><code>fr-CI</code></td>
    <td>프랑스어</td>
    <td>코트디부아르</td>
  </tr>
  <tr>
    <td><code>fr-LU</code></td>
    <td>프랑스어</td>
    <td>룩셈부르크</td>
  </tr>
  <tr>
    <td><code>fr-MR</code></td>
    <td>프랑스어</td>
    <td>모리타니아</td>
  </tr>
  <tr>
    <td><code>fr-MU</code></td>
    <td>프랑스어</td>
    <td>모리셔스</td>
  </tr>
  <tr>
    <td><code>fr-MA</code></td>
    <td>프랑스어</td>
    <td>모로코</td>
  </tr>
  <tr>
    <td><code>fr-SN</code></td>
    <td>프랑스어</td>
    <td>세네갈</td>
  </tr>
  <tr>
    <td><code>fr-CH</code></td>
    <td>프랑스어</td>
    <td>스위스</td>
  </tr>
  <tr>
    <td><code>fr-TN</code></td>
    <td>프랑스어</td>
    <td>튀니지</td>
  </tr>
  <tr>
    <td><code>gl-ES</code></td>
    <td>갈리시아어</td>
    <td>스페인</td>
  </tr>
  <tr>
    <td><code>lg-UG</code></td>
    <td>간다어</td>
    <td>우간다</td>
  </tr>
  <tr>
    <td><code>ka-GE</code></td>
    <td>그루지야어</td>
    <td>조지아</td>
  </tr>
  <tr>
    <td><code>de-AT</code></td>
    <td>독일어</td>
    <td>오스트리아</td>
  </tr>
  <tr>
    <td><code>de-DE</code></td>
    <td>독일어</td>
    <td>독일</td>
  </tr>
  <tr>
    <td><code>de-LU</code></td>
    <td>독일어</td>
    <td>룩셈부르크</td>
  </tr>
  <tr>
    <td><code>de-CH</code></td>
    <td>독일어</td>
    <td>스위스</td>
  </tr>
  <tr>
    <td><code>el-GR</code></td>
    <td>그리스어</td>
    <td>그리스</td>
  </tr>
  <tr>
    <td><code>gu-IN</code></td>
    <td>구자라트어</td>
    <td>인도</td>
  </tr>
  <tr>
    <td><code>ha-NG</code></td>
    <td>하우사어</td>
    <td>나이지리아</td>
  </tr>
  <tr>
    <td><code>he-IL</code></td>
    <td>히브리어</td>
    <td>이스라엘</td>
  </tr>
  <tr>
    <td><code>hi-IN</code></td>
    <td>힌디어</td>
    <td>인도</td>
  </tr>
  <tr>
    <td><code>hu-HU</code></td>
    <td>헝가리어</td>
    <td>헝가리</td>
  </tr>
  <tr>
    <td><code>is-IS</code></td>
    <td>아이슬란드어</td>
    <td>아이슬란드</td>
  </tr>
  <tr>
    <td><code>ig-NG</code></td>
    <td>이그보어</td>
    <td>나이지리아</td>
  </tr>
  <tr>
    <td><code>id-ID</code></td>
    <td>인도네시아어</td>
    <td>인도네시아</td>
  </tr>
  <tr>
    <td><code>it-IT</code></td>
    <td>이탈리아어</td>
    <td>이탈리아</td>
  </tr>
  <tr>
    <td><code>it-CH</code></td>
    <td>이탈리아어</td>
    <td>스위스</td>
  </tr>
  <tr>
    <td><code>ja-JP</code></td>
    <td>일본어</td>
    <td>일본</td>
  </tr>
  <tr>
    <td><code>kn-IN</code></td>
    <td>칸나다어</td>
    <td>인도</td>
  </tr>
  <tr>
    <td><code>kk-KZ</code></td>
    <td>카자흐어</td>
    <td>카자흐스탄</td>
  </tr>
  <tr>
    <td><code>km-KH</code></td>
    <td>크메르어</td>
    <td>캄보디아</td>
  </tr>
  <tr>
    <td><code>rw-RW</code></td>
    <td>킨야르완다어</td>
    <td>르완다</td>
  </tr>
  <tr>
    <td><code>kok-IN</code></td>
    <td>콩카니어</td>
    <td>인도</td>
  </tr>
  <tr>
    <td><code>ko-KR</code></td>
    <td>한국어</td>
    <td>대한민국</td>
  </tr>
  <tr>
    <td><code>lo-LA</code></td>
    <td>리투아니아어</td>
    <td>리투아니아</td>
  </tr>
  <tr>
    <td><code>lv-LV</code></td>
    <td>라트비아어</td>
    <td>라트비아</td>
  </tr>
  <tr>
    <td><code>lt-LT</code></td>
    <td>크메르어</td>
    <td>캄보디아</td>
  </tr>
  <tr>
    <td><code>mk-MK</code></td>
    <td>마케도니아어</td>
    <td>마케도니아</td>
  </tr>
  <tr>
    <td><code>ms-Latn-MY</code></td>
    <td>말레이어(라틴)</td>
    <td>말레이시아</td>
  </tr>
  <tr>
    <td><code>ml-IN</code></td>
    <td>말라얄람어</td>
    <td>인도</td>
  </tr>
  <tr>
    <td><code>mt-MT</code></td>
    <td>몰타어</td>
    <td>몰타</td>
  </tr>
  <tr>
    <td><code>mr-IN</code></td>
    <td>마라티어</td>
    <td>인도</td>
  </tr>
  <tr>
    <td><code>mn-Cyrl-MN</code></td>
    <td>몽골어(키릴)</td>
    <td>몽고</td>
  </tr>
  <tr>
    <td><code>ne-IN</code></td>
    <td>네팔어</td>
    <td>인도</td>
  </tr>
  <tr>
    <td><code>ne-NP</code></td>
    <td>네팔어</td>
    <td>네팔</td>
  </tr>
  <tr>
    <td><code>nb-NO</code></td>
    <td>노르웨이어(복말)</td>
    <td>노르웨이</td>
  </tr>
  <tr>
    <td><code>nn-NO</code></td>
    <td>노르웨이어(니노르스크)</td>
    <td>노르웨이</td>
  </tr>
  <tr>
    <td><code>or-IN</code></td>
    <td>오리야어(오디아어)</td>
    <td>인도</td>
  </tr>
  <tr>
    <td><code>om-ET</code></td>
    <td>오로모어</td>
    <td>에티오피아</td>
  </tr>
  <tr>
    <td><code>pl-PL</code></td>
    <td>폴란드어</td>
    <td>폴란드</td>
  </tr>
  <tr>
    <td><code>pt-AO</code></td>
    <td>포르투갈어</td>
    <td>앙골라</td>
  </tr>
  <tr>
    <td><code>pt-BR</code></td>
    <td>포르투갈어</td>
    <td>브라질</td>
  </tr>
  <tr>
    <td><code>pt-MO</code></td>
    <td>포르투갈어</td>
    <td>중국의 마카오 S.A.R.</td>
  </tr>
  <tr>
    <td><code>pt-MZ</code></td>
    <td>포르투갈어</td>
    <td>모잠비크</td>
  </tr>
  <tr>
    <td><code>pt-PT</code></td>
    <td>포르투갈어</td>
    <td>포르투갈</td>
  </tr>
  <tr>
    <td><code>pa-IN</code></td>
    <td>펀잡어</td>
    <td>인도</td>
  </tr>
  <tr>
    <td><code>ro-RO</code></td>
    <td>루마니아어</td>
    <td>루마니아</td>
  </tr>
  <tr>
    <td><code>ru-RU</code></td>
    <td>러시아어</td>
    <td>러시아</td>
  </tr>
  <tr>
    <td><code>sr-Cyrl-RS</code></td>
    <td>세르비아어(키릴)</td>
    <td>세르비아</td>
  </tr>
  <tr>
    <td><code>sr-Latn-ME</code></td>
    <td>세르비아어(라틴)</td>
    <td>몬테네그로</td>
  </tr>
  <tr>
    <td><code>sr-Latn-RS</code></td>
    <td>세르비아어(라틴)</td>
    <td>세르비아</td>
  </tr>
  <tr>
    <td><code>si-LK</code></td>
    <td>싱헐리즈어</td>
    <td>스리랑카</td>
  </tr>
  <tr>
    <td><code>sk-SK</code></td>
    <td>슬로바키아어</td>
    <td>슬로바키아</td>
  </tr>
  <tr>
    <td><code>sl-SI</code></td>
    <td>슬로베니아어</td>
    <td>슬로베니아</td>
  </tr>
  <tr>
    <td><code>es-AR</code></td>
    <td>스페인어</td>
    <td>아르헨티나</td>
  </tr>
  <tr>
    <td><code>es-BO</code></td>
    <td>스페인어</td>
    <td>볼리비아</td>
  </tr>
  <tr>
    <td><code>es-CL</code></td>
    <td>스페인어</td>
    <td>칠레</td>
  </tr>
  <tr>
    <td><code>es-CO</code></td>
    <td>스페인어</td>
    <td>콜롬비아</td>
  </tr>
  <tr>
    <td><code>es-CR</code></td>
    <td>스페인어</td>
    <td>코스타리카</td>
  </tr>
  <tr>
    <td><code>es-DO</code></td>
    <td>스페인어</td>
    <td>도미니카 공화국</td>
  </tr>
  <tr>
    <td><code>es-EC</code></td>
    <td>스페인어</td>
    <td>에콰도르</td>
  </tr>
  <tr>
    <td><code>es-SV</code></td>
    <td>스페인어</td>
    <td>엘살바도르</td>
  </tr>
  <tr>
    <td><code>es-GT</code></td>
    <td>스페인어</td>
    <td>과테말라</td>
  </tr>
  <tr>
    <td><code>es-HN</code></td>
    <td>스페인어</td>
    <td>온두라스</td>
  </tr>
  <tr>
    <td><code>es-MX</code></td>
    <td>스페인어</td>
    <td>멕시코</td>
  </tr>
  <tr>
    <td><code>es-NI</code></td>
    <td>스페인어</td>
    <td>니카라과</td>
  </tr>
  <tr>
    <td><code>es-PA</code></td>
    <td>스페인어</td>
    <td>파나마</td>
  </tr>
  <tr>
    <td><code>es-PY</code></td>
    <td>스페인어</td>
    <td>파라과이</td>
  </tr>
  <tr>
    <td><code>es-PE</code></td>
    <td>스페인어</td>
    <td>페루</td>
  </tr>
  <tr>
    <td><code>es-PR</code></td>
    <td>스페인어</td>
    <td>푸에토리코</td>
  </tr>
  <tr>
    <td><code>es-ES</code></td>
    <td>스페인어</td>
    <td>스페인</td>
  </tr>
  <tr>
    <td><code>es-US</code></td>
    <td>스페인어</td>
    <td>미국</td>
  </tr>
  <tr>
    <td><code>es-UY</code></td>
    <td>스페인어</td>
    <td>우루과이</td>
  </tr>
  <tr>
    <td><code>es-VE</code></td>
    <td>스페인어</td>
    <td>베네수엘라</td>
  </tr>
  <tr>
    <td><code>sw-KE</code></td>
    <td>스와힐리어</td>
    <td>케냐</td>
  </tr>
  <tr>
    <td><code>sw-TZ</code></td>
    <td>스와힐리어</td>
    <td>탄자니아</td>
  </tr>
  <tr>
    <td><code>sv-SE</code></td>
    <td>스웨덴어</td>
    <td>스웨덴</td>
  </tr>
  <tr>
    <td><code>ta-IN</code></td>
    <td>타밀어</td>
    <td>인도</td>
  </tr>
  <tr>
    <td><code>te-IN</code></td>
    <td>텔루구어</td>
    <td>인도</td>
  </tr>
  <tr>
    <td><code>th-TH</code></td>
    <td>태국어</td>
    <td>태국</td>
  </tr>
  <tr>
    <td><code>tr-TR</code></td>
    <td>터키어</td>
    <td>터키</td>
  </tr>
  <tr>
    <td><code>uk-UA</code></td>
    <td>우크라이나어</td>
    <td>우크라이나</td>
  </tr>
  <tr>
    <td><code>ur-IN</code></td>
    <td>우르두어</td>
    <td>인도</td>
  </tr>
  <tr>
    <td><code>ur-PK</code></td>
    <td>우르두어</td>
    <td>파키스탄</td>
  </tr>
  <tr>
    <td><code>uz-Cyrl-UZ</code></td>
    <td>우즈베크어(키릴)</td>
    <td>우즈베키스탄</td>
  </tr>
  <tr>
    <td><code>uz-Latn-UZ</code></td>
    <td>우즈베크어(라틴)</td>
    <td>우즈베키스탄</td>
  </tr>
  <tr>
    <td><code>vi-VN</code></td>
    <td>베트남어</td>
    <td>베트남</td>
  </tr>
  <tr>
    <td><code>cy-GB</code></td>
    <td>웨일즈어</td>
    <td>영국</td>
  </tr>
  <tr>
    <td><code>yo-NG</code></td>
    <td>요루바어</td>
    <td>나이지리아</td>
  </tr>
  <tr>
    <td><code>zu-ZA</code></td>
    <td>줄루어</td>
    <td>남아프리카</td>
  </tr>
</table>
