---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-21"

keywords: authentication, authorization, identity, app security, secure, development, idp, troubleshooting, redirected, validation

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
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}

# Resolución de problemas: SAML
{: #troubleshooting-idp}

Si tiene problemas al configurar SAML para que funcione con {{site.data.keyword.appid_full}}, tenga en cuenta estas técnicas para resolverlos y obtener ayuda.
{: shortdesc}


## Problemas de configuración comunes
{: #ts-common-saml}

La infraestructura de SAML admite varios perfiles, flujos y configuraciones, lo que significa que es esencial que la configuración del proveedor de identidad se haya realizado correctamente. Consulte los siguientes temas para obtener ayuda para resolver algunos de los problemas comunes que puede encontrar al trabajar con SAML.
{: shortdesc}


Para códigos de error específicos y mensajes de su proveedor de identidad que no aparecen en esta página, puede resultar de utilidad buscar en la [especificación de SAML](http://docs.oasis-open.org/security/saml/Post2.0/sstc-saml-tech-overview-2.0.html) para obtener explicaciones detalladas. Si no encuentra lo que busca, puede ponerse en contacto con el administrador de proveedores de identidad para obtener más información.
{: note}



### Falta el parámetro `RelayState`
{: #ts-saml-relaystate}

**¿Qué sucede?**

Falta el parámetro `RelayState` en la respuesta de autenticación.


**¿Por qué sucede?**

{{site.data.keyword.appid_short_notm}} envía un parámetro opaco conocido como `RelayState` como parte de la solicitud de autenticación. Si no ve el parámetro en la respuesta, es posible que el proveedor de identidad no esté configurado para devolverlo correctamente. `RelayState` tiene el formato siguiente:

```
https://idp.example.org/SAML2/SSO/Redirect?SAMLRequest=request&RelayState=token
```
{: screen}

**¿Cómo se soluciona?**

Verifique que el proveedor de SAML está configurado para devolver el parámetro `RelayState` a {{site.data.keyword.appid_short_notm}} sin modificarlo en nada.


### Falta el campo NameID o es incorrecto
{: #ts-saml-nameid}

**¿Qué sucede?**

Cuando envía una solicitud de autenticación, recibe un error relacionado con el `NameID`.

**¿Por qué sucede?**

{{site.data.keyword.appid_short_notm}}, como proveedor de servicios, define la forma en que el servicio y el proveedor de identidad identifican a los usuarios. Con {{site.data.keyword.appid_short_notm}}, los usuarios se identifican en la solicitud de autenticación `NameID` en el campo `NameID`, como se muestra en el ejemplo siguiente.

```
<NameIDFormat>urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress</NameIDFormat>
```
{: screen}

**¿Cómo se soluciona?**

Para resolver el problema, asegúrese de que el `NameID` del proveedor de identidad tiene el formato de una dirección de correo electrónico. Verifique que todos los usuarios del registro del proveedor de identidad tengan un formato de dirección de correo electrónico válido. A continuación, verifique que el campo `NameID` se ha definido correctamente para que siempre se devuelva un mensaje de correo electrónico válido, aunque los usuarios del registro tengan varios correos electrónicos.



### Error de firma de respuesta
{: #ts-saml-response-sign-fail}

**¿Qué sucede?**

Cuando envía una solicitud de autenticación, recibe el mensaje de error siguiente:

```
Could not verify SAML assertion signature. Ensure {{site.data.keyword.appid_short_notm}} is configurated with your SAML provider's signing certificate.
```
{: screen}

**¿Por qué sucede?**

{{site.data.keyword.appid_short_notm}} espera que todas las aserciones SAML en su respuesta estén firmadas. Si el servicio no puede encontrar ni verificar la firma en la respuesta, se devuelve el error.

**¿Cómo se soluciona?**

Para resolver el problema, asegúrese de que:

* Ha extraído el certificado de firma del archivo XML de metadatos de los proveedores de identidades. Asegúrese de utilizar la clave con `<KeyDescriptor use="signing">`.
* Ha establecido el algoritmo de firma de respuesta para que sea XXX. 





### Error al descifrar la respuesta
{: #ts-saml-decrypt-fail}

**¿Qué sucede?**

Recibe uno de los mensajes de error siguientes en respuesta a la solicitud de autenticación.

Mensaje de error 1:

```
Unexpectedly received an encrypted assertion. Please enable response encryption in your {{site.data.keyword.appid_short_notm}} SAML configuration.
```
{: screen}

Mensaje de error 2: 

```
Could not decrypt SAML assertion. Ensure your SAML provider is configured with the {{site.data.keyword.appid_short_notm}} encryption 
```
{: screen}


**¿Por qué sucede?**

Si el proveedor de identidad está configurado para cifrar, {{site.data.keyword.appid_short_notm}} se debe configurar para que firme las solicitudes de autenticación de SAML (AuthnRequest). A continuación, el proveedor de identidad debe estar configurado para esperar la configuración correspondiente. Puede recibir estos errores por una de las razones siguientes:

- {{site.data.keyword.appid_short_notm}} no está configurado para esperar que la respuesta de SAML del proveedor de identidad esté cifrada.
- {{site.data.keyword.appid_short_notm}} no puede descifrar correctamente las aserciones.


**¿Cómo se soluciona?**

Si recibe el mensaje de error 1, verifique que la configuración de SAML está establecida para esperar una respuesta cifrada. De forma predeterminada, {{site.data.keyword.appid_short_notm}} no espera que la respuesta esté cifrada. Para configurar el cifrado, establezca el parámetro `encryptResponse` a **true** utilizando [la API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp).

Si recibe el mensaje de error 2, asegúrese de que el certificado es correcto. Puede obtener el certificado de firma del archivo XML de metadatos de {{site.data.keyword.appid_short_notm}}. Asegúrese de utilizar la clave con `<KeyDescriptor use="signing">`. Verifique que el proveedor de identidades esté configurado para utilizar` ` como algoritmo de firma de firmas. 


### Código de error del respondedor
{: #ts-saml-responder}

**¿Qué sucede?**

Cuando envía una solicitud de autenticación, recibe el siguiente mensaje de error genérico:

```
urn:oasis:names:tc:SAML:2.0:status:Responder
```
{: screen}

**¿Por qué sucede?**

Aunque {{site.data.keyword.appid_short_notm}} envía la solicitud de autenticación inicial, el proveedor de identidad debe llevar a cabo la autenticación de usuario y devolver la respuesta. Existen varias razones que pueden hacer que el proveedor de identidad emita este mensaje de error.

Puede que vea el mensaje si su proveedor de identidad: 

* no puede encontrar ni verificar el nombre de usuario.
* No admite el formato `NameID` definido en la solicitud de autenticación (`AuthnRequest`).
* no admite el contexto de autenticación.
* requiere que la solicitud de autenticación se firme o que se utilice un algoritmo específico en la firma.

**¿Cómo se soluciona?**

Para resolver el problema, verifique la configuración y el nombre de usuario. Verifique que tiene definido el contexto de autenticación correcto y las variables correctas. Compruebe si su solicitud se debe firmar de una forma específica.




### Solicitud de autenticación no soportada
{: #ts-saml-unsupported-request}

**¿Qué sucede?**

Recibiese un mensaje con respecto a una solicitud de autenticación no soportada.

**¿Por qué sucede?**

Cuando {{site.data.keyword.appid_short_notm}} genera una solicitud de autenticación, puede utilizar el contexto de autenticación para solicitar la calidad de las aserciones de autenticación y SAML.

**¿Cómo se soluciona?**

Para resolver el problema, puede actualizar el contexto de autenticación. De forma predeterminada, {{site.data.keyword.appid_short_notm}} utiliza la clase de autenticación `urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport` y la comparación `exact`. Puede actualizar el parámetro de contexto para que se ajuste a su caso de uso utilizando las API.




### Error de firma de solicitud SAML
{: #ts-saml-request-sign-fail}

**¿Qué sucede?**

Recibe un error que afirma que no se puede verificar la solicitud de autenticación.

**¿Por qué sucede?**

{{site.data.keyword.appid_short_notm}} se puede configurar para que firme la solicitud de autenticación SAML (`AuthNRequest`), pero el proveedor de identidad debe estar configurado para esperar la configuración correspondiente.

**¿Cómo se soluciona?**

Para resolver el problema:

* Verifique que {{site.data.keyword.cloud_notm}} está configurado para firmar la solicitud de autenticación estableciendo el parámetro `signRequest` en `true` utilizando la [API de SAML IdP](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp). Puede comprobar si la solicitud de autenticación se ha firmado mirando el URL de la solicitud. La firma se incluye como un parámetro de consulta. Por ejemplo: `https://idp.example.org/SAML2/SSO/Redirect?SAMLRequest=request&SigAlg=value&Signature=value&RelayState=token`

* Verifique que el proveedor de identidades esté configurado con el certificado correcto. Para obtener el certificado de firma, compruebe el archivo XML de metadatos de {{site.data.keyword.cloud_notm}} que ha descargado del panel de control de {{site.data.keyword.cloud_notm}}. Asegúrese de utilizar la clave con `<KeyDescriptor use="signing">`.

* Verifique que el proveedor de identidades esté configurado para utilizar` ` como algoritmo de firma.



## Depuración de la conexión
{: #ts-saml-debug-connection}

¿Tiene la configuración correcta, pero aún tiene un error? Consulte algunos de los consejos útiles siguientes para depurar la conexión SAML.
{: shortdesc}


### ¿Cómo puedo capturar mi solicitud de autenticación SAML y la respuesta?
{: #ts-saml-capture}

Existen varias opciones para los plug-ins de navegador como, por ejemplo, [Firefox](https://addons.mozilla.org/en-US/firefox/addon/saml-tracer/) y [Chrome](https://chrome.google.com/webstore/detail/saml-tracer/mpdajninpobndbfcldcmbpnnbhibjmch?hl=en) que se pueden utilizar para capturar las solicitudes y respuestas de SAML. ¿No desea utilizar un plug-in? Ningún problema. Atlassian proporciona instrucciones para un [método de extracción más manual](https://confluence.atlassian.com/jirakb/how-to-view-a-saml-responses-in-your-browser-for-troubleshooting-872129244.html).


### NO entiendo los mensajes. ¿Cómo puedo descodificarlos?
{: #ts-saml-decode-messages}

Si sigue teniendo problemas después de utilizar la herramienta de depuración de SAML, pruebe a utilizar las [herramientas de desarrollador de SAML](https://www.samltool.com/online_tools.php) para obtener más ayuda para descodificar los mensajes. Recuerde: Según dónde intercepte los mensajes de SAML, su solicitud puede ser [codificada como URL](https://www.samltool.com/online_tools.php), [codificada como base 64 y deflactada](https://www.samltool.com/decode.php) o cifrada con [](https://www.samltool.com/decrypt.php).

No utilice las herramientas en línea para descifrar mensajes SAML como por ejemplo la respuesta de SAML. Las herramientas necesitan acceso a la clave privada de cifrado para descifrar la información. La clave se debe mantener privada y el acceso controlado. La herramienta de descodificación que se menciona en esta sección se debe utilizar únicamente para fines de depuración.
{: important}

