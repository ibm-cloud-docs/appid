---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-18"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}
{:note: .note}
{:important: .important}


# Sucesos de {{site.data.keyword.cloudaccesstrailshort}}
{: #at_events}

Puede ver, gestionar y analizar actividades iniciadas por el usuario realizadas en la instancia de servicio de {{site.data.keyword.appid_full}} utilizando el servicio de {{site.data.keyword.cloudaccesstrailshort}}.
{: shortdesc}



Para obtener más información sobre cómo funciona el servicio, consulte la [documentación de {{site.data.keyword.cloudaccesstrailshort}}](/docs/services/cloud-activity-tracker/index.html).


</br>

## Visualización de sucesos de administración
{: #monitor-admin}

Puede ver, gestionar y analizar la actividad de configuración que se realiza en la instancia de {{site.data.keyword.appid_short_notm}} mediante el servicio de {{site.data.keyword.cloudaccesstrailshort}}.
{: shortdesc}

Para supervisar la actividad administrativa:

1. Inicie sesión en su cuenta de {{site.data.keyword.Bluemix_notm}}.
2. Desde el catálogo, suministre una instancia del servicio de {{site.data.keyword.cloudaccesstrailshort}} en la misma cuenta que la instancia de {{site.data.keyword.appid_short_notm}}.
3. En el panel de control de {{site.data.keyword.cloudaccesstrailshort}}, pulse el separador **Gestionar**.
4. En la lista desplegable, seleccione las configuraciones siguientes para buscar los sucesos generados por {{site.data.keyword.appid_short_notm}}.
    * Para **Ver registros**, seleccione **Registros de cuenta**.
    * Para **Buscar**, seleccione **target.Management**.
    * Para **Filtro**, escriba **appid**.
5. Pulse **Filtrar**.

</br>

## Lista de sucesos de administración
{: #events-admin}

Consulte la tabla siguiente para obtener una lista de los sucesos que se envían a {{site.data.keyword.cloudaccesstrailshort}}.

<table>
  <tr>
    <th>Acción</th>
    <th>Descripción</th>
    <th>Ubicación de IU</th>
  </tr>
  <tr>
    <td><code>read.recentActivity</code></td>
    <td>Ver actividad reciente.</td>
    <td>Se puede encontrar en el recuadro <strong>Registro de actividad</strong> en el separador <strong>Visión general</strong>.</td>
  </tr>
  <tr>
    <td><code>read.idpConfig</code></td>
    <td>Ver la configuración del proveedor de identidad.</td>
    <td>Se puede encontrar en el separador <strong>Proveedores de identidad > Gestionar</strong>.</td>
  </tr>
  <tr>
    <td><code>update.idpConfig</code></td>
    <td>Actualizar la configuración del proveedor de identidad.</td>
    <td>Se puede actualizar en el separador <strong>Proveedores de identidad > Gestionar</strong>.</td>
  </tr>
  <tr>
    <td><code>read.tokensConfig</code></td>
    <td>Ver la configuración de caducidad de la señal.</td>
    <td>Se puede encontrar en el separador <strong>Proveedores de identidad > Caducidad de la señal</strong>.</td>
  </tr>
  <tr>
    <td><code>read.isProfilesActive</code></td>
    <td>Ver la configuración de almacenamiento del perfil de usuario.</td>
    <td>Se puede encontrar en <strong>Registro de actividad</strong> en el separador <strong>Visión general</strong>.</td>
  </tr>
  <tr>
    <td><code>update.isProfilesActive</code></td>
    <td>Actualizar la configuración de almacenamiento del perfil de usuario.</td>
    <td>Se puede encontrar en el separador <strong>Perfiles</strong>.</td>
  </tr>
  <tr>
    <td><code>read.themeColor</code></td>
    <td>Ver el color del tema de la cabecera del widget de inicio de sesión.</td>
    <td>Se puede encontrar en el separador <strong>Personalización de inicio de sesión</strong>.</td>
  </tr>
  <tr>
    <td><code>update.themeColor</code></td>
    <td>Actualizar el color del tema de la cabecera del widget de inicio de sesión.</td>
    <td>Se puede actualizar en el separador <strong>Personalización de inicio de sesión</strong>.</td>
  </tr>
  <tr>
    <td><code>read.media</code></td>
    <td>Ver la imagen que se muestra en el widget de inicio de sesión.</td>
    <td>Se puede encontrar en el separador <strong>Personalización de inicio de sesión</strong>.</td>
  </tr>
  <tr>
    <td><code>update.media</code></td>
    <td>Actualizar la imagen que se muestra en el widget de inicio de sesión.</td>
    <td>Se puede actualizar en el separador <strong>Personalización de inicio de sesión</strong>.</td>
  </tr>
  <tr>
    <td><code>read.uiConfiguration</code></td>
    <td>Ver la configuración de la IU del widget de inicio de sesión que incluye la imagen y el color de la cabecera.</td>
    <td>Se puede encontrar en el separador <strong>Personalización de inicio de sesión</strong>.</td>
  </tr>
  <tr>
    <td><code>read.uiLanguages</code></td>
    <td>Ver una lista de idiomas soportados.</td>
    <td>Se debe ver desde la API.</td>
  </tr>
  <tr>
    <td><code>update.uiLanguages</code></td>
    <td>Actualizar los idiomas soportados.</td>
    <td>Se debe actualizar a través de la API.</td>
  </tr>
  <tr>
    <td><code>read.samlMetadata</code></td>
    <td>Ver los metadatos SAML de App ID.</td>
    <td>Se puede encontrar en el separador <strong>Proveedores de identidad > Federación de SAML 2.0</strong>.</td>
  </tr>
  <tr>
    <td><code>read.cloudDirectoryUser</code></td>
    <td>Ver un usuario del Directorio en la nube.</td>
    <td>Se puede encontrar en el separador <strong>Usuarios</strong>.</td>
  </tr>
  <tr>
    <td><code>update.cloudDirectoryUser</code></td>
    <td>Actualizar un usuario del Directorio en la nube.</td>
    <td>Se puede actualizar en el separador <strong>Usuarios</strong>.</td>
  </tr>
  <tr>
    <td><code>delete.cloudDirectoryUser</code></td>
    <td>Suprimir un usuario del Directorio en la nube.</td>
    <td>Se puede suprimir en el separador <strong>Usuarios</strong>.</td>
  </tr>
  <tr>
    <td><code>read.cloudDirectoryUsers</code></td>
    <td>Ver una lista de los usuarios del Directorio en la nube.</td>
    <td>Se puede encontrar en el separador <strong>Usuarios</strong>.</td>
  </tr>
  <tr>
    <td><code>update.cloudDirectoryUsers</code></td>
    <td>Actualizar la lista de usuarios del Directorio en la nube.</td>
    <td>Se puede actualizar en el separador <strong>Usuarios</strong>.</td>
  </tr>
  <tr>
    <td><code>delete.cloudDirectoryUsers</code></td>
    <td>Suprimir una lista de usuarios del Directorio en la nube.</td>
    <td>Se puede suprimir en el separador <strong>Usuarios</strong>.</td>
  </tr>
  <tr>
    <td><code>read.emailTemplate</code></td>
    <td>Ver una plantilla de correo electrónico.</td>
    <td>Se puede encontrar en el separador <strong>Proveedores de identidad > Directorio en la nube > Plantillas</strong>.</td>
  </tr>
  <tr>
    <td><code>update.emailTemplate</code></td>
    <td>Actualizar una plantilla de correo electrónico.</td>
    <td>Se puede encontrar en el separador <strong>Proveedores de identidad > Directorio en la nube > Plantillas</strong>.</td>
  </tr>
  <tr>
    <td><code>delete.emailTemplate</code></td>
    <td>Suprimir una plantilla de correo electrónico para restablecer el valor predeterminado.</td>
    <td>Se puede encontrar en el separador <strong>Proveedores de identidad > Directorio en la nube > Plantillas</strong>.</td>
  </tr>
  <tr>
    <td><code>read.senderDetails</code></td>
    <td>Ver los detalles del remitente.</td>
    <td>Se puede encontrar en el separador <strong>Proveedores de identidad > Directorio en la nube > Valores</strong>.</td>
  </tr>
  <tr>
    <td><code>update.senderDetails</code></td>
    <td>Actualizar los detalles del remitente</td>
    <td>Se puede encontrar en el separador <strong>Proveedores de identidad > Directorio en la nube > Valores</strong>.</td>
  </tr>
  <tr>
    <td><code>update.resendNotification</code></td>
    <td>Reenviar notificaciones de usuario.</td>
    <td>Se puede encontrar en el separador <strong>Proveedores de identidad > Directorio en la nube > Valores</strong>.</td>
  </tr>
  <tr>
    <td><code>update.selfForgotPassword</code></td>
    <td>Actualizar el proceso de contraseña olvidada.</td>
    <td>Se puede encontrar en el separador <strong>Proveedores de identidad > Directorio en la nube > Valores</strong>.</td>
  </tr>
  <tr>
    <td><code>update.forgotPasswordResult</code></td>
    <td>Ver el resultado de la confirmación de contraseña olvidada.</td>
    <td>Debe realizarse a través de la API.</td>
  </tr>
  <tr>
    <td><code>update.selfSignUp</code></td>
    <td>Actualizar el proceso de registro.</td>
    <td>Se puede encontrar en el separador <strong>Proveedores de identidad > Directorio en la nube > Valores</strong>.</td>
  </tr>
  <tr>
    <td><code>update.signUpResult</code></td>
    <td>Ver la confirmación del resultado del registro.</td>
    <td>Debe realizarse a través de la API.</td>
  </tr>
  <tr>
    <td><code>read.action_url</code></td>
    <td>Ver el URL personalizado al que se llama cuando se realiza una acción.</td>
    <td>Se puede encontrar en el separador <strong>Proveedores de identidad > Directorio en la nube > Páginas de destino personalizadas</strong>.</td>
  </tr>
  <tr>
    <td><code>update.action_url</code></td>
    <td>Actualizar el URL personalizado al que se llama cuando se realiza una acción.</td>
    <td>Se puede encontrar en el separador <strong>Proveedores de identidad > Directorio en la nube > Valores</strong>.</td>
  </tr>
  <tr>
    <td><code>update.changePassword</code></td>
    <td>Cambiar la contraseña de usuario del Directorio en la nube.</td>
    <td>Se puede encontrar en el separador <strong>Proveedores de identidad > Directorio en la nube > Valores</strong>.</td>
  </tr>
  <tr>
    <td><code>read.loginWidgetConfig</code></td>
    <td>Ver la configuración del widget de inicio de sesión.</td>
    <td>Se puede encontrar en el separador <strong>Personalización de inicio de sesión</strong>.</td>
  </tr>
  <tr>
    <td><code>update.loginWidgetConfig</code></td>
    <td>Actualizar la configuración del widget de inicio de sesión.</td>
    <td>Se puede actualizar en el separador <strong>Personalización de inicio de sesión</strong>.</td>
  </tr>
</table>

</br>
</br>


