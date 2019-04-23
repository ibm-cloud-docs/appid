---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-10"

keywords: authentication, authorization, identity, app security, secure, tokens, jwt, development

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


# 驗證記號
{: #token-validation}

記號驗證是現代應用程式開發的重要部分。藉由驗證記號，您可以保護應用程式或 API 不受未獲授權使用者的存取。{{site.data.keyword.appid_full}} 使用存取及身分記號來確定已先鑑別過使用者或應用程式，他們才能獲授與存取權。如果您使用 {{site.data.keyword.appid_short_notm}} 所提供的其中一個 SDK，則會為您取得並驗證您的記號！
{: shortdesc}

如需如何在 {{site.data.keyword.appid_short_notm}} 中使用記號的相關資訊，請參閱[瞭解記號](/docs/services/appid?topic=appid-tokens#tokens)。
{: tip}

記號用來驗證人員的身分。它們會確認使用者可能保留一段指定時間的任何存取權。當使用者登入您的應用程式並對其發出記號時，您的應用程式必須先驗證使用者，他們才能獲得存取權。

</br>

**如果我使用的語言是 {{site.data.keyword.appid_short_notm}} SDK 沒有的語言，該怎麼辨？**

不必擔心！您有三個選項：

* 使用 {{site.data.keyword.appid_short_notm}} API
* 實作自己的驗證邏輯
* 使用任何符合 OIDC 標準的開放程式碼 SDK

根據意見，選項 1 通常是最簡單的執行方法。
{: tip}

</br>
</br>

## 使用 {{site.data.keyword.appid_short_notm}} API
{: #remote-validation}

使用內部檢查，您可以使用 {{site.data.keyword.appid_short_notm}} 來驗證記號。
{: shortdesc}

1. 將 POST 要求傳送至 [/introspect](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Authorization%20Server%20-%20Authorization%20Server%20V4/oauth-server.token) API 端點，以驗證您的記號。要求必須提供記號以及包含用戶端 ID 和密碼的基本授權標頭。

  要求範例：

    ```
    POST /oauth/v4/{tenant_id}/introspect HTTP/1.1
    Host: us-south.appid.cloud.ibm.com
    Content-Type: application/x-www-form-urlencoded
    Authorization: Basic jdFlUaGlZUzAwTW0Tjk15TmpFMw==
    Cache-Control: no-cache

    token=XXXXX.YYYYY.ZZZZZ
    ```
    {: screen}

2. 伺服器會檢查記號的期限和簽章，並傳回 JSON 物件，以分辨記號是作用中還是非作用中。

  回應範例：

    ```
    {
      "active": true
    }
    ```
    {: screen}


## 手動驗證記號
{: #local-validation}

您可以藉由剖析記號、驗證記號簽章，以及驗證儲存在記號中的要求，以在本端驗證記號。
{: shortdesc}


1. 剖析記號。[JSON Web 記號 (JWT)](https://tools.ietf.org/html/rfc7519) 是安全傳遞資訊的標準方式。它包含三個主要部分：「標頭」、「有效負載」及「簽章」。它們都是以 base64URL 編碼，並使用點 (.) 區隔。您可以使用任何可用來剖析記號的 base64URL 解碼器。或者，您也可以使用任何[列出的檔案庫](https://jwt.io/#libraries-io)來剖析記號。

  已編碼記號範例：

    ```
    eyJhbGciOiJSUzI1NiIsInR5cCI6IkpPU0UiLCJraWQiOiJhMmszIn0
    .eyJpc3MiOiJhcHBpZC1vYXV0aCIsImF1ZCI6ImFiYzEyMyIsImV4cCI6MTU2NDU2Nn0
    .IycnAGUmMHzpTWbe-qaRsx0B4Zi-SVav710Fb_8CTCQvLrHX9d42WuCZ5bW
    d-ikgEsf6waQxeBfhfwYxwHN87LZupApagVMZtylVAnXhG1pHu_32wbZsPvg6QjzNO
    j6ys2Lfl3qfb5Qrp9u4IsZltKPEN8HdfeOcKXxpw6UqP-8
    ```
    {: screen}

  已解碼標頭範例：

    ```
    {
      "alg": "RS256",
      "typ": "JOSE",
      "kid": "a2k3"
    }
    ```
    {: screen}

  已解碼的有效負載：

    ```
    {
      "iss": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61",
      "aud": "abc123",
      "exp": 1564566
    }
    ```
    {: screen}

2. 呼叫 [/publickeys 端點](https://us-south.appid.cloud.ibm.com/swagger-ui/#!/Authorization_Server_V4/publicKeys)，以擷取公開金鑰。傳回的公開金鑰會格式化為 [JSON Web 金鑰 (JWK)](https://tools.ietf.org/html/rfc7517)。

  要求範例：

    ```
    GET /oauth/v4/{tenant_id}/publickeys HTTP/1.1
    Host: us-south.appid.cloud.ibm.com
    Cache-Control: no-cache
    ```
    {: screen}

3. 將金鑰儲存至應用程式快取，以供未來使用。儲存金鑰可加速此處理程序，並防止網路延遲（如果已進行另一個呼叫）。

4. 匯入公開金鑰參數。

  回應範例：

    ```
    {
      "keys": [
        {
          "kty": "RSA",
          "use": "sig",
          "n": "AsdaE",
          "e": "SDAasw",
          "kid": "ad123dCAz"
        }
      ]
    }
    ```
    {: screen}

  <table>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="相關資訊圖示"/> 公開金鑰參數</th>
    </thead>
    <tbody>
      <tr>
        <td><code>kty</code></td>
        <td>定義使用的演算法。</td>
      </tr>
      <tr>
        <td><code>use</code></td>
        <td>定義金鑰的用途。</td>
      </tr>
      <tr>
        <td><code>kid</code></td>
        <td>定義金鑰的唯一 ID。</td>
      </tr>
      <tr>
        <td>其他</td>
        <td>可能還有您演算法特有、而且必須同時匯入的其他剩餘參數。</td>
      </tr>
    </tbody>
  </table>

5. 驗證記號的簽章。記號標頭包含用來簽署記號的演算法，以及相符公開金鑰的「金鑰 ID」或 `kid` 要求。因為公開金鑰不會經常變更，所以您可以在應用程式中快取公開金鑰，並偶爾重新予以整理。如果您的快取金鑰遺漏 `kid` 宣告，則您可以在本端驗證記號。

  1. 讓您的應用程式驗證送入記號標頭的內容符合公開金鑰的參數。
  2. 特別檢查已使用相同的演算法，而且公開金鑰快取包含具有相關「金鑰 ID」的金鑰。
  3. 確定雜湊值與公開金鑰的 PEM 形式簽章相同。您可以藉由結合及雜湊處理記號有效負載的標頭，來取得雜湊值。因為此處理程序可能十分複雜而無法手動實作，所以使用其中一個[列出的檔案庫](https://jwt.io/)來驗證簽章可能很有用。

6. 驗證儲存在記號中的要求。若要驗證未來的檢查，您可以使用[此清單](http://openid.net/specs/openid-connect-core-1_0.html#IDTokenValidation)。
  <table>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="相關資訊圖示"/> 必須驗證的要求</th>
    </thead>
    <tbody>
      <tr>
        <td><code>iss</code></td>
        <td>發證者必須與 {{site.data.keyword.appid_short_notm}} OAuth 伺服器相同。</td>
      </tr>
      <tr>
        <td><code>exp</code></td>
        <td>現行時間必須小於到期時間。</td>
      </tr>
      <tr>
        <td><code>aud</code></td>
        <td>適用對象必須包含應用程式的用戶端 ID。</td>
      </tr>
      <tr>
        <td><code>tenant</code></td>
        <td>承租戶必須包含應用程式的承租戶 ID。</td>
      </tr>
      <tr>
        <td><code>scope</code></td>
        <td>授與使用者的許可權範圍。這是存取記號特有的。</td>
      </tr>
    </tbody>
  </table>
