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

# Accessing predefined user information
{: #predefined}

You can view identity provider specific information about your users.
{: shortdesc}


## Accessing with the iOS SDK
{: #ios}

If new tokens are not explicitly passed to the SDK, {{site.data.keyword.appid_short_notm}} uses the last received tokens to retrieve and validate the response. For example, you can execute the following code after a successful authentication and the SDK retrieves additional information about the user.

    ```
    AppID.sharedInstance.userProfileManager.getUserInfo { (error: Error?, userInfo: [String: Any]?) in
    	guard let userInfo = userInfo, err == nil {
    		return // an error has occurred
    	}
    	// retrieved user info successfully
    }

    ```
    {: pre}

  Alternatively, you can explicitly pass access and identity tokens. The identity token is optional, but when passed, it is used to validate the user info response.

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

## Accessing with the Android SDK
{: #android}

  If new tokens are not explicitly passed to the SDK, {{site.data.keyword.appid_short_notm}} uses the last received tokens to retrieve and validate the response. For example, you can execute the following code after a successful authentication and the SDK retrieves additional information about the user.

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

  Alternatively, you can explicitly pass access and identity tokens. The identity token is optional, but when passed, it is used to validate the user info response.

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

## Accessing with the Node.js Server SDK
{: #node}


By using a server-side SDK, you can retrieve additional information about your users. You can call the following method by using the stored access and identity tokens, or you can explicitly pass the tokens. The identity token is optional, but when passed, it's used to validate the user info response.


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

## Accessing with the Swift Server SDK
{: #swift}

By using a server-side SDK, you can retrieve additional information about your users. You can call the following method by using the stored access and identity tokens, or you can explicitly pass the tokens. The identity token is optional, but when passed, it's used to validate the user info response.


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

## Accessing with the API
{: #api}

You can view additional information through the `/userinfo` endpoint.

1. Be sure that you have a valid access token with an `openid` scope. You can verify that your token is valid by using the `/introspect` endpoint.

2. Make a request to the `/userinfo` endpoint.
  ```
  GET [POST] https://{oauth-server-endpoint}/userinfo
  Authorization: 'Bearer {ACCESS_TOKEN}'
  ```
  {: pre}

  Example output:
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

3. Verify that the `sub` claim exactly matches the `sub` claim in the identity token. If these do not match, do not use the returned information. To learn more about token substitution, see the <a href="http://openid.net/specs/openid-connect-core-1_0.html#TokenSubstitution" target="__blank">OIDC specification <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.

If changes are made by an external identity provider, you can get the updated information when your users log in again. Your new tokens retrieve the most up-to-date data.
{: tip}
