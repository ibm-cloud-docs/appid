---

copyright:
  years: 2017
lastupdated: "2017-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


# Autorización y autenticación
{: authorization}

La autorización es el proceso mediante el cual puede otorgar acceso a sus apps. El servicio de {{site.data.keyword.appid_short}} utiliza señales, filtros y una cabecera para autenticar usuarios.
{: shortdesc}


## Identidad OAuth
{: #oauth}

Cuando el servicio llama a la API de inicio de sesión de OAuth, {{site.data.keyword.appid_short_notm}} utiliza los protocolos OAuth 2.0 y OIDC para autorizar y autenticar al interlocutor con un proveedor de identidad seleccionado. Tras la autenticación, la identidad se asocia con un registro de usuario de {{site.data.keyword.appid_short_notm}}. {{site.data.keyword.appid_short_notm}} devuelve una señal de acceso que se puede utilizar para acceder a los atributos de usuario, y una señal de identidad que contiene la información de identidad proporcionada por el proveedor de identidad. Se puede volver a acceder al mismo registro de usuario y sus atributos desde cualquier cliente que se autentique con esta misma identidad.

## Señales de identidad y de acceso

{{site.data.keyword.appid_short}} utiliza dos tipos de señales: acceso e identidad.
{:shortdesc}

**Nota**: Las señales están formateadas como <a href="https://jwt.io/introduction/" target="_blank">Señales web JSON <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.


### Señal de acceso
{: #access-tokens}

Las señales de acceso permiten la comunicación con [recursos de fondo](/docs/services/appid/protecting-resources.html) que están protegidos por filtros de autorización definidos por ID de app. La señal se ajusta a las especificaciones de JOSE (JavaScript Object Signing and Encryption).

Señal de ejemplo:

```
Header: {
    "typ": "JOSE",
    "alg": "RS256",
}
Payload: {
    "iss": "appid-oauth.ng.bluemix.net",
    "exp": "1495562664",
    "aud": "a3b87400-f03b-4956-844e-a52103ef26ba",
    "amr": ["facebook"],
    "sub": "de6a17d2-693d-4a43-8ea2-2140afd56a22",
    "iat": "1495559064",
    "tenant": "9781974b-6a1c-46c3-aebf-32b7e9bbbaee",
    "scope": "appid_default appid_readprofile appid_readuserattr appid_writeuserattr",
}
```
{:screen}

<table>
<caption> Tabla 1. Explicación de componentes de señal de acceso </caption>
  <tr>
    <th> Componente </th>
    <th> Descripción </th>
  </tr>
  <tr>
    <td><i> typ </i></td>
    <td> El tipo de cabecera, especificado como "JOSE". </td>
  </tr>
  <tr>
    <td><i> alg </i></td>
    <td> El algoritmo utilizado, especificado como "RS256". </td>
  </tr>
  <tr>
    <td><i> iss </i></td>
    <td> El servidor de {{site.data.keyword.appid_short}} que ha emitido la señal, especificado como serie o como URL. </td>
  </tr>
  <tr>
    <td><i> sub </i></td>
    <td> El ID del usuario para el que se ha emitido la señal. </td>
  </tr>
  <tr>
    <td><i> aud </i></td>
    <td> El ID de cliente para el que está pensada la señal. </td>
  </tr>
  <tr>
    <td><i> exp </i></td>
    <td> La hora a la que caduca la indicación de fecha y hora, especificada en tiempo de época. </td>
  </tr>
  <tr>
    <td><i> iat </i></td>
    <td> La hora a la que se emite la indicación de fecha y hora, especificada en tiempo de época. </td>
  </tr>
  <tr>
    <td><i> tenant </i></td>
    <td> El identificador de usuario único emitido con la señal.</td>
  </tr>
  <tr>
    <td><i> amr </i></td>
    <td> El proveedor de identidad utilizado para la autenticación. Esta variable puede ser <i>appid_facebook</i>, <i>appid_google</i> o <i>cloud_directory</i>. </td>
  </tr>
  <tr>
    <td><i> scope </i></td>
    <td> El ámbito para el que se emite la señal. </td>
  </tr>
</table>


### Señales de identidad
{: #identity-tokens}

Una señal de identidad contiene información sobre el usuario. Puede darle información sobre su nombre, correo electrónico, género y ubicación. También puede devolver el URL de una imagen del usuario.

Señal de ejemplo:

```
Header: {
    "typ": "JOSE",
    "alg": "RS256",
}
Payload: {
    "iss": "appid-oauth.ng.bluemix.net",
    "aud": "a3b87400-f03b-4956-844e-a52103ef26ba",
    "exp: "1495562664",
    "tenant": "9781974b-6a1c-46c3-aebf-32b7e9bbbaee",
    "iat": "1495559064",
    "name": "John Smith",
    "email": "js@mail.com",
    "gender", "male",
    "locale": "en",
    "picture": "https://url.to.photo",
    "sub": "de6a17d2-693d-4a43-8ea2-2140afd56a22",
    "identities": [
        "provider": "facebook"
        "id": "377440159275659"
    ],
    "amr": ["facebook"],
    "oauth_client":{
      "name": "BluemixApp",
      "type": "serverapp",
      "software_id": "cb638f8f-e24b-41d3-b770-23be158dd8e6.2b94e6bb-bac4-4455-8712-a43fa804d5cc.a3b87400-f03b-4956-844e-a52103ef26ba",
      "software_version": "1.0.0",
    }
}
```
{:screen}


<table>
<caption> Tabla 2. Explicación de componentes de señal de identidad </caption>
  <tr>
    <th> Componente </th>
    <th> Descripción </th>
  </tr>
  <tr>
    <td> <i> name </i> </td>
    <td> El nombre completo del usuario, tal como lo indica el proveedor de identidad. Se debe devolver. </td>
  </tr>
  <tr>
    <td> <i> email </i> </td>
    <td> El correo electrónico del usuario, tal como lo indica el proveedor de identidad. Devuelto sólo cuando esté disponible. </td>
  </tr>
  <tr>
    <td> <i> gender </i> </td>
    <td> El género del usuario, tal como lo indica el proveedor de identidad, cuando esté disponible. </td>
  </tr>
  <tr>
    <td> <i> locale </i> </td>
    <td> El entorno local del usuario, tal como lo indica el proveedor de identidad. </td>
  </tr>
  <tr>
    <td> <i> picture </i> </td>
    <td> El URL de la imagen de un usuario, si está disponible. </td>
  </tr>
  <tr>
    <td> <i> identities: </br> <ul><li> provider <li> id </ul></i></td>
    <td> </br><ul><li> El proveedor de identidad utilizado para la autenticación. Esta variable puede ser <code>appid_facebook</code>, <code>appid_google</code> o <code>cloud_directory</code> y debe devolverse. <li> Un ID de usuario exclusivo, tal como lo indica el proveedor de identidad. <li> Un objeto JSON que debe devolver el proveedor de identidad. </ul></li></td>
  </tr>
  <tr>
    <td> <i> oauth_client: </br> <ul><li> type </br><li> name <li> software_id <li> software_version<li> device_id <li>device_model<li>device_os<li>device_os_version </ul></i> </td>
    <td> </br><ul><li> El tipo de aplicación determinada durante el registro del cliente. La variable puede ser <em>serverapp</em> o <em>mobileapp</em>. <li> El nombre del cliente, tal como se haya indicado durante el registro del cliente. <li> El ID de software, tal como se haya indicado durante el registro del cliente. <li> La versión del software utilizado durante el registro del cliente. <li> El ID de dispositivo de cliente móvil. <li> El modelo de dispositivo de cliente móvil. <li> El sistema operativo del dispositivo de cliente móvil. <li> La versión del sistema operativo del dispositivo de cliente móvil. </ul></td>
  </tr>
</table>

## Cabeceras
{: #auth-header}

Una cabecera de autenticación es la combinación de las señales devueltas. Para {{site.data.keyword.appid_short}}, la cabecera de autorización consta de tres señales diferentes que están separadas por espacios en blanco: Portador, Acceso e Identidad. Las señales de portador y acceso son necesarias para otorgar acceso a sus apps. La señal de identidad es opcional y se utiliza principalmente para almacenar información sobre aquellos que utilizan la app.

Estructura de cabecera de ejemplo:

```
Authorization=Bearer {access_token} [{id_token}]
```
{: screen}


## Filtros
{: #auth-filter}

El SDK del servidor de {{site.data.keyword.appid_short}} proporciona estrategias para proteger dos tipos de recursos: API y aplicaciones web.
{:shortdesc}

La estrategia de protección de API devuelve una respuesta HTTP 401 con una lista de ámbitos para obtener la autorización para un cliente no autenticado. La estrategia de protección de aplicaciones web devuelve una redirección HTTP 302. La redirección envía a un cliente no autenticado a la página de inicio de sesión que aloja el servicio {{site.data.keyword.appid_short_notm}}, o bien directamente a la página de inicio de sesión de un proveedor de identidad, en función de su configuración.



### Estrategia de API
{: #api}

La estrategia de API espera que las solicitudes contengan una cabecera de autorización con una señal de acceso válida. La respuesta también puede incluir una señal de identidad, pero no es obligatorio. 

Si una señal no es válida o ha caducado, la estrategia de API devuelve un error HTTP 401 que contiene la siguiente información: Www-Authenticate=Bearer scope="{scope}" error="{error}". El componente `error` es opcional.

Si la solicitud devuelve una señal válida, el control se pasa al siguiente middleware y la propiedad `appIdAuthorizationContext` se inyecta en el objeto de solicitud. Esta propiedad contiene señales de acceso e identidad originales, e información de carga útil descodificada como objetos JSON simples.


### Estrategia de app web
{: #web}

Cuando la estrategia de app web detecta intentos no autenticados de acceso a un recurso protegido, automáticamente redirige el navegador de un usuario a la página de autenticación. Tras la correcta autenticación, el usuario vuelve al URL de devolución de llamada de la aplicación web. El servicio utiliza la clase de estrategia de app web para obtener señales de acceso e identidad. Después de obtener estas señales, la clase de estrategia de app web las almacena en una sesión HTTP bajo `WebAppStrategy.AUTH_CONTEXT`. Depende del usuario decidir si desea almacenar las señales de acceso e identidad en la base de datos de la aplicación.


## Autenticación progresiva
{: #oauth}

{{site.data.keyword.appid_short_notm}} utiliza protocolos OAuth 2.0 y OIDC para autorizar y autenticar usuarios. Tras la autenticación, su identidad se asocia con un registro de usuario. El servicio devuelve una señal de acceso que se puede utilizar para acceder a los atributos de usuario y una señal de identidad que contiene la información sobre el usuario proporcionada por el proveedor de identidad. Se puede volver a acceder al registro de usuario y a sus atributos desde cualquier cliente que se autentique con la misma identidad.

Es posible que se pregunte "¿Y si quiero que el inicio de sesión sea opcional?" {{site.data.keyword.appid_short_notm}} utiliza lo que se conoce como autenticación progresiva para crear [perfiles de usuario](/docs/services/appid/user-profile.html), incluso cuando son anónimos. Entonces puede transferir esa información a un perfil de usuario conocido cuando el usuario inicie sesión. 

![Mapa que muestra la vía de acceso para pasar a ser un usuario identificado.](/images/authenticationtrail.png)

Figura 2. Mapa que muestra la vía de acceso para pasar a ser un usuario identificado

Cuando un usuario elige permanecer anónimo, {{site.data.keyword.appid_short_notm}} crea un registro de usuario ad hoc y llama a la API de inicio de sesión OAuth que devuelve señales de acceso e identidad anónimas. Al utilizar esas señales, la app puede crear, leer, actualizar y suprimir los atributos almacenados en el registro de usuario. Por ejemplo, un usuario puede empezar a añadir artículos al carro de la compra sin tener que iniciar sesión en la app.


Cuando un usuario elige iniciar sesión en una app pasa a ser un usuario identificado. Se obtiene información sobre el usuario del proveedor de identidad que eligió para iniciar sesión. Reciben señales de acceso e identidad que contienen información sobre el usuario.

Un usuario anónimo puede elegir pasar a ser un usuario identificado. Pero, ¿cómo funciona?

La señal de acceso anónimo pasa a la API de inicio de sesión. El servicio autentica la llamada con un proveedor de identidad. Utiliza la señal de acceso para encontrar el registro anónimo y le adjunta la identidad. Las nuevas señales de identidad de acceso contienen la información pública compartida por el proveedor de identidad. Cuando se identifica un usuario, sus señales anónimas pasan a ser no válidas. Sin embargo, el usuario aun puede acceder a sus atributos ya que son accesibles con la nueva señal.

**Nota**: Solo se puede asignar una identidad a un registro anónimo si no ha sido asignada aun a otro usuario. Si la identidad ya está asociada con otro usuario de {{site.data.keyword.appid_short_notm}}, las señales contienen la información de ese registro de usuario y proporcionan acceso a sus atributos. Los atributos del usuario anónimo anterior no son accesibles a través de la nueva señal. Hasta que la señal caduque, aún se podrá acceder a la información a través de la señal de acceso anónimo. Durante el desarrollo, puede elegir cómo fusionar los atributos anónimos con los usuarios conocidos.
