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

# Accès aux attributs utilisateur personnalisés 
{: #custom}

En obtenant un jeton d'accès, vous pouvez accéder au noeud final des attributs utilisateur protégés.
{: shortdesc}

{{site.data.keyword.appid_short_notm}} fournit une <a href="https://appid-profiles.ng.bluemix.net/swagger-ui/index.html#/Attributes" target="_blank">API REST <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> qui permet la connexion, anonyme ou après authentification, à un [fournisseur d'identité](/docs/services/appid/identity-providers.html) pris en charge. Le noeud final d'API est une ressource protégée par le jeton d'accès qui est généré par {{site.data.keyword.appid_short_notm}} au cours du processus de connexion et d'autorisation. 

</br>

## Accès avec le logiciel SDK iOS 
{: #ios}

 Vous pouvez accéder aux attributs personnalisés en transmettant un jeton d'accès à l'aide des méthodes d'API ci-dessous. 

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

Lorsqu'un jeton d'accès n'est pas transmis explicitement, {{site.data.keyword.appid_short_notm}} utilise le dernier jeton reçu.

Par exemple, vous pouvez utiliser le code ci-dessous pour définir un nouvel attribut ou remplacer un attribut existant.

  ```swift
	AppID.sharedInstance.userProfileManager?.setAttribute("key", "value") { (error, result) in
		guard let result = result, error == nil else {
	  		return // an error has occurred
		}
		// attributes received as a Dictionary
	})
  ```
  {: pre}

  Pour plus d'informations sur l'exécution dans iOS Swift, voir le <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">logiciel SDK <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.
  {: tip}

</br>


## Accès avec le logiciel SDK Android 
{: #android}

Vous pouvez accéder aux attributs personnalisés en transmettant un jeton d'accès à l'aide des méthodes d'API ci-dessous. 

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

Lorsqu'un jeton d'accès n'est pas transmis explicitement, {{site.data.keyword.appid_short_notm}} utilise le dernier jeton reçu.

Par exemple, vous pouvez utiliser le code ci-dessous pour définir un
nouvel
attribut ou remplacer un attribut existant.

```java
appId.getUserProfileManager().setAttribute(name, value, useThisToken, new UserProfileResponseListener() {
	@Override
		public void onSuccess(JSONObject attributes) {
		//attributes received in JSON format on successful response 		}

	@Override 		public
void onFailure(UserAttributesException e) {
		// exception occurred
	}
});
```
{: pre}

Pour plus d'informations sur l'exécution dans Android, voir le <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">logiciel SDK <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.
{: tip}

</br>

## Accès avec le logiciel SDK serveur Swift 
{: #swift}

Vous pouvez accéder aux attributs personnalisés en transmettant un jeton d'accès à l'aide des méthodes d'API ci-dessous. 

  ```swift
  func getAllAttributes(accessToken: String, completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  func getAttribute(accessToken: String, attributeName: String, completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  func setAttribute(accessToken: String, attributeName: String, attributeValue : "abc", completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  func deleteAllAttributes(accessToken: String, completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  ```
  {: pre}

  Exemple d'utilisation : 

  ```swift

	let userProfileManager = UserProfileManager(options: options)
	let accesstoken = "access token"

	userProfileManager.setAttribute(accessToken: accessToken, attributeName: "name", attributeValue : "abc") { (error, response) in
		guard let response = response, error == error else {
			return // an error has occurred
		}
		// attributes received as a Dictionary
	}
  ```

  {: pre}

  Pour plus d'informations sur l'utilisation du logiciel SDK serveur Swift, voir le <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">logiciel SDK <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.
 {: tip}

</br>

## Accès avec le logiciel SDK serveur Node.js 
{: #node}

Vous pouvez accéder aux attributs personnalisés en transmettant un jeton d'accès à l'aide des méthodes d'API ci-dessous. 

  ```javascript
	function getAllAttributes(accessTokenString) {}
	function getAttribute(accessTokenString, key) {}
	function setAttribute(accessTokenString, key, value) {}
	function deleteAttribute(accessTokenString, name) {}
  ```
  {: pre}

  Exemple d'utilisation :

  ```javascript

	const userProfileManager = require("ibmcloud-appid").UserProfileManager;
	userProfileManager.init();

	var accessToken = req.session[WebAppStrategy.AUTH_CONTEXT].accessToken;

	userProfileManager.setAttribute(accessToken, name, value).then(function (attributes) {
		// attributes returned as dictionary
	});
  ```
  {: pre}

  Pour plus d'informations sur l'utilisation du logiciel SDK serveur Node.js, voir le <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">logiciel SDK <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>. {: tip}



