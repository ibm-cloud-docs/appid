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

# Directorio en la nube
{: #cd}

Con {{site.data.keyword.appid_full}}, los usuarios pueden registrarse e iniciar la sesión en sus apps web y móviles mediante un correo electrónico o un nombre de usuario y una contraseña. Un directorio en la nube es un registro de usuarios que está mantenido en la nube. Cuando un usuario se registra en su app, se le añade al directorio de usuarios. Con esta característica, los usuarios tienen la libertad de gestionar sus propias cuentas dentro de la app.
{: shortdesc}

</br>

## Gestión de los valores de directorio
{: #cd-settings}

Puede configurar las notificaciones y el nivel de control de usuario para su app. La configuración del procesador único puede realizarse rápidamente, tal como se muestra en la siguiente imagen. Estos valores pueden actualizarse en cualquier momento desde el panel de control del servicio.
{: shortdesc}


![Configuración del directorio en la nube](images/cloud-directory.png)
Figura. Guía de configuración del Directorio en la nube

1. En el separador **Gestionar** del panel de control de {{site.data.keyword.appid_short_notm}}, asegúrese de que el directorio en la nube se establezca en **Activado**.

2. Configure los valores generales.
  1. Decida si desea que los usuarios creen un nombre de usuario o utilicen su correo electrónico cuando inicien sesión. Ambas opciones requieren una contraseña. Una vez que los usuarios se hayan añadido al directorio, ya no podrá alternar entre las opciones.
  2. Pulse en **Editar** en la fila de criterios de contraseña para especificar los requisitos que desea poner en marcha. Los criterios de contraseña se proporcionan en forma de expresión regular. Para ayudar a determinar la fortaleza o ver ejemplos comunes, consulte [Gestionar la fortaleza de contraseña](#strength). Pulse en **Guardar** para poner los requisitos en acción.
  3. Establezca **Permitir a los usuarios iniciar sesión en la app** en **Sí**. Podrá continuar añadiendo usuarios a la consola si se establece en **No**. Sin embargo, debería añadir usuarios mediante la consola únicamente para fines de desarrollo.
  4. Establezca **Permitir a los usuarios gestionar su cuenta desde la app** en **Sí** si desea que los usuarios puedan restablecer o cambiar la contraseña o restablecer los detalles. Si desea limitar el autoservicio de los usuarios, establezca el valor en **No**.
  5. Pulse **Editar** en la fila **Detalles del remitente** para actualizar la configuración de correo electrónico. Los valores de correo electrónico se aplican a todas las comunicaciones que se envían a través de {{site.data.keyword.appid_short_notm}}. Especifique la dirección de correo electrónico que debe enviar el correo, el nombre y deje otro correo electrónico para que los usuarios envíen una respuesta.
  6. Habilite **Política de contraseña avanzada** para crear limitaciones y requisitos para las contraseñas. Esta característica requiere una facturación adicional. Para obtener más información sobre las opciones, consulte [Política de contraseñas avanzada](#advanced-password).
  6. Pulse **Guardar**.

3. Configure los valores de correo electrónico de verificación.
  1. Para que los usuarios verifiquen su dirección de correo electrónico, establezca **Verificación de correo electrónico** en **Activado**. Cuando un usuario se registra en su app, recibe un correo electrónico que le solicita confirmar que se han registrado en la app.
  2. Si ha decidido que desea que los usuarios verifiquen su correo electrónico, lo siguiente será decidir si desea permitir que los usuarios utilicen la aplicación antes de verificar la dirección de correo electrónico. En función de sus preferencias, establezca **Permitir a los usuarios registrarse en la app sin verificar la dirección de correo electrónico primero** en **Sí** o **No**.
  3. Personalice el contenido y diseñe el aspecto del mensaje. Existe una plantilla para el mensaje, pero puede actualizar el texto con su propio mensaje. Puede utilizar un [idioma](/docs/services/appid/cloud-directory.html#languages) que no sea el inglés, pero es responsable de la traducción del texto. Para elegir otro idioma, utilice las <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/updateLocalization" target="_blank">API de gestión de idioma <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.
  4. Proporcione al URL de verificación una hora de caducidad, especificada en minutos.  Cuando se establece la hora, esta también afecta al período de tiempo durante el cual el enlace de restablecimiento de contraseña es válido.
  5. Especifique un URL de página de verificación propio si hay una página en concreto que desea que los usuarios vean cuando pulsen en el enlace. Si deja el campo **Personalizar URL de página de verificación** en blanco, {{site.data.keyword.appid_short_notm}} proporcionará una página de verificación predeterminada.
  6. Pulse **Guardar**.

4. Configure los valores de correo electrónico de bienvenida.
  1. Para dar la bienvenida a los usuarios a través del correo electrónico cuando se registren en la app, establezca el **Correo electrónico de bienvenida** en **Activado**.
  2. Personalice el contenido y diseñe el aspecto del mensaje. Existe un mensaje de ejemplo, pero puede actualizar el texto con su propio mensaje. Puede utilizar un [idioma](#languages) que no sea el inglés, pero es responsable de la traducción del texto. Para elegir otro idioma, utilice las <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/updateLocalization" target="_blank">API de gestión de idioma <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.
  3. Pulse **Guardar**.

5. Configure los valores de restablecimiento de contraseña.
  1. Para permitir a los usuarios solicitar un restablecimiento de contraseña, establezca **Correo electrónico de contraseña olvidada** en **Activado**. **Nota**: El usuario debe haber validado el correo electrónico antes de restablecer la contraseña. Esto significa que deberá solicitar la verificación del correo electrónico para que los usuarios puedan restablecer la contraseña.
  2. Personalice el contenido y diseñe el aspecto del mensaje. Existe un mensaje de ejemplo, pero puede actualizar el texto con su propio mensaje. Puede utilizar un [idioma](#languages) que no sea el inglés, pero es responsable de la traducción del texto. Para elegir otro idioma, utilice las <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/updateLocalization" target="_blank">API de gestión de idioma <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.
  3. Proporcione al URL de restablecimiento de contraseña una hora de caducidad límite, especificada en minutos. Cuando se establece la hora, esta también afecta al período de tiempo durante el cual el enlace de verificación de correo electrónico es válido.
  4. Especifique un URL de restablecimiento de contraseña propio si hay una página en concreto que desea que los usuarios vean cuando pulsen en el enlace. Si deja el campo **Restablecer URL de página de contraseña** en blanco, {{site.data.keyword.appid_short_notm}} proporcionará una página de contraseña predeterminada.
  5. Pulse **Guardar**.

6. Configure los valores de cambio de contraseña.
  1. Para informar a los usuarios acerca de los cambios realizados en la contraseña, establezca **Correo electrónico de contraseña cambiada** en **Activado**.
  2. Personalice el contenido y diseñe el aspecto del mensaje. Existe un mensaje de ejemplo, pero puede actualizar el texto con su propio mensaje. Puede utilizar un [idioma](#languages) que no sea el inglés, pero es responsable de la traducción del texto. Para elegir otro idioma, utilice las <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/updateLocalization" target="_blank">API de gestión de idioma <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.
  3. Pulse **Guardar**.

7. Configure la autenticación de multifactores.
  1. Para solicitar la autenticación de multifactores en el inicio de sesión de usuario, establezca **Habilitar autenticación de multifactores de correo electrónico** en **Activado**.
  2. Personalice el contenido y diseño del correo electrónico utilizando la plantilla siguiente. Puede utilizar un [idioma](#languages) que no sea el inglés, pero es responsable de la traducción del texto. Para elegir otro idioma, utilice las <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/updateLocalization" target="_blank">API de gestión de idioma <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.
  3. Pulse **Guardar**.

8. En el separador **Usuarios** puede ver quien ha iniciado sesión en su app. Nota: Un solo usuario puede intentar iniciar sesión hasta 5 veces en 60 segundos. Si lo intenta por sexta vez, aparece un error.

</br>
</br>

## Tipos de mensajes
{: #types}

Puede enviar varios tipos de mensajes a sus usuarios. Puede elegir enviar el mensaje de ejemplo proporcionado por el servicio o puede personalizar el contenido para conseguir una experiencia más personal con la app. {{site.data.keyword.appid_short_notm}} utiliza <a href="https://www.sendgrid.com" target="_blank">SendGrid <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> como servicio de entrega de correo. Todos los correos electrónicos se envían con una sola cuenta de SendGrid.
{: shortdesc}

Si un usuario no proporciona la información extraída por el parámetro, aparecerá en blanco.
{: tip}

<dl>
  <dt>Bienvenido</dt>
    <dd><p>Después de haberse registrado, puede recibir a un usuario a la aplicación por correo electrónico. Para dar la bienvenida y retener a los usuarios, haga su mensaje tan interactivo como sea posible.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="Icono de más información"/> Todos los parámetros de mensaje </th>
      </thead>
      <tbody>
        <tr>
          <td><code>%{display.logo}</code></td>
          <td> Muestra la imagen que ha configurado para su widget de inicio de sesión. </td>
        </tr>
        <tr>
          <td><code>%{user.displayName}</code></td>
          <td> Muestra el nombre de pantalla que elige un usuario para utilizar al interactuar con la app. </td>
        </tr>
        <tr>
          <td><code>%{user.email}</code></td>
          <td> Muestra la dirección de correo electrónico registrada del usuario. </td>
        </tr>
        <tr>
          <td><code>%{user.username}</code></td>
          <td> Muestra el nombre de usuario especificado del usuario cuando el método de autenticación se establece en nombre de usuario y contraseña. </td>
        </tr>
        <tr>
          <td><code>%{user.firstName}</code></td>
          <td> Muestra el nombre especificado del usuario. </td>
        </tr>
        <tr>
          <td><code>%{user.formattedName}</code></td>
          <td> Muestra el nombre completo del usuario. </td>
        </tr>
        <tr>
          <td><code>%{user.lastName}</code></td>
          <td> Muestra el apellido especificado del usuario. </td>
        </tr>
      </tbody>
    </table></dd>
  <dt>Contraseña olvidada</dt>
    <dd><p>Un usuario puede pedir el restablecimiento de contraseña si la ha olvidado o si necesita actualizarla por cualquier motivo. Puede personalizar la respuesta por correo electrónico a su solicitud. Cuando un usuario solicita un cambio, su contraseña sigue siendo la misma hasta que pulsa en el enlace en este correo electrónico.</p>
    <table>
      <tr>
        <th colspan=2><img src="images/idea.png" alt="Icono de más información"/> Parámetros de contraseña olvidados </th>
      </tr>
      <tr>
        <td><code>%{linkExpiration.hours}</code></td>
        <td> Muestra el número de horas que es válido el enlace.</td>
      </tr>
      <tr>
        <td><code>%{linkExpiration.minutes}</code></td>
        <td>Muestra el número de minutos que es válido el enlace.</td>
      </tr>
      <tr>
        <td><code>%{resetPassword.code}</code></td>
        <td> Muestra una clave de acceso de un único uso como parte del URL. Esto significa que cada persona tendría un código diferente. Ejemplo: <code>https://appid.cloud.ibm.com/wfm</td>
      </tr>
      <tr>
        <td><code>%{resetPassword.link}</code></td>
        <td> Muestra el enlace que pulsa un usuario para restablecer su contraseña. </td>
      </tr>
     </tbody>
  </table></dd>
  <dt>Verificación</dt>
    <dd><p>Puede solicitar que el usuario verifique su cuenta por correo electrónico. Al solicitar una verificación, se limita el número de cuentas falsas que pueden registrarse en su app. Puede restringir el acceso a su app hasta que el usuario haya verificado su correo electrónico, o utilizarlo como forma de gestionar los usuarios para los que ha creado perfiles. Tenga en cuenta que los usuarios que se añaden manualmente mediante el panel de control de {{site.data.keyword.appid_short_notm}} o la API de creación de usuarios no reciben este correo electrónico automáticamente.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="Icono de más información"/> Parámetros de mensaje de verificación </th>
      </thead>
      <tbody>
        <tr>
          <td><code>%{linkExpiration.hours}</code></td>
          <td> Muestra el número de horas que es válido el enlace. </td>
        </tr>
        <tr>
          <td><code>%{linkExpiration.minutes}</code></td>
          <td> Muestra el número de minutos que es válido el enlace. </td>
        </tr>
        <tr>
          <td><code>%{verify.code}</code></td>
          <td> Muestra un URL de verificación de un único uso. </td>
        </tr>
        <tr>
          <td><code>%{verify.link}</code></td>
          <td> Muestra el URL de acción que especificó en los valores. </td>
        </tr>
      </tbody>
    </table></dd>
  <dt>Cambio de contraseña</dt>
    <dd><p>Puede hacer saber al usuario cuándo se ha actualizado su contraseña. Esto es útil si no ha solicitado el cambio de contraseña. Pueden llevar a cabo los pasos apropiados para volver a asegurar su cuenta.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="Icono de más información"/> Parámetros de cambio de contraseña</th>
      </thead>
      <tbody>
        <tr>
          <td><code>%{passwordChangeInfo.time}</code></td>
          <td> Muestra la hora en que entra en vigor la nueva contraseña. </td>
        </tr>
        <tr>
          <td><code>%{passwordChangeInfo.ipAddress}</code></td>
          <td> Muestra la dirección IP desde la que se ha solicitado el cambio de contraseña. </td>
        </tr>
      </tbody>
    </table></dd>
    </dd>
    <dt>Código de verificación MFA</dt>
      <dd><p>Cuando se habilita la autenticación de multifactores, los usuarios pueden recibir códigos de cambio como medio secundario de la autenticación.</p>
      <table>
        <thead>
          <th colspan=2><img src="images/idea.png" alt="Icono de más información"/> Todos los parámetros de mensaje </th>
        </thead>
        <tbody>
          <tr>
            <td><code>%{mfa.code}</code></td>
            <td> Muestra un código de verificación MFA de un único uso. </td>
          </tr>
        </tbody>
      </table></dd></dl>

</br>
</br>

## Gestión de la fortaleza de contraseña
{: #strength}

Puede definir los requisitos para las contraseñas que se pueden utilizar con el Directorio en la nube.
{: shortdesc}

Una contraseña segura es difícil o improbable de adivinar ya sea de forma manual o automática. La fortaleza de contraseña se define como una serie de expresión regular.

Estos son algunos ejemplos habituales de fortaleza de contraseña:

- Debe tener al menos ocho caracteres. Expresión regular de ejemplo: `^.{8,}$`
- Debe contener un número, una letra minúscula y una letra mayúscula. Expresión regular de ejemplo: `^(?:(?=.*\d)(?=.*[a-z])(?=.*[A-Z]).*)$`
- Debe contener solo letras y números ingleses. Expresión regular de ejemplo: `^[A-Za-z0-9]*$`
- Debe tener al menos un carácter exclusivo. Expresión regular de ejemplo: `^(\w)\w*?(?!\1)\w+$`

La fortaleza de la contraseña se puede establecer en la página de valores del directorio en la nube en la consola del ID de app o utilizando las <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/set_cloud_directory_password_regex" target="_blank">API de gestión <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.

</br>


## Política de contraseñas avanzada
{: #advanced-password}


Puede mejorar la seguridad de la aplicación imponiendo restricciones de contraseña adicionales.
{: shortdesc}


La política de contraseñas avanzada consta de 5 características que se pueden alternar por separado.

 - Bloqueo tras repetir las credenciales de forma errónea
 - Evitar la reutilización de las contraseñas
 - Caducidad de la contraseña
 - Período mínimo entre los cambios de contraseña
 - Garantizar que la contraseña no incluye el nombre de usuario


 Si habilita esta característica, se activará la facturación adicional para las prestaciones de seguridad avanzadas. Para obtener más información, consulte la [Calculador de precios](faq.html#pricing).

</br>

### Evitar la reutilización de las contraseñas
{: #avoid-reuse}

Cuando los usuarios cambien la contraseña, es posible que desee evitar que elijan una contraseña utilizada recientemente.
{: shortdesc}

Mediante la GUI o la API, puede seleccionar el número de contraseñas que debe tener un usuario antes de poder repetir una contraseña utilizada anteriormente. Puede seleccionar cualquier valor entero entre 1 y 10.

Si esta opción está activada y uno de los usuarios intenta cambiar su contraseña por otra que ha utilizado recientemente, visualizarán un error en el inicio de sesión de la IU del widget y se les solicitará que especifiquen una contraseña distinta.

Las contraseñas anteriores se almacenan de forma segura de la misma forma que se almacena la contraseña actual de un usuario.

</br>

### Bloqueo tras repetir las credenciales de forma errónea
{: #lockout}

Es posible que desee proteger las cuentas de los usuarios bloqueando temporalmente la posibilidad de iniciar sesión cuando se detecta un comportamiento sospechosos como, por ejemplo, intentos de inicio de sesión consecutivos con una contraseña incorrecta. Esta medida puede ayudarle a evitar que una parte maliciosa obtenga acceso a la cuenta de un usuario adivinando la contraseña del mismo.
{: shortdesc}

Mediante la GUI o la API, puede establecer el número máximo de intentos de inicio de sesión fallidos que puede realizar un usuario antes de que su cuenta quede bloqueada temporalmente. También puede establecer la cantidad de tiempo que la cuenta está bloqueada. Dispone de las siguientes opciones:

* Número de intentos: Cualquier valor entero entre 1 y 10.
* Período de bloqueo: Cualquier valor entero entre 1 minuto y 24 horas, especificado en minutos.

Si una cuenta está bloqueada, los usuarios no podrán iniciar sesión o realizar cualquier otra operación de autoservicio, como cambiar la contraseña hasta que haya transcurrido el período de bloqueo especificado. Cuando el período de bloqueo haya finalizado, el usuario se desbloqueará automáticamente.

Puede desbloquear un usuario antes de que se haya terminado el período de bloqueo. Para ver si están bloqueados, consulte si el campo `active` (activo) se establece en `false`. También puede comprobar si el estado del separador **Usuarios** del panel de control de servicio está establecido en `disabled` (inhabilitado). Para desbloquear un usuario, debe utilizar [la API](https://appid-management.ng.bluemix.net/swagger-ui/#!/Cloud_Directory_Users/updateCloudDirectoryUser) para establecer el campo `active` (activo) en `true`.

</br>

### Período mínimo entre los cambios de contraseña
{: #minimum-time}

Es posible que desee evitar que los usuarios cambien la contraseña rápidamente estableciendo el período de tiempo mínimo que un usuario debe esperar para poder cambiar la contraseña.
{: shortdesc}

Esta característica es especialmente útil cuando se utiliza junto a la política "Evitar la reutilización de contraseñas". Sin esta limitación, un usuario podría cambiar de contraseña varias veces seguidas para omitir la limitación de volver a utilizar contraseñas recientes. Puede seleccionar cualquier valor entre 1 hora y 30 días, especificado en horas.

</br>

### Caducidad de la contraseña
{: #expiration}

Por motivos de seguridad, es posible que desee aplicar una política de rotación de contraseñas, de manera que los usuarios deban cambiar su contraseña después de un período de tiempo.
{: shortdesc}

Al utilizar la GUI o la API, puede establecer un período de tiempo durante el cual las contraseñas del usuario seguirán siendo válidas. Cuando la contraseña del usuario caduque, este se verá obligado a restablecer la contraseña en el próximo inicio de sesión. Puede seleccionar cualquier número de días completos entre 1 y 90.

El servicio proporciona una GUI y una experiencia predeterminadas listas para usarse con el widget de inicio de sesión. El usuario recibe instrucciones para proporcionar una nueva contraseña antes de que se complete el inicio de sesión.

Si utiliza un inicio de sesión personalizado, se activará un error cuando el usuario intente iniciar sesión con una contraseña caducada. Es su responsabilidad configurar la aplicación para que proporcione la experiencia de usuario necesaria. Puede llamar la API de cambio de contraseña para establecer la nueva contraseña.

La respuesta del punto final de señal tiene un aspecto parecido al siguiente:

```javascript
{
  "error" : "invalid_grant",
  "error_description" : "Password expired",
  "user_id" : "356e065e-49da-45f6-afa3-091a7b464f51"
}
```
{: screen}

Cuando esta opción se activa, las contraseñas de usuario existentes no tendrán una fecha de caducidad. El período de caducidad empieza para dichos usuarios cuando se cambia la contraseña. Es posible que desee animar a los usuarios a actualizar la contraseña después de haber activado la característica.
{: note}

</br>

### Garantizar que la contraseña no incluye el nombre de usuario
{: #no-username}

Para obtener contraseñas más fuertes, es posible que desee evitar los usuarios que contienen su nombre de usuario o la primera parte de su dirección de correo electrónico.
{: shortdesc}

Esta restricción distingue entre mayúsculas y minúsculas, lo que significa que los usuarios no pueden alterar las mayúsculas y minúsculas de algunos o varios caracteres para poder utilizar la información personal. Para configurar esta opción, cambie el conmutado en **Activado**.

</br>

## Utilización de un remitente de correo electrónico personalizado
{: #custom-email}

Con {{site.data.keyword.appid_short_notm}}, puede definir un punto de extensión personalizado para que envíe mensajes de correo electrónico del directorio en la nube. Al definir un punto de extensión, tiene el control completo de cómo se envían los correos electrónicos y puede utilizar su propio nombre de dominio.
 {: shortdesc}

**¿Por qué debería utilizar un remitente de correo electrónico personalizo?**

DE forma predeterminada, {{site.data.keyword.appid_short_notm}} utiliza SendGrid para entregar mensajes en su nombre. Al configurar su propio remitente de correo electrónico puede mejorar aún más la experiencia de marca para los usuarios de app.

Algunos ejemplos más concretos:
- **Dominio personalizado**
Mediante la configuración de un distribuidor de correo electrónico tendrá un control completo sobre cómo se envían los mensajes de correo electrónico. Incluye la personalización del dominio de correo electrónico, que puede reducir todavía más las posibilidades de que los correos electrónicos se filtren como spam.
- **Conocimientos y resolución de problemas**
Obtenga conocimientos del proveedor de correo electrónico como, por ejemplo, el número de personas que han abierto los correos electrónicos o los mensajes que no se han entregado. Puesto que puede realizar un seguimiento de los mensajes individuales y ver las estadísticas globales, esto puede ayudarle a resolver problemas.

</br>

**¿Cómo funciona?**

Una vez configurado el punto de extensión, {{site.data.keyword.appid_short_notm}} lo llamará siempre que deba enviarse un mensaje de correo electrónico. El punto de extensión contiene toda la información sobre el mensaje, incluido el contenido final del cuerpo del correo electrónico.

</br>

**Para crear un remitente de correo electrónico personalizado:**

1. Para poder configurar la instancia de {{site.data.keyword.appid_short_notm}} para que utilice un distribuidor personalizado, utilice <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/set_cloud_directory_email_dispatcher" target="_blank">la API de gestión</a>.</br>
Debe proporcionar el URL. Además, puede proporcionar información de autorización. Los tipos de autorización soportados son: `Autorización básica` o un `valor de cabecera de autorización constante`.

  Ejemplos de configuración válidos:
  ```
  {
    "custom": {
      "url": "https://example.com/send_mail"
    }
  }
  ```
  {: screen}

  ```
  {
    "custom": {
      "url": "https://example.com/send_mail",
      "authorization": {
        "type": "basic",
        "username": "username",
        "password": "password"
      }
    }
  }
  ```
  {: screen}

  ```
  {
    "custom": {
      "url": "https://example.com/send_mail",
      "authorization": {
        "type": "value",
        "value": "myApiKey"
      }
    }
  }
  ```
  {: screen}

2. Configure un punto de extensión que pueda escuchar la solicitud de publicación. El punto final debe poder leer la carga útil que proviene de {{site.data.keyword.appid_short_notm}} y enviar el correo electrónico con el remitente de correo electrónico personalizado.

3. El cuerpo enviado desde {{site.data.keyword.appid_short_notm}} tiene el formato siguiente: `{"jws": "jws-format-string"}`. </br> Una vez haya descodificado y verificado la carga útil, el contenido será una serie JSON.</br>
  ```
    {
      "tenant": "tenant-id",
      "iss" : "appid-oauth.ng.bluemix.net",
      "iat": 1539173126,
      "jti": "uniq-id",
      "message": {
          "to": "your@mail.com",
          "from": {
              "name": "My Awesome Service",
              "address": "no-reply@company.com"
          },
          "replyTo": {
              "name": "My Awesome Service",
              "address": "yes-reply@company.com"
          },
          "subject": "Welcome to My Awesome Service",
          "body": "<p>Hello<p><br/><p>Thanks for signing up John Doe</p>"
      }
    }
  ```
  {: screen}

  - arrendatario: tenantId de la instancia de ID de app
  - iat: indicación de la fecha y la hora en que se ha enviado el mensaje
  - iss: identifica el principal que ha emitido el JWS.
  - jti: ID de transacción único
  - message: mensaje que se va a enviar; consta de los campos siguientes:
    - to: dirección de correo electrónico del destinatario
    - from: información del remitente; consta de los campos siguientes:
      - name: opcional, nombre del remitente
      - address: dirección del remitente
    - reply to: opcional, consta de los campos siguientes:
      - name: opcional, nombre del remitente
      - address: opcional, dirección del remitente
    - subject: asunto del correo electrónico
    - body: cuerpo del correo electrónico, en formato html

  Puede comprobar que la solicitud se ha realizado correctamente comprobando el código de estado de respuesta. Siempre que el rango sea de 200 a 299, se habrá realizado correctamente. Si recibe cualquier otra respuesta, intente volver a realizar la solicitud.
  {: tip}

4. Cada carga útil de HTTP que se envía desde {{site.data.keyword.appid_short_notm}} se firma de forma automática de acuerdo con el estándar JWS utilizando un par de claves asimétricas.
Para cada instancia de {{site.data.keyword.appid_short_notm}}, se generan una clave pública y privada que no se comparten con otras instancias. La clave privada se utiliza para firmar la carga útil de HTTP y puede utilizar la clave pública para verificar que {{site.data.keyword.appid_short_notm}} genera la carga útil y que no la altera ningún <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#!/Authorization_Server_V3/publicKeys" target="_blank">punto final de clave público</a> de terceros.

5. Código de ejemplo para el punto de extensión (JavaScript)
  ```
  const sgMail = require('@sendgrid/mail');
  const {promisify} = require('bluebird');
  const request = promisify(require('request'));
  const jwtVerify = promisify(require('jsonwebtoken').verify);
  const jwtDecode = require('jsonwebtoken').decode;
  const jwkToPem = require('jwk-to-pem');

  async function obtainPublicKeys() {
  	// El ID de arrendatario de la instancia de su ID de app
  	const tenantId = '<TENANT-ID>';

  	// Enviar una solicitud a un punto final de claves públicas del ID de app
  	const keysOptions = {
  		method: 'GET',
  		url: `https://appid-oauth.<REGION>.bluemix.net/oauth/v3/${tenantId}/publickeys`
  	};
  	const keysResponse = await request(keysOptions);
  	return JSON.parse(keysResponse.body).keys;
  }

  async function verifySignature(keysArray, kid, jws) {
  	const keyJson = keysArray.find(key => key.kid === kid);
  	if (keyJson) {
  		const pem = jwkToPem(keyJson);
  		await jwtVerify(jws, pem);
  		return;
  	}
  	throw new Error ("Unable to verify signature");
  }

  async function verifyAndSendMail(jws) {
  	// La clave de API de Sendgrid
  	const sgApiKey = '<SENDGRID-API-KEY>';

  	// Init Sendgrind
  	sgMail.setApiKey(sgApiKey);

  	// Mensaje de descodificación para obtener información
  	const data = jwtDecode(jws, {complete: true});

  	// Extraer hijo de la cabecera
  	const kid = data.header.kid;

  	const keysArray = await obtainPublicKeys();

  	// Verificar la firma de la carga útil con las claves públicas
  	await verifySignature(keysArray, kid ,jws);

  	// Enviar el correo electrónico con la cuenta de Sendgrid
  	const message = data.payload.message;
  	const msg = {
  		to: message.to,
  		from: message.from.address,
  		subject: message.subject,
  		html: message.body,
  	};
  	console.log(`Sending email to ${message.to}`);
  	let sendgridResponse = await sgMail.send(msg);

  	return {result : 'email_sent',sendgridResponse};
  }
  ```
  {: codeblock}

6. Compruebe que la configuración se ha configurado correctamente probando el distribuidor de correo electrónico. Utilice la <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/post_email_dispatcher_test" target="_blank">API de prueba</a> para activar una solicitud en el remitente de correo electrónico personalizado configurado.

Para obtener un ejemplo de trabajo completo, consulte <a href="https://www.ibm.com/blogs/bluemix/2018/10/use-ibm-cloud-app-id-and-your-email-provider-to-brand-mails-sent-to-app-users/" target="_blank">Utilizar un proveedor propio para el envío de correo con {{site.data.keyword.appid_full}}</a>.

</br>
</br>


## Migración de usuarios
{: #user-migration}

Es posible que en alguna ocasión deba configurar una nueva instancia de {{site.data.keyword.appid_short_notm}}. Si utiliza Cloud Directory, esto significa que los usuarios deben migrarse a la nueva instancia. Puede utilizar las API de gestión para que le ayuden con la migración.
{: shortdesc}

### Antes de empezar

Debe tener asignado el [rol de IAM](/docs/iam/quickstart.html) `Gestor` para ambas instancias de {{site.data.keyword.appid_short_notm}}.

</br>

**Exportación**

Antes de poder añadir los usuarios a la nueva instancia, deberá exportarlos desde la instancia actual. Para ello, puede utilizar la <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Cloud_Directory_Users/cloudDirectoryExport" target="_blank">API de gestión de exportación <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.

Mandato cURL de ejemplo:

```
curl -X GET --header ‘Accept: application/json’ --header ‘Authorization: Bearer <iam-token>’ ’https://<staging>eu-gb.appid.cloud.ibm.com</staging><prod>appid-management.eu-gb.bluemix.net</prod>/management/v4/111c9bj3-xxxx-4b5b-zzzz-24ad9440k8j9/cloud_directory/export?encryption_secret=myCoolSecret'
```
{: codeblock}

<table>
  <tr>
    <th>Variable</th>
    <th>Descripción</th>
  </tr>
  <tr>
    <td><code>encryption_secret</code></td>
    <td>Una serie personalizada que se utiliza para cifrar y descifrar la contraseña oculta de un usuario.</td>
  </tr>
  <tr>
    <td><code> tenantID </code></td>
    <td>El ID de arrendatario de servicio se puede encontrar en las credenciales de servicio. Encontrará las credenciales de servicio en el panel de control del ID de app.</td>
  </tr>
</table>

Solo se devuelven los usuarios del directorio en la nube y sus perfiles. Los usuarios de otros proveedores de identidad no.
{: note}

</br>

**Importación**

Ahora que los usuarios están listos para empezar, puede importar su información en la nueva instancia. Para ello, puede utilizar la <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Cloud_Directory_Users/cloudDirectoryImport" target="_blank">API de gestión de importación <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.

Mandato cURL de ejemplo:

```
curl -X POST --header ‘Content-Type: application/json’ --header ‘Accept: application/json’ --header ‘Authorization: Bearer <iam-token>’ -d ‘{“users”: [
    {
      “scimUser”: {
        “originalId”: “3f3f6779-7978-4383-926f-a43aef3b724b”,
        “name”: {
          “givenName”: “<first-name>”,
          “familyName”: “<last-name>”,
          “formatted”: “<first-name> <last-name>”
        },
        “displayName”: “<first-name>”,
        “emails”: [
          {
            “value”: “<user>@gmail.com”,
            “primary”: true
          }
        ],
        “status”: “PENDING”
      },
      “passwordHash”: “<password hash here>“,
      “passwordHashAlg”: “<password hash algorithm>",
      “profile”: {
        “attributes”: {}
      }
    }
]}’ ‘https://<staging>eu-gb.appid.cloud.ibm.com</staging><prod>appid-management.eu-gb.bluemix.net</prod>/management/v4/111c9bj3-xxxx-4b5b-zzzz-24ad9440k8j9/cloud_directory/import?encryption_secret=myCoolSecret’
```
{: codeblock}

</br>

### Utilización del script de migración

{{site.data.keyword.appid_short_notm}} proporciona un script de migración que puede utilizar mediante la CLI que puede ayudarle a agilizar el proceso de migración.

Antes de empezar, asegúrese de tener la siguiente información de parámetro:

<table>
  <tr>
    <th>Parameter</th>
    <th>Descripción</th>
  </tr>
  <tr>
    <td><code>sourceTenantId</code></td>
    <td>El ID de arrendatario de la instancia de {{site.data.keyword.appid_short_notm}} desde la que va a exportar usuarios.</td>
  </tr>
  <tr>
    <td><code>destinationTenantId</code></td>
    <td>El ID de arrendatario de la instancia de {{site.data.keyword.appid_short_notm}} desde la que va a importar usuarios.</td>
  </tr>
  <tr>
    <td>Región</td>
    <td>Las opciones actuales son: EE.UU. sur <code>ng</code>, Londres: <code>eu-gb</code>, Sídney: <code>au-syd</code>, Washington: <code>us-east</code> y Alemania: <code>eu-de</code>.</td>
  </tr>
  <tr>
    <td>Señal de IAM</td>
    <td>Asegúrese de que dispone de permisos de <code>gestor</code> antes de obtener la señal. Para obtener ayuda sobre cómo obtener una señal de IAM, compruebe <a href="https://console.bluemix.net/docs/iam/apikey_iamtoken.html#iamtoken_from_apikey" target="_blank">los documentos <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.</td>
  </tr>
</table>

Para ejecutar el script:

1. Clone el <a href="https://github.com/ibm-cloud-security/appid-sample-code-snippets/tree/master/export-import-cloud-directory-users" target="_blank">repositorio <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.
2. Abra el terminal y vaya a la carpeta en la que ha clonado el repositorio.
3. Ejecute el mandato siguiente.

  ```
  npm install
  ```
  {: codeblock}

4. Con los parámetros, ejecute el mandato siguiente.

  ```
  users_export_import 'sourceTenantId' 'destinationTenantId' 'region' 'iamToken'
  ```
  {: codeblock}

  Mandato de ejemplo:

  ```
  users_export_import e00a0366-53c5-4fcf-8fef-ab3e66b2ced8 73321c2b-d35a-497a-9845-15c580fdf58c ng eyJraWQiOiIyMDE3MTAyNS0xNjoyNzoxMCIsImFsZyI6IlJTMjU2In0.eyJpYW1faWQiOiJJQk1pZC0zMTAwMDBUNkZTIiwiaWQiOiJJQk1pZC0zMTAwMDBUNkZTIiwicmVhbG1pZCI6IklCTWlkIiwiaWRlbnRpZmllciI6IjMxMDAwMFQ2RlMiLCJnaXZlbl9uYW1lIjoiUm90ZW0iLCJmYW1pbHlfbmFtZSI6IkJyb3NoIiwibmFtZSI6IlJvdGVtIEJyb3NoIiwiZW1haWwiOiJyb3RlbWJyQGlsLmlibS5jb20iLCJzdWIiOiJyb3RlbWJyQGlsLmlibS5jb20iLCJhY2NvdW50Ijp7ImJzcyI6ImQ3OWM5YTk5NjJkYzc2Y2JkMDZlYTVhNzhjMjY0YzE5In0sImlhdCI6MTUzNzE3Mjg4NCwiZXhwIjoxNTM3MTc2NDg0LCJpc3MiOiJodHRwczovL2lhbS5zdGFnZTEuYmx1ZW1peC5uZXQvaWRlbnRpdHkiLCJncmFudF90eXBlIjoidXJuOmlibTpwYXJhbXM6b2F1dGg6Z3JhbnQtdHlwZTpwYXNzY29kZSIsInNjb3BlIjoiaWJtIG9wZW5pZCIsImNsaWVudF9pZCI6ImJ4IiwiYWNyIjoxLCJhbXIiOlsicHdkIl19.c4vLPzhvvNZLjaLy7znDa37qV4o-yuGmSKmJoQKrEQNZU8IC0NIjxwSo7W9kb0pDi3Yf_03_9ufTTGNfjtltzNWycSXjkNgoL-b9_nU61oHdgn0stY1KmNicqyBWfgUU--4xa904QN_QjRHBaUBeJf3XWEphPIMoF7mZeOxEZLnCMcQXSz9pImCMiP4SNT38cHLiI90Yx01rM7hpteepWULh5MYh-B2V03Gkgxfqvv951HF1LDg6eT4Q9in11laTQKtKuomripUju_4GIIjORVYw9NaAVKIJ9lKrPX0SKPhStsa59qGsC_7Uersms5EY1W1VbZVqOZPJbtp6tVf-Lw
  ```
  {: codeblock}

</br>
</br>


## Idiomas soportados
{: #languages}

Puede utilizar <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/updateLocalization" target="_blank">las API de gestión de idioma <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> para definir el idioma en el que se pueden escribir los mensajes de usuario. Sin embargo, solo el idioma inglés está disponible desde un principio. Usted es el responsable de la traducción de los mensajes. Una vez establecida la configuración con la API, se actualiza la interfaz gráfica de usuario, de forma que pueda modificar el texto de plantilla.
{: shortdesc}

<table>
  <col width="20%">
  <col width="25%">
  <col width="35%">
  <tr>
    <th>Código</th>
    <th>Idioma</th>
    <th>región</th>
  </tr>
  <tr>
    <td><code>af-ZA</code></td>
    <td>Afrikáans</td>
    <td>Sudáfrica</td>
  </tr>
  <tr>
    <td><code>sq-AL</code></td>
    <td>Albanés</td>
    <td>Albania</td>
  </tr>
  <tr>
    <td><code>am-ET</code></td>
    <td>Amhárico</td>
    <td>Etiopía</td>
  </tr>
  <tr>
    <td><code>ar-DZ</code></td>
    <td>Árabe</td>
    <td>Argelia</td>
  </tr>
  <tr>
    <td><code>ar-BH</code></td>
    <td>Árabe</td>
    <td>Baréin</td>
  </tr>
  <tr>
    <td><code>ar-EG</code></td>
    <td>Árabe</td>
    <td>Egipto</td>
  </tr>
  <tr>
    <td><code>ar-IQ</code></td>
    <td>Árabe</td>
    <td>Irak</td>
  </tr>
  <tr>
    <td><code>ar-JO</code></td>
    <td>Árabe</td>
    <td>Jordania</td>
  </tr>
  <tr>
    <td><code>ar-KW</code></td>
    <td>Árabe</td>
    <td>Kuwait</td>
  </tr>
  <tr>
    <td><code>ar-LB</code></td>
    <td>Árabe</td>
    <td>Líbano</td>
  </tr>
  <tr>
    <td><code>ar-LY</code></td>
    <td>Árabe</td>
    <td>Libia</td>
  </tr>
  <tr>
    <td><code>ar-MR</code></td>
    <td>Árabe</td>
    <td>Mauritania</td>
  </tr>
  <tr>
    <td><code>ar-MA</code></td>
    <td>Árabe</td>
    <td>Marruecos</td>
  </tr>
  <tr>
    <td><code>ar-OM</code></td>
    <td>Árabe</td>
    <td>Omán</td>
  </tr>
  <tr>
    <td><code>ar-QA</code></td>
    <td>Árabe</td>
    <td>Qatar</td>
  </tr>
  <tr>
    <td><code>ar-SA</code></td>
    <td>Árabe</td>
    <td>Arabia Saudí</td>
  </tr>
  <tr>
    <td><code>ar-SY</code></td>
    <td>Árabe</td>
    <td>Siria</td>
  </tr>
  <tr>
    <td><code>ar-YE</code></td>
    <td>Árabe</td>
    <td>Túnez</td>
  </tr>
  <tr>
    <td><code>ar-AE</code></td>
    <td>Árabe</td>
    <td>Emiratos Árabes Unidos</td>
  </tr>
  <tr>
    <td><code>ar-YE</code></td>
    <td>Árabe</td>
    <td>Yemen</td>
  </tr>
  <tr>
    <td><code>hy-AM</code></td>
    <td>Armenio</td>
    <td>Armenia</td>
  </tr>
  <tr>
    <td><code>as-IN</code></td>
    <td>Asamés</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>az-AZ</code></td>
    <td>Azerí</td>
    <td>Azerbaiyán</td>
  </tr>
  <tr>
    <td><code>eu-ES</code></td>
    <td>Euskera</td>
    <td>España</td>
  </tr>
  <tr>
    <td><code>be-BY</code></td>
    <td>Bielorruso</td>
    <td>Bielorrusia</td>
  </tr>
  <tr>
    <td><code>bn-BD</code></td>
    <td>Bengalí</td>
    <td>Bangladesh</td>
  </tr>
  <tr>
    <td><code>be-BY</code></td>
    <td>Bielorruso</td>
    <td>Bielorrusia</td>
  </tr>
  <tr>
    <td><code>bn-BD</code></td>
    <td>Bengalí</td>
    <td>Bangladesh</td>
  </tr>
  <tr>
    <td><code>bn-IN</code></td>
    <td>Bengalí</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>bs-Latn-BA</code></td>
    <td>Bosnio</td>
    <td>Bosnia</td>
  </tr>
  <tr>
    <td><code>bg-BG</code></td>
    <td>Búlgaro</td>
    <td>Bulgaria</td>
  </tr>
  <tr>
    <td><code>my-MM</code></td>
    <td>Birmano</td>
    <td>Myanmar</td>
  </tr>
  <tr>
    <td><code>ca-ES</code></td>
    <td>Catalán</td>
    <td>España</td>
  </tr>
  <tr>
    <td><code>zh-Hans-CN</code></td>
    <td>Chino simplificado</td>
    <td>China</td>
  </tr>
  <tr>
    <td><code>zh-Hans-SG</code></td>
    <td>Chino simplificado</td>
    <td>Singapur</td>
  </tr>
  <tr>
    <td><code>zh-Hant-HK</code></td>
    <td>Chino tradicional</td>
    <td>Hong Kong R.A.E. de China</td>
  </tr>
  <tr>
    <td><code>zh-Hant-MO</code></td>
    <td>Chino tradicional</td>
    <td>Macao</td>
  </tr>
  <tr>
    <td><code>zh-Hant-TW</code></td>
    <td>Chino tradicional</td>
    <td>Taiwán</td>
  </tr>
  <tr>
    <td><code>hr-HR</code></td>
    <td>Croata</td>
    <td>Croacia</td>
  </tr>
  <tr>
    <td><code>cs-CZ</code></td>
    <td>Checo</td>
    <td>República Checa</td>
  </tr>
  <tr>
    <td><code>da-DK</code></td>
    <td>Danés</td>
    <td>Dinamarca</td>
  </tr>
  <tr>
    <td><code>nl-BE</code></td>
    <td>Holandés</td>
    <td>Bélgica</td>
  </tr>
  <tr>
    <td><code>nl-NL</code></td>
    <td>Holandés</td>
    <td>Países Bajos</td>
  </tr>
  <tr>
    <td><code>en-AU</code></td>
    <td>Inglés</td>
    <td>Australia</td>
  </tr>
  <tr>
    <td><code>eu-BE</code></td>
    <td>Inglés</td>
    <td>Bélgica</td>
  </tr>
  <tr>
    <td><code>en-CM</code></td>
    <td>Inglés</td>
    <td>Camerún</td>
  </tr>
  <tr>
    <td><code>eu-CA</code></td>
    <td>Inglés</td>
    <td>Canadá</td>
  </tr>
  <tr>
    <td><code>en-GH</code></td>
    <td>Inglés</td>
    <td>Ghana</td>
  </tr>
  <tr>
    <td><code>eu-HK</code></td>
    <td>Inglés</td>
    <td>Hong Kong R.A.E. de China</td>
  </tr>
  <tr>
    <td><code>en-IN</code></td>
    <td>Inglés</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>en-IE</code></td>
    <td>Inglés</td>
    <td>Irlanda</td>
  </tr>
  <tr>
    <td><code>en-KE</code></td>
    <td>Inglés</td>
    <td>Kenia</td>
  </tr>
  <tr>
    <td><code>en-MU</code></td>
    <td>Inglés</td>
    <td>Mauricio</td>
  </tr>
  <tr>
    <td><code>en-NZ</code></td>
    <td>Inglés</td>
    <td>Nueva Zelanda</td>
  </tr>
  <tr>
    <td><code>en-NG</code></td>
    <td>Inglés</td>
    <td>Nigeria</td>
  </tr>
  <tr>
    <td><code>en-PH</code></td>
    <td>Inglés</td>
    <td>Filipinas</td>
  </tr>
  <tr>
    <td><code>en-SG</code></td>
    <td>Inglés</td>
    <td>Singapur</td>
  </tr>
  <tr>
    <td><code>en-ZA</code></td>
    <td>Inglés</td>
    <td>Sudáfrica</td>
  </tr>
  <tr>
    <td><code>en-TZ</code></td>
    <td>Inglés</td>
    <td>Tanzania</td>
  </tr>
  <tr>
    <td><code>en-GB</code></td>
    <td>Inglés</td>
    <td>Reino Unido</td>
  </tr>
  <tr>
    <td><code>en-US</code></td>
    <td>Inglés</td>
    <td>Estados Unidos</td>
  </tr>
  <tr>
    <td><code>en-ZM</code></td>
    <td>Inglés</td>
    <td>Zambia</td>
  </tr>
  <tr>
    <td><code>en</code></td>
    <td>Inglés</td>
    <td> </td>
  </tr>
  <tr>
    <td><code>et-EE</code></td>
    <td>Estonio</td>
    <td>Estonia</td>
  </tr>
  <tr>
    <td><code>fil-PH</code></td>
    <td>Filipino</td>
    <td>Filipinas</td>
  </tr>
  <tr>
    <td><code>fi-FI</code></td>
    <td>Finés</td>
    <td>Finlandia</td>
  </tr>
  <tr>
    <td><code>fr-DZ</code></td>
    <td>Francés</td>
    <td>Argelia</td>
  </tr>
  <tr>
    <td><code>fr-CM</code></td>
    <td>Francés</td>
    <td>Camerún</td>
  </tr>
  <tr>
    <td><code>fr-CD</code></td>
    <td>Francés</td>
    <td>República Democrática del Congo</td>
  </tr>
  <tr>
    <td><code>fr-BE</code></td>
    <td>Francés</td>
    <td>Bélgica</td>
  </tr>
  <tr>
    <td><code>fr-CA</code></td>
    <td>Francés</td>
    <td>Canadá</td>
  </tr>
  <tr>
    <td><code>fr-FR</code></td>
    <td>Francés</td>
    <td>Francia</td>
  </tr>
  <tr>
    <td><code>fr-CI</code></td>
    <td>Francés</td>
    <td>Costa de Marfil (Côte d’Ivoire)</td>
  </tr>
  <tr>
    <td><code>fr-LU</code></td>
    <td>Francés</td>
    <td>Luxemburgo</td>
  </tr>
  <tr>
    <td><code>fr-MR</code></td>
    <td>Francés</td>
    <td>Mauritania</td>
  </tr>
  <tr>
    <td><code>fr-MU</code></td>
    <td>Francés</td>
    <td>Mauricio</td>
  </tr>
  <tr>
    <td><code>fr-MA</code></td>
    <td>Francés</td>
    <td>Marruecos</td>
  </tr>
  <tr>
    <td><code>fr-SN</code></td>
    <td>Francés</td>
    <td>Senegal</td>
  </tr>
  <tr>
    <td><code>fr-CH</code></td>
    <td>Francés</td>
    <td>Suiza</td>
  </tr>
  <tr>
    <td><code>fr-TN</code></td>
    <td>Francés</td>
    <td>Túnez</td>
  </tr>
  <tr>
    <td><code>gl-ES</code></td>
    <td>Gallego</td>
    <td>España</td>
  </tr>
  <tr>
    <td><code>lg-UG</code></td>
    <td>Luganda</td>
    <td>Uganda</td>
  </tr>
  <tr>
    <td><code>ka-GE</code></td>
    <td>Georgiano</td>
    <td>Georgia</td>
  </tr>
  <tr>
    <td><code>de-AT</code></td>
    <td>Alemán</td>
    <td>Austria</td>
  </tr>
  <tr>
    <td><code>de-DE</code></td>
    <td>Alemán</td>
    <td>Alemania</td>
  </tr>
  <tr>
    <td><code>de-LU</code></td>
    <td>Alemán</td>
    <td>Luxemburgo</td>
  </tr>
  <tr>
    <td><code>de-CH</code></td>
    <td>Alemán</td>
    <td>Suiza</td>
  </tr>
  <tr>
    <td><code>el-GR</code></td>
    <td>Griego</td>
    <td>Grecia</td>
  </tr>
  <tr>
    <td><code>gu-IN</code></td>
    <td>Guyaratí</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>ha-NG</code></td>
    <td>Hausa</td>
    <td>Nigeria</td>
  </tr>
  <tr>
    <td><code>he-IL</code></td>
    <td>Hebreo</td>
    <td>Israel</td>
  </tr>
  <tr>
    <td><code>hi-IN</code></td>
    <td>Hindi</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>hu-HU</code></td>
    <td>Húngaro</td>
    <td>Hungría</td>
  </tr>
  <tr>
    <td><code>is-IS</code></td>
    <td>Islandés</td>
    <td>Islandia</td>
  </tr>
  <tr>
    <td><code>ig-NG</code></td>
    <td>Igbo</td>
    <td>Nigeria</td>
  </tr>
  <tr>
    <td><code>id-ID</code></td>
    <td>Indonesio</td>
    <td>Indonesia</td>
  </tr>
  <tr>
    <td><code>it-IT</code></td>
    <td>Italiano</td>
    <td>Italia</td>
  </tr>
  <tr>
    <td><code>it-CH</code></td>
    <td>Italiano</td>
    <td>Suiza</td>
  </tr>
  <tr>
    <td><code>ja-JP</code></td>
    <td>Japonés</td>
    <td>Japón</td>
  </tr>
  <tr>
    <td><code>kn-IN</code></td>
    <td>Canarés</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>kk-KZ</code></td>
    <td>Kazajo</td>
    <td>Kazajistán</td>
  </tr>
  <tr>
    <td><code>km-KH</code></td>
    <td>Jemer</td>
    <td>Camboya</td>
  </tr>
  <tr>
    <td><code>rw-RW</code></td>
    <td>Ruandés</td>
    <td>Ruanda</td>
  </tr>
  <tr>
    <td><code>kok-IN</code></td>
    <td>Konkani</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>ko-KR</code></td>
    <td>Coreano</td>
    <td>Corea del Sur</td>
  </tr>
  <tr>
    <td><code>lo-LA</code></td>
    <td>Lituano</td>
    <td>Lituania</td>
  </tr>
  <tr>
    <td><code>lv-LV</code></td>
    <td>Letón</td>
    <td>Letonia</td>
  </tr>
  <tr>
    <td><code>lt-LT</code></td>
    <td>Jemer</td>
    <td>Camboya</td>
  </tr>
  <tr>
    <td><code>mk-MK</code></td>
    <td>Macedonio</td>
    <td>Macedonia</td>
  </tr>
  <tr>
    <td><code>ms-Latn-MY</code></td>
    <td>Malayo latino</td>
    <td>Malasia</td>
  </tr>
  <tr>
    <td><code>ml-IN</code></td>
    <td>Malayalam</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>mt-MT</code></td>
    <td>Maltés</td>
    <td>Malta</td>
  </tr>
  <tr>
    <td><code>mr-IN</code></td>
    <td>Maratí</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>mn-Cyrl-MN</code></td>
    <td>Mongol cirílico</td>
    <td>Mongolia</td>
  </tr>
  <tr>
    <td><code>ne-IN</code></td>
    <td>Nepalí</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>ne-NP</code></td>
    <td>Nepalí</td>
    <td>Nepal</td>
  </tr>
  <tr>
    <td><code>nb-NO</code></td>
    <td>Noruego bokmål</td>
    <td>Noruega</td>
  </tr>
  <tr>
    <td><code>nn-NO</code></td>
    <td>Noruego nynorsk</td>
    <td>Noruega</td>
  </tr>
  <tr>
    <td><code>or-IN</code></td>
    <td>Oriya (Odia)</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>om-ET</code></td>
    <td>Oromo</td>
    <td>Etiopía</td>
  </tr>
  <tr>
    <td><code>pl-PL</code></td>
    <td>Polaco</td>
    <td>Polonia</td>
  </tr>
  <tr>
    <td><code>pt-AO</code></td>
    <td>Portugués</td>
    <td>Angola</td>
  </tr>
  <tr>
    <td><code>pt-BR</code></td>
    <td>Portugués</td>
    <td>Brasil</td>
  </tr>
  <tr>
    <td><code>pt-MO</code></td>
    <td>Portugués</td>
    <td>Macao</td>
  </tr>
  <tr>
    <td><code>pt-MZ</code></td>
    <td>Portugués</td>
    <td>Mozambique</td>
  </tr>
  <tr>
    <td><code>pt-PT</code></td>
    <td>Portugués</td>
    <td>Portugal</td>
  </tr>
  <tr>
    <td><code>pa-IN</code></td>
    <td>Panyabí</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>ro-RO</code></td>
    <td>Rumano</td>
    <td>Rumanía</td>
  </tr>
  <tr>
    <td><code>ru-RU</code></td>
    <td>Ruso</td>
    <td>Rusia</td>
  </tr>
  <tr>
    <td><code>sr-Cyrl-RS</code></td>
    <td>Serbio cirílico</td>
    <td>Serbia</td>
  </tr>
  <tr>
    <td><code>sr-Latn-ME</code></td>
    <td>Serbio latino</td>
    <td>Montenegro</td>
  </tr>
  <tr>
    <td><code>sr-Latn-RS</code></td>
    <td>Serbio latino</td>
    <td>Serbia</td>
  </tr>
  <tr>
    <td><code>si-LK</code></td>
    <td>Cingalés</td>
    <td>Sri Lanka</td>
  </tr>
  <tr>
    <td><code>sk-SK</code></td>
    <td>Eslovaco</td>
    <td>Eslovaquia</td>
  </tr>
  <tr>
    <td><code>sl-SI</code></td>
    <td>Esloveno</td>
    <td>Eslovenia</td>
  </tr>
  <tr>
    <td><code>es-AR</code></td>
    <td>Español</td>
    <td>Argentina</td>
  </tr>
  <tr>
    <td><code>es-BO</code></td>
    <td>Español</td>
    <td>Bolivia</td>
  </tr>
  <tr>
    <td><code>es-CL</code></td>
    <td>Español</td>
    <td>Chile</td>
  </tr>
  <tr>
    <td><code>es-CO</code></td>
    <td>Español</td>
    <td>Colombia</td>
  </tr>
  <tr>
    <td><code>es-CR</code></td>
    <td>Español</td>
    <td>Costa Rica</td>
  </tr>
  <tr>
    <td><code>es-DO</code></td>
    <td>Español</td>
    <td>República Dominicana</td>
  </tr>
  <tr>
    <td><code>es-EC</code></td>
    <td>Español</td>
    <td>Ecuador</td>
  </tr>
  <tr>
    <td><code>es-SV</code></td>
    <td>Español</td>
    <td>El Salvador</td>
  </tr>
  <tr>
    <td><code>es-GT</code></td>
    <td>Español</td>
    <td>Guatemala</td>
  </tr>
  <tr>
    <td><code>es-HN</code></td>
    <td>Español</td>
    <td>Honduras</td>
  </tr>
  <tr>
    <td><code>es-MX</code></td>
    <td>Español</td>
    <td>México</td>
  </tr>
  <tr>
    <td><code>es-NI</code></td>
    <td>Español</td>
    <td>Nicaragua</td>
  </tr>
  <tr>
    <td><code>es-PA</code></td>
    <td>Español</td>
    <td>Panamá</td>
  </tr>
  <tr>
    <td><code>es-PY</code></td>
    <td>Español</td>
    <td>Paraguay</td>
  </tr>
  <tr>
    <td><code>es-PE</code></td>
    <td>Español</td>
    <td>Perú</td>
  </tr>
  <tr>
    <td><code>es-PR</code></td>
    <td>Español</td>
    <td>Puerto Rico</td>
  </tr>
  <tr>
    <td><code>es-ES</code></td>
    <td>Español</td>
    <td>España</td>
  </tr>
  <tr>
    <td><code>es-US</code></td>
    <td>Español</td>
    <td>Estados Unidos</td>
  </tr>
  <tr>
    <td><code>es-UY</code></td>
    <td>Español</td>
    <td>Uruguay</td>
  </tr>
  <tr>
    <td><code>es-VE</code></td>
    <td>Español</td>
    <td>Venezuela</td>
  </tr>
  <tr>
    <td><code>sw-KE</code></td>
    <td>Suajili</td>
    <td>Kenia</td>
  </tr>
  <tr>
    <td><code>sw-TZ</code></td>
    <td>Suajili</td>
    <td>Tanzania</td>
  </tr>
  <tr>
    <td><code>sv-SE</code></td>
    <td>Sueco</td>
    <td>Suecia</td>
  </tr>
  <tr>
    <td><code>ta-IN</code></td>
    <td>Tamil</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>te-IN</code></td>
    <td>Télugu</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>th-TH</code></td>
    <td>Tailandés</td>
    <td>Tailandia</td>
  </tr>
  <tr>
    <td><code>tr-TR</code></td>
    <td>Turco</td>
    <td>Turquía</td>
  </tr>
  <tr>
    <td><code>uk-UA</code></td>
    <td>Ucraniano</td>
    <td>Ucrania</td>
  </tr>
  <tr>
    <td><code>ur-IN</code></td>
    <td>Urdu</td>
    <td>India</td>
  </tr>
  <tr>
    <td><code>ur-PK</code></td>
    <td>Urdu</td>
    <td>Pakistán</td>
  </tr>
  <tr>
    <td><code>uz-Cyrl-UZ</code></td>
    <td>Uzbeko cirílico</td>
    <td>Uzbekistán</td>
  </tr>
  <tr>
    <td><code>uz-Latn-UZ</code></td>
    <td>Uzbeko latino</td>
    <td>Uzbekistán</td>
  </tr>
  <tr>
    <td><code>vi-VN</code></td>
    <td>Vietnamita</td>
    <td>Vietnam</td>
  </tr>
  <tr>
    <td><code>cy-GB</code></td>
    <td>Galés</td>
    <td>Reino Unido</td>
  </tr>
  <tr>
    <td><code>yo-NG</code></td>
    <td>Yoruba</td>
    <td>Nigeria</td>
  </tr>
  <tr>
    <td><code>zu-ZA</code></td>
    <td>Zulú</td>
    <td>Sudáfrica</td>
  </tr>
</table>
