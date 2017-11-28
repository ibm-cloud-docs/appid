---

copyright:
  years: 2017
lastupdated: "2017-11-02"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# 保護 Liberty for Java 資源
{: #protecting-liberty}

您可以使用 {{site.data.keyword.appid_short_notm}} 在 IBM Liberty for Java 應用程式中保護端點。Liberty for Java 有內建的功能，可以處理 Open ID Connect (OIDC) 要求。

## 開始之前
{: #begin}

* 您需要現有、未連結的 [IBM Liberty for Java 應用程式](https://console.bluemix.net/catalog/starters/liberty-for-java)。若要熟悉開發 Liberty for Java 應用程式，請參閱[文件](/docs/runtimes/liberty/index.html)。
* 務必要安裝 [Apache Maven](https://maven.apache.org/download.cgi)。
* 瞭解 OIDC 與 Liberty for Java 搭配運作的情形。

## 保護 Liberty for Java 中的資源
{: #protecting-liberty}

1. 從使用者介面下載 Liberty for Java 範例。範例包含具有標準 Liberty 檔案的壓縮檔案。

2. 在您擷取範例所在的目錄開啟終端機。

3. 使用 Cloud Foundry 指令行登入 {{site.data.keyword.Bluemix_notm}}。提示時，輸入您的認證。

  ```
  cf login
  ```
  {: codeblock}

4. 部署應用程式。執行下列指令會建立名稱與承租戶 ID 相關的 Liberty for Java 實例。

  ```
  cf push
  ```
  {: codeblock}

5. 將您的服務實例連結至新的 Liberty for Java 實例，然後重新部署應用程式。

6. 在瀏覽器中開啟您的應用程式，並使用您的認證登入，以檢閱鑑別活動。


## 更新 Liberty for Java 範例
{: #updating-liberty}

若要在範例應用程式中進行更新，請使用下列指示：

1. 建立 servlet、jsp 及 html。
2. 定義受保護的資源，然後將它們新增至 `web.xml` 和 `server.xml` 授權過濾器。
3. 建立 war 檔然後將它部署至 Liberty for Java。

如需更新應用程式的相關資訊，請參閱[將 {{site.data.keyword.appid_short_notm}} 新增至現有的應用程式](/docs/services/appid/existing.html#existing-liberty)。
