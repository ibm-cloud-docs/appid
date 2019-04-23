---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

keywords: authentication, authorization, identity, app security, secure, directory, registry, passwords, languages, lockout

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

# Definición de políticas de contraseñas
{: #cd-strength}

Puede definir los requisitos para las contraseñas que se pueden utilizar con el Directorio en la nube. Mediante la definición de requisitos específicos que los usuarios deban cumplir, puede garantizar una mayor seguridad en las aplicaciones.
{: shortdesc}

## Política: fortaleza de contraseña
{: #cd-password-strength}

Una contraseña segura es difícil o improbable de adivinar ya sea de forma manual o automática. Para establecer los requisitos para la fortaleza de una contraseña de usuario, puede utilizar los pasos siguientes.
{: shortdesc}

1. Vaya al separador **Políticas de contraseñas** del panel de control de APP ID.

2. En el recuadro **Definir fortaleza de contraseña**, pulse **Editar**. Se mostrará una pantalla.

3. Especifique una serie de expresiones regulares válida en el recuadro **Fortaleza de contraseña**.

  Ejemplos:
    - Debe tener al menos ocho caracteres. Expresión regular de ejemplo: `^.{8,}$`
    - Debe contener un número, una letra minúscula y una letra mayúscula. Expresión regular de ejemplo: `^(?:(?=.*\d)(?=.*[a-z])(?=.*[A-Z]).*)$`
    - Debe contener solo letras y números ingleses. Expresión regular de ejemplo: `^[A-Za-z0-9]*$`
    - Debe tener al menos un carácter exclusivo. Expresión regular de ejemplo: `^(\w)\w*?(?!\1)\w+$`

4. Pulse **Guardar**.

La fortaleza de la contraseña se puede establecer en la página de valores del directorio en la nube en la consola de {{site.data.keyword.appid_short_notm}}, o utilizando las <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.set_cloud_directory_password_regex" target="_blank">API de gestión <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.
{: note}


## Políticas de contraseñas avanzadas
{: #cd-advanced-password}


Puede mejorar la seguridad de la aplicación imponiendo restricciones de contraseña adicionales.
{: shortdesc}


Puede crear una política de contraseñas avanzada que esté formada por cualquier combinación de las 5 características siguientes:

 - Bloqueo tras repetir las credenciales de forma errónea
 - Evitar la reutilización de las contraseñas
 - Caducidad de la contraseña
 - Período mínimo entre los cambios de contraseña
 - Garantizar que la contraseña no incluye el nombre de usuario


 Si habilita esta característica, se activará la facturación adicional para las prestaciones de seguridad avanzadas. Para obtener más información, consulte [¿Cómo calcula {{site.data.keyword.appid_short_notm}} los precios?](/docs/services/appid?topic=appid-faq#faq-pricing)
 {: important}


### Política: Evitar la reutilización de las contraseñas
{: #cd-avoid-reuse}

Cuando los usuarios cambien la contraseña, es posible que desee evitar que elijan una contraseña utilizada recientemente.
{: shortdesc}

Mediante la GUI o la API, puede seleccionar el número de contraseñas que debe tener un usuario antes de poder repetir una contraseña utilizada anteriormente. Puede seleccionar cualquier valor entero entre 1 y 10.

Si está opción está activada, un usuario no puede utilizar una contraseña que ya haya utilizado recientemente. Si intentan establecer su contraseña en una contraseña utilizada recientemente, aparecerá un error en la GUI del widget de inicio de sesión predeterminado y se les solicitará que especifiquen una contraseña distinta.

Las contraseñas anteriores se almacenan de forma segura de la misma forma que se almacena la contraseña actual de un usuario.
{: note}


### Política: Bloqueo tras repetir las credenciales de forma errónea
{: #cd-lockout}

Es posible que desee proteger las cuentas de los usuarios bloqueando temporalmente la posibilidad de iniciar sesión cuando se detecta un comportamiento sospechosos como, por ejemplo, intentos de inicio de sesión consecutivos con una contraseña incorrecta. Esta medida puede ayudarle a evitar que una parte maliciosa obtenga acceso a la cuenta de un usuario adivinando la contraseña del mismo.
{: shortdesc}

Mediante la GUI o la API, puede establecer el número máximo de intentos de inicio de sesión fallidos que puede realizar un usuario antes de que su cuenta quede bloqueada temporalmente. También puede establecer la cantidad de tiempo que la cuenta está bloqueada. Dispone de las siguientes opciones:

* Número de intentos: Cualquier valor entero entre 1 y 10.
* Período de bloqueo: Cualquier valor entero especificado en minutos en el rango de 1 minuto a 1440 minutos (24 horas).

Si una cuenta está bloqueada, los usuarios no podrán iniciar sesión o realizar cualquier otra operación de autoservicio, como cambiar la contraseña hasta que haya transcurrido el período de bloqueo especificado. Cuando el período de bloqueo haya finalizado, el usuario se desbloqueará automáticamente.

Puede desbloquear un usuario antes de que se haya terminado el período de bloqueo. Para ver si están bloqueados, consulte si el campo `active` (activo) se establece en `false`. También puede comprobar si el estado del separador **Usuarios** del panel de control de servicio está establecido en `disabled` (inhabilitado). Para desbloquear un usuario, debe utilizar [la API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Cloud_Directory_Users/updateCloudDirectoryUser) para establecer el campo `active` (activo) en `true`.


### Política: Período mínimo entre los cambios de contraseña
{: #cd-minimum-time}

Es posible que desee evitar que los usuarios cambien la contraseña rápidamente estableciendo el período de tiempo mínimo que un usuario debe esperar para poder cambiar la contraseña.
{: shortdesc}

Esta característica es especialmente útil cuando se utiliza con la política "Evitar la reutilización de contraseñas". Sin esta limitación, un usuario podría cambiar de contraseña varias veces seguidas para omitir la limitación de volver a utilizar contraseñas recientes. Puede seleccionar cualquier valor entre 1 hora y 30 días, especificado en horas.


### Política: Caducidad de la contraseña
{: #cd-expiration}

Por motivos de seguridad, es posible que desee aplicar una política de rotación de contraseñas, de manera que los usuarios deban cambiar su contraseña después de un período de tiempo.
{: shortdesc}

Al utilizar la GUI o la API, puede establecer un período de tiempo durante el cual las contraseñas del usuario seguirán siendo válidas. Cuando la contraseña del usuario caduque, este se verá obligado a restablecer la contraseña en el próximo inicio de sesión. Puede seleccionar cualquier número de días completos entre 1 y 90.

Puede empezar rápidamente con el widget de inicio de sesión utilizando la GUI predeterminada proporcionada. El usuario recibe instrucciones para proporcionar una nueva contraseña antes de que se complete el inicio de sesión.

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

Cuando esta opción se activa, las contraseñas de usuario existentes no tendrán una fecha de caducidad. El período de caducidad empieza para los usuarios cuando se cambia la contraseña. Es posible que desee animar a los usuarios a actualizar la contraseña después de haber activado la característica.
{: note}


### Política: Garantizar que la contraseña no incluye el nombre de usuario
{: #cd-no-username}

Para obtener contraseñas más fuertes, es posible que desee evitar los usuarios que contienen su nombre de usuario o la primera parte de su dirección de correo electrónico.
{: shortdesc}

Esta restricción distingue entre mayúsculas y minúsculas, lo que significa que los usuarios no pueden alterar las mayúsculas y minúsculas de algunos o varios caracteres para poder utilizar la información personal. Para configurar esta opción, cambie el conmutado en **Activado**.

