---

copyright:
  years: 2017
lastupdated: "2017-06-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# Cómo añadir {{site.data.keyword.appid_short_notm}} a una app existente

Puede utilizar {{site.data.keyword.appid_full}} con su aplicación existente para autenticar y almacenar información de perfil acerca de sus usuarios.


## Requisitos previos

* Una aplicación existente iOS Swift, Android, Node.js o Swift.
* Una instancia existente de {{site.data.keyword.appid_short_notm}}.


## Cómo añadir {{site.data.keyword.appid_short_notm}} a una app de Android existente

Puede añadir el servicio de ID de app a sus aplicaciones existentes de Android.

1. Añada el repositorio de JitPack a su archivo build.gradle raíz.

  ```gradle
  allprojects {
      		repositories {
         	 ...
         	 maven { url 'https://jitpack.io' }
	    }
  }
  ```
  {: pre}

2. Abra el archivo build.gradle de su aplicación, busque la sección de dependencias del archivo y añada una dependencia de compilación para el SDK del cliente de {{site.data.keyword.appid_short_notm}}.

  ```gradle
  dependencies {
      compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:1.+'
   }
  ```
  {: pre}

3. Busque la sección defaultConfig y añada la siguiente línea de código.

  ```gradle
  defaultConfig {
                         ...
            manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
  ```
  {: pre}

4. Sincronice el proyecto con Gradle.
5. Inicialice el SDK del cliente pasando los parámetros context, tenant ID y region al método initialize. Un lugar habitual, pero no obligatorio, donde poner el código de inicialización es en el método onCreate de la actividad principal de la aplicación de Android.

  ```Java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, <AppID.REGION>);
  ```
  {: pre}

  <table>
  <caption> Tabla 1. Explicación de componentes de mandatos </caption>
    <tr>
      <th> Componentes </th>
      <th> Descripción </th>
    </tr>
    <tr>
      <td> <i> tenantID </i> </td>
      <td> Puede encontrar este valor pulsando **Ver credenciales** en el separador **Credenciales de servicio** del panel de control del servicio. </td>
    </tr>
    <tr>
      <td> <i> AppID.REGION </i> </td>
      <td> Puede encontrar su región en la IU. Las opciones son `AppID.REGION_US_SOUTH`, `AppID.REGION_UK` o `AppID.REGION_Sydney`. </td>
    </tr>
  </table>

6. Después de inicializar el SDK del cliente de {{site.data.keyword.appid_short_notm}}, puede autenticar los usuarios ejecutando el widget de inicio de sesión.

  ```Java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launch(this, new AuthorizationListener() {
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
  {: pre}

  <table>
  <caption> Tabla 2. Explicación de componentes de mandatos </caption>
    <tr>
      <th> Componentes </th>
      <th> Descripción </th>
    </tr>
    <tr>
      <td> <i> onAuthorizationFailure </i> </td>
      <td> Se ha producido una excepción. </td>
    </tr>
    <tr>
      <td> <i> onAuthorizationCanceled </i> </td>
      <td> El usuario ha cancelado el proceso de autenticación. </td>
    </tr>
    <tr>
      <td> <i> onAuthorizationSuccess </i> </td>
      <td> El usuario se ha autenticado. </td>
    </tr>
  </table>

## Cómo añadir {{site.data.keyword.appid_short_notm}} a una app iOS Swift existente

1. Abra el podfile en el directorio de proyecto.
2. En el destino del proyecto, añada una dependencia para el pod de 'BluemixAppID'. Asegúrese de que el mandato `use_frameworks!` también esté bajo su destino.
3. Para descargar la dependencia de `BluemixAppID`, ejecute el mandato siguiente.

  ```
  pod install --repo-update
  ```
  {: pre}

4. Abra el proyecto Xcode y habilite el uso compartido de la cadena de claves. En **Valores de proyecto**, pulse **Prestaciones** > **Uso compartido de la cadena de claves**.
5. En **Valores de proyecto** > **Info** > **Tipos de URL**, añada un **Tipo de URL**. Rellene los recuadros de texto **Identificador** y **Esquema de URL** con el valor siguiente.

  ```
  $(PRODUCT_BUNDLE_IDENTIFIER)
  ```
  {: pre}

6. Añada la siguiente importación al archivo AppDelegate.swift.

  ```swift
  import BluemixAppID
  import BMSCore
  ```
  {: pre}

7. Inicialice el SDK del cliente pasando los parámetros de tenant ID y de region al método initialize. Un lugar habitual, pero no obligatorio, donde poner el código de inicialización es en el método application:didFinishLaunchingWithOptions: del AppDelegate de la aplicación.

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, bluemixRegion: <AppID.Region>)
  ```
  {: pre}

  <table>
  <caption> Tabla 3. Explicación de componentes de mandatos </caption>
    <tr>
      <th> Componentes </th>
      <th> Descripción </th>
    </tr>
    <tr>
      <td> <i> tenantID </i> </td>
      <td> Puede encontrar este valor pulsando **Ver credenciales** en el separador **Credenciales de servicio** del panel de control del servicio. </td>
    </tr>
    <tr>
      <td> <i> AppID.REGION </i> </td>
      <td> Puede encontrar su región en la IU. Las opciones son `AppID.REGION_US_SOUTH`, `AppID.REGION_UK` o `AppID.REGION_Sydney`. </td>
    </tr>
  </table>

