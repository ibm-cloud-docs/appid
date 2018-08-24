---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Acerca de
{: #about}

La seguridad de aplicación se puede complicar de forma increíble. Para la mayoría de los desarrolladores, es una de las partes más difíciles de la creación de una app. ¿Cómo puede estar seguro de que está protegiendo la información de los usuarios? Al integrar {{site.data.keyword.appid_full}} en sus apps, puede proteger recursos y añadir autenticación, incluso aunque no tenga mucha experiencia en seguridad.
{:shortdesc}


## Motivos para utilizar el servicio
{: #reasons}

{{site.data.keyword.appid_short_notm}} permite a los desarrolladores añadir fácilmente autenticación a sus apps web y móviles con unas pocas líneas de código, y proteger sus aplicaciones y servicios nativos de nube en {{site.data.keyword.Bluemix_notm}}. Al exigir a los usuarios que inicien sesión en la app, puede almacenar datos de usuario como preferencias de la app, o información de los perfiles sociales públicos, y luego utilizar esos datos para personalizar la experiencia de cada usuario en la app. {{site.data.keyword.appid_short_notm}} proporciona una infraestructura de inicio de sesión, pero también puede traer las pantallas de inicio de sesión de su propia marca para utilizarlas con el directorio en la nube.
{: shortdesc}

¿Por qué desea utilizar {{site.data.keyword.appid_short_notm}}? Consulte los siguientes casos de ejemplo para ver si alguno de ellos se aplican a usted.

<table>
  <tr>
    <th>Caso de ejemplo</th>
    <th>Solución</th>
  </tr>
  <tr>
    <td>Debe añadir [autorización y autenticación](/docs/services/appid/authorization.html) a sus apps web y móvil pero no tiene un fondo de seguridad.</td>
    <td>{{site.data.keyword.appid_short_notm}} permite añadir fácilmente un paso de autenticación a sus apps. Puede añadir inicio de sesión de correo electrónico o nombre de usuario, inicio de sesión social o inicio de sesión empresarial a sus apps con API, SDK, IU creadas previamente o IU de su propia marca.</td>
  </tr>
  <tr>
    <td>Desea limitar el acceso a sus apps y recursos de fondo.</td>
    <td>Puede proteger sus apps, recursos de fondo y API fácilmente mediante la autenticación basada en estándares que proporciona {{site.data.keyword.appid_short_notm}}.</td>
  </tr>
  <tr>
    <td>Desea crear experiencias de la app personalizadas para sus usuarios.</td>
    <td>Con {{site.data.keyword.appid_short_notm}} puede [almacenar datos de usuario](/docs/services/appid/user-profile.html) como preferencias de la app o información de sus perfiles sociales públicos y entonces utilizar esos datos para personalizar cada experiencia de su app.</td>
  </tr>
  <tr>
    <td>Desea gestionar usuarios de forma escalable.</td>
    <td> {{site.data.keyword.appid_short_notm}} le permite crear un [Directorio en la nube](/docs/services/appid/cloud-directory.html), que hace posible añadir el registro e inicio de sesión de usuarios a sus apps. El directorio en la nube le proporciona la infraestructura para mantener un registro de usuarios que puede escalar con su base de usuarios. Con la funcionalidad integrada para el autoservicio, como verificación de correo electrónico y restablecimiento de contraseñas, puede garantizar la seguridad de la autenticación de los usuarios de su app.</td>
  </tr>
</table>


## Integraciones
{: #integrations}

Puede utilizar {{site.data.keyword.appid_short_notm}} con otras ofertas de {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}


<dl>
  <dt>{{site.data.keyword.containerlong_notm}}</dt>
    <dd>Al configurar el ingreso en un clúster estándar, puede proteger sus apps en el nivel de clúster. Consulte la <a href="/docs/containers/cs_annotations.html#appid-auth">anotación de Ingress de autenticación de {{site.data.keyword.appid_short_notm}}</a> o la publicación de blog <a href="https://www.ibm.com/blogs/bluemix/2018/05/announcing-app-id-integration-ibm-cloud-kubernetes-service/">Anuncio de la integración de App ID en el servicio IBM Cloud Kubernetes <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> para empezar.</dd>
  <dt>{{site.data.keyword.openwhisk}} y API Connect</dt>
    <dd>Al crear sus API con [{{site.data.keyword.openwhisk_short}}](/docs/openwhisk/index.html) y [API Connect](/docs/apis/management/manage_apis.html), puede proteger sus aplicaciones en la pasarela en lugar de en el código de la app. Para ver la integración en acción, vea <a href="https://www.youtube.com/watch?v=Fa9YD2NGZiE" target="_blank">OAUTH de inicio de sesión en redes sociales rápido y simple con APIC y {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.</dd>
  <dt>Cloud Foundry</dt>
    <dd>Pruebe una de las apps de Cloud Foundry de muestra que se proporcionan para ver cómo puede integrar {{site.data.keyword.appid_short_notm}} en sus apps.</dd>
  <dt>Guía de programación de iOS</dt>
    <dd>¿Desarrolla apps para Apple? Pruebe la <a href="https://console.bluemix.net/docs/swift/index.html#overview" target="_blank">Guía de programación de iOS <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> para aprender, experimentar y mejorar sus apps de iOS existentes con {{site.data.keyword.Bluemix_notm}}.</dd>
  <dt>{{site.data.keyword.cloudaccesstrailshort}}</dt>
    <dd>Puede supervisar la actividad administrativa que se realiza en {{site.data.keyword.appid_short_notm}}, como los cambios en la configuración del panel de control, mediante el [servicio {{site.data.keyword.cloudaccesstrailshort}}](/docs/services/cloud-activity-tracker/index.html).</dd>
  <dt>Guía de programación de Node.js</dt>
    <dd>¿Desarrolla apps en Node.js? Pruebe la <a href="https://console.bluemix.net/docs/node/index.html#getting-started-tutorial" target="_blank">Guía de programación de Node.js <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> para aprender, experimentar y mejorar sus apps de Node.js existentes con {{site.data.keyword.Bluemix_notm}}.</dd>
</dl>


## Arquitectura
{: #architecture}

Con {{site.data.keyword.appid_short_notm}}, puede añadir un nivel de seguridad a sus apps solicitando a los usuarios que inicien la sesión. También puede utilizar las API o el SDK del servidor para proteger sus recursos de fondo.
{: shortdesc}

![Diagrama de arquitectura de {{site.data.keyword.appid_short_notm}}](/images/appid_architecture1.png)

<dl>
  <dt>Aplicación</dt>
    <dd><strong>SDK del servidor</strong>: Puede proteger sus recursos de programa de fondo alojados en {{site.data.keyword.Bluemix_notm}} y sus apps web utilizando el SDK del servidor. Extrae la señal de acceso de la solicitud y la valida con {{site.data.keyword.appid_short_notm}}. </br>
    <strong>SDK del cliente</strong>: Puede proteger sus apps móviles con el SDK del cliente de Android o iOS. El SDK del cliente se comunica con sus recursos en la nube para iniciar el proceso de autenticación cuando detecta un desafío de autorización.</dd>
  <dt>{{site.data.keyword.Bluemix_notm}}</dt>
    <dd><strong>{{site.data.keyword.appid_short_notm}}</strong>: Tras la correcta autenticación, {{site.data.keyword.appid_short_notm}} devuelve las señales de identidad y de acceso a la app.</br>
    <strong>Directorio en la nube</strong>: Los usuarios pueden registrarse en su servicio con su correo electrónico y contraseña. Luego podrá gestionar sus usuarios en una vista de lista a través de la IU. Con el directorio en la nube, {{site.data.keyword.appid_short_notm}} funciona como proveedor de identidad.</dd>
  <dt>Externa (de terceros)</dt>
    <dd><strong>Proveedores de identidad sociales y empresariales</strong>: {{site.data.keyword.appid_short_notm}} admite Facebook, Google+ y SAML 2.0 Federation como opciones de proveedor de identidad. El servicio organiza una redirección al proveedor de identidad y verifica las señales de autenticación devueltas. Si las señales son válidas, el servicio otorga acceso a la app incluso sin tener acceso a la frase de contraseña real.</dd>
</dl>


## Flujo de solicitudes
{: #request}

Aunque el flujo de solicitudes puede variar en función de la configuración de aplicación, hay tres flujos principales que puede encontrar al trabajar con App ID. Puede crear un flujo de app móvil, un flujo de app web o proteger los recursos con un flujo diferente. Consulte alguno de los flujos de ejemplo para ver si puede partir de ahí al configurar su app.
{: shortdesc}

### Flujo de solicitud de app web
{: #web-flow}

![{{site.data.keyword.appid_short_notm}} flujo de solicitudes](/images/web_flow1.png)

1. Mediante un navegador, un usuario realiza una acción que desencadena una solicitud al SDK de App ID.
2. Si el usuario no está autorizado, se inicia una redirección a App ID.
3. App ID abre el widget de inicio de sesión y lo envía al navegador.
4. El usuario selecciona un proveedor de identidad con el que autenticarse y completa el proceso de inicio de sesión.
5. El proveedor de identidad se redirige de nuevo al SDK de App ID con una señal de identidad.
6. El SDK de App ID obtiene señales de acceso del servicio de App ID.
7. El SDK de App ID guarda las señales y se produce una redirección.
8. Se otorga al usuario acceso a la aplicación.

### Flujo de solicitudes móviles
{: #mobile-flow}

![Flujo de solicitudes de {{site.data.keyword.appid_short_notm}}](/images/mobile_flow.png)

1. Un usuario realiza una acción que desencadena una solicitud por parte de la aplicación cliente al SDK de App ID.
2. Si el usuario no tiene señales de acceso válidas, el SDK de App ID inicia el proceso de autorización.
3. El widget de inicio de sesión se muestra al usuario.
4. Mediante uno de los proveedores de identidad configurados, el usuario se autentica.
5. Una vez que el usuario tiene una señal de identidad, el SDK obtiene una señal de acceso del servicio de App ID.
6. Con las dos señales, el SDK realiza de nuevo la solicitud.
7. Si las señales son válidas, se otorga al usuario acceso a la aplicación.

### Flujo de solicitudes de recurso protegido
{: #pr-flow}

![{{site.data.keyword.appid_short_notm}} flujo de solicitudes](/images/pr_flow.png)

1. Antes de poder realizar una solicitud al recurso, una aplicación cliente debe tener una serie de claves públicas.
2. Con las claves públicas, una aplicación cliente realiza una solicitud.
3. Si no hay ninguna señal de acceso válida, la aplicación recibe un error.
4. Después de obtener una señal válida, la app cliente puede realizar la solicitud de nuevo. Pero, esta vez, incluir la señal.
5. Cuando la aplicación pueda validar los permisos que otorga la señal de acceso, se habrá otorgado a la aplicación acceso al recurso protegido.
