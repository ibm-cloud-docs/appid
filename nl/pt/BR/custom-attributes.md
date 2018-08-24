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

# Acessando atributos de usuário customizados
{: #custom}

Ao obter um token de acesso, é possível obter acesso ao terminal protegido de atributos do usuário.
{: shortdesc}

O {{site.data.keyword.appid_short_notm}} fornece uma API de REST do <a href="https://appid-profiles.ng.bluemix.net/swagger-ui/index.html#/Attributes" target="_blank"><img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> que permite efetuar login, anonimamente ou por meio de autenticação, com um [provedor de identidade](/docs/services/appid/identity-providers.html) suportado. O terminal de API é um recurso protegido pelo token de acesso que é gerado pelo {{site.data.keyword.appid_short_notm}} durante o processo de login e de autorização.

</br>

## Acessando com o SDK do iOS
{: #ios}

 É possível acessar atributos customizados passando um token de acesso por meio dos métodos de API a seguir.

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

Quando um token de acesso não for transmitido explicitamente, o {{site.data.keyword.appid_short_notm}} usará o último token recebido.

Por exemplo, é possível chamar o código a seguir para configurar um novo atributo ou substituir um existente.

  ```swift
	AppID.sharedInstance.userProfileManager?.setAttribute("key", "value") { (error, result) in
		guard let result = result, error == nil else {
	  		return // um erro ocorreu 	}
		// attributes recieved as a Dictionary
	})
  ```
  {: pre}

  Para obter mais informações sobre como trabalhar no iOS Swift, verifique o SDK do <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank"><img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.
  {: tip}

</br>


## Acessando com o Android SDK
{: #android}

É possível acessar atributos customizados passando um token de acesso por meio dos métodos de API a seguir.

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

Quando um token de acesso não for transmitido explicitamente, o {{site.data.keyword.appid_short_notm}} usará o último token recebido.

Por exemplo, é possível chamar o código a seguir para configurar um novo atributo ou substituir um existente.

```java
appId.getUserProfileManager ().setAttribute (name, value, useThisToken, new UserProfileResponseListener () {
	@Override
		public void onSuccess(JSONObject attributes) {
		//attributes received in JSON format on successful response
		}

	@Override
		public void onFailure(UserAttributesException e) {
		// exception occurred }
});
```
{: pre}

Para obter mais informações sobre como trabalhar no Android, consulte o SDK do <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank"><img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.
{: tip}

</br>

## Acessando com o SDK do servidor Swift
{: #swift}

É possível acessar atributos customizados passando um token de acesso por meio dos métodos de API a seguir.

  ```swift
  func getAllAttributes(accessToken: String, completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  func getAttribute(accessToken: String, attributeName: String, completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  func setAttribute(accessToken: String, attributeName: String, attributeValue : "abc", completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  func deleteAllAttributes(accessToken: String, completionHandler: (Swift.Error?, [String: Any]?) -> Void)
  ```
  {: pre}

  Exemplo de Uso:

  ```swift

	let userProfileManager = UserProfileManager(options: options)
	let accesstoken = "access token"

	userProfileManager.setAttribute(accessToken: accessToken, attributeName: "name", attributeValue : "abc") { (error, response) in
		guard let response = response, error == error else {
			return // um erro ocorreu 	}
		// attributes recieved as a Dictionary
	}
  ```

  {: pre}

  Para obter mais informações sobre como trabalhar no SDK do servidor Swift, consulte o SDK do <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank"><img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.
  {: tip}

</br>

## Acessando com o SDK do servidor Node.js
{: #node}

É possível acessar atributos customizados passando um token de acesso por meio dos métodos de API a seguir.

  ```javascript
	function getAllAttributes(accessTokenString) {}
	function getAttribute(accessTokenString, key) {}
	function setAttribute(accessTokenString, key, value) {}
	function deleteAttribute(accessTokenString, name) {}
  ```
  {: pre}

  Uso de exemplo:

  ```javascript

	const userProfileManager = require ("ibmcloud-appid"). UserProfileManager; userProfileManager; userProfileManager.init ();

	var accessToken = req.session [ WebAppStrategy.AUTH_CONTEXT ] .accessToken;

	userProfileManager.setAttribute(accessToken, name, value).then(function (attributes) {
		// attributes returned as dictionary
	});
  ```
  {: pre}

  Para obter mais informações sobre como trabalhar no SDK do servidor Node.js, consulte o <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">SDK <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"> </a>.
  {: tip}



