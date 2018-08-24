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

# 사전 정의된 사용자 정보 액세스
{: #predefined}

사용자에 대한 ID 제공자별 정보를 볼 수 있습니다.
{: shortdesc}


## iOS SDK로 액세스
{: #ios}

새 토큰이 SDK에 명시적으로 전달되지 않으면 {{site.data.keyword.appid_short_notm}}에서 마지막으로 수신된 토큰을 사용하여 응답을 검색하고 유효성을 검증합니다. 예를 들어, 인증에 성공한 후 다음 코드를 실행할 수 있습니다. 그러면 SDK에서 사용자에 대한 추가 정보를 검색합니다.

```
AppID.sharedInstance.userProfileManager.getUserInfo { (error: Error?, userInfo: [String: Any]?) in
	guard let userInfo = userInfo, err == nil {
		return // an error has occurred
	}
	// retrieved user info successfully
}

```
{: pre}

또는 액세스 및 ID 토큰을 명시적으로 전달할 수 있습니다. ID 토큰은 선택사항이지만 전달된 경우 사용자 정보 응답의 유효성을 검증하는 데 사용됩니다. 

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

## Android SDK로 액세스
{: #android}

새 토큰이 SDK에 명시적으로 전달되지 않으면 {{site.data.keyword.appid_short_notm}}에서 마지막으로 수신된 토큰을 사용하여 응답을 검색하고 유효성을 검증합니다. 예를 들어, 인증에 성공한 후 다음 코드를 실행할 수 있습니다. 그러면 SDK에서 사용자에 대한 추가 정보를 검색합니다.

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

또는 액세스 및 ID 토큰을 명시적으로 전달할 수 있습니다. ID 토큰은 선택사항이지만 전달된 경우 사용자 정보 응답의 유효성을 검증하는 데 사용됩니다. 

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

## Node.js 서버 SDK로 액세스
{: #node}


서버 측 SDK를 사용하여 사용자에 대한 추가 정보를 검색할 수 있습니다. 저장된 액세스 및 ID 토큰을 사용하여 다음 메소드를 호출할 수 있습니다. 또는 명시적으로 토큰을 전달할 수 있습니다. ID 토큰은 선택사항이지만 전달된 경우 사용자 정보 응답의 유효성을 검증하는 데 사용됩니다. 


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

## Swift 서버 SDK로 액세스
{: #swift}

서버 측 SDK를 사용하여 사용자에 대한 추가 정보를 검색할 수 있습니다. 저장된 액세스 및 ID 토큰을 사용하여 다음 메소드를 호출할 수 있습니다. 또는 명시적으로 토큰을 전달할 수 있습니다. ID 토큰은 선택사항이지만 전달된 경우 사용자 정보 응답의 유효성을 검증하는 데 사용됩니다. 


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

## API로 액세스
{: #api}

`/userinfo` 엔드포인트를 통해 추가 정보를 볼 수 있습니다.

1. `openid` 범위를 사용하여 올바른 액세스 토큰이 있는지 확인하십시오. `/introspect` 엔드포인트를 사용하여 토큰이 올바른지 확인할 수 있습니다.

2. `/userinfo` 엔드포인트에 대한 요청을 작성하십시오.
  ```
  GET [POST] https://{oauth-server-endpoint}/userinfo
  Authorization: 'Bearer {ACCESS_TOKEN}'
  ```
  {: pre}

  출력 예:
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

3. `sub` 청구가 ID 토큰의 `sub` 청구와 정확히 일치하는지 확인하십시오. 일치하지 않는 경우 리턴된 정보를 사용하지 마십시오. 토큰 대체에 대해 자세히 알아보려면 <a href="http://openid.net/specs/openid-connect-core-1_0.html#TokenSubstitution" target="__blank">OIDC 스펙 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>을 참조하십시오.

외부 ID 제공자가 변경사항을 작성한 경우 사용자가 다시 로그인할 때 업데이트된 정보를 가져올 수 있습니다. 새 토큰이 최신 데이터를 검색합니다.
{: tip}
