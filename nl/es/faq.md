---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

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

Un suceso de autenticación ocurre cuando se emite una señal nueva de {{site.data.keyword.appid_short_notm}}. Para los usuarios identificados, cada nueva señal es válida durante una hora. Las señales anónimas son válidas durante un mes. Cuando la señal caduca debe crear una nueva para acceder a los recursos protegidos. Cuando se utilice {{site.data.keyword.appid_short_notm}} para la autenticación móvil, las señales del usuario se almacenarán en `key-store/key-chain` y se añadirán a cada solicitud futura. Las señales son accesibles utilizando el SDK de Swift de Android o iOS de {{site.data.keyword.appid_short_notm}}. Cuando utiliza el servicio para la autenticación web, <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">almacene la señal de usuario <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> en las cookies de sesión.

### Usuarios autorizados

Un usuario autorizado es un usuario exclusivo que inicia sesión con su servicio directa o indirectamente. Se le factura un usuario autorizado cada vez que un nuevo usuario inicia sesión desde cada proveedor de identidad, incluyendo los usuarios anónimos. Por ejemplo, si un usuario inicia sesión con Facebook y más adelante con Google, se consideran dos usuarios autorizados diferentes.

Para obtener más información sobre los precios por nivel graduado, consulte los [documentos de precios de {{site.data.keyword.Bluemix_notm}}](/docs/billing-usage/how_charged.html#services).

</br>

## ¿Qué tipo de actividad está supervisada por {{site.data.keyword.appid_short_notm}}?
{: #activity-monitor}

Puede realizar el seguimiento de la actividad que se ha generado dentro de la app que está enlazada con la instancia de servicio. También puede supervisar la actividad administrativa que se realiza en {{site.data.keyword.appid_short_notm}} utilizando el servicio {{site.data.keyword.cloudaccesstrailshort}}.

Para ver la actividad generada por su app:

1. Inicie sesión en su cuenta de {{site.data.keyword.Bluemix_notm}}.
2. Desde el panel de control, seleccione su instancia de {{site.data.keyword.appid_short_notm}}.
3. Pulse el separador **Visión general**.
4. Visualice la actividad listada en el **Registro de actividad**.

</br>
Para supervisar la actividad administrativa:

1. Inicie sesión en su cuenta de {{site.data.keyword.Bluemix_notm}}. Vaya a la organización y al espacio donde ha suministrado la instancia de {{site.data.keyword.appid_short_notm}}.
2. Desde el catálogo, suministre una instancia del servicio de {{site.data.keyword.cloudaccesstrailshort}}. Asegúrese de estar en el mismo espacio que la instancia de {{site.data.keyword.appid_short_notm}}.
3. En el panel de control de {{site.data.keyword.cloudaccesstrailshort}}, pulse el separador **Gestionar**.
4. En la lista desplegable, seleccione las configuraciones siguientes para buscar todos los sucesos generados por {{site.data.keyword.appid_short_notm}}.
<table>
  <tr>
    <th> Campo </th>
    <th> Configuración </th>
  </tr>
  <tr>
    <td>Ver registros</td>
    <td>Registros de espacio</td>
  </tr>
  <tr>
    <td>Buscar</td>
    <td>target.name</td>
  </tr>
  <tr>
    <td>Filtro</td>
    <td>appid</td>
  </tr>
</table>
5. Pulse **Filtrar**.

Consulte la [documentación de {{site.data.keyword.cloudaccesstrailshort}}](/docs/services/cloud-activity-tracker/index.html) para obtener más información sobre cómo funciona el servicio.

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
