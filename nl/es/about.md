---

copyright:
  years: 2017
lastupdated: "2017-11-09"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


# Acerca de
{: #about}

{{site.data.keyword.appid_full}} le permite gestionar fácilmente el acceso a sus aplicaciones.
{:shortdesc}


## Motivos para utilizar el servicio
{: #reasons}

¿Por qué desea utilizar {{site.data.keyword.appid_short_notm}}? Compruebe los casos de ejemplo siguientes para saber si se le aplica alguno.
{: shortdesc}

<table>
  <tr>
    <th> Caso de ejemplo </th>
    <th> Motivo </th>
  </tr>
  <tr>
    <td> Desea añadir seguridad a sus aplicaciones móviles y web. </td>
    <td> {{site.data.keyword.appid_short_notm}} permite añadir fácilmente un paso de autenticación a sus aplicaciones. Puede utilizar el servicio para comunicarse con los proveedores de identidad para gestionar el acceso a sus aplicaciones. </td>
  </tr>
  <tr>
    <td> Desea limitar el acceso a sus apps y recursos back-end. </td>
    <td> El servicio le ofrece la posibilidad de proteger sus recursos tanto para usuarios autenticados como anónimos. </td>
  </tr>
  <tr>
    <td> Desea crear experiencias de la app personalizadas para sus usuarios. </td>
    <td> {{site.data.keyword.appid_short_notm}} le permite almacenar datos de usuario como preferencias de la app o información de sus perfiles sociales públicos. Puede utilizar dichos datos para asegurarse que sus usuarios tienen una experiencia personalizada. </td>
  </tr>
</table>

**Nota**: Los protocolos implementados son totalmente compatibles con OpenID Connect (OIDC).


## Arquitectura
{: #architecture}

Con {{site.data.keyword.appid_short_notm}} puede añadir un nivel de seguridad a sus aplicaciones solicitando a los usuarios que inicien la sesión. También puede utilizar el SDK del servidor para proteger los recursos de fondo.

El siguiente diagrama muestra una visión general del funcionamiento del servicio {{site.data.keyword.appid_short_notm}}.


![Diagrama de la arquitectura de {{site.data.keyword.appid_short_notm}} ](/images/appid_architecture2.png)

Figura 1. Diagrama de la arquitectura de {{site.data.keyword.appid_short_notm}}



<dl>
  <dt> Aplicación </dt>
    <dd> El SDK del cliente proporciona una clase de solicitud para comunicarse con sus recursos de la nube. El SDK del cliente inicia automáticamente el proceso de autenticación cuando detecta un desafío de autorización. </dd>
  <dt> {{site.data.keyword.Bluemix_notm}} </dt>
    <dd>  El SDK del servidor extrae la señal de acceso de la solicitud y la valida con {{site.data.keyword.appid_short_notm}}. Tras la correcta autenticación, {{site.data.keyword.appid_short_notm}} devuelve las señales de identidad y de acceso a la aplicación. </dd>
  <dt> Proveedores de identidad </dt>
    <dd> El servicio organiza una redirección al proveedor de identidades y verifica la autenticación para proporcionar acceso a la aplicación. {{site.data.keyword.appid_short_notm}} verifica las credenciales sin tener acceso a la contraseña en sí. </dd>
</dl>


## Flujo de solicitudes
{: #request}

En el diagrama siguiente se describe el flujo de una solicitud, desde el SDK del cliente a los proveedores de identidad y de la aplicación de programa de fondo.

![{{site.data.keyword.appid_short_notm}} flujo de solicitudes](/images/appidrequestflow.png)

Figura 2. Flujo de solicitudes de {{site.data.keyword.appid_short_notm}}


* El SDK del cliente de {{site.data.keyword.appid_short_notm}} realiza una solicitud a los recursos de fondo protegidos por el SDK del servidor de {{site.data.keyword.appid_short_notm}}.
* El SDK del servidor de {{site.data.keyword.appid_short_notm}} detecta una solicitud no autorizada y devuelve HTTP 401 y el ámbito de autorización.
* El SDK del cliente detecta automáticamente el código HTTP 401 e inicia el proceso de autenticación.
* Cuando el SDK del cliente establece contacto con el servicio, el SDK del servidor devuelve el widget de inicio de sesión si hay más de un proveedor de identidad configurado. {{site.data.keyword.appid_short_notm}} llama al proveedor de identidad y presenta el formulario de inicio de sesión para dicho proveedor o devuelve un código de concesión que les permite autenticarse si no hay ningún proveedor de identidad configurado.
* {{site.data.keyword.appid_short_notm}} solicita al cliente que se autentique especificando un cambio de autenticación.
* Si hay un proveedor de identidad configurado cuando el usuario inicia una sesión, la autenticación se gestiona mediante el flujo de OAuth correspondiente.
* Si la autenticación finaliza con el mismo código de concesión, el código se envía al punto final de señal. El punto final devuelve dos señales: una señal de acceso y una de identidad. A partir de este momento, todas las solicitudes que se realicen con el SDK del cliente tendrán una cabecera de autorización nueva.
* El SDK del cliente vuelve a enviar automáticamente la solicitud original que activó el flujo de autorización.
* El SDK del servidor extrae la cabecera de autorización de la solicitud, valida la cabecera con el servicio y otorga acceso a un recurso de fondo.


## Componentes
{: #components}

El servicio consta de los componentes siguientes.

<dl>
  <dt> Panel de control </dt>
    <dd> En el panel de control del servicio puede descargar ejemplos de incorporación, ver registros de actividad y configurar proveedores de autenticación e identificación. </dd>
  <dt> SDK del cliente </dt>
    <dd> Puede utilizar el SDK del cliente con sus apps móviles y web para implementar la autenticación de usuarios. </br></br>
    Requisitos previos para Android:
    <ul><ul><li> API 25 o superior </li>
    <li> Java 8.x </li>
    <li> Herramientas del SDK de Android 25.2.5 o superior </li>
    <li> Herramientas de plataforma del SDK de Android 25.0.3 o superior </li>
    <li> Android Build Tools versión 25.0.2 o superior </li></ul></ul></br>
    Requisitos previos para iOS:
    </br>
    <ul><ul><li> iOS9 o superior </li>
    <li> MacOS 10.11.5 </li>
    <li>Xcode 8.2 </li></ul></ul></dd>
  <dt> Servidor de SDK </dt>
    <dd> Puede proteger sus recursos de back-end alojados en {{site.data.keyword.Bluemix_notm}} </br>
    Entornos de ejecución admitidos:
    <ul><ul><li> Node.js </li>
    <li> Liberty for Java </li>
    <li> Swift </li></ul></ul></dd>
</dl>
