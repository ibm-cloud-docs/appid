---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:pre: .pre}
{:tip: .tip}
{:screen: .screen}

# Acceso a información de usuario predefinida
{: #predefined}

Puede ver información específica del proveedor de identidad sobre los usuarios.
{: shortdesc}


## Acceso con el SDK de iOS
{: #ios}

Si las nuevas señales no se pasan de forma explícita al SDK, {{site.data.keyword.appid_short_notm}} utiliza las últimas señales recibidas para recuperar y validar la respuesta. Por ejemplo, puede ejecutar el código siguiente tras una autenticación satisfactoria y el SDK recuperará información adicional sobre el usuario.

```
AppID.sharedInstance.userProfileManager.getUserInfo { (error: Error?, userInfo: [String: Any]?) in
	guard let userInfo = userInfo, err == nil {
		return //se ha producido un error
		}
	//información de usuario recuperada correctamente
}

```
{: pre}

Como alternativa, puede pasar de forma explícita las señales de acceso y de identidad. La señal de identidad es opcional, pero cuando se pasa, se utiliza para validar la respuesta de información de usuario.

```
AppID.sharedInstance.userProfileManager.getUserInfo(accessToken: String, identityToken: String?) { (error: Error?, userInfo: [String: Any]?) in
	guard let userInfo = userInfo, err == nil {
		return //se ha producido un error
		}
	//información de usuario recuperada correctamente
}
```
{: pre}

</br>

## Acceso con el SDK de Android
{: #android}

Si las nuevas señales no se pasan de forma explícita al SDK, {{site.data.keyword.appid_short_notm}} utiliza las últimas señales recibidas para recuperar y validar la respuesta. Por ejemplo, puede ejecutar el código siguiente tras una autenticación satisfactoria y el SDK recuperará información adicional sobre el usuario.

```
AppID appId = AppID.getInstance();

appId.getUserProfileManager().getUserInfo(new UserProfileResponseListener() {
	@Override
	public void onSuccess(JSONObject userInfo) {
		//información de usuario recuperada correctamente
}

	@Override
	public void onFailure(UserInfoException e) {
		//se ha producido una excepción
	}
});
```
{: pre}

Como alternativa, puede pasar de forma explícita las señales de acceso y de identidad. La señal de identidad es opcional, pero cuando se pasa, se utiliza para validar la respuesta de información de usuario.

```
AppID appId = AppID.getInstance();

appId.getUserProfileManager().getUserInfo(accessToken, identityToken, new UserProfileResponseListener() {
	@Override
	public void onSuccess(JSONObject userInfo) {
		//atributo "name" recuperado correctamente
	}

	@Override
	public void onFailure(UserInfoException e) {
		//se ha producido una excepción
	}
});
```
{: pre}

</br>

## Acceso con el SDK del servidor de Node.js
{: #node}


Mediante el uso de un SDK del lado del servidor, puede recuperar información adicional sobre los usuarios. Puede llamar al método siguiente utilizando las señales de acceso y de identidad almacenadas, o puede pasar de forma explícita las señales. La señal de identidad es opcional, pero cuando se pasa, se utiliza para validar la respuesta de información de usuario.


```javascript
let userProfileManager = UserProfileManager(options: options)

let accessToken = req.session[WebAppStrategy.AUTH_CONTEXT].accessToken;
let identityToken = req.session[WebAppStrategy.AUTH_CONTEXT].identityToken;


//Recuperar información de usuario y validarla con la señal de identidad determinada
userProfileManager.getUserInfo(accessToken, identityToken).then(function (profile) {
	//información de usuario recuperada correctamente
});

//Recuperar información de usuario sin validación
userProfileManager.getUserInfo(accessToken).then(function (profile) {
	//información de usuario recuperada correctamente
});
```
{: pre}

</br>

## Acceso con el SDK del servidor de Swift
{: #swift}

Mediante el uso de un SDK del lado del servidor, puede recuperar información adicional sobre los usuarios. Puede llamar al método siguiente utilizando las señales de acceso y de identidad almacenadas, o puede pasar de forma explícita las señales. La señal de identidad es opcional, pero cuando se pasa, se utiliza para validar la respuesta de información de usuario.


```swift
let userProfileManager = UserProfileManager(options: options)

let accessToken = "<access token>"
let identityToken = "<identity token>"

//Si se proporciona la señal de identidad (enfoque recomendado), la respuesta se valida con la señal de identidad
userProfileManager.getUserInfo(accessToken: accessToken, identityToken: identityToken) { (err, userInfo) in
	guard let userInfo = userInfo, err == nil {
		return //se ha producido un error
		}
	//información de usuario recuperada correctamente
}

//Recuperar la información de usuario sin validación
userProfileManager.getUserInfo(accessToken: accessToken) { (err, userInfo) in
	guard let userInfo = userInfo, err == nil {
		return //se ha producido un error
		}
	//información de usuario recuperada correctamente
}
```
{: pre}

</br>

## Acceso con la API
{: #api}

Puede ver información adicional a través del punto final `/userinfo`.

1. Asegúrese de que tiene una señal de acceso válida con un alcance `openid`. Puede verificar que la señal es válida mediante el punto final `/introspect`.

2. Realice una solicitud al punto final `/userinfo`.
  ```
  GET [POST] https://{oauth-server-endpoint}/userinfo
  Authorization: 'Bearer {ACCESS_TOKEN}'
  ```
  {: pre}

  Resultado de ejemplo:
  ```
  "sub": "cad9f1d4-e23b-3683-b81b-d1c4c4fd7d4c",
  "name": "John Doe",
  "email": "john.doe@gmail.com",
  "picture": "https://lh3.googleusercontent.com/-XdUIqdbhg/AAAAAAAAI/AAAAAAA/42rbcbv5M/photo.jpg",
  "gender": "male",
  "locale": "en",
  "identities": [
      {
          "provider": "google",
          "id": "104560903311317789798",
          "profile": {
              "id": "104560903311317789798",
              "email": "john.doe@gmail.com",
              "verified_email": true,
              "name": "John Doe",
              "given_name": "John",
              "family_name": "Doe",
              "link": "https://plus.google.com/104560903311317789798",
              "picture": "https://lh3.googleusercontent.com/-XdUIqdbhg/AAAAAAAAI/AAAAAAA/42rbcbv5M/photo.jpg",
              "gender": "male",
              "locale": "en",
              "idpType": "google"
          }
      }
  ]
  ```
  {: screen}

3. Verifique que la reclamación `sub` coincida exactamente con la reclamación `sub` en la señal de identidad. Si no coinciden, no utilice la información devuelta. Para obtener más información sobre la sustitución de señales, consulte la <a href="http://openid.net/specs/openid-connect-core-1_0.html#TokenSubstitution" target="__blank">especificación de OIDC <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.

Si un proveedor de identidad externo hace algún cambio, puede obtener la información actualizada cuando el usuario vuelva a iniciar sesión. Las nuevas señales recuperan los datos más actualizados.
{: tip}
