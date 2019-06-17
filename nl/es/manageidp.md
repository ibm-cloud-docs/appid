---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-20"

keywords: authentication, authorization, identity, app security, secure, development, identity provider, tokens, customization, lifetime

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


# Gestión de autenticaciones
{: #managing-idp}

Los proveedores de identidad (IdP) añaden un nivel de seguridad para sus apps móviles y web a través de la autenticación. Con {{site.data.keyword.appid_full}}, puede configurar uno o varios proveedores de identidad para crear una experiencia de inicio de sesión personalizada para los usuarios.
{: shortdesc}


{{site.data.keyword.appid_short_notm}} interactúa con los proveedores de identidad utilizando varios protocolos, como OpenID Connect, SAML, etc. Por ejemplo, OpenID Connect es el protocolo que se utiliza con varios proveedores sociales, como Facebook o Google. Los proveedores de empresa como <a href="https://www.ibm.com/cloud/blog/setting-ibm-cloud-app-id-azure-active-directory" target="_blank">Azure Active Directory <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> o <a href="https://www.ibm.com/cloud/blog/setting-ibm-cloud-app-id-active-directory-federation-service" target="_blank">Active Directory Federation Service <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> suelen utilizar SAML como su protocolo de identidad. Para [Directorio en la nube](/docs/services/appid?topic=appid-cloud-directory), el servicio utiliza SCIM para verificar la información de identidad.

Cuando utiliza proveedores de identidad sociales o de empresa, {{site.data.keyword.appid_short_notm}} tiene acceso de lectura a la información de cuenta de un usuario. El servicio utiliza una señal y aserciones devueltas por el proveedor de identidad para verificar que un usuario es quien dice ser. Puesto que el servicio nunca tiene acceso de escritura a la información, los usuarios deben pasar por el proveedor de identidad elegido para realizar acciones como, por ejemplo, restablecer la contraseña. Por ejemplo, si un usuario inicia sesión en la app con Facebook y después desea cambiar la contraseña, deberá ir a `www.facebook.com` para hacerlo.

Cuando utiliza [Directorio en la nube](/docs/services/appid?topic=appid-cloud-directory), {{site.data.keyword.appid_short_notm}} es el proveedor de identidad. El servicio utiliza el registro para verificar la identidad de los usuarios. Puesto que {{site.data.keyword.appid_short_notm}} es el proveedor, los usuarios pueden sacar partido de la funcionalidad avanzada y restablecer la contraseña directamente en la app.

¿Está trabajando con la identidad de la aplicación? Consulte [Identidad de aplicación](/docs/services/appid?topic=appid-app).
{: tip}

El servicio está configurado para utilizar varios proveedores. Consulte la siguiente tabla para obtener más información sobre las opciones.

<table>
  <tr>
    <th>Proveedor</th>
    <th>Tipo</th>
    <th>Descripción</th>
  </tr>
  <tr>
    <td>[Directorio en la nube](/docs/services/appid?topic=appid-cloud-directory)</td>
    <td>Registro gestionado</td>
    <td>Puede mantener su propio registro de usuarios en la nube. Cuando un usuario se registra en su app, este se añade al directorio de usuarios. Esta opción proporciona a los usuarios más libertad para gestionar su propia cuenta dentro de la app.</td>
  </tr>
  <tr>
    <td>[SAML](/docs/services/appid?topic=appid-enterprise#enterprise)</td>
    <td>Empresa</td>
    <td>Puede crear una experiencia de inicio de sesión único para los usuarios finales.</td>
  </tr>
  <tr>
    <td>[Facebook](/docs/services/appid?topic=appid-social#facebook)</td>
    <td>Social</td>
    <td>Los usuarios finales pueden iniciar sesión en la app utilizando las credenciales de Facebook.</td>
  </tr>
  <tr>
    <td>[Google+](/docs/services/appid?topic=appid-social#google)</td>
    <td>Social</td>
    <td>Los usuarios finales pueden iniciar sesión en la app utilizando las credenciales de Google.</td>
  </tr>
  <tr>
    <td>[Personalizado](/docs/services/appid?topic=appid-custom-identity#custom-identity)</td>
    <td> </td>
    <td>Si ninguna de las opciones proporcionadas se ajusta a sus necesidades específicas, puede configurar su propio flujo de identidad para que funcione con {{site.data.keyword.appid_short_notm}}.</td>  
  </tr>
</table>

## Gestión de proveedores
{: #managing-providers}

Un proveedor de identidad crea y gestiona información sobre una entidad como, por ejemplo, un usuario, un ID funcional o una aplicación. El proveedor verifica la identidad de la entidad utilizando credenciales como, por ejemplo, una contraseña. A continuación, el proveedor de identidad envía la información de identidad a otro proveedor de servicios. Puesto que el proveedor de identidad autentica la entidad, {{site.data.keyword.appid_short_notm}} puede autorizarla y otorgar acceso a las apps.
{: shortdesc}

Para gestionar los proveedores de identidad:

1. Vaya al panel de control del servicio.
2. En la sección **Proveedores de identidad** de la navegación, seleccione la página **Gestionar**.
3. En el separador **Proveedores de identidad**, establezca los proveedores que desea utilizar en **Activados**.
4. Opcional: Decida si desea desactivar los **Usuarios anónimos** o dejar el valor predeterminado, que es **Activado**. Cuando se establecen en **Activados**, los atributos de usuario se asocian con el usuario desde el momento en que empiezan a interactuar con la app. Para obtener más información sobre la vía de acceso para convertirse en un usuario identificado, consulte [Autenticación progresiva](/docs/services/appid?topic=appid-anonymous#progressive)

{{site.data.keyword.appid_short_notm}} proporciona credenciales predeterminadas para ayudarle con la configuración inicial de Facebook y Google+. Está limitado a 100 usos de las credenciales por instancia y por día. Puesto que son credenciales de IBM, están pensadas para utilizarse solo en el desarrollo. Antes de publicar la app, actualice la configuración a sus propias credenciales.
{: tip}


## Adición de URI de redirección
{: #add-redirect-uri}

Un URI de redirección es el punto final de devolución de llamada de la app. Durante el flujo de inicio de sesión, {{site.data.keyword.appid_short_notm}} valida los URI antes de permitir que los clientes participen en el flujo de trabajo de autorización, lo que ayuda a impedir ataques de phishing y filtraciones de código. Al registrar el URI, está diciendo a {{site.data.keyword.appid_short_notm}} que el URI es de confianza y que es correcto redirigir a los usuarios.

Asegúrese de registrar solo los URI de las aplicaciones en las que confía.
{: note}


1. Pulse **Valores de autenticación** para ver las opciones de URI y configuración de señales.

2. En el campo **Añadir URI de redirección web**, escriba el URI. Cada URI debe empezar por `http://` o `https://` y debe incluir la vía de acceso completa, con los parámetros de consulta para que la redirección funcione correctamente. ¿Necesita ayuda para formatear el URI? Consulte la tabla siguiente para ver algunos ejemplos.

  <table>
    <tr>
      <th>Tipo</th>
      <th>URI de ejemplo</th>
    </tr>
    <tr>
      <td>Dominio personalizado</td>
      <td><code>http://mydomain.net/myapp2path/appid_callback</code></td>
    </tr>
    <tr>
      <td>Subdominio de ingreso</td>
      <td><code>https://mycluster.us-south.containers.appdomain.cloud/myapp1path/appid_callback</code></td>
    </tr>
    <tr>
      <td>Cierre de sesión</td>
      <td><code>http://mydomain.net/myapp2path/appid_logout</code></td>
    </tr>  
  </table>

3. Pulse el símbolo **+** en el recuadro **Añadir URI de redirección web**.

4. Repita los pasos uno a tres hasta que todos los URI posibles se añadan a la lista.



¿No está seguro de dónde proviene su URI de redirección? Mire el siguiente breve vídeo para ver cómo obtenerlo y cómo añadirlo a su lista.

<iframe class="embed-responsive-item" id="redirecturi" title="{{site.data.keyword.appid_short_notm}}: Cómo arreglar un URI de redirección no válido" type="text/html" width="640" height="390" src="//www.youtube.com/embed/6hxqbvpc054?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>



## Configuración del período de vida de la señal
{: #idp-token-lifetime}

El tiempo de vida de la señal empieza de nuevo en cada inicio de sesión de usuario. Por ejemplo, establece el período de vida de la señal de renovación en 10 días. Cuando el usuario inicia sesión por primera vez, se crea una señal de acceso y de renovación. Si el usuario vuelve a la app unos días más tarde, 3 días para ser específicos, no necesitará volver a iniciar sesión. Pero si el usuario ha esperado 12 días después de su primer inicio de sesión y después vuelve a la app, entonces deberá volver a iniciar sesión y un conjunto de señales se asociará con el usuario. Para obtener más información sobre las señales, consulte [Visión general de las señales](/docs/services/appid?topic=appid-tokens#tokens).

1. Para permitir el inicio de sesión sin la interacción del usuario, establezca las **señales de renovación** en **Activado**.

2. Establezca el período de vida de la señal de renovación. La caducidad se establece en días y puede ser cualquier valor que se encuentre en un rango de 1 a 90. Cuanto menor sea el número, el usuario deberá registrarse con más frecuencia.

3. Establezca el período de vida de la señal de acceso. La caducidad se establece en minutos y puede tener un rango entre 5 y 1440. Cuanto menor sea el valor, dispondrá de más protección cuando le roben la señal.

4. Establezca el período de vida de la señal anónima. Una [señal anónima](/docs/services/appid?topic=appid-anonymous#progressive) se asigna a los usuarios en el momento en que empiezan a interactuar con la app. Cuando un usuario inicia sesión, la información de la señal anónima se transfiere a la señal asociada con el usuario. La caducidad se establece en días y puede ser cualquier valor entre 1 y 90.


Cuando se establece la caducidad de señal, se aplica a todos los proveedores que ha configurado, incluidos los sociales y las empresas.
{: tip}
