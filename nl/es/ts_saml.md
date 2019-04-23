---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-10"

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

# Configuraciones de proveedor de identidad
{: #troubleshooting-idp}

Si tiene problemas al configurar los proveedores de identidad para que funcionen con {{site.data.keyword.appid_full}}, tenga en cuenta estas técnicas para resolverlos y obtener ayuda.
{: shortdesc}


## No se redirige a ningún usuario al proveedor de identidad
{: #ts-saml-redirect}

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

* Actualice el URL de inicio de sesión. Este URL se envía como parte de la authnRequest y debe ser exacto.
* Asegúrese de que los metadatos de {{site.data.keyword.appid_short_notm}} estén correctamente establecidos en los valores del proveedor de identidad.
* Configure el proveedor de identidad para aceptar la authnRequest en HTTP-Redirect.
* {{site.data.keyword.appid_short_notm}} no soporta la firma de authnRequests.

Si no funciona ninguna de las soluciones, es posible que pueda tener un problema de conexión.
{: tip}


## Problemas de SAML comunes
{: #ts-common-saml}

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
      <td><code>El cuerpo de respuesta SAML debe contener el parámetro RelayState.</code></td>
      <td>El parámetro no estaba incluido en el cuerpo de respuesta SAML. {{site.data.keyword.appid_short_notm}} proporciona el parámetro para el proveedor de identidad como parte de la solicitud y se debe devolver el parámetro exacto en la respuesta. Si el parámetro se modifica, puede ponerse en contacto con el administrador del proveedor de identidad. </td>
    </tr>
    <tr>
      <td><code>La configuración de SAML debe tener certificados, entityID y signInUrl del IdP.</code></td>
      <td>El proveedor de identidad SAML no está <a href="/docs/services/appid?topic=appid-enterprise#enterprise" target="_blank">configurado correctamente</a>. Valide la configuración.</td>
    </tr>
    <tr>
      <td><code>Error en la validación de aserción. Ha fallado la comprobación de firma de aserción SAML. El certificado .. podría no ser válido.</code></td>
      <td>Deben incluirse en la aserción una firma válida y un resumen. La firma debe crearse utilizando la clave privada asociada con el certificado proporcionado en la configuración de SAML, se puede utilizar uno secundario o uno primario. <strong>Nota</strong>: {{site.data.keyword.appid_short_notm}} no da soporte a la aserción cifrada. Si el proveedor de identidad cifra la aserción de SAML, inhabilite el cifrado.</td>
    </tr>
  </tbody>
</table>



## Errores de validación de la respuesta SAML
{: #ts-saml-response}

{{site.data.keyword.appid_short_notm}} impone los siguientes requisitos de validez para las aserciones. Todos los atributos son nodos XML de la respuesta de SAML obligatorios a menos que se especifique lo contrario.
{: shortdesc}


<table summary="Cada fila de tabla debe leerse de izquierda a derecha con el elemento de respuesta en la columna uno y la descripción en la columna dos">
  <thead>
    <th>Elemento de respuesta</th>
    <th>Descripción</th>
  </thead>
  <tbody>
    <tr>
      <td><code>samlp:Response</code></td>
      <td>El elemento de respuesta debe incluirse en el XML de respuesta.</td>
    </tr>
    <tr>
      <td><code>SAML version</code></td>
      <td>{{site.data.keyword.appid_short_notm}} únicamente acepta <code>SAML versión 2.0</code>.</td>
    </tr>
    <tr>
      <td><code>InResponseTo</code></td>
      <td>{{site.data.keyword.appid_short_notm}} verifica que el elemento de respuesta <code>InResponseTo</code> devuelto en la aserción coincide con el ID de solicitud guardado de la solicitud SAML.</td>
    </tr>
    <tr>
      <td><code>saml:issuer</code></td>
      <td>El emisor que se especifica en una aserción debe coincidir con el emisor especificado en la configuración del proveedor de identidad de {{site.data.keyword.appid_short_notm}}.</td>
    </tr>
    <tr>
      <td><code>ds:Signature</code></td>
      <td>Deben incluirse en la aserción una firma válida y un resumen. La firma debe crearse utilizando la clave privada asociada con el certificado proporcionado en la configuración de SAML. El resumen se valida utilizando los valores <code>CanonicalizationMethod</code> y <code>Transforms</code> especificados. <strong>Nota</strong>: {{site.data.keyword.appid_short_notm}} no valida el vencimiento de certificado. Para obtener ayuda en la gestión de certificados, pruebe el [gestor de certificados](/docs/services/certificate-manager?topic=certificate-manager-getting-started#getting-started).</td>
    </tr>
    <tr>
      <td><code>saml:subject</code></td>
      <td>El asunto o <code>name_id</code> de la aserción debe ser el correo electrónico de federación del usuario.</td>
    </tr>
    <tr>
      <td><code>saml:AttributeStatement</code></td>
      <td>Certifica que determinados atributos están asociados con un usuario autenticado específico.</td>
    </tr>
    <tr>
      <td><code>saml:Conditions</code></td>
      <td><strong>Opcional</strong>: Cuando se incluye una sentencia de condiciones en una aserción, también debe contener una marca de hora válida. {{site.data.keyword.appid_short_notm}} respeta el período de validez especificado en una aserción. Para la verificación, el servicio busca las restricciones <code>NotBefore</code> y <code>NotOnOrAfter</code> que deben definirse y validarse.</td>
    </tr>
  </tbody>
</table>

{{site.data.keyword.appid_short_notm}} no ofrece soporte a la aserción cifrada. Si se ha establecido el proveedor de identidad para cifrar la aserción, inhabilítelo. La aserción debe tener un formato no cifrado.
{: tip}
