---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:tip: .tip}

# 入門指導教學
{: #gettingstarted}

應用程式安全可能非常複雜。對於大部分的開發人員而言，這是建立應用程式的其中一個最難的部分。如何才能確定您正在保護使用者資訊？藉由將 {{site.data.keyword.appid_full}} 整合至您的應用程式，您可以保護資源並新增鑑別；即使您沒有太多安全經驗也是一樣。
{: shortdesc}

藉由要求使用者登入您的應用程式，您可以儲存使用者資料（例如來自公用社交設定檔中的應用程式喜好設定或資訊），然後使用該資料來自訂您應用程式的每一個體驗。App ID 為您提供一種登入架構，但您也可以在使用雲端目錄時，將自己的特有風格帶入登入畫面中。

身為帳戶擁有者，您現在可以設定原則，以定義團隊成員如何與 {{site.data.keyword.appid_short_notm}} 實例進行互動。您可以決定誰可以建立、更新及刪除服務的實例。如需相關資訊，請參閱[服務存取管理](/docs/services/appid/iam.html)。
{:tip}

## 建立服務實例
{: #create}

建立 {{site.data.keyword.appid_short_notm}} 的實例，並將其連結至您的應用程式，以開始使用。
{: shortdesc}

1. 在 {{site.data.keyword.Bluemix}} 型錄中，選取 {{site.data.keyword.appid_short_notm}}。即會開啟服務配置畫面。
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

根據預設，範例應用程式已配置兩個身分提供者，而且可以檢閱鑑別。您也可以使用登入小組件特性來自訂登入頁面，以及查看在應用程式中顯示您進行的更新的速度。

若要從 GUI 配置範例應用程式，請執行下列動作：

1. 在您建立服務的實例之後，可以選擇使用您覺得適合處理的語言的範例應用程式。您可以從 iOS Swift、Android、Node.js 及 Java 中進行選擇。不使用 SDK 嗎？您可以使用 API 來整合 {{site.data.keyword.appid_short_notm}}。
2. 遵循 GUI 中的步驟，以**建置並執行**範例應用程式。每一種語言的配置略有不同，因此，請務必選取您已從下拉清單下載的應用程式語言。配置應用程式之後，即可在瀏覽器中進行開啟，並使用您的認證登入。
  請確定已安裝應用程式語言的必備項目。
  <dl>
    <dt> Android</dt>
      <dd><ul><li> Android API 27 或更高版本</li><li> Java 8.x </li><li> Android SDK Tools 25.2.5+ </li><li> Android SDK Platform Tools 26.1.1+ </li><li> Android Build Tools 27.0.0+ 版</li></ul></dd>
    <dt> iOS Swift </dt>
      <dd><ul><li> CocoaPods（1.1.0 版或更高版本）</li><li> iOS 10.0 或更高版本</li><li> MacOS 10.11.5 </li><li> Xcode（9.0.1 版或更高版本）</li></ul></dd>
    <dt> Node.js </dt>
      <dd><ul><li> {{site.data.keyword.Bluemix_notm}} CLI</li></ul></dd>
    <dt> Java

</dt>
      <dd><ul><li> {{site.data.keyword.Bluemix_notm}} CLI </li><li> Maven </li></ul></dd>
  </dl>

  看不到您尋找的語言嗎？不必擔心！您可以透過 API 利用 {{site.data.keyword.appid_short_notm}}。您也可以查看<a href="https://www.ibm.com/blogs/bluemix/tag/app-id/" target="_blank">我們的部落格 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>，以取得其他語言的額外協助。
  {: tip}

3. 按一下**檢閱活動**，以查看已發生的鑑別事件。登入之後，您可以看到事件。
4. 自訂登入體驗。您可以選取影像（例如您的標誌及標頭顏色）。您可以選取其中一個顏色選項，或插入十六進位值。當您滿意預覽結果時，請按一下**儲存變更**。
5. 在瀏覽器中，重新整理登入頁面。即可看到您在前一個步驟中進行的變更。

## 後續步驟
{: #next}

準備好進入並開始使用您自己的應用程式嗎？從[將服務新增至您的應用程式](/docs/services/appid/install.md)開始。服務提供適用於最常用語言的 SDK，但如果您看不到撰寫應用程式之語言的 SDK，則仍然可以使用 API。

</br>
</br>
