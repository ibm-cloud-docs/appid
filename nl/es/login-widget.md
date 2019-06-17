---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-06"

keywords: Authentication, authorization, identity, app security, secure, development, sign in, sign up, password, social, enterprise

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


# Utilización del widget Inicio de sesión
{: #login-widget}

Con {{site.data.keyword.appid_full}} puede utilizar una interfaz de usuario predeterminada, denominada Widget de inicio de sesión, para permitir a los usuarios de la aplicación elegir el proveedor de identidad con el que desean iniciar sesión. Si utiliza el Directorio en la nube, el widget de inicio de sesión también proporciona una interfaz de usuario adicional para funciones adicionales como, por ejemplo, registrarse, olvidarse de la palabra clave, autenticación de multifactores y más.
{: shortdesc}


## Comprensión del widget de inicio de sesión
{: #widget-understanding}

Uno de los mejores aspectos del Widget de inicio de sesión es que puede empezar a utilizar {{site.data.keyword.appid_short_notm}} antes de haber implementado cualquiera de sus propias IU de autenticación, lo que hace que la experiencia de incorporación del desarrollador sea mucho más fácil.

### ¿Cuál es el comportamiento predeterminado del Widget de inicio de sesión?
{: #widget-default}

De forma predeterminada, el widget de inicio de sesión está habilitado para utilizar el Facebook, Google y el Directorio en la nube. Puede cambiar el comportamiento en cualquier momento seleccionando los proveedores de identidad que desea configurar como una opción. Cuando se configura más de un proveedor de identidad, el Widget de inicio de sesión presenta una pantalla donde el usuario puede realizar su propia selección de proveedor de identidad. Pero si sólo tiene un proveedor habilitado, los usuarios no ven esta selección. Se les lleva directamente al proveedor de identidad para comenzar el proceso de inicio de sesión.

Por ejemplo, si utiliza los productos predeterminados (Facebook, Google y Directorio en la nube), los usuarios ven la pantalla. Si habilitar únicamente Facebook, los usuarios se dirigen directamente a Facebook para autenticarse.



### ¿Qué pantallas se pueden visualizar para cada proveedor?
{: #widget-options}

Si utiliza Directorio en la nube, {{site.data.keyword.appid_short_notm}} puede proporcionarle la funcionalidad ampliada de gestión de usuarios. La funcionalidad ampliada también se aplica a las prestaciones de Widgets de inicio de sesión. Los usuarios que están almacenados en Directorio en la nube pueden beneficiarse de funcionalidad, como por ejemplo, registrarse o el restablecer la contraseña directamente en el Widget de inicio de sesión. Consulte la tabla siguiente para ver qué pantallas puede visualizar para cada tipo de proveedor de identidad.

<table>
  <thead>
    <tr>
      <th>Pantalla del widget de inicio de sesión</th>
      <th>Proveedor de identidad social</th>
      <th>Proveedor de identidad empresarial</th>
      <th>Directorio en la nube</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Iniciar sesión</td>
      <td><img src="images/confirm.png" width="32" alt="Característica disponible" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="Característica disponible" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="Característica disponible" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Registro</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Característica disponible" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Contraseña olvidada</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Característica disponible" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Cambio de contraseña</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Característica disponible" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Detalles de la cuenta</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Característica disponible" style="width:32px;" /></td>
    </tr>
  </tbody>
</table>


## Personalización del widget de inicio de sesión
{: #widget-customize}

El Widget de inicio de sesión es dinámico. Puede personalizar el aspecto o la configuración del proveedor de identidad, y los cambios se aplican de forma inmediata. No es necesario que actualice el código de la aplicación ni que vuelva a desplegar la app.
{: shortdesc}

¿Necesita más personalización de la que proporciona el Widget de inicio de sesión? Puede implementar su propia interfaz de usuario totalmente personalizada para el inicio de sesión de usuario, el registro, el restablecimiento de la contraseña y otros flujos para crear una experiencia que sea exclusiva de su app. Para empezar, consulte [Gestión de marca en la app](/docs/services/appid?topic=appid-branded).
{: tip}

Para personalizar la pantalla:

1. Abra el panel de control del servicio {{site.data.keyword.appid_short_notm}}.
2. Seleccione la sección **Personalización de inicio de sesión**. Puede modificar el aspecto del Widget de inicio de sesión para alinearlo con la marca de su empresa.
3. Suba el logotipo de su empresa seleccionando un archivo PNG o JPG del sistema local. El tamaño de imagen recomendado es de 320 x 320 píxeles. El tamaño de archivo máximo es 100 Kb.
4. Seleccione un color de cabecera para el widget desde el selector de color, o especifique el código hexadecimal para otro color.
5. Inspeccione el panel de vista previa y pulse **Guardar cambios** cuando esté satisfecho con las personalizaciones. Aparecerá un mensaje de confirmación.
6. En el navegador, renueve la página de inicio de sesión para verificar los cambios.


## Visualización del widget de inicio de sesión con el SDK de Android
{: #widget-display-android}

Puede llamar a pantallas preconfiguradas con el [SDK de cliente de Android](https://github.com/ibm-cloud-security/appid-clientsdk-android).
{: shortdesc}

Añada el mandato siguiente a su código.

  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launch(this, new AuthorizationListener() {
        @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //Se ha producido una excepción
        }

        @Override
          public void onAuthorizationCanceled () {
          //Autenticación cancelada por el usuario
        }

        @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
          //Usuario autenticado
        }
      });
  ```
{: codeblock}

</br>

### Registro
{: #widget-android-signup}

1. Configure los [valores](/docs/services/appid?topic=appid-cloud-directory#cd-settings) del directorio en la nube en la GUI. **Permitir a los usuarios iniciar sesión en la app** y **Permitir a los usuarios gestionar su cuenta desde la app** deben establecerse en **Activado**.
2. Añada el código siguiente a la app. Cuando un usuario inicia sesión en la app desde la pantalla personalizada, se inicia el flujo de registro. La llamada siguiente no solo registra al usuario, sino que también puede enviar un correo electrónico de verificación para completar el registro, en función de las configuraciones del directorio en la nube.

  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
 loginWidget.launchSignUp(this, new AuthorizationListener() {
      @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //Se ha producido una excepción
        }

      @Override
          public void onAuthorizationCanceled () {
          //Registro cancelado por el usuario
			 }

      @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          if (accessToken != null && identityToken != null) {
              //Usuario autenticado
				 } else {
              //Es necesaria la verificación de correo electrónico
				 }
      }
  });
  ```
  {: codeblock}

</br>

### Contraseña olvidada
{: #widget-android-forgot-password}

1. Configure los [valores](/docs/services/appid?topic=appid-cloud-directory#cd-settings) del directorio en la nube en la GUI. **Permitir a los usuarios gestionar la cuenta desde la app** se debe establecer en **Activado**.
2. En el separador **Restablecer contraseña** del panel de control del servicio, asegúrese de que **Correo electrónico de contraseña olvidada** se haya establecido en **Activado**.
3. Añada el código siguiente a la app. Cuando un usuario pulsa "contraseña olvidada" en la aplicación, el SDK llama a la API forgot_password para enviar un correo electrónico al usuario que le permita restablecerla.

  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launchForgotPassword(this, new AuthorizationListener() {
      @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //Se ha producido una excepción
        }

      @Override
          public void onAuthorizationCanceled () {
          //Contraseña olvidada cancelado por el usuario
      }

      @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          //Contraseña olvidada finalizada, en este caso accessToken e identityToken serán nulos.
 			 }
  });
  ```
  {: codeblock}

</br>

### Cambio de detalles
{: #widget-android-change-details}

1. Configure los [valores](/docs/services/appid?topic=appid-cloud-directory#cd-settings) del directorio en la nube en la GUI. **Permitir a los usuarios iniciar sesión en la app** y **Permitir a los usuarios gestionar su cuenta desde la app** deben establecerse en **Activado**.
2. En el separador **Contraseña cambiada** del panel de control del servicio, establezca **Correo electrónico de contraseña olvidada** en
3. Llame al widget de inicio de sesión para iniciar el flujo de cambio de detalles.

  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
   loginWidget.launchChangeDetails(this, new AuthorizationListener() {
      @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //Se ha producido una excepción
        }

      @Override
          public void onAuthorizationCanceled () {
          //Cambiar detalles cancelado por el usuario
      }

      @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          //Usuario autenticado y señales nuevas recibidas
  			 }
  });
  ```
  {: codeblock}

</br>

### Cambio de contraseña
{: #widget-android-change-password}

1. Configure los [valores](/docs/services/appid?topic=appid-cloud-directory#cd-settings) del directorio en la nube en la GUI. **Permitir a los usuarios iniciar sesión en la app** y **Permitir a los usuarios gestionar su cuenta desde la app** deben establecerse en **Activado**.
2. Añada el código siguiente en la app para iniciar el flujo de cambio de contraseña.

  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launchChangePassword(this, new AuthorizationListener() {
      @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //Se ha producido una excepción
        }

      @Override
          public void onAuthorizationCanceled () {
          //Cambiar contraseña cancelado por el usuario
      }

      @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          //Usuario autenticado y señales nuevas recibidas
  			 }
  });
  ```
  {: codeblock}



## Visualización del widget de inicio de sesión en el SDK de Swift de iOS
{: #widget-display-ios-swift}

Puede llamar pantallas preconfiguradas con el [SDK del cliente de Swift de iOS](https://github.com/ibm-cloud-security/appid-clientsdk-swift).
{: shortdesc}

Añada el mandato siguiente a su código.

  ```swift
  import IBMCloudAppID
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, refreshToken: RefreshToken?) {
          //Usuario autenticado
      }

      public func onAuthorizationCanceled() {
          //Autenticación cancelada por el usuario
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          //Se ha producido una excepción
        }
  }

  AppID.sharedInstance.loginWidget?.launch(delegate: delegate())
  ```
  {: codeblock}

</br>

### Registro
{: #widget-ios-signup}

1. Configure los [valores](/docs/services/appid?topic=appid-cloud-directory#cd-settings) del directorio en la nube en la GUI. **Permitir a los usuarios iniciar sesión en la app** y **Permitir a los usuarios gestionar su cuenta desde la app** deben establecerse en **Activado**.
2. Añada el código siguiente en la aplicación. Cuando un usuario intenta registrarse en su aplicación, se llama al widget de inicio de sesión y este muestra la página de registro personalizada.

  ```swift
  class delegate : AuthorizationDelegate {
    public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
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

### Contraseña olvidada
{: #widget-ios-forgot-password}

1. Configure los [valores](/docs/services/appid?topic=appid-cloud-directory#cd-settings) del directorio en la nube en la GUI. **Permitir a los usuarios gestionar la cuenta desde la app** se debe establecer en **Activado**.
2. En el separador **Restablecer contraseña** del panel de control del servicio, asegúrese de que **Correo electrónico de contraseña olvidada** se haya establecido en **Activado**.
3. Añada el código siguiente en la aplicación. Cuando uno de los usuarios de la app solicita que se actualice la contraseña, se llama al widget de inicio de sesión y se inicia el proceso.

  ```swift
  class delegate : AuthorizationDelegate {
     public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
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

### Cambio de detalles
{: #widget-ios-change-details}

1. Configure los [valores](/docs/services/appid?topic=appid-cloud-directory#cd-settings) del directorio en la nube en la GUI. **Permitir a los usuarios iniciar sesión en la app** y **Permitir a los usuarios gestionar su cuenta desde la app** deben establecerse en **Activado**.
2. En el separador **Contraseña cambiada** del panel de control del servicio, establezca **Correo electrónico de contraseña olvidada** en
3. Llame al widget de inicio de sesión para iniciar el flujo de cambio de detalles.

  ```swift
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
         //Usuario autenticado y señales nuevas recibidas
       }

       public func onAuthorizationCanceled() {
          //cambiar detalles cancelado por el usuario
       }

       public func onAuthorizationFailure(error: AuthorizationError) {
          //Se ha producido una excepción
        }
  }

   AppID.sharedInstance.loginWidget?.launchChangeDetails(delegate: delegate())
  ```
  {: codeblock}

</br>

### Cambio de contraseña
{: #widget-ios-change-password}

1. Configure los [valores](/docs/services/appid?topic=appid-cloud-directory#cd-settings) del directorio en la nube en la GUI. **Permitir a los usuarios iniciar sesión en la app** y **Permitir a los usuarios gestionar su cuenta desde la app** deben establecerse en **Activado**.
2. Añada el código siguiente en la app para iniciar el flujo de cambio de contraseña.

  ```swift
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
          //Usuario autenticado y señales nuevas recibidas
       }

       public func onAuthorizationCanceled() {
          //cambiar contraseña cancelado por el usuario
       }

       public func onAuthorizationFailure(error: AuthorizationError) {
           //Se ha producido una excepción
        }
   }

    AppID.sharedInstance.loginWidget?.launchChangePassword(delegate: delegate())
  ```
  {: codeblock}


## Visualización del widget de inicio de sesión con el SDK de Node.js
{: #widget-display-nodejs}

Puede llamar a pantallas preconfiguradas con el [SDK del servidor Node.js](https://github.com/ibm-cloud-security/appid-serversdk-nodejs).
{: shortdesc}

Añada una ruta de envío a su app a la que pueda llamarse con los parámetros de nombre de usuario y contraseña e inicie la sesión utilizando la contraseña del propietario del recurso.

  ```javascript
  app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true //permitir mensajes flash
  }));
  ```
  {: codeblock}

`WebAppStrategy` permite a los usuarios iniciar sesión en sus apps web con un nombre de usuario y una contraseña. Después de un inicio de sesión satisfactorio, la señal de acceso de un usuario se almacena en la sesión HTTP y está disponible durante la sesión. Cuando la sesión HTTP se ha destruido o ha caducado, la señal deja de ser válida.
{: tip}

</br>

### Registro
{: #widget-nodejs-signup}

1. Configure los [valores](/docs/services/appid?topic=appid-cloud-directory#cd-settings) del directorio en la nube en la GUI. **Permitir a los usuarios iniciar sesión en la app** y **Permitir a los usuarios gestionar su cuenta desde la app** deben establecerse en **Activado**.
2. Añada el código siguiente en la aplicación. Cuando un usuario intenta registrarse en su aplicación, se llama al widget de inicio de sesión y este muestra la página de registro personalizada.

  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: codeblock}

</br>

### Contraseña olvidada
{: #widget-nodejs-forgot-password}

1. Configure los [valores](/docs/services/appid?topic=appid-cloud-directory#cd-settings) del directorio en la nube en la GUI. **Permitir a los usuarios gestionar la cuenta desde la app** se debe establecer en **Activado**.
2. En el separador **Restablecer contraseña** del panel de control del servicio, asegúrese de que **Correo electrónico de contraseña olvidada** se haya establecido en **Activado**.
3. Añada el código siguiente en la aplicación para pasar la propiedad *show* a `WebAppStrategy.FORGOT_PASSWORD`. Cuando  un usuario solicita que se actualice la contraseña de la app, se llama al widget de inicio de sesión y se inicia el proceso.

  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: codeblock}

</br>

### Cambio de detalles
{: #widget-nodejs-change-details}

1. Configure los [valores](/docs/services/appid?topic=appid-cloud-directory#cd-settings) del directorio en la nube en la GUI. **Permitir a los usuarios iniciar sesión en la app** y **Permitir a los usuarios gestionar su cuenta desde la app** deben establecerse en **Activado**.
2. En el separador **Contraseña cambiada** del panel de control del servicio, establezca **Correo electrónico de contraseña olvidada** en
3. Añada el código siguiente en la aplicación para pasar la propiedad *show* a `WebAppStrategy.FORGOT_PASSWORD` para iniciar el formulario de modificación de detalles.

  ```javascript
  app.get("/change_details", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_DETAILS
  }));
  ```
  {: codeblock}

</br>

### Cambio de contraseña
{: #widget-nodejs-change-password}

1. Configure los [valores](/docs/services/appid?topic=appid-cloud-directory#cd-settings) del directorio en la nube en la GUI. **Permitir a los usuarios iniciar sesión en la app** y **Permitir a los usuarios gestionar su cuenta desde la app** deben establecerse en **Activado**.
2. En el separador **Contraseña cambiada** del panel de control del servicio, establezca **Correo electrónico de contraseña olvidada** en
3. Añada el código siguiente en la aplicación para pasar la propiedad *show* a `WebAppStrategy.FORGOT_PASSWORD` para iniciar el formulario de modificación de detalles.

  ```javascript
  app.get("/change_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_PASSWORD
  }));
  ```
  {: codeblock}
