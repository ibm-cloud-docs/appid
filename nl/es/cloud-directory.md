---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Configuración del directorio en la nube
{: #cd}

Los usuarios pueden registrarse e iniciar la sesión en sus apps web y móviles mediante un correo electrónico y una contraseña. Un directorio en la nube es un registro de usuarios que está mantenido en la nube. Cuando un usuario se registra en su app con correo electrónico y contraseña, se le añade al directorio de usuarios. Con esta característica, los usuarios tienen la libertad de gestionar sus propias cuentas dentro de la app.
{: shortdesc}

</br>

## Gestión de los valores de directorio
{: #cd-settings}

Puede configurar las notificaciones y el nivel de control de usuario para su app. La configuración del procesador único puede realizarse rápidamente, tal como se muestra en la siguiente imagen. Estos valores pueden actualizarse en cualquier momento desde el panel de control del servicio.
{: shortdesc}

![Configuración del directorio en la nube](/images/cloud-directory.png)

1. Asegúrese que el directorio en la nube está activado como proveedor de identidad y establezca **Permitir a los usuarios registrarse y restablecer su contraseña** en **Activado**. Si se establece en **Desactivado**, puede seguir agregando usuarios a través de la consola para fines de desarrollo.
2. Configure los detalles de su remitente. Especifique la dirección de correo electrónico desde la que enviará los mensajes, el remitente y a quién pueden responder los usuarios.
  Cuando configure el URL de acción, asegúrese de dejar tiempo suficiente para que un usuario pulse el enlace. El usuario debe verificar su correo electrónico para tener ciertas opciones, como la capacidad de solicitar un restablecimiento de su contraseña.
  {: tip}
3. Determine los tipos de correo electrónico que recibe un usuario y la información del remitente.
4. Con las plantillas proporcionadas, personalice sus mensajes con su marca o con mensajes personalizados. Para obtener más información, consulte [Gestión de mensajes](/docs/services/appid/cloud-directory.html#cd-messages).
5. Vea los usuarios que se han registrado en su app en el separador **Usuarios** de la GUI.

</br>

## Gestión de mensajes
{: #cd-messages}

Una plantilla es un ejemplo de un mensaje de correo electrónico que podría enviar a sus usuarios. Puede personalizarla actualizando el contenido y el diseño del mensaje. Puede definir estos mensajes en **Activados** o **Desactivados** en el separador de valores de directorio.
{: shortdesc}

1. Seleccione un **Tipo de mensaje**.
2. Personalice el mensaje cambiando el contenido y el diseño. Puede utilizar parámetros para personalizar sus mensajes. No se olvide de guardar los cambios.

### Tipos de mensajes

Puede enviar varios tipos de mensajes a sus usuarios. Puede elegir enviar el mensaje de ejemplo que está programado en la IU o puede personalizar el contenido para conseguir una experiencia más personal con la app.

<dl>
  <dt>Bienvenido</dt>
    <dd><p>Después de haberse registrado, puede recibir a un usuario a la aplicación por correo electrónico. Para dar la bienvenida y retener a los usuarios, haga su mensaje tan interactivo como sea posible.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> Todos los parámetros de mensaje</th>
      </thead>
      <tbody>
        <tr>
          <td> %{display.logo} </td>
          <td> Muestra la imagen que ha configurado para su widget de inicio de sesión. </td>
        </tr>
        <tr>
          <td> %{user.displayName} </td>
          <td> Muestra el nombre de pantalla que elige un usuario para utilizar al interactuar con la app. </td>
        </tr>
        <tr>
          <td> %{user.email} </td>
          <td> Muestra la dirección de correo electrónico registrada del usuario. </td>
        </tr>
        <tr>
          <td> %{user.firstName} </td>
          <td> Muestra el nombre especificado del usuario. </td>
        </tr>
        <tr>
          <td> %{user.formattedName} </td>
          <td> Muestra el nombre completo del usuario. </td>
        </tr>
        <tr>
          <td> %{user.lastName} </td>
          <td> Muestra el apellido especificado del usuario. </td>
        </tr>
      </tbody>
    </table>
    <p>**Nota**: Si un usuario no proporciona la información extraída por el parámetro, aparecerá en blanco.</p></dd>
  <dt>Contraseña olvidada</dt>
    <dd><p>Un usuario puede pedir el restablecimiento de contraseña si la ha olvidado o si necesita actualizarla por cualquier motivo. Puede personalizar la respuesta por correo electrónico a su solicitud. Cuando un usuario solicita un cambio, su contraseña sigue siendo la misma hasta que pulsa en el enlace en este correo electrónico.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> Parámetros de cambio de contraseña </th>
      </thead>
      <tbody>
        <tr>
          <td> %{linkExpiration.hours} </td>
          <td> Muestra el número de horas que es válido el enlace. </td>
        </tr>
        <tr>
          <td> %{linkExpiration.minutes} </td>
          <td> Muestra el número de minutos que es válido el enlace. </td>
        </tr>
        <tr>
          <td> %{resetPassword.code} </td>
          <td> Muestra una clave de acceso de un único uso como parte del URL. Esto significa que cada persona tendría un código diferente. Ejemplo: <code>https://appid-wfm.bluemix.net/verify/6574839563478 </code> </td>
        </tr>
        <tr>
          <td> %{resetPassword.link} </td>
          <td> Muestra el enlace que pulsa un usuario para restablecer su contraseña. </td>
        </tr>
       </tbody>
    </table>
    </dd>
  <dt>Verificación</dt>
    <dd><p>Puede solicitar que el usuario verifique su cuenta por correo electrónico. Al solicitar una verificación, se limita el número de cuentas falsas que pueden registrarse en su app. Puede restringir el acceso a su app hasta que el usuario haya verificado su correo electrónico, o utilizarlo como forma de gestionar los usuarios para los que ha creado perfiles.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> Parámetros de mensaje de verificación </th>
      </thead>
      <tbody>
        <tr>
          <td> %{linkExpiration.hours} </td>
          <td> Muestra el número de horas que es válido el enlace. </td>
        </tr>
        <tr>
          <td> %{linkExpiration.minutes} </td>
          <td> Muestra el número de minutos que es válido el enlace. </td>
        </tr>
        <tr>
          <td> %{verify.code} </td>
          <td> Muestra un URL de verificación de un único uso. </td>
        </tr>
        <tr>
          <td> %{verify.link} </td>
          <td> Muestra el URL de acción que especificó en los valores. </td>
        </tr>
      </tbody>
    </table>
    </dd>
  <dt>Cambio de contraseña</dt>
    <dd><p>Puede hacer saber al usuario cuando se ha actualizado su contraseña. Esto es útil si no ha solicitado el cambio de contraseña. Pueden llevar a cabo los pasos apropiados para volver a asegurar su cuenta.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> Parámetros de cambio de contraseña </th>
      </thead>
      <tbody>
        <tr>
          <td> %{passwordChangeInfo.time} </td>
          <td> Muestra la hora en que entra en vigor la nueva contraseña. </td>
        </tr>
        <tr>
          <td> %{passwordChangeInfo.ipAddress} </td>
          <td> Muestra la dirección IP desde la que se ha solicitado el cambio de contraseña. </td>
        </tr>
      </tbody>
    </table>
    </dd>
</dl>
</br>
**NOTA**: {{site.data.keyword.appid_short_notm}} utiliza <a href="https://www.sendgrid.com" target="_blank">SendGrid <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> como servicio de entrega de correo. Todos los correos electrónicos se envían con una sola cuenta de SendGrid.

</br>
## Pasos siguientes
Ahora que ha configurado el directorio en la nube, ya está listo para añadir el código del widget de inicio de sesión en el código de su app. Pulse en un icono de lenguaje de SDK en la siguiente imagen para ver lo que debe hacer.
{: shortdesc}

<img usemap="#options-map" border="0" class="image" id="options" src="images/options.png" width="750" alt="Pulse un icono del idioma SDK para empezar con el directorio de nube en sus apps." style="width:750px;" />
<map name="options-map" id="options-map">
<area href="login-widget.html#branded-ui-android" alt="Gestión de la experiencia de inicio de sesión con el SDK de Android" shape="rect" coords="187, 6, 305, 120" />
<area href="login-widget.html#branded-ui-ios-swift" alt="Gestión de la experiencia de inicio de sesión con el SDK de iOS Swift." shape="rect" coords="333, 6, 448, 125" />
<area href="login-widget.html#branded-ui-nodejs" alt="Gestión de la experiencia de inicio de sesión con el SDK de Node.js." shape="rect" coords="472, 7, 590, 121" />
</map>
