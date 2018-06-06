---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Guía de aprendizaje de iniciación
{: #gettingstarted}

{{site.data.keyword.appid_full}} le ayuda a añadir autenticación a sus apps móviles y web y protege sus recursos de fondo.
{: shortdesc}

## Creación de una instancia de servicio
{: #create}

Cree una instancia de {{site.data.keyword.appid_short_notm}} para empezar.
{: shortdesc}

1. En el catálogo de {{site.data.keyword.Bluemix}}, seleccione {{site.data.keyword.appid_short_notm}}. Se abre la pantalla de configuración del servicio.
2. Dé un nombre a la instancia de servicio, o utilice el nombre preestablecido.
3. Para enlazar la instancia, seleccione una app del menú **Conectar a**. Si selecciona **Dejar sin enlazar**, podrá enlazar la instancia de servicio posteriormente.
4. Seleccione el plan de precios y pulse **Crear**.

## Configuración de una app de ejemplo
{: #sample-app}

Puede utilizar una de las apps de ejemplo preconfiguradas para familiarizarse con el servicio.
{: shortdesc}

De forma predeterminada, las apps de ejemplo están configuradas con dos proveedores de identidad y la posibilidad de revisar la autenticación. También puede utilizar la característica de widget de inicio de sesión para personalizar una página de inicio de sesión y ver con qué rapidez se muestran en su app las actualizaciones que realiza.

Para configurar una app de ejemplo desde la GUI:

1. Después de crear una instancia del servicio, puede elegir una app de ejemplo en un lenguaje con que se sienta cómodo trabajando. Puede elegir entre iOS Swift, Android, Node.js y Java. ¿No desea utilizar un SDK? Consulte nuestro blog para <a href="https://github.com/mnsn/appid-python-flask-example" target="_blank">utilizar {{site.data.keyword.appid_short_notm}} con otros lenguajes, como Python <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.
2. Siga los pasos en la GUI para **Compilar y ejecutar** su app de ejemplo. Cada lenguaje está configurado de forma ligeramente distinta, por lo que asegúrese de seleccionar el lenguaje de la app que ha descargado en la lista desplegable. Una vez que su app está configurada, puede abrirla en un navegador e iniciar la sesión con sus credenciales.
  **Nota**: Asegúrese de que tenga instalados los requisitos previos del lenguaje con el que desea trabajar.
  <dl>
    <dt> Android </dt>
      <dd><ul><li> Android API 25 o posterior </li><li> Java 8.x </li><li> Android SDK Tools 25.2.5+ </li><li> Android SDK Platform Tools 25.0.3+ </li><li> Android Build Tools versión 25.0.2 </li></ul></dd>
    <dt> iOS Swift </dt>
      <dd><ul><li> CocoaPods (versión 1.1.0 o posterior) </li><li> iOS 9 o posterior </li><li> MacOS 10.11.5 </li><li> Xcode 8.1 25.0.3+ </li></ul></dd>
    <dt> Node.js </dt>
      <dd><ul><li> CLI de Cloud Foundry </li></ul></dd>
    <dt> Java </dt>
      <dd><ul><li> CLI de Cloud Foundry </li><li> Maven </li></ul></dd>
  </dl>
3. Pulse **Revisar actividad** para ver los sucesos de autenticación que se han producido. Debería ver al menos un suceso si ha iniciado la sesión.
4. Personalice la experiencia de inicio de sesión. Puede seleccionar una imagen, como su logotipo y el color de la cabecera. Puede seleccionar una de las opciones de color o insertar un valor hex. Cuando esté satisfecho con la vista previa, pulse **Guardar cambios**. Puede ver un ejemplo de la experiencia de inicio de sesión en la siguiente imagen.
5. En el navegador, actualice la página de inicio de sesión. Los cambios que ha realizado en el paso anterior ya son visibles.
