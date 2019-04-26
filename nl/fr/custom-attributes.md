---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-14"

keywords: authentication, authorization, identity, app security, secure, attributes, user information, storing, accessing

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
{:java: .ph data-hd-programlang='java'}
{:javascript: .ph data-hd-programlang='javascript'}
{:swift: .ph data-hd-programlang='swift'}
{:curl: .ph data-hd-programlang='curl'}

# Attributs utilisateur personnalisés
{: #custom-attributes}

Avec {{site.data.keyword.appid_full}}, vous pouvez sauvegarder, accéder à et mettre à jour des attributs personnalisés.
{: shortdesc}


## Définition des attributs
{: #setting-custom-attributes}

Vous pouvez définir des rôles et les portées appelés attributs dans un profil utilisateur. Vous pouvez également redéfinir des attributs existants qui proviennent d'un fournisseur d'identités externe.
{: shortdesc}


Les attributs sont des éléments d'informations sur vos utilisateurs. En les enregistrant, vous pouvez créer des profils sur vos utilisateurs vous permettant de personnaliser leur expérience. Plus le nombre d'attributs ajoutés à leur profil est élevé, plus leur expérience d'application peut être personnalisée. Consultez ce blogue pour voir comment la création de profil utilisateur peut faire la différence : <a href="https://www.ibm.com/blogs/bluemix/2017/03/introducing-ibm-bluemix-app-id-authentication-profiles-service-app-developers/" target="blank">Introducing {{site.data.keyword.appid_short_notm}}<img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.


Vous pouvez stocker jusqu'à 100 Ko d'informations par utilisateur.
{: note}


**Pour définir un attribut :**

Toutes les demandes entrantes vers votre application ont un en-tête d'autorisation avec `access_token`. Vous pouvez utiliser `access_token` pour adresser des demandes aux noeuds finaux des attributs personnalisés avec l'un des logiciels SDK fournis ou à l'aide des [API d'attribut](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Attributes).


iOS Swift :
{: ph data-hd-programlang='swift'}

  ```
	AppID.sharedInstance.userProfileManager?.setAttribute("key", "value") { (error, result) in
		guard let result = result, error == nil else {
	  		return // an error has occurred
		}
		// attributes received as a Dictionary
	})
  ```
  {: codeblock}
  {: ph data-hd-programlang='swift'}

  ```
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
  {: codeblock}
  {: ph data-hd-programlang='java'}

  ```
	const userProfileManager = require("ibmcloud-appid").UserProfileManager;
	userProfileManager.init();

	var accessToken = req.session[WebAppStrategy.AUTH_CONTEXT].accessToken;

	userProfileManager.setAttribute(accessToken, name, value).then(function (attributes) {
		// attributes returned as dictionary
	});
  ```
  {: codeblock}
  {: ph data-hd-programlang='javascript'}

Server Swift :
{: ph data-hd-programlang='swift'}

  ```
  let userProfileManager = UserProfileManager(options: options)
	let accesstoken = "access token"

  userProfileManager.setAttribute(accessToken: accessToken, attributeName: "name", attributeValue : "abc") { (error, response) in
		guard let response = response, error == error else {
      return // an error has occurred
		}
    // attributes received as a Dictionary
  }
  ```
  {: codeblock}
  {: ph data-hd-programlang='swift'}

</br>

## Accès aux attributs personnalisés
{: #accessing-custom-attributes}

Selon votre configuration, les attributs sont chiffrés et enregistrés dans le cadre d'un profil utilisateur lorsqu'un utilisateur interagit avec votre application. L'interaction peut être un utilisateur qui se connecte ou définit une préférence dans votre application. Pour accéder aux attributs, vous pouvez transmettre un jeton d'accès via une méthode d'API. Lorsqu'aucun jeton d'accès n'est explicitement transmis, {{site.data.keyword.appid_short_notm}} utilise le dernier jeton reçu.
{: shortdesc}

iOS Swift :
{: ph data-hd-programlang='swift'}

  ```
  func setAttribute(key: String, value: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func setAttribute(key: String, value: String, accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)

  func getAttribute(key: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func getAttribute(key: String, accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)

  func getAttributes(completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func getAttributes(accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)

  func deleteAttribute(key: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func deleteAttribute(key: String, accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  ```
  {: codeblock}
  {: ph data-hd-programlang='swift'}

  ```
  void setAttribute(@NonNull String name, @NonNull String value, UserAttributeResponseListener listener);
  void setAttribute(@NonNull String name, @NonNull String value, @NonNull AccessToken accessToken, UserAttributeResponseListener listener);

  void getAttribute(@NonNull String name, UserAttributeResponseListener listener);
  void getAttribute(@NonNull String name, @NonNull AccessToken accessToken, UserAttributeResponseListener listener);

  void deleteAttribute(@NonNull String name, UserAttributeResponseListener listener);
  void deleteAttribute(@NonNull String name, @NonNull AccessToken accessToken, UserAttributeResponseListener listener);

  void getAllAttributes(@NonNull UserAttributeResponseListener listener);
  void getAllAttributes(@NonNull AccessToken accessToken, @NonNull UserAttributeResponseListener listener);
  ```
  {: codeblock}
  {: ph data-hd-programlang='java'}

  ```
  function getAllAttributes(accessTokenString) {}
	function getAttribute(accessTokenString, key) {}
	function setAttribute(accessTokenString, key, value) {}
	function deleteAttribute(accessTokenString, name) {}
  ```
  {: codeblock}
  {: ph data-hd-programlang='javascript'}

Swift côté serveur :
{: ph data-hd-programlang='swift'}

  ```
  func getAllAttributes(accessToken: String, completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  func getAttribute(accessToken: String, attributeName: String, completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  func setAttribute(accessToken: String, attributeName: String, attributeValue : "abc", completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  func deleteAllAttributes(accessToken: String, completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  ```
  {: codeblock}
  {: ph data-hd-programlang='swift'}

</br>

## Remarques sur la sécurité
{: #security-custom-attributes}

Avant de commencer à travailler avec des attributs personnalisés, assurez-vous de bien comprendre les considérations liées à la sécurité.

Par défaut, les attributs personnalisés sont modifiables et peuvent être mis à jour à l'aide d'un jeton d'accès {{site.data.keyword.appid_short_notm}} provenant d'une application client. Cela signifie que sans précautions appropriées, l'utilisateur ou l'application peut mettre à jour des attributs personnalisés immédiatement après la première connexion de l'utilisateur, à condition qu'il ait accès à un jeton d'accès. Cela peut potentiellement avoir des conséquences inattendues. Par exemple, un utilisateur peut changer son rôle d'utilisateur en administrateur, ce qui peut procurer des privilèges d'administration à des utilisateurs malveillants.

Pour empêcher vos utilisateurs de modifier les attributs que vous leur attribuez, définissez **Changer les attributs personnalisés via l'application** sur **Désactivé** dans l'onglet **Profils** du tableau de bord {{site.data.keyword.appid_short_notm}}. Par défaut, la valeur est **Activé**.
{: tip}

</br>

## Etapes suivantes
{: #next-custom-attributes}

Pour plus d'informations sur l'utilisation d'un logiciel SDK dans un langage spécifique, voir les référentiels GitHub suivants :

* <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">Logiciel SDK Android<img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>
* <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">Logiciel SDK iOS Swift<img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>
* <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">Logiciel SDK Node.js<img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>
* <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">Logiciel SDK Server Swift<img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>


Vous n'avez pas trouvé de logiciel SDK pour le langage dans lequel votre application est rédigée ? Pas de problème ! Vous pouvez intégrer le service à l'aide des API. {{site.data.keyword.appid_short_notm}} fournit une <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/" target="_blank">API REST <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> qui permet la connexion, anonyme ou après authentification, à un [fournisseur d'identité](/docs/services/appid?topic=appid-managing-idp) pris en charge. Pour obtenir de l'aide concernant l'implémentation de l'API dans des langages tels que Python et Go, <a href="https://www.ibm.com/blogs/bluemix/tag/app-id/" target="_blank">consultez nos blogues <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.
{: tip}
