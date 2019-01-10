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

# 사용자 정의 사용자 속성 액세스
{: #custom}

{{site.data.keyword.appid_full}}를 사용하여 사용자 정의 속성을 저장하고 액세스할 수 있습니다.
{: shortdesc}

**사용자에 대한 추가적인 속성을 저장하는 이유가 무엇입니까?**

속성은 사용자에 대한 정보의 일부입니다. 이 정보를 저장하여 사용자의 경험을 개인화할 수 있도록 해주는 해당 사용자의 프로파일을 작성할 수 있습니다. 프로파일에 더 많은 속성이 추가될 수록 앱을 더 많이 개인화할 수 있습니다. 사용자 프로파일을 작성함으로써 어떤 차이가 발생하는지 확인하려면 <a href="https://www.ibm.com/blogs/bluemix/2017/03/introducing-ibm-bluemix-app-id-authentication-profiles-service-app-developers/" target="_blank">{{site.data.keyword.appid_short_notm}} 소개<img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a> 블로그를 참조하십시오.

</br>

**속성은 어떻게 저장됩니까?**

구성에 따라 속성은 사용자가 애플리케이션과 상호작용할 때 암호화되어 사용자 프로파일의 일부로 저장됩니다. 이 상호작용은 사용자의 사인인 또는 앱의 환경 설정이 될 수 있습니다.

</br>

**각각의 사용자에 대해 저장할 수 있는 정보의 양에 제한이 있습니까?**

각각의 사용자에 대해 100KB의 정보를 저장할 수 있습니다.

</br>

**보안 고려사항이 있습니까?**

기본적으로 사용자 정의 속성은 수정 가능하며 클라이언트 애플리케이션의 {{site.data.keyword.appid_short_notm}} 액세스 토큰을 사용하여 업데이트할 수 있습니다. 즉, 액세스 토큰에 대한 액세스 권한이 있을 경우 적절한 예방조치를 수행하지 않고 첫 번째 사용자 사인인 이후 즉시 사용자 또는 애플리케이션이 사용자 정의 속성을 업데이트할 수 있습니다. 이로 인해 잠재적으로 의도하지 않은 결과가 발생할 수 있습니다. 예를 들어 사용자가 해당 역할을 사용자에서 관리자로 변경하여 악성 사용자에게 관리 권한을 노출시킬 수 있습니다.

사용자가 제공된 속성을 변경할 수 없도록 차단하려면 {{site.data.keyword.appid_short_notm}} 대시보드의 **프로파일** 탭에서 **앱에서 사용자 정의 속성 변경**을 **끄기**로 설정하십시오. 기본적으로 이 값은 **켜기**로 설정되어 있습니다.
{: tip}

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

iOS Swift에서 작업하는 방법에 관한 자세한 정보는 <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">SDK <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 확인하십시오.
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
		// attributes received in JSON format on successful response
	}

	@Override
	public void onFailure(UserAttributesException e) {
		// exception occurred
	}
});
```
{: pre}

Android에서 작업하는 방법에 관한 자세한 정보는 <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">SDK <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 확인하십시오.
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

Node.js 서버 Sdk에서 작업하는 방법에 관한 자세한 정보는 <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">SDK <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 확인하십시오.
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

Swift 서버 Sdk에서 작업하는 방법에 관한 자세한 정보는 <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">SDK <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 확인하십시오.
{: tip}


## API로 액세스
{: #api}

앱이 작성된 언어용 SDK를 찾을 수 없습니까? 걱정하지 마십시오! API를 사용하여 서비스를 통합할 수 있습니다.
{: shortdesc}

{{site.data.keyword.appid_short_notm}}는 지원되는 [ID 제공자](/docs/services/appid/manageidp.html)를 사용하여 익명으로 또는 인증하여 로그인할 수 있도록 하는 <a href="https://appid-profiles.ng.bluemix.net/swagger-ui/index.html#/Attributes" target="_blank">REST API <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 제공합니다.
