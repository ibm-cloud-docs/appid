---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{: tip: .tip}

# Configuración de los proveedores de identidad social
{: #setting-up-idp}

Los proveedores de identidad proporcionan un nivel adicional de autenticación para sus apps móviles y web. Con {{site.data.keyword.appid_full}}, puede configurar uno o varios proveedores de identidad para establecer una experiencia de inicio de sesión único para la app.
{: shortdesc}

## Configuración predeterminada
{: #default}

{{site.data.keyword.appid_short_notm}} proporciona una configuración predeterminada para ayudar con la configuración inicial de los proveedores de identidad.
{: shortdesc}

Las credenciales predeterminadas están configuradas para Facebook y Google. Está limitado a 100 usos de las credenciales por instancia y por día. Dado que son credenciales de IBM, están pensadas para utilizarse solo en modalidad de desarrollo. Antes de publicar la app, actualice la configuración a sus propias credenciales.

## Incluir en la lista blanca el URL de redirección
{: #redirect}

Un URL de redirección es el punto final de devolución de llamada de la app. Para evitar ataques de phishing, el ID de App valida el URL en la lista blanca de las URL de redirección. Cuando se produce phishing, hay una posibilidad de que un atacante obtenga acceso a las señales del usuario.

Para añadir el URL a la lista blanca:

1. Vaya a **Proveedores de identidad > Gestionar**.
2. En el campo **Añadir URL de redirección web**, escriba el URL y pulse **+**.

No incluya ningún parámetro de consulta en el URL. Se omitirán en el proceso de validación. URL de ejemplo: `http://host:[port]/path`
{: tip}


## Configuración de Facebook
{: #facebook}

Puede configurar el servicio de {{site.data.keyword.appid_short}} para que utilice Facebook como proveedor de identidad.
{: shortdesc}

### Obtención de un ID de app y secreto de Facebook

Para utilizar Facebook como proveedor de identidad, debe añadir y configurar la plataforma de sitio web en su aplicación de Facebook.

1. Inicie sesión en su cuenta en el <a href="https://developers.facebook.com/docs/apps/register" target="_blank">sitio Facebook for Developers <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.
2. Anote el ID y el secreto de la app de Facebook. Estos valores son necesarios configurar el proyecto web para la autenticación en el panel de control de servicio.
3. Añada la plataforma web y especifique el URL del sitio.
4. En la lista de productos, seleccione **Inicio de sesión de Facebook **.
5. En el campo URL de redirección de OAuth válidos, especifique el URL de punto final de devolución de llamada del servidor de autorización.
6. Pulse **Guardar cambios**.


### Configuración de {{site.data.keyword.appid_short_notm}} para la autenticación de Facebook

Una vez que tenga el ID y secreto de la app de Facebook, y que la app de Facebook for Developers esté configurada para prestar servicio a los clientes web, puede editar la autenticación de Facebook en el panel de control del servicio.

1. Desde el separador **Gestionar** del panel de control del servicio, seleccione **Facebook** y pulse **Editar**.
2. Especifique el ID y el secreto de la app de Facebook que ha obtenido del sitio web de Facebook for Developers.
3. Copie el URI que está en el campo **URI de redirección para Facebook for Developers**. Copie el URI en el campo **URI de redirección de OAuth válido** en la sección **Inicio de sesión de Facebook** del portal de desarrolladores de Facebook.
4. Pulse **Guardar**.
5. Opcional: para apps web, especifique el URL de redirección en el campo **URL de redirección de la aplicación web**. Este valor está determinado por el desarrollador y se utiliza para acceder al URL de redirección una vez completado el proceso de autorización. El URL debe seguir un esquema `http` o `https`. Para obtener un mayor nivel de seguridad, utilice un esquema `https`.


## Configuración de Google
{: #google}

Puede configurar el servicio de {{site.data.keyword.appid_short}} para que utilice Google como proveedor de identidad.
{: shortdesc}

### Obtención de un ID de cliente y secreto de Google

Cree un proyecto en la <a href="https://developers.google.com/" target="_blank">consola de Google Developers <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>, configure el proyecto para que sirva a clientes web y obtenga un ID y un secreto de cliente.

1. Cree un proyecto.
2. Añada la API de Google+ a su proyecto de Google.
3. Añada las credenciales a la API de Google+.
    1. Seleccione la API de Google+ como tipo de API.
    2. Seleccione **Navegador web** como espacio en el que llamará la API.
    3. Seleccione **Datos de usuario**.
    4. Complete los campos necesarios para crear un ID de cliente. Se crea un secreto al mismo tiempo.
4. Anote el ID de cliente y secreto de Google. En el separador de credenciales, seleccione el ID que ha creado para obtener su secreto e ID de cliente.

### Configuración de {{site.data.keyword.appid_short}} para la autenticación de Google

Después de configurar el proyecto de Google y de tener el ID de cliente y el secreto, puede editar el panel de control de servicio para la autenticación de Google.

1. Desde el separador **Gestionar** del panel de control del servicio, seleccione **Google** y pulse **Editar**.
2. Especifique el ID de cliente y el secreto que haya obtenido de la consola de Google Developers.
3. Autorice el URL de {{site.data.keyword.appid_short}}.
    1. Copie el **URL de redirección de la consola de Google Developer** de los detalles del proveedor de identidades de Google.
    2. En el separador de credenciales de su proyecto de Google, seleccione el ID de cliente que haya creado para esta integración.
    3. Pegue el URL de {{site.data.keyword.appid_short}} en el campo **URI de redirección autorizados** y haga clic en **Guardar**.
4. Haga clic en **Guardar** para actualizar su configuración de Google en {{site.data.keyword.appid_short}}.
5. Para apps web, introduzca un URL de redirección en el separador **Gestionar**. Una vez que se haya completado el proceso de autorización, se envía un usuario a este URL. El URL debe seguir un esquema `http` o `https`. Para obtener un mayor nivel de seguridad, utilice un esquema `https`.
