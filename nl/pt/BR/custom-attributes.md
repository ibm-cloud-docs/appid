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

# Acessando atributos de usuário customizados
{: #custom}

Com o {{site.data.keyword.appid_full}}, é possível salvar e acessar atributos customizados.
{: shortdesc}

**Por que eu desejaria salvar atributos adicionais sobre um usuário?**

Os atributos são partes de informações sobre seus usuários. Ao salvá-los, é possível criar perfis sobre seus usuários
que permitem que você personalize sua experiência. Quanto mais atributos são incluídos em seus perfis, mais
personalizados podem ser seus aplicativos. Consulte este blog para ver como a criação de perfis de
usuário pode fazer a diferença: <a href="https://www.ibm.com/blogs/bluemix/2017/03/introducing-ibm-bluemix-app-id-authentication-profiles-service-app-developers/" target="_blank">Introduzindo o {{site.data.keyword.appid_short_notm}}<img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.

</br>

**Como os atributos são salvos?**

Dependendo de sua configuração, os atributos são criptografados e salvos como parte de um perfil do usuário quando um usuário interage com seu aplicativo. A
interação pode ser um usuário se conectando ou configurando uma preferência em seu aplicativo.

</br>

**Existe um limite para a quantidade de informações que podem ser armazenadas para cada usuário?**

É possível armazenar 100 KB de informações para cada usuário.

</br>

**Há alguma consideração de segurança que eu devo fazer?**

Por padrão, os atributos customizados são modificáveis e podem ser atualizados usando um token de acesso do {{site.data.keyword.appid_short_notm}} por meio de um aplicativo cliente. Isso
significa que, sem tomar precauções apropriadas, o usuário ou o aplicativo pode atualizar os atributos customizados
imediatamente após a primeira conexão do usuário, desde que ele tenha acesso a um token de acesso. Isso pode levar potencialmente a consequências indesejadas. Por
exemplo, um usuário poderia mudar a sua função de usuário para administrador, o que poderia expor privilégios
administrativos a usuários maliciosos.

Para evitar que seus usuários mudem os atributos que você dá a eles, configure **Mudar atributos
customizados do aplicativo** para **Desligado** na guia **Perfis** do painel do {{site.data.keyword.appid_short_notm}}. Por
padrão, ele é configurado como **Ligado**.
{: tip}

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

  Uso de exemplo:

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


## Acessando com a API
{: #api}

Não foi possível localizar um SDK para o idioma no qual seu aplicativo foi escrito? Sem problemas! É possível integrar o serviço usando as APIs.
{: shortdesc}

O {{site.data.keyword.appid_short_notm}} fornece uma
<a href="https://appid-profiles.ng.bluemix.net/swagger-ui/index.html#/Attributes" target="_blank">API de REST
<img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> que permite efetuar login, anonimamente ou
por meio de autenticação, com um [provedor de identidade](/docs/services/appid/manageidp.html)
suportado.
