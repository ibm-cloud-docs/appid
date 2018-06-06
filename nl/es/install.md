---
copyright:
  years: 2017, 2018
lastupdated: "2018-01-02"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Configuración de los SDK
{: #configuring}


## Configuración del SDK de Android
{: #android-setup}

Cree las apps de Android con el SDK del cliente de {{site.data.keyword.appid_short}}, inicialice el SDK, autentique usuarios, y realice solicitudes a recursos protegidos o no protegidos.
{:shortdesc}


### Antes de empezar

Necesita la siguiente información:
  * Una instancia del servicio de {{site.data.keyword.appid_short_notm}}.
  * Su ID de arrendatario. En el separador **Credenciales de servicio** del panel de control de servicio, pulse **Ver credenciales**. Su ID de arrendatario se muestra en el campo **tenantID**. Es un identificador exclusivo que se utiliza para inicializar la app.
  * Su región de {{site.data.keyword.Bluemix}}. Puede encontrar su región consultando en la IU. El valor se utiliza para inicializar la app.
    <table> <caption> Tabla 1. Regiones de {{site.data.keyword.Bluemix_notm}} y sus correspondientes valores de SDK </caption>
    <tr>
      <th> Región Bluemix </th>
      <th> Valor de SDK </th>
    </tr>
    <tr>
      <td> Sur de EE.UU. </td>
      <td> AppID.REGION_US_SOUTH </td>
    </tr>
    <tr>
      <td> Sídney </td>
      <td> AppID.REGION_SYDNEY </td>
    </tr>
    <tr>
      <td> Reino Unido </td>
      <td> AppID.REGION_UK </td>
    </tr>
  </table>

  * Un <a href="https://developers.google.com/web/tools/setup/" target="_blank">proyecto de Android Studio <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>, configurado para funcionar con Gradle.

### Instalación del SDK del cliente

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

3. Abra el archivo `build.gradle` para su aplicación.

    **Nota**: Asegúrese de abrir el archivo para su app, no el archivo `build.gradle` del proyecto.
4. Busque la sección de dependencias del archivo y añada una dependencia de compilación para el SDK del cliente de {{site.data.keyword.appid_short_notm}}.

  ```gradle
   dependencies {
       compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:1.+'
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

6. Sincronice el proyecto con Gradle. Pulse **Tools** > **Android** > **Sync Project with Gradle Files**.

### Inicialización del SDK del cliente

Inicialice el SDK del cliente pasando los parámetros context, tenant ID y region al método initialize. Un lugar habitual, pero no obligatorio, donde poner el código de inicialización es en el método onCreate de la actividad principal de la aplicación de Android.

  ```java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, AppID.REGION_UK);
  ```
  {: codeblock}

1. Sustituya *tenantId* con su ID de arrendatario de su servicio.
2. Sustituya *AppID.REGION_UK* con su región de {{site.data.keyword.Bluemix_notm}}.

Para obtener más información, consulte el <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">Repositorio GitHub de Android de {{site.data.keyword.appid_short_notm}}<img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.

## Configuración del SDK de Swift de iOS
{: #ios-setup}

Cree las aplicaciones de Swift con el SDK del cliente de {{site.data.keyword.appid_short}}, inicialice el SDK, autentique usuarios y realice solicitudes a recursos protegidos y no protegidos.
{:shortdesc}


### Antes de empezar

Necesita la siguiente información:
  * Una instancia de {{site.data.keyword.appid_short_notm}}.
  * Su ID de arrendatario. En el separador **Credenciales de servicio** del panel de control de servicio, pulse **Ver credenciales**. Su ID de arrendatario se muestra en el campo **TenantID**. Es un identificador exclusivo que se utiliza para inicializar la app.
  * Su región de {{site.data.keyword.Bluemix_notm}}.
  Puede encontrar su región consultando en la IU. El valor se utiliza para inicializar la app.
    <table> <caption> Tabla 1. Regiones de {{site.data.keyword.Bluemix_notm}} y sus correspondientes valores de SDK </caption>
    <tr>
      <th> Región Bluemix </th>
      <th> Valor de SDK </th>
    </tr>
    <tr>
      <td> Sur de EE.UU. </td>
      <td> AppID.REGION_US_SOUTH </td>
    </tr>
    <tr>
      <td> Sídney </td>
      <td> AppID.REGION_SYDNEY </td>
    </tr>
    <tr>
      <td> Reino Unido </td>
      <td> AppID.REGION_UK </td>
    </tr>
  </table>

  * Un proyecto Xcode (versión 8.1 o superior).
  * CocoaPods (versión 1.1.0 o superior).


### Instalación del SDK del cliente

El SDK del cliente de {{site.data.keyword.appid_short_notm}} se distribuye con CocoaPods, un gestor de dependencias para proyectos de Swift y de Objective-C Cocoa. CocoaPods descarga artefactos, y los pone a disposición de su proyecto.

1. Cree un proyecto de Xcode, o abra uno ya existente.
2. Abra o cree el podfile en el directorio de proyecto.
3. En el destino del proyecto, añada una dependencia para el pod de 'BluemixAppID'. Asegúrese de que el mandato `use_frameworks!` también esté bajo su destino.

  Por ejemplo:

  ```swift
  target '<yourTarget>' do
     use_frameworks!
     pod 'BluemixAppID'
  end
  ```
  {: codeblock}

4. Para descargar la dependencia de `BluemixAppID`, ejecute el mandato siguiente.

  ```swift
  pod install --repo-update
  ```
  {: codeblock}

6. Abra el proyecto Xcode y habilite el uso compartido de la cadena de claves. En **Valores de proyecto**, pulse **Prestaciones > Uso compartido de la cadena de claves**.
7. En **Valores de proyecto > Info > Tipos de URL**, añada un **Tipo de URL**. Rellene los recuadros de texto **Identificador** y **Esquema de URL** con este valor: `$(PRODUCT_BUNDLE_IDENTIFIER)`


### Inicialización del SDK del cliente

1. Añada la siguiente importación al archivo `AppDelegate.swift`.

  ```swift
  import BluemixAppID
  ```
  {: codeblock}

2. Inicialice el SDK del cliente pasando los parámetros de ID de arrendatario y region al método initialize. Un lugar habitual, pero no obligatorio, donde poner el código de inicialización es en el método `application:didFinishLaunchingWithOptions`: del AppDelegate de la aplicación Swift.

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, bluemixRegion: AppID.Region_UK)
  ```
  {: codeblock}

  * Sustituya *tenantId* por el ID de arrendatario para su servicio.
  * Sustituya AppID.REGION_UK por la región de {{site.data.keyword.appid_short_notm}}.

3. Añada el código siguiente al archivo AppDelegate.

  ```swift
  func application(_ application: UIApplication, open url: URL, options :[UIApplicationOpenURLOptionsKey : Any]) -> Bool {
          return AppID.sharedInstance.application(application, open: url, options: options)
      }
  ```
  {: codeblock}

Para obtener más información, consulte el <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">Repositorio GitHub de iOS de {{site.data.keyword.appid_short_notm}}<img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.

## Configuración del SDK de Node.js
{: #nodejs-setup}

### Antes de empezar

* Familiarícese con el desarrollo de aplicaciones Node.js en {{site.data.keyword.Bluemix_notm}}.
* El SDK del servidor de {{site.data.keyword.appid_short_notm}} necesita que se implemente el servidor de Node.js con la <a href="http://expressjs.com/" target="_blank">infraestructura Express <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.

**Nota**: otras infraestructuras utilizan infraestructuras `Express`, como LoopBack. Puede utilizar el SDK del servidor de {{site.data.keyword.appid_short_notm}} con cualquiera de estas infraestructuras.


### Instalación del SDK del servidor


1. Desde la línea de mandatos, abra el directorio con su app Node.js.
2. Ejecute los siguientes mandatos.

  ```
  npm install -save express
  npm install -save passport
  npm install -save bluemix-appid
  ```
  {: codeblock}

Para obtener más información, consulte el <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">Repositorio GitHub de Node.js de {{site.data.keyword.appid_short_notm}}<img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.

## Configuración del SDK de Swift
{: #swift-setup}

### Antes de empezar

* Familiarícese con el desarrollo de aplicaciones Swift en {{site.data.keyword.Bluemix}}.
* Instale Swift 3.0.2
* Instale Kitura 1.6


### Instalación del SDK

1. Abra el archivo `Package.swift` en el directorio de su app Swift y añada la dependencia `appid-serversdk-swift`. Por ejemplo:

  ```swift
  import PackageDescription

  let package = Package(
      dependencies: [
          .Package(url: "https://github.com/ibm-cloud-security/appid-serversdk-swift.git", majorVersion: 1)
      ]
  )
  ```
  {: codeblock}

Para obtener más información, consulte el <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">Repositorio de GitHub de Swift de {{site.data.keyword.appid_short_notm}}<img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.
