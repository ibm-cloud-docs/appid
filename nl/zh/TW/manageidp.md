---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-20"

keywords: authentication, authorization, identity, app security, secure, development, identity provider, tokens, customization, lifetime

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


# 管理鑑別
{: #managing-idp}

身分提供者 (IdP) 透過鑑別新增行動及 Web 應用程式的安全等級。使用 {{site.data.keyword.appid_full}}，您可以配置一個或數個身分提供者，以建立使用者的自訂登入體驗。
{: shortdesc}


{{site.data.keyword.appid_short_notm}} 使用多個通訊協定（例如 OpenID Connect、SAML 等等）與身分提供者互動。例如，OpenID Connect 是與許多社交提供者（例如 Facebook、Google）搭配使用的通訊協定。企業提供者（例如 <a href="https://www.ibm.com/cloud/blog/setting-ibm-cloud-app-id-azure-active-directory" target="_blank">Azure Active Directory <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 或 <a href="https://www.ibm.com/cloud/blog/setting-ibm-cloud-app-id-active-directory-federation-service" target="_blank">Active Directory Federation Service <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>）通常會使用 SAML 作為其身分通訊協定。對於[雲端目錄](/docs/services/appid?topic=appid-cloud-directory)，此服務使用 SCIM 來驗證身分資訊。

當您使用社交或企業身分提供者時，{{site.data.keyword.appid_short_notm}} 具有使用者帳戶資訊的讀取權。此服務會使用記號以及身分提供者所傳回的主張，來驗證使用者的身分。因為此服務永不具有資訊的寫入權，所以使用者必須透過其選擇的身分提供者執行動作，例如重設其密碼。例如，如果使用者使用 Facebook 來登入您的應用程式，然後想要變更其密碼，他們必須移至 `www.facebook.com` 才能執行此動作。

當您使用[雲端目錄](/docs/services/appid?topic=appid-cloud-directory)時，{{site.data.keyword.appid_short_notm}} 是身分提供者。此服務會使用您的登錄來驗證您的使用者身分。因為 {{site.data.keyword.appid_short_notm}} 是提供者，所以使用者可以直接在您的應用程式中充分運用進階功能，例如重設其密碼。

使用應用程式身分？請參閱[應用程式身分](/docs/services/appid?topic=appid-app)。
{: tip}

服務可以配置使用的提供者有好幾個。請查看下表，以瞭解您的選項。

<table>
  <tr>
    <th>提供者</th>
    <th>類型</th>
    <th>說明</th>
  </tr>
  <tr>
    <td>[雲端目錄](/docs/services/appid?topic=appid-cloud-directory)</td>
    <td>受管理登錄</td>
    <td>您可以在雲端中維護自己的使用者登錄。當使用者註冊應用程式時，即會將他們新增至使用者目錄。此選項讓使用者在應用程式內更自由地管理自己的帳戶。</td>
  </tr>
  <tr>
    <td>[SAML](/docs/services/appid?topic=appid-enterprise#enterprise)</td>
    <td>企業</td>
    <td>您可以為一般使用者建立單一登入體驗。</td>
  </tr>
  <tr>
    <td>[Facebook](/docs/services/appid?topic=appid-social#facebook)</td>
    <td>社交</td>
    <td>一般使用者可以使用其 Facebook 認證來登入您的應用程式。</td>
  </tr>
  <tr>
    <td>[Google+](/docs/services/appid?topic=appid-social#google)</td>
    <td>社交</td>
    <td>一般使用者可以使用其 Google 認證來登入您的應用程式。</td>
  </tr>
  <tr>
    <td>[自訂](/docs/services/appid?topic=appid-custom-identity#custom-identity)</td>
    <td> </td>
    <td>如果提供的選項都不符合您的特定需求，您可以配置自己的身分流程來使用 {{site.data.keyword.appid_short_notm}}。</td>  
  </tr>
</table>

## 管理提供者
{: #managing-providers}

身分提供者可建立及管理使用者、功能 ID 或應用程式這類實體的相關資訊。提供者會使用認證（例如密碼）來驗證實體的身分。然後，IdP 會將身分資訊傳送給另一個服務提供者。因為身分提供者會鑑別實體，所以 {{site.data.keyword.appid_short_notm}} 能夠對其進行授權，並授與您應用程式的存取權。
{: shortdesc}

若要管理您的身分提供者，請執行下列動作：

1. 導覽至服務儀表板。
2. 在導覽的**身分提供者**區段中，選取**管理**頁面。
3. 在**身分提供者**標籤上，將您要使用的提供者設為**開啟**。
4. 選用項目：決定是要關閉**匿名使用者**，還是保留預設值（即**開啟**）。如果設為**開啟**，則從使用者開始與應用程式互動的那一刻起，使用者屬性就與該使用者相關聯。如需如何變成已識別使用者的相關資訊，請參閱[漸進鑑別](/docs/services/appid?topic=appid-anonymous#progressive)。

{{site.data.keyword.appid_short_notm}} 提供預設認證來協助您初次設定 Facebook 及 Google+。您有每天每個實例 100 次認證使用的限制。因為它們是 IBM 認證，所以表示只能用於開發。在發佈應用程式之前，請將配置更新為您自己的認證。
{: tip}


## 新增重新導向 URI
{: #add-redirect-uri}

重新導向 URI 是應用程式的回呼端點。在登入流程期間，{{site.data.keyword.appid_short_notm}} 會在容許用戶端參與授權工作流程之前先驗證 URI，這有助於防止網路釣魚攻擊及授權碼洩漏。透過登錄 URI，您將告訴 {{site.data.keyword.appid_short_notm}} 此 URI 是可信任的，可以將您的使用者重新導向。

請務必只登錄您信任的應用程式 URI。
{: note}


1. 按一下**鑑別設定**，以查看 URI 及記號配置選項。

2. 在**新增 Web 重新導向 URI** 欄位中，鍵入 URI。每一個 URI 都應該以 `http://` 或 `https://` 作為開頭，而且必須包含完整路徑，其中包括要讓重新導向順利完成的任何查詢參數。需要格式化 URI 的協助？請查看下表的一些範例。

  <table>
    <tr>
      <th>類型</th>
      <th>範例 URI</th>
    </tr>
    <tr>
      <td>自訂網域</td>
      <td><code>http://mydomain.net/myapp2path/appid_callback</code></td>
    </tr>
    <tr>
      <td>Ingress 子網域</td>
      <td><code>https://mycluster.us-south.containers.appdomain.cloud/myapp1path/appid_callback</code></td>
    </tr>
    <tr>
      <td>登出</td>
      <td><code>http://mydomain.net/myapp2path/appid_logout</code></td>
    </tr>  
  </table>

3. 按一下**新增 Web 重新導向 URI** 方框中的 **+** 符號。

4. 重複步驟 1 到 3，直到所有可能的 URI 都新增至您的清單為止。



不確定您的重新導向 URI 從何而來？請觀看下列簡短視訊以瞭解在何處取得它，以及如何將它新增至您的清單。

<iframe class="embed-responsive-item" id="redirecturi" title="{{site.data.keyword.appid_short_notm}}：如何修正無效的重新導向 URI" type="text/html" width="640" height="390" src="//www.youtube.com/embed/6hxqbvpc054?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>



## 配置記號生命期限
{: #idp-token-lifetime}

記號生命期限會在每位使用者登入時重新開始。例如，您將重新整理記號生命期限設為 10 天。使用者第一次登入時，會建立存取記號及重新整理記號。如果使用者幾天後回到您的應用程式（具體來說，如 3 天），則不需要重新登入。但是，如果使用者在其起始登入之後等待 12 天後才回到您的應用程式，則需要重新登入，而且會有一組記號與使用者相關聯。如需記號的相關資訊，請參閱[瞭解記號](/docs/services/appid?topic=appid-tokens#tokens)。

1. 若要容許登入而不需要使用者互動，請將**重新整理記號**設為**開啟**。

2. 設定您的重新整理記號生命期限。有效期限是以天為單位設定，且可以是範圍 1 到 90 內的任何值。數字越小，使用者必須自行登入的頻率就越高。

3. 設定您的存取記號生命期限。有效期限是以分鐘為單位設定，且可以在範圍 5 到 1440 內。值越小，您就有越多保護以防止記號被竊取。

4. 設定您的匿名記號生命期限。在使用者開始與您的應用程式互動時，即會將[匿名記號](/docs/services/appid?topic=appid-anonymous#progressive)指派給使用者。當使用者登入時，匿名記號中的資訊隨後會傳送至與使用者相關聯的記號。有效期限是以天為單位設定，且可以是介於 1 與 90 之間的任何值。


當您設定記號有效期限時，它會套用到您已配置的所有提供者，包括社交及企業。
{: tip}
