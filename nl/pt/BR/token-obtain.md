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



# Obtendo tokens
{: #obtain-tokens}

Quando os usuários ou os serviços de back-end interagem com seu app, eles podem precisar de autorização para executar ações específicas. O {{site.data.keyword.appid_short_notm}} verifica se a entidade que faz a solicitação está autorizada e retorna tokens de acesso e de identidade para seu app. Se a entidade que faz a solicitação for um usuário final, os tokens poderão conter informações sobre o usuário, como o escopo de suas permissões e seu nome. Se for um serviço de back-end, somente um token de acesso será retornado.
{: shortdesc}


## Obtendo seu identificador de cliente e segredo
{: #obtain-clientid-secret}

Para obter tokens, deve-se ter seu identificador de cliente e segredo. As credenciais são específicas para cada aplicativo e são usadas para ajudar a identificar e validar os usuários para os quais um token pode ser designado.
{: shortdesc}


### Usando a GUI
{: #credentials-gui}

1. Navegue para a guia **Aplicativos** do painel do {{site.data.keyword.appid_short_notm}}.

2. Se você já tiver um conjunto de credenciais listadas, será possível ir para a etapa 3. Se ainda não tiver, crie um.
    1. Na guia **Aplicativos**, clique em **Incluir aplicativo**.
    2. Forneça um nome ao seu aplicativo e clique em **Salvar** para retornar para uma lista de seus apps registrados. O nome de seu aplicativo não pode exceder 50 caracteres.

3. Na lista de apps registrados, selecione o aplicativo com o qual deseja trabalhar. A linha se expande para mostrar suas credenciais.

4. Copie seu identificador de cliente e segredo.


### Usando a API
{: #credentials-api}

1.  Faça uma solicitação de POST para o terminal [`/management/v4/{tenantId}/applications`](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Applications/mgmt.registerApplication).

  Solicitação:

  ```
  curl -X POST \  https://us-south.appid.cloud.ibm.com/management/v4/39a37f57-a227-4bfe-a044-93b6e6060b61/applications/ \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer IAM_TOKEN' \
  -d '{"name": "ApplicationName"}'
  ```
  {: codeblock}

  Resposta de exemplo:

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

2. Copie o identificador de cliente e o segredo.



## Obtendo tokens de acesso e de identidade
{: #obtain-access-id-tokens}

Com um identificador de cliente e um segredo, é possível obter tokens de acesso e de identidade usando as etapas a seguir.
{: shortdesc}


### Obtendo tokens usando um SDK
{: obtain-token-sdk}

1. Obtenha seu ID de locatário, ID de cliente, segredo e URL do OAuth Server por meio de suas credenciais.

2. Usando as informações da etapa 1, atualize o fragmento de código a seguir e inclua-o em seu aplicativo. O código padrão é para Node.js. Se estiver trabalhando com outro idioma, será possível escolher aquele que se aplique a você no início deste tópico.

  Nó:
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
  AppID.getInstance().signinWithResourceOwnerPassword(getApplicationContext(), username, password,
         new TokenResponseListener() {
    @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
        //Exception occurred
      }

    @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
        //User authenticated
        }
  });
  ```
  {: codeblock}
  {: ph data-hd-programlang='java'}

iOS Swift:
{: ph data-hd-programlang='swift'}

  ```
  class delegate : TokenResponseDelegate {
    public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
    //User authenticated
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
    //Exception occurred
        }
  }

  AppID.sharedInstance.signinWithResourceOwnerPassword(username: username, password: password, delegate: delegate())
  ```
  {: codeblock}
  {: ph data-hd-programlang='swift'}

Servidor Swift:
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

### Obtendo tokens usando a API
{: #obtain-tokens-api}

1. Obtenha seu ID de locatário, ID de cliente, segredo e URL do OAuth Server por meio de suas credenciais.

2. Codifique o ID e o segredo do cliente.

    1. Copie seu identificador de cliente e o segredo usando as etapas da seção anterior.
    2. Use um codificador Base64 para codificar suas informações de autorização.
    3. Copie a saída.

3. Faça uma solicitação para a API para obter um token. A seção de dados de sua solicitação varia, dependendo do tipo de concessão que você está usando. 

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

O tipo de concessão usado para obter seu token pode diferir dependendo do tipo de autorização com a qual você está trabalhando. Para obter uma lista detalhada de opções, verifique a [documentação do swagger](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Authorization%20Server%20-%20Authorization%20Server%20V4/oauth-server.token).
