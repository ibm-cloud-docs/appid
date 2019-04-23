---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

keywords: authentication, authorization, identity, app security, secure, custom, proprietary, private key, public key, jwt

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

# 自訂
{: #custom-identity}

當您鑑別時，可以使用自己的自訂身分提供者。您的身分提供者可以符合任何不是 {{site.data.keyword.appid_full}} 特別支援的鑑別機制，其中包括專屬鑑別機制。
{: shortdesc}

當 {{site.data.keyword.appid_short_notm}} 沒有提供特定身分提供者的直接支援時，您可以使用自訂身分流程，將鑑別通訊協定橋接至 {{site.data.keyword.appid_short_notm}} 的現有鑑別流程。例如，您要使用 GitHub 或 LinkedIn 來容許使用者登入。您可以使用身分提供者的現有 SDK 來協助使用者鑑別資訊，然後將其包裝並與 {{site.data.keyword.appid_short_notm}} 交換。在許多企業情境中，舊式身分提供者可能使用自己的自訂鑑別通訊協定，但您仍想要運用 {{site.data.keyword.appid_short_notm}} 的功能。對於這種類型的情境，自訂身分流程提供取消連結的方法，其可安全地鑑別使用者，而不公開其認證。

## 配置自訂身分
{: #custom-configure}

您可以使用下列步驟，將自訂身分提供者配置為使用 {{site.data.keyword.appid_short_notm}}。
{: shortdesc}

### 開始之前
{: #custom-identity-before}

若要建立 {{site.data.keyword.appid_short_notm}} 與自訂身分提供者之間的信任，您必須具有長度下限為 2048 的 RSA PEM 金鑰組。請務必安全地備份您在正式作業中使用的所有金鑰。

如何使用金鑰？

- 您的私密金鑰用於應用程式或身分提供者，以簽署 JWT。
- 您的公開金鑰是由 {{site.data.keyword.appid_short_notm}} 用來驗證包含使用者資訊的 JWT。

若要使用 Open SSL 來產生 RSA PEM 金鑰組，請執行下列指令：

```
$ openssl genpkey -algorithm RSA -out private_key.pem -pkeyopt rsa_keygen_bits:2048
$ openssl rsa -pubout -in private_key.pem -out public_key.pem
```
{: codeblock}

</br>

### 使用 GUI 配置
{: #custom-identity-configure-gui}

1. 登入您的 {{site.data.keyword.cloud_notm}} 帳戶，然後導覽至您的 {{site.data.keyword.appid_short_notm}} 實例。

2. 在**管理**標籤中，將**自訂身分提供者**設為**開啟**。

3. 向 {{site.data.keyword.appid_short_notm}} 登錄您的公開金鑰。
  1. 導覽至**自訂身分提供者**標籤。
  2. 在**公開金鑰**方框中貼上您的公開金鑰，然後按一下**儲存**。



### 使用 API 進行配置
{: #custom-identity-configure-api}

對[管理 API 端點](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_custom_idp)提出 PUT 要求，以登錄您的金鑰。

```
Put {Management URI}/config/idps/custom
Content-Type: application/json
{
    isActive: true,
    config: {
        publicKey: <Your newline separated (\n) PEM public key>
    }
}
```
{: codeblock}

## 測試您的配置
{: #custom-identity-testing}

在使用有效的公開金鑰配置 {{site.data.keyword.appid_short_notm}} 實例之後，您可以使用服務所提供的測試應用程式來驗證已正確設定您的配置。在範例應用程式中，您可以看到在標準登入流程期間傳回的 {{site.data.keyword.appid_short_notm}} 存取和身分記號有效負載。

1. 從**自訂身分提供者**標籤中，按一下**測試**來開啟測試應用程式。

2. 遵循自訂身分[通訊協定](/docs/services/appid?topic=appid-custom-auth#generating-jwts)，使用 [JWT.io](https://jwt.io/) 來建立範例 JWT。

3. 將您的 JWT 貼至標示為 **JSON Web 記號**的方框中，然後按一下**測試**來執行範例鑑別。

如果成功，您現在可以看到已解碼的 {{site.data.keyword.appid_short_notm}} 身分及存取記號，而您的應用程式可在標準登入流程中使用這些記號。

## 後續步驟
{: #custom-identity-next}

既然已配置您的自訂身分提供者，請[將它新增至您的應用程式](/docs/services/appid?topic=appid-custom-auth#custom-auth)！
