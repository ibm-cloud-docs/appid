---

copyright:
  years: 2017, 2018
lastupdated: "2018-04-27"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Acerca de
{: #about}

Puede utilizar {{site.data.keyword.appid_full}} para añadir autenticación a sus apps y proteger sus recursos de fondo.
{:shortdesc}

## Motivos para utilizar el servicio
{: #reasons}

¿Por qué desea utilizar {{site.data.keyword.appid_short_notm}}? Consulte los siguientes casos de ejemplo para ver si alguno de ellos se aplican a usted.
{: shortdesc}

<table>
  <tr>
    <th> Caso de ejemplo </th>
    <th> Motivo </th>
  </tr>
  <tr>
    <td> Debe añadir [autorización y autenticación](/docs/services/appid/authorization.html) a sus apps web y móvil pero no tiene un fondo de seguridad. </td>
    <td> {{site.data.keyword.appid_short_notm}} permite añadir fácilmente un paso de autenticación a sus apps. Puede utilizar el servicio para comunicarse con los [proveedores de identidad](/docs/services/appid/identity-providers.html) para gestionar el acceso a sus apps. </td>
  </tr>
  <tr>
    <td> Desea limitar el acceso a sus apps y recursos de fondo. </td>
    <td> El servicio le ofrece la posibilidad de [proteger sus recursos](/docs/services/appid/protecting-resources.html) tanto para usuarios autenticados como anónimos. </td>
  </tr>
  <tr>
    <td> Desea crear experiencias de la app personalizadas para sus usuarios. </td>
    <td> Con {{site.data.keyword.appid_short_notm}} puede [almacenar datos de usuario](/docs/services/appid/user-profile.html) como preferencias de la app o información de sus perfiles sociales públicos y entonces utilizar esos datos para personalizar cada experiencia de su app. </td>
  </tr>
  <tr>
    <td> Desea ofrecer a los usuarios la posibilidad de obtener acceso a su app con su correo electrónico y una contraseña. </td>
    <td> {{site.data.keyword.appid_short_notm}} le permite crear un [directorio en la nube](/docs/services/appid/cloud-directory.html), que hace posible añadir el registro e inicio de sesión de usuarios a sus apps. El directorio en la nube le proporciona la infraestructura para mantener un registro de usuarios que puede escalar con su base de usuarios. Con la funcionalidad integrada para el autoservicio, como verificación de correo electrónico y restablecimiento de contraseñas, puede garantizar la seguridad de la autenticación de los usuarios de su app. </td>
  </tr>
</table>


## Integraciones
{: #integrations}

Puede utilizar {{site.data.keyword.appid_short_notm}} con otras ofertas de {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}


<dl>
  <dt>{{site.data.keyword.containerlong_notm}}</dt>
    <dd>Al configurar el ingreso en un clúster estándar, puede proteger sus apps en el nivel de clúster. Consulte la anotación de ingreso de autenticación de {{site.data.keyword.appid_short_notm}} para empezar.</dd>
  <dt>{{site.data.keyword.openwhisk}} y API Connect</dt>
    <dd>Al crear sus API con [{{site.data.keyword.openwhisk_short}}](/docs/openwhisk/index.html) y [API Connect](/docs/apis/management/manage_apis.html), puede proteger sus aplicaciones en la pasarela en lugar de en el código de la app. Para ver la integración en acción, vea <a href="https://www.youtube.com/watch?v=Fa9YD2NGZiE" target="_blank">OAUTH de inicio de sesión en redes sociales rápido y simple con APIC y {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.</dd>
  <dt>Cloud Foundry</dt>
    <dd>Pruebe una de nuestras apps de Cloud Foundry de muestra para ver cómo puede integrar el ID de app en sus apps.</dd>
  <dt>Guía de programación de iOS</dt>
    <dd>¿Desarrolla apps para Apple? Pruebe la <a href="https://console.bluemix.net/docs/swift/index.html#overview" target="_blank">Guía de programación de iOS <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> para aprender, experimentar y mejorar sus apps de iOS existentes con {{site.data.keyword.Bluemix_notm}}.</dd>
</dl>


## Arquitectura
{: #architecture}

Con {{site.data.keyword.appid_short_notm}}, puede añadir un nivel de seguridad a sus apps solicitando a los usuarios que inicien la sesión. También puede utilizar el SDK del servidor para proteger sus recursos de fondo.
{: shortdesc}

![Diagrama de arquitectura de {{site.data.keyword.appid_short_notm}}](/images/appid_architecture.png)

<dl>
  <dt> Aplicación </dt>
    <dd><strong>SDK del servidor</strong>: Puede proteger sus recursos de programa de fondo alojados en {{site.data.keyword.Bluemix_notm}} y sus apps web utilizando el SDK del servidor. Extrae la señal de acceso de la solicitud y la valida con {{site.data.keyword.appid_short_notm}}. </br>
    <strong>SDK del cliente</strong>: Puede proteger sus apps móviles con el SDK del cliente de Android o iOS. El SDK del cliente se comunica con sus recursos en la nube para iniciar el proceso de autenticación cuando detecta un desafío de autorización.</dd>
  <dt>{{site.data.keyword.Bluemix_notm}}</dt>
    <dd><strong>{{site.data.keyword.appid_short_notm}}</strong>: Tras la correcta autenticación, {{site.data.keyword.appid_short_notm}} devuelve las señales de identidad y de acceso a la app.</br>
    <strong>Directorio en la nube</strong>: Los usuarios pueden registrarse en su servicio con su correo electrónico y contraseña. Luego podrá gestionar sus usuarios en una vista de lista a través de la IU. Con el directorio en la nube, {{site.data.keyword.appid_short_notm}} funciona como proveedor de identidad.</dd>
  <dt>Externa (de terceros)</dt>
    <dd><strong>Proveedores de identidad sociales y empresariales</strong>:{{site.data.keyword.appid_short_notm}} admite dos proveedores de identidad sociales: Facebook y Google+, y un proveedor de identidad empresarial: SAML 2.0 Federation. El servicio organiza una redirección al proveedor de identidad y verifica las señales de autenticación devueltas. Si las señales son válidas, el servicio otorga acceso a la app incluso sin tener acceso a la frase de contraseña real.</dd>
</dl>


## Flujo de solicitudes
{: #request}

En el diagrama siguiente se describe el flujo de una solicitud, desde el SDK del cliente a los proveedores de identidad y de recursos de programa de fondo.
{: shortdesc}

![{{site.data.keyword.appid_short_notm}} flujo de solicitudes](/images/appidrequestflow.png)


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
