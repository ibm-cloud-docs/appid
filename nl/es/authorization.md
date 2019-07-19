---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-09"

keywords: Authentication, authorization, identity, app security, secure, access, tokens

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

# Conceptos clave
{: #key-concepts}

¿Está confundido sobre las diferencias entre la autorización y la autenticación? No es el único. Consulte la información siguiente para conocer terminología específica, procesos y la forma en que el servicio utiliza las señales.
{: shortdesc}

¿Desea saber más sobre algunos conceptos básicos de la autorización y la autenticación? No busque más. En el siguiente vídeo puede aprender sobre OAuth 2.0, tipos de otorgamiento, OIDC, etc.

<iframe class="embed-responsive-item" id="about-appid-basics" title="Acerca de {{site.data.keyword.appid_short_notm}}" type="text/html" width="640" height="390" src="//www.youtube.com/embed/ndlk-ZhKGXM?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>


## Terminología
{: #terms}

Estos términos clave pueden ayudarle a comprender la forma en que el servicio divide el proceso de autorización y de autenticación.

### OAuth 2
{: #term-oauth}
[OAuth 2.0](https://tools.ietf.org/html/rfc6749){: external} es un protocolo estándar que se utiliza para proporcionar autorización de apps.


### Open ID Connect (OIDC)
{: #term-oidc}

[OIDC](https://openid.net/developers/specs/){: external} es una capa de autenticación que opera con OAuth 2. Cuando utiliza OIDC junto con {{site.data.keyword.appid_short_notm}}, sus credenciales de aplicación le permiten configurar los puntos finales de OAuth. Si utiliza el SDK, los URL de punto final se crean automáticamente. Sin embargo, también puede crear los URL por su cuenta con sus credenciales de servicio. El URL tiene el siguiente formato: punto final de servicio de {{site.data.keyword.appid_short_notm}} + "/oauth/v4" + /tenantID.

Ejemplo:

```
{
  "clientId": "7eba72ef-b913-47b0-b3b6-54358bb69035",
  "tenantId": "8f5aa500-357e-443a-aab6-bf878f852b5a",
  "secret": "OWEzZGM4M2UtZjhlYS00MDI2LTkwNGItNDJmYzViMmU2YzIz",
  "name":testing",
  "oAuthServerUrl": "https://us-south.appid.cloud.ibm.com/oauth/v4/8f5aa500-357e-443a-aab6-bf878f852b5a",
  "profilesUrl": "https://us-south.appid.cloud.ibm.com",
  "discoveryEndpoint": "https://us-south.appid.ibm.cloud.com/oauth/v4/8f5aa500-357e-443a-aab6-bf878f852b5a/.well-known/openid-configuration"
}
```
{: screen}

Con este ejemplo, el URL sería `https://us-south.appid.cloud.ibm.com/oauth/v4/3x176051-a23x-40y4-9645-804943z660q0`. A continuación, añadiría el punto final al que desea realizar una solicitud. Consulte la tabla siguiente para ver algunos puntos finales de ejemplo.

<table>
  <tr>
    <th>Punto final</th>
    <th>Formato</th>
  </tr>
  <tr>
    <td>Autorización</td>
    <td>{oauthServerUrl}/authorization</td>
  </tr>
  <tr>
    <td>Señal</td>
    <td>{oauthServerUrl}/token</td>
  </tr>
  <tr>
    <td>Información de usuario</td>
    <td>{oauthServerUrl}/userinfo</td>
  </tr>
  <tr>
    <td>JWKS</td>
    <td>{oauthServerUrl}/publickeys</td>
  </tr>
</table>

Cuando utiliza el SDK, los URL de punto final se crean automáticamente.
{: note}

### Señales
{: #term-token}

El servicio utiliza tres tipos de señales distintas. Las señales se definen en **Proveedores de identidad > Gestionar** del panel de control de {{site.data.keyword.appid_short}}. Para obtener más información sobre las señales y cómo se utilizan en {{site.data.keyword.appid_short}}, consulte [Gestión de señales](/docs/services/appid?topic=appid-tokens).

* Señales de acceso: representan la autorización y permiten la comunicación con [recursos de fondo](/docs/services/appid?topic=appid-backend). Los recursos están protegidos por filtros de autorización definidos por {{site.data.keyword.appid_short}}.

* Señales de identidad: representan la autenticación y contienen información sobre el usuario.

* Señales de renovación: se pueden utilizar para obtener una nueva señal de acceso sin volver a autenticar al usuario. Mediante el uso de señales para renovación, los usuarios pueden permitir que la aplicación recuerde sus datos, lo que significa que pueden mantener la sesión iniciada. 

### Cabeceras de autorización
{: #term-auth-header}

{{site.data.keyword.appid_short}} cumple con la [especificación de señal de portador](https://tools.ietf.org/html/rfc6750){: external} y utiliza una combinación de señales de acceso e identidad que se envían como una cabecera de autorización HTTP. La cabecera de autorización tiene tres partes distintas separadas con un espacio en blanco. Las señales están codificadas en base64. La señal de identidad es opcional.

Ejemplo:

```
Authorization=Bearer {access_token} [{id_token}]
```
{: screen}


### Estrategia de API
{: #term-api-strategy}

La estrategia de API espera que las solicitudes contengan una cabecera de autorización con una señal de acceso válida. La solicitud también puede incluir una señal de identidad, pero no es obligatorio. Si una señal no es válida o ha caducado, la estrategia de API devuelve un error HTTP 401 que contiene la siguiente cabecera HTTP:
```
Www-Authenticate=Bearer scope="{scope}" error="{error}"
```
{: screen}

Si la solicitud devuelve una señal válida, el control se pasa al siguiente middleware y la propiedad `appIdAuthorizationContext` se inyecta en el objeto de solicitud. Esta propiedad contiene señales de acceso e identidad originales, e información de carga útil descodificada como objetos JSON simples.

### Estrategia de app web
{: #term-web-strategy}

Cuando la estrategia de app web detecta intentos no autorizados de acceso a un recurso protegido, automáticamente redirige el navegador de un usuario a la página de autenticación, que puede estar proporcionada por {{site.data.keyword.appid_short}}. Tras la correcta autenticación, el usuario vuelve al URL de devolución de llamada de la app web. La estrategia de app web obtiene las señales de acceso e identidad y las almacena en una sesión HTTP bajo `WebAppStrategy.AUTH_CONTEXT`. Depende del usuario decidir si desea almacenar las señales de acceso e identidad en la base de datos de la app.

### Separación y cifrado de datos
{: #term-data-encryption}

{{site.data.keyword.appid_short_notm}} almacena y cifra atributos de perfil de usuario. Como servicio multiarrendatario, cada arrendatario tiene una clave de cifrado designada y los datos de usuario de cada uno se cifran únicamente con la clave de dicho arrendatario.

{{site.data.keyword.appid_short_notm}} garantiza que la información privada se cifre antes de que se almacene.
{: note}


### URI de redirección
{: #term-redirect}

{{site.data.keyword.appid_short_notm}} utiliza una lista de URI completos y aprobados para redirigir a los usuarios después de una interacción con la app. Por ejemplo, si el usuario inicia sesión correctamente, {{site.data.keyword.appid_short_notm}} redirige al usuario a la página de inicio de la app o a otra página que especifique. El formato del URI puede cambiar en función de la aplicación. Consulte [Adición de URI de redirección](/docs/services/appid?topic=appid-managing-idp#add-redirect-uri) para obtener más información.


### Conjunto de claves web JSON (JWKS)
{: #term-jwks}

Un JWKS representa un conjunto de claves criptográficas. {{site.data.keyword.appid_short_notm}} utiliza un JWKS para verificar la autenticidad de las señales generadas por el servicio. Al utilizar el ID de clave para verificar la firma, podemos asegurarnos de que la señal ha sido emitida por una fuente fiable {{site.data.keyword.appid_short_notm}}, y que la información dentro de la señal no se ha modificado.


