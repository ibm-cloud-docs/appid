---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-19"

---

{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:pre: .pre}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# Visualización del widget de inicio de sesión
{: #login-widget}

{{site.data.keyword.appid_full}} proporciona un widget de inicio de sesión que permite proporcionar a los usuarios opciones de inicio de sesión seguras.
{: shortdesc}

Cuando la app está configurada para utilizar un proveedor de identidad, el widget de inicio de sesión dirigirá a los visitantes de su app a una pantalla de inicio de sesión. Con el widget de inicio de sesión puede visualizar pantallas preconfiguradas de los flujos de inicio de sesión. Y, además, puede actualizar su flujo de inicio de sesión en cualquier momento, sin cambiar el código fuente de ninguna forma.

¿Desea crear una experiencia que sea exclusiva de su app? Puede [aportar sus propias pantallas](/docs/services/appid/branded.html).
{: tip}

## Comprensión del widget de inicio de sesión
{: #understanding}

Puede beneficiarse de {{site.data.keyword.appid_short_notm}}, incluso aunque no tenga sus propias pantallas de interfaz de usuario, visualizando el widget de inicio de sesión.
{: shortdesc}

**¿Cuál es el valor predeterminado?**

Cuando se configura más de un proveedor de identidad, se redirige a un usuario al widget de inicio de sesión cuando este intenta iniciar sesión en la aplicación. Utilizando el widget de inicio de sesión, los usuarios pueden elegir el proveedor con el que desean verificar su identidad. Pero, cuando solo se establece un proveedor en **Activado**, los visitantes serán redirigidos a dicha pantalla de autenticación de proveedores de identidad.

**¿Cuánta información obtiene {{site.data.keyword.appid_short_notm}} de un proveedor de identidad?**

Cuando utiliza proveedores de identidad sociales o de empresa, {{site.data.keyword.appid_short_notm}} tiene acceso de lectura a la información de cuenta de un usuario. El servicio utiliza una señal y aserciones devueltas por el proveedor de identidad para verificar que un usuario es quien dice ser. Puesto que el servicio nunca tiene acceso de escritura a la información, los usuarios deben pasar por el proveedor de identidad elegido para realizar acciones como, por ejemplo, restablecer la contraseña. Por ejemplo, si un usuario inicia sesión en la app con Facebook y después desea cambiar la contraseña, deberá dirigirse a www.facebook.com para hacerlo.

Cuando utiliza [Directorio en la nube](/docs/services/appid/cloud-directory.html), {{site.data.keyword.appid_short_notm}} es el proveedor de identidad. El servicio utiliza el registro para verificar la identidad de los usuarios. Puesto que {{site.data.keyword.appid_short_notm}} es el proveedor, los usuarios pueden sacar partido de la funcionalidad avanzada y restablecer la contraseña directamente en la app.

**¿Qué tipo de pantallas se pueden visualizar para cada tipo de proveedor?**

Consulte la tabla siguiente para ver qué pantallas puede visualizar para cada tipo de proveedor de identidad.

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

</br>
</br>

## Personalización del widget de inicio de sesión
{: #customize}

{{site.data.keyword.appid_short_notm}} proporciona una pantalla de inicio de sesión predeterminada que puede llamar si no tiene sus propias pantallas de IU para mostrar. Puede personalizar la pantalla para visualizar el logotipo y los colores que elija.
{: shortdesc}

Para personalizar la pantalla:

1. Abra el panel de control del servicio de {{site.data.keyword.appid_short_notm}}.
2. Seleccione la sección **Personalización de inicio de sesión**. Puede modificar el aspecto del Widget de inicio de sesión para alinearlo con la marca de su empresa.
3. Suba el logotipo de su empresa seleccionando un archivo PNG o JPG del sistema local. El tamaño de imagen recomendado es de 320 x 320 píxeles. El tamaño de archivo máximo es 100 Kb.
4. Seleccione un color de cabecera para el widget desde el selector de color, o especifique el código hexadecimal para otro color.
5. Inspeccione el panel de vista previa y pulse **Guardar cambios** cuando esté satisfecho con las personalizaciones. Aparecerá un mensaje de confirmación.
6. En el navegador, renueve la página de inicio de sesión para verificar los cambios.

Recuerde: También puede sacar partido de {{site.data.keyword.appid_short_notm}} con otros idiomas. Si no ve un SDK del idioma con el que está trabajando, siempre puede utilizar las API. Consulte <a href="https://www.ibm.com/blogs/bluemix/tag/app-id/" target="blank">nuestros blogs<img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.
{: tip}


## Visualización del widget de inicio de sesión con el SDK de Android
{: #android}

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

**Registro**

1. Configure los [valores](cloud-directory.html#cd-settings) del directorio en la nube en la GUI. **Permitir a los usuarios iniciar sesión en la app** y **Permitir a los usuarios gestionar su cuenta desde la app** deben establecerse en **Activado**.
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
  {: pre}

</br>

**Contraseña olvidada**

1. Configure los [valores](cloud-directory.html#cd-settings) del directorio en la nube en la GUI. **Permitir a los usuarios gestionar la cuenta desde la app** se debe establecer en **Activado**.
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

**Cambiar detalles**

1. Configure los [valores](cloud-directory.html#cd-settings) del directorio en la nube en la GUI. **Permitir a los usuarios iniciar sesión en la app** y **Permitir a los usuarios gestionar su cuenta desde la app** deben establecerse en **Activado**.
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

**Cambio de contraseña**

1. Configure los [valores](cloud-directory.html#cd-settings) del directorio en la nube en la GUI. **Permitir a los usuarios iniciar sesión en la app** y **Permitir a los usuarios gestionar su cuenta desde la app** deben establecerse en **Activado**.
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


</br>
</br>

## Visualización del widget de inicio de sesión en el SDK de Swift de iOS
{: #ios-swift}

Puede llamar pantallas preconfiguradas con el [SDK del cliente de Swift de iOS](https://github.com/ibm-cloud-security/appid-clientsdk-swift).
{: shortdesc}

Añada el mandato siguiente a su código.

  ```swift
  import BluemixAppID
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

**Registro**

1. Configure los [valores](cloud-directory.html#cd-settings) del directorio en la nube en la GUI. **Permitir a los usuarios iniciar sesión en la app** y **Permitir a los usuarios gestionar su cuenta desde la app** deben establecerse en **Activado**.
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

**Contraseña olvidada**

1. Configure los [valores](cloud-directory.html#cd-settings) del directorio en la nube en la GUI. **Permitir a los usuarios gestionar la cuenta desde la app** se debe establecer en **Activado**.
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

**Cambiar detalles**

1. Configure los [valores](cloud-directory.html#cd-settings) del directorio en la nube en la GUI. **Permitir a los usuarios iniciar sesión en la app** y **Permitir a los usuarios gestionar su cuenta desde la app** deben establecerse en **Activado**.
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

**Cambio de contraseña**

1. Configure los [valores](cloud-directory.html#cd-settings) del directorio en la nube en la GUI. **Permitir a los usuarios iniciar sesión en la app** y **Permitir a los usuarios gestionar su cuenta desde la app** deben establecerse en **Activado**.
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

</br>
</br>

## Visualización del widget de inicio de sesión con el SDK de Node.js
{: #nodejs}

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

**Registro**

1. Configure los [valores](cloud-directory.html#cd-settings) del directorio en la nube en la GUI. **Permitir a los usuarios iniciar sesión en la app** y **Permitir a los usuarios gestionar su cuenta desde la app** deben establecerse en **Activado**.
2. Añada el código siguiente en la aplicación. Cuando un usuario intenta registrarse en su aplicación, se llama al widget de inicio de sesión y este muestra la página de registro personalizada.

  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: codeblock}

</br>

**Contraseña olvidada**

1. Configure los [valores](cloud-directory.html#cd-settings) del directorio en la nube en la GUI. **Permitir a los usuarios gestionar la cuenta desde la app** se debe establecer en **Activado**.
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

**Cambiar detalles**

1. Configure los [valores](cloud-directory.html#cd-settings) del directorio en la nube en la GUI. **Permitir a los usuarios iniciar sesión en la app** y **Permitir a los usuarios gestionar su cuenta desde la app** deben establecerse en **Activado**.
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

**Cambio de contraseña**

1. Configure los [valores](cloud-directory.html#cd-settings) del directorio en la nube en la GUI. **Permitir a los usuarios iniciar sesión en la app** y **Permitir a los usuarios gestionar su cuenta desde la app** deben establecerse en **Activado**.
2. En el separador **Contraseña cambiada** del panel de control del servicio, establezca **Correo electrónico de contraseña olvidada** en
3. Añada el código siguiente en la aplicación para pasar la propiedad *show* a `WebAppStrategy.FORGOT_PASSWORD` para iniciar el formulario de modificación de detalles.

  ```javascript
  app.get("/change_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_PASSWORD
  }));
  ```
  {: codeblock}

</br>
