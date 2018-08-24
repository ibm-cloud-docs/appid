---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}

# Cómo añadir {{site.data.keyword.appid_short}} a la app
{: #configuring}

Iniciación a {{site.data.keyword.appid_short}} configurando el servicio en la aplicación.
{: shortdesc}


## Configuración del SDK de Android
{: #android-setup}

Cree las apps de Android con el SDK del cliente de {{site.data.keyword.appid_short}}, inicialice el SDK, autentique usuarios, y realice solicitudes a recursos protegidos o no protegidos.
{:shortdesc}


### Antes de empezar
{: #before-android}

Necesita la siguiente información:
  * Una instancia del servicio de {{site.data.keyword.appid_short_notm}}.
  * Su ID de arrendatario. El ID de arrendatario es un identificador exclusivo que se utiliza para inicializar la app y se encuentra en el separador **Credenciales de servicio** del panel de control.
  * Su región de {{site.data.keyword.Bluemix}}. Puede encontrar su región consultando en la IU. El valor se utiliza para inicializar la app.
    <table><caption> Tabla 1. Regiones de {{site.data.keyword.Bluemix_notm}} y sus correspondientes valores de SDK</caption>
    <tr>
      <th>Región de {{site.data.keyword.Bluemix}}</th>
      <th>Valor de SDK</th>
    </tr>
    <tr>
      <td>Sur de EE.UU.</td>
      <td><code>AppID.REGION_US_SOUTH</code> </td>
    </tr>
    <tr>
      <td>Sídney</td>
      <td><code>AppID.REGION_SYDNEY </code></td>
    </tr>
    <tr>
      <td>Reino Unido</td>
      <td><code>AppID.REGION_UK </code></td>
    </tr>
    <tr>
      <td>Alemania</td>
      <td><code>AppID.REGION_GERMANY</code></td>
    </tr>
  </table>

  * Un <a href="https://developers.google.com/web/tools/setup/" target="_blank">proyecto de Android Studio <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>, configurado para funcionar con Gradle.

### Instalación del SDK
{: #install-android}

1. Cree un proyecto de Android Studio o abra uno ya existente.
2. Añada el repositorio de JitPack a su archivo `build.gradle` raíz.

  ```gradle
    allprojects {
	    repositories {
		    ...
		    maven { url 'https://jitpack.io' }
	    }
    }
  ```
  {: codeblock}

3. Busque la sección de dependencias del archivo `build.gradle` de la app y añada una dependencia de compilación para el SDK del cliente de {{site.data.keyword.appid_short_notm}}. **Nota**: Asegúrese de abrir el archivo para su app, no el archivo `build.gradle` del proyecto.

  ```gradle
   dependencies {
       compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:4.+'
   }
  ```
  {: codeblock}

5. Busque la sección `defaultConfig` y añada las siguientes líneas de código.

  ```gradle
  defaultConfig {
  ...
  manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
  ```
  {: codeblock}

6. Sincronice el proyecto con Gradle. Pulse **Tools > Android > Sync Project with Gradle Files**.

### Inicialización del SDK
{: #initialize-android}

Inicialice el SDK del cliente pasando los parámetros context, tenant ID y region al método initialize. Un lugar habitual, pero no obligatorio, donde poner el código de inicialización es en el método onCreate de la actividad principal de la aplicación de Android.

  ```java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, AppID.REGION_UK);
  ```
  {: codeblock}

  <table>
  <caption> Tabla. Explicación de componentes de mandatos </caption>
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
      <td> Puede encontrar su región en la IU. Las opciones son `AppID.REGION_US_SOUTH`, `AppID.REGION_UK`, `AppID.REGION_Sydney` o `AppID.REGION_Germany`. </td>
    </tr>
  </table>

Ya está listo para configurar los proveedores de identidad y empezar a autenticar usuarios. Para obtener más información, consulte el <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">Repositorio GitHub de Android de {{site.data.keyword.appid_short_notm}}<img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.


</br>

## Configuración del SDK de Swift de iOS
{: #ios-setup}

Cree las aplicaciones de Swift con el SDK del cliente de {{site.data.keyword.appid_short}}, inicialice el SDK, autentique usuarios y realice solicitudes a recursos protegidos y no protegidos.
{:shortdesc}


### Antes de empezar
{: #before-ios}

Necesita la siguiente información:
  * Una instancia de {{site.data.keyword.appid_short_notm}}.
  * Su ID de arrendatario. El ID de arrendatario es un identificador exclusivo que se utiliza para inicializar la app y se encuentra en el separador **Credenciales de servicio** del panel de control.
  * Su región de {{site.data.keyword.Bluemix_notm}}.
  Puede encontrar su región consultando en la IU. El valor se utiliza para inicializar la app.
  <table> <caption> Tabla. Regiones de {{site.data.keyword.Bluemix_notm}} y sus correspondientes valores de SDK </caption>
    <tr>
      <th>Región de {{site.data.keyword.Bluemix}}</th>
      <th>Valor de SDK</th>
    </tr>
    <tr>
      <td>Sur de EE.UU.</td>
      <td><code>AppID.REGION_US_SOUTH </code></td>
    </tr>
    <tr>
      <td>Sídney</td>
      <td><code>AppID.REGION_SYDNEY </code></td>
    </tr>
    <tr>
      <td>Reino Unido</td>
      <td><code>AppID.REGION_UK </code></td>
    </tr>
    <tr>
      <td>Alemania</td>
      <td><code>AppID.REGION_GERMANY</code></td>
    </tr>
  </table>

  * Un proyecto Xcode (versión 9.0.1 o superior).
  * CocoaPods (versión 1.1.0 o superior).


### Instalación del SDK
{: #install-ios}

El SDK del cliente de {{site.data.keyword.appid_short_notm}} se distribuye con CocoaPods, un gestor de dependencias para proyectos de Swift y de Objective-C Cocoa. CocoaPods descarga artefactos, y los pone a disposición de su proyecto.

1. Cree un proyecto de Xcode, o abra uno ya existente.
2. Abra o cree el podfile en el directorio de proyecto.
3. Tras el destino del proyecto, añada una dependencia para el pod 'IBMCloudAppID' y el mandato `use_frameworks!`.

  ```swift
  target '<yourTarget>' do
     use_frameworks!
     pod 'IBMCloudAppID'
  end
  ```
  {: codeblock}

4. Descargue la dependencia 'IBMCloudAppID'.

  ```swift
  pod install --repo-update
  ```
  {: codeblock}

6. Habilite la compartición de cadena de claves en el proyecto Xcode. Vaya a **Project Settings > Capabilities > Keychain Sharing** y seleccione **Enable keychain sharing**.
7. Abra **Project Settings > Info > URL Types**, y añada un **URL Type**. Coloque el valor siguiente en los recuadros de texto **Identificador** y **Esquema de URL**.
  ```
  $(PRODUCT_BUNDLE_IDENTIFIER)
  ```
  {: codeblock}


### Inicialización del SDK
{: #initialize-ios}

1. Inicialice el SDK del cliente pasando los parámetros de ID de arrendatario y region al método initialize. Un lugar habitual, pero no obligatorio, donde poner el código de inicialización es en el método `application:didFinishLaunchingWithOptions`: del AppDelegate de la aplicación Swift.

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, region: AppID.Region_UK)
  ```
  {: codeblock}

  <table>
  <caption> Tabla. Explicación de componentes de mandatos </caption>
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
      <td> Puede encontrar su región en la IU. Las opciones son `AppID.REGION_US_SOUTH`, `AppID.REGION_UK`, `AppID.REGION_Sydney` o `AppID.REGION_Germany`.</td>
    </tr>
  </table>

2. Añada la siguiente importación al archivo `AppDelegate`.

    ```swift
    import IBMCloudAppID
    ```
    {: codeblock}

3. Añada el código siguiente al archivo AppDelegate.

  ```swift
  func application( application: UIApplication, open url: URL, options :[UIApplicationOpenURLOptionsKey : Any]) -> Bool {
          return AppID.sharedInstance.application(application, open: url, options: options)
      }
  ```
  {: codeblock}

Ya está listo para configurar los proveedores de identidad y empezar a autenticar usuarios. Para obtener más información sobre el SDK de iOS, consulte el <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">Repositorio GitHub de iOS de {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.

</br>

## Configuración del SDK de Node.js
{: #nodejs-setup}

### Antes de empezar
{: #before-nodejs}

Asegúrese de que dispone de los siguientes requisitos previos listos para utilizar:
1. Instale la [CLI de IBM Cloud](../cli/index.html).
2. Implemente el servidor de Node.js con la <a href="http://expressjs.com/" target="_blank">infraestructura Express <img src="../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>. Para instalar la infraestructura Express, utilice la línea de mandatos para abrir el directorio con la app Node.js y ejecute el mandato siguiente:
  ```
  npm install --save express
  ```
  {: codeblock}
3. Instale Passport. Utilice la línea de mandatos para abrir el directorio con la app Node.js y ejecute el mandato siguiente:
  ```
  npm install --save passport
  ```
  {: codeblock}

**Nota**: otras infraestructuras utilizan infraestructuras `Express`, como LoopBack. Puede utilizar el SDK del servidor de {{site.data.keyword.appid_short_notm}} con cualquiera de estas infraestructuras.


### Instalación del SDK
{: #install-nodejs}

1. Desde la línea de mandatos, abra el directorio con su app Node.js.
2. Instale el servicio {{site.data.keyword.appid_short_notm}}.
  ```
  npm install --save ibmcloud-appid
  ```
  {: codeblock}

### Inicialización del SDK
{: #initialize}

1. Añada las siguientes definiciones de `require` al archivo `server.js`.
    ```
    const express = require('express');
    const session = require('express-session')
    const passport = require('passport');
    const WebAppStrategy = require("ibmcloud-appid").WebAppStrategy;
    const CALLBACK_URL = "/ibm/cloud/appid/callback";
    ```
    {: codeblock}

2. Configurar la app express para utilizar el middleware de sesión express. **Nota**: debe configurar el middleware con el almacenamiento de sesión adecuado para entornos de producción. Para obtener más información, consulte la <a href="https://github.com/expressjs/session" target="_blank">documentación de expressjs <img src="../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.
    ```
    const app = express();
    app.use(session({
        secret: "123456",
        resave: true,
        saveUninitialized: true
        }));
    app.use(passport.initialize());
    app.use(passport.session());
    ```
    {: codeblock}

3. Pase el ID de arrendatario y las credenciales para inicializar el SDK.
    ```
    passport.use(new WebAppStrategy({
    	  tenantId: "{tenant-id}",
   	    clientId: "{client-id}",
      	secret: "{secret}",
      	oauthServerUrl: "{oauth-server-url}",
      	redirectUri: "{app-url}" + CALLBACK_URL
      }));
    ```
    {: codeblock}

 <table summary="Componentes de mandato: apps Node.js">
  <caption>Componentes de mandato para apps Node.js</caption>
    <tr>
      <th>Componentes</th>
      <th>Descripción</th>
    </tr>
    <tr>
      <td><i> tenantID </i></td>
      <td>El ID de arrendatario es un identificador exclusivo que se utiliza para inicializar la app. Puede encontrar el valor en el panel de control de servicio de {{site.data.keyword.appid_short_notm}} pulsando **Ver credenciales** en el separador **Credenciales de servicio**.</td>
    </tr>
    <tr>
      <td><i> clientID </i> </br> <i> secret </i> </br> <i> oauth-server-url </i> </br> </td>
      <td>Puede encontrar estos valores pulsando **Ver credenciales** en el separador **Credenciales de servicio** del panel de control del servicio.</td>
    </tr>
    <tr><td><i>redirectUri</i></td>
    <td>El valor redirectUri se puede suministrar de tres maneras:</br>
        1. Manualmente en un nuevo WebAppStrategy({redirectUri: "...."})</br>
        2. Como variable de entorno denominada `redirectUri`</br>
        3. Si no se suministra de las formas anteriores, el SDK de App ID intentará recuperar el application_uri de la aplicación que se ejecuta en IBM Cloud y añadir un sufijo predeterminado "/ibm/cloud/appid/callback"</td>
    </tr>
    <tr>
      <td><i> CALLBACK_URL </i></td>
      <td>El URL de la página que ven los usuarios después de iniciar sesión.</td>
    </tr>
  </table>

4. Configurar passport con serialización y deserialización. Este paso de configuración es necesario para la persistencia de la sesión autenticada en las solicitudes HTTP. Para obtener más información, consulte la <a href="http://passportjs.org/docs" target="_blank">documentación de passport <img src="../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.

  ```
  passport.serializeUser(function(user, cb) {
    cb(null, user);
    });

  passport.deserializeUser(function(obj, cb) {
    cb(null, obj);
    });
  ```
  {: codeblock}

5. Añada el código siguiente al archivo `server.js` para emitir las redirecciones de servicio:
   ```
   app.get(CALLBACK_URL, passport.authenticate(WebAppStrategy.STRATEGY_NAME));
   app.get('/protected', passport.authenticate(WebAppStrategy.STRATEGY_NAME)), function(req, res)
        res.json(req.user);
   });
   ```
   {: codeblock}

   **Nota**: el servicio se redirige en el orden siguiente:
    1. El URL original de la solicitud que ha desencadenado el proceso de autenticación, como haya persistido en la sesión HTTP clave `WebAppStrategy.ORIGINAL_URL`.
    2. Una redirección correcta, tal como se especifica en `passport.authenticate(name, {successRedirect: "...."}).`
    3. Raíz de la aplicación ("/")

6. Vuelva a desplegar la aplicación.

Para obtener más información, consulte el <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">Repositorio GitHub de Node.js de {{site.data.keyword.appid_short_notm}} <img src="../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.

## Configuración del SDK de Swift
{: #swift-setup}

Proteja sus programas de fondo y API con el SDK del servidor de {{site.data.keyword.appid_short}}.
{:shortdesc}


### Antes de empezar
{: #before-swift}

Antes de trabajar con el SDK de Swift, debe tener los siguientes requisitos previos:

* MacOS o Linux
* OpenSSL 1.0.2 en Linux
* Instale Swift 3.0.2
* Instale Kitura 1.6


### Instalación del SDK
{: #install-swift}

1. Abra el archivo `Package.swift` en el directorio de su app Swift y añada la dependencia `appid-serversdk-swift`.

  ```swift
  let package = Package(
      name: “myApp",
      dependencies: [
          .package(url: "https://github.com/ibm-cloud-security/appid-serversdk-swift.git", .upToNextMinor(from: “4.0.0")),
      ],
      targets: [
          .target(
              name: "myApp",
              dependencies: ["IBMCloudAppID"]),
      ]
  )
  ```
  {: codeblock}

2. Para MacOS: al crear en la línea de mandatos, todos los paquetes deberían incluir los distintivos siguientes.
  ```
  swift build -Xlinker -L/usr/local/opt/openssl/lib -Xcc -I/usr/local/opt/openssl/include
  ```
  {: pre}

3. Utilice el mandato siguiente al crear un xcodeproject:
  ```
  swift package generate-xcodeproj --xcconfig-overrides openssl.xcconfig
  ```
  {: pre}

  Puede copiar openssl.xcconfig desde el <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">GitHub de Swift {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>
  {: tip}

4. Añada el código siguiente a la aplicación Swift para:
    * Configurar Kitura para utilizar el middleware de sesión. **Nota**: debe configurar Kitura con el almacenamiento de sesión adecuado para entornos de producción. Para obtener más información, consulte la <a href="https://github.com/IBM-Swift/Kitura-Session" target="_blank">documentación de Kitura <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.
    * Recuperar las señales de identidad y de acceso del servicio de {{site.data.keyword.appid_short_notm}} ejecutando un mandato get en el URL de devolución de llamada.

    ```swift
    import Foundation
    import Kitura
    import KituraSession
    import Credentials
    import SwiftyJSON
    import IBMCloudAppID
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
    {: codeblock}

5. Vuelva a desplegar la aplicación.

</br>

## Configuración del SDK de Liberty for Java
{: #lfj-setup}

Puede configurar {{site.data.keyword.appid_short_notm}} para trabajar con sus aplicaciones web de Liberty for Java.
{:shortdesc}

1. Añada una <a href="https://www.ibm.com/support/knowledgecenter/en/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/twlp_config_oidc_rp.html" target="_blank">característica OpenID <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> a su `server.xml`.

  ```xml
  <feature manager>
  <feature>appSecurity-2.0</feature>
  <feature>openidConnectClient-1.0</feature>  
  ```
  {: codeblock}

2. En la característica Open ID Connect Client, defina los marcadores siguientes. Posteriormente {{site.data.keyword.Bluemix_notm}} los rellena automáticamente. La variable del nombre de instancia debe coincidir exactamente con el nombre de la instancia de {{site.data.keyword.appid_short_notm}}.

  ```
  clientId='${cloud.services.AppID-Instance-Name.credentials.clientId}'
  clientSecret='${cloud.services.AppID-Instance-Name.credentials.clientSecret}'
  authorizationEndpointUrl='${cloud.services.AppID-Instance-Name.credentials.authorizationEndpointUrl}'
  tokenEndpointUrl='${cloud.services.AppID-Instance-Name.credentials.tokenEndpointUrl}'
  jwkEndpointUrl='${cloud.services.AppID-Instance-Name.credentials.jwkEndpointUrl}'
  issuerIdentifier='appid-oauth.ng.bluemix.net'
  tokenEndpointAuthMethod="basic"
  signatureAlgorithm="RS256"
  authFilterid="myAuthFilter"
  ```
  {: codeblock}

  **Nota**: la variable issuerIdentifier cambia según la región. Puede adoptar uno de los valores siguientes:
  * issuerIdentifier="appid-oauth.ng.bluemix.net"
  * issuerIdentifier="appid-oauth.eu-gb.bluemix.net"
  * issuerIdentifier="appid-oauth.au-syd.bluemix.net"</ul> </td>

3. Defina un filtro de autorización para especificar recursos protegidos. Si no se <a href="https://www.ibm.com/support/knowledgecenter/en/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/rwlp_auth_filter.html" target="_blank">define <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> un filtro, el servicio protegerá todos los recursos.
  ```
  <authFilter id="myAuthFilter">
             <requestUrl id="myRequestUrl" urlPattern="/protected" matchType="contains"/>
    </authFilter>
  ```
  {: codeblock}

4. En el archivo `server.xml`, defina el tipo de sujeto especial como ALL_AUTHENTICATED_USERS.

  ```xml
  <application type="war" id="ProtectedServlet" context-root="/appidSample"
  location="${server.config.dir}/apps/libertySample-1.0.0.war">
    <application-bnd>
        <security-role name="myrole">
        <special-subject type="ALL_AUTHENTICATED_USERS"/>
        </security-role>
            </application-bnd>
        </application>
  ```
  {: codeblock}

5. En el elemento `<application-bnd>`, <a href="https://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_authorization.html?cp=SSAW57_8.5.5&cm_mc_uid=18498555367014888859884&cm_mc_sid_50200000=1494855872" target="_blank">defina los roles <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> tal como se encuentran en su app web: `web.xml`.

  ```xml
  <security-role>
  <role-name>myrole</role-name>
  </security-role>

  <security-constraint>
  <web-resource-collection>
  <web-resource-name>ProtectedServlet</web-resource-name>
  <url-pattern>/ProtectedServlet/*</url-pattern>
  <http-method>GET</http-method>
  <http-method>PUT</http-method>
  <http-method>POST</http-method>
  <http-method>DELETE</http-method>
  </web-resource-collection>

  <auth-constraint>
  <role-name>myrole</role-name>
  </auth-constraint>
  <user-data-constraint>
  <transport-guarantee>NONE</transport-guarantee>
  </user-data-constraint>
  </security-constraint>
  ```
  {: codeblock}

6. Obtenga un certificado.

    a. En el panel de control {{site.data.keyword.appid_short_notm}}, pulso Credenciales del servicio.

    b. Pulse **Ver credenciales** y copie el `oauthServerUrl`.

    c. Añada `/token` al URL. Utilice Firefox para examinar la salida URL y obtener el certificado. Puede utilizar el URL siguiente como ejemplo.

    ```
    https://appid-oauth.ng.bluemix.net/oauth/v3/5d12852e-b0a0-46a3-9547-67a4a33a7164/token
    ```
    {: screen}

    d. En la barra de direcciones de Firefox, haga clic en el icono de bloqueo > **flecha hacia la derecha** > **más información** > **ver certificado**.

    e. En el separador **Seguridad**, pulse **Ver detalles** > **del certificado**.

    f. Exporte el certificado y guárdelo en su unidad local como archivo PEM.

7. Añada el certificado al archivo trustore.jks de Liberty for Java mediante la <a href="https://www.ibm.com/support/knowledgecenter/SSYKE2_6.0.0/com.ibm.java.security.component.60.doc/security-component/keytoolDocs/keytool_overview.html" target="_blank">keytool de Liberty <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> y añada una referencia al alias del certificado en el elemento de OIDC. El `archivo .jks` está en el directorio del servidor: **recursos** > **seguridad** > **<i>nombre del archivo de archivo de almacén de confianza</i>** > **`archivo .jks`**. Puede utilizar una de las opciones siguientes para añadir el certificado al archivo.

    * En el terminal, vaya a la carpeta de seguridad de Liberty for Java: wlp > usr > servers > <i>servername</i> > resources > security y utilice el mandato siguiente para añadir el certificado.

      ```
      keytool -importcert -keystore ./trust.jks -file ~/Documents/secbluemix.cer`
      ```
      {: codeblock}      

      **Nota**: `~/Documents/[certificatename].cer` demuestra la ubicación del archivo en la unidad local.

    * Puede utilizar el <a href="http://keystore-explorer.org/index.html" target="_blank">Explorador del almacén de claves <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> para añadir el certificado. Abra el Explorador del almacén de claves y seleccione **Abrir un almacén de clave existente**.

    **Nota**: el certificado puede caducar/cambiarse, en este caso debe actualizar el almacén de confianza con el nuevo certificado.

8. En el archivo `manifest.yml`, defina la instancia {{site.data.keyword.appid_short_notm}}.

  ```yml
  services:
  - <appid service name>

  Manifest.yml file example:
  applications:
  - name: LibertyExampl
  buildpack: liberty-for-java
  instances: 1
  random-route: true
  memory: 512M
  disk_quota: 1024M
  timeout: 180
  services:
  - AppID-Instance-Name
  ```
  {: codeblock}

    Un archivo `server.xml` de ejemplo que se configura para {{site.data.keyword.appid_short_notm}}:

  ```
  <?xml version="1.0" encoding="UTF-8"?>
  <server description="sample server">
      <featureManager>
        <feature>ssl-1.0</feature>
        <feature>servlet-3.1</feature>
        <feature>appSecurity-2.0</feature>
        <feature>openidConnectClient-1.0</feature>  
      </featureManager>
      <openidConnectClient id="MyDefaultRP"
         clientId='${cloud.services.AppID-Instance-Name.credentials.clientId}'
         clientSecret='${cloud.services.AppID-Instance-Name.credentials.clientSecret}'
         authorizationEndpointUrl='${cloud.services.AppID-Instance-Name.credentials.authorizationEndpointUrl}'
         tokenEndpointUrl='${cloud.services.AppID-Instance-Name.credentials.tokenEndpointUrl}'
         jwkEndpointUrl='${cloud.services.AppID-Instance-Name.credentials.jwkEndpointUrl}'
         issuerIdentifier='${cloud.services.AppID-Instance-Name.credentials.appid-oauth.ng.bluemix.net}'
         tokenEndpointAuthMethod="basic"
         signatureAlgorithm="RS256"
         authFilterid="myAuthFilter"/>
      <authFilter id="myAuthFilter">
               <requestUrl id="myRequestUrl" urlPattern="/protected" matchType="contains"/>
      </authFilter>
      <application type="war" id="ProtectedServlet" context-root="/appidSample" location="${server.config.dir}/apps/libertySample-1.0.0.war">
          <application-bnd>
              <security-role name="myrole">
                  <special-subject type="ALL_AUTHENTICATED_USERS" />
              </security-role>
          </application-bnd>
      </application>
   <applicationManager autoExpand="true"/>
  <keyStore id="defaultKeyStore" password="Password"/>
  <keyStore id="defaulttrustore" password="Liberty" location="<FileContainingCertificated>.jks"/>
  <ssl id="defaultSSLSettings" keyStoreRef="defaultKeyStore" trustStoreRef="defaulttrustore"/>
  <sslDefault sslRef="defaultSSLSettings"/>
      <httpEndpoint id="defaultHttpEndpoint" httpPort="9080" host="*" httpsPort="9443" />
      <applicationManager autoExpand="true"/>
  </server>
  ```
  {: codeblock}



</br>

## Cómo añadir {{site.data.keyword.appid_short_notm}} a una aplicación existente que no se ejecuta en {{site.data.keyword.Bluemix_notm}}
{: #existing}

Puede añadir {{site.data.keyword.appid_short_notm}} a las aplicaciones que no se ejecutan en {{site.data.keyword.Bluemix_notm}}. Puede ver algunos ejemplos en este tema, pero estos no son los únicos lenguajes con los que puede utilizar el servicio.

</br>

**Node.js **

En su Node.js, sustituya `passport.use(new WebAppStrategy());` por el código siguiente.

  ```
  passport.use(new WebAppStrategy({
    	  tenantId: "{tenant-id}",
   	    clientId: "{client-id}",
      	secret: "{secret}",
      	oauthServerUrl: "{oauth-server-url}",
      	redirectUri: "{app-url}" + CALLBACK_URL
      }));
  ```
  {: codeblock}

  <table>
  <caption> Tabla. Explicación de componentes de mandato para apps Node.js </caption>
    <tr>
      <th> Componentes </th>
      <th> Descripción </th>
    </tr>
    <tr>
      <td><code>tenant-id</code> </br> <code> clientID </code> </br> <code> secret </code> </br> <code> oauth-server-url </code> </br></td>
      <td> Puede encontrar estos valores pulsando **Ver credenciales** en el separador **Credenciales de servicio** del panel de control del servicio. </td>
    </tr>
    <tr>
      <td><code> app-url </code></td>
      <td>El URL de la aplicación.</td>
    </tr>
    <tr>
      <td><code> CALLBACK_URL </code></td>
      <td> El URL de la página que ven los usuarios después de iniciar sesión. </td>
    </tr>
  </table>

</br>

**Swift**

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
  {: codeblock}

  <table>
  <caption>Tabla. Explicación de componentes de mandato para apps Swift</caption>
    <tr>
      <th> Componentes </th>
      <th> Descripción </th>
    </tr>
    <tr>
      <td><code>tenant-id</code> </br> <code>clientID</code> </br> <code>secret</code> </br> <code>oauth-server-url</code> </br></td>
      <td> Puede encontrar estos valores pulsando **Ver credenciales** en el separador **Credenciales de servicio** del panel de control del servicio. </td>
    </tr>
    <tr>
      <td><code> app-url </code></td>
      <td>El URL de la aplicación.</td>
    </tr>
    <tr>
      <td><code> CALLBACK_URL </code></td>
      <td> El URL de la página que ven los usuarios después de iniciar sesión. </td>
    </tr>
  </table>


</br>

**Liberty for Java**

En las apps de Liberty for Java, siga los pasos de [Configuración del SDK de Liberty for Java](#lfj-setup), pero sustituya las variables del elemento de cliente de OIDC con el código siguiente.

  ```
  clientId='App ID client_ID'
  clientSecret='App Id Secret'      
  authorizationEndpointUrl='oauthServerUrl/authorization'       
  tokenEndpointUrl='oauthServerUrl/token'
  jwkEndpointUrl='oauthServerUrl/publickeys'
  issuerIdentifier='Changed according to the region'
  tokenEndpointAuthMethod="basic"
  signatureAlgorithm="RS256"
  authFilterid="myAuthFilter"
  trustAliasName="my.bluemix.certificate"
  ```
  {: codeblock}

  <table>
  <caption>Tabla. Variables del elemento de OIDC para las apps de Liberty for Java</caption>
    <tr>
      <th> Componente </th>
      <th> Descripción </th>
    </tr>
    <tr>
    <td><code> clientID </code> </br> <code> secret </code> </br> <code> oauth-server-url </code> </br></td>
    <td>Puede encontrar estos valores pulsando **Ver credenciales** en el separador **Credenciales de servicio** del panel de control del servicio.</td>
    </tr>
    <tr>
      <td><code> authorizationEndpointURL </code></td>
      <td> Añada `/authorization` al final de su oauthServerURL.</td>
    </tr>
    <tr>
      <td><code> tokenEndpointUrl </code></td>
      <td>Añada `/token` al final de su oauthServerURL.</td>
    </tr>
    <tr>
      <td><code> jwkEndpointUrl </code></td>
      <td>Añada `/publickeys` al final de su oauthServerURL.</td>
    </tr>
    <tr>
      <td><code> issuerIdentifier </code></td>
      <td>Cambia según la región. Puede adoptar uno de los valores siguientes: </br><ul><li>issuerIdentifier="appid-oauth.ng.bluemix.net" </br><li> issuerIdentifier="appid-oauth.eu-gb.bluemix.net" </br><li>issuerIdentifier="appid-oauth.au-syd.bluemix.net"</ul></td>
    </tr>
    <tr>
      <td><code> tokenEndpointAuthMethod </code></td>
      <td>Especificado como "basic".</td>
    </tr>
    <tr>
      <td><code> signatureAlgorithm </code></td>
      <td>Especificado como "RS256".</td>
    </tr>
    <tr>
      <td><code> authFilterid </code></td>
      <td>La lista de recursos para proteger.</td>
    </tr>
    <tr>
      <td><code> trustAliasName </code></td>
      <td>El nombre del certificado dentro del almacén de confianza.</td>
    </tr>
  </table>
