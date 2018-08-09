---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

---

{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:pre: .pre}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# Gestión de la experiencia de inicio de sesión

{{site.data.keyword.appid_full}} proporciona un widget de inicio de sesión que permite dar a los usuarios opciones de inicio de sesión seguras.
{: shortdesc}

Cuando la app está configurada para utilizar un proveedor de identidad, el widget de inicio de sesión dirigirá a los visitantes de su app a una pantalla de inicio de sesión. De forma predeterminada, cuando solo se establece en activado un proveedor, los visitantes serán redirigidos a dicha pantalla de autenticación de proveedores de identidad. Con el widget de inicio de sesión puede mostrar una pantalla de inicio de sesión predeterminada o, con el directorio en la nube, puede reutilizar la IU existente.

Puede actualizar su flujo de inicio de sesión en cualquier momento, sin cambiar el código fuente de ninguna forma.
{: tip}

El servicio utiliza tipos de concesión OAuth 2 para correlacionar el proceso de autorización. Cuando configura los proveedores de identidad social como Facebook, se utilizará el [flujo de concesión de autorización de Oauth 2](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html) para llamar al widget de inicio de sesión. Cuando visualice sus propias pantallas de IU, se utiliza el [flujo de Credenciales de contraseña del propietario de recursos](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html) para iniciar sesión y obtener señales de acceso y de identidad.


## Personalización de la pantalla de inicio de sesión predeterminada
{: #login-widget}

Puede personalizar la pantalla de inicio de sesión preconfigurada para mostrar el logotipo y los colores de su elección.
{: shortdesc}

Para personalizar la pantalla:

1. Abra el panel de control del servicio de {{site.data.keyword.appid_short_notm}}.
2. Seleccione la sección **Personalización de inicio de sesión**. Puede modificar el aspecto del widget de inicio de sesión para alinearlo con la marca de su empresa.
3. Suba el logotipo de su empresa seleccionando un archivo PNG o JPG del sistema local. El tamaño de imagen recomendado es de 320 x 320 píxeles. El tamaño de archivo máximo es 100 Kb.
4. Seleccione un color de cabecera para el widget desde el selector de color, o especifique el código hexadecimal para otro color.
5. Inspeccione el panel de vista previa y pulse **Guardar cambios** cuando esté satisfecho con las personalizaciones. Aparecerá un mensaje de confirmación.
6. En el navegador, renueve la página de inicio de sesión para verificar los cambios.


## Visualización de las pantallas predeterminadas
{: #default}

{{site.data.keyword.appid_short_notm}} proporciona una pantalla de inicio de sesión predeterminada que puede llamar si no tiene sus propias pantallas de IU para mostrar.
{: shortdesc}

Dependiendo de la configuración del proveedor de identidad, las pantallas que puede visualizar difieren. El servicio no proporciona funcionalidad avanzada para proveedores de identidad social porque no tenemos acceso nunca a la información de la cuenta de un usuario. Los usuarios tienen que ir al proveedor de identidad para gestionar su información. Por ejemplo, si querían cambiar su contraseña de Facebook, tendrían que ir a www.facebook.com.

Consulte la tabla siguiente para ver qué pantallas puede visualizar para cada tipo de proveedor de identidad.

<table>
  <thead>
    <tr>
      <th>Pantalla de visualización</th>
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

Después de haber configurado los valores para [proveedores de identidad social](/docs/services/appid/identity-providers.html), y [directorio en la nube](/docs/services/appid/cloud-directory.html), pulse en el idioma de su elección en la imagen siguiente para empezar a implementar el código.


Pulse en el idioma de su elección en la imagen siguiente para empezar a implementar el código.

<img usemap="#default-options-map" border="0" class="image" id="options" src="images/default-options.png" width="750" alt="Pulse un icono del lenguaje SDK para empezar con el directorio en la nube en sus apps." style="width:750px;" />
<map name="default-options-map" id="default-options-map">
<area href="login-widget.html#android" alt="Gestión de la experiencia de inicio de sesión con el SDK de Android" shape="rect" coords="113, 8, 224, 123" />
<area href="login-widget.html#ios-swift" alt="Gestión de la experiencia de inicio de sesión con el SDK de iOS Swift." shape="rect" coords="251, 12, 362, 127" />
<area href="login-widget.html#nodejs" alt="Gestión de la experiencia de inicio de sesión con el SDK de Node.js." shape="rect" coords="387, 10, 498, 125" />
<area href="login-widget.html#swift" alt="Gestión de la experiencia de inicio de sesión con el SDK de Swift." shape="rect" coords="525, 10, 636, 125" />
</map>
</br>

### Visualización de las pantallas predeterminadas con el SDK de Android
{: #android}

Puede llamar las pantallas preconfiguradas con el SDK de Android.
{: shortdesc}

</br>

**Iniciar la sesión**
1. Añada el mandato siguiente a su código.
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
  {: pre}

</br>
**Registrarse**

1. Establezca **Permitir a los usuarios registrarse y restablecer su contraseña** en **Activado** en los valores del directorio en la nube.
2. Llame a LoginWidget para iniciar el flujo de registro.
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
  		 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
  			 if (accessToken != null && identityToken != null) {
  			 } else {
  			 }

  		 }
  	 });
  ```
  {: pre}

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
   			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
   			 }
   		 });
    ```
    {: pre}

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
  			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
  			 }
  		 });
   ```
   {: pre}

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
   			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
   			 }
   		 });
   ```
   {: pre}
