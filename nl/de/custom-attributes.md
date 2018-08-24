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

# Auf angepasste Benutzerattribute zugreifen
{: #custom}

Wenn Sie ein Zugriffstoken anfordern, können Sie Zugriff auf den Endpunkt der geschützten Benutzerattribute zugreifen.
{: shortdesc}

{{site.data.keyword.appid_short_notm}} stellt eine <a href="https://appid-profiles.ng.bluemix.net/swagger-ui/index.html#/Attributes" target="_blank">REST-API <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> bereit, die die Anmeldung - anonym oder mit Authentifizierung - über einen unterstützten [Identitätsprovider](/docs/services/appid/identity-providers.html) ermöglicht. Der API-Endpunkt ist eine Ressource, die durch das Zugriffstoken geschützt ist, das beim Anmelde- und Berechtigungsprozess von {{site.data.keyword.appid_short_notm}} generiert wird.

</br>

## Über das iOS-SDK zugreifen
{: #ios}

 Sie können auf angepasste Attribute zugreifen, indem Sie ein Zugriffstoken über die folgenden API-Methoden übergeben.


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

Wenn ein Zugriffstoken nicht explizit übergeben wird, verwendet {{site.data.keyword.appid_short_notm}} das zuletzt empfangene Token.

Sie können beispielsweise diesen Code aufrufen, um ein neues Attribut festzulegen oder ein vorhandenes Attribut zu überschreiben.

  ```swift
	AppID.sharedInstance.userProfileManager?.setAttribute("key", "value") { (error, result) in
		guard let result = result, error == nil else {
	  		return // Ein Fehler ist aufgetreten.
		}
		// Attribute als Verzeichnis empfangen.
	})
  ```
  {: pre}

  Weitere Informationen zur Arbeit mit iOS Swift finden Sie im Abschnitt <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">SDK <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.
  {: tip}

</br>


## Über das Android-SDK zugreifen
{: #android}

Sie können auf angepasste Attribute zugreifen, indem Sie ein Zugriffstoken über die folgenden API-Methoden übergeben.


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

Wenn ein Zugriffstoken nicht explizit übergeben wird, verwendet {{site.data.keyword.appid_short_notm}} das zuletzt empfangene Token.

Sie können beispielsweise diesen Code aufrufen, um ein neues Attribut festzulegen oder ein vorhandenes Attribut zu überschreiben.

```java
appId.getUserProfileManager().setAttribute(name, value, useThisToken, new UserProfileResponseListener() {
	@Override
		public void onSuccess(JSONObject attributes) {
		// Attribute im JSON-Format nach erfolgreicher Antwort empfangen.
		}

	@Override
		public void onFailure(UserAttributesException e) {
		// Eine Ausnahmebedingung ist aufgetreten.
	}
});
```
{: pre}

Weitere Informationen zur Arbeit mit Android finden Sie im Abschnitt <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">SDK <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.
{: tip}

</br>

## Über das Swift-Server-SDK zugreifen
{: #swift}

Sie können auf angepasste Attribute zugreifen, indem Sie ein Zugriffstoken über die folgenden API-Methoden übergeben.


  ```swift
  func getAllAttributes(accessToken: String, completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  func getAttribute(accessToken: String, attributeName: String, completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  func setAttribute(accessToken: String, attributeName: String, attributeValue : "abc", completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  func deleteAllAttributes(accessToken: String, completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  ```
  {: pre}

  Beispiel: 

  ```swift

	let userProfileManager = UserProfileManager(options: options)
	let accesstoken = "access token"

	userProfileManager.setAttribute(accessToken: accessToken, attributeName: "name", attributeValue : "abc") { (error, response) in
		guard let response = response, error == error else {
			return // Ein Fehler ist aufgetreten.
		}
		// Attribute als Verzeichnis empfangen.
	}
  ```

  {: pre}

  Weitere Informationen zur Arbeit mit dem Swift-Server-SDK finden Sie im Abschnitt <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">SDK <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>.
  {: tip}

</br>

## Über das Nodejs-Server-SDK zugreifen
{: #node}

Sie können auf angepasste Attribute zugreifen, indem Sie ein Zugriffstoken über die folgenden API-Methoden übergeben.


  ```javascript
	function getAllAttributes(accessTokenString) {}
	function getAttribute(accessTokenString, key) {}
	function setAttribute(accessTokenString, key, value) {}
	function deleteAttribute(accessTokenString, name) {}
  ```
  {: pre}

  Beispiel: 

  ```javascript

	const userProfileManager = require("ibmcloud-appid").UserProfileManager;
	userProfileManager.init();

	var accessToken = req.session[WebAppStrategy.AUTH_CONTEXT].accessToken;

	userProfileManager.setAttribute(accessToken, name, value).then(function (attributes) {
		// Attribute als Verzeichnis zurückgegeben.
	});
  ```
  {: pre}

  Weitere Informationen zur Arbeit mit dem Nodejs-Server-SDK finden Sie im Abschnitt <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">SDK <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>.
  {: tip}



