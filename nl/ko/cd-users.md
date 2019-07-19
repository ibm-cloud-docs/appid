---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-09"

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


# 사용자 관리
{: #cd-users}

Cloud Directory를 사용할 경우 보안 및 셀프 서비스를 강화하는 사전 빌드 기능을 통해 확장 가능한 레지스트리에서 사용자를 관리할 수 있습니다.
{: shortdesc}

Cloud Directory 사용자는 {{site.data.keyword.appid_short_notm}} 사용자와 다릅니다. 사용자는 구성된 다양한 ID 제공자 옵션을 사용하여 앱에 등록하거나, 디렉토리에 사용자를 추가할 수 있습니다. 이 페이지에서 설명하는 사용자는 ID 제공자 역할을 하는 Cloud Directory와 연관된 사용자입니다.
{: note}

## 사용자 정보 보기
{: #cd-user-info}

API를 사용하거나 대시보드를 사용하여 모든 Cloud Directory 사용자에 대해 JSON 오브젝트로 알려진 모든 정보를 확인할 수 있습니다. 
{: shortdesc}


### GUI 사용

{{site.data.keyword.appid_short_notm}} 대시보드에서 앱 사용자에 대한 세부사항을 볼 수 있습니다. 

1. {{site.data.keyword.appid_short_notm}} 인스턴스의 **Cloud Directory > 사용자** 탭으로 이동하십시오.

2. 테이블을 검토하거나 이메일 주소로 검색하여 정보를 보려는 사용자를 찾으십시오.

3. 사용자 행의 오버플로우 메뉴에서 **사용자 세부사항 보기**를 클릭하십시오. 사용자 정보가 포함된 페이지가 열립니다. 다음 표에서 볼 수 있는 정보를 확인하십시오.

<table>
  <tr>
    <th colspan="2">사용자 세부사항</th>
  </tr>
  <tr>
    <td>사용자 ID</td>
    <td>사용자 ID는 구성한 사용자 등록 유형에 따라 다릅니다. 이메일 및 비밀번호 플로우가 구성되어 있는 경우 ID는 사용자 이메일입니다. 사용자 이름 및 비밀번호 플로우를 사용하는 경우 ID는 등록 시 제공되는 사용자 이름입니다. </td>
  </tr>
  <tr>
    <td>이메일</td>
    <td>사용자에게 첨부되는 기본 이메일 주소입니다.</td>
  </tr>
    <tr>
    <td>이름과 성</td>
    <td>가입 프로세스 중에 제공한 사용자의 이름과 성입니다.</td>
  </tr>
  <tr>
    <td>마지막 로그인</td>
    <td>사용자가 애플리케이션에 마지막으로 로그인한 시간의 시간소인입니다. 참고: 대시보드를 통해 사용자를 추가한 경우에는 사용자가 앱에 직접 로그인할 때까지 로그인이 비어 있습니다. 로그인을 수행하면 App ID 사용자가 됩니다. </td>
  </tr>
  <tr>
    <td>ID</td>
    <td>{{site.data.keyword.appid_short_notm}}에서 사용자에게 지정한 ID입니다. UI에는 표시되지 않지만, 이 값을 복사하여 문서 편집기에 붙여넣으면 값을 볼 수 있습니다. </td>
  </tr>
  <tr>
    <td>사전 정의된 속성</td>
    <td>사전 정의된 속성은 SCIM 기반 사용자에 대해 알려진 속성입니다.</td>
  </tr>
  <tr>
    <td>사용자 정의 속성</td>
    <td>사용자 정의 속성은 사용자 프로파일에 추가되거나 애플리케이션과 상호작용하는 사용자에 대해 학습한 추가 정보입니다.</td>
  </tr>
  <tr>
    <td>요약</td>
    <td>모든 속성을 컴파일하여 Cloud Directory 사용자의 전체 개요를 제공하는 하나의 프로파일을 생성합니다. 자세한 정보는 [사용자 프로파일](/docs/services/appid?topic=appid-profiles)을 참조하십시오.</td>
  </tr>
</table>

</br>

### API 사용

{{site.data.keyword.appid_short_notm}} API를 사용하여 앱 사용자에 대한 세부사항을 볼 수 있습니다. 

1. 서비스 인스턴스에서 테넌트 ID를 얻으십시오.

2. 식별 조회(예: 이메일 주소)로 App ID 사용자를 검색하여 사용자 ID를 찾으십시오.

  ```
  curl -X GET "https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/cloud_directory/Users?query={identifying-search-query}" -H "accept: application/json" -H "authorization: Bearer {token}"
  ```
  {: codeblock}

      예:

  ```
  curl -X GET https://us-south.appid.cloud.ibm.com/management/v4/e19a2778-3262-4986-8875-8khjafsdkhjsdafkjh/cloud_directory/Users?query=example@email.com -H "accept: application/json" -H "authorization: Bearer eyJraWQiOiIyMDE3MTEyOSIsImFsZ...."
  ```
  {: screen}

3. 이전 단계에서 얻은 ID로 `cloud_directory/users` 엔드포인트에 대해 GET 요청을 작성하여 전체 사용자 프로파일을 표시하십시오.

  ```
  curl -X GET "https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/cloud_directory/Users/{user-ID}" -H "accept: application/json" -H "authorization: Bearer {token}"
  ```
  {: codeblock}

  응답 예제:

  ```
  {
    sub: "c155c0ff-337a-46d3-a22a-a8f2cca08995",
    name: "Test User",
    email: "testuser@test.com",
    identities: [
      {
        provider: "cloud_directory",
        id: "f1772fcc-ff70-4d88-81a0-07dd7a3d988f",
        idpUserInfo: {
          displayName: "Test User",
          active: true,
          mfaContext: {},
          emails: [
            {
              value: "testuser@test.com",
              primary: true
            }
          ],
          meta: {
            lastLogin: "2019-05-20T16:33:20.699Z",
            created: "2019-05-20T16:25:13.019Z",
            location: "/v1/6b8ab644-1d4a-4b3e-bcd9-777ba8430a51/Users/f1772fcc-ff70-4d88-81a0-07dd7a3d988f",
            lastModified: "2019-05-20T16:33:20.707Z",
            resourceType: "User"
          },
          scemas: [
            "urn:ietf:params:scim:schemas:core:2.0:User"
          ],
          name: {
            givenName: "Test",
            familyName: "User",
            formatted: "Test User"
            },
          id: "f1772fcc-ff70-4d88-81a0-07dd7a3d988f",
          status: "CONFIRMED",
          idpType: "cloud_directory"
        }
      }
    ]
  }
  ```
  {: screen}

  {{site.data.keyword.appid_short_notm}}에서 지원하는 전체 사용자 데이터 세트를 확인하려면 [SCIM 코어 스키마](https://tools.ietf.org/html/rfc7643#section-8.2)를 참조하십시오.
  {: tip}


## 사용자 추가 및 삭제
{: #add-delete-users}

{{site.data.keyword.appid_short_notm}} 대시보드를 통해 또는 API를 사용하여 Cloud Directory 사용자를 관리할 수 있습니다.
{: shortdesc}

사용자가 애플리케이션에 등록하는 경우 셀프 서비스 워크플로우를 통해 등록됩니다. 이 경우 환영 또는 검증 요청과 같은 이메일이 자동으로 트리거됩니다. 관리자가 사용자를 앱에 추가하는 경우에 셀프 서비스 워크플로우가 시작되지 않습니다. 즉, 사용자는 애플리케이션으로부터 이메일을 받지 않습니다. 사용자가 추가되었다는 알림을 계속 받으려는 경우 [App ID 관리 API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.set_cloud_directory_email_dispatcher)를 통해 메시지 플로우를 트리거할 수 있습니다. 


### 사용자 추가
{: #add-users}

사용자가 앱에 등록하면 해당 사용자가 사용자로 추가됩니다. 테스트를 위해 {{site.data.keyword.appid_short_notm}} 대시보드 또는 API를 통해 사용자를 추가할 수 있습니다.

셀프 서비스 등록을 사용 안함으로 설정하거나 사용자를 대신해 추가하는 경우 해당 사용자는 추가될 때 환영 또는 검증 이메일을 수신하지 않습니다.
{: tip}



**GUI를 사용하여 사용자 추가:**

1. {{site.data.keyword.appid_short_notm}} 대시보드의 **Cloud Directory > 사용자** 탭으로 이동하십시오.

2. **사용자 추가**를 클릭하십시오. 양식이 열립니다. 

3. **이름**, **성**, **이메일** 및 **비밀번호**를 입력하십시오. 등록하려는 이메일을 다른 사용자가 이미 사용하고 있지 않은지 확인하십시오. 비밀번호를 올바르게 입력하기 위해 **비밀번호 다시 입력** 필드에 해당 비밀번호를 입력하여 확인하십시오.

4. **저장**을 클릭하십시오. Cloud Directory 사용자가 작성되었습니다.

</br>


**API를 사용하여 사용자 추가:**

다음 플로우는 이메일 및 비밀번호를 사용하여 사용자를 추가하는 방법을 보여줍니다. 사용자 이름 및 비밀번호 플로우를 사용하도록 선택할 수도 있습니다. 

1. 애플리케이션 또는 서비스 인증 정보에서 `tenantID`를 얻으십시오.

2. {{site.data.keyword.cloud_notm}} IAM 토큰을 얻으십시오.

  ```
  curl --X GET "https://iam.cloud.ibm.com/oidc/token" -H "accept: application/x-www-form-urlencoded"
  ```
  {: codeblock}

3. 2단계에서 얻은 토큰을 사용하여 `cloud-directory/users` 엔드포인트에 대해 POST 요청을 작성하십시오. 이 예에서는 이메일/비밀번호 플로우를 사용합니다. 사용자 이름/비밀번호 플로우를 사용할 수도 있습니다.

  ```
  curl --X POST "https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/cloud_directory/Users"
  -H "accept: application/json"
  -H "content-type: application/json"
  -H "authorization: Bearer {token}"
  -d {
    "displayName": "Test User",
    "password": "{App-ID-Cloud-Directory-User-Password}",
    "active": true,
    "emails": [
      {
        "value": "{App-ID-Cloud-Directory-User-Email}",
        "primary": true
      }
    ]
  }
  ```
  {: codeblock}

</br>


### 사용자 삭제
{: #delete-users}

디렉토리에서 사용자를 제거하려는 경우 GUI 또는 API에서 해당 사용자를 삭제할 수 있습니다.
{: shortdesc}

**GUI를 통해 사용자 삭제:**

1. {{site.data.keyword.appid_short_notm}} 대시보드의 **Cloud Directory > 사용자** 탭으로 이동하십시오.

2. 삭제할 사용자의 옆에 있는 선택란을 클릭하십시오. 상자가 열립니다.

3. 상자에서 **삭제**를 클릭하십시오. 화면이 열립니다.

4. **삭제**를 클릭하여 사용자를 삭제하면 해당 작업을 취소할 수 없습니다. 실수로 이 조치를 수행한 경우 사용자를 다시 디렉토리에 추가할 수 있지만 해당 사용자에 대한 정보는 더 이상 사용할 수 없습니다.

</br>

**API를 통해 사용자 삭제:**

1. 테넌트 ID를 얻으십시오.

2. 사용자에게 첨부된 이메일로 디렉토리를 검색하여 사용자 ID를 찾으십시오.

  ```
  curl -X GET "https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/users?email={user-email}" -H "accept: application/json"
  ```
  {: codeblock}

3. 사용자를 삭제하십시오.

  ```
  curl --X DELETE "https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/cloud_directory/Users/{user-GUID}"
  -H "accept: application/x-www-form-urlencoded"
  ```
  {: codeblock}



## 사용자 마이그레이션
{: #user-migration}

경우에 따라 {{site.data.keyword.appid_short_notm}}의 인스턴스를 추가해야 할 수도 있습니다. Cloud Directory를 사용하여 작업하는 경우 사용자를 새 인스턴스에 마이그레이션해야 합니다. 마이그레이션을 지원하기 위해 관리 API를 사용할 수 있습니다.
{: shortdesc}


{{site.data.keyword.appid_short_notm}}의 양쪽 인스턴스 모두에 대해 `관리자` [IAM 역할](/docs/iam?topic=iam-getstarted#getstarted)이 지정되어 있어야 합니다.
{: note}


### 내보내기
{: cd-export}

새 인스턴스에 사용자를 추가하려면 먼저 현재 인스턴스에서 해당 사용자를 내보내야 합니다. 이 작업을 위해 <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryExport" target="_blank">내보내기 관리 API <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 사용할 수 있습니다.

cURL 명령 예제:

```
curl -X GET --header ‘Accept: application/json’ --header ‘Authorization: Bearer <iam-token>’ ’https://us-south.appid.cloud.ibm.com/management/v4/111c9bj3-xxxx-4b5b-zzzz-24ad9440k8j9/cloud_directory/export?encryption_secret=myCoolSecret'
```
{: codeblock}

<table>
  <tr>
    <th>변수</th>
    <th>설명</th>
  </tr>
  <tr>
    <td><code>encryption_secret</code></td>
    <td>사용자 해시 비밀번호를 암호화 및 복호화하기 위해 사용되는 사용자 정의 문자열입니다.</td>
  </tr>
  <tr>
    <td><code> tenantID </code></td>
    <td>서비스 인증 정보에서 찾을 수 있는 서비스 테넌트 ID입니다. 서비스 인증 정보는 {{site.data.keyword.appid_short_notm}} 대시보드에서 찾을 수 있습니다.</td>
  </tr>
</table>

Cloud Directory 사용자 및 해당 프로파일만 리턴됩니다. 다른 ID 제공자의 사용자는 리턴되지 않습니다.
{: note}


### 가져오기
{: #cd-import}

사용자가 이동할 준비가 되었기 때문에 해당 정보를 새 인스턴스로 가져올 수 있습니다. 이 작업을 위해 <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryImport" target="_blank">가져오기 관리 API <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 사용할 수 있습니다.


cURL 명령 예제:

```
curl -X POST --header ‘Content-Type: application/json’ --header ‘Accept: application/json’ --header ‘Authorization: Bearer <iam-token>’ -d ‘{“users”: [
    {
      “scimUser”: {
        “originalId”: “3f3f6779-7978-4383-926f-a43aef3b724b”,
        “name”: {
          “givenName”: “<first-name>”,
          “familyName”: “<last-name>”,
          “formatted”: “<first-name> <last-name>”
        },
        “displayName”: “<first-name>”,
        “emails”: [
          {
            “value”: “<user>@gmail.com”,
            “primary”: true
          }
        ],
        “status”: “PENDING”
      },
      “passwordHash”: “<password hash here>“,
      “passwordHashAlg”: “<password hash algorithm>",
      “profile”: {
        “attributes”: {}
      }
    }
]}’ ‘https://us-south.appid.cloud.ibm.com/management/v4/111c9bj3-xxxx-4b5b-zzzz-24ad9440k8j9/cloud_directory/import?encryption_secret=myCoolSecret’
```
{: codeblock}



### 마이그레이션 스크립트
{: cd-migration-script}

{{site.data.keyword.appid_short_notm}}에서는 CLI를 통해 사용할 수 있으며 마이그레이션 프로세스를 가속화하는 마이그레이션 스크립트를 제공합니다.

시작하기 전에 다음과 같은 매개변수 정보가 있는지 확인하십시오.

<table>
  <tr>
    <th>매개변수</th>
    <th>설명</th>
  </tr>
  <tr>
    <td><code>sourceTenantId</code></td>
    <td>사용자를 내보내려는 {{site.data.keyword.appid_short_notm}} 인스턴스의 테넌트 ID입니다.</td>
  </tr>
  <tr>
    <td><code>destinationTenantId</code></td>
    <td>사용자를 가져오려는 {{site.data.keyword.appid_short_notm}} 인스턴스의 테넌트 ID입니다.</td>
  </tr>
  <tr>
    <td>Region</td>
    <td>지역 옵션에는 <code>au-syd</code>, <code>eu-de</code>, <code>eu-gb</code>, <code>jp-tok</code> 및 <code>us-south</code>가 있습니다.</td>
  </tr>
  <tr>
    <td>IAM token</td>
    <td>토큰을 얻으려면 먼저 <code>관리자</code> 권한이 있는지 확인하십시오. IAM 토큰을 얻는 방법에 대한 도움말은 <a href="/docs/iam?topic=iam-iamtoken_from_apikey#iamtoken_from_apikey" target="_blank">이 문서 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 참조하십시오.</td>
  </tr>
</table>

스크립트를 실행하려면 다음 작업을 수행하십시오.

1. <a href="https://github.com/ibm-cloud-security/appid-sample-code-snippets/tree/master/export-import-cloud-directory-users" target="_blank">저장소 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 복제하십시오.
2. 콘솔을 열고 저장소를 복제한 폴더로 이동하십시오.
3. 다음 명령을 실행하십시오.

  ```
  npm install
  ```
  {: codeblock}

4. 해당 매개변수를 사용하여 다음 명령을 실행하십시오.

  ```
  users_export_import 'sourceTenantId' 'destinationTenantId' 'region' 'iamToken'
  ```
  {: codeblock}

  명령 예제:

  ```
  users_export_import e00a0366-53c5-4fcf-8fef-ab3e66b2ced8 73321c2b-d35a-497a-9845-15c580fdf58c ng eyJraWQiOiIyMDE3MTAyNS0xNjoyNzoxMCIsImFsZyI6IlJTMjU2In0.eyJpYW1faWQiOiJJQk1pZC0zMTAwMDBUNkZTIiwiaWQiOiJJQk1pZC0zMTAwMDBUNkZTIiwicmVhbG1pZCI6IklCTWlkIiwiaWRlbnRpZmllciI6IjMxMDAwIFQ2RlMiPCJnaXZlbl9uYW1lIjoiUm90ZW0iLCJmYW1pbHlfbmFtZSI6IkJyb3NoIiwibmFtZSI6IlJvdGVtIEJyb3NoIiwiZW1haWwiOiJyb3RlbWJyQGlsLmlibS5jb20iLCJzdWIiOiJyb3RlbWJyQGlsLmlibS5jb20iLCJhY2NvdW50Ijp7ImJzcyI6ImQ3OWM5YTk5NjJkYzc2Y2JkMDZlYTVhNzhjMjY0YzE5In0sImlhdCI6MTUzNrE3Mjg4NCwiZXhwIjoxNTM3MTc2NDg0LCJpc3MiOiJodHRwczovL2lhbS5zdGFnZTEuYmx1ZW1peC5uZXQvaWRlbnRpdHkiLCJncmFudF90eXBlIjoidXJuOmlibTpwYXJhbXM6b2F1dGg6Z3JhbnQtdHlwZTpwYXNzY29kZSIsInNjb3BlIjoiaWJtIG9wZW5pZCIsImNsaWVudF9pZCI6ImJ4IiwiYWNyIjoxLCJhbXIiOlsicHdkIl19.c4vLPzhvvNZLjaLy7znDa37qV4o-yuGmSKmJoQKrEQNZU8IC0NIjxwSo7W9kb0pDi3Yf_03_9ufTTGNfjtltzNWycSXjkNgoL-b9_nU61oHdgn0stY1KmNicqyBWfgUU--4xa904QN_QjRHBaUBeJf3XWEphPIMoF7mZeOxEZLnCMcQXSz9pImCMiP4SNT38cHLiI90Yx01rM7hpteepWULh5MYh-B2V03Gkgxfqvv951HF1LDg6eT4Q9in11laTQKtKuomripUju_4GIIjORVYw9NaAVKIJ9lKrPX0SKPhStsa59qGsC_7Uersms5EY1W1VbZVqOZPJbtp6tVf-Lw
  ```
  {: codeblock}
