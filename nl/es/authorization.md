---

copyright:
  years: 2017, 2018
lastupdated: "2018-05-2"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}

# Autorización y autenticación
{: #authorization}

Con {{site.data.keyword.appid_full}}, los usuarios pueden aprovechar las señales y los filtros de autorización para garantizar que sus apps estén protegidas. Antes de que un usuario pueda otorgar autorización a una app, un proveedor de identidad debe autenticar su identidad.
{: shortdesc}


## Conceptos clave
{: #key-concepts}

Estos términos clave pueden ayudarle a comprender la forma en que el servicio divide el proceso de autorización y de autenticación.

<dl>
  <dt>OAuth 2</dt>
    <dd><a href="https://tools.ietf.org/html/rfc6749" target="_blank">OAuth 2 <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> es un protocolo estándar que se utiliza para proporcionar autorización de apps.</dd>
  <dt>Open ID Connect (OIDC)</dt>
    <dd><a href="http://openid.net/developers/specs/" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> es una capa de autenticación que funciona sobre OAuth 2.</dd>
  <dt>Señales de acceso</dt>
    <dd><p>Las señales de acceso representan una autorización y permiten la comunicación con [recursos de fondo](/docs/services/appid/protecting-resources.html) que están protegidos por filtros de autorización definidos por {{site.data.keyword.appid_short}}. La señal se ajusta a las especificaciones de JOSE (JavaScript Object Signing and Encryption). Las señales están formateadas como <a href="https://jwt.io/introduction/" target="blank">Señales web JSON <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.</br>
    Ejemplo:</p>
    <pre><code>Header: {
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
    </code></pre></dd>
  <dt>Señales de identidad</dt>
    <dd><p>Las señales de identidad representan una autenticación y contienen información sobre el usuario. Puede darle información sobre su nombre, correo electrónico, género y ubicación. También puede devolver el URL de una imagen del usuario.</br>
    Ejemplo:</p>
    <pre><code>Header: {
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
    </pre></code></dd>
  <dt>Señal de actualización</dt>
      <dd><p>{{site.data.keyword.appid_short}} admite la posibilidad de adquirir nuevas señales de acceso e identidad sin reautenticación, tal como se define en <a href="http://openid.net/specs/openid-connect-core-1_0.html#RefreshTokens" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.
      Al registrarse con una señal de renovación, un usuario no tiene que realizar ninguna acción, como por ejemplo proporcionar credenciales. Generalmente, las señales de renovación están configuradas para tener una vida más larga que una señal de acceso normal.</p><p>
      Para aprovechar las señales de renovación, conserve las señales durante su vida completa. Un usuario no puede acceder directamente a los recursos con tan solo una señal de renovación, lo que hace su persistencia mucho más segura que una señal de acceso. Para obtener ejemplos de cómo trabajar con señales de renovación y cómo utilizarlas para implementar una funcionalidad *recuérdame*, consulte los ejemplos de cómo empezar.</p><p>Como práctica recomendada, la renovación de señales la debe almacenar de forma segura el cliente que las recibió, y solo se debería enviar al servidor de autorización que las haya emitido.</p></dd>
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

## Cómo funciona el proceso
{: #process}

Al programar apps, una de las mayores preocupaciones es la seguridad. ¿Cómo puede garantizar que solo los usuarios con el acceso correcto estén utilizando la app? Utilizando un proceso de autorización. En la mayoría de los procesos, la autorización y la autenticación están unidas, lo que puede hacer complicado cambiar las políticas de seguridad y los proveedores de identidad. Con {{site.data.keyword.appid_short}}, la autorización y la autenticación son procesos separados.
{: shortdesc}

Cuando configura proveedores de identidad social como Facebook, se utiliza el [flujo de otorgamiento de autorización de Oauth2](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html) para llamar al widget de inicio de sesión. Con el directorio en la nube como proveedor de identidad, se utiliza el [flujo ROPC (credenciales de contraseña de propietario de recurso)](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html) para proporcionar señales de acceso e identidad.

![Recorrido para convertirse en un usuario identificado.](/images/authenticationtrail.png)

Cuando un usuario elige iniciar sesión, se convierten en un usuario identificado. El proveedor de identidad devuelve señales de acceso e identidad a {{site.data.keyword.appid_short}} que contienen información sobre el usuario. El servicio toma las señales proporcionadas y determina si un usuario tiene las credenciales suficientes para acceder a la app. Si las señales están validadas, el servicio autoriza el acceso de los usuarios. La información de autenticación está asociada con el registro del usuario una vez que esté autorizado. Se puede volver a acceder al registro de usuario y a sus atributos desde cualquier cliente que se autentique con la misma identidad.

### Autenticación progresiva

Con {{site.data.keyword.appid_short_notm}}, un usuario anónimo puede elegir pasar a ser un usuario identificado.

Pero, ¿cómo funciona?

Cuando un usuario no inicia la sesión inmediatamente, se considera como un usuario anónimo. Como ejemplo, un usuario puede empezar inmediatamente a añadir artículos al carro de la compra sin iniciar la sesión. Para los usuarios anónimos, {{site.data.keyword.appid_short_notm}} crea un registro de usuario ad hoc y llama a la API de inicio de sesión OAuth que devuelve señales de acceso e identidad anónimas. Al utilizar esas señales, la app puede crear, leer, actualizar y suprimir los atributos almacenados en el registro de usuario.

![Recorrido para convertirse en un usuario identificado cuando se empieza como anónimo.](/images/anon-authenticationtrail.png)

Cuando un usuario anónimo inicia la sesión, la señal de acceso pasa a la API de inicio de sesión. El servicio autentica la llamada con un proveedor de identidad. El servicio utiliza la señal de acceso para encontrar el registro anónimo y le adjunta la identidad. Las nuevas señales de acceso e identidad contienen la información pública compartida por el proveedor de identidad. Cuando se identifica un usuario, su señal anónima pasa a ser no válida. Sin embargo, el usuario aún puede acceder a sus atributos ya que son accesibles con la nueva señal.

Se puede asignar una identidad a un registro anónimo solo si todavía no se ha asignado a otro usuario.
{: tip}

Si la identidad ya está asociada con otro usuario de {{site.data.keyword.appid_short_notm}}, las señales contienen la información de ese registro de usuario y proporcionan acceso a sus atributos. Los atributos del usuario anónimo anterior no son accesibles a través de la nueva señal. Hasta que la señal caduque, aún se podrá acceder a la información a través de la señal de acceso anónimo. Durante el desarrollo, puede elegir cómo fusionar los atributos anónimos con los usuarios conocidos.
