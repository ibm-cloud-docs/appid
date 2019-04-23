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

# Atributos do usuário customizados
{: #custom-attributes}

Com o {{site.data.keyword.appid_full}}, é possível salvar, acessar e atualizar atributos customizados.
{: shortdesc}


## Configurando atributos
{: #setting-custom-attributes}

É possível configurar funções e escopos que são conhecidos como atributos para um perfil do usuário. Também é possível substituir os atributos existentes que podem ter sido extraídos de um provedor de identidade externo.
{: shortdesc}


Os atributos são partes de informações sobre seus usuários. Ao salvá-los, é possível criar perfis sobre seus usuários
que permitem que você personalize sua experiência. Quanto mais atributos são incluídos em seu perfil, mais personalizado a experiência do aplicativo pode ser. Consulte este blog para ver como a criação de perfis de
usuário pode fazer a diferença: <a href="https://www.ibm.com/blogs/bluemix/2017/03/introducing-ibm-bluemix-app-id-authentication-profiles-service-app-developers/" target="blank">Introduzindo o {{site.data.keyword.appid_short_notm}}<img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.


É possível armazenar 100 KB de informações para cada usuário.
{: note}


**Para configurar um atributo:**

Todas as solicitações recebidas para seu app têm o cabeçalho Autorização, com `access_token`. É possível usar `access_token`para fazer solicitações para os terminais de atributos customizados com um dos SDKs fornecidos ou usando [as APIs de atributos](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Attributes).


iOS Swift:
{: ph data-hd-programlang='swift'}

  ```
	AppID.sharedInstance.userProfileManager?.setAttribute("key", "value") { (error, result) in
		guard let result = result, error == nil else {
	  		return // um erro ocorreu 	}
		// attributes recieved as a Dictionary
	})
  ```
  {: codeblock}
  {: ph data-hd-programlang='swift'}

  ```
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
  {: codeblock}
  {: ph data-hd-programlang='java'}

  ```
	const userProfileManager = require ("ibmcloud-appid"). UserProfileManager; userProfileManager; userProfileManager.init ();

	var accessToken = req.session [ WebAppStrategy.AUTH_CONTEXT ] .accessToken;

	userProfileManager.setAttribute(accessToken, name, value).then(function (attributes) {
		// attributes returned as dictionary
	});
  ```
  {: codeblock}
  {: ph data-hd-programlang='javascript'}

Servidor Swift:
{: ph data-hd-programlang='swift'}

  ```
  let userProfileManager = UserProfileManager(options: options)
	let accesstoken = "access token"

  userProfileManager.setAttribute(accessToken: accessToken, attributeName: "name", attributeValue : "abc") { (error, response) in
		guard let response = response, error == error else {
      return // um erro ocorreu 	}
    // atributos recebidos como um Dicionário
  }
  ```
  {: codeblock}
  {: ph data-hd-programlang='swift'}

</br>

## Acessando atributos customizados
{: #accessing-custom-attributes}

Dependendo de sua configuração, os atributos são criptografados e salvos como parte de um perfil do usuário quando um usuário interage com seu aplicativo. A
interação pode ser um usuário se conectando ou configurando uma preferência em seu aplicativo. Para acessar os atributos, é possível passar um token de acesso por meio de um método da API. Se um token de acesso não for passado explicitamente, o {{site.data.keyword.appid_short_notm}} usará o token recebido pela última vez.
{: shortdesc}

iOS Swift:
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

Swift do lado do servidor:
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

## Considerações de segurança
{: #security-custom-attributes}

Antes de começar a trabalhar com atributos customizados, certifique-se de entender as considerações de segurança.

Por padrão, os atributos customizados são modificáveis e podem ser atualizados usando um token de acesso do {{site.data.keyword.appid_short_notm}} por meio de um aplicativo cliente. Isso
significa que, sem tomar precauções apropriadas, o usuário ou o aplicativo pode atualizar os atributos customizados
imediatamente após a primeira conexão do usuário, desde que ele tenha acesso a um token de acesso. Isso pode levar potencialmente a consequências indesejadas. Por exemplo, um usuário pode mudar a sua função de usuário para administrador, o que pode expor privilégios administrativos a usuários maliciosos.

Para evitar que seus usuários mudem os atributos que você dá a eles, configure **Mudar atributos
customizados do aplicativo** para **Desligado** na guia **Perfis** do painel do {{site.data.keyword.appid_short_notm}}. Por
padrão, ele é configurado como **Ligado**.
{: tip}

</br>

## Próximas Etapas
{: #next-custom-attributes}

Para obter mais informações sobre como trabalhar com um SDK de linguagem específico, consulte os repositórios GitHub a seguir:

* <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">Android SDK <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>
* <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">iOS Swift SDK <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>
* <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">Node.js SDK <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>
* <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">Server Swift SDK <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>


Não foi possível localizar um SDK para o idioma no qual seu aplicativo foi escrito? Sem problemas! É possível integrar o serviço usando as APIs. O {{site.data.keyword.appid_short_notm}} fornece uma
<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/" target="_blank">API de REST
<img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> que permite efetuar login, anonimamente ou
por meio de autenticação, com um [provedor de identidade](/docs/services/appid?topic=appid-managing-idp)
suportado. Para ajudar a implementar a API em linguagens, como a Python e a Go, <a href="https://www.ibm.com/blogs/bluemix/tag/app-id/" target="_blank">consulte nossos blogs <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.
{: tip}
