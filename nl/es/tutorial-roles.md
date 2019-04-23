---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-08"

keywords: authentication, authorization, identity, app security, secure, access management, roles, attributes, users

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


# Guía de aprendizaje: Establecimiento de roles de usuario
{: #tutorial-roles}

Garantizar que las personas adecuadas, tengan el acceso correcto, en el momento preciso puede ser difícil cuando codifica la aplicación. Para facilitar este proceso, puede utilizar {{site.data.keyword.appid_full}} para definir un atributo personalizado como, por ejemplo, `role`, que le permite asignar distintos tipos de usuarios. A continuación, puede utilizar la aplicación para imponer distintos niveles de permisos para cada tipo de usuario. Con esta guía paso a paso aprenderá a establecer atributos de usuario, actualizarlos e inyectarlos en una señal utilizando las API de {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

¿Nuevo en las API? Pruébelas con esta [recopilación de Postman](https://github.com/ibm-cloud-security/appid-postman).
{: tip}

## Caso de ejemplo
{: #roles-scenario}

Trabaja como desarrollador en un parque temático de ficción. Se le asigna la tarea de gestionar el acceso para la [aplicación web](/docs/services/appid?topic=appid-web-apps), y cree que la forma más sencilla será establecer roles para cada tipo de usuario. Tiene varios tipos distintos de roles, como personal de parque y visitantes, que necesitan distintos niveles de permisos. Quiere ser capaz de agilizar el proceso y asegurarse de que a los usuarios se les asigna el rol correcto desde la primera vez que se registran en la aplicación.  
{: shortdesc}

No hay ningún problema. Puede utilizar la [característica de atributos personalizados](/docs/services/appid?topic=appid-custom-attributes) de {{site.data.keyword.appid_short_notm}} para almacenar cualquier tipo de información relacionada con el usuario. Por lo tanto, dado que está trabajando con el control de acceso basado en roles, puede crear un atributo denominado `role` y asignar valores diferentes para especificar un tipo de rol. Por ejemplo, el parque temático podría tener `visitors` (visitantes) o `staff` (personal), que cada uno podría ser un valor diferente para el atributo `role`. A continuación, puede asegurarse de que el código de la aplicación aplica las políticas de acceso y los privilegios que ha asignado.

Aunque esta guía de aprendizaje está escrita específicamente para apps web y el directorio en la nube, los atributos se pueden utilizar en un sentido mucho más amplio. Los atributos personalizados pueden ser cualquier cosa que quiera que sean. Mientras no se pase de los 100.000 atributos y tengan el formato de un objeto JSON simples, puede almacenar toda clase de información.
{: note}


## Antes de empezar
{: #roles-before}

¿Está preparado? ¡Empecemos!

Asegúrese de que tiene los requisitos previos siguientes antes de empezar:
- Una instancia del servicio de {{site.data.keyword.appid_short_notm}}
- Un conjunto de credenciales de servicio
- Una dirección de correo electrónico a la que puede acceder y validar


## Paso 1: Configurar la instancia de {{site.data.keyword.appid_short_notm}}
{: #roles-configure-app}

Antes de empezar a añadir atributos para los usuarios de Cloud Land, tiene que configurar la instancia de {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

1. En el separador **Proveedores de identidad** del panel de control del servicio, habilite **Directorio en la nube**. Aunque esta guía de aprendizaje utiliza el [Directorio en la nube](/docs/services/appid?topic=appid-cloud-directory), podría utilizar cualquier IdP, como [SAML](/docs/services/appid?topic=appid-enterprise), [Facebook](/docs/services/appid?topic=appid-social#facebook), [Google](/docs/services/appid?topic=appid-social#google) o un [proveedor personalizado](/docs/services/appid?topic=appid-custom-identity).

2. En el separador **Directorio en la nube > Verificación de correo electrónico**, habilite la verificación y establezca **Permitir que los usuarios inicien sesión en la app sin verificar primero su dirección de correo electrónico** en **No**. Cuando utilice atributos personalizados para establecer roles relacionados con los permisos, asegúrese de que los usuarios deban validar su identidad antes de que asuman los atributos que establezca.

3. En el separador **Perfiles**, establezca **Cambiar los atributos personalizados de la app** en **Inhabilitado**.

  De forma predeterminada, cualquier persona con una señal de acceso puede cambiar los atributos personalizados. Para garantizar la seguridad de la aplicación, debe configurar {{site.data.keyword.appid_short_notm}} de modo que solo el administrador o el propietario de la app puedan modificar los atributos personalizados. Esto evita que los usuarios cambien sus propios atributos personalizados y se otorguen permisos que no deberían tener.
  {: important}

¡Excelente! El panel de control está configurado y está listo para empezar a establecer roles.


## Paso 2: Definir roles en nombre de otro usuario antes de iniciar la sesión
{: #roles-set-before}

Cloud Land tiene un nuevo miembro de personal. Usted conoce toda su información, pero no empieza hasta dentro de unos días. Puede [registrarlo previamente](/docs/services/appid?topic=appid-preregister) creando un usuario y perfil de {{site.data.keyword.appid_short_notm}} que contenga atributos como el rol `staff`.
{: shortdesc}

Este proceso no completa el registro del directorio en la nube. El usuario todavía deberá registrarse en la app para heredar el atributo en el perfil que ha creado.
{: tip}

1. Inicie sesión en {{site.data.keyword.cloud_notm}} utilizando la CLI.

  ```
  ibmcloud login
  ```
  {: pre}

2. Obtenga una señal de acceso de IAM.

  ```
  ibmcloud iam oauth-tokens
  ```
  {: pre}

3. Realice una solicitud POST para crear un perfil de usuario para el nuevo usuario que contenga el atributo `staff`. Asegúrese de que puede acceder y validar el correo electrónico que utiliza.

  ```
  curl --request POST \
  https://us-south.appid.cloud.ibm.com/management/v4/{{APPID_TENANT_ID}}/users \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  - d '{
    "idp": "cloud_directory",
    "idp-identity": “user@email.com“,
    "profile": {
      "attributes": {
        “role”: “staff”
      }
    }
  }'
  ```
  {: pre}

  Salida de respuesta correcta:

  ```
  {
      "id": "5ty78b09-1356-4py8-l45p-808l633101zz"
  }
  ```
  {: screen}

6. Valide que el perfil se ha creado con el rol `staff`.

  ```
  curl --request GET \
  https://us-south.appid.cloud.ibm.com/management/v4/<tenant-ID>/users?email=<user-email> \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  ```
  {: pre}

  Cuerpo de respuesta correcto:

  ```
  {
      "users": [
          {
              "idp": "nominated_cloud_directory",
              "id": "5ty78b09-1356-4py8-l45p-808l633101zz"
          }
      ]
  }
  ```
  {: screen}

¡Buen trabajo! Ha realizado el registro previo de un usuario para la aplicación. Ahora, cuando dicho usuario inicie sesión en la app con el identificador que le ha asignado en el registro previo, se crea un usuario del directorio en la nube y hereda el perfil de usuario de {{site.data.keyword.appid_short_notm}}. A continuación, aprenda a actualizar los atributos.


## Paso 3: Actualizar los atributos de usuario
{: #roles-update-attributes}

Cloud Land está creciendo. Para dar soporte a este crecimiento, su compañía está contratando más personal. El usuario `staff` del paso dos ahora es gestor. Puede actualizar su perfil [asignando un nuevo rol](/docs/services/appid?topic=appid-custom-attributes).
{: shortdesc}

1. Actualice el perfil.

  ```
  curl --request PUT \
  https://us-south.appid.cloud.ibm.com/management/v4/<tenant-id>/users/<user-id>/profile \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  - d '{
    "profile": {
      "attributes": {
        “role”: “manager”
      }
    }
  }'
  ```
  {: pre}

3. Compruebe el perfil para verificar que se ha actualizado correctamente.

  ```
  curl --request POST \
  GET https://us-south.appid.cloud.ibm.com/management/v4/{{APPID_TENANT_ID}}/users/{{user_profile_id}}/profile \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  ```
  {: pre}

  Salida de respuesta correcta:

  ```
  {
      "id": "5ce78e09-1356-4ef8-a45d-808b633101db",
      "identities": [],
      "attributes": {
          "role": "manager"
      }
  }
  ```
  {: screen}

¡Buen trabajo!


## Paso 4: Inyectar atributos a las señales
{: #roles-map-claims}

El parque temático es cada día más popular, y su crecimiento es imparable. Con tantos nuevos visitantes y persona, ahora quiere limitar el número de solicitudes que se realizan. Para mejorar el rendimiento, puede correlacionar los atributos de perfil de usuario con las reclamaciones de señal de acceso e identidad. Al correlacionar reclamaciones personalizadas, es capaz de almacenar los atributos personalizados en las propias señales.
{: shortdesc}

La [configuración de señales](/docs/services/appid?topic=appid-customizing-tokens#customizing-tokens) es global, lo que significa que se aplica a todos los usuarios con un atributo `role`, independientemente del rol real que se les asigna.
{: tip}


1. Realice una solicitud al punto final de configuración de la señal.

  ```
  curl --request PUT \
  https://us-south.appid.cloud.ibm.com/management/v4/{{APPID_TENANT_ID}}/config/tokens \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  - d '{
      "access": {
          "expires_in": 3601
      },
      "refresh": {
          "enabled": false,
          "expires_in": 2592001
      },
      "anonymousAccess": {
          "expires_in": 2592001
      },
      "accessTokenClaims": [
      {
      "source": "attributes",
      "sourceClaim": "role"
      }
      ]
  }'
  ```
  {: pre}

  <table>
    <tr>
      <th>Variable</th>
      <th>Descripción</th>
    </tr>
    <tr>
      <td><code>tenant-id</code></td>
      <td>Un ID de arrendatario es la forma en la que se identifica la instancia de {{site.data.keyword.appid_short_notm}} en la solicitud. Puede encontrar el ID en el separador <em>Credenciales de servicio</em> del panel de control. Si no dispone de un conjunto de credenciales, puede seguir los pasos de la GUI para crear credenciales.</td>
    </tr>
    <tr>
      <td><code>source</code></td>
      <td>Tanto para <code>accessTokenClaim</code> como para <code>idTokenClaims</code>, establezca el origen en <code>attribute</code>.</td>
    </tr>
    <tr>
      <td><code>sourceClaim</code></td>
      <td>Tanto para <code>accessTokenClaim</code> como para <code>idTokenClaims</code>, establezca la reclamación origen en <code>role</code>.</td>
    </tr>
    <tr>
      <td><code>expires_in</code></td>
      <td>Este valor se aplica a cada tipo de señal y debe establecerse en cada solicitud. Si ha establecido previamente el valor en la GUI y, a continuación, ejecuta esta solicitud, los valores de la solicitud sustituyen a los valores establecidos previamente. Asegúrese de establecer la caducidad en el valor correcto para la configuración.</td>
    </tr>
  </table>

  Salida de respuesta correcta:

  ```
  {
      "access": {
          "expires_in": 3601
      },
      "refresh": {
          "enabled": false,
          "expires_in": 2592001
      },
      "anonymousAccess": {
          "expires_in": 2592001
      },
      "accessTokenClaims": [
      {
      "source": "attributes",
      "sourceClaim": "role"
      }
      ]
  }
  ```
  {: screen}


## Paso 5: Visualizar la señal de acceso
{: #roles-view-token}

Opcionalmente, puede verificar que el paso 4 se ha realizado correctamente visualizando una señal de acceso.
{: shortdesc}

1. A efectos de prueba, cree un usuario del directorio en la nube utilizando la GUI de {{site.data.keyword.appid_short_notm}}.

  1. En el separador **Usuarios**, pulse **Añadir usuario**. Aparece un formulario.
  2. Escriba un nombre y apellido, correo electrónico y contraseña.
  3. Pulse **Guardar**.

2. Codificar el ID de cliente y el secreto.

  1. En el separador **Credenciales de servicio** de la GUI de {{site.data.keyword.appid_short_notm}}, copie el ID de cliente y el secreto.
  2. Utilice un codificador base64 para codificar la información de autorización.
  3. Copie la salida que se va a utilizar en el mandato siguiente.

4. Inicie sesión utilizando las API para obtener información de señal de acceso. La señal devuelta está codificada.

  ```
  curl --request PUT \
  https://appid.cloud.ibm.com/oauth/v4/<tenant-ID>/token \
  --header 'Authorization: Basic <encoded-clientID>:<encoded-client-secret>' \
  --header 'Content-Type: application/x-www-form-urlencoded' \
  --header `Accept: application/json`
  - d 'grant_type=password&username=<user-email>%40<user-email-domain>&password=<user-password>
  ```
  {: pre}

5. Decodifique la señal de acceso.
  1. Copie la señal en la salida de la respuesta del mandato anterior.
  2. En un navegador, vaya a https://jwt.io/.
  3. Pegue la señal en el recuadro etiquetado **Codificado**.

6. En la sección **Decodificado**, verifique que puede ver el rol.

  ```
  {
    "iss": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61",
    "exp": 1551903163,
    "aud": [
      "968c2306-9aef-4109-bc06-4f5ed6axi24a"
    ],
    "sub": "2b96cc04-eca5-4122-a8de-6e07d14c13a5",
    "email_verified": true,
    "amr": [
      "cloud_directory"
    ],
    "iat": 1551899553,
    "tenant": "39a37f57-a227-4bfe-a044-93b6e6050a61",
    "scope": "openid appid_default appid_readprofile appid_readuserattr appid_writeuserattr appid_authenticated"
    "role": "manager"
  }
  ```
  {: screen}



## Pasos siguientes
{: #roles-next}

¡Buen trabajo! Ha completado la guía de aprendizaje. A continuación, puede intentar configurar la [autenticación de multifactores](/docs/services/appid?topic=appid-cd-mfa) o configurar [su propia GUI de acuerdo con su marca](/docs/services/appid?topic=appid-branded).