</br>
</br>

### Visualización de las pantallas predeterminadas con el SDK de Swift de iOS
{: #ios-swift}

Puede llamar las pantallas preconfiguradas con el SDK de Swift de iOS.
{: shortdesc}

</br>
**Iniciar la sesión**

1. Añada el mandato siguiente a su código.
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
  {: pre}


</br>
**Registrarse**

1. Establezca **Permitir a los usuarios registrarse y restablecer su contraseña** en **Activado** en los valores del directorio en la nube.
2. Llame a LoginWidget para iniciar el flujo de registro.
  ```swift
  class delegate : AuthorizationDelegate {
    public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?) {
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

1. Establezca **Permitir a los usuarios registrarse y restablecer su contraseña** y **Correo electrónico de contraseña olvidada** en **Activado** en los valores del directorio en la nube.
2. Llame al LoginWidget para iniciar el flujo de contraseña olvidada.
  ```swift
  class delegate : AuthorizationDelegate {
     public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?) {
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
**Detalles de la cuenta**

1. Establezca **Permitir a los usuarios registrarse y restablecer su contraseña** en **Activado** en los valores del directorio en la nube.
2. Llame al LoginWidget para iniciar el flujo de cambio de detalles.
  ```swift

   class delegate : AuthorizationDelegate {
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?) {
       }

       public func onAuthorizationCanceled() {
     }

       public func onAuthorizationFailure(error: AuthorizationError) {
     }
   }

   AppID.sharedInstance.loginWidget?.launchChangeDetails(delegate: delegate())
  ```
  {: pre}

</br>
**Cambiar contraseña**

1. Establezca **Permitir a los usuarios registrarse y restablecer su contraseña** en **Activado** en los valores del directorio en la nube.
2. Llame al LoginWidget para iniciar el flujo de cambio de contraseña.
  ```swift
   class delegate : AuthorizationDelegate {
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?) {
       }

       public func onAuthorizationCanceled() {
     }

       public func onAuthorizationFailure(error: AuthorizationError) {
     }
    }

    AppID.sharedInstance.loginWidget?.launchChangePassword(delegate: delegate())
  ```
  {: pre}
</br>
</br>

### Visualización de las pantallas predeterminadas con el SDK de Node.js
{: #nodejs}

Puede llamar las pantallas preconfiguradas con el SDK de Node.js.
{: shortdesc}

</br>
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

</br>
**Registrarse**

1. Establezca **Permitir a los usuarios registrarse y restablecer su contraseña** en **Activado** en los valores del directorio en la nube. Si se establece en no, el proceso finaliza sin recuperar las señales de acceso e identidad.
2. Pase la propiedad `show` de WebAppStrategy y establézcala en `WebAppStrategy.SIGN_UP`.
  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: pre}

</br>
**Contraseña olvidada**

1. Establezca **Permitir a los usuarios registrarse y restablecer su contraseña** y **Correo electrónico de contraseña olvidada** en **Activado** en los valores del directorio en la nube. Si se establece en no, el proceso finaliza sin recuperar las señales de acceso e identidad.
2. Pase la propiedad `show` de WebAppStrategy y establézcala en `WebAppStrategy.FORGOT_PASSWORD`.
  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: pre}

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
  {: pre}

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
  {: pre}

</br>
</br>
### Visualización de la IU predeterminada con el SDK de Swift
{: #swift}

Con los proveedores de identidad social habilitados, puede llamar a la pantalla de inicio de sesión preconfigurada con el SDK de Swift.
{: shortdesc}

1. El código siguiente muestra cómo utilizar WebAppKituraCredentialsPlugin en una app Kitura para proteger el punto final `/protected`.

  ```swift
  import Foundation
  import Kitura
  import KituraSession
  import Credentials
  import SwiftyJSON
  import BluemixAppID

  // Los siguientes URL se utilizarán para flujos AppID OAuth
  var LOGIN_URL = "/ibm/bluemix/appid/login"
  var CALLBACK_URL = "/ibm/bluemix/appid/callback"
  var LOGOUT_URL = "/ibm/bluemix/appid/logout"
  var LANDING_PAGE_URL = "/index.html"

  // Configure Kitura para utilizar el middleware de sesión
  // Debe configurarse con el almacenamiento de sesión adecuado para entornos
  // de producción. Consulte https://github.com/IBM-Swift/Kitura-Session para
  // obtener documentación adicional
  let router = Router()
  let session = Session(secret: "Some secret")
  router.all(middleware: session)

  let options = [
  	"clientId": "{client-id}",
  	"secret": "{secret}",
  	"tenantId": "{tenant-id}",
  	"oauthServerUrl": "{oauth-server-url}",
  	"redirectUri": "{app-url}" + CALLBACK_URL
  ]
  let webappKituraCredentialsPlugin = WebAppKituraCredentialsPlugin(options: options)
  let kituraCredentials = Credentials()
  kituraCredentials.register(plugin: webappKituraCredentialsPlugin)

  // Punto final de inicio de sesión explícito
  router.get(LOGIN_URL,
  		   handler: kituraCredentials.authenticate(credentialsType: webappKituraCredentialsPlugin.name,
  												   successRedirect: LANDING_PAGE_URL,
  												   failureRedirect: LANDING_PAGE_URL
  ))

  // Devolución de llamada para finalizar el proceso de autorización. Se recuperarán las señales de acceso e identidad de AppID
  router.get(CALLBACK_URL,
  		   handler: kituraCredentials.authenticate(credentialsType: webappKituraCredentialsPlugin.name,
  												   successRedirect: LANDING_PAGE_URL,
  												   failureRedirect: LANDING_PAGE_URL
  ))

  // Punto final de cierre de sesión. Borra la información de autenticación de la sesión
  router.get(LOGOUT_URL, handler:  { (request, response, next) in
  	kituraCredentials.logOut(request: request)
  	webappKituraCredentialsPlugin.logout(request: request)
  	_ = try? response.redirect(LANDING_PAGE_URL)
  })

  // Área protegida
  router.get("/protected", handler: kituraCredentials.authenticate(credentialsType: webappKituraCredentialsPlugin.name), { (request, response, next) in
      let appIdAuthContext:JSON? = request.session?[WebAppKituraCredentialsPlugin.AuthContext]
      let identityTokenPayload:JSON? = appIdAuthContext?["identityTokenPayload"]

      guard appIdAuthContext?.dictionary != nil, identityTokenPayload?.dictionary != nil else {
          response.status(.unauthorized)
          return next()
      }

      response.send(json: identityTokenPayload!)
      next()
  })
  var port = 3000
  if let portString = ProcessInfo.processInfo.environment["PORT"]{
      port = Int(portString)!
  }
  print("Starting on \(port)")

  // Añada un servidor HTTP y conéctelo al direccionador
  Kitura.addHTTPServer(onPort: port, with: router)

  // Inicie Kitura runloop (esta llamada nunca vuelve)
  Kitura.run()
  ```
  {: codeblock}
</br>
</br>


### Visualización de pantallas personalizadas con el SDK de Android
{: #branded-ui-android}

Con el directorio en la nube habilitado, puede llamar a pantallas personalizadas con el SDK de Android. Puede elegir la combinación de las pantallas con las que desea que sus usuarios puedan interactuar.<a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="blank">Consulte este blog<img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> para obtener un ejemplo detallado.
{: shortdesc}

</br>
**Iniciar la sesión**

1. Establezca **Directorio en la nube** en **Activado** como proveedor de identidad.
2. Añada el mandato siguiente a su código.
  ```java
  AppID.getInstance().signinWithResourceOwnerPassword(getApplicationContext(), username, password,
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
  {: pre}

</br>
</br>

### Visualización de pantallas personalizadas con el SDK de iOS Swift
{: #branded-ui-ios-swift}

Con el directorio en la nube habilitado, puede llamar a pantallas personalizadas con el SDK de Swift de iOS.
{: shortdesc}

</br>
**Iniciar la sesión**

1. En el separador de proveedor de identidad de la GUI, establezca el directorio en la nube en **Activado**.
2. Inicie la sesión utilizando la contraseña del propietario del recurso. Las señales de acceso e identidad se obtienen cuando un usuario intenta iniciar sesión utilizando su nombre de usuario y contraseña.
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
</br>

### Visualización de pantallas personalizadas con el SDK de Node.js
{: #branded-ui-nodejs}

Con el directorio en la nube habilitado, puede llamar a pantallas personalizadas con el SDK de Node.js. Puede elegir la combinación de las pantallas con que desea que sus usuarios puedan interactuar. Si elige un fondo Node.js, puede utilizar nuestro módulo de autoservicio que se encuentra en el SDK de Node.js de {{site.data.keyword.appid_short_notm}} (enlace).
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

</br>
</br>

## Visualización de pantallas personalizadas con la API
{: #branding}

Puede mostrar sus propias pantallas personalizadas y aprovechar las posibilidades de autenticación y autorización de {{site.data.keyword.appid_short_notm}}. Con el directorio en la nube como proveedor de identidad, sus usuarios pueden interactuar con su app requiriendo menos ayuda. Son capaces de iniciar la sesión, registrarse, restablecer su contraseña, etc., sin necesidad de solicitar ayuda.
{: shortdesc}

Para hacer esto posible, {{site.data.keyword.appid_short_notm}} expuso API REST. Puede utilizar la API REST para crear un servidor de fondo que sirva a sus apps web, o para interactuar con una app móvil con sus propias pantallas personalizadas.

La API de gestión está protegida con las señales generadas de IBM Cloud Identity and Access Management. Esto significa que los propietarios de las cuentas pueden especificar qué persona de su equipo tiene qué nivel de acceso para cada instancia de servicio. Para obtener más información sobre cómo funcionan juntos IAM y {{site.data.keyword.appid_short_notm}}, consulte [Gestión de acceso de servicio](/docs/services/appid/iam.html).

Cuando un usuario pulsa el inicio de sesión desde la pantalla personalizada, el [flujo de Credenciales de contraseña de propietario de recurso](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html) se utiliza para obtener acceso y señales de identidad directamente desde sus apps web o móviles.

Después de haber configurado los [valores](/docs/services/appid/cloud-directory.html),


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

Para actualizar su contraseña después de una solicitud de restablecimiento:

Proporcione los datos siguientes en el cuerpo de solicitud:
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
