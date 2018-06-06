---

copyright:
  years: 2017, 2018
lastupdated: "2018-01-02"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


# Protección de recursos de fondo

Puede utilizar el SDK del servidor de {{site.data.keyword.appid_short_notm}} para proteger y acceder a los puntos finales en las apps. También puede utilizar los SDK del cliente para acceder a recursos protegidos.

**Nota**: Llamar a un recurso protegido inicia el widget de inicio de sesión, en caso necesario. Si ya se ha obtenido una señal válida, el widget de inicio de sesión no se inicia, y se accede al recurso directamente.

## Protección de recursos en Liberty for Java
{: #protecting-liberty}

Puede utilizar {{site.data.keyword.appid_short_notm}} para proteger los puntos finales de apps de IBM Liberty for Java. Liberty for Java tiene la capacidad integrada para gestionar solicitudes de Open ID Connect (OIDC).

Antes de empezar:
* Es necesario disponer de una [app de IBM Liberty for Java](https://console.bluemix.net/catalog/starters/liberty-for-java) desenlazada. Para familiarizarse con el desarrollo de apps de Liberty for Java, consulte [la documentación](/docs/runtimes/liberty/index.html).
* Asegúrese de que tenga instalado [Apache Maven](https://maven.apache.org/download.cgi).
* Obtenga información sobre cómo funciona OIDC con Liberty for Java.

Para proteger sus recursos:

1. Descargue el ejemplo de Liberty for Java de la IU. El ejemplo contiene un archivo zip con los archivos Liberty estándar.
2. Abra el terminal en el directorio en el que haya extraído el ejemplo.
3. Inicie la sesión en {{site.data.keyword.Bluemix_notm}} mediante la línea de mandatos Cloud Foundry. Cuando se le solicite, introduzca sus credenciales.

  ```
  cf login
  ```
  {: codeblock}

4. Despliegue la app. Al ejecutar el mandato siguiente se crea una instancia de Liberty for Java con un nombre relacionado con el tenantid.

  ```
  cf push
  ```
  {: codeblock}

5. Enlace su instancia de servicio a la nueva instancia de Liberty for Java y redespliegue la app.
6. Abra la app en un navegador e inicie la sesión con sus credenciales para revisar las actividades de autenticación.

## Protección de recursos en Node.js
{: #protecting-resources-nodesdk}

El SDK del servidor de {{site.data.keyword.appid_short_notm}} proporciona una estrategia de pasaporte de ApiStrategy que se utiliza en apps de fondo que se despliegan en {{site.data.keyword.Bluemix_notm}}. Para proteger la app de accesos no autorizados, debe instrumentar el servidor Node.js con ApiStrategy. El `módulo appid-serversdk-nodejs npm` proporciona la estrategia de pasaporte ApiStrategy y el método de verificación para validar la señal de acceso y la señal de ID que emite {{site.data.keyword.appid_short_notm}}.

El SDK del servidor de {{site.data.keyword.appid_short_notm}} utiliza la <a href="http://passportjs.org/" target="_blank">infraestructura Passport <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> para imponer la autorización.

El siguiente fragmento de código muestra cómo utilizar `APIStrategy` en una app Express sencilla para proteger los métodos GET del punto final `/protected`.

  ```JavaScript

  var express = require('express');
  var passport = require('passport');
  var APIStrategy = require('bluemix-appid').APIStrategy;

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


## Acceso a recursos protegidos con el SDK de Swift de iOS
{: #requesting-swift}

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
