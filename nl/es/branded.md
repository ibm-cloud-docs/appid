---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:tip: .tip}

# Gestión de marca en la app
{: #branding}

Puede mostrar sus propias pantallas personalizadas y aprovechar las posibilidades de autenticación y autorización de {{site.data.keyword.appid_full}}. Con el Directorio en la nube como proveedor de identidad, sus usuarios pueden interactuar con su app requiriendo menos ayuda. Son capaces de iniciar la sesión, registrarse, modificar su contraseña, etc., sin necesidad de solicitar ayuda.
{: shortdesc}

Cuando utilice sus propias pantallas, se utiliza el [flujo de ROPC (credenciales de contraseña de propietario de recurso)](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html).


## Gestión de marca en la app con el SDK de iOS Swift
{: #branded-ui-ios-swift}

Con el Directorio en la nube habilitado, puede llamar a las pantallas de su propia marca con el SDK de iOS Swift.
{: shortdesc}

</br>
**Iniciar la sesión**

1. En el separador de proveedor de identidad de la GUI, establezca el Directorio en la nube en **Activado**.
2. Llame al widget de inicio de sesión para iniciar el flujo de inicio de sesión. Las señales de acceso e identidad se obtienen cuando un usuario intenta iniciar sesión utilizando su nombre de usuario o correo electrónico y una contraseña.
  ```swift
  class delegate : TokenResponseDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
      //Usuario autenticado
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
      //Se ha producido una excepción
        }
  }

  AppID.sharedInstance.signinWithResourceOwnerPassword(username: username, password: password, delegate: delegate())
  ```
  {: pre}

</br>

**Registro**

1. En el separador de proveedor de identidad de la GUI, establezca el Directorio en la nube en **Activado**.
2. Establezca **Permitir a los usuarios registrarse y restablecer su contraseña** en **Activado** en los valores del Directorio en la nube.
3. Llame al widget de inicio de sesión para iniciar el flujo de registro.
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
  {: pre}

</br>

**Contraseña olvidada**

1. En el separador de proveedor de identidad de la GUI, establezca el Directorio en la nube en **Activado**.
2. Establezca **Permitir a los usuarios registrarse y restablecer su contraseña** en **Activado** en los valores del Directorio en la nube.
3. Llame al widget de inicio de sesión para iniciar el flujo de contraseña olvidada.
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
  {: pre}

</br>

**Cambiar detalles**

1. En el separador de proveedor de identidad de la GUI, establezca el Directorio en la nube en **Activado**.
2. Establezca **Permitir a los usuarios registrarse y restablecer su contraseña** en **Activado** en los valores del Directorio en la nube.
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
  {: pre}

</br>

**Cambio de contraseña**

1. En el separador de proveedor de identidad de la GUI, establezca el Directorio en la nube en **Activado**.
2. Establezca **Permitir a los usuarios registrarse y restablecer su contraseña** en **Activado** en los valores del Directorio en la nube.
3. Llame al widget de inicio de sesión para iniciar el flujo de cambio de detalles.
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
  {: pre}

</br>


## Gestión de marca en la app con el SDK de Android
{: #branded-ui-android}

Con el directorio en la nube habilitado, puede llamar a pantallas personalizadas con el SDK de Android. Puede elegir la combinación de las pantallas con las que desea que sus usuarios puedan interactuar.<a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="blank">Consulte este blog<img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> para obtener un ejemplo detallado.
{: shortdesc}

</br>

**Iniciar la sesión**

1. Establezca **Directorio en la nube** en **Activado** como proveedor de identidad.
2. Obtenga una señal de acceso, identidad y renovación proporcionando el nombre de usuario y la contraseña del usuario final.
3. Llame al widget de inicio de sesión para iniciar el flujo de inicio de sesión.
  ```java
  AppID.getInstance().signinWithResourceOwnerPassword(getApplicationContext(), username, password,
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

**Registro**

1. Establezca **Directorio en la nube** en **Activado** como proveedor de identidad.
2. Establezca **Permitir a los usuarios registrarse y restablecer su contraseña** en **Activado** en los valores del Directorio en la nube.
3. Llame al widget de inicio de sesión para iniciar el flujo de registro.
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

1. Establezca **Directorio en la nube** en **Activado** como proveedor de identidad.
2. Establezca **Permitir a los usuarios registrarse y restablecer su contraseña** en **Activado** en los valores del Directorio en la nube.
3. Llame al widget de inicio de sesión para iniciar el flujo de contraseña olvidada.
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
  {: pre}

</br>

**Cambiar detalles**

1. Establezca **Directorio en la nube** en **Activado** como proveedor de identidad.
2. Establezca **Permitir a los usuarios registrarse y restablecer su contraseña** en **Activado** en los valores del Directorio en la nube.
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
  {: pre}


</br>

**Cambio de contraseña**

1. Establezca **Directorio en la nube** en **Activado** como proveedor de identidad.
2. Establezca **Permitir a los usuarios registrarse y restablecer su contraseña** en **Activado** en los valores del Directorio en la nube.
3. Llame al widget de inicio de sesión para iniciar el flujo de cambio de contraseña.
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
  {: pre}

</br>
</br>


## Gestión de marca en la app con el SDK de Node.js
{: #branded-ui-nodejs}

Con el Directorio en la nube habilitado, puede llamar a pantallas personalizadas con el SDK de Node.js.
{: shortdesc}

**Iniciar la sesión**

Mediante WebAppStrategy, los usuarios pueden iniciar sesión en sus apps web con su nombre de usuario y una contraseña. Una vez que un usuario inicia sesión correctamente en la app, su señal de acceso persiste en una sesión HTTP durante el tiempo que se mantiene activa. Una vez que la sesión HTTP se cierra o caduca, la señal de acceso también se destruye.

1. Establezca el Directorio en la nube en **Activado** en los valores de proveedor de identidad y especifique un punto final de devolución de llamada.
2. Añada una ruta de envío a su app a la que pueda llamarse con los parámetros de nombre de usuario y contraseña e inicie la sesión con el flujo de contraseña del propietario del recurso.
  ```javascript
  app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true //permitir mensajes flash
  }));
  ```
  {: pre}
  <table>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="Icono de más información"/> Parámetros de mandato </th>
    </thead>
    <tbody>
      <tr>
        <td><code> successRedirect </code></td>
        <td>El URL al que desea redirigir al usuario tras una autenticación correcta.</td>
      </tr>
      <tr>
        <td><code> failureRedirect </code></td>
        <td>El URL al que desea redirigir al usuario si la autenticación falla.</td>
      </tr>
      <tr>
        <td><code> failureFlash </code></td>
        <td>Si se establece en <code>true</code>, se devuelve un mensaje de error desde el servicio del Directorio en la nube. De manera predeterminada, el valor se establece en <code>false</code>.</td>
      </tr>
    </tbody>
  </table>

  1. Si envía la solicitud en formato HTML, puede utilizar middleware [analizador de cuerpo](https://www.npmjs.com/package/body-parser).
  2. Para obtener el mensaje de error devuelto, puede utilizar [connect-flash](https://www.npmjs.com/package/connect-flash). Para obtener más información, consulte el [ejemplo de app web](https://github.com/ibm-cloud-security/appid-serversdk-nodejs/blob/master/samples/web-app-sample.js).
  {: tip}

</br>
**Registrarse**

1. Establezca el Directorio en la nube en **Activado** en los valores de proveedor de identidad y especifique un punto final de devolución de llamada.
2. Establezca **Permitir a los usuarios registrarse y restablecer su contraseña** en **Activado** en los valores del Directorio en la nube.
3. Establezca **Permitir a los usuarios iniciar sesión sin verificación de correo electrónico** en **No**. De lo contrario, las señales de identidad y acceso de {{site.data.keyword.appid_short_notm}} no se podrán recuperar.
4. Añada una ruta de envío a su app a la que pueda llamarse con los parámetros de nombre de usuario y contraseña e inicie la sesión con el flujo de contraseña del propietario del recurso.
  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: pre}

</br>

**Contraseña olvidada**

1. Establezca el Directorio en la nube en **Activado** en los valores de proveedor de identidad y especifique un punto final de devolución de llamada.
2. Establezca **Permitir a los usuarios registrarse y restablecer su contraseña** en **Activado** en los valores del Directorio en la nube.
3. Establezca **Correo electrónico de contraseña olvidada** en **Activado**.
4. Pase la propiedad *show* a `WebAppStrategy.FORGOT_PASSWORD` para abrir el formulario de contraseña olvidada.
  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: pre}

</br>

**Cambiar detalles**

1. Establezca el Directorio en la nube en **Activado** en los valores de proveedor de identidad y especifique un punto final de devolución de llamada.
2. Establezca **Permitir a los usuarios registrarse y restablecer su contraseña** en **Activado** en los valores del Directorio en la nube.
3. Verifique que el usuario se haya autenticado previamente con {{site.data.keyword.appid_short_notm}}.
4. Pase la propiedad *show* a `WebAppStrategy.CHANGE_DETAILS` para abrir el formulario de contraseña olvidada.
  ```javascript
  app.get("/change_details", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_DETAILS
  }));
  ```
  {: pre}

</br>

## Gestión de marca en la app con la API
{: #branded-ui-api}

Puede mostrar sus propias pantallas personalizadas y aprovechar las posibilidades de autenticación y autorización de {{site.data.keyword.appid_short_notm}}. Con el directorio en la nube como proveedor de identidad, sus usuarios pueden interactuar con su app requiriendo menos ayuda. Son capaces de iniciar la sesión, registrarse, restablecer su contraseña, etc., sin necesidad de solicitar ayuda.
{: shortdesc}

Para hacer esto posible, {{site.data.keyword.appid_short_notm}} expone API REST. Puede utilizar la API REST para crear un servidor de fondo que sirva a sus apps web, o para interactuar con una app móvil con sus propias pantallas personalizadas.

La API de gestión está protegida con las señales generadas de IBM Cloud Identity and Access Management. Esto significa que los propietarios de las cuentas pueden especificar qué persona de su equipo tiene qué nivel de acceso para cada instancia de servicio. Para obtener más información sobre cómo funcionan juntos IAM y {{site.data.keyword.appid_short_notm}}, consulte [Gestión de acceso de servicio](/docs/services/appid/iam.html).

Después de haber configurado los [valores](/docs/services/appid/cloud-directory.html), puede llamar a los siguientes puntos finales para visualizar cada pantalla.


**Regístrese**
Puede utilizar el punto final `/sign_up` para permitir que los usuarios se registren ellos mismos para su app.
Proporcione los datos siguientes en el cuerpo de solicitud:
  * Su tenantID.
  * Datos de usuario del directorio en la nube. Consulte [Representación de usuario completo de SCIM](https://tools.ietf.org/html/rfc7643#section-8.2) para obtener más detalles.
    * Un atributo `password`.
    * En la matriz de correo electrónico con un atributo `primary` establecido en `true`, debe tener al menos una dirección de correo electrónico.

Dependiendo de las [configuraciones de correo electrónico](/docs/services/appid/cloud-directory.html), un usuario podría recibir una solicitud para su verificación, o un correo electrónico que le da la bienvenida cuando se registra para su app. Ambos tipos de correos electrónicos se desencadenan cuando un usuario se registra para su app. El correo electrónico de verificación contiene un botón **Verificar**. Después de pulsar el botón y confirmar su identidad, se mostrará una pantalla mediante {{site.data.keyword.appid_short_notm}} que agradece al usuario que se haya verificado.  

Puede presentar su propia página postverificación:

1. Vaya al separador **Páginas de destino personalizadas** del panel de control de {{site.data.keyword.appid_short_notm}}.
2. Especifique el URL para la página de destino en el **URL para su página de verificación de dirección de correo electrónico personalizada**

Cuando se proporcione este valor, {{site.data.keyword.appid_short_notm}} llama al URL junto con una consulta `context`. Cuando llama al punto final `/sign_up/confirmation_result` y pasa el parámetro `context` recibido, el resultado le indica si el usuario ha verificado su cuenta. Si lo ha hecho, puede mostrar su página personalizada.

</br>
**Contraseña olvidada**

Puede utilizar el punto final `/forgot_password` para permitir que los usuarios recuperen su contraseña si la olvidan.

Proporcione los datos siguientes en el cuerpo de solicitud:
  * Su tenantID.
  * El correo electrónico del usuario del directorio en la nube.

Cuando se llame al punto final, se enviará un correo electrónico de restablecimiento de contraseña al usuario. El correo electrónico contiene un botón **Restablecer**. Una vez que pulsen el botón, se mostrará una pantalla mediante {{site.data.keyword.appid_short_notm}} que les permite restablecer su contraseña.

Puede presentar su propia página de restablecimiento de contraseña:

1. Vaya al separador **Páginas de destino personalizadas** del panel de control de {{site.data.keyword.appid_short_notm}}.
2. Especifique el URL de la página de destino en el **URL para su página de restablecimiento de contraseña personalizada**  

Cuando se proporcione este valor, {{site.data.keyword.appid_short_notm}} llama al URL junto con una consulta `context`. El parámetro `context` se utiliza para recibir el resultado cuando se llame a `/forgot_password/confirmation_result`. Si el resultado es correcto, puede mostrar su página personalizada.

Añada una serie aleatoria a la página de restablecimiento de contraseña personalizada y pásela a su programa de fondo cuando se envíe la solicitud. Haga que el manejador valide la serie y llame al punto final `/change_password` solo si es válido. De esta manera, puede reducir la vulnerabilidad del punto final de programa de fondo del programa de fondo.
{: tip}

</br>
**Cambiar contraseña**

Puede utilizar el punto final `/change_password` de dos formas. Cuando un usuario envía una solicitud de restablecimiento, o cuando un usuario ha iniciado sesión en la app y desea actualizar su contraseña.

Proporcione los datos siguientes en el cuerpo de solicitud para actualizar su contraseña después de una solicitud de restablecimiento:
  * Su tenantID.
  * La nueva contraseña de los usuarios.
  * El UUID del usuario del directorio en la nube.
  * Opcional: la dirección IP desde la que se ha realizado el restablecimiento de contraseña. Si elige pasar la dirección IP, el marcador `%{passwordChangeInfo.ipAddress}` estará disponible para la plantilla de correo electrónico de cambio de contraseña.

Dependiendo de la configuración, cuando se modifica una contraseña, {{site.data.keyword.appid_short_notm}} podría enviar un correo electrónico al usuario haciéndole saber que hubo un cambio.

</br>
Para permitir a los usuarios cambiar su contraseña mientras estén dentro de su app:

Proporcione los datos siguientes en el cuerpo de solicitud:
  * Su tenantID.
  * La nueva contraseña de los usuarios.
  * El UUID del usuario del directorio en la nube.

La página de cambio de contraseña debe aparecerle al usuario para que especifique su contraseña actual y su nueva contraseña.
{: tip}

El programa de fondo valida la contraseña actual del usuario con la API ROP, y si es válida, llama al punto final con la contraseña nueva. Dependiendo de la configuración, cuando se modifica una contraseña, {{site.data.keyword.appid_short_notm}} podría enviar un correo electrónico al usuario haciéndole saber que hubo un cambio.

</br>
**Reenviar**

Puede utilizar `/resend/{templateName}` para volver a enviar un correo electrónico cuando un usuario no lo recibe por cualquier motivo.

Proporcione los datos siguientes en el cuerpo de solicitud:
  * El tenantID.
  * El nombre de la plantilla.
  * El UUID del usuario del directorio en la nube.


**Cambiar detalles**

Cuando un usuario haya iniciado sesión en su app, puede actualizar una parte de su información. Puede utilizar `/Users/{userId}` para obtener y actualizar su información.

Cuando se actualizan los detalles de usuario, el punto final obtiene los datos de usuario actualizados en el cuerpo de solicitud en [formato SCIM](https://tools.ietf.org/html/rfc7643#section-8.2). Asegúrese de cambiar únicamente los detalles relevantes.

Su dirección de correo electrónico no se puede cambiar.
{: tip}
