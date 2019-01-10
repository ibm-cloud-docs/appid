---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:pre: .pre}
{:tip: .tip}
{:screen: .screen}

# Accès aux attributs utilisateur personnalisés
{: #custom}

Avec {{site.data.keyword.appid_full}}, vous pouvez enregistrer et accéder aux attributs personnalisés.
{: shortdesc}

**Pourquoi voudrais-je sauvegarder des attributs supplémentaires concernant un utilisateur ?**

Les attributs sont des éléments d'informations sur vos utilisateurs. En les enregistrant, vous pouvez créer des profils sur vos utilisateurs vous permettant de personnaliser leur expérience. Plus le nombre d'attributs ajoutés à leur profil est élevé, plus leur application peut être personnalisée. Consultez ce blogue pour voir comment la création de profil utilisateur peut faire la différence : <a href="https://www.ibm.com/blogs/bluemix/2017/03/introducing-ibm-bluemix-app-id-authentication-profiles-service-app-developers/" target="_blank">Introducing {{site.data.keyword.appid_short_notm}}<img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.

</br>

**Comment les attributs sont-ils sauvegardés ?**

Selon votre configuration, les attributs sont chiffrés et enregistrés dans le cadre d'un profil utilisateur lorsqu'un utilisateur interagit avec votre application. L'interaction peut être un utilisateur qui se connecte ou définit une préférence dans votre application.

</br>

**Y a-t-il une limite à la quantité d'informations pouvant être stockées pour chaque utilisateur ?**

Vous pouvez stocker jusqu'à 100 Ko d'informations par utilisateur.

</br>

**Y a-t-il des considérations de sécurité que je devrais prendre en compte ?**

Par défaut, les attributs personnalisés sont modifiables et peuvent être mis à jour à l'aide d'un jeton d'accès {{site.data.keyword.appid_short_notm}} provenant d'une application client. Cela signifie que sans précautions appropriées, l'utilisateur ou l'application peut mettre à jour des attributs personnalisés immédiatement après la première connexion de l'utilisateur, à condition qu'il ait accès à un jeton d'accès. Cela peut potentiellement avoir des conséquences inattendues. Par exemple, un utilisateur peut changer son rôle d'utilisateur en administrateur, ce qui peut exposer des privilèges d'administration à des utilisateurs malveillants.

Pour empêcher vos utilisateurs de modifier les attributs que vous leur attribuez, définissez **Changer les attributs personnalisés via l'application** sur **Désactivé** dans l'onglet **Profils** du tableau de bord {{site.data.keyword.appid_short_notm}}. Par défaut, la valeur est **Activé**.
{: tip}

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

Par exemple, vous pouvez utiliser le code ci-dessous pour définir un
nouvel
attribut ou remplacer un attribut existant.

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

Pour plus d'informations sur l'utilisation du logiciel SDK serveur Node.js, voir le <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">logiciel SDK <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.
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


## Accès avec l'API
{: #api}

Vous n'avez pas trouvé de logiciel SDK pour la langue dans laquelle votre application est rédigée ? Pas de problème ! Vous pouvez intégrer le service à l'aide des API.
{: shortdesc}

{{site.data.keyword.appid_short_notm}} fournit une <a href="https://appid-profiles.ng.bluemix.net/swagger-ui/index.html#/Attributes" target="_blank">API REST <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> qui permet la connexion, anonyme ou après authentification, à un [fournisseur d'identité](/docs/services/appid/manageidp.html) pris en charge.
