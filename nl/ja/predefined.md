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

# 事前定義されたユーザー属性
{: #predefined-attributes}

{{site.data.keyword.appid_full}} を使用して、ユーザーに関する ID プロバイダー固有の情報を表示できます。
{: shortdesc}


## iOS SDK を使用したアクセス
{: #predefined-access-ios}

新しいトークンが SDK に明示的に渡されない場合、{{site.data.keyword.appid_short_notm}} は最後に受信したトークンを使用して応答の取得と検証を行います。 例えば、認証が正常に完了した後に以下のコードを実行して、SDK がユーザーに関する追加情報を取得するようにすることができます。

```
AppID.sharedInstance.userProfileManager.getUserInfo { (error: Error?, userInfo: [String: Any]?) in
	guard let userInfo = userInfo, err == nil {
		return // an error has occurred
	}
	// retrieved user info successfully
}
```
{: pre}

代わりに、アクセス権限と識別トークンを明示的に渡すことができます。 識別トークンはオプションですが、渡された場合には、ユーザー情報応答の検証に使用されます。

```
AppID.sharedInstance.userProfileManager.getUserInfo(accessToken: String, identityToken: String?) { (error: Error?, userInfo: [String: Any]?) in
	guard let userInfo = userInfo, err == nil {
		return // an error has occurred
	}
	// retrieved user info successfully
}
```
{: pre}


## Android SDK を使用したアクセス
{: #predefined-access-android}

新しいトークンが SDK に明示的に渡されない場合、{{site.data.keyword.appid_short_notm}} は最後に受信したトークンを使用して応答の取得と検証を行います。 例えば、認証が正常に完了した後に以下のコードを実行して、SDK がユーザーに関する追加情報を取得するようにすることができます。

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

代わりに、アクセス権限と識別トークンを明示的に渡すことができます。 識別トークンはオプションですが、渡された場合には、ユーザー情報応答の検証に使用されます。

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


## Node.js Server SDK を使用したアクセス
{: #predefined-access-node}


サーバー・サイドの SDK を使用すると、ユーザーに関する追加情報を取得できます。 ストアード・アクセスと ID トークンを使用して以下のメソッドを呼び出すことも、トークンを明示的に渡すこともできます。 識別トークンはオプションですが、渡された場合には、ユーザー情報応答の検証に使用されます。


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



## Swift Server SDK を使用したアクセス
{: #predefined-access-swift}

サーバー・サイドの SDK を使用すると、ユーザーに関する追加情報を取得できます。 ストアード・アクセスと ID トークンを使用して以下のメソッドを呼び出すことも、トークンを明示的に渡すこともできます。 識別トークンはオプションですが、渡された場合には、ユーザー情報応答の検証に使用されます。


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



## API を使用したアクセス
{: #predefined-access-api}

`/userinfo` エンドポイントを介して、追加情報を表示できます。

1. `openid` スコープを持つ有効なアクセス・トークンを所有していることを確認してください。 `/introspect` エンドポイントを使用して、トークンが有効であることを確認できます。

2. [`/userinfo` エンドポイント](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Authorization_Server_V4/userInfo)に対して要求を行います。
  ```
  GET [POST] https://{oauth-server-endpoint}/userinfo
  Authorization: 'Bearer {ACCESS_TOKEN}'
  ```
  {: pre}

  出力例:
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

3. この `sub` クレームが識別トークン内の `sub` クレームと正確に一致することを確認します。 それらが一致しない場合は、返された情報を使用しないでください。 トークンの置換について詳しくは、<a href="http://openid.net/specs/openid-connect-core-1_0.html#TokenSubstitution" target="__blank">OIDC の仕様 <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を参照してください。

外部の ID プロバイダーによって変更が行われた場合は、ユーザーが再度ログインするときに、更新された情報を取得できます。 新しいトークンにより、最新のデータが取得されます。
{: tip}
