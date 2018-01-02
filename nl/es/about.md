---

copyright:
  years: 2017
lastupdated: "2017-12-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


# Acerca de
{: #about}

Puede utilizar {{site.data.keyword.appid_full}} para añadir autenticación a sus apps y proteger sus recursos de fondo.
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
    <td> Debe añadir [autorización y autenticación](/docs/services/appid/authorization.html) a sus aplicaciones web y móvil pero no tiene un fondo de seguridad.</td>
    <td> {{site.data.keyword.appid_short_notm}} permite añadir fácilmente un paso de autenticación a sus aplicaciones. Puede utilizar el servicio para comunicarse con los [proveedores de identidad](/docs/services/appid/identity-providers.html) para gestionar el acceso a sus aplicaciones. </td>
  </tr>
  <tr>
    <td> Desea limitar el acceso a sus apps y recursos de fondo. </td>
    <td> El servicio le ofrece la posibilidad de [proteger sus recursos](/docs/services/appid/protecting-resources.html) tanto para usuarios autenticados como anónimos. </td>
  </tr>
  <tr>
    <td> Desea crear experiencias de la app personalizadas para sus usuarios. </td>
    <td> {{site.data.keyword.appid_short_notm}} le permite [almacenar datos de usuario](/docs/services/appid/user-profile.html) como preferencias de la app o información de sus perfiles sociales públicos. Puede utilizar dichos datos para asegurarse que sus usuarios tienen una experiencia personalizada. </td>
  </tr>
</table>


## Arquitectura
{: #architecture}

Con {{site.data.keyword.appid_short_notm}} puede añadir un nivel de seguridad a sus aplicaciones solicitando a los usuarios que inicien la sesión. También puede utilizar el SDK del servidor para proteger sus recursos de fondo.

El siguiente diagrama muestra una visión general del funcionamiento del servicio {{site.data.keyword.appid_short_notm}}.

![Diagrama de arquitectura de {{site.data.keyword.appid_short_notm}}](/images/appid_architecture.png)

Figura 1. Diagrama de la arquitectura de {{site.data.keyword.appid_short_notm}}


<dl>
  <dt> Aplicación </dt>
    <dd> SDK del servidor: Puede proteger sus recursos de programa de fondo alojados en {{site.data.keyword.Bluemix_notm}} y sus aplicaciones web utilizando el SDK del servidor. Extrae la señal de acceso de la solicitud y la valida con {{site.data.keyword.appid_short_notm}}. </br>
    SDK del cliente: Puede proteger sus aplicaciones móviles con el SDK del cliente de Android o iOS. El SDK del cliente se comunica con sus recursos en la nube para iniciar el proceso de autenticación cuando detecta un desafío de autorización. </dd>
  <dt> {{site.data.keyword.Bluemix_notm}} </dt>
    <dd> ID de app: Tras la correcta autenticación, {{site.data.keyword.appid_short_notm}} devuelve las señales de identidad y de acceso a la aplicación. </br>
    Directorio de nube: Los usuarios pueden registrarse en su servicio con su correo electrónico y contraseña. Luego podrá gestionar sus usuarios en una vista de lista a través de la IU. </dd>
  <dt> Externa (de terceros) </dt>
    <dd>  {{site.data.keyword.appid_short_notm}} admite dos proveedores de identidad social: Facebook y Google+. El servicio organiza una redirección al proveedor de identidades y proporciona acceso a su app después de verificar la autenticación. {{site.data.keyword.appid_short_notm}} verifica las credenciales sin tener acceso a la contraseña en sí. </dd>
</dl>


## Flujo de solicitudes
{: #request}

En el diagrama siguiente se describe el flujo de una solicitud, desde el SDK del cliente a los proveedores de identidad y de recursos de programa de fondo.

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

**Nota**: Los protocolos implementados son totalmente compatibles con OpenID Connect (OIDC).