8. Añada el código siguiente al archivo AppDelegate.

  ```swift
  func application(_ application: UIApplication, open url: URL, options :[UIApplicationOpenURLOptionsKey : Any]) -> Bool {
         	return AppID.sharedInstance.application(application, open: url, options: options)
      }
  class delegate : AuthorizationDelegate {
     public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, response:Response?) {
     }

     public func onAuthorizationCanceled() {
     }

     public func onAuthorizationFailure(error: AuthorizationError) {
     }
  }

  AppID.sharedInstance.loginWidget?.launch(delegate: delegate())
  ```
  {: pre}
  <table>
  <caption> Tabla 4. Explicación de componentes de mandatos </caption>
    <tr>
      <th> Componentes </th>
      <th> Descripción </th>
    </tr>
    <tr>
      <td> <i> onAuthorizationSuccess </i> </td>
      <td> El usuario se ha autenticado. </td>
    </tr>
    <tr>
      <td> <i> onAuthorizationCanceled </i> </td>
      <td> El usuario ha cancelado el proceso de autenticación. </td>
    </tr>
    <tr>
      <td> <i> onAuthorizationFailure </i> </td>
      <td> Se ha producido una excepción. </td>
    </tr>
  </table>

## Cómo añadir {{site.data.keyword.appid_short_notm}} a una app web Node.js existente

1. Añada el módulo `bluemix-appid` a la aplicación Node.js.

  ```javaScript
  npm install --save bluemix-appid
  ```
  {: pre}

2. Instale los módulos siguientes si no están instalados todavía.

  ```javaScript
  npm install --save express
  npm install --save passport
  npm install --save express-session
  ```
  {: pre}

