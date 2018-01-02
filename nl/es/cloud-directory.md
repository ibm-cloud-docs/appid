---

copyright:
  years: 2017
lastupdated: "2017-12-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Gestión del Directorio de nube
{: #cd}

Puede configurar {{site.data.keyword.appid_short_notm}} para utilizar el Directorio de nube como proveedor de identidad. Cuando los usuarios inician sesión con su correo electrónico y una contraseña, se agregan a su directorio y puede gestionarlos desde la interfaz gráfica de usuario del servicio.
{: shortdesc}

<!--- What is a cloud directory? --->

## Gestión de los valores de directorio

Puede configurar las notificaciones y el nivel de control de usuario para su app. En el separador **Valores de directorio** de la interfaz gráfica de usuario, puede decidir cuanto autoservicio podrán hacer sus usuarios.

1. Para permitir a los usuarios utilizar un correo electrónico para registrarse, debe establecer **Permitir a los usuarios registrarse y restablecer su contraseña** en **Activado**. Puede seguir agregando usuarios a través de la consola cuando está definido en **Desactivado**, pero solo para desarrollo.
2. Configure los detalles de su remitente. Especifique el correo electrónico que enviará los mensajes, quien aparecerá como remitente y a quien pueden responder los usuarios. **Nota**: Asegúrese de dejar tiempo suficiente para que un usuario pulse el enlace al configurar el URL de acción. El usuario debe verificar su correo electrónico para tener ciertas opciones, como la capacidad de solicitar un restablecimiento de su contraseña.
3. Determine los tipos de correo electrónico que recibe un usuario y la información del remitente.



## Gestión de mensajes

Una plantilla es un ejemplo de un mensaje de correo electrónico que puede enviar a sus usuarios. Puede personalizarla actualizando el contenido y el diseño del mensaje. Puede definir estos mensajes en **Activados** o **Desactivados** en el separador de valores de directorio.

1. Seleccione un **Tipo de mensaje**.
2. Personalice el mensaje cambiando el contenido y el diseño. Puede utilizar parámetros para personalizar sus mensajes. No se olvide de guardar los cambios.

### Tipos de mensajes

<dl>
  <dt> Bienvenido</dt>
    <dd>Puede dar la bienvenida a su aplicación a un usuario a través de correo electrónico una vez se registre. Para dar la bienvenida y retener a los usuarios, haga su mensaje tan interactivo como sea posible.<table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> Parámetros que pueden utilizarse en cualquier tipo de mensaje</th>
      </thead>
      <tbody>
        <tr>
          <td> %{display.logo} </td>
          <td> Muestra la imagen que ha configurado para su widget de inicio de sesión. </td>
        </tr>
	 <tr>
          <td> %{display.headerColor} </td>
          <td> Muestra el color de cabecera que ha configurado para su widget de inicio de sesión. </td>
        </tr>
        <tr>
          <td> %{user.displayName} </td>
          <td> Muestra el nombre de pantalla que ha elegido un usuario para utilizar para interactuar con la app.</td>
        </tr>
        <tr>
          <td> %{user.email} </td>
          <td> Muestra la dirección de correo electrónico registrada del usuario. </td>
        </tr>
        <tr>
          <td> %{user.firstName} </td>
          <td> Muestra el nombre del usuario especificado.</td>
        </tr>
        <tr>
          <td> %{user.formattedName} </td>
          <td> Muestra el nombre completo del usuario. </td>
        </tr>
        <tr>
          <td> %{user.lastName} </td>
          <td> Muestra los apellidos del usuario especificados. </td>
        </tr>
      </tbody>
    </table>

    **Nota**: Si un usuario no proporciona la información extraída por el parámetro, aparecerá en blanco.</dd>
  <dt> Contraseña olvidada</dt>
    <dd> Un usuario puede pedir el restablecimiento de contraseña si la ha olvidado o necesita actualizarla por cualquier motivo. Puede personalizar la respuesta por correo electrónico a su solicitud. Cuando un usuario solicita un cambio, su contraseña sigue siendo la misma hasta que pulsa en el enlace en este correo electrónico.<table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> Parámetros de cambio de contraseña</th>
      </thead>
      <tbody>
        <tr>
          <td> %{linkExpiration.hours} </td>
          <td> Muestra el número de horas que es válido el enlace. </td>
        </tr>
        <tr>
          <td> %{linkExpiration.minutes} </td>
          <td> Muestra el número de minutos que es válido el enlace. </td>
        </tr>
        <tr>
          <td> %{resetPassword.code} </td>
          <td> Muestra una clave de acceso de un único uso como parte del URL. Esto significaría que cada persona tendría un código diferente. Ejemplo: <code>https://appid-wfm.bluemix.net/verify/6574839563478 </code> </td>
        </tr>
        <tr>
          <td> %{resetPassword.link} </td>
          <td> Muestra el enlace que pulsa un usuario para restablecer su contraseña. </td>
        </tr>
       </tbody>
    </table></dd>
  <dt> Verificación</dt>
    <dd> Puede solicitar que el usuario verifique su cuenta por correo electrónico. Al solicitar una verificación, se limita el número de cuentas falsas que pueden registrarse en su app. Puede restringir el acceso a su app hasta que el usuario haya verificado su correo electrónico, o utilizarlo como forma de gestionar los usuarios para los que ha creado perfiles.<table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> Parámetros de mensaje de verificación</th>
      </thead>
      <tbody>
        <tr>
          <td> %{linkExpiration.hours} </td>
          <td> Muestra el número de horas que es válido el enlace. </td>
        </tr>
        <tr>
          <td> %{linkExpiration.minutes} </td>
          <td> Muestra el número de minutos que es válido el enlace. </td>
        </tr>
        <tr>
          <td> %{verify.code} </td>
          <td> Muestra un URL de verificación de un único uso. </td>
        </tr>
        <tr>
          <td> %{verify.link} </td>
          <td> Muestra el URL de acción que especificó en los valores.</td>
        </tr>
      </tbody>
    </table></dd>
  <dt> Cambio de contraseña</dt>
    <dd> Puede hacer saber al usuario cuando se ha actualizado su contraseña. Esto es útil si no ha solicitado el cambio de contraseña. Pueden llevar a cabo los pasos apropiados para volver a asegurar su cuenta.<table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> Parámetros de cambio de contraseña</th>
      </thead>
      <tbody>
        <tr>
          <td> %{passwordChangeInfo.time} </td>
          <td> Muestra la hora en que entra en vigor la nueva contraseña. </td>
        </tr>
        <tr>
          <td> %{passwordChangeInfo.ipAddress} </td>
          <td> Muestra la dirección IP desde la que se ha solicitado el cambio de contraseña. </td>
        </tr>
      </tbody>
    </table></dd>
</dl>



## Gestión del Directorio de nube con el SDK de Android
{: #managing-android}

Asegúrese de establecer el **proveedor de identidad del directorio de nube** en **ACTIVADO** al utilizar las siguientes API.

### Iniciar sesión utilizando la contraseña de propietario de recurso
Puede obtener una señal de acceso y de ID proporcionando el nombre de usuario y contraseña del usuario final.

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

### Registro

Asegúrese de establecer **Permitir a los usuarios registrarse y restablecer su contraseña** en **ACTIVADO** en los valores del Directorio de nube. 

 Utilice la clase LoginWidget para iniciar el flujo de registro.
 ```java
 LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
 loginWidget.launchSignUp(this, new AuthorizationListener() {
			 @Override
		public void onAuthorizationFailure(AuthorizationException exception) {
				 //Se ha producido una excepción
		}

			 @Override
        public void onAuthorizationCanceled () {
				 //Registro cancelado por el usuario
			 }

			 @Override
		public void onAuthorizationSuccess(AccessToken accessToken, IdentityToken identityToken) {
				 if (accessToken != null && identityToken != null) {
				     //Usuario autenticado
				 } else {
				     //Es necesaria la verificación de correo electrónico
				 }

			 }
		 });
 ```
 {: codeblock}

### Contraseña olvidada
Asegúrese de establecer **Permitir a los usuarios registrarse y restablecer su contraseña** y **Correo electrónico de contraseña olvidada** en **ACTIVADO** en los valores del Directorio de nube. 

Utilice la clase LoginWidget para iniciar el flujo de contraseña olvidada.
  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launchForgotPassword(this, new AuthorizationListener() {
 			 @Override
		public void onAuthorizationFailure(AuthorizationException exception) {
 				 //Se ha producido una excepción
		}

 			 @Override
        public void onAuthorizationCanceled () {
 				 //contraseña olvidada cancelada por el usuario
 			 }

 			 @Override
		public void onAuthorizationSuccess(AccessToken accessToken, IdentityToken identityToken) {
 				 //contraseña olvidada finalizada, en este caso accessToken e identityToken serán nulos.

 			 }
 		 });
  ```
  {: codeblock}

### Cambiar detalles
Asegúrese de establecer **Permitir a los usuarios registrarse y restablecer su contraseña** en **ACTIVADO** en los valores del Directorio de nube. Utilice la clase LoginWidget para iniciar el flujo de cambio de detalles. Esta API solo se puede utilizar cuando el usuario inicia sesión utilizando el Directorio de nube como proveedor de identidad.
   ```java
   LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
   loginWidget.launchChangeDetails(this, new AuthorizationListener() {
  			 @Override
		public void onAuthorizationFailure(AuthorizationException exception) {
  				 //Se ha producido una excepción
		}

  			 @Override
        public void onAuthorizationCanceled () {
  				 //cambiar detalles cancelado por el usuario
  			 }

  			 @Override
		public void onAuthorizationSuccess(AccessToken accessToken, IdentityToken identityToken) {
  				 //Usuario autenticado y señales nuevas recibidas
  			 }
  		 });
   ```
   {: codeblock}

### Cambiar contraseña
Asegúrese de establecer **Permitir a los usuarios registrarse y restablecer su contraseña** en **ACTIVADO** en los valores del Directorio de nube. 

Utilice la clase LoginWidget para iniciar el flujo de cambio de contraseña. Esta API solo se puede utilizar cuando el usuario ha iniciado sesión utilizando el Directorio de nube como proveedor de identidad.

   ```java
    LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launchChangePassword(this, new AuthorizationListener() {
   			 @Override
		public void onAuthorizationFailure(AuthorizationException exception) {
   				 //Se ha producido una excepción
		}

   			 @Override
        public void onAuthorizationCanceled () {
   				 //cambiar contraseña cancelado por el usuario
   			 }

   			 @Override
		public void onAuthorizationSuccess(AccessToken accessToken, IdentityToken identityToken) {
   				   //Usuario autenticado y señales nuevas recibidas
  			 }
  		 });
   ```
   {: codeblock}

## Gestión del Directorio de nube con el SDK de Swift de iOS


### Iniciar sesión utilizando la contraseña de propietario de recurso

Puede obtener una señal de acceso y de ID proporcionando el nombre de usuario y contraseña del usuario final.
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

### Registro

Asegúrese de establecer **Permitir a los usuarios registrarse y restablecer su contraseña** en **ACTIVADO** en los valores del Directorio de nube. 

Utilice la clase LoginWidget para iniciar el flujo de registro.
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

### Contraseña olvidada
Asegúrese de establecer **Permitir a los usuarios registrarse y restablecer su contraseña** y **Correo electrónico de contraseña olvidada** en **ACTIVADO** en los valores del Directorio de nube. 

Utilice la clase LoginWidget para iniciar el flujo de contraseña olvidada.
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

### Cambiar detalles

Asegúrese de establecer **Permitir a los usuarios registrarse y restablecer su contraseña** en **ACTIVADO** en los valores del Directorio de nube. 

Utilice la clase LoginWidget para iniciar el flujo de cambio de detalles. Esta API solo se puede utilizar cuando el usuario inicia sesión utilizando el Directorio de nube como proveedor de identidad.
  ```swift

   class delegate : AuthorizationDelegate {
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
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

### Cambiar contraseña

Asegúrese de establecer **Permitir a los usuarios registrarse y restablecer su contraseña** en **ACTIVADO** en los valores del Directorio de nube. 

Utilice la clase LoginWidget para iniciar el flujo de cambio de contraseña. Esta API solo se puede utilizar cuando el usuario inicia sesión utilizando el Directorio de nube como proveedor de identidad.
  ```swift
   class delegate : AuthorizationDelegate {
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
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


## Gestión del Directorio de nube con el SDK de Node.js
Asegúrese de que el proveedor de identidad del Directorio de nube está definido en **ACTIVADO** e incluye el punto final de devolución de llamada.

### Iniciar sesión utilizando el flujo de la contraseña de propietario de recurso
WebAppStrategy permite a los usuarios iniciar sesión en su aplicación web utilizando un nombre de usuario y una contraseña.
Después de un inicio de sesión satisfactorio, la señal de acceso de usuario se persiste en la sesión HTTP y está disponible mientras se mantenga activa la sesión HTTP. Cuando la sesión HTTP se ha destruido o ha caducado la señal también se destruye.

Para permitir a los usuarios iniciar sesión utilizando un nombre de usuario y una contraseña, agregue a su app una ruta de envío a la que se llamará con los parámetros de nombre de usuario y contraseña.

  ```javascript
  app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true //permitir mensajes flash
  }));
  ```
  {: codeblock}

  <table>
    <thead>
      <th colspan=2><img src="images/idea.png"/> Descripción de los componentes de este mandato</th>
    </thead>
    <tbody>
      <tr>
        <td><code> successRedirect </code></td>
        <td> Establezca este valor en el URL al que desea redireccionar a un usuario tras la autenticación satisfactoria. El valor predeterminado es el URL de solicitud original. Ejemplo: <code>/form/submit</code> </td>
      </tr>
      <tr>
        <td><code> failureRedirect </code></td>
        <td> Establezca este valor en el URL al que desea redireccionar a un usuario si falla la autenticación. El valor predeterminado es el URL de solicitud original. </td>
      </tr>
      <tr>
        <td><code> failureFlash </code></td>
        <td> Establezca este valor en <code>true</code> para recibir un mensaje de error devuelto desde el Directorio de nube. El valor predeterminado es false. </td>
      </tr>
     </tbody>
  </table>


**Nota**:
  * Si envía la solicitud utilizando un formulario HTML, utilice el middleware [body-parser](https://www.npmjs.com/package/body-parser).
  * Utilice [connect-flash](https://www.npmjs.com/package/connect-flash) para obtener el mensaje de error devuelto. Vea `web-app-sample-server.js`.

### Registro
Para iniciar el formulario de registro de {{site.data.keyword.appid_short_notm}}, pase la propiedad "show" de WebAppStrategy y establézcala en `WebAppStrategy.SIGN_UP`.
  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: codeblock}

    **Nota**:
    * Si en los valores de su Directorio de nube, **Permitir a los usuarios iniciar sesión sin verificación de correo electrónico** se establece en **No**, el proceso finaliza sin recuperar las señales de acceso y de ID de {{site.data.keyword.appid_short_notm}}.
    * Asegúrese de establecer **Permitir a los usuarios registrarse y restablecer su contraseña** en **ACTIVADO** en los valores del Directorio de nube. 


### Contraseña olvidada
Para iniciar el formulario de contraseña olvidada de {{site.data.keyword.appid_short_notm}}, pase la propiedad `show` de WebAppStrategy y establézcala en `WebAppStrategy.FORGOT_PASSWORD`.
  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: codeblock}

**Nota**:
* Si en los valores de su Directorio de nube, **Permitir a los usuarios iniciar sesión sin verificación de correo electrónico** se establece en **No**, el proceso finaliza sin recuperar las señales de acceso y de ID de {{site.data.keyword.appid_short_notm}}.
* Asegúrese de establecer **Permitir a los usuarios registrarse y restablecer su contraseña** y **Correo electrónico de contraseña olvidada** en **ACTIVADO** en los valores del Directorio de nube. 

### Cambiar detalles
Para iniciar el formulario de cambiar detalles de {{site.data.keyword.appid_short_notm}}, pase la propiedad `show` de WebAppStrategy y establézcala en `WebAppStrategy.CHANGE_DETAILS`.
  ```javascript
  app.get("/change_details", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_DETAILS
  }));
  ```
  {: codeblock}

**Nota**:
* El usuario debe estar autenticado utilizando el Directorio de nube como proveedor de identidad.
* Asegúrese de establecer **Permitir a los usuarios registrarse y restablecer su contraseña** en **ACTIVADO** en los valores del Directorio de nube. 


### Cambiar contraseña
Para iniciar el formulario de cambiar contraseña de {{site.data.keyword.appid_short_notm}}, pase la propiedad `show` de WebAppStrategy y establézcala en `WebAppStrategy.CHANGE_PASSWORD`.
  ```javascript
  app.get("/change_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_PASSWORD
  }));
  ```
  {: codeblock}

**Nota**:
* El usuario debe estar autenticado utilizando el Directorio de nube como proveedor de identidad.
* Asegúrese de establecer **Permitir a los usuarios registrarse y restablecer su contraseña** en **ACTIVADO** en los valores del Directorio de nube. 
