---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Gestión de la experiencia de inicio de sesión
{: #branding}

Puede mostrar su propia IU personalizada y al mismo tiempo aprovechar las capacidades de autenticación y autorización de {{site.data.keyword.appid_full}}. Con el directorio en la nube como proveedor de identidad, sus usuarios pueden interactuar con su app requiriendo menos ayuda. Pueden iniciar la sesión, registrarse, cambiar su contraseña y más sin necesidad de solicitar ayuda.
{: shortdesc}

Con el directorio en la nube como proveedor de identidad, se utiliza el [flujo ROPC (credenciales de contraseña de propietario de recurso)](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html) para proporcionar señales de acceso e identidad.

**Nota**: Solo puede utilizar páginas de inicio de sesión personalizadas si el directorio en la nube es la única opción configurada. Si tiene otros proveedores de identidad **activados**, se mostrará la pantalla de inicio de sesión preconfigurada.

## Visualización de pantallas personalizadas con el SDK de Android
{: #branded-ui-android}

Con el directorio en la nube habilitado, puede llamar a pantallas personalizadas con el SDK de Android. Puede elegir la combinación de las pantallas con que desea que sus usuarios puedan interactuar. <a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="blank">Visite nuestro blog <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>
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
        public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
            //Usuario autenticado
        }
         });
  ```
  {: codeblock}

</br>
**Registrarse**

1. Establezca **Permitir a los usuarios registrarse y restablecer su contraseña** en **Activado** en los valores del directorio en la nube.
2. Llame al LoginWidget para iniciar el flujo de registro.
  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
 loginWidget.launchSignUp(this, new AuthorizationListener() {
  		 @Override
          public void onAuthorizationFailure (AuthorizationException exception) {
          }

  		 @Override
          public void onAuthorizationCanceled () {
          }

  		 @Override
  		 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
  			 if (accessToken != null && identityToken != null) {
  			 } else {
  			 }

  		 }
  	 });
  ```
  {: codeblock}

</br>
**Contraseña olvidada**

1. Establezca **Permitir a los usuarios registrarse y restablecer su contraseña** y **Correo electrónico de contraseña olvidada** en **Activado** en los valores del directorio en la nube.
2. Llame al LoginWidget para iniciar el flujo de contraseña olvidada.
    ```java
    LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launchForgotPassword(this, new AuthorizationListener() {
   			 @Override
          public void onAuthorizationFailure (AuthorizationException exception) {
          }

   			 @Override
          public void onAuthorizationCanceled () {
          }

   			 @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
          }
   		 });
    ```
    {: codeblock}

</br>
**Detalles de la cuenta**

1. Establezca **Permitir a los usuarios registrarse y restablecer su contraseña** en **Activado** en los valores del directorio en la nube.
2. Llame al LoginWidget para iniciar el flujo de cambio de detalles.
   ```java
   LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
   loginWidget.launchChangeDetails(this, new AuthorizationListener() {
  			 @Override
          public void onAuthorizationFailure (AuthorizationException exception) {
          }

  			 @Override
          public void onAuthorizationCanceled () {
          }

  			 @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
          }
  		 });
   ```
   {: codeblock}

</br>
**Cambiar contraseña**

1. Establezca **Permitir a los usuarios registrarse y restablecer su contraseña** en **Activado** en los valores del directorio en la nube.
2. Llame al LoginWidget para iniciar el flujo de cambio de contraseña.
   ```java
    LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launchChangePassword(this, new AuthorizationListener() {
   			 @Override
          public void onAuthorizationFailure (AuthorizationException exception) {
          }

   			 @Override
          public void onAuthorizationCanceled () {
          }

   			 @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
          }
   		 });
   ```
   {: codeblock}

</br>
</br>

