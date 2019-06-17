---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-05"

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



# Información sobre las señales
{: #tokens}

Cuando un usuario se autentica correctamente, la aplicación recibe señales de {{site.data.keyword.appid_short_notm}}. El servicio utiliza tres tipos de señales principales para completar el proceso de autenticación.
{: shortdesc}


## Señales de acceso
{: #access}

Las señales de acceso representan una autorización y permiten la comunicación con [recursos de fondo](/docs/services/appid?topic=appid-backend) que están protegidos por filtros de autorización definidos por {{site.data.keyword.appid_short}}. La señal se ajusta a las especificaciones de JOSE (JavaScript Object Signing and Encryption). La señal tiene el formato de <a href="https://jwt.io/introduction/" target="blank">señales web de JSON <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> que se firman con una clave de web JSON que utiliza el algoritmo RS256.

Ejemplo de señal:
  ```
  Header: {
    "alg": "RS256",
    "typ": "JWT",
    "kid": "appId-39a37f57-a227-4bfe-a044-93b6e6050a61-2018-08-02T11:57:43.401",
    "ver": 4
  }
  Payload:
  {
    "iss": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61",
    "exp": 1551903163,
    "aud": [
      "968c2306-9aef-4109-bc06-4f5ed6axi24a"
    ],
    "sub": "2b96cc04-eca5-4122-a8de-6e07d14c13a5",
    "email_verified": true,
    "amr": [
      "cloud_directory"
    ],
    "iat": 1551899553,
    "tenant": "39a37f57-a227-4bfe-a044-93b6e6050a61",
    "scope": "openid appid_default appid_readprofile appid_readuserattr appid_writeuserattr appid_authenticated"
  }
  ```
  {: screen}

## ¿Qué son las señales de identidad?
{: #identity}

Las señales de identidad representan una autenticación y contienen información sobre el usuario. Le pueden proporcionar información acerca del nombre, el correo electrónico, el género y la ubicación. Una señal también puede devolver un URL a una imagen del usuario. La señal tiene el formato de <a href="https://jwt.io/introduction/" target="blank">señales web de JSON <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> que se firman con una clave de web JSON que utiliza el algoritmo RS256.

Ejemplo de señal:
  ```
  Header: {
    "alg": "RS256",
    "typ": "JWT",
    "kid": "appId-39a37f57-a227-4bfe-a044-93b6e6050a61-2018-08-02T11:57:43.401",
    "ver": 4
  }
  Payload:
  {
    "iss": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61",
    "aud": [
      "968c2306-9aef-4109-bc06-4f5ed6axi24a"
    ],
    "exp": 1551903163,
    "tenant": "39a37f57-a227-4bfe-a044-93b6e6050a61",
    "iat": 1551899553,
    "email": "appid155@mailinator.com",
    "name": "appid155@mailinator.com",
    "sub": "2b96cc04-eca5-4122-a8de-6e07d14c13a5",
    "email_verified": true,
    "identities": [
      {
        "provider": "cloud_directory",
        "id": "118c0278-3526-4954-876b-cf70eb88efa2"
      }
    ],
    "amr": [
      "cloud_directory"
    ]
  }
  ```
  {: screen}


Las señales de identidad solo contienen información de usuario parcial. Para ver toda la información que proporciona el proveedor de identidad, puede utilizar el punto final [/userinfo](/docs/services/appid?topic=appid-profiles#profile-predefined-api).

## ¿Qué son las señales de renovación?
{: #refresh}

{{site.data.keyword.appid_short}} ofrece soporte a la capacidad de adquirir nuevas señales de identidad y acceso sin autenticación, como se define en <a href="https://openid.net/specs/openid-connect-core-1_0.html#RefreshTokens" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>. Se puede utilizar una señal de acceso para renovar la señal de manera que el usuario no tenga que realizar ninguna acción, como proporcionar las credenciales, para iniciar sesión. De forma similar a las señales de acceso, las señales para renovación contienen datos que permiten a {{site.data.keyword.appid_short_notm}} determinar si ha autorizado. Sin embargo, dichas señales son opacas.

Las señales para renovación están configuradas para tener un período de vida superior al de una señal de acceso normal para que cuando la señal de acceso caduque, la señal de renovación siga siendo válida y se pueda utilizar para renovar la señal de acceso. Las señales para renovación de {{site.data.keyword.appid_short_notm}} se pueden configurar para que duren de 1 a 90 días. Para sacar el máximo partido de las señales para renovación, mantenga las señales durante todo el período activo o hasta que se renueven. Un usuario no puede acceder directamente a recursos con solo una señal para renovación, por lo que es mucho más seguro que esta se mantenga en lugar de la señal de acceso. Se recomienda que el cliente que reciba señales de acceso las almacene de forma segura y las envíe únicamente al servidor de autorización que las ha enviado.

Para mayor comodidad, {{site.data.keyword.appid_short_notm}} también renueva su señal para renovación (y la fecha de caducidad) cuando se renueva la señal de acceso, lo que permite al usuario permanecer conectado siempre que esté activo en algún momento antes de que caduque la señal para renovación actual. Por otro lado, si desea utilizar señales para renovación y también forzar al usuario a iniciar sesión de forma periódica, la app solo puede utilizar las señales de actualización devueltas cuando el usuario inicia sesión especificando sus credenciales. Sin embargo, se recomienda utilizar siempre la última señal para renovación recibida desde {{site.data.keyword.appid_short_notm}}, tal y como se describe en las <a href="https://tools.ietf.org/html/rfc6749#page-47" target="_blank">especificaciones de OAuth 2.0 <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.


Aunque estas señales pueden simplificar el proceso de inicio de sesión, la app no debería depender de ellas, puesto que se pueden revocar en cualquier momento como, por ejemplo, cuando considera que las señales para renovación se han visto comprometidas. Si desea revocar una señal para renovación, existen dos formas de hacerlo. Si dispone de la señal para renovación, puede revocarla en función de <a href="https://tools.ietf.org/html/rfc7009#section-2" target="_blank">RFC7009 <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>. De forma alternativa, si tiene el ID de usuario, puede revocar la señal para renovación utilizando la <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/" target="_blank">API de gestión <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>. Para obtener más información sobre cómo acceder a la API de gestión, consulte [Gestión del acceso del servicio](/docs/services/appid?topic=appid-service-access-management#service-access-management).

Para obtener ejemplo de cómo trabajar con señales para renovación y cómo utilizarlas para implementar una funcionalidad recuérdame, consulte los [ejemplo de iniciación](/docs/services/appid?topic=appid-getting-started#getting-started).


## ¿De dónde provienen las señales?
{: #where}

Las señales se emiten a través del servidor OAuth de {{site.data.keyword.appid_short_notm}} y tienen el formato de [señales web de JSON (JWT)](https://jwt.io/introduction/). Las señales están firmadas con una [clave web de JSON (JWK)](https://tools.ietf.org/html/rfc7517) con el algoritmo RS256.

## ¿Qué sucede con la información que contiene la señal?
{: #contains}

La señal de acceso contiene un conjunto de reclamaciones JWT y un grupo de reclamaciones específicas de {{site.data.keyword.appid_short_notm}} como, por ejemplo, un ID de arrendatario. La señal de identidad contiene información específica del usuario. La información de las señales de acceso se almacena en forma de reclamaciones como parte de un [perfil de usuario](/docs/services/appid?topic=appid-profiles).

## ¿Cómo se reciben las señales?
{: #received}

Las señales las recibe la app después de que se haya realizado una autenticación correcta. La app puede utilizar las señales para recuperar información sobre la autenticación y autorización del usuario. La señal de acceso se puede utilizar para obtener acceso a los recursos protegidos enviando una solicitud al recurso. En la solicitud, la señal de acceso se describe en el [Esquema de autenticación del portador](https://tools.ietf.org/html/rfc6750#page-5). Para extraer las señales, la app debe analizar la cabecera.

Solicitud de ejemplo:

  ```
  GET /resource HTTP/1.1
  Host: server.example.com
  Authorization: Bearer  mF_9.B5f-4.1JqM mF_9.B5f-4.1JqM
  ```
  {: screen}

## ¿Cómo se establecen las señales?
{: #set}

Las configuraciones de señales se pueden habilitar e inhabilitar mediante el panel de control de {{site.data.keyword.appid_short_notm}}. Para obtener más información sobre las opciones de configuración, consulte [Gestión de señales](/docs/services/appid?topic=appid-managing-idp#managing-idp).
