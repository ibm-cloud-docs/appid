---

copyright:
  years: 2017, 2018
lastupdated: "2018-06-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tip: .tip}

# Configuraciones de proveedor de identidad
{: #troubleshooting-idp}

Si tiene problemas al configurar los proveedores de identidad para que funcionen con {{site.data.keyword.appid_full}}, tenga en cuenta estas técnicas para resolverlos y obtener ayuda.
{: shortdesc}


## No hay redirección a la app después de iniciar sesión
{: #signin-fail}

{: tsSymptoms}
Un usuario entra a la aplicación mediante una página de inicio de sesión del proveedor de identidades, y o bien no ocurre nada o el inicio de sesión falla.

{: tsCauses}
El inicio de sesión podría fallar por los motivos siguientes:

* El URL de redirección no se ha añadido correctamente a [la lista blanca](identity-providers.html#redirect).
* El usuario no está autorizado.
* El usuario ha intentado iniciar sesión con credenciales erróneas.

{: tsResolve}
Para que se produzca una redirección:

* Verifique que el URL de redirección sea correcto. Debe ser exacto para que la redirección funcione.
* Asegúrese de que el usuario haya iniciado sesión con las credenciales correctas.
* Compruebe que estén configuradas en los valores de usuario del proveedor de identidad.


## Problemas comunes al trabajar con SAML
{: #common-saml}

Revise la tabla siguiente para obtener explicaciones y resoluciones para los problemas más comunes que se producen al trabajar con SAML.

<table summary="Cada fila de tabla debe leerse de izquierda a derecha, con el estado de clúster en la columna uno y una descripción en la columna dos.">
  <thead>
    <th>Mensaje</th>
    <th>Descripción</th>
  </thead>
  <tbody>
    <tr>
      <td><code>No se ha podido analizar el xml de aserción.</code></td>
      <td>La respuesta de SAML estaba mal formada.</td>
    </tr>
    <tr>
      <td><code>Atributo sin nombre no válido. Póngase en contacto con el administrador del proveedor de identidad.</code></td>
      <td>Hay un <code>&lt;saml:Attribute&gt;</code> sin un valor definido. Póngase en contacto con el administrador del proveedor de identidad.</td>
    </tr>
    <tr>
      <td><code>El cuerpo de respuesta SAML debe contener RelayState.</code></td>
      <td>El parámetro RelayState no estaba incluido en el cuerpo de respuesta SAML. {{site.data.keyword.appid_short_notm}} proporciona el parámetro para el proveedor de identidad como parte de la solicitud y se debe devolver el parámetro exacto en la respuesta. Si el parámetro se modifica, puede ponerse en contacto con el administrador del proveedor de identidad. </td>
    </tr>
    <tr>
      <td><code>La configuración de SAML debe tener certificados, entityID y signInUrl del IdP.</code></td>
      <td>El proveedor de identidad SAML no está configurado correctamente. Valide la configuración. Para obtener ayuda, consulte <a href="enterprise.html#configuring-saml" target="_blank">Configuración de la app para trabajar con un proveedor de identidad SAML externo.</a></td>
    </tr>
    <tr>
      <td><code>Error en la validación de aserción. Ha fallado la comprobación de firma de aserción SAML. El certificado .. podría no ser válido.</code></td>
      <td>Deben incluirse en la aserción una firma válida y un resumen. La firma debe crearse utilizando la clave privada asociada con el certificado proporcionado en la configuración de SAML; se puede utilizar uno secundario o uno primario. <strong>Nota</strong>: {{site.data.keyword.appid_short_notm}} no da soporte a la aserción cifrada. Si el proveedor de identidad hace esto en la aserción de SAML, inhabilite el cifrado.</td>
    </tr>
  </tbody>
</table>


## No hay redirección al proveedor de identidad
{: #saml-redirect}

{: tsSymptoms}
Un usuario intenta iniciar sesión en su aplicación, pero la página de inicio de sesión no se muestra cuando se solicita.

{: tsCauses}
El proveedor de identidad puede fallar por varias razones:

* El URL de redirección configurado es incorrecto.
* El proveedor de identidad no reconoce la solicitud de autenticación.
* El proveedor de identidad espera un enlace HTTP-POST.
* El proveedor de identidad espera una authnRequest firmada.

{: tsResolve}
Puede intentar algunas de estas soluciones:

* Actualice su URL de inicio de sesión. Este URL se envía como parte de la authnRequest y debe ser exacto.
* Asegúrese de que los metadatos de {{site.data.keyword.appid_short_notm}} estén correctamente establecidos en los valores del proveedor de identidad.
* Configure el proveedor de identidad para aceptar la authnRequest en HTTP-Redirect.
* {{site.data.keyword.appid_short_notm}} no soporta la firma de authnRequests.

Si no funciona ninguna de las soluciones, es posible que pueda tener un problema de conexión.
{: tip}

## Un atributo muestra el valor incorrecto
{: #saml-attribute}

{: tsSymptoms}
Existe un valor de atributo en un perfil de usuario, pero no está conectado al atributo correcto.

{: tsCauses}
El Atributo de perfil de usuario no está correlacionado correctamente.

{: tsResolve}
Correlacione el atributo en los valores del proveedor de identidad. {{site.data.keyword.appid_short_notm}} espera los atributos siguientes:
* `nombre`
* `correo electrónico`
* `entorno local`
* `imagen`


