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

# Accès aux informations utilisateur prédéfinies 
{: #predefined}

Vous pouvez afficher les informations d'un fournisseur d'identité sur vos utilisateurs.
{: shortdesc}


## Accès avec le logiciel SDK iOS 
{: #ios}

Si de nouveaux jetons ne sont pas transmis explicitement au logiciel SDK, {{site.data.keyword.appid_short_notm}} utilise les derniers jetons reçus pour extraire et valider la réponse. Par exemple, vous pouvez exécuter le code suivant une fois que l'authentification a réussi pour que le logiciel SDK extraie des informations supplémentaires sur l'utilisateur : 

```
AppID.sharedInstance.userProfileManager.getUserInfo { (error: Error?, userInfo: [String: Any]?) in
	guard let userInfo = userInfo, err == nil {
		return // an error has occurred
	}
	// retrieved user info successfully
}

```
{: pre}

Vous pouvez aussi transmettre explicitement des jetons d'accès et d'identité. Le jeton d'identité est facultatif mais lorsqu'il est transmis, il est utilisé pour valider la réponse relative aux informations utilisateur. 

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

## Accès avec le logiciel SDK Android 
{: #android}

Si de nouveaux jetons ne sont pas transmis explicitement au logiciel SDK, {{site.data.keyword.appid_short_notm}} utilise les derniers jetons reçus pour extraire et valider la réponse. Par exemple, vous pouvez exécuter le code suivant une fois que l'authentification a réussi pour que le logiciel SDK extraie des informations supplémentaires sur l'utilisateur : 

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

Vous pouvez aussi transmettre explicitement des jetons d'accès et d'identité. Le jeton d'identité est facultatif mais lorsqu'il est transmis, il est utilisé pour valider la réponse relative aux informations utilisateur. 

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

## Accès avec le logiciel SDK serveur Node.js 
{: #node}


Si vous utilisez un logiciel SDK côté serveur, vous pouvez extraire des informations supplémentaires sur vos utilisateurs. Vous pouvez appeler la méthode ci-après en utilisant les jetons d'accès et d'identité stockés, ou transmettre explicitement les jetons. Le jeton d'identité est facultatif mais lorsqu'il est transmis, il est utilisé pour valider la réponse relative aux informations utilisateur. 


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

## Accès avec le logiciel SDK serveur Swift 
{: #swift}

Si vous utilisez un logiciel SDK côté serveur, vous pouvez extraire des informations supplémentaires sur vos utilisateurs. Vous pouvez appeler la méthode ci-après en utilisant les jetons d'accès et d'identité stockés, ou transmettre explicitement les jetons. Le jeton d'identité est facultatif mais lorsqu'il est transmis, il est utilisé pour valider la réponse relative aux informations utilisateur.


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

## Accès avec l'API 
{: #api}

Vous pouvez afficher des informations supplémentaires via le noeud final `/userinfo`. 

1. Assurez-vous de disposer d'un jeton d'accès valide dont la portée est `openid`. Vous pouvez vérifier que votre jeton est valide à l'aide du noeud final `/introspect`. 

2. Envoyez une demande au noeud final `/userinfo`. 
  ```
  GET [POST] https://{oauth-server-endpoint}/userinfo
  Authorization: 'Bearer {ACCESS_TOKEN}'
  ```
  {: pre}

  Exemple de sortie : 
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

3. Vérifiez que la réclamation `sub` correspond exactement
à la
réclamation `sub` qui existe dans le jeton d'identité. Si les demandes ne correspondent pas, n'utilisez pas les informations renvoyées. Pour en savoir plus sur la substitution de jeton, voir la <a href="http://openid.net/specs/openid-connect-core-1_0.html#TokenSubstitution" target="__blank">spécification OIDC <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.

Si des modifications sont apportées par un fournisseur d'identité externe, vous pouvez obtenir les informations mises à jour lorsque vos utilisateurs se reconnectent. Vos nouveaux jetons extraient les informations les plus à jour.
{: tip}
