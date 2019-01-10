---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:pre: .pre}
{:tip: .tip}
{:screen: .screen}

# 存取自訂使用者屬性
{: #custom}

使用 {{site.data.keyword.appid_full}}，您可以儲存及存取自訂屬性。
{: shortdesc}

**為何我想要儲存有關使用者的其他屬性？**

屬性是有關您使用者的資訊片段。藉由儲存它們，您可以對使用者建立可讓您個人化其體驗的設定檔。新增至其人員資訊的屬性越多，他們的應用程式就越個人化。請參閱此部落格，以瞭解建立使用者設定檔如何做出差異：<a href="https://www.ibm.com/blogs/bluemix/2017/03/introducing-ibm-bluemix-app-id-authentication-profiles-service-app-developers/" target="_blank">Introducing {{site.data.keyword.appid_short_notm}}<img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示">。</a>

</br>

**如何儲存屬性？**

根據您的配置，當使用者與您的應用程式互動時，屬性會加密並儲存為使用者設定檔的一部分。互動可以是使用者登入，或在您的應用程式中設定喜好設定。

</br>

**可為每一個使用者儲存的資訊數量有限制嗎？**

您可為每一個使用者儲存 100KB 的資訊。

</br>

**有任何我應該做出的安全考量嗎？**

依預設，自訂屬性是可修改的，而且可以使用來自用戶端應用程式的 {{site.data.keyword.appid_short_notm}} 存取記號來更新。這表示，在沒有採取適當預防措施的情況下，若使用者或應用程式對存取記號具有存取權，則在第一個使用者登入之後，他們就可以立即更新自訂屬性。這可能會導致非預期的結果。例如，使用者可以將其角色從使用者變更為管理者，因而可能向惡意使用者公開管理專用權。

若要防止使用者變更您提供給他們的屬性，請在 {{site.data.keyword.appid_short_notm}} 儀表板的**設定檔**標籤上，將**變更來自應用程式的自訂屬性**設為**關閉**。依預設，它會設為**開啟**。
{: tip}

</br>


## 使用 iOS SDK 存取
{: #ios}

 您可以透過下列 API 方法來傳遞存取記號，以存取自訂屬性。

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
	AppID.sharedInstance.userProfileManager?.setAttribute("key", "value") { (error, result) in
		guard let result = result, error == nil else {
	  		return // an error has occurred
		}
		// attributes recieved as a Dictionary
	})
  ```
  {: pre}

如需在 iOS Swift 中工作的相關資訊，請參閱 <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">SDK <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。
{: tip}

</br>


## 使用 Android SDK 存取
{: #android}

您可以透過下列 API 方法來傳遞存取記號，以存取自訂屬性。

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
appId.getUserProfileManager().setAttribute(name, value, useThisToken, new UserProfileResponseListener() {
	@Override
		public void onSuccess(JSONObject attributes) {
			//attributes received in JSON format on successful response
		}

		@Override
		public void onFailure(UserAttributesException e) {
			// exception occurred
	}
});
```
{: pre}

如需在 Android 中工作的相關資訊，請參閱 <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">SDK <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。
{: tip}

</br>

## 使用 Node.js 伺服器 SDK 存取
{: #node}

您可以透過下列 API 方法來傳遞存取記號，以存取自訂屬性。

  ```javascript
	function getAllAttributes(accessTokenString) {}
	function getAttribute(accessTokenString, key) {}
	function setAttribute(accessTokenString, key, value) {}
	function deleteAttribute(accessTokenString, name) {}
  ```
  {: pre}

  用法範例：

  ```javascript

	const userProfileManager = require("ibmcloud-appid").UserProfileManager;
	userProfileManager.init();

	var accessToken = req.session[WebAppStrategy.AUTH_CONTEXT].accessToken;

	userProfileManager.setAttribute(accessToken, name, value).then(function (attributes) {
		// attributes returned as dictionary
	});
  ```
  {: pre}

如需在「Node.js 伺服器 SDK」中工作的相關資訊，請參閱 <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">SDK <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。
{: tip}

</br>

## 使用 Swift 伺服器 SDK 存取
{: #swift}

您可以透過下列 API 方法來傳遞存取記號，以存取自訂屬性。

  ```swift
  func getAllAttributes(accessToken: String, completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  func getAttribute(accessToken: String, attributeName: String, completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  func setAttribute(accessToken: String, attributeName: String, attributeValue : "abc", completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  func deleteAllAttributes(accessToken: String, completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  ```
  {: pre}

  用法範例：

  ```swift

	let userProfileManager = UserProfileManager(options: options)
	let accesstoken = "access token"

	userProfileManager.setAttribute(accessToken: accessToken, attributeName: "name", attributeValue : "abc") { (error, response) in
		guard let response = response, error == error else {
			return // an error has occurred
		}
		// attributes recieved as a Dictionary
	}
  ```

  {: pre}

如需在「Swift 伺服器 SDK」中工作的相關資訊，請參閱 <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">SDK <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。
{: tip}


## 使用 API 存取
{: #api}

找不到撰寫應用程式所用之語言的 SDK 嗎？沒有問題！您可以使用 API 來整合服務。
{: shortdesc}

{{site.data.keyword.appid_short_notm}} 提供 <a href="https://appid-profiles.ng.bluemix.net/swagger-ui/index.html#/Attributes" target="_blank">REST API <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>，可容許使用支援的[身分提供者](/docs/services/appid/manageidp.html)登入（匿名或藉由鑑別）。
