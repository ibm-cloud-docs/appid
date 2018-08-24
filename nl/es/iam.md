---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# Gestión de acceso de servicio
{: #service-access-management}

Con {{site.data.keyword.appid_full}} y {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM), los propietarios de cuentas pueden gestionar el acceso de usuario en su cuenta.
{: shortdesc}

Como propietario de una cuenta, puede establecer políticas dentro de la cuenta para crear distintos niveles de acceso para distintos usuarios. Por ejemplo, algunos usuarios pueden tener acceso de **Solo lectura** a una instancia, pero acceso de **Escritura** a otra. Puede decidir quién tiene permiso para crear, actualizar y suprimir instancias de {{site.data.keyword.appid_short_notm}}.

Para obtener más información sobre IAM, consulte [Acceso de IAM](/docs/iam/users_roles.html).

## Roles de usuario
{: #roles}

El ámbito de una política de acceso se basa en el rol asignado de un usuario.
{: shortdesc}

Las políticas permiten que se otorgue acceso en distintos niveles. Algunas de las opciones incluyen:
<ul><ul>
  <li>Acceso a todas las instancias del servicio de su cuenta</li>
  <li>Acceso a instancias de un servicio individual de su cuenta</li>
  <li>Acceso a un recurso específico dentro de una instancia</li>
  <li>Acceso a todos los servicios habilitados para IAM de su cuenta</li>
</ul></ul>

Los roles de gestión de plataformas permiten a los usuarios realizar tareas en recursos de servicio en el nivel de plataforma. Por ejemplo, los roles pueden asignarse para determinar quién puede crear o suprimir ID, crear instancias y enlazar instancias a apps. La tabla siguiente detalla las acciones a medida que se correlacionan con los roles de gestión de plataformas.

<table>
  <tr>
    <th>Rol de plataforma</th>
    <th>Permisos</th>
    <th>Acciones de ejemplo</th>
  </tr>
  <tr>
    <td><i>Visor</i></td>
    <td>Ver instancias de {{site.data.keyword.appid_short_notm}}.</td>
    <td>Puede ver los datos de usuario de un Directorio de nube o la configuración de proveedor de identidad.</td>
  </tr>
  <tr>
    <td><i>Editor</i></td>
    <td>Ver y enlazar instancias de {{site.data.keyword.appid_short_notm}}.</td>
    <td>Puede enlazar aplicaciones a una instancia de {{site.data.keyword.appid_short_notm}}.</td>
  </tr>
  <tr>
    <td><i>Operador</i></td>
    <td>Crear, suprimir, editar, suspender, reanudar, ver o enlazar instancias de {{site.data.keyword.appid_short_notm}}.</td>
    <td>Puede crear o suprimir una instancia de {{site.data.keyword.appid_short_notm}} desde el catálogo.</td>
  </tr>
  <tr>
    <td><i>Administrador</i></td>
    <td>Todas las acciones de gestión para todos los servicios de la cuenta.</td>
    <td>Puede realizar todas las acciones del operador y la capacidad de asignar políticas a otros usuarios.</td>
  </tr>
</table>

</br>
</br>
La tabla siguiente detalla las acciones que se correlacionan con roles de acceso de servicio. Los roles de acceso de servicio permiten a los usuarios acceder a {{site.data.keyword.appid_short_notm}}, así como la posibilidad de llamar a la API de {{site.data.keyword.appid_short_notm}}.


<table>
  <tr>
    <th>Rol de servicio</th>
    <th>Permisos</th>
    <th>Acciones de ejemplo</th>
  </tr>
  <tr>
    <td><i>Lector</i></td>
    <td>Ver datos de instancia de {{site.data.keyword.appid_short_notm}}.</td>
    <td>Puede ver los detalles de la instancia de servicio como los datos de usuario o la información del proveedor de identidad.</td>
  </tr>
  <tr>
    <td> <i>Escritor o Gestor</i></td>
    <td>Ver y cambiar una instancia de {{site.data.keyword.appid_short_notm}}.</td>
    <td>Puede realizar todas las acciones del Lector y editar la instancia de servicio, como por ejemplo editar la configuración del proveedor de identidad. </li></ul></td>
  </tr>
</table>

Para obtener más información sobre la asignación de roles de usuario en la IU, consulte [Gestión del acceso IAM](/docs/iam/mngiam.html#iammanidaccser).


## Políticas de acceso de {{site.data.keyword.appid_short_notm}}
{: #access}

Cada usuario que acceda al servicio de {{site.data.keyword.appid_short_notm}} en su cuenta debe tener asignada una política de acceso con un rol de usuario de IAM definido. Esa política determina qué acciones puede realizar el usuario dentro del contexto del servicio o de la instancia que seleccione.
{: shortdesc}

Las acciones son personalizadas y están definidas por el servicio de {{site.data.keyword.Bluemix_notm}} como operaciones permitidas para realizarse en el servicio. Las acciones se correlacionarán entonces con los roles de usuario de IAM. Con el servicio {{site.data.keyword.cloudaccesstrailshort}}, se puede realizar un seguimiento de algunas de las acciones que se realizan. En la tabla siguiente, se correlacionan las acciones y los permisos necesarios para {{site.data.keyword.appid_short_notm}}.

<table>
  <tr>
    <th>Acción</th>
    <th>Explicación</th>
    <th>Rol necesario</th>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-redirect-uris</code></td>
    <td>Ver los URL de redirección posteriores a la autenticación.</td>
    <td>Lector, Escritor, Gestor</td>
  </tr>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-redirect-uris</code></td>
    <td>Añadir o actualizar URL de redirección posteriores a la autenticación.</td>
    <td>Lector, Gestor</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-idps</code></td>
    <td>Actualizar la configuración del proveedor de identidad.</td>
    <td>Lector, Gestor</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-idps</code></td>
    <td>Ver la configuración del proveedor de identidad.</td>
    <td>Lector, Escritor, Gestor</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-recent-activities</code></td>
    <td>Ver cualquier suceso reciente de autenticación como una lista.</td>
    <td>Lector, Escritor, Gestor</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-ui-config</code></td>
    <td>Ver la configuración de widgets de inicio de sesión, como el logotipo y los colores.</td>
    <td>Lector, Escritor, Gestor</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-ui-config</code></td>
    <td>Actualizar la configuración de widgets de inicio de sesión.</td>
    <td>Lector, Gestor</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-user-profile-config</code></td>
    <td>Ver la configuración del perfil de usuario.</td>
    <td>Lector, Escritor, Gestor</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-user-profile-config</code></td>
    <td>Cambiar la configuración del perfil de usuario.</td>
    <td>Lector, Gestor</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-cd-users</code></td>
    <td>Ver la configuración del perfil de usuario.</td>
    <td>Lector, Escritor, Gestor</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-add-cd-user</code></td>
    <td>Añadir nuevos usuarios al directorio en la nube.</td>
    <td>Lector, Gestor</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-cd-user</code></td>
    <td>Actualizar los detalles de usuario de un directorio en la nube.</td>
    <td>Lector, Gestor</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-delete-cd-user</code></td>
    <td>Suprimir un usuario del directorio en la nube.</td>
    <td>Lector, Gestor</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-email-template</code></td>
    <td>Ver las plantillas de correo electrónico del directorio en la nube.</td>
    <td>Lector, Escritor, Gestor</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-update-email-template</code></td>
    <td>Actualizar la plantilla de correo electrónico con su propio contenido.</td>
    <td>Lector, Gestor</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-delete-email-template</code></td>
    <td>Suprimir una plantilla de correo electrónico del directorio en la nube.</td>
    <td>Lector, Gestor</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-saml-metadata</code></td>
    <td>Ver los metadatos del proveedor de servicios (SP) SAML del Directorio en la nube.</td>
    <td>Lector, Escritor, Gestor</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-post-saml-logo</code></td>
    <td>Establecer o actualizar la imagen en el widget de inicio de sesión del proveedor de identidad SAML.</td>
    <td>Lector, Gestor</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-send-email-cd</code></td>
    <td>Enviar un correo electrónico a un usuario basándose en una plantilla.</td>
    <td>Lector, Gestor</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-sender-details-cd</code></td>
    <td>Ver los detalles del remitente para el correo electrónico.</td>
    <td>Lector, Escritor, Gestor</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-sender-details-cd</code></td>
    <td>Actualizar los detalles del remitente.</td>
    <td>Lector, Gestor</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-revoke-refresh-token</code></td>
    <td>Revocar la señal para renovación de un usuario con su ID de usuario.</td>
    <td>Lector, Gestor</td>
  </tr>
</table>

## Seguimiento de cambios en las instancias de {{site.data.keyword.appid_short_notm}}
{: #tracking}

Puede ver, gestionar y auditar la actividad de configuración que se realiza en la instancia de {{site.data.keyword.appid_short_notm}} mediante el servicio de {{site.data.keyword.cloudaccesstrailshort}}.
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
    <td>Ver la imagen que se visualiza en el widget de inicio de sesión.</td>
    <td>Se puede encontrar en el separador <strong>Personalización de inicio de sesión</strong>.</td>
  </tr>
  <tr>
    <td><code>update.media</code></td>
    <td>Actualizar la imagen que se visualiza en el widget de inicio de sesión.</td>
    <td>Se puede actualizar en el separador <strong>Personalización de inicio de sesión</strong>.</td>
  </tr>
  <tr>
    <td><code>read.uiConfiguration</code></td>
    <td>Ver la configuración de la IU del widget de inicio de sesión, incluida la imagen y el color de la cabecera.</td>
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


Para obtener más información sobre cómo funciona el servicio, consulte la [documentación de {{site.data.keyword.cloudaccesstrailshort}}](/docs/services/cloud-activity-tracker/index.html).

</br>
</br>

## Ejemplo: dar acceso a otro usuario a una instancia de {{site.data.keyword.appid_short_notm}}
{: #example}

En este caso de ejemplo, un administrador ha creado una instancia de {{site.data.keyword.appid_short_notm}} y necesita otorgar acceso de visor a otro miembro del equipo.
{: shortdesc}

Antes de empezar:
* Instale la [CLI de {{site.data.keyword.Bluemix_notm}}](/docs/cli/index.html).

Para actualizar los permisos de acceso, el administrador completa los pasos siguientes:

1. Inicie sesión en la consola de {{site.data.keyword.Bluemix_notm}}.
2. Proporcione al empleado acceso de visualización siguiendo los pasos que figuran en la [documentación de IAM](/docs/iam/iamusermanage.html#iamusermanage).
3. Vaya al separador **Credenciales de servicio** del panel de control de {{site.data.keyword.appid_short_notm}}. Pulse **Ver credenciales** y copie el **tentantID**.
4. Inicie sesión con la CLI de {{site.data.keyword.Bluemix_notm}} en el terminal.
    ```
    bx login -a api.<region>.bluemix.net
    ```
    {: codeblock}
5. Obtenga una señal de IAM y tome nota de la misma.
    ```
    bx iam oauth-tokens
    ```
    {: codeblock}
6. Verifique que el miembro del equipo no pueda realizar cambios.
    ```
    curl -X PUT --header 'Content-Type: application/json' \
    --header 'Accept: application/json' \
    --header 'Authorization: <IAM token value>' \
    -d '{
     "isActive": false,
     "config": {
       "idpId": "appID",
       "secret": "appsecret"
     }
    }' \
    'https://appid-management.ng.bluemix.net/management/v4/<tenantId>/config/idps/facebook'
    ```
    {: codeblock}

    El resultado es un mensaje 403 unauthorized.

Para ver las configuraciones de {{site.data.keyword.appid_short_notm}} de la CLI, el miembro del equipo completa los pasos siguientes:

1. Utilizando la CLI de {{site.data.keyword.Bluemix_notm}} en el terminal, inicie la sesión.
    ```
    bx login -a api.<region>.bluemix.net
    ```
    {: codeblock}
2. Obtenga una señal de IAM y tome nota de la misma.
    ```
    bx iam oauth-tokens
    ```
    {: codeblock}
3. Vea la configuración del proveedor de identidad para Facebook utilizando cURL.
    ```
    curl -X GET --header 'Accept: application/json' --header 'Authorization: <IAM token value>' \  'https://appid-management.ng.bluemix.net/management/v4/<tenantId>/config/idps/facebook'
    ```
    {: codeblock}
    El resultado es un mensaje 200 que contiene la información del proveedor de identidad.