3. Añada el código siguiente al archivo app.js para:
    * Configurar la app express para utilizar el middleware de sesión express. **Nota**: debe configurar el middleware con el almacenamiento de sesión adecuado para entornos de producción. Para obtener más información, consulte los [documentos de expressjs](https://github.com/expressjs/session).
    * Configurar passportjs con serialización y deserialización. Esto es necesario para que la sesión autenticada persista en todas las solicitudes HTTP. Para obtener más información, consulte los [documentos de passportjs](http://passportjs.org/docs).
    * Recuperar las señales de identidad y de acceso del servicio de ID de app ejecutando un mandato get en el URL de devolución de llamada.

  ```javaScript
  const express = require("express");
  const session = require("express-session");
  const passport = require("passport");
  const WebAppStrategy = require("bluemix-appid").WebAppStrategy;
  const app = express();
  const CALLBACK_URL = "/ibm/bluemix/appid/callback";
  app.use(session({
      secret: "123456",
      resave: true,
      saveUninitialized: true
    }));
  app.use(passport.initialize());
    app.use(passport.session());

    passport.use(new WebAppStrategy());
  passport.serializeUser(function(user, cb) {
      cb(null, user);
    });

    passport.deserializeUser(function(obj, cb) {
      cb(null, obj);
    });
  app.get(CALLBACK_URL, passport.authenticate(WebAppStrategy.STRATEGY_NAME));
  app.get("/protected", passport.authenticate(WebAppStrategy.STRATEGY_NAME), function(req, res)
    		res.json(req.user);
    });
  ```
  {: pre}

    **Nota**: el servicio se redirige en el orden siguiente:
    1. El URL original de la solicitud que ha desencadenado el proceso de autenticación, como haya persistido en la sesión HTTP clave `WebAppStrategy.ORIGINAL_URL`.
    2. Una redirección correcta, tal como se especifica en `passport.authenticate(name, {successRedirect: "...."}).`
    3. Raíz de la aplicación ("/")

4. Vuelva a desplegar la aplicación.


## Cómo añadir {{site.data.keyword.appid_short_notm}} a una aplicación web Swift existente

1. Abra el archivo `Package.swift` en el directorio de su app Swift y añada la dependencia `appid-serversdk-swift`.
  Por ejemplo:

    ```swift
    import PackageDescription

    let package = Package(
      dependencies: [
           	.Package(url: "https://github.com/ibm-cloud-security/appid-serversdk-swift.git", majorVersion: 1)
      ]
    )
    ```
    {: pre}

2. Añada el código siguiente a la aplicación Swift para:
    * Configurar Kitura para utilizar el middleware de sesión. **Nota**: debe configurar Kitura con el almacenamiento de sesión adecuado para entornos de producción. Para obtener más información, consulte [los documentos de Kitura](https://github.com/IBM-Swift/Kitura-Session).
    * Recuperar las señales de identidad y de acceso del servicio de ID de app ejecutando un mandato get en el URL de devolución de llamada.

  ```swift
  import Foundation
  import Kitura
  import KituraSession
  import Credentials
  import SwiftyJSON
  import BluemixAppID
  let router = Router()
  let session = Session(secret: "Some secret")
  router.all(middleware: session)
  let webappKituraCredentialsPlugin = WebAppKituraCredentialsPlugin()
  let kituraCredentials = Credentials()
  kituraCredentials.register(plugin: webappKituraCredentialsPlugin)
  router.get(CALLBACK_URL,
    handler: kituraCredentials.authenticate(credentialsType: webappKituraCredentialsPlugin.name,
      successRedirect: LANDING_PAGE_URL,
      failureRedirect: LANDING_PAGE_URL
      ))
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
  ```
  {: pre}

  <table>
  <caption> Tabla 6. Explicación de componentes de mandatos</caption>
    <tr>
      <th> Componentes </th>
      <th> Descripción </th>
    </tr>
    <tr>
      <td> <i> var CALLBACK_URL </i> </td>
      <td> /ibm/bluemix/appid/callback </td>
    </tr>
    <tr>
      <td> <i> var LANDING_PAGE_URL </i> </td>
      <td> /index.html </td>
    </tr>
    </table>

5. Vuelva a desplegar la aplicación.



## Cómo añadir {{site.data.keyword.appid_short_notm}} a una aplicación existente que no se ejecuta en {{site.data.keyword.Bluemix_notm}}


Si tiene una aplicación Node.js o Swift que no se ejecuta en Bluemix, puede configurar WebAppStrategy o WebAppKituraCredentialsPlugin para que trabajen de forma remota.


En su Node.js, sustituya `passport.use(new WebAppStrategy());` por el código siguiente.

  ```javaScript
  passport.use(new WebAppStrategy({
    	  tenantId: "{tenant-id}",
   	    clientId: "{client-id}",
      	secret: "{secret}",
      	oauthServerUrl: "{oauth-server-url}",
      	redirectUri: "{app-url}" + CALLBACK_URL
      }));
  ```
{: pre}

En su app Swift, sustituya `let webappKituraCredentialsPlugin = WebAppKituraCredentialsPlugin()` por el código siguiente.

  ```swift
  let options = [
        "clientId": "{client-id}",
  	"secret": "{secret}",
  	"tenantId": "{tenant-id}",
  	"oauthServerUrl": "{oauth-server-url}",
  	"redirectUri": "{app-url}" + CALLBACK_URL
  ]
    let webappKituraCredentialsPlugin = WebAppKituraCredentialsPlugin(options: options)
  ```
  {: pre}

<table>
<caption> Tabla 7. Explicación de componentes de mandatos para apps Swift y Node.js</caption>
  <tr>
    <th> Componentes </th>
    <th> Descripción </th>
  </tr>
  <tr>
    <td> <i> tenantID </i> </br> <i> clientID </i> </br> <i> secret </i> </br> <i> oauth-server-url </i> </br> </td>
    <td> Puede encontrar estos valores pulsando **Ver credenciales** en el separador **Credenciales de servicio** del panel de control del servicio. </td>
  </tr>
  <tr>
    <td> <i> app-url </i> </td>
    <td> El URL de la aplicación. </td>
  </tr>
  <tr>
    <td> <i> CALLBACK_URL </i> </td>
    <td> El URL de la página que ven los usuarios después de iniciar sesión. </td>
  </tr>
</table>
