---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:faq: data-hd-content-type='faq'}


# Preguntas más frecuentes (FAQ)
{: #faq}

Estas preguntas más frecuentes proporcionan respuestas a preguntas comunes sobre el servicio de {{site.data.keyword.appid_full}}.
{: shortdesc}


## ¿Cómo calcula {{site.data.keyword.appid_short_notm}} los precios?
{: #pricing}
{: faq}

Con {{site.data.keyword.appid_short_notm}} paga menos cuantos más recursos utiliza.
{: shortdesc}

El plan de niveles graduado consta de tres partes: el número de sucesos de autenticación, seguridad normal y avanzada y el número de usuarios autorizados. Se le facturará cada mes en función del resumen de las dos partes. El precio total es el cargo acumulado de cada nivel de uso que consiste en la cantidad multiplicada por el precio unitario en ese nivel.

Los primeros 1000 sucesos de autenticación y 1000 usuarios autorizados son gratuitos cada mes, a excepción de los sucesos de seguridad avanzados. Los sucesos de seguridad avanzados generan cargos adicionales.

### Sucesos de autenticación

Se produce un suceso de autenticación cuando se emite una nueva señal de acceso, normal o anónima. Las señales se pueden emitir como respuesta a una solicitud de inicio de sesión iniciada por un usuario o en nombre del usuario por parte de una app. De forma predeterminada, las señales de acceso son válidas durante una hora y las señales anónimas son válidas durante 30 días. Cuando la señal caduca debe crear una nueva para acceder a los recursos protegidos. Puede actualizar la hora de caducidad de las señales de {{site.data.keyword.appid_short_notm}} en la página **Caducidad de inicio de sesión** del panel de control del servicio.

#### Características de seguridad avanzadas

Las características de seguridad avanzadas le proporcionan la posibilidad de fortalecer la seguridad de la aplicación.
{: shortdesc}

<table>
  <tr>
    <th>Función</th>
    <th>Ventaja</th>
  </tr>
  <tr>
    <td>Autenticación de multifactores</td>
    <td>[MFA para el directorio en la nube](mfa.html) confirma la identidad de un usuario solicitando al usuario que especifique un código de acceso de una sola vez que se envía a su correo electrónico además de especificar el correo electrónico y la contraseña.</td>
  </tr>
  <tr>
    <td>Gestión de política de contraseñas</td>
    <td>Como propietario de una cuenta, puede imponer contraseñas más seguras para el directorio en la nube configurando un conjunto de reglas a las que deben ajustarse las contraseñas de usuario. Los ejemplos incluyen el número de intentos de inicio de sesión antes del bloqueo, las horas de caducidad, el intervalo de tiempo mínimo entre actualizaciones de contraseña o el número de veces que una contraseña no se puede repetir. Para obtener una lista completa de las opciones y la información de configuración, consulte [Gestión avanzada de contraseñas](cloud-directory.html#advanced-password).</td>
  </tr>
</table>

Las características de seguridad avanzadas están inhabilitadas de forma predeterminada. Si activa la autenticación de varios factores o la gestión de políticas de contraseñas, se incurre un cargo adicional. Si inhabilita todas las características avanzadas, la cuenta vuelve a la política de costes más bajos. Por ejemplo, si ha obtenido 10.000 señales de acceso. Después, activa la MFA y la gestión de políticas de contraseñas y se obtienen 10.000 más. En ese caso, pagaría por 20.000 sucesos de autenticación y 10.000 sucesos de seguridad avanzada.

Estas características están disponibles solo para aquellas instancias que están en el plan de precios de nivel graduado y que se crearon después del 15 de marzo de 2018.
{: note}

### Usuarios autorizados

Un usuario autorizado es un usuario exclusivo que inicia sesión con su servicio de forma directa o indirecta, incluidos los usuarios anónimos. Se le factura un usuario autorizado cada vez que un nuevo usuario inicia sesión en la aplicación, incluidos los usuarios anónimos. Por ejemplo, si un usuario inicia sesión con Facebook y más adelante con Google, se consideran dos usuarios autorizados diferentes.

Para obtener la información sobre precios más reciente de {{site.data.keyword.appid_short_notm}}, consulte la [calculadora de precios](https://console.cloud.ibm.com/pricing/configure/service/AdvancedMobileAccess-d6aece47-d840-45b0-8ab9-ad15354deeea).
{: important}

</br>


## ¿Por qué tengo que incluir en una lista blanca mi URL de redirección?
{: #redirect}
{: faq}

Un URL de redirección es el punto final de devolución de llamada de la app. Para evitar ataques de suplantación, {{site.data.keyword.appid_short_notm}} valida el URL con la lista blanca de URL de redirección. Cuando se produce phishing, existe la posibilidad de que un atacante obtenga acceso a las señales del usuario.

Para añadir el URL a la lista blanca:

1. Vaya a **Proveedores de identidad > Gestionar**.
2. En el campo **Añadir URL de redirección web**, escriba el URL y pulse **+**.

No incluya ningún parámetro de consulta en el URL. Se omitirán en el proceso de validación. URL de ejemplo: `http://host:[port]/path`
{: tip}

</br>

## ¿Cómo funciona el cifrado en {{site.data.keyword.appid_short_notm}}?
{: #encryption}
{: faq}

Consulte la tabla siguiente para obtener respuestas a las preguntas más frecuentes sobre el cifrado.

<table>
  <thead>
    <th colspan=2><img src="images/idea.png" alt="Icono de más información"/>  </th>
  </thead>
  <tbody>
    <tr>
      <td>¿Por qué se utiliza el cifrado?</td>
      <td>Una forma de proteger la información de nuestros usuarios consiste en cifrar los datos de cliente en reposo. El servicio cifra datos de cliente en reposo con claves por arrendatario.</td>
    </tr>
    <tr>
      <td>¿Se han creado algoritmos propios? ¿Cuáles se utilizan en el código?</td>
      <td>No hemos creado algoritmos propios, el servicio utiliza <code>AES</code> y <code>SHA-256</code> con salting.</td>
    </tr>
    <tr>
      <td>¿Se utilizan módulos o proveedores de cifrado de código abierto o público? ¿Se exponen las funciones de cifrado en algún momento? </td>
      <td>El servicio utiliza bibliotecas Java <code>javax.crypto</code>, pero nunca expone las funciones de cifrado.</td>
    </tr>
    <tr>
      <td>¿Cómo se almacenan las claves?</td>
      <td>Las claves se generan y cifran con una clave maestra que es específica de cada región y que después se almacena localmente. Las claves maestras se almacenan en {{site.data.keyword.keymanagementserviceshort}}. En los niveles de almacenamiento y middleware existe un cifrado de nivel de servicio, lo que significa que hay una clave para todos los clientes. En el nivel de app, cada cliente tiene su propia clave de cifrado.</td>
    </tr>
    <tr>
      <td>¿Qué fortaleza de clave se utiliza?</td>
      <td>El servicio utiliza 16 bytes.</td>
    </tr>
    <tr>
      <td>¿Se invoca alguna API remota que exponga las capacidades de cifrado?</td>
      <td>No, no se hace.</td>
    </tr>
  </tbody>
</table>

</br>

## ¿A qué espera {{site.data.keyword.appid_short_notm}} que se parezca una aserción SAML?
{: #saml-example}
{: faq}

El servicio espera que una aserción SAML se parezca al ejemplo siguiente.

```
<samlp:Response xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol" ID="s2202bbbbafa9d270d1c15990b738f4ab36139d463" InResponseTo="_e4a78780-35da-012e-8ea7-0050569200d8" Version="2.0" IssueInstant="2011-03-21T11:22:02Z" Destination="https://example.example.com/">
  <saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">idp_entityId</saml:Issuer>
  <samlp:Status xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <samlp:StatusCode  xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol"Value="urn:oasis:names:tc:SAML:2.0:status:Success"/>
  </samlp:Status>
  <saml:Assertion xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="2.0" ID="pfx539c9774-de5c-5f52-0c3f-b1c2e2697a89" IssueInstant="2018-01-29T13:02:58Z" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <saml:Issuer>idp_entityId</saml:Issuer>
    <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      <ds:SignedInfo>
        <ds:CanonicalizationMethod Algorithm="one_of_supported_algo"/>
        <ds:SignatureMethod Algorithm="one_of_supported_algo"/>
        <ds:Reference URI="#pfx539c9774-de5c-5f52-0c3f-b1c2e2697a89">
          <ds:Transforms>
            <ds:Transform Algorithm="one_of_supported_algo"/>
            <ds:Transform Algorithm="one_of_supported_algo"/>
          </ds:Transforms>
          <ds:DigestMethod Algorithm="one_of_supported_algo"/>
          <ds:DigestValue>huywDPPfOEGyyzE7d5hjOG97p7FDdGrjoSfes6RB19g=</ds:DigestValue>
        </ds:Reference>
      </ds:SignedInfo>
 <ds:SignatureValue>BAwNZFgWF2oxD1ux0WPfeHnzL+IWYqGhkM9DD28nI9v8XtPN8tqmIb5y4bomaYknmNpWYn7TgNO2Rn/XOq+N9fTZXO2RybaC49iF+zWibRIcNwFKCCpDL6H6jA5eqJX2YKBR+K6Yt2JPoUIRLmqdgm2lMr4Nwq1KYcSzQ/yoV5W0SN/V5t8EfctFoaXVPdtfHVXkwqHeufo+L4gobFt9NRTzXB0SQEClA1L8hQ+/LhY4l46k1D0c34iWjVLZr+ecQyubf7rekOG/R7DjWCFMTke822dR+eJTPWFsHGSPWCDDHFYqB4QMinTvUnsngjY3AssPqIOjeUxjL3p+GXn8IQ==</ds:SignatureValue>
    </ds:Signature>
    <saml:Subject>
      <saml:NameID Format="urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress">JohnDoe@gmail.com</saml:NameID>
    </saml:Subject>
    <saml:Conditions NotBefore="2018-01-29T12:59:58Z" NotOnOrAfter="2018-01-29T13:05:58Z">
    </saml:Conditions>
</samlp:Response>
```
{: screen}

</br>

## ¿Qué tipo de algoritmos están soportados para las firmas SAML?
{: #saml-signatures}
{: faq}

Puede utilizar cualquiera de los siguientes algoritmos para procesar las firmas digitales XML.

<table>
  <tr>
    <th> Tipo de algoritmo </th>
    <th> Opciones de algoritmo </th>
  </tr>
  <tr>
    <td>Algoritmos de canonicalización y de transformación con y sin comentarios</td>
    <td><ul><li><a href="http://www.w3.org/TR/2001/REC-xml-c14n-20010315" target="_blank">Canonicalización <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></li>
    <li><a href="http://www.w3.org/2001/10/xml-exc-c14n#" target="_blank">Canonicalización exclusiva con y sin comentarios <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></li>
    <li><a href=" http://www.w3.org/2000/09/xmldsig#enveloped-signature" target="_blank">Transformación de Enveloped Signature <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></li></ul></td>
  </tr>
  <tr>
    <td>Algoritmos hash</td>
    <td><ul><li><a href="http://www.w3.org/2000/09/xmldsig#sha1" target="_blank">Resúmenes de SHA1 <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmlenc#sha256" target="_blank">Resúmenes de SHA256 <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmlenc#sha512" target="_blank">Resúmenes de SHA512 <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></li></ul></td>
  </tr>
  <tr>
    <td>Algoritmos de firma</td>
    <td><ul><li><a href="http://www.w3.org/2000/09/xmldsig#rsa-sha1" target="_blank">RSA-SHA1 <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmldsig-more#rsa-sha256" target="_blank">RSA-SHA256 <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmldsig-more#rsa-sha512" target="_blank">RSA-SHA512 <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></li>
    <li><a href="http://www.w3.org/2000/09/xmldsig#hmac-sha1" target="_blank">HMAC-SHA1 <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></li></ul></td>
  </tr>
</table>

Para obtener más información sobre cómo utilizar un proveedor de identidad SAML, consulte [Configuración de proveedores de identidad empresariales](enterprise.html).
