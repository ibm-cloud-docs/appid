---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:tip: .tip}

# Guía de aprendizaje de iniciación
{: #gettingstarted}

La seguridad de aplicación se puede complicar de forma increíble. Para la mayoría de los desarrolladores, es una de las partes más difíciles de la creación de una app. ¿Cómo puede estar seguro de que está protegiendo la información de los usuarios? Al integrar {{site.data.keyword.appid_full}} en sus apps, puede proteger recursos y añadir autenticación; incluso aunque no tenga mucha experiencia en seguridad.
{: shortdesc}

Al exigir a los usuarios que inicien sesión en la app, puede almacenar datos de usuario como preferencias de la app o información de los perfiles sociales públicos, y luego utilizar esos datos para personalizar cada experiencia de la app. El ID de app proporciona un registro en la infraestructura, pero también puede traer las pantallas de inicio de sesión de su propia marca al trabajar con el directorio en la nube.

Como propietario de una cuenta, ahora puede establecer políticas que definan cómo pueden interactuar los miembros del equipo con instancias de {{site.data.keyword.appid_short_notm}}. Puede decidir quién puede crear, actualizar y suprimir instancias del servicio. Para obtener más información, consulte [Gestión de acceso de servicio](/docs/services/appid/iam.html).
{:tip}

## Creación de una instancia de servicio
{: #create}

Cree y enlace una instancia de {{site.data.keyword.appid_short_notm}} a su app para empezar.
{: shortdesc}

1. En el catálogo de {{site.data.keyword.Bluemix}}, seleccione {{site.data.keyword.appid_short_notm}}. Se abre la pantalla de configuración del servicio.
2. Dé un nombre a la instancia de servicio, o utilice el nombre preestablecido.
3. Seleccione el plan de precios y pulse **Crear**.
4. Enlace la instancia de {{site.data.keyword.appid_short_notm}}.
    1. Para ver una lista de apps que se pueden enlazar a su instancia de servicio, pulse **Conexiones**.
    2. Pulse **Crear conexión**. Se abrirá una página con todas las apps de las que tenga la opción de enlazar.
    3. Pulse **Conectar** en la app que desea enlazar.
    4. Pulse **Volver a transferir** para aplicar el cambio.

Eso es todo. Está listo para empezar a configurar los valores de la aplicación.


## Configuración de una app de ejemplo
{: #sample-app}

Puede utilizar una de las apps de ejemplo preconfiguradas para familiarizarse con el servicio.
{: shortdesc}

De forma predeterminada, las apps de ejemplo están configuradas con dos proveedores de identidad y la posibilidad de revisar la autenticación. También puede utilizar la característica de widget de inicio de sesión para personalizar una página de inicio de sesión y ver con qué rapidez se muestran en su app las actualizaciones que realiza.

Para configurar una app de ejemplo desde la GUI:

1. Después de crear una instancia del servicio, puede elegir una app de ejemplo en un lenguaje en el que se sienta cómodo trabajando. Puede elegir entre iOS Swift, Android, Node.js y Java. ¿No desea utilizar un SDK? Puede integrar {{site.data.keyword.appid_short_notm}} utilizando las API.
2. Siga los pasos de la GUI para **Crear y ejecutar** su app de ejemplo. Cada lenguaje está configurado de forma ligeramente distinta, por lo que asegúrese de seleccionar el lenguaje de la app que ha descargado en la lista desplegable. Una vez que su app está configurada, puede abrirla en un navegador e iniciar la sesión con sus credenciales. Asegúrese de que estén instalados los requisitos previos para el lenguaje de la app.
  <dl>
    <dt> Android </dt>
      <dd><ul><li> Android API 27 o posterior </li><li> Java 8.x </li><li> Android SDK Tools 25.2.5+ </li><li> Android SDK Platform Tools 26.1.1+ </li><li> Android Build Tools versión 27.0.0+</li></ul></dd>
    <dt> iOS Swift </dt>
      <dd><ul><li> CocoaPods (versión 1.1.0 o posterior) </li><li> iOS 10.0 o posterior</li><li> MacOS 10.11.5 </li><li> Xcode (versión 9.0.1 o posterior) </li></ul></dd>
    <dt> Node.js </dt>
      <dd><ul><li> La CLI de {{site.data.keyword.Bluemix_notm}}</li></ul></dd>
    <dt> Java </dt>
      <dd><ul><li> La CLI de {{site.data.keyword.Bluemix_notm}} </li><li> Maven </li></ul></dd>
  </dl>

  ¿No ve el idioma que está buscando? No se preocupe. Puede utilizar {{site.data.keyword.appid_short_notm}} a través de las API. También puede consultar <a href="https://www.ibm.com/blogs/bluemix/tag/app-id/" target="_blank">nuestros blogs <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> para obtener más ayuda en otros idiomas.
  {: tip}

3. Pulse **Revisar actividad** para ver los sucesos de autenticación que se han producido. Después de iniciar la sesión, puede ver un suceso.
4. Personalice la experiencia de inicio de sesión. Puede seleccionar una imagen, como su logotipo y el color de la cabecera. Puede seleccionar una de las opciones de color o insertar un valor hex. Cuando esté satisfecho con la vista previa, pulse **Guardar cambios**.
5. En el navegador, actualice la página de inicio de sesión. Los cambios que ha realizado en el paso anterior ya son visibles.

## Pasos siguientes
{: #next}

¿Listo para entrar y empezar con sus propias apps? Primero, [añada el servicio a la app](/docs/services/appid/install.md). El servicio proporciona SDK para los idiomas más utilizados, pero si no ve un SDK para el idioma en el que está escrita la app, puede utilizar la API.

</br>
</br>
