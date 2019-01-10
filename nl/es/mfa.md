---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}


# Autenticación de multifactores
{: #mfa}

La autenticación de multifactores (MFA) es un método para confirmar la identidad de un usuario requiriendo al mismo utilizar algo que tenga además de algo que conozca para verificar que es quien dicen ser. Por ejemplo, con {{site.data.keyword.appid_full}} puede hacer que un usuario especifique un código de un solo uso que se envía a su correo electrónico tras identificarse con el correo electrónico y la contraseña.
{: shortdesc}

MFA está disponible solo para los usuarios del directorio en la nube.  Si utiliza el inicio de sesión de la empresa con SAML 2.0 o el inicio de sesión social, puede habilitar MFA en el proveedor de identidad que está utilizando.
{: note}

Cuando la MFA está habilitada, el widget de inicio de sesión requiere la misma cada vez que un nuevo usuario intenta iniciar sesión. Una vez que el usuario haya especificado correctamente sus credenciales, se enviará un código de acceso puntual a la dirección de correo electrónico que registró cuando creó la cuenta. Cada código tiene seis caracteres y caduca pasados cinco minutos. Si un usuario no recibe el código, puede solicitar que se envíe otro código, pero la hora de caducidad no se restablece. Cuando un código caduca, el usuario se ve forzado a repetir todo el proceso de inicio de sesión.

Si un correo electrónico de usuario no se ha confirmado a través de las API de gestión o mediante la verificación de correo electrónico en el registro, se confirma cuando una verificación de código de MFA se realiza correctamente. Si tiene que cambiar la dirección de correo electrónico de un usuario, el administrador puede utilizar las [API de gestión](https://appid-management.ng.bluemix.net/swagger-ui/#!/Cloud_Directory_Users/updateCloudDirectoryUser).

MFA está disponible para las instancias de {{site.data.keyword.appid_short_notm}} que se encuentran en el [plan de precios de nivel graduado](faq.html#pricing).
{: note}

## Comprensión del flujo
{: #understanding}



1. El usuario de la app se muestra en la IU del inicio de sesión predeterminado de {{site.data.keyword.appid_short_notm}}.

2. El usuario especifica las credenciales de usuario del directorio en la nube, como el correo electrónico o el nombre de usuario y su contraseña.

3. Las credenciales se validan y el formulario de MFA se devuelve. El formulario solicita al usuario pegar el código que se ha enviado por correo electrónico.

4. El usuario recibe un código de acceso puntual en la dirección de correo electrónico y lo especifica en la IU de MFA predeterminada.

5. El código de MFA se valida y redirige a la app de cliente con el código de autorización para continuar con el flujo de OAuth 2.


</br>

## Configuración de MFA
{: #configuration}

La MFA de {{site.data.keyword.appid_short_notm}} se soporta como parte del flujo de código de autorización OAuth 2.0 para usuarios de Directorio en la nube mediante el widget de inicio de sesión.
{: shortdesc}

Para configurar la MFA mediante la GUI, consulte [Directorio en la nube](cloud-directory.html).
{: note}

### Configuración con la API

Puede configurar la MFA utilizando las API de gestión.
{: shortdesc}

**Antes de empezar**

Asegúrese de que tiene los requisitos previos siguientes:

* El ID de arrendatario de la instancia de {{site.data.keyword.appid_short_notm}}. Lo encontrará en la sección **Credenciales de servicio** del panel de control.
* La señal Gestión de identidad y acceso (IAM). Si necesita ayuda para obtener la señal de IAM, consulte los [documentos de IAM](/docs/iam/apikey_iamtoken.html).


1. Habilite la MFA, realizando una solicitud PUT en el punto final `/config/mfa` con la configuración de MFA para establecer `isActive` en `true`.

  Cabecera:
  ```
  PUT {management-url}/management/v4/{tenantId}/config/mfa
       Host: <management-server-url>
       Authorization: Bearer <IAM_TOKEN>
       Content-Type: application/json
  ```
  {: pre}

  Cuerpo:
  ```
   {
       "isActive": true
   }
  ```
  {: pre}

  Solicitud de ejemplo:
  ```
  $ curl -X PUT
    --header 'Content-Type: application/json'
    --header 'Accept: application/json'
    --header 'Authorization: Bearer <IAM_TOKEN>'
    -d '{
          "isActive": true
      }'
    }'
    '{management-url}/management/v4/{tenantId}/config/mfa'
  ```
  {: screen}

2. Habilite el canal de MFA realizando una solicitud PUT en el punto final `/mfa/channels/{channelType}` con la configuración de MFA. Cuando `isActive` se establece en `true`, se habilita el canal de MFA.

  Cabecera:
  ```
  PUT /management/v4/{tenantId}/mfa/channels/{channelType}
       Host: <management-server-url>
       Authorization: Bearer <IAM_TOKEN>
       Content-Type: application/json
  ```
  {: pre}

  <table>
    <thead>
      <th colspan=3>Tipos de canal soportados</th>
    </thead>
    <tbody>
      <tr>
        <td>`correo electrónico`</td>
      </tr>
    </tbody>
  </table>

  Cuerpo:
  ```
   {
       "isActive": true
   }
  ```
  {: pre}

  Solicitud de ejemplo:
  ```
  $ curl -X PUT
    --header 'Content-Type: application/json'
    --header 'Accept: application/json'
    --header 'Authorization: Bearer <IAM_TOKEN>'
    -d '{
          "isActive": true
      }'
    }'
    '{management-url}/management/v4/{tenantId}/mfa/channels/{channelType}'
  ```
  {: screen}

</br>
