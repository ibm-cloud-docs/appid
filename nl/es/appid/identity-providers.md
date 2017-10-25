---

copyright:
  years: 2017
lastupdated: "2017-06-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Configuración de los proveedores de identidad
{: #setting-up-idp}

Puede configurar Facebook, Google, IBMid o una combinación de los tres para que se utilice un inicio de sesión único para los usuarios. Utilizando un proveedor de identidad, los usuarios pueden iniciar la sesión con unas credenciales a las que ya están familiarizados.
{:shortdesc}


## Configuración de la autenticación de Facebook
{: #facebook}

Configure el servicio de {{site.data.keyword.appid_short}} para utilizar Facebook como proveedor de identidad.


### Obtención de un ID de app y secreto de Facebook
{: #getting-facebook-appid}

Para utilizar Facebook como proveedor de identidad en sus apps web o móviles, debe añadir y configurar la plataforma de sitio web en su aplicación de Facebook.

1. Inicie sesión en su cuenta en el <a href="https://developers.facebook.com/docs/apps/register" target="_blank">sitio Facebook for Developers <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.
2. Anote el ID y el secreto de la app de Facebook. Estos valores son necesarios configurar el proyecto web para la autenticación en el panel de control de servicio.
3. Añada la plataforma web y especifique el URL del sitio.
4. En la lista de productos, seleccione **Inicio de sesión de Facebook **.
5. En el campo URL de redirección de OAuth válidos, especifique el URL de punto final de devolución de llamada del servidor de autorización. Tras configurar la instancia de servicio, puede añadir este valor.
6. Pulse **Guardar cambios**.

### Configuración de {{site.data.keyword.appid_short_notm}} para la autenticación de Facebook
{: #configuring-facebook-appid}

Una vez que tenga el ID y secreto de la app de Facebook, y que la app de Facebook for Developers esté configurada para prestar servicio a los clientes web, puede editar la autenticación de Facebook en el panel de control del servicio.

1. Desde el separador **Gestionar** del panel de control del servicio, seleccione **Facebook** y pulse **Editar**.
2. Especifique el ID y el secreto de la app de Facebook que ha obtenido del sitio web de Facebook for Developers.
3. Copie el URI que está en el campo **URI de redirección para Facebook for Developers**. Copie el URI en el campo **URI de redirección de OAuth válido** en la sección **Inicio de sesión de Facebook** del portal de desarrolladores de Facebook.
4. Pulse **Guardar**.
5. Opcional: para apps web, especifique el URL de redirección en el campo **URL de redirección de la aplicación web**. Este valor está determinado por el desarrollador y se utiliza para acceder al URL de redirección una vez completado el proceso de autorización.


## Configuración de la autenticación de Google
{: #google}

Configure el servicio de {{site.data.keyword.appid_short_notm}} para utilizar Google como proveedor de identidad.


### Obtención de un ID de cliente y secreto de Google
{: #google-client-id}

Para utilizar Google como proveedor de identidad, obtenga un ID de cliente y secreto de Google y cree un proyecto en Google Developer Console.

1. Abra la aplicación de Google en la <a href="https://console.developers.google.com/apis/library" target="_blank">consola del desarrollador de Google <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.
2. Añada la API de Google+.
3. Cree credenciales mediante OAuth. En el campo **Tipo de aplicación**, seleccione **Aplicación web**. En el campo **URI de redirección autorizados**, especifique el URI de redirección de {{site.data.keyword.appid_short_notm}}. Puede obtener el URI de autorización de redirección de {{site.data.keyword.appid_short_notm}} desde la pantalla de configuración de Google del panel de control del servicio.
4. Anote el ID de cliente y el secreto de Google y guarde los cambios.



### Configuración de {{site.data.keyword.appid_short_notm}} para la autenticación de Google
{: #google-client-appid}

Una vez que tenga el cliente y secreto de Google, y la consola de Google Developers esté configurada para prestar servicio a los clientes web, puede editar la autenticación de Google en el panel de control del servicio.

1. Desde el separador **Gestionar** del panel de control del servicio, seleccione **Google** y pulse **Editar**.
3. Especifique el ID de cliente y el secreto de Google que ha obtenido de la consola de Google Developers.
4. Copie el URI que está en el campo **URI de redirección para Google for Developers**. Copie el URI en el campo **URI de redirección autorizados** que se encuentra en **Restricciones** en la sección **ID de cliente para la aplicación web** del portal de desarrolladores de Google.
5. Pulse **Guardar**.
6. Opcional: para apps web, especifique el URI de redirección en el campo **URI de redirección de la aplicación web**. Este valor se determina por parte del desarrollador y el que se utiliza para acceder a la redirección URI después de la autorización proceso se completa.


## Configuración de la autenticación de IBMid

Para utilizar IBMid como proveedor de identidad, utilice la <a href="https://ibm.ent.box.com/notes/78040808400?v=IBMid-Federation-Guide" target="_blank">Guía de federación de IBMid <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>. Si ya tiene una app BlueID, consiga un ID de cliente y un secreto de BlueID.


### Obtención de un ID de cliente y secreto de IBMid

Para obtener un ID de cliente y un secreto, siga estos pasos.

1. En <a href="https://w3.innovate.ibm.com/tools/sso/home.html" target="_blank">SSO Self-Service Provisioner <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>, inicie sesión en su cuenta de BlueID.
2. Registre una app BlueID. Asegúrese de seleccionar **preproducción** o **producción** para el proveedor de identidad.
3. En **Información de cliente**, indique el URL de redirección de ID de app. Puede obtener el URI de autorización de redirección de la pantalla de configuración de IBMid del panel de control de su servicio.
4. Asegúrese de que esté seleccionado **Código de autorización**.
5. Tome nota de su tipo de proveedor de identidad de cuenta, secreto e ID de cliente de BlueID. Pulse **Continuar y finalizar**.

### Configuración de ID de app para autenticación de IBMid

Una vez que tenga su ID de cliente y secreto de BlueID y que su app BlueID esté configurada con el URI de redirección correcto, podrá editar la sección de autenticación de BlueID del panel de control del servicio.

1. Desde el separador **Gestionar** del panel de control del servicio, seleccione **IBMid** y pulse **Editar**.
2. Indique el ID de cliente y secreto de BlueID.
3. Copie el URI que está en el campo **URI de redirección para IBMid for Developers** y péguelo en **URI de redirección**.
4. Seleccione **preproducción** o **producción** para el proveedor de identidad y pulse **Guardar**.
5. Opcional: para apps web, especifique el URI de redirección en el campo **URI de redirección de la aplicación web**. Este valor está determinado por el desarrollador y se utiliza para acceder al URI de redirección tras la autorización.
