---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:tip: .tip}

# Gestión de la experiencia de inicio de sesión
{: #branding}

Puede mostrar sus propias pantallas personalizadas y aprovechar las posibilidades de autenticación y autorización de {{site.data.keyword.appid_full}}. Con el directorio en la nube como proveedor de identidad, sus usuarios pueden interactuar con su app requiriendo menos ayuda. Pueden iniciar la sesión sin necesidad de solicitar ayuda.
{: shortdesc}

Cuando utilice sus propias pantallas, se utiliza el [flujo de ROPC (credenciales de contraseña de propietario de recurso)](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html).


## Visualización de pantallas personalizadas con el SDK de Android
{: #branded-ui-android}

Con el directorio en la nube habilitado, puede llamar a pantallas personalizadas con el SDK de Android. <a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="blank">Visite este blog <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>
{: shortdesc}

</br>
**Iniciar la sesión**

1. Establezca **Directorio en la nube** en **Activado** como proveedor de identidad.
2. Añada el mandato siguiente a su código.
  ```java
  AppID.getInstance().obtainTokensWithROP(getApplicationContext(), username, password,
         new TokenResponseListener() {
         @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
             //Se ha producido una excepción
        }

          @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
            //Usuario autenticado
        }
         });
  ```
  {: pre}

</br>
</br>

## Visualización de pantallas personalizadas con el SDK de iOS Swift
{: #branded-ui-ios-swift}

Con el directorio en la nube habilitado, puede llamar a pantallas personalizadas con el SDK de Swift de iOS.
{: shortdesc}

</br>
**Iniciar la sesión**

1. En el separador de proveedor de identidad de la GUI, establezca el directorio en la nube en **Activado**.
2. Inicie la sesión utilizando la contraseña del propietario del recurso. Las señales de acceso e identidad se obtienen cuando un usuario intenta iniciar sesión utilizando su nombre de usuario y contraseña.
  ```swift
  class delegate : TokenResponseDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
      //Usuario autenticado
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
      //Se ha producido una excepción
        }
  }

  AppID.sharedInstance.obtainTokensWithROP(username: username, password: password, delegate: delegate())
  ```
  {: pre}


</br>
</br>

## Visualización de pantallas personalizadas con el SDK de Node.js
{: #branded-ui-nodejs}

Con el directorio en la nube habilitado, puede llamar a pantallas personalizadas con el SDK de Node.js. 
{: shortdesc}

**Iniciar la sesión**
1. Establezca el directorio en la nube en **Activado** en los valores de proveedor de identidad y especifique un punto final de devolución de llamada.
2. Añada una ruta de envío a su app a la que pueda llamarse con los parámetros de nombre de usuario y contraseña e inicie la sesión utilizando la contraseña del propietario del recurso.
    ```javascript
    app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
    	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true //permitir mensajes flash
  }));
    ```
    {: pre}
    `WebAppStrategy` permite a los usuarios iniciar sesión en sus apps web con un nombre de usuario y una contraseña. Después de un inicio de sesión satisfactorio, la señal de acceso de un usuario se almacena en la sesión HTTP y está disponible durante la sesión. Cuando la sesión HTTP se ha destruido o ha caducado, la señal deja de ser válida.
    {: tip}

