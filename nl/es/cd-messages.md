---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-10"

keywords: Authentication, authorization, identity, app security, secure, directory, registry, passwords, languages, lockout

subcollection: appid

---

{:external: target="_blank" .external}
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

# Personalización de mensajes de correo electrónico
{: #cd-types}

Cuando un usuario interactúa con la aplicación, es probable que desee enviar una respuesta o solicitar la verificación. {{site.data.keyword.appid_short_notm}} proporciona plantillas predeterminadas que puede utilizar para estas interacciones. También puede utilizar las plantillas como una guía y personalizar la mensajería para ajustarla a su marca.
{: shortdesc}

{{site.data.keyword.appid_short_notm}} utiliza <a href="https://www.sendgrid.com" target="_blank">SendGrid <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> como servicio de entrega de correo. Todos los correos electrónicos se envían con una sola cuenta de SendGrid.
{: note}

## Plantillas de correo electrónico
{: #cd-messages}

Cuando envía mensajes a los usuarios, puede utilizar cualquier combinación de las plantillas siguientes. O bien, puede editar las plantillas para personalizar el mensaje.
{: shortdesc}

Además de los siguientes tipos de mensajes, también puede aprovechar las plantillas de [SSO](/docs/services/appid?topic=appid-cd-sso#cd-sso) y [MFA](/docs/services/appid?topic=appid-cd-mfa#cd-mfa).
{: tip}

Para una mayor personalización, puede utilizar parámetros en los mensajes. Consulte la tabla siguiente para ver los parámetros que puede utilizar en todos los tipos de mensajes.

<table>
  <tr>
    <th colspan=2><img src="images/idea.png" alt="Icono de más información"/> Todos los parámetros de mensaje </th>
  </tr>
  <tr>
    <td><code>%{display.logo}</code></td>
    <td> Muestra la imagen que ha configurado para su widget de inicio de sesión.</td>
  </tr>
  <tr>
    <td><code>%{user.displayName}</code></td>
    <td> Muestra el nombre de pantalla que elige un usuario para utilizar al interactuar con la app.</td>
  </tr>
  <tr>
    <td><code>%{user.email}</code></td>
    <td> Muestra la dirección de correo electrónico registrada del usuario.</td>
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
</table>


### Correo electrónico: Bienvenido
{: #cd-messages-welcome}

Cuando un usuario se registra en su app, es probable que desee enviarle un mensaje de bienvenida a la app. 
{: shortdesc}

1. Vaya al separador **Plantillas de flujo de trabajo > Correo electrónico de bienvenida** del panel de control de servicio.

2. Establezca la opción **Correo electrónico de bienvenida** en **Habilitado**.

3. Personalice el contenido del mensaje. Puede añadir parámetros e insertar imágenes utilizando la interfaz de usuario. Para cambiar el [idioma](/docs/services/appid?topic=appid-cd-messages#cd-languages) del mensaje, puede utilizar <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">las API de <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> para establecer el idioma. Sin embargo, usted es el responsable del contenido y la traducción del mensaje. Consulte la tabla siguiente para ver la lista de tablas que puede utilizar en este mensaje y todos los demás mensajes que puede enviar. Si un usuario no proporciona la información que extrae el parámetro, aparecerá en blanco.

4. Pulse **Guardar**.


### Correo electrónico: Verificación
{: #cd-messages-verification}

Cuando un usuario se registra en su aplicación mediante su correo electrónico, puede enviarle un correo electrónico que le solicite confirmar su identidad. Al solicitar una verificación, se limita el número de cuentas falsas que pueden registrarse en su app. Puede restringir el acceso a su app hasta que el usuario verifique su correo electrónico, o utilizarlo como forma de gestionar los usuarios para los que ha creado perfiles.
{: shortdesc}

Los usuarios que se añaden manualmente mediante el panel de control de {{site.data.keyword.appid_short_notm}} o la API de creación de usuarios no reciben este correo electrónico automáticamente.
{: note}


1. Vaya al separador **Plantillas de flujo de trabajo > Verificación de correo electrónico** del panel de control de servicio.

2. Establezca la opción **Verificación de correo electrónico** en **Habilitada**.

3. Establezca **Permitir a los usuarios registrarse en la app sin verificar la dirección de correo electrónico primero** en **Sí**. Cuando se establece en sí, los usuarios pueden interactuar con la aplicación después de registrarse, pero antes de verificar su dirección de correo electrónico. El valor predeterminado es no.

4. Personalice el contenido del mensaje. Puede añadir parámetros e insertar imágenes utilizando la interfaz de usuario. Para cambiar el [idioma](/docs/services/appid?topic=appid-cd-messages#cd-languages) del mensaje, puede utilizar <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">las API de <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> para establecer el idioma. Sin embargo, usted es el responsable del contenido y la traducción del mensaje. Consulte la tabla siguiente para ver los distintos parámetros que puede utilizar en el mensaje. Si un usuario no proporciona la información que extrae el parámetro, aparecerá en blanco.

  <table>
    <tr>
      <th colspan=2><img src="images/idea.png" alt="Icono de más información"/> Parámetros de mensaje de verificación</th>
    </tr>
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
  </table>

  También puede utilizar los parámetros de mensaje que se listan en la sección [Mensaje de bienvenida](/docs/services/appid?topic=appid-cd-messages#cd-messages-welcome).
  {: tip}

5. Defina una hora de vencimiento para el URL de acción. El URL de vencimiento es la cantidad de tiempo, en minutos, en la que un usuario debe completar la acción antes de que caduque el enlace de verificación. Este valor también afecta a la cantidad de tiempo que su enlace de restablecimiento de contraseña es válido.
 
6. Especifique un URL para la página que desea visualizar después de que un usuario verifique su correo electrónico en el recuadro **URL de la página de agradecimiento**. Si elige dejar este campo en blanco, se muestra una página predeterminada de {{site.data.keyword.appid_short_notm}}.

7. Pulse **Guardar**. 


### Correo electrónico: Restablecimiento de contraseña
{: #cd-messages-reset}

Cuando un usuario interactúa con la app, es posible que olvide su contraseña o que necesite actualizarla. Puede personalizar la respuesta por correo electrónico a su solicitud. Cuando un usuario solicita un cambio, su contraseña sigue siendo la misma hasta que pulsa en el enlace en este correo electrónico.
{: shortdesc}


1. Vaya al separador **Plantillas de flujo de trabajo > Restablecer contraseña** del panel de control de servicio.

2. Establezca la opción **Correo electrónico de contraseña olvidada** en **Habilitado**.

3. Personalice el contenido del mensaje. Puede añadir parámetros e insertar imágenes utilizando la interfaz de usuario. Para cambiar el [idioma](/docs/services/appid?topic=appid-cd-messages#cd-languages) del mensaje, puede utilizar <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">las API de <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> para establecer el idioma. Sin embargo, usted es el responsable del contenido y la traducción del mensaje. Consulte la tabla siguiente para ver los distintos parámetros que puede utilizar en el mensaje. Si un usuario no proporciona la información que extrae el parámetro, aparecerá en blanco.

  <table>
    <tr>
      <th colspan=2><img src="images/idea.png" alt="Icono de más información"/> Parámetros de contraseña olvidados</th>
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
      <td> Muestra una clave de acceso de un solo uso como parte del URL. Esto significa que cada persona tendría un código diferente. Ejemplo: `https://us-south.appid.cloud.ibm.com/wfm/verify/6574839563478`</td>
    </tr>
    <tr>
      <td><code>%{resetPassword.link}</code></td>
      <td> Muestra el enlace que pulsa un usuario para restablecer su contraseña.</td>
    </tr>
  </table>

  También puede utilizar los parámetros de mensaje que se listan en la sección [Mensaje de bienvenida](/docs/services/appid?topic=appid-cd-messages#cd-messages-welcome).
  {: tip}

4. Defina una hora de vencimiento para el URL de acción. El URL de vencimiento es la cantidad de tiempo, en minutos, en la que un usuario debe completar la acción antes de que caduque el enlace de verificación. Este valor también afecta a la cantidad de tiempo que su enlace de restablecimiento de contraseña es válido.
 
5. Especifique un URL para la página que desea visualizar después de que un usuario verifique su correo electrónico en el recuadro **URL de la página de restablecer contraseña**. Si elige dejar este campo en blanco, se muestra una página predeterminada de {{site.data.keyword.appid_short_notm}}.

6. Pulse **Guardar**.


### Correo electrónico: Cambio de contraseña
{: #cd-messages-password-change}

Puede notificar a un usuario cuando se actualice su contraseña. La notificación es útil si no ha solicitado el cambio de contraseña. Pueden llevar a cabo los pasos apropiados para volver a asegurar su cuenta.
{: shortdesc}

1. Vaya al separador **Plantillas de flujo de trabajo > Cambio de contraseña** del panel de control de servicio.

2. Establezca la opción **Correo electrónico de contraseña cambiada** en **Habilitado**.

3. Personalice el contenido del mensaje. Puede añadir parámetros e insertar imágenes utilizando la interfaz de usuario. Para cambiar el [idioma](/docs/services/appid?topic=appid-cd-messages#cd-languages) del mensaje, puede utilizar <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">las API de <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> para establecer el idioma. Sin embargo, usted es el responsable del contenido y la traducción del mensaje. Consulte la tabla siguiente para ver los distintos parámetros que puede utilizar en el mensaje. Si un usuario no proporciona la información que extrae el parámetro, aparecerá en blanco.

  <table>
    <tr>
      <th colspan=2><img src="images/idea.png" alt="Icono de más información"/> Parámetros de cambio de contraseña</th>
    </tr>
    <tr>
      <td><code>%{passwordChangeInfo.time}</code></td>
      <td> Muestra la hora en que entra en vigor la nueva contraseña. </td>
    </tr>
    <tr>
      <td><code>%{passwordChangeInfo.ipAddress}</code></td>
      <td> Muestra la dirección IP desde la que se ha solicitado el cambio de contraseña. </td>
    </tr>
  </table>

  También puede utilizar los parámetros de mensaje que se listan en la sección [Mensaje de bienvenida](/docs/services/appid?topic=appid-cd-messages#cd-messages-welcome).
  {: tip}

4. Pulse **Guardar**.




## Utilización de un remitente de correo electrónico personalizado
{: #cd-custom-email}

Con {{site.data.keyword.appid_short_notm}}, puede definir un punto de extensión personalizado para que envíe mensajes de correo electrónico del directorio en la nube. Al definir un punto de extensión, tiene el control completo de cómo se envían los correos electrónicos y puede utilizar su propio nombre de dominio. De forma predeterminada, {{site.data.keyword.appid_short_notm}} utiliza <a href="https://www.sendgrid.com" target="_blank">SendGrid <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> como servicio de entrega de correo.
 {: shortdesc}

Es posible que quiera utilizar un remitente de correo personalizado por las siguientes razones:

- **Dominio personalizado**
Mediante la configuración de un distribuidor de correo electrónico tendrá un control completo sobre cómo se envían los mensajes de correo electrónico. Más concretamente, puede personalizar el dominio de correo electrónico, que puede reducir las posibilidades de que un correo electrónico se filtre como spam. También puede mejorar aún más la experiencia de marca para los usuarios de app.

- **Conocimientos y resolución de problemas**
Obtenga conocimientos del proveedor de correo electrónico como, por ejemplo, el número de personas que han abierto los correos electrónicos o los mensajes que no se han entregado. Puesto que puede realizar un seguimiento de los mensajes individuales y ver las estadísticas globales, esto puede ayudarle a resolver problemas.

Una vez configurado el punto de extensión, {{site.data.keyword.appid_short_notm}} lo llamará siempre que deba enviarse un mensaje de correo electrónico. El punto de extensión contiene toda la información sobre el mensaje, incluido el contenido final del cuerpo del correo electrónico.



### Configuración del remitente personalizado
{: #cd-messages-configure-custom-sender}

Para configurar el remitente de correo electrónico personalizado, debe utilizar la <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.set_cloud_directory_email_dispatcher" target="_blank">API de gestión</a> del directorio en la nube.


1. Proporcione el URL. Además, puede proporcionar información de autorización. Los tipos de autorización soportados son: `Autorización básica` o `valor de cabecera de autorización constante`.

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

3. El cuerpo que envía {{site.data.keyword.appid_short_notm}} tiene el formato siguiente: `{"jws": "jws-format-string"}`. Una vez haya descodificado y verificado la carga útil, el contenido será una serie JSON.

  ```
  {
    "tenant": "tenant-id",
      "iss" : "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61", 
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

  <table>
    <tr>
      <th>Variable</th>
      <th>Descripción</th>
    </tr>
    <tr>
      <td><code>tenant</code></td>
      <td>El ID de arrendatario de la instancia de {{site.data.keyword.appid_short_notm}}.</td>
    </tr>
    <tr>
      <td><code>iat</code></td>
      <td>La indicación de fecha y hora de cuando se envió el mensaje.</td>
    </tr>
    <tr>
      <td><code>iss</code></td>
      <td>El principio, o la instancia de {{site.data.keyword.appid_short_notm}}, que ha emitido la señal JWS.</td>
    </tr>
    <tr>
      <td><code>jti</code></td>
      <td>El ID de transacción exclusivo.</td>
    </tr>
    <tr>
      <td><code>message: to</code></td>
      <td>La dirección de correo electrónico del destinatario del mensaje.</td>
    </tr>
    <tr>
      <td><code>message: from</code> </br><code>name</code> </br><code>address</code></td>
      <td></br>El nombre del remitente del mensaje. </br>La dirección de correo electrónico del remitente.</td>
    </tr>
    <tr>
      <td><code>Opcional: message: reply to</code></br><code>name</code></br><code>address</code></td>
      <td></br>El nombre que se adjunta a la dirección de correo electrónico de respuesta.</br>La dirección de correo electrónico a la que puede responder un usuario.</td>
    </tr>
  </table>

  Puede comprobar que la solicitud se ha realizado correctamente comprobando el código de estado de respuesta. Siempre que el rango sea de 200 a 299, se habrá realizado correctamente. Si recibe cualquier otra respuesta, intente volver a realizar la solicitud.
  {: tip}

4. Cada carga útil de HTTP que se envía desde {{site.data.keyword.appid_short_notm}} se firma de forma automática de acuerdo con el estándar JWS utilizando un par de claves asimétricas.
Para cada instancia de {{site.data.keyword.appid_short_notm}}, se generan una clave pública y privada que no se comparten con otras instancias. La clave privada se utiliza para firmar la carga útil de HTTP y puede utilizar la clave pública para verificar que {{site.data.keyword.appid_short_notm}} genera la carga útil y que no la altera ningún <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#!/Authorization_Server_V4/publicKeys" target="_blank">punto final de clave público</a> de terceros.

5. Código de ejemplo para el punto de extensión (JavaScript).
  ```
  const sgMail = require('@sendgrid/mail');
  const {promisify} = require('bluebird');
  const request = promisify(require('request'));
  const jwtVerify = promisify(require('jsonwebtoken').verify);
  const jwtDecode = require('jsonwebtoken').decode;
  const jwkToPem = require('jwk-to-pem');

  async function obtainPublicKeys() {
  	// El ID de arrendatario de la instancia de {{site.data.keyword.appid_short_notm}}
  	const tenantId = '<TENANT-ID>';

  	// Enviar una solicitud a un punto final de claves públicas de {{site.data.keyword.appid_short_notm}}
  	const keysOptions = {
  		method: 'GET',
  		url: `https://<REGION>.appid.cloud.ibm.com/oauth/v4/${tenantId}/publickeys`
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
  {: screen}

6. Compruebe que la configuración se ha configurado correctamente probando el distribuidor de correo electrónico. Utilice la <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Config/post_email_dispatcher_test" target="_blank">API de prueba</a> para activar una solicitud en el remitente de correo electrónico personalizado configurado.

Para obtener un ejemplo funcional completo, consulte <a href="https://www.ibm.com/cloud/blog/use-ibm-cloud-app-id-and-your-email-provider-to-brand-mails-sent-to-app-users" target="_blank">Utilizar un proveedor propio para el correo que se envía con {{site.data.keyword.appid_full}}</a>.



## Idiomas soportados
{: #cd-languages}

Puede utilizar <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">las API de gestión de idioma <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> para definir el idioma en el que se pueden escribir los mensajes de usuario. Sin embargo, solo el idioma inglés está disponible desde un principio. Usted es el responsable de la traducción de los mensajes. Una vez establecida la configuración con la API, se actualiza la interfaz gráfica de usuario, de forma que pueda modificar el texto de plantilla.
{: shortdesc}

<table>
  <col width="20%">
  <col width="25%">
  <col width="35%">
  <tr>
    <th>Código</th>
    <th>Idioma</th>
    <th>Región</th>
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
    <td>Macao, R.A.E. de la RPC</td>
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
    <td>Macao, R.A.E. de la PRC</td>
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
