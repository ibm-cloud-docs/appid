---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}


# Protección de recursos de fondo
{: #secure-back-end}

Puede utilizar el SDK del servidor de {{site.data.keyword.appid_short_notm}} para proteger y acceder a los puntos finales en las apps. También puede utilizar los SDK del cliente para acceder a recursos protegidos.
{: shortdesc}

Llamar un recurso protegido inicia el widget de inicio de sesión, si es necesario. Si ya se ha obtenido una señal válida, el widget de inicio de sesión no se inicia, y se accede al recurso directamente.
{: tip}

## Protección de recursos en Liberty for Java
{: #protecting-liberty}

Puede utilizar {{site.data.keyword.appid_short_notm}} para proteger los puntos finales de apps de IBM Liberty for Java. Liberty for Java tiene la capacidad incorporada para gestionar solicitudes de Open ID Connect (OIDC).
{: shortdesc}



Antes de empezar:
* Es necesario disponer de una <a href="https://console.bluemix.net/catalog/starters/liberty-for-java" target="_blank">app de Liberty for Java de {{site.data.keyword.Bluemix_notm}} <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> existente sin vincular. Para familiarizarse con el desarrollo de apps de Liberty for Java, consulte [la documentación](/docs/runtimes/liberty/index.html).
* Asegúrese de que tiene <a href="https://maven.apache.org/download.cgi" target="_blank">Apache Maven <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> instalado.
* Obtenga información sobre cómo funciona OIDC con Liberty for Java.



Para proteger sus recursos:

1. Descargue el ejemplo de Liberty for Java de la IU. El ejemplo contiene un archivo comprimido con los archivos Liberty estándares.
2. Siga las instrucciones que se proporcionan en la interfaz de usuario para desplegar la aplicación en IBM Cloud.
3. Abra la app en un navegador e inicie la sesión con sus credenciales para revisar las actividades de autenticación.

## Protección de recursos en Node.js
{: #protecting-resources-nodesdk}

El SDK del servidor de {{site.data.keyword.appid_short_notm}} proporciona una estrategia de pasaporte de ApiStrategy que se utiliza en apps de fondo que se despliegan en {{site.data.keyword.Bluemix_notm}}. Para proteger la app de accesos no autorizados, debe instrumentar el servidor Node.js con ApiStrategy. El `módulo appid-serversdk-nodejs npm` proporciona la estrategia de pasaporte ApiStrategy y el método de verificación para validar la señal de acceso y la señal de ID que emite {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

El SDK del servidor de {{site.data.keyword.appid_short_notm}} utiliza la <a href="http://passportjs.org/" target="_blank">infraestructura Passport <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> para imponer la autorización.

El siguiente fragmento de código muestra cómo utilizar `APIStrategy` en una app Express sencilla para proteger los métodos GET del punto final `/protected`.
  ```JavaScript

  var express = require('express');
  var passport = require('passport');
  var APIStrategy = require('ibmcloud-appid').APIStrategy;

  passport.use(new APIStrategy());
  var app = express();
  app.use(passport.initialize());

  app.get('/protected', passport.authenticate('APIStrategy.STRATEGY_NAME', {session: false }),
      function(request, response){
          console.log("Securty context", request.securityContext)
          response.send(200, "Success!");
      }
  );

  app.listen(process.env.PORT);
  ```
  {: codeblock}


## Protección de recursos con el SDK de Swift
{: #protecting-swift}

Puede utilizar {{site.data.keyword.appid_short_notm}} para proteger los recursos de lado del servidor utilizando el SDK de Swift.
{: shortdesc}

El SDK del servidor de Swift de {{site.data.keyword.appid_short_notm}} proporciona un plugin de middleware de protección de la API que se utiliza para proteger sus apps de fondo. Al asociar las API con el middleware, puede proteger la app de acceso no autorizado. Una vez que la API esté protegida, el middleware garantiza que las señales generadas por {{site.data.keyword.appid_short_notm}} estén validadas. Entonces podrá modificar el comportamiento de la API dependiendo de los resultados de la validación.

Consulte el siguiente fragmento de código para ver un ejemplo de cómo proteger la API de `/protectedendpoint`.

```Swift
import Foundation
import Kitura              // server
import Credentials         // middleware
import IBMCloudAppID       // SDK

// configurar rutas
let router = Router()

// opción obligatoria que se pasará si la app no está desplegada en IBM Cloud
let options = [
    "oauthServerUrl": "https://appid-oauth.ng.bluemix.net/oauth/v3/d8438de6-c325-4956-ad34-abd49194affd",
]
let apiCreds = Credentials()

// Versión de macOS mínima necesaria
if #available(OSX 10.12, *) {

    // configuración de la protección de la API
    let apiKituraCredentialsPlugin = APIKituraCredentialsPlugin(options: options)
    apiCreds.register(plugin: apiKituraCredentialsPlugin)

    // asociar ruta con protección de la API
    router.all(middleware: apiCreds)

    // crear API protegida
    router.get("/protectedendpoint") { request, response, next in

        response.headers["Content-Type"] = "text/html; charset=utf-8"
        do {
            if let userProfile = request.userProfile  {
                try response.status(.OK).send(
                    "<!DOCTYPE html><html><body>" +
                        "Welcome " + userProfile.displayName  +
                        "! You are logged in with " + userProfile.provider + ".
" +
                    "</body></html>\n\n").end()
                next()
                return
            }
            try response.status(.unauthorized).send(
                "<!DOCTYPE html><html><body>” + “You are not authorized!" +
                "</body></html>\n\n").end()
        }
        catch {}
        next()
    }

    // Iniciar el servidor
    Kitura.addHTTPServer(onPort: 8090, with: router)

    Kitura.run()  
}
```


## Acceso a recursos protegidos con el SDK de Swift de iOS
{: #requesting-swift}

Puede utilizar {{site.data.keyword.appid_short_notm}} para proteger los puntos finales de apps de Swift de iOS.
{: shortdesc}

1. Importe BMSCore.
  ```swift
  import BMSCore
  ```
  {: codeblock}

2. Invoque una solicitud de recurso protegido.
  ```swift
  BMSClient.sharedInstance.initialize(bluemixRegion: AppID.<region>)
  BMSClient.sharedInstance.authorizationManager = AppIDAuthorizationManager(appid:AppID.sharedInstance)
  var request:Request =  Request(url: "<your protected resource url>")
  request.send(completionHandler: {(response:Response?, error:Error?) in
      //el código maneja la respuesta aquí
  })
  ```
  {: codeblock}


## Acceso a recursos protegidos con el SDK de Android
{: #requesting-android}

Puede utilizar {{site.data.keyword.appid_short_notm}} para proteger los puntos finales en las apps de Android.
{: shortdesc}

1. Invoque una solicitud de recurso protegido.
  ```java
  BMSClient bmsClient = BMSClient.getInstance();
  bmsClient.initialize(getApplicationContext(), AppID.REGION_UK);

  AppIDAuthorizationManager appIdAuthMgr = new AppIDAuthorizationManager(AppID.getInstance())
  bmsClient.setAuthorizationManager(appIdAuthMgr);

  Request request = new Request("<your protected resource url>", Request.GET);
  request.send(this, new ResponseListener() {
  @Override
		public void onSuccess (Response response) {
     //el código maneja la respuesta aquí
  }
  @Override
		public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
      //el código maneja el error aquí
  });
  ```
  {: codeblock}
