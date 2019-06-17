---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-20"

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

Si tiene un proveedor de identidad basado en SAML, puede configurar {{site.data.keyword.appid_short_notm}} para que actúe como proveedor de servicios que inicia un inicio sesión en un proveedor de terceros de tipo inicio de sesión único (SSO). Durante el flujo de inicio de sesión, los usuarios se pueden autenticar fácilmente y pueden obtener señales de seguridad de {{site.data.keyword.appid_short_notm}} que les permitan acceder a las apps y las API protegidas.
{: shortdesc}

 
¿Trabaja con un proveedor de identidad SAML específico? Consulte estas publicaciones de blog sobre cómo configurar {{site.data.keyword.appid_short_notm}} con [Ping One ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/cloud/blog/setting-ibm-cloud-app-id-ping-one), con [un Azure Active Directory ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/cloud/blog/setting-ibm-cloud-app-id-azure-active-directory) o con [un Active Directory Federation Service ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/cloud/blog/setting-ibm-cloud-app-id-active-directory-federation-service).
{: tip}


## SAML
{: #saml-understanding}

Security Assertion Markup Language (SAML) es un estándar abierto para intercambiar datos de autenticación y de autorización entre un proveedor de identidad que certifique la identidad del usuario y un proveedor de servicio que consuma la información de identidad de usuario.
{: shortdesc}

El protocolo <a href="http://saml.xml.org/saml-specifications" target="blank">SAML <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> admite perfiles distintos y opciones de enlace. {{site.data.keyword.appid_short_notm}} admite el perfil SSO del navegador web, con el enlace HTTP Post.

### ¿Cuál es la base técnica de los flujos?
{: #saml-tech-basis}

SAML 2.0 es una de las infraestructuras más establecidas para los estándares de autenticación y autorización. Es un protocolo basado en XML entre un proveedor de servicios ({{site.data.keyword.appid_short_notm}}) y un proveedor de identidad. Cuando un proveedor de identidad autentica a un usuario, crea señales SAML, que contienen aserciones o sentencias sobre el usuario. Las sentencias pueden contener:

- información de autenticación como la forma en que se ha autenticado el usuario (una contraseña, MFA, etc.).
- atributos asociados al usuario: el grupo al que pertenece.
- decisiones de autorización que declaran si el usuario tiene permiso para realizar una acción determinada en un recurso determinado.

Cuando se devuelven las aserciones a {{site.data.keyword.appid_short_notm}}, el servicio federa la identidad de usuario y se generan las señales adecuadas. Si la aserción SAML se corresponde a una de las siguientes reclamaciones de OIDC, se añade automáticamente a la señal de identidad.  Si uno o varios de estos valores cambian en el lado del proveedor, los nuevos valores estarán disponibles solo después de que el usuario inicie sesión de nuevo.

 * `nombre`
 * `correo electrónico`
 * `entorno local`
 * `imagen`

Las aserciones que no se corresponden con ninguno de los nombres estándar se omiten de forma predeterminada, pero si el proveedor de SAML devuelve otras aserciones, es posible obtener la información cuando un usuario inicia sesión. Creando una matriz de las aserciones que desea utilizar, puede [inyectar la información en las señales](/docs/services/appid?topic=appid-customizing-tokens#customizing-tokens). Sin embargo, asegúrese de no añadir más información de la necesaria a las señales. Las señales normalmente se envían en las cabeceras http, que tienen un tamaño limitado.
{: tip}

### ¿Qué aspecto tiene el flujo?
{: #saml-flow}

Aunque {{site.data.keyword.appid_short_notm}} y el proveedor de identidad utilicen la infraestructura de SAML para autenticar el usuario, {{site.data.keyword.appid_short_notm}} sigue utilizando la infraestructura OAuth 2.0/ OIDC más moderna para intercambiar señales de seguridad con la aplicación. Consulte la imagen siguiente para ver un flujo de información detallado.

![Flujo de autenticación de empresa de SAML](/images/ibmid-flow.png)

1. Un usuario accede a la página de inicio de sesión o a un recurso restringido en su aplicación, que inicia una solicitud en el punto final de {{site.data.keyword.appid_short_notm}} `/authorization` a través de un SDK o una API de {{site.data.keyword.appid_short_notm}}. Si el usuario no está autorizado, el flujo de autenticación empieza con una redirección a {{site.data.keyword.appid_short_notm}}.
2. {{site.data.keyword.appid_short_notm}} genera una solicitud de autenticación de SAML (AuthNRequest) y el navegador redirige automáticamente al usuario al proveedor de identidad de SAML.
3. El proveedor de identidad analiza la solicitud SAML, autentica al usuario y genera una respuesta SAML con sus aserciones.
4. El proveedor de identidad redirige al usuario y la respuesta de vuelta a {{site.data.keyword.appid_short_notm}} con la respuesta SAML.
5. Si la autenticación es satisfactoria, {{site.data.keyword.appid_short_notm}} crea señales de acceso y de identidad que representan la autorización y la autenticación de un usuario y las devuelve a la app. SI la autenticación falla, {{site.data.keyword.appid_short_notm}} devuelve el código de error del proveedor de identidad a la app.
6. El usuario tiene otorgado el acceso a la app o a los recursos protegidos.



### ¿El SSO cambia el flujo?
{: #saml-sso-flow}

El perfil de SSO del navegador web que implementa {{site.data.keyword.appid_short_notm}} lo inicia un proveedor de servicios, lo que significa que {{site.data.keyword.appid_short_notm}} debe enviar una solicitud SAML al proveedor de identidad para iniciar la sesión de autenticación. 

{{site.data.keyword.appid_short_notm}} no da soporte actualmente a los flujos iniciados por el proveedor de identidad y no se deben utilizar con el servicio en este momento.
{: note}

Si su proveedor de identidad admite SSO, es posible que la autenticación SAML utilice la sesión de SSO ya establecida para autenticar al usuario. Si no lo hace, el usuario se redirige a una página de inicio de sesión. Puede que se redirijan si el proveedor de identidad no puede hacer coincidir los requisitos de autenticación que se definen en la solicitud de autenticación de {{site.data.keyword.cloud_notm}} con lo que utiliza para establecer el SSO. Por ejemplo, si el proveedor de identidad establece una sesión de SSO de usuario utilizando biometría, se debe cambiar el contexto de autenticación predeterminado de {{site.data.keyword.appid_short_notm}}. De forma predeterminada, {{site.data.keyword.appid_short_notm}} espera que los usuarios se autentiquen con una contraseña sobre HTTPS: `urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport`.



## Configuración de SAML para funcionar con {{site.data.keyword.appid_short_notm}}
{: #saml-configure}

Puede configurar SAML para que funcione con {{site.data.keyword.appid_short_notm}} proporcionando metadatos de {{site.data.keyword.appid_short_notm}} a su proveedor de identidad y metadatos del proveedor de identidad a {{site.data.keyword.appid_short_notm}}.



### Suministro de metadatos a su proveedor de identidad
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
      <td>Forma en la que el proveedor de identidad sabe qué formato de identificador necesita para enviarlo en el asunto de una aserción y cómo {{site.data.keyword.appid_short_notm}} identifica a los usuarios. El ID debería tener el formato siguiente: <code><saml:NameID Format="urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress"/></code></td>
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



### Suministro de metadatos a {{site.data.keyword.appid_short_notm}}
{: #saml-provide-appid}

Obtenga datos del proveedor de identidad y proporciónelos a {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

**Suministro de metadatos con la GUI** 

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
      <td><code>Certificado para firmas</code></td>
      <td>Certificado emitido por el proveedor de identidad SAML. Se utiliza para firmar y validar aserciones SAML. Todos los proveedores son distintos, pero podría descargar el certificado de firma desde el proveedor de identidad. El certificado debe estar en formato <code>.pem</code>.</td>
    </tr>
  </table>

2. Opcional: Proporcione un **Certificado secundario** que se utilice si la validación de firma falla en el certificado primario. Si la clave de firma sigue siendo la misma, {{site.data.keyword.appid_short_notm}} no bloquea la autenticación de certificados caducados.
3. Actualice el **Nombre de proveedor** y pulse **Guardar**. El nombre predeterminado es SAML.

¿Desea establecer un contexto de autenticación? Puede hacerlo a través de la API.
{: tip}

</br>

**Suministro de metadatos con la API**

1. Para visualizar la configuración de SAML actual, incluyendo el contexto de autenticación y los certificados, realice una solicitud GET en el [punto final de API `/saml`](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.get_saml_idp).

  Código de ejemplo:
  ```
  curl --request GET \
  https://us-south.appid.cloud.ibm.com/management/v4/<tenant-ID>/config/idps/saml \
  --header `Accept: application/json`
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
    }
  }
  ```
  {: screen}

2. Cree la configuración de SAML sustituyendo los valores del ejemplo siguiente por la información de su proveedor. Los valores que se muestran en el ejemplo son los obligatorios, pero puede elegir incluir más información, como se muestra en la tabla.

  ```
  "config": {
    "authnContext": {
      "class": [
        "urn:oasis:names:tc:SAML:2.0:ac:classes:YourChosenClassValue",
          "urn:oasis:names:tc:SAML:2.0:ac:classes:YourOtherChosenClassValue"
      ],
      "comparison": "sampleComparisonValue"}
    "entityID": "https://example.com/saml2/metadata/706634",
    "signInUrl": "https://example.com/saml2/sso-redirect/706634",
    "certificates": [
      "primary-certificate-example-pem-format"
        "secondary-certificate-example-pem-format"
    ],
    "displayName": "my saml example",
  }
  ```
  {: codeblock}
  {: #configuring-saml-new}

  <table>
    <tr>
      <th> Variable </th>
      <th> Descripción </th>
    </tr>
    <tr>
      <td><code>signInUrl</code></td>
      <td>El URL al que se redirige el usuario para su autenticación. Se aloja mediante el proveedor de identidad SAML.</td>
    </tr>
    <tr>
      <td><code>entityID</code></td>
      <td>Nombre exclusivo globalmente para un proveedor de identidad SAML.</td>
    </tr>
    <tr>
      <td><code>displayName</code></td>
      <td>El nombre que asigna a la configuración de SAML.</td>
    </tr>
    <tr>
      <td><code>primary-certificate-example-pem-format</code></td>
      <td>El certificado emitido por el proveedor de identidad de SAML. Se utiliza para firmar y validar aserciones SAML. Todos los proveedores son distintos, pero podría descargar el certificado de firma desde el proveedor de identidad. El certificado debe estar en formato <code>.pem</code>.</td>
    </tr>
    <tr>
      <td>Opcional: <code>secondary-certificate-example-pem-format</code></td>
      <td>El certificado de copia de seguridad emitido por el proveedor de identidad de SAML. Se utiliza si la validación de firma falla con el certificado primario. <strong>Nota</strong>: Si la clave de firma sigue siendo la misma, {{site.data.keyword.appid_short_notm}} no bloquea la autenticación de certificados caducados.</td>
    </tr>
    <tr>
      <td>Opcional: <code>authnContext</code></td>
      <td>El contexto de autenticación se utiliza para verificar la calidad de la autenticación y de las aserciones SAML. Puede añadir un contexto de autenticación añadiendo una matriz de clase y una serie de comparación al código. ASEGÚRESE de actualizar los parámetros <code>class</code> y <code>comparison</code> con sus valores. Por ejemplo, el parámetro <code>class</code> podría ser algo como <code>urn:oasis:names:tc:SAML:2.0:ac:classes:YourChosenClassValue</code>.</td>
    </tr>
  </table>

3. Haga una solicitud PUT al [punto final de API `/saml`](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp) para proporcionar la configuración que ha creado en el paso 2 a {{site.data.keyword.appid_short_notm}}. Consulte el ejemplo siguiente ver cómo podría ser su solicitud.

  ```
  curl --request PUT \
  https://us-south.appid.cloud.ibm.com/management/v4/<tenant-ID>/config/idps/saml \
  --header `Accept: application/json` \
  --data \
  {
    "isActive": true,
    "config": {
      "entityID": "https://example.com/saml2/metadata/706634",
      "signInUrl": "https://example.com/saml2/sso-redirect/706634",
      "certificates": [
        "primary-certificate-example-pem-format"
      ],
      "displayName": "my saml example",
    }
  }
  ```
  {: screen}



## Probar la configuración
{: #saml-testing}

Puede probar la configuración entre el proveedor de identidad SAML y {{site.data.keyword.appid_short_notm}}.

1. Asegúrese de que haya guardado la configuración.
2. Vaya al separador **SAML 2.0** del panel de control de {{site.data.keyword.appid_short_notm}} y pulse **Probar**. Se abre un nuevo separador.
3. Inicie sesión con un usuario que ya haya autenticado su proveedor de identidad.
4. Después de completar el formulario, se le redirigirá a otra página.
  * Autenticación correcta: La conexión entre {{site.data.keyword.appid_short_notm}} y el proveedor de identidad funciona correctamente. La página muestra [señales de acceso y de identidad](/docs/services/appid?topic=appid-tokens#tokens) válidas.
  * Error de autenticación: La conexión se ha bloqueado. La página muestra los errores y el archivo XML de la respuesta SAML.


¿Tiene problemas? Consulte [Resolución de problemas: SAML](/docs/services/appid?topic=appid-troubleshooting-idp#troubleshooting-idp).
{: tip}




## Preguntas más frecuentes de SAML
{: #saml-assertions}

Las aserciones SAML se pueden devolver de formas diferentes. Consulte los ejemplos siguientes para ver el formato que {{site.data.keyword.appid_short_notm}} espera en la respuesta.
{: shortdesc}


### ¿Cómo espera {{site.data.keyword.appid_short_notm}} que sea una aserción SAML?
{: #saml-example}

El servicio espera que una aserción SAML sea similar a la del ejemplo siguiente.

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

