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

# Identidade e autorização do aplicativo
{: #app}

Com o {{site.data.keyword.appid_short_notm}}, é possível proteger aplicativos usando o fluxo de identidade e
autorização do aplicativo aproveitando os recursos do OAuth2.0.
{: shortdesc}

## Entendendo o fluxo de comunicação
{: #understanding}

**Quando esse fluxo seria útil?**

Há várias razões pelas quais você pode desejar que um aplicativo se comunique com outro serviço ou aplicativo sem nenhuma intervenção do usuário. Por exemplo, um aplicativo não interativo que precisa acessar outro aplicativo para executar seu trabalho. Isso pode incluir processos, CLIs, daemons ou um dispositivo IoT que monitora e relata variáveis de ambiente para um servidor de envio de dados. O
caso de uso específico é exclusivo para cada aplicativo, mas a coisa mais importante a ser lembrada é que as
solicitações são trocadas em nome do aplicativo, não em nome de um usuário final, e é o aplicativo que é autenticado e
autorizado.

Confira esse exemplo em <a href="https://www.ibm.com/blogs/bluemix/2018/02/using-app-id-secure-docker-kubernetes-applications/" target="_blank">Usando o {{site.data.keyword.appid_short_notm}} para proteger os aplicativos do Docker e do Kubernetes <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.

**Como funciona o fluxo de autorização e de identidade do aplicativo?**

O {{site.data.keyword.appid_short_notm}} aproveita o fluxo de credenciais do cliente OAuth2.0 para
proteger a comunicação. Depois que um aplicativo é registrado com o {{site.data.keyword.appid_short_notm}}, ele obtém um identificador de cliente e um segredo. Com
essas informações, o aplicativo pode solicitar um token de acesso por meio do
{{site.data.keyword.appid_short_notm}} e ser autorizado a acessar uma API ou um recurso protegido. No
fluxo de identidade e autorização do aplicativo, apenas um token de acesso é fornecido ao aplicativo. Ele não obtém um token de identidade ou um token de atualização. Para
obter mais informações sobre tokens, consulte [Entendendo os tokens](/docs/services/appid/authorization.html#tokens).

Esse fluxo de trabalho é destinado a ser usado apenas com aplicativos confiáveis em que não há risco de o segredo ser
usado indevidamente ou vazado. O aplicativo sempre mantém o segredo do cliente. Ele não funcionará para aplicativos móveis.
{: tip}

**Qual é o aspecto do fluxo?**

Na imagem a seguir, é possível ver a direção da comunicação entre o serviço e seu aplicativo.

![Fluxo de autorização e identidade de aplicativo do {{site.data.keyword.appid_short_notm}}](images/app-to-app-flow.png)
Figura. Fluxo de autorização e identidade de aplicativo

1. O aplicativo A é registrado com o {{site.data.keyword.appid_short_notm}} para obter um identificador de cliente e um segredo.
2. O aplicativo A faz uma solicitação para o {{site.data.keyword.appid_short_notm}} enviando as credenciais recuperadas na etapa anterior.
3. O {{site.data.keyword.appid_short_notm}} valida a solicitação, autentica o aplicativo e retorna uma resposta ao Aplicativo A que contém um token de acesso.
4. O aplicativo A agora é capaz de usar o token de acesso para enviar solicitações ao Aplicativo B, tal como um recurso
protegido.

## Registrando seu aplicativo
{: #registering}

**Registrando seu aplicativo com a GUI**

1. Na guia **Aplicativo** do painel do {{site.data.keyword.appid_short_notm}}, clique em **Incluir aplicativo**.
2. Inclua o nome do aplicativo e clique em **Salvar** para retornar a uma lista de seus aplicativos registrados. O nome de seu aplicativo não pode exceder 50 caracteres.
3. Na lista de apps registrados, selecione o aplicativo que você incluiu na etapa anterior. A linha se expande para mostrar suas credenciais.

**Registrando seu aplicativo com a API**

1. Faça uma solicitação de POST para o terminal [`/management/v4/{tenantId}/applications`](https://appid-management.ng.bluemix.net/swagger-ui/#!/Applications/registerApplication).

  Solicitação:
  ```
  curl -X POST \  https://appid-management.ng.bluemix.net/management/v4/39a37f57-a227-4bfe-a044-93b6e6060b61/applications/ \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer IAM_TOKEN' \
  -d '{"name": "ApplicationName"}'
  ```
  {: codeblock}

  Resposta de exemplo:
  ```
  {
  "clientId": "111c22c3-38ea-4de8-b5d4-338744d83b0f",
   "tenantId": "39a37f57-a227-4bfe-a044-93b6e6060b61",
  "secret": "ZmE5ZDQ5ODctMmA1ZS00OGRiLWExZDMtZTA1MjkyZTc4MDB4",
  "name": "ApplicationName",
   "oAuthServerUrl": "https://appid-oauth.eu-gb.bluemix.net/oauth/v3/39a37f57-a227-4bfe-a044-93b6e6060b61"
   }
  ```
  {: codeblock}


## Obtendo um token de acesso
{: #obtain-token}

Após o seu aplicativo ser registrado com o {{site.data.keyword.appid_short_notm}} e você obter suas credenciais,
será possível fazer uma solicitação para o servidor de autorizações {{site.data.keyword.appid_short_notm}} para obter um token de acesso.

1. Faça uma solicitação de HTTP POST para o [terminal `/oauth/v3/{tenantId}/token`](https://appid-oauth.ng.bluemix.net/swagger-ui/#!/Authorization_Server_V3/token). A
autorização para a solicitação é `Basic auth` com o identificador de cliente e o segredo sendo usado
como o nome de usuário e a senha que são codificados em Base64.

  Solicitação:
  ```
  curl -X POST \
    http://localhost:6002/oauth/v3/39a37f57-a227-4bfe-a044-93b6e6060b61/token \
    -H 'Authorization: Basic base64Encoded{clientId:secret}' \
    -H 'Content-Type: application/x-www-form-urlencoded' \
    -d grant_type=client_credentials
  ```
  {: codeblock}

  Resposta de exemplo:
  ```
  {
  "access_token": "eyJhbGciOiJS...F9A",
  "expires_in": "3600",
  "token_type": "Bearer"
  }
  ```
  {: codeblock}


## Tutorial: fluxo de ponta a ponta com o SDK Node.js
{: tutorial-node}

1. Obtenha um [token de acesso](/docs/services/appid/authorization.html#tokens) de uma das seguintes maneiras:

  * Por meio do [SDK do servidor Node.js](https://github.com/ibm-cloud-security/appid-serversdk-nodejs) do {{site.data.keyword.appid_short_notm}} usando o gerenciador de token. Inicialize o gerenciador de token com suas credenciais de aplicativo e faça uma chamada para o método `getApplicationIdentityToken()` para obter o token.

    ```
    const TokenManager = require('ibmcloud-appid').TokenManager;
    const config = {
     clientId: "29a19759-aafb-41c7-9ef7-ee7b0ca88818",
     tenantId: "39a37f57-a227-4bfe-a044-93b6e6060b61",
     secret: "ZTEzZTA2MDAtMjljZS00MWNlLTk5NTktZDliMjY3YzUxZTYx",
     oauthServerUrl: "https://appid-oauth.eu-gb.bluemix.net/oauth/v3/39a37f57-a227-4bfe-a044-93b6e6060b61"
    };

    const tokenManager = new TokenManager(config);

    tokenManager.getApplicationIdentityToken().then((appIdAuthContext) => {
     console.log(' Access tokens from SDK : ' + JSON.stringify(appIdAuthContext));
    }).catch((err) => {
     //console.error('Error retrieving tokens : ' + err);
    });
    ```
    {: codeblock}

  * Por meio do servidor de autorizações do {{site.data.keyword.appid_short_notm}}. **Nota**: o `oauthServerUrl` na solicitação é obtido ao registrar o aplicativo. Se você registrou seu aplicativo com as APIs de gerenciamento, a URL do servidor estará no corpo de resposta. Se
você registrou seu aplicativo ligando-o ao console do IBM Cloud, a URL poderá ser localizada em seu objeto JSON VCAP_SERVICES ou por meio de seus segredos do Kubernetes.

    ```
    var request = require('request');

    function getAccessToken() {
      let options = {
          method: 'POST',
          url: oauthServerUrl + '/token',
          headers: { 'content-type': 'application/x-www-form-urlencoded',
              'Authorization': 'Basic ' +Buffer.from('clientId: secret').toString('base64')
          },
          form: {
              grant_type: 'client_credentials'
          }
      };

      return new Promise((resolve, reject) => {
          request(options, function (error, response, body) {
              if (error) {
                  return reject(error);
              }

              let data = JSON.parse(body);
              if(data.access_token) {
                  resolve(data.access_token);
              } else {
                  reject(data);
              }
          })
      });
    }
    ```
    {: codeblock}

2. Faça uma solicitação para seu recurso protegido usando o token de acesso obtido na etapa anterior.

  ```
  let options = {
      method: 'GET',
      url: 'http://localhost:8081/protected_resource',
      headers: { authorization : 'Bearer ' + accessToken}
  }

  request(options, function (error, response, body) {
      if (error) {
       console.log(error)
      } else {
          res.status(response.statusCode).send({
      console.log(JSON.stringify(body));
          });
      }
  });
  ```
  {: codeblock}

3. Faça com que seus recursos protegidos fiquem seguros usando a estratégia de API por meio do SDK do Node.js do {{site.data.keyword.appid_short_notm}}.

  ```
  const express = require('express'),
    passport = require('passport');

  var app = express();
app.use(passport.initialize());

  passport.use(new APIStrategy({
      oauthServerUrl: "https://appid-oauth.eu-gb.bluemix.net/oauth/v3/398ec248-5e93-48b8-a122-ccabc714fe85",
      tenantId:"398ec248-5e93-48b8-a122-ccabc714fe85"
  }));

  app.get('/protected_resource',
      passport.authenticate(APIStrategy.STRATEGY_NAME, {session: false}),
      (req, res) => {
          res.send("Hello from protected resource");
  });
  ```
  {: codeblock}
