---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-10"

keywords: authentication, authorization, identity, app security, secure, tokens, jwt, development

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


# Validación de señales
{: #token-validation}

La validación de señales es una parte importante del desarrollo de apps modernas. Mediante la validación de señales, puede proteger la app o las API de usuarios no autorizados. {{site.data.keyword.appid_full}} utiliza señales de identidad y acceso para garantizar que un usuario o app se autentican antes de que se les otorgue acceso. Si está utilizando uno de los SDK proporcionados por {{site.data.keyword.appid_short_notm}}, la obtención y la validación de señales se realizarán en su nombre.
{: shortdesc}

Para obtener más información sobre cómo se utilizan las señales en {{site.data.keyword.appid_short_notm}}, consulte [Comprensión de las señales](/docs/services/appid?topic=appid-tokens#tokens).
{: tip}

Las señales se utilizan para verificar que una persona es quien dice ser. Confirman los permisos de acceso que el usuario puede tener durante un período de tiempo especificado. Cuando un usuario inicia sesión en la aplicación y se emite una señal, la app debe validar el usuario antes de que se le proporcione acceso.

</br>

**¿Qué ocurre si estoy trabajando en un idioma para el que {{site.data.keyword.appid_short_notm}} no dispone de un SDK?**

No se preocupe. Dispone de tres opciones:

* Trabajar con las API de {{site.data.keyword.appid_short_notm}}
* Implementar su propia lógica de validación
* Utilizar un SDK de código abierto compatible con OpenID Connect

Si nos basamos en los comentarios que hemos recibido, la opción 1 es la forma más fácil de solucionar el problema.
{: tip}

</br>
</br>

## Utilización de la API {{site.data.keyword.appid_short_notm}}
{: #remote-validation}

Al utilizar la introspección, puede utilizar {{site.data.keyword.appid_short_notm}} para validar las señales.
{: shortdesc}

1. Envíe una solicitud POST al punto final de API de [/introspect](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Authorization%20Server%20-%20Authorization%20Server%20V4/oauth-server.token) para validar la señal. La solicitud debe proporcionar la señal y una cabecera de autorización básica que contenga el ID de cliente y el secreto.

  Solicitud de ejemplo:

    ```
    POST /oauth/v4/{tenant_id}/introspect HTTP/1.1
    Host: us-south.appid.cloud.ibm.com
    Content-Type: application/x-www-form-urlencoded
    Authorization: Basic jdFlUaGlZUzAwTW0Tjk15TmpFMw==
    Cache-Control: no-cache

    token=XXXXX.YYYYY.ZZZZZ
    ```
    {: screen}

2. El servidor comprueba la caducidad y la firma de la señal y devuelve un objeto JSON que indica si la señal está activa o inactiva.

  Ejemplo de respuesta:

    ```
    {
      "active": true
    }
    ```
    {: screen}


## Validación manual de señales
{: #local-validation}

Puede validar las señales de forma local analizando la señal, verificando la firma de la señal y validando las reclamaciones que se almacenan en la señal.
{: shortdesc}


1. Analice las señales. La [señal web de JSON (JWT)](https://tools.ietf.org/html/rfc7519) es una forma estándar de pasar información de forma segura. Consta de tres partes principales: cabecera, carga útil y firma. Están codificadas en base64URL y separadas por un punto (.). Puede utilizar cualquier decodificador base64URL disponible para analizar la señal. De forma alternativa, puede utilizar cualquiera de las [bibliotecas que aparecen en la lista](https://jwt.io/#libraries-io) para analizar la señal.

  Señal codificada de ejemplo:

    ```
    eyJhbGciOiJSUzI1NiIsInR5cCI6IkpPU0UiLCJraWQiOiJhMmszIn0
    .eyJpc3MiOiJhcHBpZC1vYXV0aCIsImF1ZCI6ImFiYzEyMyIsImV4cCI6MTU2NDU2Nn0
    .IycnAGUmMHzpTWbe-qaRsx0B4Zi-SVav710Fb_8CTCQvLrHX9d42WuCZ5bW
    d-ikgEsf6waQxeBfhfwYxwHN87LZupApagVMZtylVAnXhG1pHu_32wbZsPvg6QjzNO
    j6ys2Lfl3qfb5Qrp9u4IsZltKPEN8HdfeOcKXxpw6UqP-8
    ```
    {: screen}

  Cabecera decodificada de ejemplo:

    ```
    {
      "alg": "RS256",
      "typ": "JOSE",
      "kid": "a2k3"
    }
    ```
    {: screen}

  Carga útil decodificada:

    ```
    {
      "iss": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61",
      "aud": "abc123",
      "exp": 1564566
    }
    ```
    {: screen}

2. Realice una llamada al punto final [/publickeys](https://us-south.appid.cloud.ibm.com/swagger-ui/#!/Authorization_Server_V4/publicKeys) para recuperar las claves públicas. Las claves públicas devueltas tienen el formato de [claves web de JSON (JWK)](https://tools.ietf.org/html/rfc7517).

  Solicitud de ejemplo:

    ```
    GET /oauth/v4/{tenant_id}/publickeys HTTP/1.1
    Host: us-south.appid.cloud.ibm.com
    Cache-Control: no-cache
    ```
    {: screen}

3. Almacene las claves en la memoria caché de la app para su uso futuro. El almacenamiento de claves acelera el proceso e impide el retraso de la red si se realiza otra llamada.

4. Importe los parámetros de clave pública.

  Ejemplo de respuesta:

    ```
    {
      "keys": [
        {
          "kty": "RSA",
          "use": "sig",
          "n": "AsdaE",
          "e": "SDAasw",
          "kid": "ad123dCAz"
        }
      ]
    }
    ```
    {: screen}

  <table>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="Icono de más información"/> Parámetros de clave pública </th>
    </thead>
    <tbody>
      <tr>
        <td><code>kty</code></td>
        <td>Define el algoritmo que se utiliza.</td>
      </tr>
      <tr>
        <td><code>use</code></td>
        <td>Define la finalidad de la clave.</td>
      </tr>
      <tr>
        <td><code>kid</code></td>
        <td>Define el ID exclusivo de la clave.</td>
      </tr>
      <tr>
        <td>Other</td>
        <td>Es posible que haya otros parámetros que sean específicos de su algoritmo que también deban importarse.</td>
      </tr>
    </tbody>
  </table>

5. Verifique la firma de la señal. La cabecera de la señal contiene el algoritmo que se ha utilizado para firmar la señal y el ID de clave o reclamación `kid` de la clave pública coincidente. Puesto que las claves públicas no cambian con frecuencia, puede almacenar en memoria caché claves públicas en la app y renovarlas ocasionalmente. Si a la clave almacenada en caché le falta la reclamación `kid`, puede validar las señales localmente.

  1. Haga que la aplicación verifique que el contenido de la cabecera de señal de entrada coincida con los parámetros de la clave pública.
  2. Compruebe de forma específica que se han utilizado los mismos algoritmos y que la memoria caché de la clave pública contiene una clave con el ID de clave relevante.
  3. Asegúrese de que el valor de hash es el mismo que el de la firma del formulario PEM de la clave pública. El valor hash se puede obtener mediante el hashing y la combinación de la cabecera de la carga útil de la señal. Puesto que el proceso puede ser completo para implementarlo de forma manual, puede resultar útil utilizar una de las [bibliotecas listadas](https://jwt.io/) para validar la firma.

6. Valide las reclamaciones que se almacenan en las señales. Para verificar comprobaciones futuras, puede utilizar [esta lista](http://openid.net/specs/openid-connect-core-1_0.html#IDTokenValidation).
  <table>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="Icono Más información"/> Reclamaciones que deben validarse </th>
    </thead>
    <tbody>
      <tr>
        <td><code>iss</code></td>
        <td>El emisor debe ser el mismo que el del servidor OAuth de {{site.data.keyword.appid_short_notm}}.</td>
      </tr>
      <tr>
        <td><code>exp</code></td>
        <td>La hora actual debe ser inferior a la hora de caducidad.</td>
      </tr>
      <tr>
        <td><code>aud</code></td>
        <td>El público debe contener el ID de cliente de la app.</td>
      </tr>
      <tr>
        <td><code>tenant</code></td>
        <td>El arrendatario debe contener el ID de arrendatario de la app.</td>
      </tr>
      <tr>
        <td><code>scope</code></td>
        <td>El ámbito de permisos que se otorga al usuario. Es específico de la señal de acceso.</td>
      </tr>
    </tbody>
  </table>
