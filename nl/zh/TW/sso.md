---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-09"

keywords: Authentication, authorization, identity, app security, secure, development, sso, directory, users, registry, multiple apps

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


# 單一登入 (SSO)
{: #cd-sso}

透過 Cloud Directory 的「單一登入 (SSO)」，您可以在多個 Web 應用程式之間提供順暢的鑑別體驗。如果在使用者初次登入時已開啟 SSO，則下次使用者登入時，就不需要重新輸入其認證。相反地，它們會自動登入到受同一個 {{site.data.keyword.appid_short_notm}} 實例保護的任何應用程式。


## 如何運作
{: #cd-sso-how-it-works}

請查看下圖，以瞭解 SSO 的運作狀況。

![SSO 圖](images/sso.png)

1. Cloud Directory 使用者第一次登入您的應用程式。
2. 會要求他們提供使用者名稱或電子郵件及密碼來進行鑑別。
3. 如果認證有效，使用者就會登入您的應用程式。同時，{{site.data.keyword.appid_short_notm}} 會建立一個階段作業，並在使用者的瀏覽器上設定 Cookie。
4. 如果使用者嘗試登入您其他的應用程式之一，則 {{site.data.keyword.appid_short_notm}} 會偵測階段作業 Cookie，並讓使用者自動登入到您的應用程式。{{site.data.keyword.appid_short_notm}} 階段作業 Cookie 是實例特有的 Cookie，並由實例的唯一私密金鑰所簽署。

此時，SSO 已配置為在 Cloud Directory 是唯一啟用身分提供者的情況下運作。如果您的 {{site.data.keyword.appid_short_notm}} 實例配置為使用多身分提供者，在登入流程中啟用 SSO 不會有影響。在每次登入時，系統會提示使用者輸入其 Cloud Directory 認證，或選擇其他提供者之一。
{: note}


## 配置 SSO
{: #cd-sso-configure}

您可以使用 {{site.data.keyword.appid_short_notm}} 儀表板或使用 API 來配置單一登入。
{: shortdesc}


### 使用 GUI
{: #cd-sso-configure-gui}


您可以透過 GUI 來配置 SSO。

1. 導覽至 {{site.data.keyword.appid_short_notm}} 儀表板的 **Cloud Directory > 單一登入**標籤。

2. 在**啟用單一登入**方框中，將 SSO 切換至**已啟用**。

3. 設定在 SSO 階段作業到期之前使用者可以處於非作用中狀態的時間量。一旦到期，使用者就必須重新登入。此時間是以分鐘為單位指定，無活動狀態的最長容許時間為 10,080 分鐘（7 天）。預設時間為 1440 分鐘，相當於 1 天。

4. 將您的重新導向 URI 新增至**登出重新導向 URI** 方框，然後按一下 **+** 符號。請務必只登錄您信任的應用程式。登錄此 URI，即表示您授權 {{site.data.keyword.appid_short_notm}} 將其包含在授權工作流程中。

5. 按一下**儲存**。



### 使用 API
{: #cd-sso-configure-api}

透過使用「SSO 配置管理 API」來定義三項設定，您就可以開啟該特性。

範例呼叫：

```json
{
  "isActive": true,
  "inactivityTimeoutSeconds": 86400,
  "logoutRedirectUris": [
    "http://my-first-app.com/after_logout",
    "http://my-second-app.com/after_logout"
  ]
}
```
{: screen}

<table>
  <tr>
    <th>設定</th>
    <th>定義</th>
  </tr>
  <tr>
    <td><code>isActive</code></td>
    <td>若要啟用 SSO，請將此值設為 <code>true</code>。預設值為 <code>false</code>。</td>
  </tr>
  <tr>
    <td><code>inactivityTimeoutSeconds</code></td>
    <td>在要求使用者重新輸入其認證之前經歷過沒有任何使用者活動的最長時間。這個值是以秒為單位指定，最多可以有 <code>604800 seconds</code>（7 天）。預設值為 <code>86400 seconds</code>（1 天）。</td>
  </tr>
  <tr>
    <td><code>logoutRedirectUris</code></td>
    <td>{{site.data.keyword.appid_short_notm}} 可以在使用者登出之後將使用者重新導向至其中的已容許 URI 逗點區隔清單。</td>
  </tr>
</table>



## 配置登出
{: #cd-sso-log-out}

您可以使用 {{site.data.keyword.appid_short_notm}} 來結束現行瀏覽器的使用者 SSO 階段作業。如果使用者的瀏覽器存取 API 端點，則會終止其階段作業，並提示使用者在該瀏覽器的下一次登入嘗試中輸入其認證 - 針對您的任何應用程式。
{: shortdesc}


當變更、重設或更新密碼流程的其中之一啟動時，就會針對該使用者自動終止所有用戶端的階段作業。
{: note}


### 透過使用 API
{: #cd-sso-log-out-api}

若要登出使用者，請使用您的資訊來完成下列 API 呼叫，以重新導向其瀏覽器。

```
https://<region>.appid.cloud.ibm.com/oauth/v4/<tenant-id>/cloud_directory/sso/logout?redirect_uri=<redirect_uri>&client_id=<clientId>
```
{: codeblock}

<table>
  <tr>
    <th>變數</th>
    <th>值</th>
  </tr>
  <tr>
    <td><code>地區</code></td>
    <td>在其中佈建 {{site.data.keyword.appid_short_notm}} 實例的地區。選項包括：<code>au-syd</code>、<code>eu-de</code>、<code>eu-gb</code>、<code>jp-tok</code> 及 <code>us-south</code>。</td>
  </tr>
  <tr>
    <td><code>tenant-id</code></td> <td>{{site.data.keyword.appid_short_notm}} 實例的唯一 ID。您可以在 {{site.data.keyword.appid_short_notm}} 儀表板的<em>服務認證</em> 標籤中找到這個值。如果您沒有一組服務認證，則可以建立一組服務認證，並從中取得值。</td>
  </tr>
  <tr>
    <td><code>redirect_uri</code></td>
    <td>您透過 {{site.data.keyword.appid_short_notm}} 儀表板在 SSO 配置中指定的 URI。基於安全理由，如果您未指定值，則重新導向就無法進行，而且會顯示錯誤。</td>
  </tr>
</table>

即使已結束 SSO 階段作業，具有其階段作業所儲存之有效存取記號的使用者，在其記號到期之前，可能不需要再次輸入其認證。依預設，記號會在一個小時後到期。
{: note}


### 透過使用 Node.JS 伺服器 SDK
{: #cd-sso-log-out-nodejs}

您也可以使用 {{site.data.keyword.appid_short_notm}} Node.js 伺服器 SDK 為您自動處理重新導向。

範例：

```javascript
app.get('/logoutSSO', (req, res) => {
  res.clearCookie("refreshToken");
  webAppStrategy.logoutSSO(req,res, { "redirect_uri": "https://my-app.com/after_logout" });
  });
```
{: screen}


## 結束使用者的所有階段作業
{: cd-sso-ending-all-sessions}

身為管理者，您可以使用 {{site.data.keyword.appid_short_notm}} 管理 API 來結束任何給定使用者的所有 SSO 階段作業。這些 API 受到 Cloud IAM 記號保護。

API 要求範例：

```
POST https://<region>.appid.cloud.ibm.com/management/v4/{tenant-id}/cloud_directory/Users/{user-id}/sso/logout
Headers:
Authorization: <IAM TOKEN>
```
{: codeblock}

<table>
  <tr>
    <th>變數</th>
    <th>值</th>
  </tr>
  <tr>
    <td><code>地區</code></td>
    <td>在其中佈建 {{site.data.keyword.appid_short_notm}} 實例的地區。選項包括：<code>us-south</code>、<code>eu-gb</code> 及 <code>eu-de</code>。</td>
  </tr>
  <tr>
    <td><code>tenant-id</code></td> <td>{{site.data.keyword.appid_short_notm}} 實例的唯一 ID。您可以在 {{site.data.keyword.appid_short_notm}} 儀表板的<em>服務認證</em> 標籤中找到這個值。如果您沒有一組服務認證，則可以建立一組服務認證，並從中取得值。</td>
  </tr>
  <tr>
    <td><code>user-id</code></td>
    <td>Cloud Directory 使用者的唯一 ID。您可以使用 [Cloud Directory 使用者 API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/) 或檢視使用者的身分記號來取得 ID。</td>
  </tr>
</table>

當您呼叫這個 API 時，所有指定使用者的 SSO 階段作業都會失效。這表示下次使用者嘗試從任何裝置或瀏覽器登入任何應用程式時，都需要重新輸入其認證。

