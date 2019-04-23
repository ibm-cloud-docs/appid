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


# 管理使用者
{: #cd-users}

當您啟用 Cloud Directory 時，使用者可以使用電子郵件或使用者名稱及密碼來註冊您的應用程式。
{: shortdesc}


Cloud Directory 使用者與 {{site.data.keyword.appid_short_notm}} 使用者不同。使用者可以使用不同於您所配置的身分提供者選項來註冊您的應用程式。本主題所提及的使用者，是選擇在註冊您的應用程式時使用 Cloud Directory 選項的那些使用者。
{: note}


## 新增及刪除使用者
{: #add-delete-users}

您可以透過 {{site.data.keyword.appid_short_notm}} 儀表板或使用 API 來管理 Cloud Directory 使用者。
{: shortdesc}

若要查看特定使用者的完整資料，您可以使用 API 將 Cloud Directory 使用者資訊傳回為 JSON 物件。若要查看 {{site.data.keyword.appid_short_notm}} 支援的完整使用者資料集，請參閱 [SCIM 核心綱目](https://tools.ietf.org/html/rfc7643#section-8.2)。

### 新增使用者
{: #add-users}

您可以使用下列步驟，透過 {{site.data.keyword.appid_short_notm}} 儀表板來新增使用者。

基於測試目的，您可以透過 {{site.data.keyword.appid_short_notm}} 儀表板來新增使用者。

1. 導覽至 {{site.data.keyword.appid_short_notm}} 儀表板的 **Cloud Directory > 使用者**標籤。

2. 按一下**新增使用者**。即會顯示表單。

3. 輸入**名字**、**姓氏**、**電子郵件**及**密碼**。請確定您嘗試要登錄的電子郵件尚未由另一位使用者使用。若要確定您已正確鍵入密碼，請在**重新輸入密碼**欄位中輸入該密碼來加以確認。

4. 按一下**儲存**。即建立 Cloud Directory 使用者。


### 刪除使用者
{: #delete-users}

如果您要從目錄中移除使用者，則可以從 GUI 中刪除該使用者。

1. 導覽至 {{site.data.keyword.appid_short_notm}} 儀表板的 **Cloud Directory > 使用者**標籤。

2. 請按一下您要刪除之使用者旁的勾選框。即會顯示方框。

3. 在此方框中，按一下**刪除**。即會顯示畫面。

4. 按一下**刪除**，以確認您瞭解刪除使用者動作無法復原。如果此動作是錯的，您可以重新將使用者新增至目錄中，但該使用者的任何相關資訊已不再可用。


## 移轉使用者
{: #user-migration}

您有時可能需要設定新的 {{site.data.keyword.appid_short_notm}} 實例。如果您是使用「雲端目錄」，這表示您的使用者必須移轉至新的實例。您可以使用管理 API 來協助移轉。
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
    <td>在取得記號之前，請確定您具有<code>管理員</code>許可權。如需協助取得 IAM 記號，請參閱<a href="https://cloud.ibm.com/docs/iam/apikey_iamtoken.html#iamtoken_from_apikey" target="_blank">文件 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。</td>
  </tr>
</table>

若要執行 Script，請執行下列動作：

1. 複製<a href="https://github.com/ibm-cloud-security/appid-sample-code-snippets/tree/master/export-import-cloud-directory-users" target="_blank">儲存庫 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。
2. 開啟終端機，並導覽至您將儲存庫複製到其中的資料夾。
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
