---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:pre: .pre}
{:tip: .tip}
{:screen: .screen}

# 存取預先定義的使用者資訊
{: #predefined}

您可以檢視使用者的身分提供者特定資訊。
{: shortdesc}


## 使用 iOS SDK 存取
{: #ios}

如果新的記號未明確地傳遞至 SDK，則 {{site.data.keyword.appid_short_notm}} 會使用最後一個收到的記號來擷取及驗證回應。例如，您可以在成功鑑別之後執行下列程式碼，而 SDK 會擷取使用者的其他資訊。

```
AppID.sharedInstance.userProfileManager.getUserInfo { (error: Error?, userInfo: [String: Any]?) in
	guard let userInfo = userInfo, err == nil {
		return // an error has occurred
	}
	// retrieved user info successfully
}

```
{: pre}

或者，您可以明確地傳遞存取及身分記號。身分記號是選用的，但在傳遞時，會使用它來驗證使用者資訊回應。

```
AppID.sharedInstance.userProfileManager.getUserInfo(accessToken: String, identityToken: String?) { (error: Error?, userInfo: [String: Any]?) in
	guard let userInfo = userInfo, err == nil {
		return // an error has occurred
	}
	// retrieved user info successfully
}
```
{: pre}

</br>

## 使用 Android SDK 存取
{: #android}

如果新的記號未明確地傳遞至 SDK，則 {{site.data.keyword.appid_short_notm}} 會使用最後一個收到的記號來擷取及驗證回應。例如，您可以在成功鑑別之後執行下列程式碼，而 SDK 會擷取使用者的其他資訊。

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

或者，您可以明確地傳遞存取及身分記號。身分記號是選用的，但在傳遞時，會使用它來驗證使用者資訊回應。

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

</br>

## 使用 Node.js 伺服器 SDK 存取
{: #node}


藉由使用伺服器端 SDK，您可以擷取使用者的其他資訊。 您可以使用預存存取及身分記號來呼叫下列方法，也可以明確地傳遞記號。身分記號是選用的，但在傳遞時，會使用它來驗證使用者資訊回應。


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

</br>

## 使用 Swift 伺服器 SDK 存取
{: #swift}

藉由使用伺服器端 SDK，您可以擷取使用者的其他資訊。 您可以使用預存存取及身分記號來呼叫下列方法，也可以明確地傳遞記號。身分記號是選用的，但在傳遞時，會使用它來驗證使用者資訊回應。


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

</br>

## 使用 API 存取
{: #api}

您可以透過 `/userinfo` 端點來檢視其他資訊。

1. 確保您具有含 `openid` 範圍的有效存取記號。您可以使用 `/introspect` 端點來驗證記號是否有效。

2. 向 `/userinfo` 端點提出要求。
  ```
  GET [POST] https://{oauth-server-endpoint}/userinfo
  Authorization: 'Bearer {ACCESS_TOKEN}'
  ```
  {: pre}

  輸出範例：
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

3. 驗證 `sub` 宣告與身分記號中的 `sub` 宣告完全相符。如果這些不相符，則請不要使用傳回的資訊。若要進一步瞭解記號替代，請參閱 <a href="http://openid.net/specs/openid-connect-core-1_0.html#TokenSubstitution" target="__blank">OIDC 規格 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。

如果外部身分提供者進行變更，則您可以在使用者重新登入時取得更新過的資訊。您的新記號會擷取最新的資料。
{: tip}
