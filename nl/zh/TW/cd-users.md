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


# 管理使用者
{: #cd-users}

使用 Cloud Directory，您可以使用預先建置的功能（它會加強安全及自助），在可擴充的登錄中管理使用者。
{: shortdesc}

Cloud Directory 使用者與 {{site.data.keyword.appid_short_notm}} 使用者不同。使用者可以使用您配置的不同身分提供者選項來註冊您的應用程式，您也可以將他們新增至您的目錄。此頁面上所提及的使用者，是指與作為身分提供者的 Cloud Directory 相關聯的那些使用者。
{: note}

## 檢視使用者資訊
{: #cd-user-info}

您可以使用 API 或使用儀表板，以 JSON 物件查看針對所有 Cloud Directory 使用者了解的所有資訊。
{: shortdesc}


### 使用 GUI

您可以使用 {{site.data.keyword.appid_short_notm}} 儀表板，來檢視應用程式使用者的詳細資料。 

1. 導覽至 {{site.data.keyword.appid_short_notm}} 實例的 **Cloud Directory > 使用者**標籤。

2. 在表格中尋找，或是使用電子郵件位址進行搜尋，以尋找您要查看其資訊的使用者。

3. 在使用者列的溢位功能表中，按一下**檢視使用者詳細資料**。即會開啟包含使用者資訊的頁面。請參閱下表，以查看您可以看見的資訊。

<table>
  <tr>
    <th colspan="2">使用者詳細資料</th>
  </tr>
  <tr>
    <td>使用者 ID</td>
    <td>使用者 ID 視您所配置的使用者註冊類型而定。如果您已配置電子郵件及密碼流程，則 ID 是使用者的電子郵件。如果您使用使用者名稱及密碼流程，則 ID 是在註冊時提供的使用者名稱。</td>
  </tr>
  <tr>
    <td>電子郵件</td>
    <td>附加至使用者的主要電子郵件位址。</td>
  </tr>
    <tr>
    <td>名字及姓氏</td>
    <td>使用者在註冊程序期間所提供的名字及姓氏。</td>
  </tr>
  <tr>
    <td>前次登入時間</td>
    <td>使用者前次登入應用程式的時間戳記。附註：如果您是透過儀表板新增使用者，則在使用者自己登入應用程式之前，登入會是空白的。在進行登入時，他們也會變成 App ID 使用者。</td>
  </tr>
  <tr>
    <td>ID</td>
    <td>{{site.data.keyword.appid_short_notm}} 指派給使用者的 ID。在使用者介面中，不會顯示該值，但您可以複製該值，並貼到文字編輯器中，以查看該值。</td>
  </tr>
  <tr>
    <td>預先定義屬性</td>
    <td>預先定義的屬性是根據 SCIM，關於使用者的已知事情。</td>
  </tr>
  <tr>
    <td>自訂屬性</td>
    <td>自訂屬性是新增至使用者設定檔的其他資訊，或是在使用者與您的應用程式互動時瞭解到關於使用者的其他資訊。</td>
  </tr>
  <tr>
    <td>摘要</td>
    <td>所有屬性都會進行編譯，以形成一個設定檔，該設定檔會為您提供 Cloud Directory 使用者的完整概觀。如需相關資訊，請參閱[使用者設定檔](/docs/services/appid?topic=appid-profiles)。</td>
  </tr>
</table>

</br>

### 使用 API

您可以使用 {{site.data.keyword.appid_short_notm}} API，來檢視應用程式使用者的詳細資料。 

1. 從服務實例中取得您的承租戶 ID。

2. 使用識別查詢（例如電子郵件位址）搜尋您的 App ID 使用者，以尋找使用者 ID。

  ```
  curl -X GET "https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/cloud_directory/Users?query={identifying-search-query}" -H "accept: application/json" -H "authorization: Bearer {token}"
  ```
  {: codeblock}

  範例：

  ```
  curl -X GET https://us-south.appid.cloud.ibm.com/management/v4/e19a2778-3262-4986-8875-8khjafsdkhjsdafkjh/cloud_directory/Users?query=example@email.com -H "accept: application/json" -H "authorization: Bearer eyJraWQiOiIyMDE3MTEyOSIsImFsZ...."
  ```
  {: screen}

3. 透過使用您在先前步驟中所取得的 ID，對 `cloud_directory/users` 端點發出 GET 要求，以查看其完整使用者設定檔。

  ```
  curl -X GET "https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/cloud_directory/Users/{user-ID}" -H "accept: application/json" -H "authorization: Bearer {token}"
  ```
  {: codeblock}

  回應範例：

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

  若要查看 {{site.data.keyword.appid_short_notm}} 支援的完整使用者資料集，請參閱 [SCIM 核心綱目](https://tools.ietf.org/html/rfc7643#section-8.2)。
  {: tip}


## 新增及刪除使用者
{: #add-delete-users}

您可以透過 {{site.data.keyword.appid_short_notm}} 儀表板或使用 API 來管理 Cloud Directory 使用者。
{: shortdesc}

當使用者註冊應用程式時，他們會透過自助工作流程來進行，工作流程會自動觸發電子郵件，例如歡迎或驗證要求。身為管理者的您將使用者新增至應用程式時，不會起始自助工作流程，這表示使用者不會收到來自您應用程式的任何電子郵件。如果您希望使用者仍然收到已新增他們的通知，可以透過 [App ID 管理 API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.set_cloud_directory_email_dispatcher) 來觸發傳訊流程。


### 新增使用者
{: #add-users}

當使用者註冊您的應用程式時，系統會將他們新增為使用者。為了進行測試，您可以透過 {{site.data.keyword.appid_short_notm}} 儀表板或使用 API 來新增使用者。

如果您停用自助登入或新增一個代表他們的使用者，則在新增使用者時，他們不會收到歡迎或驗證電子郵件。
{: tip}



**若要使用 GUI 新增使用者，請執行下列動作：**

1. 移至 {{site.data.keyword.appid_short_notm}} 儀表板的 **Cloud Directory > 使用者**標籤。

2. 按一下**新增使用者**。即會開啟表單。

3. 輸入**名字**、**姓氏**、**電子郵件**及**密碼**。請確定您嘗試要登錄的電子郵件尚未由另一位使用者使用。若要確定您已正確鍵入密碼，請在**重新輸入密碼**欄位中輸入該密碼來加以確認。

4. 按一下**儲存**。即建立 Cloud Directory 使用者。

</br>


**若要使用 API 新增使用者，請執行下列動作：**

下列流程顯示如何使用電子郵件及密碼來新增使用者。您也可以選擇使用使用者名稱及密碼流程。

1. 從您的應用程式或服務認證取得 `tenantID`。

2. 取得 {{site.data.keyword.cloud_notm}} IAM 記號。

  ```
  curl --X GET "https://iam.cloud.ibm.com/oidc/token" -H "accept: application/x-www-form-urlencoded"
  ```
  {: codeblock}

3. 使用您在步驟 2 中取得的記號，對 `cloud-directory/users` 端點發出 POST 要求。這個範例使用電子郵件/密碼流程。您也可以使用使用者名稱/密碼流程。

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


### 刪除使用者
{: #delete-users}

如果您要從目錄移除使用者，則可以從 GUI 或使用 API 刪除該使用者。
{: shortdesc}

**若要透過 GUI 刪除使用者，請執行下列動作：**

1. 移至 {{site.data.keyword.appid_short_notm}} 儀表板的 **Cloud Directory > 使用者**標籤。

2. 請按一下您要刪除之使用者旁的勾選框。即會開啟方框。

3. 在此方框中，按一下**刪除**。即會開啟畫面。

4. 按一下**刪除**，以確認您瞭解刪除使用者動作無法復原。如果此動作是錯的，您可以重新將使用者新增至目錄中，但該使用者的任何相關資訊已不再可用。

</br>

**若要使用 API 刪除使用者，請執行下列動作：**

1. 取得您的承租戶 ID。

2. 透過使用附加至使用者的電子郵件，搜尋目錄以尋找使用者的 ID。

  ```
  curl -X GET "https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/users?email={user-email}" -H "accept: application/json"
  ```
  {: codeblock}

3. 刪除使用者。

  ```
  curl --X DELETE "https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/cloud_directory/Users/{user-GUID}"
  -H "accept: application/x-www-form-urlencoded"
  ```
  {: codeblock}



## 移轉使用者
{: #user-migration}

有時，您可能需要新增 {{site.data.keyword.appid_short_notm}} 的實例。如果您是使用 Cloud Directory，您的使用者必須移轉至新的實例。若要協助移轉，您可以使用管理 API。
{: shortdesc}


您必須為 {{site.data.keyword.appid_short_notm}} 的兩個實例指派`管理員` [IAM 角色](/docs/iam?topic=iam-getstarted#getstarted)。
{: note}


### 匯出
{: cd-export}

在可以將您的使用者新增至新的實例之前，您需要從現行實例中匯出他們。若要這樣做，您可以使用<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryExport" target="_blank">匯出管理 API <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。

cURL 指令範例：

```
curl -X GET --header ‘Accept: application/json’ --header ‘Authorization: Bearer <iam-token>’ ’https://us-south.appid.cloud.ibm.com/management/v4/111c9bj3-xxxx-4b5b-zzzz-24ad9440k8j9/cloud_directory/export?encryption_secret=myCoolSecret'
```
{: codeblock}

<table>
  <tr>
    <th>變數</th>
    <th>說明</th>
  </tr>
  <tr>
    <td><code>encryption_secret</code></td>
    <td>用來加密和解密使用者雜湊式密碼的自訂字串。</td>
  </tr>
  <tr>
    <td><code> tenantID </code> </td>
    <td>可在您的服務認證中找到服務承租戶 ID。您可以在 {{site.data.keyword.appid_short_notm}} 儀表板中找到您的服務認證。</td>
  </tr>
</table>

只會傳回您的「雲端目錄」使用者及其設定檔。不會傳回其他身分提供者的使用者。
{: note}


### 匯入
{: #cd-import}

既然您已備妥使用者，就可以將其資訊匯入至新的實例。若要這樣做，您可以使用<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryImport" target="_blank">匯入管理 API <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。


cURL 指令範例：

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



### 移轉 Script
{: cd-migration-script}

{{site.data.keyword.appid_short_notm}} 提供一個您可以透過 CLI 使用的移轉 Script，其可協助加速移轉處理程序。

開始之前，請確定您具有下列參數資訊：

<table>
  <tr>
    <th>參數</th>
    <th>說明</th>
  </tr>
  <tr>
    <td><code>sourceTenantId</code></td>
    <td>您計劃從其中匯出使用者之 {{site.data.keyword.appid_short_notm}} 實例的承租戶 ID。</td>
  </tr>
  <tr>
    <td><code>destinationTenantId</code></td>
    <td>您計劃將使用者匯入其中之 {{site.data.keyword.appid_short_notm}} 實例的承租戶 ID。</td>
  </tr>
  <tr>
    <td>地區</td>
    <td>地區選項包括：<code>au-syd</code>、<code>eu-de</code>、<code>eu-gb</code>、<code>jp-tok</code> 及 <code>us-south</code>。</td>
  </tr>
  <tr>
    <td>IAM 記號</td>
    <td>在取得記號之前，請確定您具有<code>管理員</code>許可權。如需協助取得 IAM 記號，請參閱 <a href="/docs/iam?topic=iam-iamtoken_from_apikey#iamtoken_from_apikey" target="_blank">文件 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。</td>
  </tr>
</table>

若要執行 Script，請執行下列動作：

1. 複製<a href="https://github.com/ibm-cloud-security/appid-sample-code-snippets/tree/master/export-import-cloud-directory-users" target="_blank">儲存庫 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。
2. 開啟主控台，移至您複製儲存庫的資料夾。
3. 執行下列指令。

  ```
  npm install
  ```
  {: codeblock}

4. 搭配您的參數，執行下列指令。

  ```
  users_export_import 'sourceTenantId' 'destinationTenantId' 'region' 'iamToken'
  ```
  {: codeblock}

  指令範例：

  ```
  users_export_import e00a0366-53c5-4fcf-8fef-ab3e66b2ced8 73321c2b-d35a-497a-9845-15c580fdf58c ng eyJraWQiOiIyMDE3MTAyNS0xNjoyNzoxMCIsImFsZyI6IlJTMjU2In0.eyJpYW1faWQiOiJJQk1pZC0zMTAwMDBUNkZTIiwiaWQiOiJJQk1pZC0zMTAwMDBUNkZTIiwicmVhbG1pZCI6IklCTWlkIiwiaWRlbnRpZmllciI6IjMxMDAwIFQ2RlMiPCJnaXZlbl9uYW1lIjoiUm90ZW0iLCJmYW1pbHlfbmFtZSI6IkJyb3NoIiwibmFtZSI6IlJvdGVtIEJyb3NoIiwiZW1haWwiOiJyb3RlbWJyQGlsLmlibS5jb20iLCJzdWIiOiJyb3RlbWJyQGlsLmlibS5jb20iLCJhY2NvdW50Ijp7ImJzcyI6ImQ3OWM5YTk5NjJkYzc2Y2JkMDZlYTVhNzhjMjY0YzE5In0sImlhdCI6MTUzNrE3Mjg4NCwiZXhwIjoxNTM3MTc2NDg0LCJpc3MiOiJodHRwczovL2lhbS5zdGFnZTEuYmx1ZW1peC5uZXQvaWRlbnRpdHkiLCJncmFudF90eXBlIjoidXJuOmlibTpwYXJhbXM6b2F1dGg6Z3JhbnQtdHlwZTpwYXNzY29kZSIsInNjb3BlIjoiaWJtIG9wZW5pZCIsImNsaWVudF9pZCI6ImJ4IiwiYWNyIjoxLCJhbXIiOlsicHdkIl19.c4vLPzhvvNZLjaLy7znDa37qV4o-yuGmSKmJoQKrEQNZU8IC0NIjxwSo7W9kb0pDi3Yf_03_9ufTTGNfjtltzNWycSXjkNgoL-b9_nU61oHdgn0stY1KmNicqyBWfgUU--4xa904QN_QjRHBaUBeJf3XWEphPIMoF7mZeOxEZLnCMcQXSz9pImCMiP4SNT38cHLiI90Yx01rM7hpteepWULh5MYh-B2V03Gkgxfqvv951HF1LDg6eT4Q9in11laTQKtKuomripUju_4GIIjORVYw9NaAVKIJ9lKrPX0SKPhStsa59qGsC_7Uersms5EY1W1VbZVqOZPJbtp6tVf-Lw
  ```
  {: codeblock}
