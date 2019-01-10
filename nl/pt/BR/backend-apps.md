---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:pre: .pre}
{:tip: .tip}
{:screen: .screen}

# Aplicativos de back-end
{: #adding-backend}

É possível usar os SDKs e as APIs do {{site.data.keyword.appid_full}} para proteger os terminais e as APIs do
aplicativo back-end.
{: shortdesc}


## Entendendo o fluxo
{: #understanding}

**Quando esse fluxo seria útil?**

Parte do desenvolvimento dos aplicativos back-end é verificar se suas APIs estão protegidas contra acesso não
autorizado. Os SDKs do {{site.data.keyword.appid_short_notm}} facilitam a proteção de seus terminais de API e garantem a segurança de seu aplicativo.

**Qual é a base técnica do fluxo?**

O {{site.data.keyword.appid_short_notm}} implementa o
[OAuth2](https://tools.ietf.org/html/rfc6749) e a especificação OIDC, que usa tokens do portador para autenticação e autorização. Esses
tokens são formatados como [JSON Web Tokens](https://tools.ietf.org/html/rfc7519), que são assinados
digitalmente e contêm solicitações que descrevem o assunto que está sendo autenticado e o provedor de
identidade. As APIs de seu aplicativo são protegidas pelos tokens de acesso e de identidade. Clientes que precisam de
acesso às suas APIs podem se autenticar com o provedor de identidade por meio do {{site.data.keyword.appid_short_notm}} em troca desses tokens. As
solicitações nos tokens devem ser validadas para conceder acesso às APIs protegidas.

Para obter mais informações sobre como os tokens são usados no {{site.data.keyword.appid_short_notm}}, consulte [Entendendo os tokens](/docs/services/appid/authorization.html#tokens).
{: tip}

**Qual é o aspecto desse fluxo?**

![Fluxo de back-end do {{site.data.keyword.appid_short_notm}}. As etapas são listadas em ordem na imagem a seguir.](images/backend-flow.png)

1. Um cliente faz uma solicitação de POST para o servidor de autorizações do {{site.data.keyword.appid_short_notm}} para obter um token de acesso. Uma solicitação de POST geralmente tem o seguinte formato:

  ```
  POST/oauth/v3/{tenantId}/token HTTP/1.1
  Content_type: application/x-www-form-urlencoded
  Authorization header = "Basic" + base64encode({clientId}:{secret})
  FormData = {grant_type}
  ```
  {: screen}

2. Se o cliente atender às qualificações, o servidor de autorizações retornará um token de acesso.

3. O cliente envia uma solicitação para o recurso protegido.

4. O recurso protegido ou a API valida o token. Se o token for válido, o acesso ao recurso será concedido para o cliente. Se o token não puder ser validado, o acesso será negado.


## Protegendo recursos com o SDK do Node.js
{: #secure-node}

O SDK do servidor {{site.data.keyword.appid_short_notm}} impõe a autenticação e a autorização com a [Estrutura de passaporte](http://www.passportjs.org/). Com a `ApiStrategy`, é possível proteger os recursos com backup requerendo que os tokens de acesso e de identidade sejam validados no cabeçalho de autorização como parte da solicitação.
{: shortdesc}

**Antes de iniciar**

Deve-se ter os seguintes pré-requisitos antes de poder iniciar:
 * Uma instância do {{site.data.keyword.appid_short_notm}}
 * NPM versão 4 ou superior
 * Node versão 6 ou superior

**Instalando o SDK**

1. Inclua o SDK do Node.js do {{site.data.keyword.appid_short_notm}} no arquivo `package.json` do aplicativo.

  ```
  "dependencies": {
      "ibmcloud-appid": "^4.0.0"
  }
  ```
  {: codeblock}

2. Execute o comando a seguir.

  ```
  npm install
  ```
  {: codeblock}

**Inicializando o SDK**

É possível inicializar o SDK usando um `oauth server url`.

1. Obtenha o seu `oauth server url`.
  1. Navegue para a guia **Credenciais de serviço** do painel do {{site.data.keyword.appid_short_notm}}.
  2. Se você ainda não tiver um conjunto de credenciais, clique em **Nova credencial** e, em seguida, clique em **Incluir** para criar um novo conjunto. Se
você fizer isso, ignore essa etapa.
  3. Clique na alternância **Visualizar credenciais** para ver suas informações.
  4. Copie o seu `oauth server url` para usar na próxima etapa.

2. Inicialize a estratégia de passaporte do {{site.data.keyword.appid_short_notm}}, conforme mostrado no exemplo a seguir.

  ```javascript
  var express = require('express'); 
  var passport = require('passport');
  var APIStrategy = require('ibmcloud-appid').APIStrategy; 
  passport.use(new APIStrategy({ oauthServerUrl: "{oauth-server-url}" })); 
  var app = express();
  app.use(passport.initialize());
  ```
  {: codeblock}


Se o aplicativo Node.js for executado no {{site.data.keyword.Bluemix_notm}} e estiver ligado à sua instância do {{site.data.keyword.appid_short_notm}}, não será necessário fornecer a configuração de estratégia da API. A configuração {{site.data.keyword.appid_short_notm}} obtém as informações usando a variável de ambiente VCAP_SERVICES.
{: tip}

**Protegendo a API**

O fragmento a seguir demonstra como usar o `ApiStrategy` em um aplicativo Express para proteger a API GET `/protected`.

  ```javascript
   app.get('/protected', passport.authenticate('APIStrategy.STRATEGY_NAME', { session: false }), function(request, response){
      console.log("Security context", request.appIdAuthorizationContext);
      response.send(200, "Success!");
      }
   );
   ```
  {: codeblock}

Quando os tokens são válidos, o próximo middleware na cadeia de solicitação é chamado e a propriedade `appIdAuthorizationContext` é incluída no objeto de solicitação. A
propriedade contém os tokens de acesso e de identidade originais, bem como as informações de carga útil
decodificadas dos respectivos tokens.


## Protegendo recursos com o SDK Swift
{: #secure-swift}

É possível usar o {{site.data.keyword.appid_short_notm}} para proteger seus recursos do lado do servidor usando o SDK Swift.
{: shortdesc}

O [SDK do servidor Swift](https://github.com/ibm-cloud-security/appid-serversdk-swift) do
{{site.data.keyword.appid_short_notm}} fornece um plug-in de middleware de proteção de API que é usado para proteger seus aplicativos back-end. Associando suas APIs ao middleware, é possível proteger seu app contra acesso não autorizado. Após a API ser protegida, o middleware assegura que os tokens gerados pelo {{site.data.keyword.appid_short_notm}} sejam validados. Em seguida, é possível modificar o comportamento da API dependendo dos resultados da validação.

Veja o fragmento de código a seguir para um exemplo de como proteger a API `/protectedendpoint`.

```Swift
import Foundation
import Kitura              // server
import Credentials         // middleware
import IBMCloudAppID       // SDK

// setup routes
let router = Router()

// mandatory option to be passed in if app not deployed on IBM Cloud
let options = [
    "oauthServerUrl": "https://appid-oauth.ng.bluemix.net/oauth/v3/d8438de6-c325-4956-ad34-abd49194affd",
]
let apiCreds = Credentials()

// Minimum macOS version required
if #available(OSX 10.12, *) {

    // setup API protection
    let apiKituraCredentialsPlugin = APIKituraCredentialsPlugin(options: options)
    apiCreds.register(plugin: apiKituraCredentialsPlugin)

    // associate route with API protection
    router.all(middleware: apiCreds)

    // create protected API
    router.get("/protectedendpoint") { request, response, next in

        response.headers["Content-Type"] = "text/html; charset=utf-8"
        do {
            if let userProfile = request.userProfile  {
                try response.status(.OK).send(
                    "<!DOCTYPE html><html><body>" +
                        "Welcome " + userProfile.displayName  +
                        "! You are logged in with " + userProfile.provider + ".
" +
                    "</body></html>\n\n").end()
                next()
                return
            }
            try response.status(.unauthorized).send(
                "<!DOCTYPE html><html><body>” + “You are not authorized!" +
                "</body></html>\n\n").end()
        }
        catch {}
        next()
    }

    // Start server
    Kitura.addHTTPServer(onPort: 8090, with: router)

    Kitura.run()  
}
```
{: codeblock}

## Protegendo recursos manualmente
{: secure-api}

A proteção dos aplicativos back-end e dos recursos protegidos envolve a validação de tokens. É possível validar os
tokens de identidade e de acesso do {{site.data.keyword.appid_short_notm}} de várias maneiras. Para ajudar a
validar os tokens, consulte [Validando os tokens](/docs/services/appid/tokens.html).


## Próximas Etapas
{: #next}

Com o {{site.data.keyword.appid_short_notm}} instalado em seu aplicativo, você está quase pronto para começar a autenticar os usuários! Tente executar uma das atividades a seguir em seguida:

* Configure os seus [provedores de identidade](/docs/services/appid/identity-providers.html)
* Customize e configure [o Widget de login](/docs/services/appid/login-widget.html)
* Saiba mais sobre o <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">SDK do Node.js<img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>
* Saiba mais sobre o <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">SDK do Swift<img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>
