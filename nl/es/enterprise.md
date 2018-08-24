---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}

# Configuración de los proveedores de identidad empresariales
{: #enterprise}

Si ya tiene un repositorio de usuario existente y una forma certificada para autenticar a los usuarios en sus sistemas internos, puede configurar el servicio de {{site.data.keyword.appid_full}} para utilizar un proveedor de identidad empresarial.
{: shortdesc}

## Comprensión de SAML
{: #saml}

SAML es un estándar abierto para intercambiar datos de autenticación y de autorización entre un proveedor de identidad que certifique la identidad del usuario y un proveedor de servicio que consuma la información de identidad de usuario.
{: shortdesc}

¿Cómo funciona?

{{site.data.keyword.appid_short_notm}} funciona como un proveedor de servicio e inicia un inicio de sesión único (SSO) en un proveedor de terceros como Active Directory Federation Services. El protocolo <a href="http://saml.xml.org/saml-specifications" target="_blank">SAML <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> admite perfiles distintos y opciones de enlace. {{site.data.keyword.appid_short_notm}} admite el perfil SSO del navegador web, con el enlace HTTP Post.

### Aserciones SAML y reclamaciones de señal de identidad

Una aserción SAML es un paquete de información que contiene una o varias sentencias. La aserción contiene la decisión de autorización, y podría contener información de identidad sobre el usuario.

Cuando un usuario inicia sesión con un proveedor de identidad, dicho proveedor envía una aserción a {{site.data.keyword.appid_short_notm}}. {{site.data.keyword.appid_short_notm}} propaga la información de identidad de usuario que se devuelve en la aserción SAML a la app como reclamaciones de señales OIDC. El atributo SAML debe corresponderse con una de las siguientes reclamaciones de OIDC que se añadirán a la señal de identidad.

Se pueden añadir las siguientes reclamaciones:
* `nombre`
* `correo electrónico`
* `entorno local`
* `imagen`

Los elementos de atributos SAML restantes que no se correspondan con ninguno de los nombres estándares se omitirán. Tenga en cuenta que, si uno o varios de estos valores cambian en el lado del proveedor, los nuevos valores estarán disponibles solo después de que el usuario inicie sesión de nuevo.

## Configuración de la app para trabajar con un proveedor de identidad SAML externo
{: #configuring-saml}

Puede configurar el servicio de {{site.data.keyword.appid_short_notm}} para que utilice un proveedor de identidad SAML (Security Assertion Markup Language).
{: shortdesc}

Para ver los pasos sobre cómo utilizar un proveedor de identidad SAML específico, consulte estas publicaciones de blog sobre la configuración de {{site.data.keyword.appid_short_notm}} con [Ping One ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-ping-one/), [Azure Active Directory ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-azure-active-directory/) o [Active Directory Federation Service ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-active-directory-federation-service/).
{: tip}

### Suministro de metadatos a su proveedor de identidad

Para configurar la app, debe proporcionar información a un proveedor de identidad compatible con SAML. La información se intercambia mediante un archivo XML de metadatos que también contiene datos de configuración que se utilizan para establecer la confianza.

1. En el separador **Gestionar** del panel de control {{site.data.keyword.appid_short_notm}}, establezca **SAML 2.0** en **Activado**. A continuación, pulse **Editar** para configurar los valores de SAML.
2. Pulse **Descargar archivo de metadatos SAML**. El proveedor de identidad espera la información siguiente del archivo.
  <table>
    <tr>
      <th> Variable </th>
      <th> Descripción </th>
    </tr>
    <tr>
      <td><code>ID de entidad</code></td>
      <td>El identificador que permite al proveedor de identidad saber que {{site.data.keyword.appid_short_notm}} ha emitido la solicitud SAML.</td>
    </tr>
    <tr>
      <td><code>URL de ubicación</code></td>
      <td>La ubicación que el proveedor de identidad envía a las aserciones de SAML tras autenticar correctamente un usuario.</td>
    </tr>
    <tr>
      <td><code>Enlace</code></td>
      <td>Instrucciones sobre cómo debería enviar el proveedor de identidad la respuesta SAML.</td>
    </tr>
    <tr>
      <td><code>Formato de ID de nombre</code></td>
      <td>Forma en la que el proveedor de identidad sabe qué formato de identificador necesita para enviarlo en el asunto de una aserción. La forma en que {{site.data.keyword.appid_short_notm}} identifica a los usuarios.</td>
    </tr>
    <tr>
      <td><code>WantAssertionsSigned</code></td>
      <td>Forma en la que un proveedor de identidad comprueba para ver si necesita firmar la aserción. El servicio espera a que se firme la aserción, pero no da soporte a las aserciones cifradas.</td>
    </tr>
  </table>

3. Proporcione los datos a su proveedor de identidad. Si el proveedor de identidad permite cargar el archivo de metadatos, puede hacerlo. Si no lo permite, configure las propiedades manualmente. No todos los proveedores de identidad utilizarán las mismas propiedades, por lo que si no las utiliza todas, es correcto.

Los nombres de propiedades pueden diferir entre los proveedores de identidad.
{: tip}

### Suministro de metadatos a {{site.data.keyword.appid_short_notm}}

Necesitará obtener datos del proveedor de identidad y proporcionarlos a {{site.data.keyword.appid_short_notm}}.

1. Vaya al separador **SAML 2.0** del panel de control de {{site.data.keyword.appid_short_notm}}. Entre los metadatos siguientes que ha obtenido del proveedor de identidad en la sección **Proporcionar metadatos de IdP SAML**.
  <table>
    <tr>
      <th> Variable </th>
      <th> Descripción </th>
    </tr>
    <tr>
      <td><code>URL de inicio de sesión</code></td>
      <td>El URL al que se redirige el usuario para su autenticación. Se aloja mediante el proveedor de identidad SAML.</td>
    </tr>
    <tr>
      <td><code>ID de entidad</code></td>
      <td>Nombre exclusivo globalmente para un proveedor de identidad SAML.</td>
    </tr>
    <tr>
      <td><code>Certificado de firma</code></td>
      <td>Certificado emitido por el proveedor de identidad SAML. Se utiliza para firmar y validar aserciones SAML. Todos los proveedores son distintos, pero podría descargar el certificado de firma desde el proveedor de identidad. El certificado debe estar en formato <code>.pem</code>.</td>
    </tr>
  </table>

2. Opcional: Proporcione un **Certificado secundario** que se utilice si la validación de firma falla en el certificado primario. Si la clave de firma sigue siendo la misma, {{site.data.keyword.appid_short_notm}} no bloquea la autenticación de certificados caducados.

3. Actualice el **Nombre de proveedor** y pulse **Guardar**. El nombre predeterminado es SAML.


### Probar la configuración

Puede probar la configuración entre el proveedor de identidad SAML y {{site.data.keyword.appid_short_notm}}.

1. Asegúrese de que haya guardado la configuración.
2. Vaya al separador **SAML 2.0** del panel de control de {{site.data.keyword.appid_short_notm}} y pulse **Probar**. Se abre un nuevo separador.
3. Inicie sesión con un usuario que ya haya autenticado su proveedor de identidad.
4. Después de completar el formulario, se le redirigirá a otra página.
  * Autenticación correcta: La conexión entre {{site.data.keyword.appid_short_notm}} y el proveedor de identidad funciona correctamente. La página muestra [señales de acceso y de identidad](/docs/services/appid/authorization.html#key-concepts) válidas.
  * Error de autenticación: La conexión se ha bloqueado. La página muestra los errores y el archivo XML de la respuesta SAML.
