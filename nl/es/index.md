---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-27"

keywords: authentication, authorization, identity, app security, secure, development,

subcollection: appid

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}

# Guía de aprendizaje de iniciación
{: #getting-started}

La seguridad de aplicación se puede complicar de forma increíble. Para la mayoría de los desarrolladores, es una de las partes más difíciles de la creación de una app. ¿Cómo puede estar seguro de que está protegiendo la información de los usuarios? Al integrar {{site.data.keyword.appid_full}} en sus apps, puede proteger recursos y añadir autenticación; incluso aunque no tenga mucha experiencia en seguridad.
{: shortdesc}

Al exigir a los usuarios que inicien sesión en la app, puede almacenar datos de usuario como preferencias de la app o información de los perfiles sociales públicos, y luego utilizar esos datos para personalizar cada experiencia de la app. {{site.data.keyword.appid_short_notm}} proporciona un registro para el usuario, pero también puede traer las pantallas de inicio de sesión de su propia marca al trabajar con el directorio en la nube.

Nos gustaría conocer su opinión con comentarios y preguntas.
* Si tiene preguntas técnicas sobre {{site.data.keyword.appid_short_notm}}, publique la pregunta en <a href="https://stackoverflow.com/search?q=ibm-appid" target="_blank">Stack Overflow <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> y etiquete la pregunta con `ibm-appid`.
* Para formular preguntas sobre el servicio y obtener instrucciones de iniciación, utilice el foro <a href="https://developer.ibm.com/answers/topics/appid/" target="_blank">dW Answers <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>. Incluya la etiqueta `appid`.

## Creación de una instancia de servicio
{: #create}

Cree y enlace una instancia de {{site.data.keyword.appid_short_notm}} a su app para empezar.
{: shortdesc}

1. En el catálogo de {{site.data.keyword.cloud_notm}}, seleccione {{site.data.keyword.appid_short_notm}}. Se abre la pantalla de configuración del servicio.
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

De forma predeterminada, las apps de ejemplo están configuradas con dos proveedores de identidad y la posibilidad de revisar la autenticación. Las apps de ejemplo se ofrecen en `iOS Swift`, `Android`, `Node.js` y `Java`. Si no ve ningún idioma con el que se sienta cómo trabajando, no se preocupe. Puede integrar {{site.data.keyword.appid_short_notm}} en su propia aplicación de ejemplo utilizando las API proporcionadas.

Para crear una app de ejemplo:

1. Pulse **Descargar ejemplo**.
2. Pulse en el idioma de su elección para descargar el ejemplo.
  ¿No ve el idioma que está buscando? No se preocupe. Puede utilizar {{site.data.keyword.appid_short_notm}} a través de las API. También puede consultar <a href="https://www.ibm.com/blogs/bluemix/tag/app-id/" target="_blank">nuestros blogs <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> para obtener más ayuda en otros idiomas.
  {: tip}
3. Asegúrese de que ha instalado o completado los requisitos previos.
4. Siga los pasos de **Crear y ejecutar** para configurar el ejemplo con {{site.data.keyword.appid_short_notm}}.
5. Haga clic en **Revisar actividad** para ver los sucesos de autenticación que se han producido. Cualquier tipo de inicio de sesión crea un suceso visible en esta página.
6. Personalice el widget de inicio de sesión.
  1. Añada una imagen como, por ejemplo, un logotipo pulsando en **Seleccionar** y examinando el sistema local para que se cargue una imagen.
  2. Elija un esquema de color seleccionando una de las opciones de color o especificando un valor hexadecimal.
  3. Cambie entre web y móvil para ver el aspecto que tiene el esquema de colores en cada dispositivo.
  4. Cuando esté satisfecho con las opciones, pulse **Guardar cambios**.
7. En un navegador, actualice la página de inicio de sesión. Los cambios que ha realizado en el paso anterior ya son visibles.


## Pasos siguientes
{: #next}

¿Listo para entrar y empezar con sus propias apps? Primero, [añada el servicio a la app](/docs/services/appid?topic=appid-web-apps#web-apps). El servicio proporciona SDK para los idiomas más utilizados, pero si no ve un SDK para el idioma en el que está escrita la app, puede sacar partido de {{site.data.keyword.appid_short_notm}} utilizando las API.
