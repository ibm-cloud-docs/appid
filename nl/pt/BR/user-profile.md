---

copyright:
  years: 2017, 2018
lastupdated: "2018-01-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# Acessando atributos do usuário
{: #user-profile}

É possível gerenciar dados do usuário final que podem ser usados para construir experiências de app personalizadas.
{:shortdesc}

Um atributo do usuário é um segmento de informações em uma entidade que são armazenadas e mantidas pelo {{site.data.keyword.appid_full}}. O perfil contém os atributos e a identidade de um usuário e pode ser anônimo ou vinculado a uma identidade gerenciada por um provedor de identidade.

O {{site.data.keyword.appid_short_notm}} fornece uma API para efetuar login, seja anonimamente, seja por autenticação com
[provedores de identidade](/docs/services/appid/identity-providers.html) OpenId Connect (OIDC). O terminal de API do atributo de perfil do usuário é um recurso protegido pelo token de acesso gerado pelo {{site.data.keyword.appid_short_notm}} durante o processo de login e de autorização.


## Armazenando, lendo e excluindo atributos do usuário
{: #storing-data}

O {{site.data.keyword.appid_short_notm}} fornece uma <a href="https://appid-profiles.ng.bluemix.net/swagger-ui/index.html#/Attributes" target="_blank">API de REST <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> para executar operações de criação, recuperação, atualização e exclusão em atributos do usuário. O serviço também fornece um SDK para <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">Android <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> e clientes móveis do <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">Swift <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.

## Acessando atributos do usuário com o SDK Android
{: #accessing}

Ao obter um token de acesso, é possível obter acesso ao terminal protegido de atributos do usuário. É possível obter acesso usando os métodos de API a seguir.

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
  {: codeblock}

Quando um token de acesso não for transmitido explicitamente, o {{site.data.keyword.appid_short_notm}} usará o último token recebido.

Por exemplo, é possível chamar o código a seguir para configurar um novo atributo ou substituir um existente.

  ```java
  appId.getUserAttributeManager().setAttribute(name, value, useThisToken,new UserAttributeResponseListener() {
		@Override
		public void onSuccess(JSONObject attributes) {
			//attributes received in JSON format on successful response
		}

		@Override
		public void onFailure(UserAttributesException e) {
			//Exception occurred
		}
	});
  ```
  {: codeblock}

### Login anônimo
{: #anonymous notoc}

Com o {{site.data.keyword.appid_short_notm}} é possível efetuar login [anonimamente](/docs/services/appid/user-profile.html#anonymous).

  ```java
  appId.loginAnonymously(getApplicationContext(), new AuthorizationListener() {
		@Override
		public void onAuthorizationFailure(AuthorizationException exception) {
			//Exception occurred
		}

		@Override
		public void onAuthorizationCanceled() {
			//Authentication canceled by the user
		}

		@Override
		public void onAuthorizationSuccess(AccessToken accessToken, IdentityToken identityToken) {
			//User authenticated
		}
	});
  ```
  {: codeblock}

### Autenticação progressiva
{: #progressive notoc}

Quando o usuário mantém um token de acesso anônimo, ele pode ser identificado passando-o para o método `loginWidget.launch`.

  ```java
  void launch (@NonNull final Activity activity, @NonNull final AuthorizationListener authorizationListener, String accessTokenString);
  ```
  {: codeblock}

Após um login anônimo, a autenticação progressiva ocorrerá mesmo se o widget de login for chamado sem passar um token de acesso porque o serviço usou o último
token recebido. Se desejar limpar os tokens armazenados, execute o comando a seguir.

  ```java
  	appIDAuthorizationManager = new AppIDAuthorizationManager(this.appId);
  appIDAuthorizationManager.clearAuthorizationData();
  ```
  {: codeblock}


## Acessando atributos do usuário com o SDK iOS
{: #accessing}

Ao obter um token de acesso, é possível obter acesso ao terminal protegido de atributos do usuário. Isso é feito usando os métodos de API a seguir.

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
  {: codeblock}

Quando um token de acesso não for transmitido explicitamente, o {{site.data.keyword.appid_short_notm}} usará o último token recebido.

Por exemplo, é possível chamar o código a seguir para configurar um novo atributo ou substituir um existente.

  ```swift
  AppID.sharedInstance.userAttributeManager?.setAttribute("key", "value", completionHandler: { (error, result) in
      if error = nil {
          //Attributes recieved as a Dictionary
      } else {
          // An error has occurred
      }
  })
  ```
  {: codeblock}


### Login anônimo
{: #anonymous notoc}

Com o {{site.data.keyword.appid_short_notm}} é possível efetuar login [anonimamente](/docs/services/appid/user-profile.html#anonymous).

  ```swift
  class delegate : AuthorizationDelegate {

      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, response:Response?) {
          //User authenticated
      }

      public func onAuthorizationCanceled() {
          //Authentication canceled by the user
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          //Error occurred
      }
   }

  AppID.sharedInstance.loginAnonymously( authorizationDelegate: delegate())
  ```
  {: codeblock}

### Autenticação progressiva
{: #progressive notoc}

Quando você retém um token de acesso anônimo, o usuário pode se tornar um usuário identificado passando-o para o método `loginWidget.launch`.

  ```swift
  func launch(accessTokenString: String? , delegate: AuthorizationDelegate)
  ```
  {: codeblock}

Após um login anônimo, a autenticação progressiva ocorrerá mesmo se o widget de login for chamado sem passar um token de acesso porque o serviço usou o último
token recebido. Se desejar limpar os tokens armazenados, execute o comando a seguir.

  ```swift
  var appIDAuthorizationManager = AppIDAuthorizationManager(appid: AppID.sharedInstance)
  appIDAuthorizationManager.clearAuthorizationData()
  ```
  {: codeblock}

## Separação e criptografia de dados
{: #data}

O {{site.data.keyword.appid_short_notm}} armazena e criptografa atributos de perfil do usuário. Como um serviço de múltiplos locatários, cada locatário
tem uma chave de criptografia designada e os dados do usuário em cada locatário são criptografados com apenas essa chave do locatário.

O {{site.data.keyword.appid_short_notm}} assegura que as informações privadas sejam criptografadas antes de serem armazenadas.
