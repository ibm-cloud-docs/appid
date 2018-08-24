---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-09"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Configuración del directorio en la nube
{: #cd}

Los usuarios pueden registrarse e iniciar la sesión en sus apps web y móviles mediante un correo electrónico o un nombre de usuario y una contraseña. Un directorio en la nube es un registro de usuarios que está mantenido en la nube. Cuando un usuario se registra en su app, se le añade al directorio de usuarios. Con esta característica, los usuarios tienen la libertad de gestionar sus propias cuentas dentro de la app.
{: shortdesc}

</br>

## Gestión de los valores de directorio
{: #cd-settings}

Puede configurar las notificaciones y el nivel de control de usuario para su app. La configuración del procesador único puede realizarse rápidamente, tal como se muestra en la siguiente imagen. Estos valores pueden actualizarse en cualquier momento desde el panel de control del servicio.
{: shortdesc}


![Configuración del directorio en la nube](/images/cloud-directory.png)
Figura. Guía de configuración del Directorio en la nube


1. Asegúrese de que el Directorio en la nube esté activado como proveedor de identidad y establezca **Permitir a los usuarios registrarse y restablecer su contraseña** en **Activado**. Si se establece en **Desactivado**, puede seguir agregando usuarios a través de la consola para fines de desarrollo.
2. Seleccione si los usuarios se van a autenticar con un nombre de usuario especificado o con un correo electrónico. Este campo se utiliza para los flujos de registro, de inicio de sesión y de contraseña olvidada. Si permite a los usuarios iniciar sesión con un nombre de usuario y una contraseña, el nombre de usuario debe tener al menos 8 caracteres y no puede contener espacios, comas ni barras inclinadas. **Nota:** Puede cambiar de opción sólo si no hay usuarios en el Directorio en la nube.
3. Configure los detalles de su remitente. Especifique la dirección de correo electrónico desde la que enviará los mensajes, el remitente y a quién pueden responder los usuarios.
  Cuando configure el URL de acción, asegúrese de dejar tiempo suficiente para que un usuario pulse el enlace. El usuario debe verificar su correo electrónico para tener ciertas opciones, como la capacidad de solicitar un restablecimiento de su contraseña.
  {: tip}
4. Determine los tipos de correo electrónico que recibe un usuario y la información del remitente.
5. Con las plantillas proporcionadas, personalice sus mensajes con su marca o con mensajes personalizados. Para obtener más información, consulte [Gestión de mensajes](/docs/services/appid/cloud-directory.html#cd-messages).
6. Vea los usuarios que se han registrado en su app en el separador **Usuarios** de la GUI.

Un solo usuario puede intentar iniciar sesión hasta 5 veces en un minuto. Si lo intenta por sexta vez, aparece un error.
{: tip}

</br>

## Gestión de mensajes
{: #cd-messages}

Una plantilla es un ejemplo de un mensaje de correo electrónico que podría enviar a sus usuarios. Puede personalizarla actualizando el contenido y el diseño del mensaje.
{: shortdesc}

1. En el separador **Proveedores de identidad > Directorio en la nube > Valores** del panel de control, establezca los mensajes que desea enviar en **Activado**.

2. Opcional: utilice <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/updateLocalization" target="_blank">las API de gestión de idioma <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> para definir otro idioma que desee utilizar en las plantillas de mensaje. Para obtener una lista de los códigos de idioma que se admiten, consulte [Idiomas admitidos](#languages).

3. Seleccione un **Tipo de mensaje**.

4. Personalice el mensaje cambiando el contenido y el diseño. Puede utilizar parámetros para personalizar sus mensajes. No se olvide de guardar los cambios.

### Tipos de mensajes

Puede enviar varios tipos de mensajes a sus usuarios. Puede elegir enviar el mensaje de ejemplo que está programado en la IU o puede personalizar el contenido para conseguir una experiencia más personal con la app.

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
    </table>
    <p>**Nota**: Si un usuario no proporciona la información extraída por el parámetro, aparecerá en blanco.</p></dd>
  <dt>Contraseña olvidada</dt>
    <dd><p>Un usuario puede pedir el restablecimiento de contraseña si la ha olvidado o si necesita actualizarla por cualquier motivo. Puede personalizar la respuesta por correo electrónico a su solicitud. Cuando un usuario solicita un cambio, su contraseña sigue siendo la misma hasta que pulsa en el enlace en este correo electrónico.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="Icono de más información"/> Parámetros de cambio de contraseña </th>
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
          <td><code>%{resetPassword.code}</code></td>
          <td> Muestra una clave de acceso de un único uso como parte del URL. Esto significa que cada persona tendría un código diferente. Ejemplo: <code>https://appid-wfm.bluemix.net/verify/6574839563478 </code> </td>
        </tr>
        <tr>
          <td><code>%{resetPassword.link}</code></td>
          <td> Muestra el enlace que pulsa un usuario para restablecer su contraseña. </td>
        </tr>
       </tbody>
    </table>
    </dd>
  <dt>Verificación</dt>
    <dd><p>Puede solicitar que el usuario verifique su cuenta por correo electrónico. Al solicitar una verificación, se limita el número de cuentas falsas que pueden registrarse en su app. Puede restringir el acceso a su app hasta que el usuario haya verificado su correo electrónico, o utilizarlo como forma de gestionar los usuarios para los que ha creado perfiles.</p>
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
    </table>
    </dd>
  <dt>Cambio de contraseña</dt>
    <dd><p>Puede hacer saber al usuario cuándo se ha actualizado su contraseña. Esto es útil si no ha solicitado el cambio de contraseña. Pueden llevar a cabo los pasos apropiados para volver a asegurar su cuenta.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="Icono de más información"/> Parámetros de cambio de contraseña </th>
      </thead>
      <tbody>
        <tr>
          <td><code>%{passwordChangeInfo.time}</code></td>
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

## Gestión de la fortaleza de contraseña
{: #strength}

Puede definir los requisitos para las contraseñas que se pueden utilizar con el Directorio en la nube.
{: shortdesc}

Una contraseña segura es difícil o improbable de adivinar ya sea de forma manual o automática. La fortaleza de contraseña se define como una serie de expresión regular.

Estos son algunos ejemplos habituales de fortaleza de contraseña:

- Debe tener al menos 8 caracteres. Expresión regular de ejemplo: `^.{8,}$`
- Debe incluir 1 número, 1 letra minúscula y 1 letra mayúscula. Expresión regular de ejemplo: `^(?:(?=.*\\d)(?=.*[a-z])(?=.*[A-Z]).*)$`
- Debe contener solo letras y números ingleses. Expresión regular de ejemplo: `^[A-Za-z0-9]*$`
- Debe tener al menos 1 carácter exclusivo. Expresión regular de ejemplo: `^(\w)\w*?(?!\1)\w+$`

Debe utilizar <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/set_cloud_directory_password_regex" target="_blank">las API de gestión <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> para definir los requisitos.

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
