---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

keywords: authentication, authorization, identity, app security, secure, directory, registry, passwords, languages, lockout

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


# 사용자 관리
{: #cd-users}

Cloud Directory를 사용으로 설정하는 경우 사용자가 이메일 또는 사용자 이름 및 비밀번호를 사용하여 애플리케이션에 등록할 수 있습니다.
{: shortdesc}


Cloud Directory 사용자는 {{site.data.keyword.appid_short_notm}} 사용자와 다릅니다. 사용자는 구성된 다양한 ID 제공자 옵션을 사용하여 앱에 등록할 수 있습니다. 이 주제에서 언급되는 사용자는 앱에 등록할 때 Cloud Directory 옵션을 사용하도록 선택한 사용자입니다.
{: note}


## 사용자 추가 및 삭제
{: #add-delete-users}

{{site.data.keyword.appid_short_notm}} 대시보드를 통해 또는 API를 사용하여 Cloud Directory 사용자를 관리할 수 있습니다.
{: shortdesc}

특정 사용자에 대한 전체 데이터를 확인하기 위해 API를 사용하여 Cloud Directory 사용자의 정보를 JSON 오브젝트로 리턴할 수 있습니다. {{site.data.keyword.appid_short_notm}}에서 지원하는 전체 사용자 데이터 세트를 확인하려면 [SCIM 코어 스키마](https://tools.ietf.org/html/rfc7643#section-8.2)를 참조하십시오.

### 사용자 추가
{: #add-users}

다음 단계를 사용하여 {{site.data.keyword.appid_short_notm}} 대시보드를 통해 사용자를 추가할 수 있습니다.

테스트용으로 {{site.data.keyword.appid_short_notm}} 대시보드를 통해 사용자를 추가할 수 있습니다.

1. {{site.data.keyword.appid_short_notm}} 대시보드의 **Cloud Directory > 사용자** 탭으로 이동하십시오.

2. **사용자 추가**를 클릭하십시오. 양식이 표시됩니다.

3. **이름**, **성**, **이메일** 및 **비밀번호**를 입력하십시오. 등록하려는 이메일을 다른 사용자가 이미 사용하고 있지 않은지 확인하십시오. 비밀번호를 올바르게 입력하기 위해 **비밀번호 다시 입력** 필드에 해당 비밀번호를 입력하여 확인하십시오.

4. **저장**을 클릭하십시오. Cloud Directory 사용자가 작성되었습니다.


### 사용자 삭제
{: #delete-users}

디렉토리에서 사용자를 제거하려는 경우 GUI에서 해당 사용자를 삭제할 수 있습니다.

1. {{site.data.keyword.appid_short_notm}} 대시보드의 **Cloud Directory > 사용자** 탭으로 이동하십시오.

2. 삭제할 사용자의 옆에 있는 선택란을 클릭하십시오. 상자가 표시됩니다.

3. 상자에서 **삭제**를 클릭하십시오. 화면이 표시됩니다.

4. **삭제**를 클릭하여 사용자를 삭제하면 해당 작업을 취소할 수 없습니다. 실수로 이 조치를 수행한 경우 사용자를 다시 디렉토리에 추가할 수 있지만 해당 사용자에 대한 정보는 더 이상 사용할 수 없습니다.


## 사용자 마이그레이션
{: #user-migration}

{{site.data.keyword.appid_short_notm}}의 새 인스턴스를 설정해야 하는 경우도 있습니다. 클라우드 디렉토리를 사용하는 경우 이 설정은 사용자를 새 인스턴스로 마이그레이션해야 함을 의미합니다. 관리 API를 사용하여 마이그레이션을 지원할 수 있습니다.
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

클라우드 디렉토리 사용자 및 해당 프로파일만 리턴됩니다. 다른 ID 제공자의 사용자는 리턴되지 않습니다.
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
    <td>토큰을 얻으려면 먼저 <code>관리자</code> 권한이 있는지 확인하십시오. IAM 토큰을 얻는 방법에 대한 도움말은 <a href="https://cloud.ibm.com/docs/iam/apikey_iamtoken.html#iamtoken_from_apikey" target="_blank">이 문서 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 참조하십시오.</td>
  </tr>
</table>

스크립트를 실행하려면 다음 작업을 수행하십시오.

1. <a href="https://github.com/ibm-cloud-security/appid-sample-code-snippets/tree/master/export-import-cloud-directory-users" target="_blank">저장소 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 복제하십시오.
2. 터미널을 열고 저장소를 복제한 폴더로 이동하십시오.
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
