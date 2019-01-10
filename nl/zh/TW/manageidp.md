---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}


# 管理
{: #managing}

身分提供者 (IdP) 透過鑑別新增行動及 Web 應用程式的安全等級。使用 {{site.data.keyword.appid_full}}，您可以配置一個或數個身分提供者，以建立使用者的自訂登入體驗。
{: shortdesc}


**何謂身分提供者？**

身分提供者可建立及管理使用者、功能 ID 或應用程式這類實體的相關資訊。提供者會使用認證（例如密碼）來驗證實體的身分。然後，IdP 會將身分資訊傳送給另一個服務提供者。因為身分提供者會鑑別實體，所以 {{site.data.keyword.appid_short_notm}} 能夠授權它，並授與您應用程式的存取權。

</br>

**何謂 {{site.data.keyword.appid_short_notm}} 為其提供整合的身分提供者？**

已預先配置服務使用數個提供者。

<table>
  <tr>
    <th>提供者</th>
    <th>類型</th>
    <th>說明</th>
  </tr>
  <tr>
    <td>[Cloud Directory](/docs/services/appid/cloud-directory.html)</td>
    <td>受管理登錄</td>
    <td>您可以在雲端中維護您自己的使用者登錄。使用者註冊應用程式時，即會將他們新增至使用者目錄。此選項可讓使用者在應用程式內更自由地管理自己的帳戶。</td>
  </tr>
  <tr>
    <td>[SAML](/docs/services/appid/enterprise.html)</td>
    <td>企業</td>
    <td>您可以建立一般使用者的單一登入體驗。</td>
  </tr>
  <tr>
    <td>[Facebook](/docs/services/appid/identity-providers.html#facebook)</td>
    <td>社交</td>
    <td>一般使用者可以使用其 Facebook 認證來登入您的應用程式。</td>
  </tr>
  <tr>
    <td>[Google+](/docs/services/appid/identity-providers.html#google)</td>
    <td>社交</td>
    <td>一般使用者可以使用其 Google+ 認證來登入您的應用程式。</td>
  </tr>
  <tr>
    <td>[自訂](/docs/services/appid/custom.html)</td>
    <td> </td>
    <td>如果提供的選項不符合您的特定需求，則您可以配置自己的身分流程來使用 {{site.data.keyword.appid_short_notm}}。</td>
  </tr>
  
</table>

</br>

**{{site.data.keyword.appid_short_notm}} 如何與身分提供者互動？**

{{site.data.keyword.appid_short_notm}} 透過使用多個通訊協定（例如 OpenID Connect、SAML 等等）與身分提供者互動。例如，OpenID Connect 是與許多社交提供者（例如 Facebook、Google）搭配使用的通訊協定。企業提供者（例如 <a href="https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-azure-active-directory/" target="_blank">Azure Active Directory <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 或 <a href="https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-active-directory-federation-service/" target="_blank">Active Directory Federation Service <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>）通常會使用 SAML 作為其身分通訊協定。對於 [Cloud Directory](cloud-directory.html)，此服務使用 SCIM 來驗證身分資訊。

使用應用程式身分？請查看[應用程式身分](app-to-app.html)。
{: tip}

</br>
</br>

## 配置設定
{: #configuring}

您可以決定想要使用的提供者、重新導向 URL 及您應用程式的記號資訊。您配置的設定會套用至此服務實例中的所有身分提供者。例如：當您設定記號有效期限時，它會套用至您已配置的所有提供者，不論其為社群還是企業。

</br>

**若要配置提供者，請執行下列動作：**

1. 導覽至服務儀表板。
2. 在導覽的**身分提供者**區段中，選取**管理**頁面。
3. 在**身分提供者**標籤上，將您要使用的提供者設為**開啟**。
4. 選用項目：決定關閉**匿名使用者**還是保留預設值（即**開啟**）。設為**開啟**時，自訂使用者屬性會與使用者相關聯，從這時開始，即會開始與您的應用程式互動。如需變成已識別使用者之路徑的相關資訊，請參閱[漸進鑑別](progressive.html#progressive)。

{{site.data.keyword.appid_short_notm}} 提供預設認證來協助您初次設定 Facebook 及 Google+。您有每天每個實例 100 次認證使用的限制。因為它們是 IBM 認證，所以表示只能用於開發。在發佈應用程式之前，請將配置更新為您自己的認證。
{: tip}

</br>

**若要配置設定，請執行下列動作：**

1. 新增重新導向 URL。重新導向 URL 是應用程式的回呼端點。為了防止網路釣魚攻擊，{{site.data.keyword.appid_short_notm}} 會根據白名單來驗證 URL。
  1. 在**新增 Web 重新導向 URL** 欄位中，鍵入 URL，然後按一下 **+** 圖示。
  2. 重複步驟 1，直到將所有可能的重新導向 URL 都新增至清單為止。

  請不要在您的 URL 中包括任何查詢參數。在驗證處理程序中，會忽略它們。例如：`http://host:[port]/path`
  {: tip}

2. 配置記號。記號生命期限會在每位使用者登入時再次開始。例如，您將重新整理記號生命期限設為 10 天。使用者第一次登入時，會建立存取記號及重新整理記號。如果使用者幾天後回到您的應用程式（較具體為 3 天），則不需要重新登入。但是，如果使用者已在其起始登入之後等待 12 天後回到您的應用程式，則需要再次登入，而且會有一組記號與使用者相關聯。
  1. 若要容許登入，而不需要使用者互動，請將**重新整理記號**設為**開啟**。
  2. 設定重新整理記號生命期限。有效期限是以日為單位來設定，而且可以是 1 到 90 範圍內的任何值。數字越小，使用者必須自行登入的頻率就越高。
  3. 設定存取記號生命期限。有效期限是以分鐘為單位來設定，而且範圍在 5 到 1440 之間。值越小，您在記號被竊取時會有更多的保護。
  4. 設定匿名記號生命期限。在使用者開始與您的應用程式互動時，會將[匿名記號](/docs/services/appid/progressive.html#anonymous)指派給使用者。使用者登入時，會將匿名記號中的資訊傳送至與使用者相關聯的記號。有效期限是以日為單位來設定，而且可以是 1 與 90 之間的任何值。

</br>
</br>
