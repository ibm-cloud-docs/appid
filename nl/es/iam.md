---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

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

Las acciones son personalizadas y están definidas por el servicio de {{site.data.keyword.Bluemix_notm}} como operaciones permitidas para realizarse en el servicio. Las acciones se correlacionarán entonces con los roles de usuario de IAM. Para {{site.data.keyword.appid_short_notm}}, existen las acciones siguientes:

<table>
  <tr>
    <th>Mandato</th>
    <th>Explicación</th>
    <th>Rol</th>
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
</table>




## Ejemplo: dar acceso a otro usuario a una instancia de {{site.data.keyword.appid_short_notm}}
{: #example}

En este caso de ejemplo, un administrador ha creado una instancia de {{site.data.keyword.appid_short_notm}} y necesita otorgar acceso de visor a otro miembro del equipo.
{: shortdesc}

Antes de empezar:
* Instale la [CLI de {{site.data.keyword.Bluemix_notm}}](/docs/cli/reference/bluemix_cli/get_started.html).

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
    'https://appid-management.stage1.ng.bluemix.net/management/v4/<tenantId>/config/idps/facebook'
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
