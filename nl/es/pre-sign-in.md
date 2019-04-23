---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

keywords: authentication, authorization, identity, app security, secure, development, user information, attributes, profiles, 

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

# Adición de atributos antes del inicio de sesión del usuario
{: #preregister}

Con {{site.data.keyword.appid_full}} puede empezar a crear un perfil para los usuarios que sabe que van a necesitar acceso a la app antes del primer inicio de sesión.
{: shortdesc}

Para obtener más información sobre los tipos de atributos, consulte [Comprensión de los perfiles de usuario](/docs/services/appid?topic=appid-user-profile). Para obtener más información sobre los atributos personalizados y las consideraciones de seguridad, consulte [Atributos personalizados](/docs/services/appid?topic=appid-custom-attributes).
{: tip}

## Visión general del registro previo
{: #preregister-understand}

### ¿Por qué debería utilizar el registro previo?
{: #preregister-why}

Supongamos que tenemos una aplicación en la que utiliza {{site.data.keyword.appid_short_notm}} para federar usuarios existentes del proveedor de identidad de SAML. Es posible que desee que determinados usuarios tengan acceso de `admin` inmediatamente después de iniciar sesión por primera vez. Para que esto suceda, puede utilizar el punto final de registro previo para establecer un atributo `admin` personalizado para los usuarios y otorgarles acceso a la consola de administración sin ninguna acción adicional por su parte. Asegúrese de tener en cuenta los [problemas de seguridad](/docs/services/appid?topic=appid-custom-attributes#custom-attributes) que se pueden producir cambiando el valor predeterminado.

### ¿Cómo se identifican los usuarios?
{: #preregister-identify-user}

Puede identificar los usuarios utilizando lo siguiente:

* El ID exclusivo del usuario, denominado **GUID**, en el proveedor de identidad. Aunque este identificador siempre existe y es único, no siempre está disponible ni es fácil de comprender. Para la instancia, el directorio en la nube utiliza un GUID de 16 bytes.
* El **correo electrónico** del usuario, si está disponible.

### ¿Qué información proporcionan los proveedores de identidad?
{: #preregister-idp-provide}

Consulte la tabla siguiente para ver qué tipo de información de identidad puede utilizar.

<table>
  <thead>
    <tr>
      <th>Proveedor de identidad</th>
      <th>GUID</th>
      <th>Correo electrónico</th>
      <th>Sub</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Directorio en la nube</td>
      <td><img src="images/confirm.png" width="32" alt="Característica disponible" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="Característica disponible" style="width:32px;" /></td>
      <td> </td>
    </tr>
    <tr>
      <td>Facebook</td>
      <td><img src="images/confirm.png" width="32" alt="Característica disponible" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="Característica disponible" style="width:32px;" /></td>
      <td> </td>
    </tr>
    <tr>
      <td>Google</td>
      <td><img src="images/confirm.png" width="32" alt="Característica disponible" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="Característica disponible" style="width:32px;" /></td>
      <td> </td>
    </tr>
    <tr>
      <td>SAML</td>
      <td></td>
      <td><img src="images/confirm.png" width="32" alt="Característica disponible" style="width:32px;" /></td>
      <td> </td>
    </tr>
    <tr>
      <td>Personalizado</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Característica disponible" style="width:32px;" /></td>
    </tr>
  </tbody>
</table>

### ¿Cómo se maneja el directorio en la nube?
{: #preregister-cd}


Para garantizar la integridad de los atributos de usuario registrados previamente, el directorio en la nube solicita requisitos adicionales a los usuarios. El registro previo solo se puede producir cuando la validación de correo electrónico se ha habilitado y verificado. Si registra previamente un usuario del directorio en la nube con atributos específicos, dichos atributos estarán pensados para una persona en concreto. Si el correo electrónico no se verifica primero, es posible que otro usuario reclame la dirección de correo electrónico y los atributos asignados a la misma.

1. Establezca el directorio en la nube en el modo de contraseña y correo electrónico. Puede hacerlo mediante la IU, en los valores generales del separador **Directorio en la nube**. También puede establecerlo mediante las [API de gestión](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.createCloudDirectoryUser).

2. Verifique la dirección de correo electrónico de los usuarios para confirmar su identidad de una de las formas siguientes:

  * Para verificar la identidad de los usuarios por correo electrónico, establezca **Verificación de correo electrónico** en **Activado** en el separador **Directorio en la nube** del panel de control de servicio. Si añade un usuario y este inicia sesión en la app sin verificar primero el correo electrónico, el inicio de sesión se completa correctamente, pero el atributo predefinido se suprime.
  * Para verificar los usuarios de forma manual, debe ser administrador y utilizar las [API de gestión](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.createCloudDirectoryUser) del directorio en la nube. Al crear o actualizar un usuario, debe establecer explícitamente el campo `estado` en `CONFIRMADO` en la carga útil de datos del usuario.

**¿Es necesario realizar algo en concreto al utilizar el proveedor de identidad personalizado?**

Cuando añada información de usuario a la aplicación por adelantado, podrá utilizar cualquier identificador exclusivo proporcionado por el flujo de autenticación. El identificador debe coincidir _exactamente_ con el `sub` de la señal web de JSON firmada que se ha enviado durante la solicitud de autorización. Si el identificador no coincide, significa que el perfil que desea añadir no se ha enlazado correctamente.



## Adición de información de usuario a la app
{: #preregister-add-info}

Ahora que ha aprendido sobre el proceso y ha considerado las implicaciones de seguridad, intente añadir un usuario.

**Antes de empezar:**

Para añadir atributos personalizados para un usuario específico con el punto final de la API de gestión [/users](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Users/mgmt.users_search_user_profile), debe conocer la información siguiente:

* Qué proveedor de identidad va a utilizar el usuario para iniciar sesión.
* El identificador exclusivo del usuario que proporciona el proveedor de identidad.

Cuando un usuario inicia sesión en la app por primera vez, {{site.data.keyword.appid_short_notm}} busca al usuario. Si lo encuentra, el usuario hereda la identidad que le ha asignado. Si no encuentra al usuario, se crea uno nuevo en función de la información que proporciona el proveedor de identidad.

**Para añadir un usuario:**

1. Inicie sesión en IBM Cloud.
  ```
  ibmcloud login
  ```
  {: pre}

2. Busque la señal de IAM ejecutando el mandato siguiente.
  ```
  ibmcloud iam oauth-tokens
  ```
  {: pre}

3. Realice una solicitud POST en el punto final `/users` que contenga una descripción del usuario y los atributos que desea establecer como objeto JSON.

  Cabecera:
  ```
  POST {management-url}/management/v4/{tenantId}/users
       Host: <management-server-url>
       Authorization: 'Bearer <IAM_TOKEN>'
       Content-Type: application/json
  ```
  {: pre}

  Cuerpo:
  ```
   {
       "idp": "<Identity Provider>",
       "idp-identity": "<User's unique identifier>",
       "profile": {
           "attributes": {
             "mealPreference":"vegeterian"
           }
       }
   }
  ```
  {: pre}

  <table>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="Icono de idea"/> Comprensión de los componentes</th>
    </thead>
    <tbody>
      <tr>
        <td><code><em>idp</em></code></td>
        <td>El proveedor de identidad con el que se autenticará el usuario. Entre las opciones se incluyen: `saml`, `cloud_directory`, `facebook`, `google`, `appid_custom`, `ibmid`.</td>
      </tr>
      <tr>
        <td><code><em>idp-identity</em></code></td>
        <td>El identificador único proporcionado por el proveedor de identidad.</td>
      </tr>
      <tr>
        <td><code><em>profile</em></code></td>
        <td>El perfil del usuario que contiene la correlación JSON del atributo personalizado.</td>
      </tr>
    </tbody>
  </table>

  Solicitud de ejemplo:
  ```
  $ curl --request POST \
       --url 'https://{Management_URI}/users \
       --header 'Authorization: Bearer {IAM_TOKEN}' \
       --header 'Content-Type: application/json' \
       --data '{"idp": "saml", "idp-identity": "user@ibm.com", "profile": { "attributes": { "role": "admin",
       "frequent_flyer_points": 1000 }}}'
  ```
  {: screen}

3. Verifique que el registro se ha realizado correctamente de una de las maneras siguientes:
  * Compruebe el ID de usuario en la respuesta.
    ```
    {
        "id": "<{{site.data.keyword.appid_short_notm}} User Id>"
    }
    ```
    {: screen}
  * Compruebe el perfil de usuario que se ha creado.

Tenga en cuenta que los atributos predefinidos del usuario están vacíos hasta que se lleva a cabo la primera autenticación, pero el usuario es, a todos los efectos, un usuario autenticado. Puede utilizar el ID exclusivo tal y como lo haría con alguien que ya ha iniciado sesión. Por ejemplo, puede modificar, buscar o suprimir el perfil.

Ahora que ha asociado un usuario con atributos específicos, intente [acceder o actualizar atributos](/docs/services/appid?topic=appid-custom-attributes).


</br>
