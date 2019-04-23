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

# 定制用户属性
{: #custom-attributes}

通过 {{site.data.keyword.appid_full}}，您可以保存、访问和更新定制属性。
{: shortdesc}


## 设置属性
{: #setting-custom-attributes}

可以设置角色和作用域，这些对象称为用户概要文件的属性。您还可以覆盖可能已从外部身份提供者那里拉取的现有属性。
{: shortdesc}


属性是有关用户的信息片段。通过保存这些属性，可以对用户创建概要文件，以允许您对其体验进行个性化。添加到用户概要文件的属性越多，其应用程序体验的个性化程度越高。请查看此博客以了解如何通过创建用户概要文件进行个性化：<a href="https://www.ibm.com/blogs/bluemix/2017/03/introducing-ibm-bluemix-app-id-authentication-profiles-service-app-developers/" target="blank">Introducing {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>。


您可以为每个用户存储 100 KB 信息。
{: note}


**设置属性：**

对应用程序的所有入局请求都具有 Authorization 头，并包含 `access_token`。可以使用 `access_token` 通过其中一个提供的 SDK 或使用[属性 API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Attributes) 向定制属性端点发出请求。


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

服务器 Swift：
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

## 访问定制属性
{: #accessing-custom-attributes}

根据您的配置，当用户与应用程序交互时，属性会被加密并保存为用户概要文件的一部分。交互可能是用户登录，也可能是在应用程序中设置首选项。要访问这些属性，可以通过 API 方法来传递访问令牌。未显式传递访问令牌时，{{site.data.keyword.appid_short_notm}} 会使用最后一次收到的令牌。
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

服务器端 Swift：
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

## 安全注意事项
{: #security-custom-attributes}

开始使用定制属性之前，请确保了解安全注意事项。

缺省情况下，定制属性是可修改的，并且可以通过客户机应用程序使用 {{site.data.keyword.appid_short_notm}} 访问令牌来更新。这意味着，只要用户或应用程序有权对访问令牌进行访问，那么在第一个用户登录后，该用户或应用程序就可以立即更新定制属性，而不必执行适当的预防措施。这可能会导致意外的后果。例如，用户可以将其角色从用户更改为管理员，而这可能会向恶意用户公开管理特权。

为了防止用户更改您所提供的属性，请在 {{site.data.keyword.appid_short_notm}} 仪表板的**概要文件**选项卡上，将**更改应用程序中的定制属性**设置为**关闭**。缺省情况下，此值设置为**开启**。
{: tip}

</br>

## 后续步骤
{: #next-custom-attributes}

有关使用特定语言 SDK 的更多信息，请参阅以下 GitHub 存储库：

* <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">Android SDK <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>
* <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">iOS Swift SDK <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>
* <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">Node.js SDK <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>
* <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">服务器 Swift SDK <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>


找不到与编写应用程序的语言相应的 SDK？没问题！您可以使用 API 来集成服务。
{{site.data.keyword.appid_short_notm}} 提供 <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/" target="_blank">REST API <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>，允许使用受支持的[身份提供者](/docs/services/appid?topic=appid-managing-idp)以匿名方式或认证方式登录。要获取使用各种语言（如 Python 和 Go）实现 API 的帮助，请<a href="https://www.ibm.com/blogs/bluemix/tag/app-id/" target="_blank">查看我们的博客 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>。
{: tip}
