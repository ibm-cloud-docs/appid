---

copyright:
  years: 2017
lastupdated: "2017-11-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Señales de identidad y de acceso

{{site.data.keyword.appid_short}} utiliza dos tipos de señales: acceso e identidad. Las señales están formateadas como <a href="https://jwt.io/introduction/" target="_blank">Señales web JSON <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.
{:shortdesc}


## Señal de acceso
{: #access-tokens}

La señal de acceso permite la comunicación con [recursos de fondo](/docs/services/appid/protecting-resources.html) que están protegidos por filtros de autorización de {{site.data.keyword.appid_short_notm}}. La señal se ajusta a las especificaciones de JOSE (JavaScript Object Signing and Encryption) y tiene el formato siguiente:

```
Header: {
    "typ": "JOSE",
    "alg": "RS256",
}
Payload: {
    "iss": "appid-oauth.ng.bluemix.net",
    "exp": "1495562664",
    "aud": "a3b87400-f03b-4956-844e-a52103ef26ba",
    "amr": "facebook",
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
    <td> <i> typ </i> </td>
    <td> El tipo de cabecera, especificado como "JOSE". </td>
  </tr>
  <tr>
    <td> <i> alg </i> </td>
    <td> El algoritmo utilizado, especificado como "RS256". </td>
  </tr>
  <tr>
    <td> <i> iss </i> </td>
    <td> El servidor de {{site.data.keyword.appid_short}} que ha emitido la señal, especificado como serie o como URL. </td>
  </tr>
  <tr>
    <td> <i> sub </i> </td>
    <td> El ID del usuario para el que se ha emitido la señal. </td>
  </tr>
  <tr>
    <td> <i> aud </i> </td>
    <td> El ID de cliente para el que está pensada la señal. </td>
  </tr>
  <tr>
    <td> <i> exp </i> </td>
    <td> La hora a la que caduca la indicación de fecha y hora, especificada en tiempo de época. </td>
  </tr>
  <tr>
    <td> <i> iat </i> </td>
    <td> La hora a la que se emite la indicación de fecha y hora, especificada en tiempo de época. </td>
  </tr>
  <tr>
    <td> <i> tenant </i> </td>
    <td> El ID de arrendatario para el que se emite la señal. </td>
  </tr>
  <tr>
    <td> <i> amr </i> </td>
    <td> El proveedor de identidad utilizado para la autenticación. Esta variable puede ser <i>appid_facebook</i> o <i>appid_google</i>. </td>
  </tr>
  <tr>
    <td> <i> scope </i> </td>
    <td> El ámbito para el que se emite la señal. </td>
  </tr>
</table>


## Señal de identidad
{: #identity-tokens}

La señal de identidad contiene información sobre el usuario, tal como el nombre, el correo electrónico, el género, la imagen y la ubicación.

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
        "id": "377440159275659",
        "amr: "facebook",
    ],
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
    <td> <i> identities: </br> <ul><li> provider <li> id <li> amr </ul></i></td>
    <td> </br><ul><li> El proveedor de identidad utilizado para la autenticación. Esta variable puede ser <code>appid_facebook</code> o <code>appid_google</code> y debe devolverse. </li><li> Un ID de usuario exclusivo, tal como lo indica el proveedor de identidad. </li><li> Un objeto JSON que debe devolver el proveedor de identidad. </li></ul></td>
  </tr>
  <tr>
    <td> <i> oauth_client: </br> <ul><li> type <li> name <li> software_id <li> software_version</ul></i> </td>
    <td> </br><ul><li> El tipo de aplicación determinada durante el registro del cliente. La variable puede ser <i>serverapp</i> o <i>mobileapp</i>. <li> El nombre del cliente, tal como se haya indicado durante el registro del cliente. <li> El ID de software, tal como se haya indicado durante el registro del cliente. <li> La versión del software utilizado durante el registro del cliente. </ul></td>
  </tr>
</table>
