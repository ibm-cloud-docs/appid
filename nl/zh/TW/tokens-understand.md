---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-05"

keywords: authentication, authorization, identity, app security, secure, access, tokens

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



# 瞭解記號
{: #tokens}

當順利鑑別使用者時，應用程式會從 {{site.data.keyword.appid_short_notm}} 收到記號。服務會使用三種主要類型的記號來完成鑑別處理程序。
{: shortdesc}


## 存取記號
{: #access}

存取記號代表授權，並啟用與[後端資源](/docs/services/appid?topic=appid-backend)的通訊，這些資源會受到 {{site.data.keyword.appid_short}} 所設定的授權過濾器保護。此記號符合「JavaScript 物件簽署及加密 (JOSE)」規格。記號會格式化為 <a href="https://jwt.io/introduction/" target="blank">JSON Web 記號 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>，其是以使用 RS256 演算法的「JSON Web 金鑰」進行簽署。

記號範例：
  ```
Header: {

    "alg": "RS256",
    "typ": "JWT",
    "kid": "appId-39a37f57-a227-4bfe-a044-93b6e6050a61-2018-08-02T11:57:43.401",
    "ver": 4
  }
  Payload:
  {
    "iss": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61",
    "exp": 1551903163,
    "aud": [
      "968c2306-9aef-4109-bc06-4f5ed6axi24a"
    ],
    "sub": "2b96cc04-eca5-4122-a8de-6e07d14c13a5",
    "email_verified": true,
    "amr": [
      "cloud_directory"
    ],
    "iat": 1551899553,
    "tenant": "39a37f57-a227-4bfe-a044-93b6e6050a61",
    "scope": "openid appid_default appid_readprofile appid_readuserattr appid_writeuserattr appid_authenticated"
  }
  ```
  {: screen}

## 何謂身分記號？
{: #identity}

身分記號代表鑑別，並包含使用者的相關資訊。它可以將使用者名稱、電子郵件、性別及位置的相關資訊提供給您。記號也可以傳回使用者影像的 URL。記號會格式化為 <a href="https://jwt.io/introduction/" target="blank">JSON Web 記號 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>，其是以使用 RS256 演算法的「JSON Web 金鑰」進行簽署。

記號範例：
  ```
Header: {

    "alg": "RS256",
    "typ": "JWT",
    "kid": "appId-39a37f57-a227-4bfe-a044-93b6e6050a61-2018-08-02T11:57:43.401",
    "ver": 4
  }
  Payload:
  {
    "iss": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61",
    "aud": [
      "968c2306-9aef-4109-bc06-4f5ed6axi24a"
    ],
    "exp": 1551903163,
    "tenant": "39a37f57-a227-4bfe-a044-93b6e6050a61",
    "iat": 1551899553,
    "email": "appid155@mailinator.com",
    "name": "appid155@mailinator.com",
    "sub": "2b96cc04-eca5-4122-a8de-6e07d14c13a5",
    "email_verified": true,
    "identities": [
      {
        "provider": "cloud_directory",
        "id": "118c0278-3526-4954-876b-cf70eb88efa2"
      }
    ],
    "amr": [
      "cloud_directory"
    ]
  }
  ```
  {: screen}


身分記號僅包含局部使用者資訊。若要查看身分提供者所提供的所有資訊，您可以使用 [/userinfo 端點](/docs/services/appid?topic=appid-profiles#profile-predefined-api)。

## 何謂重新整理記號？
{: #refresh}

{{site.data.keyword.appid_short}} 支援在沒有重新鑑別的情況下獲得新存取和身分記號的能力，如 <a href="https://openid.net/specs/openid-connect-core-1_0.html#RefreshTokens" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 中所定義。
      重新整理記號可以用來更新存取記號，因此使用者不需要採取任何動作即可登入，例如提供認證。與存取記號類似，重新整理記號包含容許 {{site.data.keyword.appid_short_notm}} 判定您是否已獲授權的資料。不過，這些記號是不透明的。

重新整理記號會配置為具有比一般存取記號還要長的有效期限，因此當存取記號到期時，重新整理記號仍然有效，且可用來更新存取記號。{{site.data.keyword.appid_short_notm}} 的重新整理記號可以配置為持續 1 到 90 天。若要充分運用重新整理記號，請持續保存這些記號，直到其完整有效期限結束，或直到它們已更新。使用者無法只利用重新整理記號來直接存取資源，這使得它們比存取記號更能安全地持續保存。最佳作法是，重新整理記號應該由接收它們的用戶端安全地儲存，且只傳送至發出它們的授權伺服器。

為了方便新增，{{site.data.keyword.appid_short_notm}} 也會在更新存取記號時，更新其重新整理記號及其到期日，讓使用者可以保持登入狀態，只要他們在現行重新整理記號到期之前的某個時間點處於作用中狀態。另一方面，如果您想要使用重新整理記號，但強制使用者定期登入，則您的應用程式只能使用在使用者輸入其認證登入時所傳回的重新整理記號。不過，我們建議一律使用從 {{site.data.keyword.appid_short_notm}} 接收的最新重新整理記號，如 <a href="https://tools.ietf.org/html/rfc6749#page-47" target="_blank">OAuth 2.0 規格 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 所述。


雖然這些記號可以簡化登入處理程序，但您的應用程式不應該依賴它們，因為可以隨時撤銷它們，例如您認為重新整理記號已受損時。如果您需要撤銷重新整理記號，則有兩種撤銷重新整理記號的方法。如果您有重新整理記號，則可以根據 <a href="https://tools.ietf.org/html/rfc7009#section-2" target="_blank">RFC7009 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 來撤銷它。或者，如果您具有使用者 ID，則可以使用<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/" target="_blank">管理 API <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 來撤銷重新整理記號。如需存取管理 API 的相關資訊，請參閱[管理服務存取](/docs/services/appid?topic=appid-service-access-management#service-access-management)。

如需使用重新整理記號，以及如何使用它們來實作 remember me 功能的範例，請參閱[入門範例](/docs/services/appid?topic=appid-getting-started#getting-started)。


## 記號來自何處？
{: #where}

記號是透過 {{site.data.keyword.appid_short_notm}}OAuth Server 發出，且會格式化為 [JSON Web 記號 (JWT)](https://jwt.io/introduction/)。這些記號已使用 [JSON Web 金鑰 (JWK)](https://tools.ietf.org/html/rfc7517) 搭配 RS256 演算法來進行簽署。

## 記號包含的資訊會發生什麼情況？
{: #contains}

存取記號包含一組標準 JWT 要求，以及一組 {{site.data.keyword.appid_short_notm}}特定要求（如承租戶 ID）。身分記號包含使用者特定資訊。記號中的資訊儲存為要求，作為[使用者設定檔](/docs/services/appid?topic=appid-profiles)的一部分。

## 如何接收記號？
{: #received}

在順利鑑別之後，您的應用程式會收到記號。您的應用程式可以使用記號，來擷取使用者授權和鑑別的相關資訊。存取記號可以用來藉由將要求傳送至資源來取得受保護資源的存取權。在要求中，存取記號說明於 [Bearer 鑑別方法](https://tools.ietf.org/html/rfc6750#page-5)中。若要擷取記號，您的應用程式必須剖析標頭。

要求範例：

  ```
  GET /resource HTTP/1.1
  Host: server.example.com
  Authorization: Bearer  mF_9.B5f-4.1JqM mF_9.B5f-4.1JqM
  ```
  {: screen}

## 如何設定記號？
{: #set}

記號配置可以透過 {{site.data.keyword.appid_short_notm}} 儀表板來啟用及停用。如需配置選項的相關資訊，請參閱[管理記號](/docs/services/appid?topic=appid-managing-idp#managing-idp)。
