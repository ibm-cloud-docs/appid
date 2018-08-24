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

# Auf vordefinierte Benutzerinformationen zugreifen
{: #predefined}

Sie können Informationen von Identitätsprovidern zu Ihren Benutzern anzeigen.
{: shortdesc}


## Über das iOS-SDK zugreifen
{: #ios}

Werden neue Token nicht explizit an das SDK übergeben, verwendet {{site.data.keyword.appid_short_notm}} die zuletzt empfangenen Token zum Abrufen und Validieren der Antwort. Sie können nach einer erfolgreichen Authentifizierung beispielsweise den folgenden Code ausführen. Das SDK ruft daraufhin zusätzliche Informationen zu dem jeweiligen Benutzer ab. 

```
AppID.sharedInstance.userProfileManager.getUserInfo { (error: Error?, userInfo: [String: Any]?) in
	guard let userInfo = userInfo, err == nil {
		return // Ein Fehler ist aufgetreten.
	}
	// Benutzerinformationen erfolgreich abgerufen.
}

```
{: pre}

Sie können stattdessen jedoch auch explizit Zugriffs- und Identitätstoken übergeben. Das Identitätstoken ist optional und dient, wenn es übergeben wird, zur Validierung der Antwort auf die Benutzerinformationen. 

```
AppID.sharedInstance.userProfileManager.getUserInfo(accessToken: String, identityToken: String?) { (error: Error?, userInfo: [String: Any]?) in
	guard let userInfo = userInfo, err == nil {
		return // Ein Fehler ist aufgetreten.
	}
	// Benutzerinformationen erfolgreich abgerufen.
}
```
{: pre}

</br>

## Über das Android-SDK zugreifen
{: #android}

Werden neue Token nicht explizit an das SDK übergeben, verwendet {{site.data.keyword.appid_short_notm}} die zuletzt empfangenen Token zum Abrufen und Validieren der Antwort. Sie können nach einer erfolgreichen Authentifizierung beispielsweise den folgenden Code ausführen. Das SDK ruft daraufhin zusätzliche Informationen zu dem jeweiligen Benutzer ab. 

```
AppID appId = AppID.getInstance();

appId.getUserProfileManager().getUserInfo(new UserProfileResponseListener() {
	@Override
	public void onSuccess(JSONObject userInfo) {
		// Benutzerinformationen erfolgreich abgerufen
 }

 @Override
	public void onFailure(UserInfoException e) {
		// Eine Ausnahmebedingung ist aufgetreten.
	}
});
```
{: pre}

Sie können stattdessen jedoch auch explizit Zugriffs- und Identitätstoken übergeben. Das Identitätstoken ist optional und dient, wenn es übergeben wird, zur Validierung der Antwort auf die Benutzerinformationen. 

```
AppID appId = AppID.getInstance();

appId.getUserProfileManager().getUserInfo(accessToken, identityToken, new UserProfileResponseListener() {
	@Override
	public void onSuccess(JSONObject userInfo) {
		// Attribut "name" wurde erfolgreich abgerufen
	}

	@Override
	public void onFailure(UserInfoException e) {
		// Eine Ausnahmebedingung ist aufgetreten.
	}
});
```
{: pre}

</br>

## Über das Nodejs-Server-SDK zugreifen
{: #node}


Mithilfe eines serverseitigen SDKs können Sie zusätzliche Informationen zu Ihren Benutzern abrufen. Sie können die folgende Methode mit den gespeicherten Zugriffs- und Identitätstoken aufrufen oder explizit Token übergeben. Das Identitätstoken ist optional und dient, wenn es übergeben wird, zur Validierung der Antwort auf die Benutzerinformationen. 


```javascript
let userProfileManager = UserProfileManager(options: options)

let accessToken = req.session[WebAppStrategy.AUTH_CONTEXT].accessToken;
let identityToken = req.session[WebAppStrategy.AUTH_CONTEXT].identityToken;


// Benutzerinformationen abrufen und anhand des gegebenen Identitätstokens validieren
userProfileManager.getUserInfo(accessToken, identityToken).then(function (profile) {
	// Benutzerinformationen erfolgreich abgerufen
});

// Benutzerinformationen ohne Validierung abrufen
userProfileManager.getUserInfo(accessToken).then(function (profile) {
	// Benutzerinformationen erfolgreich abgerufen
});
```
{: pre}

</br>

## Über das Swift-Server-SDK zugreifen
{: #swift}

Mithilfe eines serverseitigen SDKs können Sie zusätzliche Informationen zu Ihren Benutzern abrufen. Sie können die folgende Methode mit den gespeicherten Zugriffs- und Identitätstoken aufrufen oder explizit Token übergeben. Das Identitätstoken ist optional und dient, wenn es übergeben wird, zur Validierung der Antwort auf die Benutzerinformationen. 


```swift
let userProfileManager = UserProfileManager(options: options)

let accessToken = "<access token>"
let identityToken = "<identity token>"

// Bei Übergabe eines Identitätstokens (empfohlene Vorgehensweise) wird die Antwort mit dem Identitätstoken validiert.
userProfileManager.getUserInfo(accessToken: accessToken, identityToken: identityToken) { (err, userInfo) in
	guard let userInfo = userInfo, err == nil {
		return // Ein Fehler ist aufgetreten.
	}
	// Benutzerinformationen erfolgreich abgerufen.
}

// Benutzerinformationen ohne Validierung abrufen
userProfileManager.getUserInfo(accessToken: accessToken) { (err, userInfo) in
	guard let userInfo = userInfo, err == nil {
		return // Ein Fehler ist aufgetreten.
	}
	// Benutzerinformationen erfolgreich abgerufen.
}
```
{: pre}

</br>

## Über die API zugreifen
{: #api}

Sie können zusätzliche Informationen über den Endpunkt `/userinfo` anzeigen. 

1. Stellen Sie sicher, dass Sie über ein gültiges Zugriffstoken mit dem Bereich `openid` verfügen. Sie können mithilfe des Endpunkts `/introspect` überprüfen, ob Ihr Token gültig ist. 

2. Erstellen Sie eine Anforderung für den Endpunkt `/userinfo`. 
  ```
  GET [POST] https://{oauth-server-endpoint}/userinfo
  Authorization: 'Bearer {ACCESS_TOKEN}'
  ```
  {: pre}

  Beispielausgabe: 
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

3. Stellen Sie sicher, dass die Anforderung `sub` genau mit der Anforderung `sub` im Identitätstoken übereinstimmt. Verwenden Sie die zurückgegebenen Informationen nicht, wenn diese Anforderungen nicht übereinstimmen. Weitere Informationen zur Tokenersetzung finden Sie in der <a href="http://openid.net/specs/openid-connect-core-1_0.html#TokenSubstitution" target="__blank">OIDC-Spezifikation<img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>.

Wenn Änderungen von einem externen Identitätsprovider vorgenommen werden, erhalten Sie die aktualisierten Informationen bei der nächsten Anmeldung der Benutzer. Ihre neuen Token rufen die aktuellen Daten ab.
{: tip}
