---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-13"

keywords: authentication, authorization, identity, app security, secure, access, platform, management, permissions

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


# Gestión de acceso de servicio
{: #service-access-management}

Con {{site.data.keyword.appid_full}} y {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM), los propietarios de cuentas pueden gestionar el acceso de usuario en su cuenta.
{: shortdesc}

Como propietario de una cuenta, puede establecer políticas dentro de la cuenta para crear distintos niveles de acceso para distintos usuarios. Por ejemplo, algunos usuarios pueden tener acceso de **Solo lectura** a una instancia, pero acceso de **Escritura** a otra. Puede decidir quién tiene permiso para crear, actualizar y suprimir instancias de {{site.data.keyword.appid_short_notm}}.

Para obtener más información sobre IAM, consulte [Acceso de IAM](/docs/iam?topic=iam-userroles).

## Roles de usuario
{: #iam-roles}

El ámbito de una política de acceso se basa en el rol asignado de un usuario.
{: shortdesc}

Las políticas permiten otorgar acceso a distintos niveles. Algunas de las opciones incluyen:
<ul><ul>
  <li>Acceso a todas las instancias del servicio de su cuenta</li>
  <li>Acceso a instancias de un servicio individual de su cuenta</li>
  <li>Acceso a un recurso específico dentro de una instancia</li>
  <li>Acceso a todos los servicios habilitados para IAM de su cuenta</li>
</ul></ul>

### Roles de plataforma
{: #iam-platform-roles}

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

### Roles de acceso al servicio
{: #iam-service-roles}
La tabla siguiente detalla las acciones que se correlacionan con roles de acceso al servicio. Los roles de acceso al servicio permiten a los usuarios acceder a {{site.data.keyword.appid_short_notm}}, así como la posibilidad de llamar a la API de {{site.data.keyword.appid_short_notm}}.


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

Para obtener más información sobre la asignación de roles de usuario en la IU, consulte [Gestión del acceso IAM](/docs/iam?topic=iam-iammanidaccser#iammanidaccser).


## Políticas de acceso de {{site.data.keyword.appid_short_notm}}
{: #iam-access}

Todos los usuarios que accedan al servicio {{site.data.keyword.appid_short_notm}} en su cuenta deben tener asignada una política de acceso con un rol de usuario de IAM definido. Esa política determina qué acciones puede realizar el usuario dentro del contexto del servicio o de la instancia que seleccione.
{: shortdesc}

Las acciones son personalizadas y están definidas por el servicio de {{site.data.keyword.cloud_notm}} como operaciones permitidas para realizarse en el servicio. Las acciones se correlacionan entonces con los roles de usuario de IAM. Con el servicio {{site.data.keyword.cloudaccesstrailshort}}, se puede realizar un seguimiento de algunas de las acciones que se realizan. En la tabla siguiente, se correlacionan las acciones y los permisos necesarios para {{site.data.keyword.appid_short_notm}}.

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

</br>

## Ejemplo: dar acceso a otro usuario a una instancia de {{site.data.keyword.appid_short_notm}}
{: #iam-example}

En este caso de ejemplo, un administrador ha creado una instancia de {{site.data.keyword.appid_short_notm}} y necesita otorgar acceso de visor a otro miembro del equipo.
{: shortdesc}

Antes de empezar:
* Instale la [CLI de {{site.data.keyword.cloud_notm}}](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli).

Para actualizar los permisos de acceso, el administrador completa los pasos siguientes:

1. Inicie sesión en la consola de {{site.data.keyword.cloud_notm}}.

2. Proporcione al empleado acceso de visualización siguiendo los pasos que figuran en la [documentación de IAM](/docs/iam?topic=iam-iammanidaccser).

3. Vaya al separador **Credenciales de servicio** del panel de control de {{site.data.keyword.appid_short_notm}}. Pulse **Ver credenciales** y copie el **tentantID**.

4. Inicie sesión con la CLI de {{site.data.keyword.cloud_notm}} en el terminal.

    ```
    ibmcloud login -api -a https://api.<region>.cloud.ibm.com
    ```
    {: pre}

    <table>
      <tr>
        <th>Región</th>
        <th>Punto final</th>
      </tr>
      <tr>
        <td>Dallas</td>
        <td><code>us-south</code></td>
      </tr>
      <tr>
        <td>Frankfurt</td>
        <td><code>eu-de</code></td>
      </tr>
      <tr>
        <td>Sídney</td>
        <td><code>au-syd</code></td>
      </tr>
      <tr>
        <td>Londres</td>
        <td><code>eu-gb</code></td>
      </tr>
      <tr>
        <td>Tokio</td>
        <td><code>jp-tok</code></td>
      </tr>
    </table>

5. Obtenga una señal de IAM y tome nota de la misma.

    ```
    ibmcloud iam oauth-tokens
    ```
    {: pre}

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
    'https://us-south.appid.cloud.ibm.com/management/v4/<tenantID>/config/idps/facebook'
    ```
    {: pre}

    El resultado es un mensaje 403 unauthorized.

Para ver las configuraciones de {{site.data.keyword.appid_short_notm}} de la CLI, el miembro del equipo completa los pasos siguientes:

1. Utilizando la CLI de {{site.data.keyword.cloud_notm}} en el terminal, inicie la sesión.

    ```
    ibmcloud login -a api.<region>.console.cloud.ibm.com
    ```
    {: pre}

2. Obtenga una señal de IAM y tome nota de la misma.

    ```
    ibmcloud iam oauth-tokens
    ```
    {: pre}

3. Vea la configuración del proveedor de identidad para Facebook utilizando cURL.

    ```
    curl -X GET --header 'Accept: application/json' --header 'Authorization: <IAM token value>' \  'https://us-south.appid.cloud.ibm.com/management/v4/<tenantID>/config/idps/facebook'
    ```
    {: pre}

    El resultado es un mensaje 200 que contiene la información del proveedor de identidad.
