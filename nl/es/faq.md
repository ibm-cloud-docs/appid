---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-17"

keywords: authentication, authorization, identity, app security, secure

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
{:faq: data-hd-content-type='faq'}


# Preguntas más frecuentes
{: #faq}

Estas preguntas más frecuentes proporcionan respuestas a preguntas comunes sobre el servicio {{site.data.keyword.appid_full}}.
{: shortdesc}


## ¿Cómo calcula {{site.data.keyword.appid_short_notm}} los precios?
{: #faq-pricing}
{: faq}

Con {{site.data.keyword.appid_short_notm}} paga menos cuantos más recursos utiliza.
{: shortdesc}

El plan de niveles graduado consta de tres partes: el número de sucesos de autenticación, seguridad normal y avanzada y el número de usuarios autorizados. Se le facturará cada mes en función del resumen de las dos partes. El precio total es el cargo acumulado de cada nivel de uso que consiste en la cantidad multiplicada por el precio unitario en ese nivel.

Los primeros 1000 sucesos de autenticación y 1000 usuarios autorizados son gratuitos cada mes, excepto los sucesos de seguridad avanzados. Los sucesos de seguridad avanzados generan cargos adicionales.

### Sucesos de autenticación
{: #faq-authentication}

Se produce un suceso de autenticación cuando se emite una nueva señal de acceso, normal o anónima. Las señales se pueden emitir como respuesta a una solicitud de inicio de sesión iniciada por un usuario o en nombre del usuario por parte de una app. De forma predeterminada, las señales de acceso son válidas durante una hora y las señales anónimas son válidas durante 30 días. Cuando la señal caduca debe crear una nueva para acceder a los recursos protegidos. Puede actualizar la hora de caducidad de las señales de {{site.data.keyword.appid_short_notm}} en la página **Proveedores de identidad > Gestionar > Valores de autenticación** del panel de control del servicio.

#### Características de seguridad avanzadas

Las características de seguridad avanzadas le proporcionan la posibilidad de fortalecer la seguridad de la aplicación.
{: shortdesc}

<table>
  <tr>
    <th>Función</th>
    <th>Ventaja</th>
  </tr>
  <tr>
    <td>Autenticación de multifactores</td>
    <td>[MFA para el directorio en la nube](/docs/services/appid?topic=appid-cd-mfa#cd-mfa) confirma la identidad de un usuario solicitando al usuario que especifique un código de acceso de una sola vez que se envía a su correo electrónico además de especificar el correo electrónico y la contraseña.</td>
  </tr>
  <tr>
    <td>Gestión de política de contraseñas</td>
    <td>Como propietario de una cuenta, puede imponer contraseñas más seguras para el directorio en la nube configurando un conjunto de reglas a las que deben ajustarse las contraseñas de usuario. Los ejemplos incluyen el número de intentos de inicio de sesión antes del bloqueo, las horas de caducidad, el intervalo de tiempo mínimo entre actualizaciones de contraseña o el número de veces que una contraseña no se puede repetir. Para obtener una lista completa de las opciones y de la información de configuración, consulte [Gestión avanzada de contraseñas](/docs/services/appid?topic=appid-cd-strength#cd-advanced-password).</td>
  </tr>
</table>

Las características de seguridad avanzadas están inhabilitadas de forma predeterminada. Si activa la autenticación de multifactores (MFA) o la gestión de políticas de contraseñas, se incurre un cargo adicional. Si inhabilita todas las características avanzadas, la cuenta vuelve a la política de costes más bajos. Por ejemplo, si ha obtenido 10.000 señales de acceso. A continuación, ha activado la gestión de políticas de contraseñas y ha obtenido 10.000 más. En ese caso, pagaría por 20.000 sucesos de autenticación y 10.000 sucesos de seguridad avanzada.

Estas características están disponibles solo para aquellas instancias que están en el plan de precios de nivel graduado y que se crearon después del 15 de marzo de 2018.
{: note}

### Usuarios autorizados
{: #faq-authorized}

Un usuario autorizado es un usuario exclusivo que inicia sesión con su servicio de forma directa o indirecta, incluidos los usuarios anónimos. Se le factura un usuario autorizado cada vez que un nuevo usuario inicia sesión en la aplicación, incluidos los usuarios anónimos. Por ejemplo, si un usuario inicia sesión con Facebook y más adelante con Google, se consideran dos usuarios autorizados diferentes.

Para obtener la información de precios más actualizada, puede generar una estimación del coste pulsando **Añadir a estimación** en la sección de {{site.data.keyword.appid_short_notm}} del [catálogo de {{site.data.keyword.cloud_notm}}](https://cloud.ibm.com/catalog/services/app-id).
{: tip}



## ¿Por qué tengo que incluir en una lista blanca mi URI de redirección?
{: #faq-redirect}
{: faq}

Un URI de redirección es el punto final de devolución de llamada de la app. Para evitar ataques de suplantación, {{site.data.keyword.appid_short_notm}} valida el URI con la lista blanca de URL de redirección. Cuando se produce phishing, existe la posibilidad de que un atacante obtenga acceso a las señales del usuario. Para obtener más información acerca de los URI de redirección, consulte [Adición de URI de redirección](/docs/services/appid?topic=appid-managing-idp#add-redirect-uri).

No incluya ningún parámetro de consulta en el URL. Se omitirán en el proceso de validación. URL de ejemplo: `http://host:[port]/path`
{: tip}



## ¿Cómo funciona el cifrado en {{site.data.keyword.appid_short_notm}}?
{: #faq-encryption}
{: faq}

Consulte la tabla siguiente para obtener respuestas a las preguntas más frecuentes sobre el cifrado.

<table>
  <thead>
    <th colspan=2><img src="images/idea.png" alt="Icono de más información"/>  </th>
  </thead>
  <tbody>
    <tr>
      <td>¿Por qué se utiliza el cifrado?</td>
      <td>Una forma de proteger la información de nuestros usuarios consiste en cifrar los datos de cliente en reposo. El servicio cifra datos de cliente en reposo con claves por arrendatario.</td>
    </tr>
    <tr>
      <td>¿Se han creado algoritmos propios? ¿Cuáles se utilizan en el código?</td>
      <td>No hemos creado algoritmos propios, el servicio utiliza <code>AES</code> y <code>SHA-256</code> con salting.</td>
    </tr>
    <tr>
      <td>¿Se utilizan módulos o proveedores de cifrado de código abierto o público? ¿Se exponen las funciones de cifrado en algún momento? </td>
      <td>El servicio utiliza bibliotecas Java <code>javax.crypto</code>, pero nunca expone una función de cifrado.</td>
    </tr>
    <tr>
      <td>¿Cómo se almacenan las claves?</td>
      <td>Las claves se generan y cifran con una clave maestra que es específica de cada región y que después se almacena localmente. Las claves maestras se almacenan en {{site.data.keyword.keymanagementserviceshort}}. En los niveles de almacenamiento y middleware existe un cifrado de nivel de servicio, lo que significa que hay una clave para todos los clientes. En el nivel de app, cada cliente tiene su propia clave de cifrado.</td>
    </tr>
    <tr>
      <td>¿Qué fortaleza de clave se utiliza?</td>
      <td>El servicio utiliza 16 bytes.</td>
    </tr>
    <tr>
      <td>¿Se invoca alguna API remota que exponga las capacidades de cifrado?</td>
      <td>No, no se hace.</td>
    </tr>
  </tbody>
</table>



## ¿Qué diferencia hay entre {{site.data.keyword.appid_short_notm}} y Keycloak?
{:# faq-keycloak}

Tanto {{site.data.keyword.appid_short_notm}} como Keycloak se pueden utilizar para añadir autenticación a las aplicaciones y a los servicios seguros. La principal diferencia entre las dos ofertas es la forma en la que están empaquetadas.
{: shortdesc}

Keycloak se empaqueta como software, lo que significa que usted, como desarrollador, es el responsable de mantener la funcionalidad del producto después de descargarlo. Usted es responsable del alojamiento, la alta disponibilidad, la conformidad, las copias de seguridad, la protección de DDoS, el equilibrio de carga, los cortafuegos web, las bases de datos y demás.

{{site.data.keyword.appid_short_notm}} es una oferta totalmente gestionada que se ofrece "como servicio". Esto significa que IBM se hace cargo del funcionamiento del servicio, controla la conformidad, la disponibilidad en varias zonas, el SLA y demás. {{site.data.keyword.appid_short_notm}} también tiene una experiencia integrada estándar con la plataforma de {{site.data.keyword.cloud_notm}} que incluye tiempos de ejecución y servicios nativos como, por ejemplo {{site.data.keyword.containershort_notm}}, {{site.data.keyword.openwhisk_short}} y {{site.data.keyword.cloudaccesstrailshort}}.
