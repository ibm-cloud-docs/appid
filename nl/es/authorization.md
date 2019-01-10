---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}




# Conceptos clave
{: #key-concepts}

¿Está confundido sobre las diferencias entre la autorización y la autenticación? No es el único. Consulte la información de esta página para conocer terminología específica, procesos y la forma en que el servicio utiliza las señales.
{: shortdesc}


## Terminología
{: #terms}


Estos términos clave pueden ayudarle a comprender la forma en que el servicio divide el proceso de autorización y de autenticación.

<dl>
  <dt>OAuth 2</dt>
    <dd><a href="https://tools.ietf.org/html/rfc6749" target="_blank">OAuth 2 <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> es un protocolo estándar que se utiliza para proporcionar autorización de apps.</dd>
  <dt>Open ID Connect (OIDC)</dt>
    <dd><p><a href="http://openid.net/developers/specs/" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> es una capa de autenticación que funciona sobre OAuth 2.</p>
    <p>Cuando utiliza OIDC junto con {{site.data.keyword.appid_short_notm}}, las credenciales de servicio permiten configurar los puntos finales de OAuth. Cuando utiliza el SDK, los URL de punto final se crean automáticamente. Sin embargo, también puede crear los URL por su cuenta con sus credenciales de servicio. Consulte cómo crear los URL en la tabla y el ejemplo siguientes.</p>
    <pre class="codeblock">
    <code>{
      "version": 3,
      "clientId": "e8ac1132-5151-4d8a-934e-0141de8e2b34",
      "secret": "XYZ5ZYXzXYZtNyz5Yi00YzQ2LXYwMZctXyM5ODA4NjFhYxYZ",
      "tenantId": "3x176051-a23x-40y4-9645-804943z660q0",
      "oauthServerUrl": "https://appid-oauth.ng.bluemix.net/oauth/v3/3x176051-a23x-40y4-9645-804943z660q0",
      "profilesUrl": "https://appid-profiles.ng.bluemix.net/"
    }</code></pre>
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
    <p><strong>Nota</strong>: Cuando utiliza el SDK, los URL de punto final se crean automáticamente.</p></dd>
  <dt>Señales</dt>
    <dd>El servicio utiliza tres tipos de señales distintas. Las señales de acceso representan una autorización y permiten la comunicación con [recursos de fondo](/docs/services/appid/backend-apps.html) que están protegidos por filtros de autorización definidos por {{site.data.keyword.appid_short}}. Las señales de identidad representan una autenticación y contienen información sobre el usuario. Se puede utilizar una señal para renovación para obtener una nueva señal de acceso sin volver a autenticar al usuario. Mediante el uso de señales para renovación, los usuarios pueden permitir que la aplicación recuerde sus datos. De esta forma, pueden mantener la sesión iniciada. Para obtener más información sobre las señales y cómo se utilizan en {{site.data.keyword.appid_short}}, consulte [Validación de señales](tokens.html#remote-validation).
  </dd>
  <dt>Cabeceras de autorización</dt>
    <dd><p>{{site.data.keyword.appid_short}} cumple con la <a href="https://tools.ietf.org/html/rfc6750" target="blank">especificación de señal de portador <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> y utiliza una combinación de señales de acceso e identidad que se envían como una cabecera de autorización HTTP. La cabecera de autorización contiene tres partes distintas separadas con un espacio en blanco. Las señales están codificadas en base64. La señal de identidad es opcional.</br>
    Ejemplo:</p>
    <pre><code>Authorization=Bearer {access_token} [{id_token}]</pre></code></dd>
  <dt>Estrategia de API</dt>
    <dd><p>La estrategia de API espera que las solicitudes contengan una cabecera de autorización con una señal de acceso válida. La solicitud también puede incluir una señal de identidad, pero no es obligatorio. Si una señal no es válida o ha caducado, la estrategia de API devuelve un error HTTP 401 que contiene la siguiente cabecera HTTP:</p> <pre><code>Www-Authenticate=Bearer scope="{scope}" error="{error}"</code></pre>
    <p>Si la solicitud devuelve una señal válida, el control se pasa al siguiente middleware y la propiedad <code>appIdAuthorizationContext</code> se inyecta en el objeto de solicitud. Esta propiedad contiene señales de acceso e identidad originales, e información de carga útil descodificada como objetos JSON simples.</dd>
  <dt>Estrategia de app web</dt>
    <dd>Cuando la estrategia de app web detecta intentos no autorizados de acceso a un recurso protegido, automáticamente redirige el navegador de un usuario a la página de autenticación, que puede estar proporcionada por {{site.data.keyword.appid_short}}. Tras la correcta autenticación, el usuario vuelve al URL de devolución de llamada de la app web. La estrategia de app web obtiene las señales de acceso e identidad y las almacena en una sesión HTTP bajo <code>WebAppStrategy.AUTH_CONTEXT</code>. Depende del usuario decidir si desea almacenar las señales de acceso e identidad en la base de datos de la app.</dd>
  <dt>Separación y cifrado de datos</dt>
    <dd><p>{{site.data.keyword.appid_short_notm}} almacena y cifra atributos de perfil de usuario. Como servicio multiarrendatario, cada arrendatario tiene una clave de cifrado designada y los datos de usuario de cada uno se cifran únicamente con la clave de dicho arrendatario.</p>
    <p>{{site.data.keyword.appid_short_notm}} garantiza que la información privada se cifre antes de que se almacene.</p></dd>
</dl>

</br>
</br>


## Información sobre las señales
{: #tokens}

Cuando un usuario se autentica correctamente, la aplicación recibe señales de {{site.data.keyword.appid_short_notm}}. El servicio utiliza tres tipos de señales principales para completar el proceso de autenticación.
{: shortdesc}


**¿Qué es una señal de acceso?**

Las señales de acceso representan una autorización y permiten la comunicación con [recursos de fondo](/docs/services/appid/backend-apps.html) que están protegidos por filtros de autorización definidos por {{site.data.keyword.appid_short}}. La señal se ajusta a las especificaciones de JOSE (JavaScript Object Signing and Encryption). La señal tiene el formato de <a href="https://jwt.io/introduction/" target="blank">señales web de JSON <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> que se firman con una clave de web JSON que utiliza el algoritmo RS256.

Ejemplo de señal:
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
  ```
  {: screen}

**¿Qué es una señal de identidad?**

Las señales de identidad representan una autenticación y contienen información sobre el usuario. Le pueden proporcionar información acerca del nombre, el correo electrónico, el género y la ubicación. Una señal también puede devolver un URL a una imagen del usuario. La señal tiene el formato de <a href="https://jwt.io/introduction/" target="blank">señales web de JSON <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> que se firman con una clave de web JSON que utiliza el algoritmo RS256.

Ejemplo de señal:
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
      "picture": "<URL-to-photo>",
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
  {: screen}

Las señales de identidad solo contienen información de usuario parcial. Para ver toda la información que proporciona el proveedor de identidad, puede utilizar el [punto final de información de usuario](/docs/services/appid/predefined.html#api).

**¿Qué es una señal para renovación?**

{{site.data.keyword.appid_short}} ofrece soporte a la capacidad de adquirir nuevas señales de identidad y acceso sin autenticación, como se define en <a href="http://openid.net/specs/openid-connect-core-1_0.html#RefreshTokens" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>. Se puede utilizar una señal de acceso para renovar la señal de manera que el usuario no tenga que realizar ninguna acción, como proporcionar las credenciales, para iniciar sesión. De forma similar a las señales de acceso, las señales para renovación contienen datos que permiten a {{site.data.keyword.appid_short_notm}} determinar si ha autorizado. Sin embargo, dichas señales son opacas.

Las señales para renovación están configuradas para tener un período de vida superior al de una señal de acceso normal para que cuando la señal de acceso caduque, la señal de renovación siga siendo válida y se pueda utilizar para renovar la señal de acceso. Las señales para renovación de {{site.data.keyword.appid_short_notm}} se pueden configurar para que duren de 1 a 90 días. Para sacar el máximo partido de las señales para renovación, mantenga las señales durante todo el período activo o hasta que se renueven. Un usuario no puede acceder directamente a recursos con solo una señal para renovación, por lo que es mucho más seguro que esta se mantenga en lugar de la señal de acceso. Se recomienda que el cliente que reciba señales de acceso las almacene de forma segura y las envíe únicamente al servidor de autorización que las ha enviado.

Para mayor comodidad, {{site.data.keyword.appid_short_notm}} también renueva su señal para renovación (y la fecha de caducidad) cuando se renueva la señal de acceso, lo que permite al usuario permanecer conectado siempre que esté activo en algún momento antes de que caduque la señal para renovación actual. Por otro lado, si desea utilizar señales para renovación y también forzar al usuario a iniciar sesión de forma periódica, la app solo puede utilizar las señales de actualización devueltas cuando el usuario inicia sesión especificando sus credenciales. Sin embargo, se recomienda utilizar siempre la última señal para renovación recibida desde el ID de app, tal y como se describe en <a href="https://tools.ietf.org/html/rfc6749#page-47" target="_blank">Especificaciones de Oauth <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.


Aunque estas señales pueden simplificar el proceso de inicio de sesión, la app no debería depender de ellas, puesto que se pueden revocar en cualquier momento como, por ejemplo, cuando considera que las señales para renovación se han visto comprometidas. Si desea revocar una señal para renovación, existen dos formas de hacerlo. Si dispone de la señal para renovación, puede revocarla en función de <a href="https://tools.ietf.org/html/rfc7009#section-2" target="_blank">RFC7009 <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>. De forma alternativa, si tiene el ID de usuario, puede revocar la señal para renovación utilizando la <a href="https://appid-management.ng.bluemix.net/swagger-ui/" target="_blank">API de gestión <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>. Para obtener más información sobre cómo acceder a la API de gestión, consulte [Gestión del acceso del servicio](iam.html#service-access-management).

Para obtener ejemplo de cómo trabajar con señales para renovación y cómo utilizarlas para implementar una funcionalidad recuérdame, consulte los [ejemplo de iniciación](index.html).


**¿De donde provienen las señales?**

Las señales se emiten a través del servidor OAuth de {{site.data.keyword.appid_short_notm}} y tienen el formato de [señales web de JSON (JWT)](https://jwt.io/introduction/). Las señales están firmadas con una [clave web de JSON (JWK)](https://tools.ietf.org/html/rfc7517) con el algoritmo RS256.

**¿Qué sucede con la información que contiene la señal?**

La señal de acceso contiene un conjunto de reclamaciones JWT y un grupo de reclamaciones específicas de {{site.data.keyword.appid_short_notm}} como, por ejemplo, un ID de arrendatario. La señal de identidad contiene información específica del usuario. La información de las señales de acceso se almacena en forma de reclamaciones como parte de un [perfil de usuario](/docs/services/appid/user-profile.html).

**¿Cómo se reciben las señales?**

Las señales las recibe la app después de que se haya realizado una autenticación correcta. La app puede utilizar las señales para recuperar información sobre la autenticación y autorización del usuario. La señal de acceso se puede utilizar para obtener acceso a los recursos protegidos enviando una solicitud al recurso. En la solicitud, la señal de acceso se describe en el [Esquema de autenticación del portador](https://tools.ietf.org/html/rfc6750#page-5). Para extraer las señales, la app debe analizar la cabecera.

Solicitud de ejemplo:

  ```
  GET /resource HTTP/1.1
  Host: server.example.com
  Authorization: Bearer  mF_9.B5f-4.1JqM mF_9.B5f-4.1JqM
  ```
  {: screen}

</br>
</br>
