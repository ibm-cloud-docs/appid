---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-08"

keywords: authentication, authorization, identity, app security, secure, access management, roles, attributes, users

subcollection: appid

---

{:new_window: target="_blank"}
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


# 튜토리얼: 사용자 역할 설정
{: #tutorial-roles}

애플리케이션을 코딩하는 경우 올바른 사용자가 올바른 시간에 올바른 액세스 권한을 보유하고 있는지 확인하기 어려울 수도 있습니다. 해당 프로세스를 지원하기 위해 {{site.data.keyword.appid_full}}를 사용하여 다양한 사용자 유형을 지정할 수 있도록 해주는 사용자 정의 속성(예: `role`)을 정의할 수 있습니다. 그런 다음 애플리케이션을 사용하여 각각의 사용자 유형에 대해 다양한 권한 레벨을 적용할 수 있습니다. 이 단계별 안내서를 사용하여 {{site.data.keyword.appid_short_notm}} API를 통해 사용자 속성을 설정하고 업데이트한 후 토큰에 삽입하는 방법에 대해 학습할 수 있습니다.
{: shortdesc}

API가 처음이십니까? 이 [Postman 콜렉션](https://github.com/ibm-cloud-security/appid-postman)을 통해 사용해 보십시오.
{: tip}

## 시나리오
{: #roles-scenario}

귀하는 가상의 테마 공원 개발자입니다. 귀하는 [웹 애플리케이션](/docs/services/appid?topic=appid-web-apps)에 대한 액세스를 관리하는 업무를 담당하며 해당 업무를 수행하는 가장 간단한 방법이 각각의 사용자 유형에 대한 역할을 설정하는 것이라고 생각합니다. 모두 서로 다른 레벨의 권한이 필요한 공원 직원 및 방문자 등의 몇 가지 서로 다른 역할 유형이 존재합니다. 귀하는 프로세스를 간소화하고 사용자가 애플리케이션에 처음으로 사인인하는 순간부터 해당 사용자에게 올바른 역할이 지정되기를 원합니다.  
{: shortdesc}

걱정하지 마십시오! {{site.data.keyword.appid_short_notm}}의 [사용자 정의 속성 기능](/docs/services/appid?topic=appid-custom-attributes)을 사용하여 모든 유형의 사용자 관련 정보를 저장할 수 있습니다. 따라서 역할 기반 액세스 제어 관련 작업을 수행 중이기 때문에 `role`로 이름 지정된 속성을 작성한 후 특정 유형의 역할을 지정하기 위해 서로 다른 값을 지정할 수 있습니다. 예를 들어 테마 공원에 각각 `role` 속성에 대한 값이 서로 다른 `visitors` 또는 `staff`이 포함될 수 있습니다. 그런 다음 애플리케이션 코드에서 사용자가 지정한 액세스 정책 및 권한을 적용하도록 할 수 있습니다.

이 튜토리얼은 특히 웹 앱 및 Cloud Directory를 염두에 두고 작성되었지만 더욱 광범위한 의미로 속성을 사용할 수 있습니다. 사용자 정의 속성은 사용자가 원하는 모든 속성이 될 수 있습니다. 속성의 숫자가 100,000개 미만인 상태에서 일반 JSON 오브젝트로 형식화하는 경우 모든 유형의 정보를 저장할 수 있습니다!
{: note}


## 시작하기 전에
{: #roles-before}

준비되셨습니까? 시작합니다!

시작하기 전에 다음과 같은 전제조건이 충족되는지 확인하십시오.
- {{site.data.keyword.appid_short_notm}} 서비스의 인스턴스
- 서비스 인증 정보 세트
- 액세스 및 유효성 검증할 수 있는 이메일 주소


## 1단계: {{site.data.keyword.appid_short_notm}} 인스턴스 구성
{: #roles-configure-app}

Cloud Land 사용자에 대한 속성 추가를 시작하려면 먼저 {{site.data.keyword.appid_short_notm}}의 인스턴스를 구성해야 합니다.
{: shortdesc}

1. 서비스 대시보드의 **ID 제공자** 탭에서 **Cloud Directory**를 사용으로 설정하십시오. 이 튜토리얼에서는 [Cloud Directory](/docs/services/appid?topic=appid-cloud-directory)를 사용하지만 [SAML](/docs/services/appid?topic=appid-enterprise), [Facebook](/docs/services/appid?topic=appid-social#facebook), [Google](/docs/services/appid?topic=appid-social#google) 또는 [사용자 정의 제공자](/docs/services/appid?topic=appid-custom-identity)와 같은 다른 IdP를 선택할 수도 있습니다.

2. **Cloud Directory > 이메일 검증** 탭에서 검증을 사용으로 설정한 후 **사용자가 먼저 이메일 주소를 검증하지 않고도 앱에 사인인할 수 있도록 허용**을 **아니오**로 설정하십시오. 사용자 정의 속성을 사용하여 권한 관련 역할을 설정하는 경우 사용자가 설정한 속성을 파악하려면 먼저 해당 ID를 유효성 검증해야 합니다.

3. **프로파일** 탭에서 **앱에서 사용자 정의 속성 변경**을 **사용 안함**으로 설정하십시오.

  기본적으로 사용자 정의 속성은 액세스 토큰이 있는 모든 사용자가 변경할 수 있습니다. 애플리케이션 보안을 보증하려면 앱의 관리자 또는 소유자만 사용자 정의 속성을 변경할 수 있도록 {{site.data.keyword.appid_short_notm}}를 구성해야 합니다. 이 경우 사용자가 자신의 사용자 정의 속성을 변경하고 해당 사용자가 소유해서는 안 되는 권한을 부여할 수 없도록 차단됩니다.
  {: important}

수고하셨습니다! 대시보드가 구성되었으며 역할 설정을 시작할 준비가 되었습니다.


## 2단계: 로그인하기 전에 다른 사용자 대신 역할 설정
{: #roles-set-before}

Cloud Land에 새로운 직원 구성원이 추가되었습니다! 해당 구성원의 정보를 모두 알고 있지만 해당 구성원이 며칠 동안 시작하지 않았습니다. {{site.data.keyword.appid_short_notm}} 사용자 및 `staff` 역할 등의 속성이 포함된 프로파일을 작성하여 [해당 구성원을 사전 등록](/docs/services/appid?topic=appid-preregister)할 수 있습니다.
{: shortdesc}

이 프로세스는 Cloud Directory 등록을 완료하지 않습니다. 이 사용자는 여전히 사용자가 작성하는 프로파일의 속성을 상속받기 위해 앱에 등록해야 합니다.
{: tip}

1. CLI를 사용하여 {{site.data.keyword.cloud_notm}}에 로그인하십시오.

  ```
  ibmcloud login
  ```
  {: pre}

2. IAM 액세스 토큰을 받으십시오.

  ```
  ibmcloud iam oauth-tokens
  ```
  {: pre}

3. `staff` 속성이 포함된 새 사용자에 대한 사용자 프로파일을 작성하기 위한 POST 요청을 작성하십시오. 사용되는 이메일에 액세스하여 유효성 검증할 수 있는지 확인하십시오.

  ```
  curl --request POST \
  https://us-south.appid.cloud.ibm.com/management/v4/{{APPID_TENANT_ID}}/users \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  - d '{
    "idp": "cloud_directory",
    "idp-identity": “user@email.com“,
    "profile": {
      "attributes": {
        “role”: “staff”
      }
    }
  }'
  ```
  {: pre}

  정상적인 응답 출력:

  ```
  {
      "id": "5ty78b09-1356-4py8-l45p-808l633101zz"
  }
  ```
  {: screen}

6. 프로파일이 `staff` 역할로 작성되었는지 유효성 검증하십시오.

  ```
  curl --request GET \
  https://us-south.appid.cloud.ibm.com/management/v4/<tenant-ID>/users?email=<user-email> \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  ```
  {: pre}

  정상적인 응답 본문:

  ```
  {
      "users": [
          {
              "idp": "nominated_cloud_directory",
              "id": "5ty78b09-1356-4py8-l45p-808l633101zz"
          }
      ]
  }
  ```
  {: screen}

수고하셨습니다! 애플리케이션의 사용자를 사전 등록했습니다. 이제 해당 사용자가 사전 등록에 사용된 ID를 사용하여 앱에 사인인하면 Cloud Directory 사용자가 작성되어 {{site.data.keyword.appid_short_notm}} 사용자 프로파일을 상속받습니다. 이제 속성을 업데이트하는 방법에 대해 학습합니다.


## 3단계: 사용자 속성 업데이트
{: #roles-update-attributes}

Cloud Land가 성장하고 있습니다! 이러한 성장을 따라잡기 위해 회사에서 새 직원을 고용합니다. 2단계의 `staff` 사용자는 이제 관리자가 되었습니다. [새 역할을 지정](/docs/services/appid?topic=appid-custom-attributes)하여 해당 프로파일을 업데이트할 수 있습니다.
{: shortdesc}

1. 프로파일을 업데이트하십시오.

  ```
  curl --request PUT \
  https://us-south.appid.cloud.ibm.com/management/v4/<tenant-id>/users/<user-id>/profile \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  - d '{
    "profile": {
      "attributes": {
        “role”: “manager”
      }
    }
  }'
  ```
  {: pre}

3. 프로파일을 보고 올바르게 업데이트되었는지 확인하십시오.

  ```
  curl --request POST \
  GET https://us-south.appid.cloud.ibm.com/management/v4/{{APPID_TENANT_ID}}/users/{{user_profile_id}}/profile \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  ```
  {: pre}

  정상적인 응답 출력:

  ```
  {
      "id": "5ce78e09-1356-4ef8-a45d-808b633101db",
      "identities": [],
      "attributes": {
          "role": "manager"
      }
  }
  ```
  {: screen}

수고하셨습니다!


## 4단계: 토큰에 속성 삽입
{: #roles-map-claims}

더욱 유명해짐에 따라 테마 공원이 계속 성장하고 있습니다! 새로운 방문자 및 직원이 너무 많아져서 작성되는 요청의 수를 제한하려고 합니다. 성능을 개선하기 위해 사용자 프로파일 속성을 액세스 및 ID 토큰 청구에 맵핑할 수 있습니다. 사용자 정의 청구를 맵핑하는 경우 토큰 자체에 사용자 정의 속성을 저장할 수 있습니다.
{: shortdesc}

[토큰 구성](/docs/services/appid?topic=appid-customizing-tokens#customizing-tokens)은 글로벌이며, 이는 지정된 실제 역할에 관계 없이 `role` 속성이 있는 모든 사용자에게 적용됨을 의미합니다.
{: tip}


1. 토큰 구성 엔드포인트에 대한 요청을 작성하십시오.

  ```
  curl --request PUT \
  https://us-south.appid.cloud.ibm.com/management/v4/{{APPID_TENANT_ID}}/config/tokens \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  - d '{
      "access": {
          "expires_in": 3601
      },
      "refresh": {
          "enabled": false,
          "expires_in": 2592001
      },
      "anonymousAccess": {
          "expires_in": 2592001
      },
      "accessTokenClaims": [
      {
      "source": "attributes",
      "sourceClaim": "role"
      }
      ]
  }'
  ```
  {: pre}

  <table>
    <tr>
      <th>변수</th>
      <th>설명</th>
    </tr>
    <tr>
      <td><code>tenant-id</code></td>
      <td>테넌트 ID는 요청에서 {{site.data.keyword.appid_short_notm}}의 인스턴스를 식별하는 방법입니다. ID는 대시보드의 <em>서비스 인증 정보</em> 탭에서 찾을 수 있습니다. 해당 세트가 없는 경우 GUI의 단계에 따라 인증 정보를 작성할 수 있습니다.</td>
    </tr>
    <tr>
      <td><code>source</code></td>
      <td><code>accessTokenClaim</code> 및 <code>idTokenClaims</code>는 둘 다 소스를 <code>attribute</code>로 설정합니다.</td>
    </tr>
    <tr>
      <td><code>sourceClaim</code></td>
      <td><code>accessTokenClaim</code> 및 <code>idTokenClaims</code>는 둘 다 소스 청구를 <code>role</code>로 설정합니다.</td>
    </tr>
    <tr>
      <td><code>expires_in</code></td>
      <td>이 값은 각각의 토큰 유형에 적용되며 각각의 요청에 설정되어 있어야 합니다. 이전에 GUI에서 값을 설정한 후 이 요청을 실행하는 경우 해당 요청의 값이 이전에 설정된 값을 대체합니다. 만기가 사용자 구성에 대한 올바른 값으로 설정되어 있는지 확인하십시오.</td>
    </tr>
  </table>

  정상적인 응답 출력:

  ```
  {
      "access": {
          "expires_in": 3601
      },
      "refresh": {
          "enabled": false,
          "expires_in": 2592001
      },
      "anonymousAccess": {
          "expires_in": 2592001
      },
      "accessTokenClaims": [
      {
      "source": "attributes",
      "sourceClaim": "role"
      }
      ]
  }
  ```
  {: screen}


## 5단계: 액세스 토큰 보기
{: #roles-view-token}

선택적으로 액세스 토큰을 보고 4단계가 정상적으로 완료되었는지 확인할 수 있습니다.
{: shortdesc}

1. 테스트용으로 {{site.data.keyword.appid_short_notm}} GUI를 사용하여 Cloud Directory 사용자를 작성하십시오.

  1. **사용자** 탭에서 **사용자 추가**를 클릭하십시오. 양식이 표시됩니다.
  2. 이름, 성, 이메일 및 비밀번호를 입력하십시오.
  3. **저장**을 클릭하십시오.

2. 클라이언트 ID 및 시크릿을 인코딩하십시오.

  1. {{site.data.keyword.appid_short_notm}} GUI의 **서비스 인증 정보** 탭에서 클라이언트 ID 및 시크릿을 복사하십시오.
  2. Base-64 인코더를 사용하여 권한 정보를 인코딩하십시오.
  3. 다음 명령에서 사용하기 위해 출력을 복사하십시오.

4. 액세스 토큰 정보를 얻기 위해 API를 사용하여 사인인하십시오. 리턴되는 토큰은 인코딩되어 있습니다.

  ```
  curl --request PUT \
  https://appid.cloud.ibm.com/oauth/v4/<tenant-ID>/token \
  --header 'Authorization: Basic <encoded-clientID>:<encoded-client-secret>' \
  --header 'Content-Type: application/x-www-form-urlencoded' \
  --header `Accept: application/json`
  - d 'grant_type=password&username=<user-email>%40<user-email-domain>&password=<user-password>
  ```
  {: pre}

5. 액세스 토큰을 디코딩하십시오.
  1. 이전 명령에서 응답 출력에 있는 토큰을 복사하십시오.
  2. 브라우저에서 https://jwt.io/로 이동하십시오.
  3. 토큰을 **인코딩됨**으로 레이블 지정된 상자에 붙여넣으십시오.

6. **디코딩됨** 섹션에서 해당 역할이 표시되는지 확인하십시오.

  ```
  {
    "iss": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61",
    "exp": 1551903163,
    "aud": [
      "968c2306-9aef-4109-bc06-4f5ed6axi24a"
    ],
    "sub": "2b96cc04-eca5-4122-a8de-6e07d14c13a5",
    "email_verified": true,
    "amr": [
      "cloud_directory"
    ],
    "iat": 1551899553,
    "tenant": "39a37f57-a227-4bfe-a044-93b6e6050a61",
    "scope": "openid appid_default appid_readprofile appid_readuserattr appid_writeuserattr appid_authenticated"
    "role": "manager"
  }
  ```
  {: screen}



## 다음 단계
{: #roles-next}

수고하셨습니다! 튜토리얼이 완료되었습니다. 이제 [다단계 인증(MFA)](/docs/services/appid?topic=appid-cd-mfa)을 구성하거나 [고유 브랜드 GUI](/docs/services/appid?topic=appid-branded)를 설정해 볼 수 있습니다.
