---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-14"

keywords: authentication, authorization, identity, app security, secure, attributes, user information, storing, accessing

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
{:java: .ph data-hd-programlang='java'}
{:javascript: .ph data-hd-programlang='javascript'}
{:swift: .ph data-hd-programlang='swift'}
{:curl: .ph data-hd-programlang='curl'}

# 自訂使用者屬性
{: #custom-attributes}

使用 {{site.data.keyword.appid_full}}，您可以儲存、存取及更新自訂屬性。
{: shortdesc}


## 設定屬性
{: #setting-custom-attributes}

您可以設定已知為使用者設定檔屬性的角色及範圍。您也可以置換可能已從外部身分提供者取回的現有屬性。
{: shortdesc}


屬性是有關您使用者的資訊片段。儲存它們，您可以對使用者建立容許您個人化其體驗的設定檔。新增至其設定檔的屬性越多，他們的應用程式體驗就更加個人化。請參閱此部落格，以瞭解建立使用者設定檔如何做出差異：<a href="https://www.ibm.com/blogs/bluemix/2017/03/introducing-ibm-bluemix-app-id-authentication-profiles-service-app-developers/" target="blank">{{site.data.keyword.appid_short_notm}} 簡介 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。


您可以為每位使用者儲存 100 KB 的資訊。
{: note}


**若要設定屬性：**

您應用程式的所有送入要求都具有「授權」標頭，且含有 `access_token`。您可以使用 `access_token`，透過其中一個提供的 SDK 或使用[屬性 API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Attributes)，對自訂屬性端點提出要求。


iOS Swift：
{: ph data-hd-programlang='swift'}

  ```
	AppID.sharedInstance.userProfileManager?.setAttribute("key", "value") { (error, result) in
		guard let result = result, error == nil else {
	  		return // an error has occurred
		}
		// attributes recieved as a Dictionary
	})
  ```
  {: codeblock}
  {: ph data-hd-programlang='swift'}

  ```
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
  {: codeblock}
  {: ph data-hd-programlang='java'}

  ```
	const userProfileManager = require("ibmcloud-appid").UserProfileManager;
	userProfileManager.init();

	var accessToken = req.session[WebAppStrategy.AUTH_CONTEXT].accessToken;

	userProfileManager.setAttribute(accessToken, name, value).then(function (attributes) {
		// attributes returned as dictionary
	});
  ```
  {: codeblock}
  {: ph data-hd-programlang='javascript'}

伺服器 Swift：
{: ph data-hd-programlang='swift'}

  ```
let userProfileManager = UserProfileManager(options: options)
	let accesstoken = "access token"

	userProfileManager.setAttribute(accessToken: accessToken, attributeName: "name", attributeValue : "abc") { (error, response) in
		guard let response = response, error == error else {
			return // an error has occurred
		}
		// attributes received as a Dictionary
  }
  ```
  {: codeblock}
  {: ph data-hd-programlang='swift'}

</br>

## 存取自訂屬性
{: #accessing-custom-attributes}

取決於您的配置，當使用者與您的應用程式互動時，屬性會加密並儲存為使用者設定檔的一部分。互動可以是使用者登入，或在您的應用程式中設定喜好設定。若要存取屬性，您可以透過 API 方法來傳遞存取記號。如果未明確傳遞存取記號，{{site.data.keyword.appid_short_notm}} 會使用前次收到的記號。
{: shortdesc}

iOS Swift：
{: ph data-hd-programlang='swift'}

  ```
  func setAttribute(key: String, value: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func setAttribute(key: String, value: String, accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func getAttribute(key: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func getAttribute(key: String, accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func getAttributes(completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func getAttributes(accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func deleteAttribute(key: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func deleteAttribute(key: String, accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  ```
  {: codeblock}
  {: ph data-hd-programlang='swift'}

  ```
  void setAttribute(@NonNull String name, @NonNull String value, UserAttributeResponseListener listener);
  void setAttribute(@NonNull String name, @NonNull String value, @NonNull AccessToken accessToken, UserAttributeResponseListener listener);

  void getAttribute(@NonNull String name, UserAttributeResponseListener listener);
  void getAttribute(@NonNull String name, @NonNull AccessToken accessToken, UserAttributeResponseListener listener);

  void deleteAttribute(@NonNull String name, UserAttributeResponseListener listener);
  void deleteAttribute(@NonNull String name, @NonNull AccessToken accessToken, UserAttributeResponseListener listener);

  void getAllAttributes(@NonNull UserAttributeResponseListener listener);
  void getAllAttributes(@NonNull AccessToken accessToken, @NonNull UserAttributeResponseListener listener);
  ```
  {: codeblock}
  {: ph data-hd-programlang='java'}

  ```
function getAllAttributes(accessTokenString) {}
	function getAttribute(accessTokenString, key) {}
	function setAttribute(accessTokenString, key, value) {}
	function deleteAttribute(accessTokenString, name) {}
  ```
  {: codeblock}
  {: ph data-hd-programlang='javascript'}

伺服器端 Swift：
{: ph data-hd-programlang='swift'}

  ```
  func getAllAttributes(accessToken: String, completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  func getAttribute(accessToken: String, attributeName: String, completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  func setAttribute(accessToken: String, attributeName: String, attributeValue : "abc", completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  func deleteAllAttributes(accessToken: String, completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  ```
  {: codeblock}
  {: ph data-hd-programlang='swift'}

</br>

## 安全考量
{: #security-custom-attributes}

在開始使用自訂屬性之前，請確定您已瞭解安全考量。

依預設，自訂屬性是可修改的，而且可以使用來自用戶端應用程式的 {{site.data.keyword.appid_short_notm}} 存取記號予以更新。這表示，在沒有採取適當預防措施的情況下，若使用者或應用程式對存取記號具有存取權，則在第一位使用者登入之後，他們就可以立即更新自訂屬性。這可能會導致非預期的結果。例如，使用者可以將其角色從使用者變更為管理者，因而可能會向惡意使用者公開管理專用權。

若要防止使用者變更您提供給他們的屬性，請在 {{site.data.keyword.appid_short_notm}} 儀表板的**設定檔**標籤上，將**變更來自應用程式的自訂屬性**設為**關閉**。依預設，它會設為**開啟**。
{: tip}

</br>

## 後續步驟
{: #next-custom-attributes}

如需使用特定語言 SDK 的相關資訊，請參閱下列 GitHub 儲存庫：

* <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">Android SDK <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>
* <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">iOS Swift SDK <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>
* <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">Node.js SDK <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>
* <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">伺服器 Swift SDK <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>


找不到撰寫應用程式所用之語言的 SDK 嗎？沒有問題！您可以使用 API 來整合服務。
{{site.data.keyword.appid_short_notm}} 提供 <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/" target="_blank">REST API <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>，可容許使用支援的[身分提供者](/docs/services/appid?topic=appid-managing-idp)登入（匿名或藉由鑑別）。以 Python 及 Go 之類的語言實作 API 時如需協助，<a href="https://www.ibm.com/blogs/bluemix/tag/app-id/" target="_blank">請參閱我們的部落格 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。
{: tip}
