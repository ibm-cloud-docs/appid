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

# 访问定制用户属性
{: #custom}

通过 {{site.data.keyword.appid_full}}，您可以保存和访问定制属性。
{: shortdesc}

**为什么要保存有关用户的其他属性？**

属性是有关用户的信息片段。通过保存这些属性，可以对用户创建概要文件，以允许您对其体验进行个性化。添加到用户概要文件的属性越多，其应用程序的个性化程度越高。请查看此博客以了解如何通过创建用户概要文件进行个性化：<a href="https://www.ibm.com/blogs/bluemix/2017/03/introducing-ibm-bluemix-app-id-authentication-profiles-service-app-developers/" target="_blank">Introducing {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>。

</br>

**如何保存属性？**

根据您的配置，当用户与应用程序交互时，属性会被加密并保存为用户概要文件的一部分。交互可能是用户登录，也可能是在应用程序中设置首选项。

</br>

**对于每个用户可以存储的信息量是否有限制？**

您可以为每个用户存储 100 KB 信息。

</br>

**有任何安全注意事项应该考虑吗？**

缺省情况下，定制属性是可修改的，并且可以通过客户机应用程序使用 {{site.data.keyword.appid_short_notm}} 访问令牌来更新。这意味着，只要用户或应用程序有权对访问令牌进行访问，那么在第一个用户登录后，该用户或应用程序就可以立即更新定制属性，而不必执行适当的预防措施。这可能会导致意外的后果。例如，用户可以将其角色从用户更改为管理员，而这可能会向恶意用户公开管理特权。

为了防止用户更改您所提供的属性，请在 {{site.data.keyword.appid_short_notm}} 仪表板的**概要文件**选项卡上，将**更改应用程序中的定制属性**设置为**关闭**。缺省情况下，此值设置为**开启**。
{: tip}

</br>


## 使用 iOS SDK 访问
{: #ios}

 可以通过以下 API 方法传递访问令牌来访问定制属性。


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

未显式传递访问令牌时，{{site.data.keyword.appid_short_notm}} 会使用最后一次收到的令牌。

例如，可以调用以下代码来设置新属性，或者覆盖现有属性。

  ```swift
	AppID.sharedInstance.userProfileManager?.setAttribute("key", "value") { (error, result) in
		guard let result = result, error == nil else {
	  		return // an error has occurred
		}
		// attributes recieved as a Dictionary
	})
  ```
  {: pre}

有关在 iOS Swift 中工作的更多信息，请参阅 <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">SDK <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>。
{: tip}

</br>


## 使用 Android SDK 访问
{: #android}

可以通过以下 API 方法传递访问令牌来访问定制属性。


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

未显式传递访问令牌时，{{site.data.keyword.appid_short_notm}} 会使用最后一次收到的令牌。

例如，可以调用以下代码来设置新属性，或者覆盖现有属性。

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

有关在 Android 中工作的更多信息，请参阅 <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">SDK <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>。
{: tip}

</br>

## 使用 Node.js Server SDK 访问
{: #node}

可以通过以下 API 方法传递访问令牌来访问定制属性。


  ```javascript
	function getAllAttributes(accessTokenString) {}
	function getAttribute(accessTokenString, key) {}
	function setAttribute(accessTokenString, key, value) {}
	function deleteAttribute(accessTokenString, name) {}
  ```
  {: pre}

  示例用法：

  ```javascript

	const userProfileManager = require("ibmcloud-appid").UserProfileManager;
	userProfileManager.init();

	var accessToken = req.session[WebAppStrategy.AUTH_CONTEXT].accessToken;

	userProfileManager.setAttribute(accessToken, name, value).then(function (attributes) {
		// attributes returned as dictionary
	});
  ```
  {: pre}

有关在 Node.js Server Sdk 中工作的更多信息，请参阅 <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">SDK <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>。
{: tip}

</br>

## 使用 Swift Server SDK 访问
{: #swift}

可以通过以下 API 方法传递访问令牌来访问定制属性。


  ```swift
  func getAllAttributes(accessToken: String, completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  func getAttribute(accessToken: String, attributeName: String, completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  func setAttribute(accessToken: String, attributeName: String, attributeValue : "abc", completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  func deleteAllAttributes(accessToken: String, completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  ```
  {: pre}

  示例用法：

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

有关在 Swift Server Sdk 中工作的更多信息，请参阅 <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">SDK <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>。
{: tip}


## 使用 API 访问
{: #api}

找不到与编写应用程序的语言相应的 SDK？没问题！您可以使用 API 来集成服务。
{: shortdesc}

{{site.data.keyword.appid_short_notm}} 提供 <a href="https://appid-profiles.ng.bluemix.net/swagger-ui/index.html#/Attributes" target="_blank">REST API <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>，允许使用受支持的[身份提供者](/docs/services/appid/manageidp.html)以匿名方式或认证方式登录。
