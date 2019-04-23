---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

keywords: authentication, authorization, identity, app security, secure, access, tokens

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
    <p>Cuando utiliza OIDC junto con {{site.data.keyword.appid_short_notm}}, las credenciales de aplicación permiten configurar los puntos finales de OAuth. Cuando utiliza el SDK, los URL de punto final se crean automáticamente. Sin embargo, también puede crear los URL por su cuenta con sus credenciales de servicio.</p> <p>El URL tiene el siguiente formato: punto final de servicio de {{site.data.keyword.appid_short_notm}} + "/oauth/v4" + /tenantID.</p>
    <p><pre class="codeblock">
    <code>{
      "clientId": "7eba72ef-b913-47b0-b3b6-54358bb69035",
      "tenantId": "8f5aa500-357e-443a-aab6-bf878f852b5a",
      "secret": "OWEzZGM4M2UtZjhlYS00MDI2LTkwNGItNDJmYzViMmU2YzIz",
      "name":testing",
      "oAuthServerUrl": "https://us-south.appid-oauth.cloud.ibm.com/oauth/v4/8f5aa500-357e-443a-aab6-bf878f852b5a",
      "profilesUrl": "https://us-south.appid.cloud.ibm.com",
      "discoveryEndpoint": "https://us-south.appid-oauth.cloud.ibm.com/oauth/v4/8f5aa500-357e-443a-aab6-bf878f852b5a/.well-known/openid-configuration"
    }</code></pre></p>
    <p>Con este ejemplo, el URL sería <code>https://us-south.appid.cloud.ibm.com/oauth/v4/3x176051-a23x-40y4-9645-804943z660q0</code>. A continuación, añadiría el punto final al que desea realizar una solicitud. Consulte la tabla siguiente para ver algunos puntos finales de ejemplo.</p>
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
    <dd>El servicio utiliza tres tipos de señales distintas. Las señales de acceso representan una autorización y permiten la comunicación con [recursos de fondo](/docs/services/appid?topic=appid-backend) que están protegidos por filtros de autorización definidos por {{site.data.keyword.appid_short}}. Las señales de identidad representan una autenticación y contienen información sobre el usuario. Se puede utilizar una señal para renovación para obtener una nueva señal de acceso sin volver a autenticar al usuario. Mediante el uso de señales para renovación, los usuarios pueden permitir que la aplicación recuerde sus datos. De esta forma, pueden mantener la sesión iniciada. Las señales se definen en <b>Proveedores de identidad > Gestionar</b> del panel de control de {{site.data.keyword.appid_short}}. Para obtener más información sobre las señales y cómo se utilizan en {{site.data.keyword.appid_short}}, consulte [Gestión de señales](/docs/services/appid?topic=appid-tokens#tokens).
  </dd>
  <dt>Cabeceras de autorización</dt>
    <dd><p>{{site.data.keyword.appid_short}} cumple con la <a href="https://tools.ietf.org/html/rfc6750" target="blank">especificación de señal de portador <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> y utiliza una combinación de señales de acceso e identidad que se envían como una cabecera de autorización HTTP. La cabecera de autorización contiene tres partes distintas separadas con un espacio en blanco. Las señales están codificadas en base64. La señal de identidad es opcional.</br>
    Ejemplo:</p>
    <pre><code>Authorization=Bearer {access_token} [{id_token}]</code></pre></dd>
  <dt>Estrategia de API</dt>
    <dd><p>La estrategia de API espera que las solicitudes contengan una cabecera de autorización con una señal de acceso válida. La solicitud también puede incluir una señal de identidad, pero no es obligatorio. Si una señal no es válida o ha caducado, la estrategia de API devuelve un error HTTP 401 que contiene la siguiente cabecera HTTP:</p> <pre><code>Www-Authenticate=Bearer scope="{scope}" error="{error}"</code></pre>
    <p>Si la solicitud devuelve una señal válida, el control se pasa al siguiente middleware y la propiedad <code>appIdAuthorizationContext</code> se inyecta en el objeto de solicitud. Esta propiedad contiene señales de acceso e identidad originales, e información de carga útil descodificada como objetos JSON simples.</dd>
  <dt>Estrategia de app web</dt>
    <dd>Cuando la estrategia de app web detecta intentos no autorizados de acceso a un recurso protegido, automáticamente redirige el navegador de un usuario a la página de autenticación, que puede estar proporcionada por {{site.data.keyword.appid_short}}. Tras la correcta autenticación, el usuario vuelve al URL de devolución de llamada de la app web. La estrategia de app web obtiene las señales de acceso e identidad y las almacena en una sesión HTTP bajo <code>WebAppStrategy.AUTH_CONTEXT</code>. Depende del usuario decidir si desea almacenar las señales de acceso e identidad en la base de datos de la app.</dd>
  <dt>Separación y cifrado de datos</dt>
    <dd><p>{{site.data.keyword.appid_short_notm}} almacena y cifra atributos de perfil de usuario. Como servicio multiarrendatario, cada arrendatario tiene una clave de cifrado designada y los datos de usuario de cada uno se cifran únicamente con la clave de dicho arrendatario.</p>
    <p>{{site.data.keyword.appid_short_notm}} garantiza que la información privada se cifre antes de que se almacene.</p></dd>
  <dt>URI de redirección</dt>
    <dd><p>{{site.data.keyword.appid_short_notm}} utiliza una lista de URI completos y aprobados para redirigir a los usuarios después de una interacción con la app. Por ejemplo, si el usuario inicia sesión correctamente, {{site.data.keyword.appid_short_notm}} redirige al usuario a la página de inicio de la app o a otra página que especifique. El formato del URI puede cambiar en función de la aplicación. Consulte [Adición de URI de redirección](/docs/services/appid?topic=appid-managing-idp#add-redirect-uri) para obtener más información.</p></dd>
  <dt>Conjunto de claves web JSON (JWKS)</dt>
    <dd>Un JWKS representa un conjunto de claves criptográficas. {{site.data.keyword.appid_short_notm}} utiliza un JWKS para verificar la autenticidad de las señales generadas por el servicio. Al utilizar el ID de clave para verificar la firma, podemos asegurarnos de que la señal ha sido emitida por una fuente fiable {{site.data.keyword.appid_short_notm}}, y que la información dentro de la señal no se ha modificado.</dd>
</dl>

