---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}


# Preguntas más frecuentes (FAQ)

Estas preguntas más frecuentes proporcionan respuestas a preguntas comunes sobre el servicio de {{site.data.keyword.appid_full}}.
{: shortdesc}


## ¿Cómo calcula {{site.data.keyword.appid_short_notm}} los precios?
{: #pricing}

Con {{site.data.keyword.appid_short_notm}} paga menos cuantos más recursos utiliza.
{: shortdesc}

El plan de niveles graduado consta de dos partes: El número de sucesos de autenticación y el de usuarios autorizados. Se le facturará cada mes en función del resumen de las dos partes. El precio total es el cargo acumulado de cada nivel de uso que consiste en la cantidad multiplicada por el precio unitario en ese nivel.

### Sucesos de autenticación

Se produce un suceso de autenticación cuando se emite una nueva señal de acceso, normal o anónima. Para los usuarios identificados, cada nueva señal de acceso es válida de forma predeterminada durante 1 hora (ya sea mediante la autenticación de usuario real o mediante señales de renovación). Las señales anónimas son válidas de forma predeterminada durante 1 mes. Cuando la señal caduca debe crear una nueva para acceder a los recursos protegidos. Puede actualizar la hora de caducidad de las señales de {{site.data.keyword.appid_short_notm}} en la página **Caducidad de inicio de sesión** en el panel de control de {{site.data.keyword.appid_short_notm}}.

Cuando se utiliza {{site.data.keyword.appid_short_notm}} en aplicaciones móviles, las señales se almacenan en el almacén de claves o en la cadena de claves y se añaden a cada solicitud futura. Se puede acceder a las señales utilizando el SDK de Android o iOS de App ID. Cuando se utiliza {{site.data.keyword.appid_short_notm}} en aplicaciones web, se recomienda almacenar las señales en las cookies de sesión de aplicación.


### Usuarios autorizados

Un usuario autorizado es un usuario exclusivo que inicia sesión con su servicio directa o indirectamente. Se le factura un usuario autorizado cada vez que un nuevo usuario inicia sesión desde cada proveedor de identidad, incluyendo los usuarios anónimos. Por ejemplo, si un usuario inicia sesión con Facebook y más adelante con Google, se consideran dos usuarios autorizados diferentes.

Para obtener más información sobre los precios por nivel graduado, consulte los [documentos de precios de {{site.data.keyword.Bluemix_notm}}](/docs/billing-usage/how_charged.html#services).

</br>


## ¿Cómo funciona el cifrado en {{site.data.keyword.appid_short_notm}}?
{: #encryption}

Consulte la tabla siguiente para obtener respuestas a las preguntas más frecuentes sobre el cifrado.

<table>
  <thead>
    <th colspan=2><img src="images/idea.png" alt="Icono de más información"/>  </th>
  </thead>
  <tbody>
    <tr>
      <td>¿Por qué se utiliza el cifrado?</td>
      <td>El servicio cifra los datos del cliente en reposo.</td>
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
      <td>Las claves se generan y luego se almacenan localmente después de ser cifradas utilizando una clave maestra que es específica de cada región. Las claves maestras se almacenan en {{site.data.keyword.keymanagementserviceshort}}.</td>
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
