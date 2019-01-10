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


# 多因子鑑別
{: #mfa}

「多因子鑑別 (MFA)」是一種確認使用者身分的方法，方法是除了他們知道要驗證其身分的某個事項之外，還要求他們使用現有的某個事項。例如，使用 {{site.data.keyword.appid_full}}，您可以讓使用者輸入一次性代碼，而此代碼會在輸入其電子郵件及密碼之後傳送至其電子郵件。
{: shortdesc}

MFA 僅適用於 Cloud Directory 使用者。如果您使用具有 SAML 2.0 的企業登入或是社交登入，則可以在您使用的身分提供者中啟用 MFA。
{: note}

啟用 MFA 時，每次新使用者嘗試登入時，登入小組件都需要 MFA。在使用者順利輸入其認證之後，會將一次性密碼傳送至其在建立帳戶時所登錄的電子郵件位址。每個代碼都為六個字元，且有效期限為五分鐘。如果使用者未收到其代碼，則可以要求傳送另一個代碼，但不會重設有效期限。代碼到期之後，會強制執行使用者來重複整個登入處理程序。

如果尚未透過管理 API 或在註冊時透過電子郵件驗證來確認使用者電子郵件，則會在 MFA 代碼驗證成功時確認該使用者電子郵件。如果您需要變更使用者的電子郵件位址，則管理者可以使用[管理 API](https://appid-management.ng.bluemix.net/swagger-ui/#!/Cloud_Directory_Users/updateCloudDirectoryUser)。

MFA 適用於[累進層級定價方案](faq.html#pricing)上的 {{site.data.keyword.appid_short_notm}} 實例。
{: note}

## 瞭解流程
{: #understanding}



1. 會向應用程式使用者顯示 {{site.data.keyword.appid_short_notm}} 的預設登入使用者介面。

2. 使用者輸入其 Cloud Directory 使用者認證，例如其電子郵件或使用者名稱及其密碼。

3. 即會驗證認證，並傳回 MFA 表單。此表單會要求使用者貼上透過電子郵件所傳送的代碼。

4. 使用者會收到其電子郵件位址的一次性密碼，並將它輸入預設的 MFA 使用者介面。

5. 系統會驗證 MFA 代碼，並使用授權碼將其重新導向至用戶端應用程式，以繼續 OAuth 2 流程。


</br>

## 配置 MFA
{: #configuration}

支援 {{site.data.keyword.appid_short_notm}} MFA 作為透過登入小組件之 Cloud Directory 使用者的 OAuth 2.0 授權碼流程一部分。
{: shortdesc}

若要透過 GUI 配置 MFA，請查看 [Cloud Directory](cloud-directory.html)。
{: note}

### 使用 API 配置

您可以使用管理 API，來配置 MFA。
{: shortdesc}

**開始之前**

請確定您具有下列必備項目：

* {{site.data.keyword.appid_short_notm}} 實例的承租戶 ID。您可以在儀表板的**服務認證**區段中找到此值。
* Identity and Access Management (IAM) 記號。如需取得 IAM 記號的協助，請查看 [IAM 文件](/docs/iam/apikey_iamtoken.html)。


1. 啟用 MFA，方法是使用將 `isActive` 設為 `true` 的 MFA 配置，以對 `/config/mfa` 端點提出 PUT 要求。

  標頭：
  ```
  PUT {management-url}/management/v4/{tenantId}/config/mfa
       Host: <management-server-url>
       Authorization: Bearer <IAM_TOKEN>
       Content-Type: application/json
  ```
  {: pre}

  內文：
  ```
   {
       "isActive": true
   }
  ```
  {: pre}

  範例要求：
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

2. 啟用 MFA 頻道，方法是使用 MFA 配置，以對 `/mfa/channels/{channelType}` 端點提出 PUT 要求。`isActive` 設為 `true` 時，會啟用 MFA 頻道。

  標頭：
  ```
  PUT /management/v4/{tenantId}/mfa/channels/{channelType}
       Host: <management-server-url>
       Authorization: Bearer <IAM_TOKEN>
       Content-Type: application/json
  ```
  {: pre}

  <table>
    <thead>
      <th colspan=3>支援的頻道類型</th>
    </thead>
    <tbody>
      <tr>
        <td>`email`</td>
      </tr>
    </tbody>
  </table>

  內文：
  ```
   {
       "isActive": true
   }
  ```
  {: pre}

  範例要求：
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
