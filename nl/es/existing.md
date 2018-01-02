---

copyright:
  years: 2017
lastupdated: "2017-12-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


# Cómo añadir {{site.data.keyword.appid_short_notm}} a una app existente

Puede utilizar {{site.data.keyword.appid_full}} con su aplicación existente para autenticar y almacenar información de perfil acerca de sus usuarios.


## Requisitos previos

* Una aplicación existente de iOS Swift, Android, Node.js, Swift o Liberty for Java.
* Una instancia existente de {{site.data.keyword.appid_short_notm}}.


## Cómo añadir {{site.data.keyword.appid_short_notm}} a una app de Android existente
{: #existing-android}

Puede añadir el servicio {{site.data.keyword.appid_short_notm}} a sus aplicaciones de Android existentes.

1. Añada el repositorio de JitPack a su archivo `build.gradle` raíz.

  ```gradle
  allprojects {
      		repositories {
         	 ...
         	 maven { url 'https://jitpack.io' }
	    }
  }
  ```
  {: codeblock}

2. Abra el archivo `build.gradle` de su aplicación, busque la sección de dependencias del archivo y añada una dependencia de compilación para el SDK del cliente de {{site.data.keyword.appid_short_notm}}.

  ```gradle
  dependencies {
      compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:1.+'
   }
  ```
  {: codeblock}

3. Busque la sección defaultConfig y añada la siguiente línea de código.

  ```gradle
  defaultConfig {
                         ...
            manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
  ```
  {: codeblock}

4. Sincronice el proyecto con Gradle.
5. Inicialice el SDK del cliente pasando los parámetros context, tenant ID y region al método initialize. Un lugar habitual, pero no obligatorio, donde poner el código de inicialización es en el método onCreate de la actividad principal de la aplicación de Android.

  ```Java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, <AppID.REGION>);
  ```
  {: codeblock}

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
  {: codeblock}

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
{: #existing-ios}

1. Abra el podfile en el directorio de proyecto.
2. En el destino del proyecto, añada una dependencia para el pod de 'BluemixAppID'. Asegúrese de que el mandato `use_frameworks!` también esté bajo su destino.
3. Para descargar la dependencia de `BluemixAppID`, ejecute el mandato siguiente.

  ```
  pod install --repo-update
  ```
  {: codeblock}

4. Abra el proyecto Xcode y habilite el uso compartido de la cadena de claves. En **Valores de proyecto**, pulse **Prestaciones** > **Uso compartido de la cadena de claves**.
5. En **Valores de proyecto** > **Info** > **Tipos de URL**, añada un **Tipo de URL**. Rellene los recuadros de texto **Identificador** y **Esquema de URL** con el valor siguiente.

  ```
  $(PRODUCT_BUNDLE_IDENTIFIER)
  ```
  {: codeblock}

6. Añada la siguiente importación al archivo `AppDelegate.swift`.

  ```swift
  import BluemixAppID
  import BMSCore
  ```
  {: codeblock}

7. Inicialice el SDK del cliente pasando los parámetros de tenant ID y de region al método initialize. Un lugar habitual, pero no obligatorio, donde poner el código de inicialización es en el método application:didFinishLaunchingWithOptions: del AppDelegate de la aplicación.

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, bluemixRegion: <AppID.Region>)
  ```
  {: codeblock}

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
  {: codeblock}

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
{: #existing-node}

1. Añada el módulo `bluemix-appid` a la aplicación Node.js.

  ```javaScript
  npm install --save bluemix-appid
  ```
  {: codeblock}

2. Instale los módulos siguientes si no están instalados todavía.

  ```javaScript
  npm install --save express
  npm install --save passport
  npm install --save express-session
  ```
  {: codeblock}

3. Añada el código siguiente al archivo `app.js` para:
    * Configurar la app express para utilizar el middleware de sesión express. **Nota**: debe configurar el middleware con el almacenamiento de sesión adecuado para entornos de producción. Para obtener más información, consulte la <a href="https://github.com/expressjs/session" target="_blank">documentación de expressjs <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.
    * Configurar passportjs con serialización y deserialización. Esto es necesario para que la sesión autenticada persista en todas las solicitudes HTTP. Para obtener más información, consulte la <a href="http://passportjs.org/docs" target="_blank">documentación de passportjs <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.  
    * Recuperar las señales de identidad y de acceso del servicio de {{site.data.keyword.appid_short_notm}} ejecutando un mandato get en el URL de devolución de llamada.

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
  app.get("/protected", passport.authenticate(WebAppStrategy.STRATEGY_NAME)), function(req, res)
    		res.json(req.user);
    });
  ```
  {: codeblock}

    **Nota**: el servicio se redirige en el orden siguiente:
    1. El URL original de la solicitud que ha desencadenado el proceso de autenticación, como haya persistido en la sesión HTTP clave `WebAppStrategy.ORIGINAL_URL`.
    2. Una redirección correcta, tal como se especifica en `passport.authenticate(name, {successRedirect: "...."}).`
    3. Raíz de la aplicación ("/")

4. Vuelva a desplegar la aplicación.


## Cómo añadir {{site.data.keyword.appid_short_notm}} a una aplicación web Swift existente
{: #existing-swift}

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
    {: codeblock}

2. Añada el código siguiente a la aplicación Swift para:
    * Configurar Kitura para utilizar el middleware de sesión. **Nota**: debe configurar Kitura con el almacenamiento de sesión adecuado para entornos de producción. Para obtener más información, consulte la <a href="https://github.com/IBM-Swift/Kitura-Session" target="_blank">documentación de Kitura <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.
    * Recuperar las señales de identidad y de acceso del servicio de {{site.data.keyword.appid_short_notm}} ejecutando un mandato get en el URL de devolución de llamada.

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
  {: codeblock}

  <table>
  <caption> Tabla 5. Explicación de componentes de mandatos </caption>
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



## Cómo añadir {{site.data.keyword.appid_short_notm}} a una app Liberty for Java existente
{: #existing-liberty}

Puede configurar {{site.data.keyword.appid_short_notm}} para trabajar con sus aplicaciones web de Liberty for Java existentes.

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

3. En el archivo `server.xml`, defina el tipo de sujeto especial como ALL_AUTHENTICATED_USERS.

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

4. En el elemento `<application-bnd>`, <a href="https://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_authorization.html?cp=SSAW57_8.5.5&cm_mc_uid=18498555367014888859884&cm_mc_sid_50200000=1494855872" target="_blank">defina los roles <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> tal como se encuentran en su app web: `web.xml`.

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

5. Obtenga un certificado.

    a. En el panel de control {{site.data.keyword.appid_short_notm}}, pulso Credenciales del servicio.

    b. Pulse **Ver credenciales** y copie el `oauthServerUrl`.

    c. Añada `/token` al URL. Utilice Firefox para examinar la salida URL y obtener el certificado. Puede utilizar el URL siguiente como ejemplo.

    ```
    https://appid-oauth.eu-gb.bluemix.net/oauth/v3/5d12852e-b0a0-46a3-9547-67a4a33a7164/token
    ```
    {: screen}

    d. En la barra de direcciones de Firefox, haga clic en el icono de bloqueo > **flecha hacia la derecha** > **más información** > **ver certificado**.

    e. En el separador **Seguridad**, pulse **Ver detalles** > **del certificado**.

    f. Exporte el certificado y guárdelo en su unidad local como archivo PEM.

6. Añada el certificado al archivo trustore.jks de Liberty for Java mediante la <a href="https://www.ibm.com/support/knowledgecenter/SSYKE2_6.0.0/com.ibm.java.security.component.60.doc/security-component/keytoolDocs/keytool_overview.html" target="_blank">keytool de Liberty <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> y añada una referencia al alias del certificado en el elemento de OIDC. El `archivo .jks` está en el directorio del servidor: **recursos** > **seguridad** > **<i>nombre del archivo de archivo de almacén de confianza</i>** > **`archivo .jks`**. Puede utilizar una de las opciones siguientes para añadir el certificado al archivo.

    * En el terminal, vaya a la carpeta de seguridad de Liberty for Java: wlp > usr > servers > <i>servername</i> > resources > security y utilice el mandato siguiente para añadir el certificado.

      ```
      keytool -importcert -keystore ./trust.jks -file ~/Documents/secbluemix.cer`
      ```
      {: codeblock}      

      **Nota**: `~/Documents/[certificatename].cer` demuestra la ubicación del archivo en la unidad local.

    * Puede utilizar el <a href="http://keystore-explorer.org/index.html" target="_blank">Explorador del almacén de claves <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> para añadir el certificado. Abra el Explorador del almacén de claves y seleccione **Abrir un almacén de clave existente**.

7. En el archivo `manifest.yml`, defina la instancia {{site.data.keyword.appid_short_notm}}.

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

  ```xml
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
         authFilterid="myAuthFilter"
         trustAliasName="my.bluemix.certificate "
      />
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

      <!-- Automatically expand WAR files and EAR files -->
      <applicationManager autoExpand="true"/>

  </server>
  ```
  {: codeblock}



## Cómo añadir {{site.data.keyword.appid_short_notm}} a una aplicación existente que no se ejecuta en {{site.data.keyword.Bluemix_notm}}
{: #existing}

Si tiene una aplicación Node.js o Swift que no se ejecuta en {{site.data.keyword.Bluemix_notm}}, puede configurar WebAppStrategy o WebAppKituraCredentialsPlugin para que trabajen de forma remota. Para una app de Liberty for Java que no se ejecuta en Bluemix, configure las variables del elemento de OIDC.


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
  {: codeblock}

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
  <caption> Tabla 6. Explicación de componentes de mandatos para apps Swift y Node.js </caption>
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

En las apps de Liberty for Java, siga los pasos de [Añadir {{site.data.keyword.appid_short_notm}} a una app de Liberty for Java existente](/docs/services/appid/existing.html#existing-liberty), pero sustituya las variables del elemento de cliente de OIDC con el código siguiente.

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
  <caption> Tabla 7. Variables del elemento de OIDC para las apps de Liberty for Java que no se ejecutan en Bluemix </caption>
    <tr>
      <th> Componente </th>
      <th> Descripción </th>
    </tr>
    <tr>
    <td> <i> clientID </i> </br> <i> secret </i> </br> <i> oauth-server-url </i> </br> </td>
    <td> Puede encontrar estos valores pulsando **Ver credenciales** en el separador **Credenciales de servicio** del panel de control del servicio. </td>
    </tr>
    <tr>
      <td> <i> authorizationEndpointURL </i> </td>
      <td> Añada `/authorization` al final de su oauthServerURL. </td>
    </tr>
    <tr>
      <td> <i> tokenEndpointUrl </i> </td>
      <td> Añada `/token` al final de su oauthServerURL. </td>
    </tr>
    <tr>
      <td> <i> jwkEndpointUrl </i> </td>
      <td> Añada `/publickeys` al final de su oauthServerURL. </td>
    </tr>
    <tr>
      <td> <i> issuerIdentifier </i> </td>
      <td> Cambia según la región. Puede adoptar uno de los valores siguientes: </br><ul><li> issuerIdentifier="appid-oauth.ng.bluemix.net" </br><li> issuerIdentifier="appid-oauth.eu-gb.bluemix.net" </br><li> issuerIdentifier="appid-oauth.au-syd.bluemix.net" </ul></td>
    </tr>
    <tr>
      <td> <i> tokenEndpointAuthMethod </i> </td>
      <td> Especificado como "basic". </td>
    </tr>
    <tr>
      <td> <i> signatureAlgorithm </i> </td>
      <td> Especificado como "RS256". </td>
    </tr>
    <tr>
      <td> <i> authFilterid </i> </td>
      <td> La lista de recursos para proteger. </td>
    </tr>
    <tr>
      <td> <i> trustAliasName </i> </td>
      <td> El nombre del certificado dentro del almacén de confianza. </td>
    </tr>
  </table>
