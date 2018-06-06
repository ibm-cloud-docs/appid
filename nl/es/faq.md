---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-02"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# Preguntas más frecuentes (FAQ)

Estas preguntas más frecuentes proporcionan respuestas a preguntas comunes sobre el servicio de {{site.data.keyword.appid_full}}.
{: shortdesc}


## ¿Cómo calcula {{site.data.keyword.appid_short_notm}} los precios?
{: #pricing}

Con {{site.data.keyword.appid_short_notm}} paga menos cuantos más recursos utiliza.
{: shortdesc}

El plan de niveles graduado consta de dos partes: El número de sucesos de autenticación y el de usuarios autorizados. Se le facturará cada mes en función del resumen de las dos partes. El precio total es el cargo acumulado de cada nivel de uso que consiste en la cantidad multiplicada por el precio unitario en ese nivel.

### Sucesos de autenticación

Un suceso de autenticación ocurre cuando se emite una señal nueva de {{site.data.keyword.appid_short_notm}}. Para los usuarios identificados, cada nueva señal es válida durante una hora. Para los usuarios anónimos las señales son válidas durante un mes. Cuando la señal caduca debe crear una nueva para acceder a los recursos protegidos. Cuando utiliza el ID de app para la autenticación móvil las señales de usuario se almacenan en `key-store/key-chain` y se agregan a cada solicitud futura. Las señales son accesibles utilizando el SDK de Swift de Android o iOS de {{site.data.keyword.appid_short_notm}}. Cuando utiliza el servicio para la autenticación web, <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">almacene la señal de usuario <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> en las cookies de sesión.

### Usuarios autorizados

Un usuario autorizado es un usuario exclusivo que inicia sesión con su servicio directa o indirectamente. Se le factura un usuario autorizado cada vez que un nuevo usuario inicia sesión desde cada proveedor de identidad, incluyendo los usuarios anónimos. Por ejemplo, si un usuario inicia sesión con Facebook y más adelante con Google, se consideran dos usuarios autorizados diferentes.

Para obtener más información sobre los precios por nivel graduado, consulte los [documentos de precios de {{site.data.keyword.Bluemix_notm}}](/docs/billing-usage/how_charged.html#services).

</br>

## ¿Qué tipo de actividad supervisa App ID?
{: #activity-monitor}

Puede realizar el seguimiento de la actividad que se ha generado dentro de la app que está enlazada con la instancia de servicio. También puede supervisar la actividad administrativa realizada en App ID utilizando el servicio Activity Tracker.

Para ver la actividad generada por su app:

1. Inicie sesión en la cuenta de IBM Cloud.
2. En el panel de control, seleccione su instancia de App ID.
3. Pulse el separador **Visión general**.
4. Visualice la actividad listada en **Registro de actividad**.

</br>
Para supervisar la actividad administrativa:

1. Inicie sesión en la cuenta de IBM Cloud. Navegue a la organización y espacio donde ha suministrado la instancia de App ID.
2. Desde el catálogo, suministre una instancia del servicio Activity Tracker. Asegúrese de estar en el mismo espacio que la instancia de App ID.
3. En el panel de control de Activity Tracker, pulse el separador **Gestionar**.
4. En la lista desplegable, seleccione las siguientes configuraciones para buscar todos los sucesos generados por App ID.
<table>
  <tr>
    <th> Campo </th>
    <th> Configuración </th>
  </tr>
  <tr>
    <td><i>Ver registros</i></td>
    <td><b>Registros de espacio</b></td>
  </tr>
  <tr>
    <td><i>Buscar</i></td>
    <td><b>target.name</b></td>
  </tr>
  <tr>
    <td>Filtro</td>
    <td>appid</td>
  </tr>
</table>
5. Pulse **Filtrar**.

Consulte la [documentación de Activity Tracker](/docs/services/cloud-activity-tracker/index.html) para obtener más información sobre el funcionamiento del servicio.
