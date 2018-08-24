---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-03"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:pre: .pre}
{:tip: .tip}
{:screen: .screen}

# カスタム・ユーザー属性へのアクセス
{: #custom}

アクセス・トークンを取得すれば、ユーザーの保護された属性のエンドポイントにアクセスできます。
{: shortdesc}

{{site.data.keyword.appid_short_notm}} には、サポートされる [ID プロバイダー](/docs/services/appid/identity-providers.html)を使用した、匿名または認証によるログインを可能にする <a href="https://appid-profiles.ng.bluemix.net/swagger-ui/index.html#/Attributes" target="_blank">REST API <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> が用意されています。API エンドポイントは、ログインと許可のプロセス中に {{site.data.keyword.appid_short_notm}} が生成するアクセス・トークンによって保護されるリソースです。

</br>

## iOS SDK を使用したアクセス
{: #ios}

 以下の API メソッドを介してアクセス・トークンを渡すことによって、カスタム属性にアクセスします。

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

アクセス・トークンを明示的に渡さないと、{{site.data.keyword.appid_short_notm}} は最後に受け取ったトークンを使用します。

例えば、以下のコードを呼び出して、新しい属性を設定したり既存の属性をオーバーライドしたりできます。

  ```swift
	AppID.sharedInstance.userProfileManager?.setAttribute("key", "value") { (error, result) in
		guard let result = result, error == nil else {
	  		return // an error has occurred
		}
		// attributes recieved as a Dictionary
	})
  ```
  {: pre}

  iOS Swift での作業について詳しくは、<a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">SDK <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を参照してください。
  {: tip}

</br>


## Android SDK を使用したアクセス
{: #android}

以下の API メソッドを介してアクセス・トークンを渡すことによって、カスタム属性にアクセスします。

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

アクセス・トークンを明示的に渡さないと、{{site.data.keyword.appid_short_notm}} は最後に受け取ったトークンを使用します。

例えば、以下のコードを呼び出して、新しい属性を設定したり既存の属性をオーバーライドしたりできます。

```java
appId.getUserProfileManager().setAttribute(name, value, useThisToken, new UserProfileResponseListener() {
	@Override
		public void onSuccess(JSONObject attributes) {
		//正常な応答から受け取った JSON 形式の属性
		}

	@Override
		public void onFailure(UserAttributesException e) {
		// exception occurred
	}
});
```
{: pre}

Android での作業について詳しくは、<a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">SDK <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を参照してください。
{: tip}

</br>

## Swift Server SDK を使用したアクセス
{: #swift}

以下の API メソッドを介してアクセス・トークンを渡すことによって、カスタム属性にアクセスします。

  ```swift
  func getAllAttributes(accessToken: String, completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  func getAttribute(accessToken: String, attributeName: String, completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  func setAttribute(accessToken: String, attributeName: String, attributeValue : "abc", completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  func deleteAllAttributes(accessToken: String, completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  ```
  {: pre}

  使用例:

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

  Swift Server Sdk での作業について詳しくは、<a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">SDK <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を参照してください。
  {: tip}

</br>

## Node.js Server SDK を使用したアクセス
{: #node}

以下の API メソッドを介してアクセス・トークンを渡すことによって、カスタム属性にアクセスします。

  ```javascript
	function getAllAttributes(accessTokenString) {}
	function getAttribute(accessTokenString, key) {}
	function setAttribute(accessTokenString, key, value) {}
	function deleteAttribute(accessTokenString, name) {}
  ```
  {: pre}

  使用例:

  ```javascript

	const userProfileManager = require("ibmcloud-appid").UserProfileManager;
	userProfileManager.init();

	var accessToken = req.session[WebAppStrategy.AUTH_CONTEXT].accessToken;

	userProfileManager.setAttribute(accessToken, name, value).then(function (attributes) {
		// attributes returned as dictionary
	});
  ```
  {: pre}

  Node.js Server Sdk での作業について詳しくは、<a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">SDK <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を参照してください。
  {: tip}



