---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-09"

keywords: Authentication, authorization, identity, app security, secure, development,

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

# 入門指導教學
{: #getting-started}

應用程式安全可能非常複雜。對於大部分的開發人員而言，這是建立應用程式時，其中一個最難的部分。如何才能確定您正在保護使用者資訊？藉由將 {{site.data.keyword.appid_full}} 整合至您的應用程式，您可以保護資源並新增鑑別；即使您沒有太多安全經驗也是一樣。
{: shortdesc}

藉由要求使用者登入您的應用程式，您可以儲存使用者資料（例如來自公用社交設定檔中的應用程式喜好設定或資訊），然後使用該資料來自訂您應用程式的每一個體驗。{{site.data.keyword.appid_short_notm}} 為您提供一個架構，但您也可以在使用雲端目錄時，帶入自己的品牌登入畫面。

我們很樂意聽取您的意見和問題！
* 如果您有 {{site.data.keyword.appid_short_notm}} 的相關技術問題，請將問題張貼在 <a href="https://stackoverflow.com" target="_blank">Stack Overflow <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>，並使用 `ibm-appid` 來標記問題。
* 若為服務及開始使用指示的相關問題，請使用 <a href="https://developer.ibm.com" target="_blank">dW Answers <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 討論區。請包括 `appid` 標籤。

## 建立服務實例
{: #create}

建立 {{site.data.keyword.appid_short_notm}} 的實例，並將其連結至您的應用程式，以開始使用。
{: shortdesc}

1. 在 {{site.data.keyword.cloud_notm}} 型錄中，選取 {{site.data.keyword.appid_short_notm}}。即會開啟服務配置畫面。
2. 提供服務實例的名稱，或使用預設名稱。
3. 選取定價方案，然後按一下**建立**。
4. 連結您的 {{site.data.keyword.appid_short_notm}} 實例。
    1. 若要查看您可以連結至服務實例的應用程式清單，請按一下**連線**。
    2. 按一下**建立連線**。即會開啟一個頁面，其中具有您可以選擇連結的所有應用程式。
    3. 在您要連結的應用程式上按一下**連接**。
    4. 按一下**重新編譯打包**來套用變更。

就這樣！您已準備好開始配置您的應用程式設定。

## 配置範例應用程式
{: #sample-app}

您可以使用其中一個預先配置的範例應用程式來熟悉如何使用服務。
{: shortdesc}

根據預設，範例應用程式已配置兩個身分提供者，而且可以檢閱鑑別。`iOS Swift`、`Android`、`Node.js` 及 `Java` 中提供有範例應用程式。如果您沒有看到感覺可以輕鬆運作的語言，請不要擔心！您可以使用提供的 API，將 {{site.data.keyword.appid_short_notm}} 整合至自己的範例應用程式。

若要建置範例應用程式，請執行下列動作：

1. 按一下**下載範例**。
2. 按一下您選擇的語言來下載範例。看不到您尋找的語言嗎？不必擔心！您可以透過 API 利用 {{site.data.keyword.appid_short_notm}}。
  {: tip}
3. 確定您已安裝或完成必備項目。
4. 遵循**建置並執行**步驟，使用 {{site.data.keyword.appid_short_notm}} 來設定您的範例。
5. 按一下**檢閱活動**，以查看所有已發生的鑑別事件。任何類型的登入都會建立一個可在此頁面上看到的事件。
6. 自訂登入小組件。
  1. 按一下**選取**，然後瀏覽您的本端系統以取得要上傳的影像，來新增影像（例如品牌標誌）。
  2. 選取其中一個顏色選項，或以十六進位值指定，來選擇色系。
  3. 在網站與行動裝置之間變更，以在每一種類型的裝置上查看色系的外觀。
  4. 當您滿意選擇時，請按一下**儲存變更**。
7. 在瀏覽器中，重新整理您的登入頁面。即可看到您在前一個步驟中進行的變更。


## 後續步驟
{: #next}

準備好進入並開始使用您自己的應用程式嗎？從[將服務新增至您的應用程式](/docs/services/appid?topic=appid-web-apps#web-apps)開始。服務提供適用於最常用語言的 SDK，但如果您看不到撰寫應用程式所用之語言的 SDK，則仍然可以使用 API 來充分運用 {{site.data.keyword.appid_short_notm}}。
