---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-09"

keywords: Authentication, authorization, identity, app security, secure, troubleshooting, help, support, requests, uri

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
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}

# Resolución de problemas: General
{: #troubleshooting}

Si tiene problemas mientras trabaja con {{site.data.keyword.appid_full}}, considere estas técnicas para resolverlos y obtener ayuda.
{: shortdesc}

## Obtención de ayuda y soporte
{: #ts-gettinghelp}

Puede obtener ayuda buscando información o planteando preguntas en el foro. También puede abrir una incidencia de soporte. Si utiliza el foro para hacer preguntas, etiquete su pregunta para que los equipos de desarrolladores de {{site.data.keyword.cloud_notm}} la puedan ver.
  * Si tiene preguntas técnicas sobre {{site.data.keyword.appid_short_notm}}, publique la pregunta en <a href="https://stackoverflow.com/" target="_blank">Stack Overflow <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> y etiquete la pregunta con "ibm-appid".
  * Para formular preguntas sobre el servicio y obtener instrucciones de iniciación, utilice el foro <a href="https://developer.ibm.com/" target="_blank">dW Answers <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>. Incluya la etiqueta `appid`.

Para obtener más información sobre cómo obtener ayuda, consulte [¿cómo puedo obtener la ayuda que necesito?](/docs/get-support?topic=get-support-getting-customer-support#getting-customer-support).


## No se redirige a ningún usuario a la app después de iniciar sesión
{: #ts-signin-fail}

{: tsSymptoms}
Un usuario entra a la aplicación mediante una página de inicio de sesión del proveedor de identidades, y o bien no ocurre nada o el inicio de sesión falla.

{: tsCauses}
El inicio de sesión podría fallar por los motivos siguientes:

* El URL de redirección no se ha añadido correctamente a [la lista blanca](/docs/services/appid?topic=appid-faq#faq-redirect).
* El usuario no está autorizado.
* El usuario ha intentado iniciar sesión con credenciales erróneas.

{: tsResolve}
Para que se produzca una redirección:

* Verifique que el URL de redirección sea correcto. Debe ser exacto para que la redirección funcione.
* Asegúrese de que el usuario haya iniciado sesión con las credenciales correctas.
* Compruebe que estén configuradas en los valores de usuario del proveedor de identidad.



## Se ha rechazado un URI personalizado
{: #ts-custom-uri}

{: tsSymptoms}
Cuando especifica un URL de redirección web que utiliza un esquema de URL personalizado, la consola de {{site.data.keyword.appid_short_notm}} lo rechaza.

{: tsCauses}
Es posible que el URL se haya rechazado por los motivos siguientes:

* El URL no sigue un esquema `http` o `https`
* El URL termina en `://`
* Hay un error tipográfico en el URL

Existen limitaciones por motivos de seguridad.

{: tsResolve}
Para resolver este problema, verifique que el URL sea correcto. Si el URL no cumple con los requisitos, puede crear un punto final HTTPS en la app para redirigir el código de concesión recibido al URL personalizado. Especifique el punto final creado como URL de redirección en la consola de {{site.data.keyword.appid_short_notm}}. Para obtener más información acerca de los URI de redirección, consulte [Adición de URI de redirección](/docs/services/appid?topic=appid-managing-idp#add-redirect-uri).

## No se redirige a ningún usuario al proveedor de identidad
{: #ts-redirect}

{: tsSymptoms}
Un usuario intenta iniciar sesión en su aplicación, pero la página de inicio de sesión no se muestra cuando se solicita.

{: tsCauses}
El proveedor de identidad puede fallar por varias razones:

* El URL de redirección configurado es incorrecto.
* El proveedor de identidad no reconoce la solicitud de autenticación.
* El proveedor de identidad espera un enlace HTTP-POST.
* El proveedor de identidad espera una AuthnRequest firmada.

{: tsResolve}
Puede intentar algunas de estas soluciones:

* Actualice el URL de inicio de sesión. Este URL se envía como parte de la AuthnRequest y debe ser exacto.
* Asegúrese de que los metadatos de {{site.data.keyword.appid_short_notm}} estén correctamente establecidos en los valores del proveedor de identidad.
* Configure el proveedor de identidad para aceptar la AuthnRequest en HTTP-Redirect.
* {{site.data.keyword.appid_short_notm}} no soporta la firma de AuthnRequests.

Si no funciona ninguna de las soluciones, es posible que pueda tener un problema de conexión.
{: tip}


## Un atributo muestra el valor incorrecto
{: #ts-saml-attribute}

{: tsSymptoms}
Existe un valor de atributo en un perfil de usuario, pero no está asociado al atributo correcto.

{: tsCauses}
El atributo de perfil de usuario no está correlacionado correctamente.

{: tsResolve}
Correlacione el atributo en los valores del proveedor de identidad. {{site.data.keyword.appid_short_notm}} espera los atributos siguientes:
* `nombre`
* `correo electrónico`
* `entorno local`
* `imagen`



## Error: Demasiadas solicitudes
{: #ts-requests}

{: tsSymptoms}
Intenta visualizar la página de inicio de la app pero recibe el siguiente error:

```
{"error_code":"too many requests","error_description":"too many requests"}
```
{: screen}

{: tsCauses}
Es posible que reciba un error de "demasiadas solicitudes" si está realizando pruebas automatizadas con un solo usuario virtual. Cada usuario está limitado a cinco intentos de inicio de sesión en un intervalo de tiempo de un minuto. Los intentos de inicio de sesión están limitados para evitar DDoS de fuerza bruta y otro tipo de ataques similares.

{: tsResolve}
Para resolver el problema, es posible que desee utilizar varios usuarios virtuales cuando realice las pruebas.
</br>
