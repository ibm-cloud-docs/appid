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

Con el widget de inicio de sesión, puede actualizar el flujo de inicio de sesión en cualquier momento sin tener que añadir, eliminar o cambiar el código fuente. Puede estar listo en cuestión de minutos utilizando el código proporcionado en las apps de ejemplo.
{: shortdesc}

**Nota**: Cuando configura proveedores de identidad social como Facebook, se utiliza el [flujo de otorgamiento de autorización de Oauth2](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html) para llamar al widget de inicio de sesión.

</br>

## Personalización del código de la app de ejemplo
{: #login-widget}

Puede personalizar la pantalla de inicio de sesión preconfigurada para mostrar el logotipo y los colores de su elección. Si desea mostrar la IU con su propia marca, consulte el [directorio en la nube](/docs/services/appid/cloud-directory.html).
{: shortdesc}

![Ejemplo de experiencia de inicio de sesión personalizada](/images/customize.gif)

Para personalizar la pantalla:

1. Abra el panel de control del servicio de {{site.data.keyword.appid_short_notm}}.
2. Seleccione la sección **Personalización de inicio de sesión**, donde puede modificar el aspecto del widget de inicio de sesión para alinearlo con la marca de su empresa.
3. Suba el logotipo de su empresa seleccionando un archivo PNG o JPG del sistema local. El tamaño de imagen recomendado es de 320 x 320 píxeles. El tamaño de archivo máximo es 100 Kb.
4. Seleccione un color de cabecera para el widget desde el selector de color, o especifique el código hexadecimal para otro color.
5. Inspeccione el panel de vista previa y pulse **Guardar cambios** cuando esté satisfecho con las personalizaciones. Aparecerá un mensaje de confirmación.
6. Verifique sus cambios visitando su app. No es necesario que vuelva a compilar la app. Sus imágenes se almacenan en la base de datos de {{site.data.keyword.appid_short}} y se mostrarán la próxima vez que llame al widget de inicio de sesión.


</br>

## Llamada al widget de inicio de sesión con el SDK de Android
{: #android}

Con los proveedores de identidad social habilitados, puede llamar a la pantalla de inicio de sesión preconfigurada con el SDK de Android.
{: shortdesc}

1. Configure los proveedores de identidad.
2. Añada el mandato siguiente a su código.
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
        public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
            //Usuario autenticado
        }
        });
    ```
    {: codeblock}


</br>

## Llamada al widget de inicio de sesión con el SDK de iOS Swift
{: ios-swift}

Con los proveedores de identidad social habilitados, puede llamar a la pantalla de inicio de sesión preconfigurada con el SDK de iOS Swift.
{: shortdesc}

1. Configure los proveedores de identidad.
2. Añada el mandato siguiente al código de su app.
  ```swift
  import BluemixAppID
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, response:Response?) {
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

## Llamada al widget de inicio de sesión con el SDK de Node.js
{: #nodejs}

Con los proveedores de identidad social habilitados, puede llamar a la pantalla de inicio de sesión preconfigurada con el SDK de Node.js.
{: shortdesc}

1. Configure los proveedores de identidad.
2. Añada el mandato siguiente al código.
    ```JavaScript

    var express = require('express');
  var passport = require('passport');
  var WebAppStrategy = require('bluemix-appid').WebAppStrategy;
    ```
    {: codeblock}


</br>

## Llamada al widget de inicio de sesión con el SDK de Swift
{: #swift}

Con los proveedores de identidad social habilitados, puede llamar a la pantalla de inicio de sesión preconfigurada con el SDK de Swift.
{: shortdesc}

WebAppKituraCredentialsPlugin se basa en el flujo de concesión de código de autorización de OAuth2 y debe utilizarse para aplicaciones web que usan navegadores. El plugin proporciona herramientas para implementar flujos de autorización y autenticación. El plugin también proporciona mecanismos para detectar intentos no autenticados de acceder a los recursos protegidos y redirige automáticamente el navegador de un usuario a una página de autenticación. Tras la correcta autenticación, se conduce al usuario al URL de devolución de llamada de la aplicación web, que utiliza el plugin para obtener señales de acceso e identidad de {{site.data.keyword.appid_short_notm}}. Después de obtener estas señales, el plugin las almacena en una sesión HTTP bajo WebAppKituraCredentialsPlugin.AuthContext.

El código siguiente muestra cómo utilizar WebAppKituraCredentialsPlugin en una aplicación Kitura para proteger el punto final `/protected`.

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
