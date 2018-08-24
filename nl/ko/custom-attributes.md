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

# 사용자 정의 사용자 속성 액세스
{: #custom}

액세스 토큰을 확보할 때 사용자 보호 속성 엔드포인트에 대한 액세스 권한을 얻을 수 있습니다.
{: shortdesc}

{{site.data.keyword.appid_short_notm}}는 지원되는 [ID 제공자](/docs/services/appid/identity-providers.html)를 사용하여 익명으로 또는 인증하여 로그인할 수 있도록 하는 <a href="https://appid-profiles.ng.bluemix.net/swagger-ui/index.html#/Attributes" target="_blank">REST API <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 제공합니다. API 엔드포인트는 로그인 및 권한 부여 프로세스 중에 {{site.data.keyword.appid_short_notm}}에서 생성된 액세스 토큰이 보호하는 리소스입니다.

</br>

## iOS SDK로 액세스
{: #ios}

 다음 API 메소드를 통해 액세스 토큰을 전달하여 사용자 속성에 액세스할 수 있습니다.


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

액세스 토큰이 명시적으로 전달되지 않을 때 {{site.data.keyword.appid_short_notm}}는 마지막으로 수신된 토큰을 사용합니다.

예를 들어, 다음과 같은 코드를 호출하여 새 속성을 설정하거나 기존 속성을 대체할 수 있습니다.

  ```swift
	AppID.sharedInstance.userProfileManager?.setAttribute("key", "value") { (error, result) in
		guard let result = result, error == nil else {
	  		return // an error has occurred
		}
		// attributes recieved as a Dictionary
	})
  ```
  {: pre}

  iOS Swift에서 작업하는 데 대한 자세한 정보는 <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">SDK <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 확인하십시오.
  {: tip}

</br>


## Android SDK로 액세스
{: #android}

다음 API 메소드를 통해 액세스 토큰을 전달하여 사용자 속성에 액세스할 수 있습니다. 

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

액세스 토큰이 명시적으로 전달되지 않을 때 {{site.data.keyword.appid_short_notm}}는 마지막으로 수신된 토큰을 사용합니다.

예를 들어, 다음과 같은 코드를 호출하여 새 속성을 설정하거나 기존 속성을 대체할 수 있습니다.

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

Android에서 작업하는 데 대한 자세한 정보는 <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">SDK <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 확인하십시오.
  {: tip}

</br>

## Swift 서버 SDK로 액세스
{: #swift}

다음 API 메소드를 통해 액세스 토큰을 전달하여 사용자 속성에 액세스할 수 있습니다. 

  ```swift
  func getAllAttributes(accessToken: String, completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  func getAttribute(accessToken: String, attributeName: String, completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  func setAttribute(accessToken: String, attributeName: String, attributeValue : "abc", completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  func deleteAllAttributes(accessToken: String, completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  ```
  {: pre}

  사용법 예:

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

  Swift 서버 Sdk에서 작업하는 데 대한 자세한 정보는 <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">SDK <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 확인하십시오.
  {: tip}

</br>

## Node.js 서버 SDK로 액세스
{: #node}

다음 API 메소드를 통해 액세스 토큰을 전달하여 사용자 속성에 액세스할 수 있습니다. 

  ```javascript
	function getAllAttributes(accessTokenString) {}
	function getAttribute(accessTokenString, key) {}
	function setAttribute(accessTokenString, key, value) {}
	function deleteAttribute(accessTokenString, name) {}
  ```
  {: pre}

  사용법 예:

  ```javascript

	const userProfileManager = require("ibmcloud-appid").UserProfileManager;
	userProfileManager.init();

	var accessToken = req.session[WebAppStrategy.AUTH_CONTEXT].accessToken;

	userProfileManager.setAttribute(accessToken, name, value).then(function (attributes) {
		// attributes returned as dictionary
	});
  ```
  {: pre}

  Node.js 서버 Sdk에서 작업하는 데 대한 자세한 정보는 <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">SDK <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 확인하십시오.
  {: tip}



