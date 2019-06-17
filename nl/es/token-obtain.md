---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-29"

keywords: authentication, authorization, identity, app security, secure, access management, roles, attributes, users

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
{:java: .ph data-hd-programlang='java'}
{:javascript: .ph data-hd-programlang='javascript'}
{:swift: .ph data-hd-programlang='swift'}
{:curl: .ph data-hd-programlang='curl'}



# Obtención de señales
{: #obtain-tokens}

Cuando los usuarios o los servicios de programa de fondo interactúan con la app, es posible que necesiten estar autorizados para realizar acciones específicas. {{site.data.keyword.appid_short_notm}} verifica que la entidad que realiza la solicitud esté autorizada y devuelva las señales de acceso y de identidad a la app. Si la entidad que realiza la solicitud es un usuario final, las señales pueden contener información sobre el usuario, por ejemplo, el ámbito de sus permisos y su nombre. Si se trata de un servicio de programa de fondo, sólo se devuelve una señal de acceso.
{: shortdesc}


## Obtención del ID y el secreto de cliente
{: #obtain-clientid-secret}

Para obtener señales, debe tener el ID y el secreto de cliente. Las credenciales son específicas de cada aplicación y se utilizan para ayudar a identificar y validar a los usuarios a los que se puede asignar una señal. 
{: shortdesc}


### Utilizando la GUI
{: #credentials-gui}

1. Vaya al separador **Aplicaciones** del panel de control de {{site.data.keyword.appid_short_notm}}.

2. Si ya tiene un conjunto de credenciales en la lista, puede saltar al paso 3. Si no las tiene, cree una.
    1. En el separador **Aplicaciones**, pulse **Añadir aplicación**.
    2. Asigne un nombre a la aplicación y haga clic en **Guardar** para volver a una lista de las apps registradas. El nombre de la aplicación no puede superar los 50 caracteres.

3. En la lista de apps registradas, seleccione la aplicación con la que desea trabajar. La fila se expande para mostrar las credenciales.

4. Copie el ID y el secreto de cliente.


### Utilizando la API
{: #credentials-api}

1.  Realice una solicitud POST en el punto final [`/management/v4/{tenantId}/applications`](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Applications/mgmt.registerApplication).

  Solicitud:

  ```
  curl -X POST \  https://us-south.appid.cloud.ibm.com/management/v4/39a37f57-a227-4bfe-a044-93b6e6060b61/applications/ \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer IAM_TOKEN' \
  -d '{"name": "ApplicationName"}'
  ```
  {: codeblock}

  Ejemplo de respuesta:

  ```
  {
    "clientId": "c90830bf-11b0-4b65-bffe-9773f8703bad",
    "tenantId": "b42f7429-fc24-48ds-b4f9-616bcc31cfd5",
    "secret": "YWQyNjdkZjMtMGRhZC00ZWRkLThiOTQtN2E3ODEyZjhkOWQz",
    "name": "testing",
    "oAuthServerUrl": "https://us-south.appid.cloud.ibm.com/oauth/v4/b42f7429-fc24-48ds-b4f9-616bcb31cfd5",
    "profilesUrl": "https://us-south.appid.cloud.ibm.com",
    "discoveryEndpoint": "https://us-south.appid.cloud.ibm.com/oauth/v4/b42f7429-fc24-48ds-b4f9-616bcb31cfd5/.well-known/openid-configuration"
  }
  ```
  {: screen}

2. Copie el ID y el secreto de cliente.



## Obtención de señales de identidad y de acceso
{: #obtain-access-id-tokens}

Con un ID y un secreto de cliente, puede obtener las señales de acceso y de identidad siguiendo los pasos siguientes.
{: shortdesc}


### Obtención de señales utilizando un SDK
{: obtain-token-sdk}

1. Obtenga el ID de arrendatario, el ID de cliente, el secreto y el URL de servidor OAuth de sus credenciales.

2. Con la información obtenida en el paso 1, actualice el siguiente fragmento de código y añádalo a su aplicación. El código predeterminado es para Node.js. Si trabaja con otro lenguaje, puede elegir el que se aplica al principio de este tema.

  Node:
  {: ph data-hd-programlang='javascript'}

  ```
  const config = {
    tenantId: "{tenant-id}",
    clientId: "{client-id}",
    secret: "{secret}",
    oauthServerUrl: "{oauth-server-url}"
  };

  const TokenManager = require('ibmcloud-appid').TokenManager;

  const tokenManager = new TokenManager(config);

  async function getAppIdentityToken() {
    try {
        const tokenResponse = await tokenManager.getApplicationIdentityToken();
        console.log('Token response : ' + JSON.stringify(tokenResponse));

        //the token response contains the access_token, expires_in, token_type
    } catch (err) {
        console.log('err obtained : ' + err);
    }
  }
  ```
  {: codeblock}
  {: ph data-hd-programlang='javascript'}

  Java:
  {: ph data-hd-programlang='java'}
  ```
  AppID.getInstance().signinWithResourceOwnerPassword(getApplicationContext(), username, password, new TokenResponseListener() {
    @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
        //Se ha producido una excepción
        }

    @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
        //Usuario autenticado
        }
  });
  ```
  {: codeblock}
  {: ph data-hd-programlang='java'}

Swift de iOS:
{: ph data-hd-programlang='swift'}

  ```
  class delegate : TokenResponseDelegate {
    public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
    //Usuario autenticado
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
    //Se ha producido una excepción
        }
  }

  AppID.sharedInstance.signinWithResourceOwnerPassword(username: username, password: password, delegate: delegate())
  ```
  {: codeblock}
  {: ph data-hd-programlang='swift'}

Swift de servidor:
{: ph data-hd-programlang='swift'}

  ```
  let options = [
    "clientId": "{client-id}",
  	"secret": "{secret}",
  	"tenantId": "{tenant-id}",
  	"oauthServerUrl": "{oauth-server-url}",
  	"redirectUri": "{app-url}" + CALLBACK_URL
  ]
  let webappKituraCredentialsPlugin = WebAppKituraCredentialsPlugin(options: options)
  let kituraCredentials = Credentials()
  kituraCredentials.register(plugin: webappKituraCredentialsPlugin)
  ```
  {: codeblock}
  {: ph data-hd-programlang='swift'}


</br>

### Obtención de señales utilizando la API
{: #obtain-tokens-api}

1. Obtenga el ID de arrendatario, el ID de cliente, el secreto y el URL de servidor OAuth de sus credenciales.

2. Codifique el ID de cliente y el secreto.

    1. Copie el ID de cliente y el secreto siguiendo los pasos de la sección anterior.
    2. Utilice un codificador base64 para codificar la información de autorización.
    3. Copie la salida.

3. Haga una solicitud a la API para obtener una señal. La sección de datos de la solicitud varía en función del tipo de tipo de otorgamiento que utilice. 

  ```
  curl -X POST \
  https://{region}.appid.cloud.ibm.com/oauth/v4/{tenant_id}/token \
  -H 'Authorization: Basic base64Encoded{{client-ID}:{client-secret}}' \
  -H 'Content-Type: application/x-www-form-urlencoded' \
  -H `Accept: application/json` \
  -F grant_type=password \
  -F username=testuser@test.com \
  -F password=testuser
  ```
  {: codeblock}

El tipo de tipo de otorgamiento que utilice para obtener la señal puede diferir según el tipo de autorización con el que trabaje. Para obtener una lista detallada de las opciones, consulte la [documentación de swagger](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Authorization%20Server%20-%20Authorization%20Server%20V4/oauth-server.token).
