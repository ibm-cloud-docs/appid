---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

keywords: authentication, authorization, identity, app security, secure, custom, service provider, identity provider, enterprise, assertions

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

# SAML
{: #enterprise}

Security Assertion Markup Language (SAML) es un estándar abierto para intercambiar datos de autenticación y de autorización entre un proveedor de identidad que certifique la identidad del usuario y un proveedor de servicio que consuma la información de identidad de usuario.
{: shortdesc}

{{site.data.keyword.appid_short_notm}} funciona como un proveedor de servicio e inicia un inicio de sesión único (SSO) en un proveedor de terceros como Active Directory Federation Services. El protocolo <a href="http://saml.xml.org/saml-specifications" target="blank">SAML <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> admite perfiles distintos y opciones de enlace. {{site.data.keyword.appid_short_notm}} admite el perfil SSO del navegador web, con el enlace HTTP Post.

Para ver los pasos sobre cómo utilizar un proveedor de identidad SAML específico, consulte estas publicaciones de blog sobre la configuración de {{site.data.keyword.appid_short_notm}} con [Ping One ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-ping-one/), [Azure Active Directory ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-azure-active-directory/) o [Active Directory Federation Service ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-active-directory-federation-service/).
{: tip}



## Visión general de las aserciones
{: #saml-assertions}

Una aserción SAML es similar a un [atributo de usuario](/docs/services/appid?topic=appid-user-profile#user-profile). Se trata de una sentencia o información acerca de un usuario que un proveedor de identidad devuelve a {{site.data.keyword.appid_short_notm}} cuando un usuario inicia sesión correctamente en la app. En función de la configuración de la app y del proveedor de identidad que utilice, la información puede incluir un nombre de usuario, correo electrónico u otro campo que se le solicite.
{: shortdesc}

Cuando las aserciones se devuelven a {{site.data.keyword.appid_short_notm}}, el servicio unifica la identidad de usuario. Si la aserción SAML se corresponde a una de las siguientes reclamaciones de OIDC, se añade automáticamente a la señal de identidad.  Si uno o varios de estos valores cambian en el lado del proveedor, los nuevos valores estarán disponibles solo después de que el usuario inicie sesión de nuevo.

 * `nombre`
 * `correo electrónico`
 * `entorno local`
 * `imagen`

Las aserciones que no se corresponden con ninguno de los nombres estándar se omiten de forma predeterminada, pero si el proveedor de SAML devuelve otras aserciones, es posible obtener la información cuando un usuario inicia sesión. Creando una matriz de las aserciones que desea utilizar, puede [inyectar la información en las señales](/docs/services/appid?topic=appid-customizing-tokens#customizing-tokens). Sin embargo, asegúrese de no añadir más información de la necesaria a las señales. Las señales normalmente se envían en las cabeceras http, que tienen un tamaño limitado.
{: tip}

### ¿A qué espera {{site.data.keyword.appid_short_notm}} que se parezca una aserción SAML?
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


### ¿Qué tipos de algoritmos admite {{site.data.keyword.appid_short_notm}}?
{: #saml-signatures}

{{site.data.keyword.appid_short_notm}} utiliza el algoritmo <a href="http://www.w3.org/2001/04/xmldsig-more#rsa-sha256" target="_blank">RSA-SHA256 <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> para procesar las firmas digitales XML.




## Suministro de metadatos a su proveedor de identidad
{: #saml-provide-idp}

Para configurar la app, debe proporcionar información a un proveedor de identidad compatible con SAML. La información se intercambia mediante un archivo XML de metadatos que también contiene datos de configuración que se utilizan para establecer la confianza.
{: shortdesc}

No puede habilitar SAML si no lo configura primero como proveedor de identidad.
{: tip}

1. En el separador **Gestionar** del panel de control de {{site.data.keyword.appid_short_notm}}, pulse **Editar** en la fila **SAML** para configurar los valores.
2. Pulse **Descargar archivo de metadatos SAML**. El proveedor de identidad espera la información siguiente del archivo.
  <table>
    <tr>
      <th> Variable </th>
      <th> Descripción </th>
    </tr>
    <tr>
      <td><code>ID de entidad</code></td>
      <td>El identificador que permite al proveedor de identidad saber que {{site.data.keyword.appid_short_notm}} ha emitido la solicitud SAML.</td>
    </tr>
    <tr>
      <td><code>URL de ubicación</code></td>
      <td>La ubicación que el proveedor de identidad envía a las aserciones de SAML tras autenticar correctamente un usuario.</td>
    </tr>
    <tr>
      <td><code>Enlace</code></td>
      <td>Instrucciones sobre cómo debería enviar el proveedor de identidad la respuesta SAML.</td>
    </tr>
    <tr>
      <td><code>Formato de ID de nombre</code></td>
      <td>Forma en la que el proveedor de identidad sabe qué formato de identificador necesita para enviarlo en el asunto de una aserción. La forma en que {{site.data.keyword.appid_short_notm}} identifica a los usuarios.</td>
    </tr>
    <tr>
      <td><code>WantAssertionsSigned</code></td>
      <td>Forma en la que un proveedor de identidad comprueba para ver si necesita firmar la aserción. El servicio espera a que se firme la aserción, pero no da soporte a las aserciones cifradas.</td>
    </tr>
  </table>

3. Proporcione los datos a su proveedor de identidad. Si el proveedor de identidad permite cargar el archivo de metadatos, puede hacerlo. Si no lo permite, configure las propiedades manualmente. No todos los proveedores de identidad utilizan las mismas propiedades, por lo que es posible que no las utilice todas.

  Los nombres de propiedades pueden diferir entre los proveedores de identidad.
  {: tip}

4. Cambie **SAML 2.0 Federation** a **Habilitado**.

## Suministro de metadatos a {{site.data.keyword.appid_short_notm}}
{: #saml-provide-appid}

Obtenga datos del proveedor de identidad y proporciónelos a {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

### Suministro de metadatos con la GUI
{: #saml-provide-gui}

1. Vaya al separador **SAML 2.0** del panel de control de {{site.data.keyword.appid_short_notm}}. Entre los metadatos siguientes que ha obtenido del proveedor de identidad en la sección **Proporcionar metadatos de IdP SAML**.
  <table>
    <tr>
      <th> Variable </th>
      <th> Descripción </th>
    </tr>
    <tr>
      <td><code>URL de inicio de sesión</code></td>
      <td>El URL al que se redirige el usuario para su autenticación. Se aloja mediante el proveedor de identidad SAML.</td>
    </tr>
    <tr>
      <td><code>ID de entidad</code></td>
      <td>Nombre exclusivo globalmente para un proveedor de identidad SAML.</td>
    </tr>
    <tr>
      <td><code>Certificado de firma</code></td>
      <td>Certificado emitido por el proveedor de identidad SAML. Se utiliza para firmar y validar aserciones SAML. Todos los proveedores son distintos, pero podría descargar el certificado de firma desde el proveedor de identidad. El certificado debe estar en formato <code>.pem</code>.</td>
    </tr>
  </table>

2. Opcional: Proporcione un **Certificado secundario** que se utilice si la validación de firma falla en el certificado primario. Si la clave de firma sigue siendo la misma, {{site.data.keyword.appid_short_notm}} no bloquea la autenticación de certificados caducados.
3. Actualice el **Nombre de proveedor** y pulse **Guardar**. El nombre predeterminado es SAML.

¿Desea establecer un contexto de autenticación? Puede hacerlo a través de la API.
{: tip}


### Suministro de metadatos con la API
{: #saml-provide-api}

1. Obtenga metadatos de SAML realizando una solicitud GET en el punto final de la API [/getSamlMetadata](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.get_saml_idp).

  Código de ejemplo:
  ```
  <?xml version="1.0"?>
  <getSamlMetadata>
    <?xml version="1.0"?> <EntityDescriptor> <SPSSODescriptor> <NameIDFormat> </NameIDFormat> <AssertionConsumerService /> </SPSSODescriptor>
   </EntityDescriptor>
    </getSamlMetadata>
  ```
  {: codeblock}

  Salida de ejemplo:
  ```
    {
    "isActive": true,
    "config": {
      "entityID": "https://example.com/saml2/metadata/706634",
      "signInUrl": "https://example.com/saml2/sso-redirect/706634",
      "certificates": [
        "certificate-example-pem-format"
      ],
      "displayName": "my saml example",
      "authnContext": {
        "class": [
          "urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport"
        ],
        "comparison": "exact"
      }
    },
    "validation_data": {
      "certificates": [
        {
          "certificate_index": 0,
          "expiration_timestamp": 1674473996,
          "warning": "Your certificate will expire in 18 days."
        }
      ]
    }
  }
  ```
  {: screen}

2. Configure la solicitud POST en el punto final de la API [/set_saml_idp](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp).

  1. En el ejemplo de metadatos siguiente, sustituya las variables con su propia información.

    ```
    Put {Management URI}/config/idps/saml
    Content-Type: application/json
    {
      "isActive": true,
      "config": {
        "entityID": "https://example.com/saml2/metadata/706634",
        "signInUrl": "https://example.com/saml2/sso-redirect/706634",
        "certificates": [
          "primary-certificate-example-pem-format"
        ],
        "displayName": "my saml example"
      }
    }
    ```
    {: codeblock}

    <table>
      <tr>
        <th> Variable </th>
        <th> Descripción </th>
      </tr>
      <tr>
        <td><code>URL de inicio de sesión</code></td>
        <td>El URL al que se redirige el usuario para su autenticación. Se aloja mediante el proveedor de identidad SAML.</td>
      </tr>
      <tr>
        <td><code>ID de entidad</code></td>
        <td>Nombre exclusivo globalmente para un proveedor de identidad SAML.</td>
      </tr>
      <tr>
        <td><code>Certificado de firma</code></td>
        <td>Certificado emitido por el proveedor de identidad SAML. Se utiliza para firmar y validar aserciones SAML. Todos los proveedores son distintos, pero podría descargar el certificado de firma desde el proveedor de identidad. El certificado debe estar en formato <code>.pem</code>.</td>
      </tr>
    </table>

  2. Opcional: Añada un certificado secundario a la matriz de certificados siguiendo el certificado primario. El certificado secundario se utiliza si la validación de firma falla con el certificado primario. Si la clave de firma sigue siendo la misma, {{site.data.keyword.appid_short_notm}} no bloquea la autenticación de certificados caducados.

    Ejemplo:
    ```
    {
      "isActive": true,
      "config": {
        ...
        "certificates": [
          "primary-certificate-example-pem-format",
          "secondary-certificate-example-pem-format"
        ],
        ...
      }
    }
    ```
    {: screen}
  {: #configuring-saml-new}
  3. Opcional: Añada un contexto de autenticación añadiendo una matriz de clase y una serie de comparación al código. Asegúrese de actualizar los parámetros `class` y `comparison` con los valores. Un contexto de autenticación se utiliza para verificar la calidad de la autenticación y las aserciones SAML.

    Ejemplo:
    ```
    {
      "isActive": true,
      "config": {
        ...
        "authnContext": {
          "class": [
            "urn:oasis:names:tc:SAML:2.0:ac:classes:YourChosenClassValue",
            "urn:oasis:names:tc:SAML:2.0:ac:classes:YourOtherChosenClassValue"
          ],
          "comparison": "sampleComparisonValue"
        }
      }
    }
    ```
    {: screen}

3. Realice la solicitud. Si ha elegido añadir los valores opcionales, la solicitud debe tener un aspecto similar al del ejemplo siguiente.

  ```
  Put {Management URI}/config/idps/saml
  Content-Type: application/json
  {
    "isActive": true,
    "config": {
      ...
      "authnContext": {
        "class": [
          "urn:oasis:names:tc:SAML:2.0:ac:classes:YourChosenClassValue",
          "urn:oasis:names:tc:SAML:2.0:ac:classes:YourOtherChosenClassValue"
        ],
        "comparison": "sampleComparisonValue"
      "entityID": "https://example.com/saml2/metadata/706634",
      "signInUrl": "https://example.com/saml2/sso-redirect/706634",
      "certificates": [
        "primary-certificate-example-pem-format"
        "secondary-certificate-example-pem-format"
      ],
      "displayName": "my saml example"
    }
  }
  ```
  {: codeblock}


## Probar la configuración
{: #saml-testing}

Puede probar la configuración entre el proveedor de identidad SAML y {{site.data.keyword.appid_short_notm}}.

1. Asegúrese de que haya guardado la configuración.
2. Vaya al separador **SAML 2.0** del panel de control de {{site.data.keyword.appid_short_notm}} y pulse **Probar**. Se abre un nuevo separador.
3. Inicie sesión con un usuario que ya haya autenticado su proveedor de identidad.
4. Después de completar el formulario, se le redirigirá a otra página.
  * Autenticación correcta: La conexión entre {{site.data.keyword.appid_short_notm}} y el proveedor de identidad funciona correctamente. La página muestra [señales de acceso y de identidad](/docs/services/appid?topic=appid-tokens#tokens) válidas.
  * Error de autenticación: La conexión se ha bloqueado. La página muestra los errores y el archivo XML de la respuesta SAML.


¿Tiene problemas? Consulte [Resolución de problemas de las configuraciones del proveedor de identidad](/docs/services/appid?topic=appid-troubleshooting-idp#troubleshooting-idp).
{: tip}
