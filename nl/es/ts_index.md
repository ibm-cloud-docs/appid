---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}

# Resolución general de problemas
{: #troubleshooting}

Si tiene problemas mientras trabaja con {{site.data.keyword.appid_full}}, considere estas técnicas para resolverlos y obtener ayuda.
{: shortdesc}

## Obtención de ayuda y soporte
{: #gettinghelp}

Obtendrá ayuda en la información que encuentre o planteando preguntas en el foro. También puede abrir una incidencia de soporte. Si utiliza el foro para hacer preguntas, etiquete su pregunta para que los equipos de desarrolladores de {{site.data.keyword.Bluemix_notm}} la puedan ver.
  * Si tiene preguntas técnicas sobre {{site.data.keyword.appid_short_notm}}, publique la pregunta en <a href="https://stackoverflow.com/search?q=ibm-appid" target="_blank">Stack Overflow <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> y etiquete la pregunta con "ibm-appid".
  * Para preguntas referentes al servicio e instrucciones sobre cómo empezar, utilice el foro <a href="https://developer.ibm.com/answers/topics/appid/" target="_blank">dW Answers <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>. Incluya la etiqueta `appid`.

Para obtener más información sobre cómo obtener ayuda, consulte [¿Cómo puedo obtener la ayuda que necesito?](/docs/get-support/howtogetsupport.html#getting-customer-support).

</br>

## Se ha rechazado un URL personalizado
{: #ts-custom-url}


{: tsSymptoms}
Cuando especifica un URL de redirección web que utiliza un esquema de URL personalizado, la consola de {{site.data.keyword.appid_short_notm}} lo rechaza.

{: tsCauses}
Es posible que el URL se haya rechazado por los motivos siguientes:

* El URL no sigue un esquema `http` o `https`
* El URL termina en `://`
* Hay un error tipográfico en el URL

Existen limitaciones por motivos de seguridad.

{: tsResolve}
Para resolver este problema, verifique que el URL sea correcto. Si el URL no cumple con los requisitos, puede crear un punto final HTTPS en la app para redirigir el código de concesión recibido al URL personalizado. Especifique el punto final creado como URL de redirección en la consola de {{site.data.keyword.appid_short_notm}}.

</br>