## Visualización de pantallas personalizadas con el SDK de iOS Swift
{: #branded-ui-ios-swift}

Con el directorio en la nube habilitado, puede llamar a pantallas personalizadas con el SDK de iOS Swift. Puede elegir la combinación de las pantallas con que desea que sus usuarios puedan interactuar.
{: shortdesc}

</br>
**Iniciar la sesión**

1. En el separador de proveedor de identidad de la GUI, establezca el directorio en la nube en **Activado**.
2. Inicie la sesión utilizando la contraseña del propietario del recurso. Puede obtener una señal de acceso y de ID proporcionando el nombre de usuario y contraseña del usuario final.
  ```swift
  class delegate : TokenResponseDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
      //Usuario autenticado
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
      //Se ha producido una excepción
        }
  }

  AppID.sharedInstance.obtainTokensWithROP(username: username, password: password, delegate: delegate())
  ```
  {: codeblock}

</br>
**Registrarse**

1. Establezca **Permitir a los usuarios registrarse y restablecer su contraseña** en **Activado** en los valores del directorio en la nube.
2. Llame al LoginWidget para iniciar el flujo de registro.
  ```swift
  class delegate : AuthorizationDelegate {
    public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
       if accessToken == nil && identityToken == nil {
        //es necesaria la verificación de correo electrónico
        return
       }
     //Usuario autenticado
      }

      public func onAuthorizationCanceled() {
        //Registro cancelado por el usuario
    }

    public func onAuthorizationFailure(error: AuthorizationError) {
        //Se ha producido una excepción
        }
  }

  AppID.sharedInstance.loginWidget?.launchSignUp(delegate: delegate())
  ```
  {: codeblock}

</br>
**Contraseña olvidada**

1. Establezca **Permitir a los usuarios registrarse y restablecer su contraseña** y **Correo electrónico de contraseña olvidada** en **Activado** en los valores del directorio en la nube.
2. Llame al LoginWidget para iniciar el flujo de contraseña olvidada.
  ```swift
  class delegate : AuthorizationDelegate {
     public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
        //contraseña olvidada finalizada, en este caso accessToken e identityToken serán nulos.

 			 }

     public func onAuthorizationCanceled() {
         //contraseña olvidada cancelado por el usuario
     }

     public func onAuthorizationFailure(error: AuthorizationError) {
         //Se ha producido una excepción
        }
  }

  AppID.sharedInstance.loginWidget?.launchForgotPassword(delegate: delegate())
  ```
  {: codeblock}

</br>
**Detalles de la cuenta**

1. Establezca **Permitir a los usuarios registrarse y restablecer su contraseña** en **Activado** en los valores del directorio en la nube.
2. Llame al LoginWidget para iniciar el flujo de cambio de detalles.
  ```swift

   class delegate : AuthorizationDelegate {
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
       }

       public func onAuthorizationCanceled() {
     }

       public func onAuthorizationFailure(error: AuthorizationError) {
     }
   }

   AppID.sharedInstance.loginWidget?.launchChangeDetails(delegate: delegate())
  ```
  {: codeblock}

</br>
**Cambiar contraseña**

1. Establezca **Permitir a los usuarios registrarse y restablecer su contraseña** en **Activado** en los valores del directorio en la nube.
2. Llame al LoginWidget para iniciar el flujo de cambio de contraseña.
  ```swift
   class delegate : AuthorizationDelegate {
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
       }

       public func onAuthorizationCanceled() {
     }

       public func onAuthorizationFailure(error: AuthorizationError) {
     }
    }

    AppID.sharedInstance.loginWidget?.launchChangePassword(delegate: delegate())
  ```
  {: codeblock}

</br>

## Visualización de pantallas personalizadas con el SDK de Node.js
{: #branded-ui-nodejs}

Con el directorio en la nube habilitado, puede llamar a pantallas personalizadas con el SDK de Node.js. Puede elegir la combinación de las pantallas con que desea que sus usuarios puedan interactuar.
{: shortdesc}

**Iniciar la sesión**
1. Establezca el directorio en la nube en **Activado** en los valores de proveedor de identidad y especifique un punto final de devolución de llamada.
2. Añada una ruta de envío a su app a la que pueda llamarse con los parámetros de nombre de usuario y contraseña e inicie la sesión utilizando la contraseña del propietario del recurso.
    **Nota**: `WebAppStrategy` permite a los usuarios iniciar la sesión en sus apps web con un nombre de usuario y contraseña. Tras iniciar la sesión correctamente, la señal de acceso de un usuario se almacena en la sesión HTTP y está disponible durante el transcurso de la sesión. Una vez que la sesión HTTP se ha destruido o ha caducado, la señal deja de ser válida.
    ```javascript
    app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
    	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true //permitir mensajes flash
  }));
    ```
    {: codeblock}

</br>
**Registrarse**

1. Establezca **Permitir a los usuarios registrarse y restablecer su contraseña** en **Activado** en los valores del directorio en la nube. Si está establecido en no, el proceso finaliza sin recuperar las señales de acceso e identidad.
2. Pase la propiedad `show` de WebAppStrategy y establézcala en `WebAppStrategy.SIGN_UP`.
  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: codeblock}

</br>
**Contraseña olvidada**

1. Establezca **Permitir a los usuarios registrarse y restablecer su contraseña** y **Correo electrónico de contraseña olvidada** en **Activado** en los valores del directorio en la nube. Si está establecido en no, el proceso finaliza sin recuperar las señales de acceso e identidad.
2. Pase la propiedad `show` de WebAppStrategy y establézcala en `WebAppStrategy.FORGOT_PASSWORD`.
  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: codeblock}

</br>
**Detalles de la cuenta**
1. Establezca **Permitir a los usuarios registrarse y restablecer su contraseña** en **Activado** en los valores del directorio en la nube.
2. Pase la propiedad `show` de WebAppStrategy y establézcala en `WebAppStrategy.CHANGE_DETAILS`.
  ```javascript
  app.get("/change_details", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_DETAILS
  }));
  ```
  {: codeblock}

</br>
**Cambiar contraseña**
1. Establezca **Permitir a los usuarios registrarse y restablecer su contraseña** en **Activado** en los valores del directorio en la nube.
2. Pase la propiedad `show` de WebAppStrategy y establézcala en `WebAppStrategy.CHANGE_PASSWORD`.
  ```javascript
  app.get("/change_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_PASSWORD
  }));
  ```
  {: codeblock}
