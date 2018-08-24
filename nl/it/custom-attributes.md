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

# Accesso agli attributi dell'utente personalizzati
{: #custom}

Quando ottieni un token di accesso, è possibile ottenere l'accesso all'endpoint degli attributi protetti dell'utente.
{: shortdesc}

{{site.data.keyword.appid_short_notm}} fornisce un'API REST <a href="https://appid-profiles.ng.bluemix.net/swagger-ui/index.html#/Attributes" target="_blank"> <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> che consente l'accesso, in modo anonimo o tramite autenticazione, con un [provider di identità](/docs/services/appid/identity-providers.html). L'endpoint API è una risorsa protetta dal token di accesso generato da {{site.data.keyword.appid_short_notm}} durante il processo di autorizzazione e accesso.

</br>

## Accesso con l'SDK iOS
{: #ios}

 Puoi accedere agli attributi degli utenti personalizzati passando un token di accesso tramite i seguenti metodi API.

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

Quando il token di accesso non viene esplicitamente trasmesso, {{site.data.keyword.appid_short_notm}} utilizza l'ultimo token ricevuto.

Ad esempio, puoi richiamare questo codice per impostare un nuovo attributo o sovrascriverne uno esistente.

  ```swift
	AppID.sharedInstance.userProfileManager?.setAttribute("key", "value") { (error, result) in
		guard let result = result, error == nil else {
	  		return // si è verificato un errore
		}
		// attributi ricevuti come un dizionario
	})
  ```
  {: pre}

  Per ulteriori informazioni sull'utilizzo di iOS Swift, consulta <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">SDK <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>.
  {: tip}

</br>


## Accesso con l'SDK Android
{: #android}

Puoi accedere agli attributi degli utenti personalizzati passando un token di accesso tramite i seguenti metodi API.

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

Quando il token di accesso non viene esplicitamente trasmesso, {{site.data.keyword.appid_short_notm}} utilizza l'ultimo token ricevuto.

Ad esempio, puoi richiamare questo codice per impostare un nuovo attributo o sovrascriverne uno esistente.

```java
appId.getUserProfileManager().setAttribute(name, value, useThisToken, new UserProfileResponseListener() {
	@Override
		public void onSuccess(JSONObject attributes) {
		//attributi ricevuti nel formato JSON per una risposta positiva
		}

	@Override
		public void onFailure(UserAttributesException e) {
		// si è verificata un'eccezione
	}
});
```
{: pre}

Per ulteriori informazioni sull'utilizzo di Android, consulta <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">SDK <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>.
{: tip}

</br>

## Accesso con l'SDK Swift Server
{: #swift}

Puoi accedere agli attributi degli utenti personalizzati passando un token di accesso tramite i seguenti metodi API.

  ```swift
  func getAllAttributes(accessToken: String, completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  func getAttribute(accessToken: String, attributeName: String, completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  func setAttribute(accessToken: String, attributeName: String, attributeValue : "abc", completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  func deleteAllAttributes(accessToken: String, completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  ```
  {: pre}

  Esempio di utilizzo:

  ```swift

	let userProfileManager = UserProfileManager(options: options)
	let accesstoken = "access token"

	userProfileManager.setAttribute(accessToken: accessToken, attributeName: "name", attributeValue : "abc") { (error, response) in
		guard let response = response, error == error else {
			return // si è verificato un errore
		}
		// attributi ricevuti come un dizionario
	}
  ```

  {: pre}

  Per ulteriori informazioni sull'utilizzo dell'SDK Swift Server, consulta <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">SDK <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>.
  {: tip}

</br>

## Accesso con l'SDK Node.js Server
{: #node}

Puoi accedere agli attributi degli utenti personalizzati passando un token di accesso tramite i seguenti metodi API.

  ```javascript
	function getAllAttributes(accessTokenString) {}
	function getAttribute(accessTokenString, key) {}
	function setAttribute(accessTokenString, key, value) {}
	function deleteAttribute(accessTokenString, name) {}
  ```
  {: pre}

  Utilizzo di esempio:

  ```javascript

	const userProfileManager = require("ibmcloud-appid").UserProfileManager;
	userProfileManager.init();

	var accessToken = req.session[WebAppStrategy.AUTH_CONTEXT].accessToken;

	userProfileManager.setAttribute(accessToken, name, value).then(function (attributes) {
		// attributi restituiti come un dizionario
	});
  ```
  {: pre}

  Per ulteriori informazioni sull'utilizzo dell'SDK Node.js Server, consulta <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">SDK <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>.
  {: tip}



