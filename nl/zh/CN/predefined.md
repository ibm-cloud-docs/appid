---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

keywords: authentication, authorization, identity, app security, secure, user information, attributes, accessing, storing, preregister, profiles

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

# 预定义的用户属性
{: #predefined-attributes}

通过 {{site.data.keyword.appid_full}}，您可以查看有关用户的特定于身份提供者的信息。
{: shortdesc}


## 使用 iOS SDK 访问
{: #predefined-access-ios}

如果未显式地将新令牌传递给 SDK，那么 {{site.data.keyword.appid_short_notm}} 使用上次收到的令牌来检索并验证响应。例如，您可以在认证成功后执行以下代码，并且 SDK 检索有关用户的其他信息。

```
AppID.sharedInstance.userProfileManager.getUserInfo { (error: Error?, userInfo: [String: Any]?) in
	guard let userInfo = userInfo, err == nil {
		return // an error has occurred
	}
	// retrieved user info successfully
}
```
{: pre}

或者，也可以显式地传递访问和身份令牌。身份令牌为可选，但是在传递时，用于验证用户信息响应。

```
AppID.sharedInstance.userProfileManager.getUserInfo(accessToken: String, identityToken: String?) { (error: Error?, userInfo: [String: Any]?) in
	guard let userInfo = userInfo, err == nil {
		return // an error has occurred
	}
	// retrieved user info successfully
}
```
{: pre}


## 使用 Android SDK 访问
{: #predefined-access-android}

如果未显式地将新令牌传递给 SDK，那么 {{site.data.keyword.appid_short_notm}} 使用上次收到的令牌来检索并验证响应。例如，您可以在认证成功后执行以下代码，并且 SDK 检索有关用户的其他信息。

```
AppID appId = AppID.getInstance();

appId.getUserProfileManager().getUserInfo(new UserProfileResponseListener() {
	@Override
	public void onSuccess(JSONObject userInfo) {
		// retrieved user info successfully
	}

	@Override
	public void onFailure(UserInfoException e) {
		// exception occurred
	}
});
```
{: pre}

或者，也可以显式地传递访问和身份令牌。身份令牌为可选，但是在传递时，用于验证用户信息响应。

```
AppID appId = AppID.getInstance();

appId.getUserProfileManager().getUserInfo(accessToken, identityToken, new UserProfileResponseListener() {
	@Override
	public void onSuccess(JSONObject userInfo) {
		// retrieved attribute "name" successfully
	}

	@Override
	public void onFailure(UserInfoException e) {
		// exception occurred
	}
});
```
{: pre}


## 使用 Node.js Server SDK 访问
{: #predefined-access-node}


通过使用服务器端 SDK，您可以检索有关用户的其他信息。您可以使用存储的访问和身份令牌来调用以下方法，也可以显式地传递令牌。身份令牌为可选，但是在传递时，用于验证用户信息响应。


```javascript
let userProfileManager = UserProfileManager(options: options)

let accessToken = req.session[WebAppStrategy.AUTH_CONTEXT].accessToken;
let identityToken = req.session[WebAppStrategy.AUTH_CONTEXT].identityToken;


// Retrieve user info and validate against the given identity token
userProfileManager.getUserInfo(accessToken, identityToken).then(function (profile) {
	// retrieved user info successfully
});

// Retrieve user info without validation
userProfileManager.getUserInfo(accessToken).then(function (profile) {
	// retrieved user info successfully
});
```
{: pre}



## 使用 Swift Server SDK 访问
{: #predefined-access-swift}

通过使用服务器端 SDK，您可以检索有关用户的其他信息。您可以使用存储的访问和身份令牌来调用以下方法，也可以显式地传递令牌。身份令牌为可选，但是在传递时，用于验证用户信息响应。


```swift
let userProfileManager = UserProfileManager(options: options)

let accessToken = "<access token>"
let identityToken = "<identity token>"

// If identity token is provided (recommended approach), response is validated against the identity token
userProfileManager.getUserInfo(accessToken: accessToken, identityToken: identityToken) { (err, userInfo) in
	guard let userInfo = userInfo, err == nil {
		return // an error has occurred
	}
	// retrieved user info successfully
}

// Retrieve the UserInfo without any validation
userProfileManager.getUserInfo(accessToken: accessToken) { (err, userInfo) in
	guard let userInfo = userInfo, err == nil {
		return // an error has occurred
	}
	// retrieved user info successfully
}
```
{: pre}



## 使用 API 访问
{: #predefined-access-api}

您可以通过 `/userinfo` 端点查看其他信息。

1. 请确保您具有范围为 `openid` 的有效访问令牌。您可以使用 `/introspect` 端点来验证令牌是否有效。

2. 对 [`/userinfo` 端点](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Authorization_Server_V4/userInfo)发出请求。
  ```
  GET [POST] https://{oauth-server-endpoint}/userinfo
  Authorization: 'Bearer {ACCESS_TOKEN}'
  ```
  {: pre}

  下面是输出示例：
  ```
  "sub": "cad9f1d4-e23b-3683-b81b-d1c4c4fd7d4c",
  "name": "John Doe",
  "email": "john.doe@gmail.com",
  "picture": "https://lh3.googleusercontent.com/-XdUIqdbhg/AAAAAAAAI/AAAAAAA/42rbcbv5M/photo.jpg",
  "gender": "male",
  "locale": "en",
  "identities": [
      {
          "provider": "google",
          "id": "104560903311317789798",
          "profile": {
              "id": "104560903311317789798",
              "email": "john.doe@gmail.com",
              "verified_email": true,
              "name": "John Doe",
              "given_name": "John",
              "family_name": "Doe",
              "link": "https://plus.google.com/104560903311317789798",
              "picture": "https://lh3.googleusercontent.com/-XdUIqdbhg/AAAAAAAAI/AAAAAAA/42rbcbv5M/photo.jpg",
              "gender": "male",
              "locale": "en",
              "idpType": "google"
          }
      }
  ]
  ```
  {: screen}

3. 验证 `sub` 声明是否与身份令牌中的 `sub` 声明完全匹配。如果不匹配，那么请勿使用返回的信息。要了解有关令牌替换的更多信息，请参阅 <a href="http://openid.net/specs/openid-connect-core-1_0.html#TokenSubstitution" target="__blank">OIDC 规范 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>。

如果外部身份提供者执行更改，那么在用户再次登录时可获取更新的信息。新令牌会检索最新的数据。
{: tip}
