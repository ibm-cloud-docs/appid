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

# Atributos de usuario personalizados
{: #custom-attributes}

Con {{site.data.keyword.appid_full}}, podrá guardar, acceder y actualizar atributos personalizados.
{: shortdesc}


## Establecimiento de atributos
{: #setting-custom-attributes}

Puede establecer los roles y los ámbitos que se conocen como atributos para un perfil de usuario. También puede sustituirlos atributos existentes que se hayan extraído de un proveedor de identidad externo.
{: shortdesc}


Los atributos son partes de información de los usuarios. A guardarlos, puede crear perfiles sobre sus usuarios que le permitan personalizar su experiencia. Cuantos más atributos se añadan al perfil, más se podrá personalizar la experiencia de la app. Consulte este blog para ver cómo la creación de los perfiles de usuario puede marcar la diferencia <a href="https://www.ibm.com/blogs/bluemix/2017/03/introducing-ibm-bluemix-app-id-authentication-profiles-service-app-developers/" target="blank">Introducción de {{site.data.keyword.appid_short_notm}}<img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.


Puede almacenar hasta 100 KB de información de cada usuario.
{: note}


**Para establecer un atributo:**

Todas las solicitudes entrantes a la app tienen la cabecera de autorización, con `access_token`. Puede utilizar `access_token` para realizar solicitudes a los puntos finales de atributos personalizados con uno de los SDK proporcionados o utilizando las [API de atributos](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Attributes).


Swift de iOS:
{: ph data-hd-programlang='swift'}

  ```
	AppID.sharedInstance.userProfileManager?.setAttribute("key", "value") { (error, result) in
		guard let result = result, error == nil else {
	  		return //se ha producido un error
		}
		//atributos recibidos como diccionario
	})
  ```
  {: codeblock}
  {: ph data-hd-programlang='swift'}

  ```
  appId.getUserProfileManager().setAttribute(name, value, useThisToken, new UserProfileResponseListener() {
  	@Override
		public void onSuccess(JSONObject attributes) {
  		//atributos recibidos en formato JSON con una respuesta satisfactoria
		}

  	@Override
		public void onFailure(UserAttributesException e) {
  		//se ha producido una excepción
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
		//atributos devueltos como diccionario
	});
  ```
  {: codeblock}
  {: ph data-hd-programlang='javascript'}

Swift de servidor:
{: ph data-hd-programlang='swift'}

  ```
  let userProfileManager = UserProfileManager(options: options)
	let accesstoken = "access token"

  userProfileManager.setAttribute(accessToken: accessToken, attributeName: "name", attributeValue : "abc") { (error, response) in
		guard let response = response, error == error else {
      return //se ha producido un error
		}
    //atributos recibidos como diccionario
	}
  ```
  {: codeblock}
  {: ph data-hd-programlang='swift'}

</br>

## Acceso a atributos personalizados
{: #accessing-custom-attributes}

En función de la configuración, los atributos se cifran y guardan como parte el perfil de usuario cuando este interactúa con la aplicación. La interacción puede ser, por ejemplo, un usuario iniciando sesión o estableciendo una preferencia en la app. Para acceder a los atributos, puede pasar una señal de acceso a través de un método de API. Si no se ha aprobado explícitamente una señal de acceso, {{site.data.keyword.appid_short_notm}} utiliza la última señal recibida.
{: shortdesc}

Swift de iOS:
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

Swift del lado del servidor:
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

## Consideraciones sobre seguridad
{: #security-custom-attributes}

Antes de empezar a trabajar con atributos personalizados, asegúrese de que comprende las consideraciones de seguridad.

De forma predeterminada, es posible modificar y actualizar los atributos mediante la señal de acceso de {{site.data.keyword.appid_short_notm}} desde una aplicación de cliente. Esto significa que si no se toman las precauciones adecuadas, el usuario o la aplicación pueden actualizar atributos personalizados inmediatamente tras el inicio de sesión del primer usuario, siempre que tengan acceso a una señal de acceso. Esto puede provocar consecuencias no deseadas. Por ejemplo, un usuario podría cambiar el rol de usuario a administrador, lo que podría exponer privilegios administrativos a usuarios malintencionados.

Para evitar que los usuarios cambien los atributos que les proporciona, establezca **Cambiar los atributos personalizados de la app** en **Desactivado** en el separador **Perfiles** del panel de control de {{site.data.keyword.appid_short_notm}}. De forma predeterminada, se establece en **Activado**.
{: tip}

</br>

## Pasos siguientes
{: #next-custom-attributes}

Para obtener más información sobre cómo trabajar con un SDK de lenguaje específico, consulte los siguientes repositorios de GitHub:

* <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">SDK de Android <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>
* <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">SDK de Swift de iOS <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>
* <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">SDK de Node.js <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>
* <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">SDK de Swift de servidor <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>


¿No ha encontrado un SDK para el idioma en el que está escrita su app? No hay ningún problema. Puede integrar el servicio utilizando las API. {{site.data.keyword.appid_short_notm}} proporciona una <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/" target="_blank">API REST <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> que permite el inicio de sesión, de forma anónima o mediante autenticación, con un [proveedor de identidad](/docs/services/appid?topic=appid-managing-idp) admitido. Para obtener ayuda para implementar la API en lenguajes como Python y Go, <a href="https://www.ibm.com/blogs/bluemix/tag/app-id/" target="_blank">consulte nuestros blogs <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.
{: tip}
