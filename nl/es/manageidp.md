---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}


# Gestión
{: #managing}

Los proveedores de identidad (IdP) añaden un nivel de seguridad para sus apps móviles y web a través de la autenticación. Con {{site.data.keyword.appid_full}}, puede configurar uno o varios proveedores de identidad para crear una experiencia de inicio de sesión personalizada para los usuarios.
{: shortdesc}


**¿Qué es un proveedor de identidad?**

Un proveedor de identidad crea y gestiona información sobre una entidad como, por ejemplo, un usuario, un ID funcional o una aplicación. El proveedor verifica la identidad de la entidad utilizando credenciales como, por ejemplo, una contraseña. A continuación, el proveedor de identidad envía la información de identidad a otro proveedor de servicios. Puesto que el proveedor de identidad autentica la entidad, {{site.data.keyword.appid_short_notm}} puede autorizarla y otorgar acceso a las apps.

</br>

**¿Cuáles son los proveedores de identidad para los que {{site.data.keyword.appid_short_notm}} proporciona una integración?**

El servicio está preconfigurado para utilizar varios proveedores.

<table>
  <tr>
    <th>Proveedor</th>
    <th>Tipo</th>
    <th>Descripción</th>
  </tr>
  <tr>
    <td>[Directorio en la nube ](/docs/services/appid/cloud-directory.html)</td>
    <td>Registro gestionado</td>
    <td>Puede mantener su propio registro de usuarios en la nube. Cuando un usuario se registra en su app, este se añade al directorio de usuarios. Esta opción proporciona a los usuarios más libertad para gestionar su propia cuenta dentro de la app.</td>
  </tr>
  <tr>
    <td>[SAML](/docs/services/appid/enterprise.html)</td>
    <td>Empresa</td>
    <td>Puede crear una experiencia de inicio de sesión único para los usuarios finales.</td>
  </tr>
  <tr>
    <td>[Facebook](/docs/services/appid/identity-providers.html#facebook)</td>
    <td>Social</td>
    <td>Los usuarios finales pueden iniciar sesión en la app utilizando las credenciales de Facebook.</td>
  </tr>
  <tr>
    <td>[Google+](/docs/services/appid/identity-providers.html#google)</td>
    <td>Social</td>
    <td>Los usuarios finales pueden iniciar sesión en la app utilizando las credenciales de Google+.</td>
  </tr>
  <tr>
    <td>[Personalizado](/docs/services/appid/custom.html)</td>
    <td> </td>
    <td>Si ninguna de las opciones proporcionadas se ajusta a sus necesidades específicas, puede configurar su propio flujo de identidad para que funcione con {{site.data.keyword.appid_short_notm}}.</td>
  </tr>
  
</table>

</br>

**¿Cómo interactúa {{site.data.keyword.appid_short_notm}} con un proveedor de identidad?**

{{site.data.keyword.appid_short_notm}} interactúa con los proveedores de identidad utilizando varios protocolos, como OpenID Connect, SAML, etc. Por ejemplo, OpenID Connect es el protocolo que se utiliza con varios proveedores sociales, como Facebook o Google. Los proveedores de empresa como <a href="https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-azure-active-directory/" target="_blank">Azure Active Directory <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> o <a href="https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-active-directory-federation-service/" target="_blank">Active Directory Federation Service <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> suelen utilizar SAML como su protocolo de identidad. Para [Directorio en la nube](cloud-directory.html), el servicio utiliza SCIM para verificar la información de identidad.

¿Está trabajando con la identidad de la aplicación? Consulte [Identidad de aplicación](app-to-app.html).
{: tip}

</br>
</br>

## Configuración de valores
{: #configuring}

Puede decidir qué proveedores desea utilizar, los URL de redirección y la información de la señal para la app. Los valores que configure se aplican en todos los proveedores de identidad de esta instancia del servicio. Por ejemplo: cuando establece la caducidad de la señal, se aplica a todos los proveedores que ha configurado, ya sean los de su empresa o sociales.

</br>

**Para configurar los proveedores:**

1. Vaya al panel de control del servicio.
2. En la sección **Proveedores de identidad** de la navegación, seleccione la página **Gestionar**.
3. En el separador **Proveedores de identidad**, establezca los proveedores que desea utilizar en **Activados**.
4. Opcional: Decida si desea desactivar los **Usuarios anónimos** o dejar el valor predeterminado, que es **Activado**. Cuando se establecen en **Activados**, los atributos de usuario personalizados se asocian con el usuario desde el momento en que empiezan a interactuar con la app. Para obtener más información sobre la vía de acceso para convertirse en un usuario identificado, consulte [Autenticación progresiva](progressive.html#progressive).

{{site.data.keyword.appid_short_notm}} proporciona credenciales predeterminadas para ayudarle con la configuración inicial de Facebook y Google+. Está limitado a 100 usos de las credenciales por instancia y por día. Puesto que son credenciales de IBM, están pensadas para utilizarse solo en el desarrollo. Antes de publicar la app, actualice la configuración a sus propias credenciales.
{: tip}

</br>

**Para configurar los valores:**

1. Añada los URL de redirección. Un URL de redirección es el punto final de devolución de llamada de la app. Para evitar los ataques de phishing, {{site.data.keyword.appid_short_notm}} valida los URL con la lista blanca.
  1. En el campo **Añadir URL de redirección web**, escriba el URL y pulse en el icono **+**.
  2. Repita el paso 1 hasta que todos los URL de redirección posibles se añadan a la lista.

  No incluya ningún parámetro de consulta en el URL. Se omitirán en el proceso de validación. Por ejemplo: `http://host:[port]/path`
  {: tip}

2. Configure las señales. El tiempo de vida de la señal empieza de nuevo en cada inicio de sesión de usuario. Por ejemplo, establece el período de vida de la señal de renovación en 10 días. Cuando el usuario inicia sesión por primera vez, se crea una señal de acceso y de renovación. Si el usuario vuelve a la app unos días más tarde, 3 días para ser específicos, no necesitará volver a iniciar sesión. Pero si el usuario ha esperado 12 días después de su primer inicio de sesión y después vuelve a la app, entonces deberá volver a iniciar sesión y un conjunto de señales se asociará con el usuario.
  1. Para permitir el inicio de sesión sin la interacción del usuario, establezca las **señales de renovación** en **Activado**.
  2. Establezca el período de vida de la señal de renovación. La caducidad se establece en días y puede ser cualquier valor que se encuentre en un rango de 1 a 90. Cuanto menor sea el número, el usuario deberá registrarse con más frecuencia.
  3. Establezca el período de vida de la señal de acceso. La caducidad se establece en minutos y puede tener un rango entre 5 y 1440. Cuanto menor sea el valor, dispondrá de más protección cuando le roben la señal.
  4. Establezca el período de vida de la señal anónima. Una [señal anónima](/docs/services/appid/progressive.html#anonymous) se asigna a los usuarios en el momento en que empiezan a interactuar con la app. Cuando un usuario inicia sesión, la información de la señal anónima se transfiere a la señal asociada con el usuario. La caducidad se establece en días y puede ser cualquier valor entre 1 y 90.

</br>
</br>
