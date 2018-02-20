---

copyright:
  years: 2017, 2018
lastupdated: "2018-01-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# Acceso a los atributos de usuario
{: #user-profile}

Puede gestionar los datos de usuario final que puede utilizar para construir experiencias de app personalizadas.
{:shortdesc}

Un atributo de usuario es un segmento de información en una entidad que {{site.data.keyword.appid_full}} almacena y mantiene. El perfil contiene los atributos y la identidad de un usuario y puede ser anónimo o bien estar vinculado a una identidad gestionada por un proveedor de identidad.

{{site.data.keyword.appid_short_notm}} proporciona una API para iniciar sesión, ya sea de forma anónima o autenticándose con [proveedores de identidad](/docs/services/appid/identity-providers.html) OpenId Connect (OIDC). El punto final de API de atributos de perfil de usuario es un recurso protegido por una señal de acceso, que genera {{site.data.keyword.appid_short_notm}} durante el proceso de inicio de sesión y autorización.


## Cómo almacenar, leer y suprimir atributos de usuario
{: #storing-data}

{{site.data.keyword.appid_short_notm}} proporciona una <a href="https://appid-profiles.ng.bluemix.net/swagger-ui/index.html#/Attributes" target="_blank">API REST <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> para realizar operaciones de creación, recuperación, actualización y supresión en los atributos de usuario. El servicio también proporciona un SDK para los clientes de dispositivos móviles <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">Android <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> y <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">Swift <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.

## Acceder a los atributos de usuario con el SDK de Android
{: #accessing}

Cuando obtenga una señal de acceso, es posible obtener acceso al punto final de los atributos protegidos del usuario. Puede obtener acceso utilizando los siguientes métodos de la API.

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

Cuando no se haya aprobado explícitamente una señal de acceso, {{site.data.keyword.appid_short_notm}} utilizará la última señal recibida.

Por ejemplo, puede llamar al código siguiente para establecer un atributo nuevo, o para alterar temporalmente uno existente.

  ```java
  appId.getUserAttributeManager().setAttribute(name, value, useThisToken,new UserAttributeResponseListener() {
		@Override
		public void onSuccess(JSONObject attributes) {
			//atributos recibidos en formato JSON con una respuesta satisfactoria
		}

		@Override
		public void onFailure(UserAttributesException e) {
			//Se ha producido una excepción
		}
	});
  ```
  {: codeblock}

### Inicio de sesión anónimo
{: #anonymous notoc}

Con {{site.data.keyword.appid_short_notm}}, puede iniciar sesión [de forma anónima](/docs/services/appid/user-profile.html#anonymous).

  ```java
  appId.loginAnonymously(getApplicationContext(), new AuthorizationListener() {
		@Override
		public void onAuthorizationFailure(AuthorizationException exception) {
			//Se ha producido una excepción
		}

		@Override
		public void onAuthorizationCanceled() {
			//Autenticación cancelada por el usuario
		}

		@Override
		public void onAuthorizationSuccess(AccessToken accessToken, IdentityToken identityToken) {
			//Usuario autenticado
		}
	});
  ```
  {: codeblock}

### Autenticación progresiva
{: #progressive notoc}

Cuando el usuario contiene una señal de acceso anónimo, puede ser identificado pasándola al método `loginWidget.launch`.

  ```java
  void launch (@NonNull final Activity activity, @NonNull final AuthorizationListener authorizationListener, String accessTokenString);
  ```
  {: codeblock}

Tras un inicio de sesión anónimo, se producirá la autenticación progresiva, aunque se invoque el widget de inicio de sesión sin pasar una señal de acceso porque el servicio ha utilizado la última señal recibida. Si desea borrar las señales almacenadas, ejecute el siguiente mandato.

  ```java
  	appIDAuthorizationManager = new AppIDAuthorizationManager(this.appId);
  appIDAuthorizationManager.clearAuthorizationData();
  ```
  {: codeblock}


## Acceder a los atributos de usuario con el SDK de iOS
{: #accessing}

Cuando obtenga una señal de acceso, es posible obtener acceso al punto final de los atributos protegidos del usuario. Esta operación se realiza mediante los siguientes métodos de la API.

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

Cuando no se haya aprobado explícitamente una señal de acceso, {{site.data.keyword.appid_short_notm}} utilizará la última señal recibida.

Por ejemplo, puede llamar al código siguiente para establecer un atributo nuevo, o para alterar temporalmente uno existente.

  ```swift
  AppID.sharedInstance.userAttributeManager?.setAttribute("key", "value", completionHandler: { (error, result) in
      if error = nil {
          //Atributos recibidos como un diccionario
      } else {
          // Se ha producido un error
      }
  })
  ```
  {: codeblock}


### Inicio de sesión anónimo
{: #anonymous notoc}

Con {{site.data.keyword.appid_short_notm}}, puede iniciar sesión [de forma anónima](/docs/services/appid/user-profile.html#anonymous).

  ```swift
  class delegate : AuthorizationDelegate {

      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, response:Response?) {
          //Usuario autenticado
      }

      public func onAuthorizationCanceled() {
          //Autenticación cancelada por el usuario
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          //Se ha producido un error
      }
   }

  AppID.sharedInstance.loginAnonymously( authorizationDelegate: delegate())
  ```
  {: codeblock}

### Autenticación progresiva
{: #progressive notoc}

Cuando alberga una señal de acceso anónimo, el usuario puede convertirse en un usuario identificado si lo pasa al método `loginWidget.launch`.

  ```swift
  func launch(accessTokenString: String? , delegate: AuthorizationDelegate)
  ```
  {: codeblock}

Tras un inicio de sesión anónimo, se producirá la autenticación progresiva, aunque se invoque el widget de inicio de sesión sin pasar una señal de acceso porque el servicio ha utilizado la última señal recibida. Si desea borrar las señales almacenadas, ejecute el siguiente mandato.

  ```swift
  var appIDAuthorizationManager = AppIDAuthorizationManager(appid: AppID.sharedInstance)
  appIDAuthorizationManager.clearAuthorizationData()
  ```
  {: codeblock}

## Separación y cifrado de datos
{: #data}

{{site.data.keyword.appid_short_notm}} almacena y cifra atributos de perfil de usuario. Como servicio multiarrendatario, cada arrendatario tiene una clave de cifrado designada y los datos de usuario de cada uno se cifran únicamente con la clave de dicho arrendatario.

{{site.data.keyword.appid_short_notm}} garantiza que la información privada se cifre antes de que se almacene.
