---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:pre: .pre}


# 存取使用者屬性
{: #user-profile}

使用者屬性是實體中由 {{site.data.keyword.appid_full}} 儲存及維護的資訊區段。設定檔包含使用者的屬性，以及由身分提供者管理或其可以是匿名的身分。您可以使用設定檔，為每一位使用者建立您應用程式的個人化體驗。
{:shortdesc}


{{site.data.keyword.appid_short_notm}} 提供 API，以透過匿名方式或使用 OpenId Connect (OIDC) [身分提供者](/docs/services/appid/identity-providers.html)進行鑑別來登入。使用者設定檔屬性 API 端點是 {{site.data.keyword.appid_short_notm}} 所產生的存取記號在登入及授權處理程序期間所保護的資源。


## 儲存、讀取及刪除使用者屬性
{: #storing-data}

{{site.data.keyword.appid_short_notm}} 提供 <a href="https://appid-profiles.ng.bluemix.net/swagger-ui/index.html#/Attributes" target="_blank">REST API <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>，以對使用者的屬性執行 create、retrieve、update 及 delete 作業。此服務也會提供適用於 <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">Android <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 及 <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">Swift <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 行動用戶端的 SDK。

## 使用 Android SDK 存取使用者屬性
{: #accessing}

取得存取記號時，即可存取使用者保護的屬性端點。您可以使用下列 API 方法來取得存取權。

  ```java
  void setAttribute(@NonNull String name, @NonNull String value, UserAttributeResponseListener listener);
  void setAttribute(@NonNull String name, @NonNull String value, @NonNull AccessToken accessToken, UserAttributeResponseListener listener);

  void getAttribute(@NonNull String name, UserAttributeResponseListener listener);
  void getAttribute(@NonNull String name, @NonNull AccessToken accessToken, UserAttributeResponseListener listener);

  void deleteAttribute(@NonNull String name, UserAttributeResponseListener listener);
  void deleteAttribute(@NonNull String name, @NonNull AccessToken accessToken, UserAttributeResponseListener listener);

  void getAllAttributes(@NonNull UserAttributeResponseListener listener);
  void getAllAttributes(@NonNull AccessToken accessToken, @NonNull UserAttributeResponseListener listener);
  ```
  {: pre}

若未明確地傳遞存取記號，{{site.data.keyword.appid_short_notm}} 會使用最後一個收到的記號。

例如，您可以呼叫下列程式碼來設定新屬性，或置換現有屬性。

  ```java
  appId.getUserAttributeManager().setAttribute(name, value, useThisToken,new UserAttributeResponseListener() {
		@Override
		public void onSuccess(JSONObject attributes) {
			//attributes received in JSON format on successful response
		}

		@Override
		public void onFailure(UserAttributesException e) {
			//Exception occurred
		}
	});
  ```
  {: pre}

### 匿名登入
{: #anonymous notoc}

使用 {{site.data.keyword.appid_short_notm}}，您可以[匿名](/docs/services/appid/user-profile.html#anonymous)登入。

  ```java
  appId.loginAnonymously(getApplicationContext(), new AuthorizationListener() {
		@Override
		public void onAuthorizationFailure(AuthorizationException exception) {
			//Exception occurred
		}

		@Override
		public void onAuthorizationCanceled() {
			//Authentication canceled by the user
		}

		@Override
		public void onAuthorizationSuccess(AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
			//User authenticated
		}
	});
  ```
  {: pre}

### 漸進鑑別
{: #progressive notoc}

若使用者保有匿名存取記號，將它傳遞給 `loginWidget.launch` 方法，即可識別。

  ```java
  void launch (@NonNull final Activity activity, @NonNull final AuthorizationListener authorizationListener, String accessTokenString);
  ```
  {: pre}

匿名登入之後，即使因服務已使用最後一個收到的記號而在未傳遞存取記號的情況下呼叫登入小組件，還是會進行漸進鑑別。如果您要清除儲存的記號，請執行下列指令。

  ```java
  	appIDAuthorizationManager = new AppIDAuthorizationManager(this.appId);
  appIDAuthorizationManager.clearAuthorizationData();
  ```
  {: pre}


## 使用 iOS SDK 存取使用者屬性
{: #accessing}

透過下列 API 方法來傳遞存取記號，以存取使用者屬性。
{: shortdesc}

  ```swift
  func setAttribute(key: String, value: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func setAttribute(key: String, value: String, accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func getAttribute(key: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func getAttribute(key: String, accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func getAttributes(completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func getAttributes(accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func deleteAttribute(key: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func deleteAttribute(key: String, accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  ```
  {: pre}

若未明確地傳遞存取記號，{{site.data.keyword.appid_short_notm}} 會使用最後一個收到的記號。

例如，您可以呼叫下列程式碼來設定新屬性，或置換現有屬性。

  ```swift
  AppID.sharedInstance.userAttributeManager?.setAttribute("key", "value", completionHandler: { (error, result) in
      if error = nil {
          //Attributes recieved as a Dictionary
      } else {
          // An error has occurred
      }
  })
  ```
  {: pre}


### 匿名登入

使用 {{site.data.keyword.appid_short_notm}}，您可以[匿名](/docs/services/appid/user-profile.html#anonymous)登入。

  ```swift
  class delegate : AuthorizationDelegate {

      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, refreshToken: RefreshToken?, response:Response?) {
          //User authenticated
      }

      public func onAuthorizationCanceled() {
          //Authentication canceled by the user
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          //Error occurred
      }
   }

  AppID.sharedInstance.loginAnonymously( authorizationDelegate: delegate())
  ```
  {: pre}

### 漸進鑑別

當您保留匿名存取記號時，使用者可以變成已識別的使用者，方法是將它傳遞給 `loginWidget.launch` 方法。

  ```swift
  func launch(accessTokenString: String? , delegate: AuthorizationDelegate)
  ```
  {: pre}

匿名登入之後，即使因服務已使用最後一個收到的記號而在未傳遞存取記號的情況下呼叫登入小組件，還是會進行漸進鑑別。如果您要清除儲存的記號，請執行下列指令。

  ```swift
  var appIDAuthorizationManager = AppIDAuthorizationManager(appid: AppID.sharedInstance)
  appIDAuthorizationManager.clearAuthorizationData()
  ```
  {: pre}

## 資料分隔及加密
{: #data}

{{site.data.keyword.appid_short_notm}} 儲存及加密使用者設定檔屬性。身為多方承租戶服務，每個承租戶都會有一個指定的加密金鑰，而且只會使用該承租戶的金鑰來加密每一個承租戶中的使用者資料。

{{site.data.keyword.appid_short_notm}} 確定專用資訊在儲存之前已進行加密。
