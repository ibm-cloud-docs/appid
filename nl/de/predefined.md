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

# Vordefinierte Benutzerattribute
{: #predefined-attributes}

Mit {{site.data.keyword.appid_full}} können Sie Informationen von Identitätsprovidern zu Ihren Benutzern anzeigen.
{: shortdesc}


## Über das iOS-SDK zugreifen
{: #predefined-access-ios}

Werden neue Tokens nicht explizit an das SDK übergeben, verwendet {{site.data.keyword.appid_short_notm}} die zuletzt empfangenen Tokens zum Abrufen und Validieren der Antwort. Sie können nach einer erfolgreichen Authentifizierung beispielsweise den folgenden Code ausführen. Das SDK ruft daraufhin zusätzliche Informationen zu dem jeweiligen Benutzer ab.

```
AppID.sharedInstance.userProfileManager.getUserInfo { (error: Error?, userInfo: [String: Any]?) in
	guard let userInfo = userInfo, err == nil {
		return // Ein Fehler ist aufgetreten.
	}
	// Benutzerinformationen erfolgreich abgerufen.
}
```
{: pre}

Sie können stattdessen jedoch auch explizit Zugriffs- und Identitätstokens übergeben. Das Identitätstoken ist optional und dient, wenn es übergeben wird, zur Validierung der Antwort auf die Benutzerinformationen.

```
AppID.sharedInstance.userProfileManager.getUserInfo(accessToken: String, identityToken: String?) { (error: Error?, userInfo: [String: Any]?) in
	guard let userInfo = userInfo, err == nil {
		return // Ein Fehler ist aufgetreten.
	}
	// Benutzerinformationen erfolgreich abgerufen.
}
```
{: pre}


## Über das Android-SDK zugreifen
{: #predefined-access-android}

Werden neue Tokens nicht explizit an das SDK übergeben, verwendet {{site.data.keyword.appid_short_notm}} die zuletzt empfangenen Tokens zum Abrufen und Validieren der Antwort. Sie können nach einer erfolgreichen Authentifizierung beispielsweise den folgenden Code ausführen. Das SDK ruft daraufhin zusätzliche Informationen zu dem jeweiligen Benutzer ab.

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

Sie können stattdessen jedoch auch explizit Zugriffs- und Identitätstokens übergeben. Das Identitätstoken ist optional und dient, wenn es übergeben wird, zur Validierung der Antwort auf die Benutzerinformationen.

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


## Über das Nodejs-Server-SDK zugreifen
{: #predefined-access-node}


Mithilfe eines serverseitigen SDKs können Sie zusätzliche Informationen zu Ihren Benutzern abrufen. Sie können die folgende Methode mit den gespeicherten Zugriffs- und Identitätstokens aufrufen oder Tokens explizit übergeben. Das Identitätstoken ist optional und dient, wenn es übergeben wird, zur Validierung der Antwort auf die Benutzerinformationen.


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



## Über das Swift-Server-SDK zugreifen
{: #predefined-access-swift}

Mithilfe eines serverseitigen SDKs können Sie zusätzliche Informationen zu Ihren Benutzern abrufen. Sie können die folgende Methode mit den gespeicherten Zugriffs- und Identitätstokens aufrufen oder Tokens explizit übergeben. Das Identitätstoken ist optional und dient, wenn es übergeben wird, zur Validierung der Antwort auf die Benutzerinformationen.


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



## Über die API zugreifen
{: #predefined-access-api}

Sie können zusätzliche Informationen über den Endpunkt `/userinfo` anzeigen.

1. Stellen Sie sicher, dass Sie über ein gültiges Zugriffstoken mit dem Bereich `openid` verfügen. Sie können mithilfe des Endpunkts `/introspect` überprüfen, ob Ihr Token gültig ist.

2. Setzen Sie eine Anforderung an den Endpunkt [`/userinfo` ab](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Authorization_Server_V4/userInfo).
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

3. Stellen Sie sicher, dass der Claim `sub` genau mit dem Claim `sub` im Identitätstoken übereinstimmt. Verwenden Sie die zurückgegebenen Informationen nicht, wenn diese Claims nicht übereinstimmen. Weitere Informationen zur Tokenersetzung finden Sie in der <a href="http://openid.net/specs/openid-connect-core-1_0.html#TokenSubstitution" target="__blank">OIDC-Spezifikation <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>.

Wenn Änderungen von einem externen Identitätsprovider vorgenommen werden, erhalten Sie die aktualisierten Informationen bei der nächsten Anmeldung der Benutzer. Ihre neuen Tokens rufen die aktuellen Daten ab.
{: tip}
