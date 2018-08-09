---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}


# Protegendo recursos de backend
{: #secure-back-end}

É possível usar os SDKs do servidor {{site.data.keyword.appid_short_notm}} para proteger recursos em seu app Node.js. Também é possível usar os SDKs do cliente para acessar recursos protegidos.
{: shortdesc}

Chamar um recurso protegido iniciará o widget de login, se necessário. Se um token válido já tiver sido obtido, o widget de login não será iniciado e o recurso será acessado diretamente.
{: tip}

## Protegendo recursos no Liberty for Java
{: #protecting-liberty}

É possível usar o {{site.data.keyword.appid_short_notm}} para proteger terminais em
seus apps IBM Liberty for Java. O Liberty for Java tem a capacidade integrada para manipular solicitações Open ID Connect (OIDC).
{: shortdesc}



Antes de iniciar:
* Você precisa de um app <a href="https://console.bluemix.net/catalog/starters/liberty-for-java" target="_blank">{{site.data.keyword.Bluemix_notm}} Liberty for Java <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> existente e ilimitado. Para se familiarizar com o desenvolvimento de
apps Liberty for Java, veja [os docs](/docs/runtimes/liberty/index.html).
* Certifique-se de que você tenha <a href="https://maven.apache.org/download.cgi" target="_blank">Apache Maven <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> instalado.
* Aprenda sobre como o OIDC funciona com o Liberty for Java.



Para proteger seus recursos:

1. Faça download da amostra do Liberty for Java na UI. A amostra contém um arquivo compactado com os arquivos Liberty padrão.
2. Abra o terminal no diretório no qual você extraiu a amostra.
3. Efetue login no {{site.data.keyword.Bluemix_notm}} usando a linha de comandos do
Cloud Foundry. Quando solicitado, insira suas credenciais.
  ```
  cf login
  ```
  {: codeblock}

4. Implemente o app. Executar o comando a seguir cria uma instância do Liberty for Java com um nome que está relacionado ao ID do locatário.
  ```
  cf push
  ```
  {: codeblock}

5. Conecte a instância de serviço à nova instância do Liberty for Java e reimplemente o app.
6. Abra seu app em um navegador e efetue login usando suas credenciais para revisar as atividades de autenticação.

## Protegendo recursos no Node.js
{: #protecting-resources-nodesdk}

O SDK do servidor {{site.data.keyword.appid_short_notm}} fornece uma estratégia de passaporte ApiStrategy que é usada em aplicativos backend que são implementados no {{site.data.keyword.Bluemix_notm}}. Para proteger o seu app contra acesso não autorizado, deve-se instrumentar o seu servidor Node.js com a
ApiStrategy. O `appid-serversdk-nodejs npm module` fornece a estratégia de passaporte ApiStrategy e o método de verificação para validar o token de
acesso e o token de ID emitidos pelo {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

O SDK do servidor {{site.data.keyword.appid_short_notm}} usa a estrutura do <a href="http://passportjs.org/" target="_blank">Passport
<img src="../../icons/launch-glyph.svg" alt="ícone de Link externo"></a> para impingir a autorização.

O fragmento a seguir demonstra como usar o `APIStrategy` em um app Express simples para proteger os métodos GET de terminal `/protected`.
  ```JavaScript

  var express = require('express');
  var passport = require('passport');
  var APIStrategy = require('bluemix-appid').APIStrategy;

  passport.use(new APIStrategy());
  var app = express();
  app.use(passport.initialize());

  app.get('/protected', passport.authenticate('APIStrategy.STRATEGY_NAME', {session: false }),
      function(request, response){
          console.log("Securty context", request.securityContext)    
          response.send(200, "Success!");
      }
  );

  app.listen(process.env.PORT);
  ```
  {: codeblock}


## Protegendo recursos com o SDK Swift
{: #requesting-swift}

É possível usar o {{site.data.keyword.appid_short_notm}} para proteger seus recursos do lado do servidor usando o SDK Swift.
{: shortdesc}

O SDK do servidor Swift do {{site.data.keyword.appid_short_notm}} fornece um plug-in de middleware de proteção de API que é usado para proteger seus apps de backend. Associando suas APIs ao middleware, é possível proteger seu app contra acesso não autorizado. Após a API ser protegida, o middleware assegura que os tokens gerados pelo {{site.data.keyword.appid_short_notm}} sejam validados. Em seguida, é possível modificar o comportamento da API dependendo dos resultados da validação.

Veja o fragmento de código a seguir para um exemplo de como proteger a API `/protectedendpoint`.

```Swift
import Foundation
import Kitura              // server
import Credentials         // middleware
import BluemixAppID        // SDK

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


## Acessando recursos protegidos com o SDK do Swift iOS
{: #requesting-swift}

É possível usar o {{site.data.keyword.appid_short_notm}} para proteger terminais em seus apps iOS Swift.
{: shortdesc}

1. Importe o BMSCore.
  ```swift
  import BMSCore
  ```
  {: codeblock}

2. Chame uma solicitação de recurso protegido.
  ```swift
  BMSClient.sharedInstance.initialize(bluemixRegion: AppID.<region>)
  BMSClient.sharedInstance.authorizationManager = AppIDAuthorizationManager(appid:AppID.sharedInstance)
  var request:Request =  Request(url: "<your protected resource url>")
  request.send(completionHandler: {(response:Response?, error:Error?) in
      //code handling the response here
  })
  ```
  {: codeblock}


## Acessando recursos protegidos com o SDK Android
{: #requesting-android}

É possível usar o {{site.data.keyword.appid_short_notm}} para proteger terminais em seus apps Android.
{: shortdesc}

1. Chame uma solicitação de recurso protegido.
  ```java
  BMSClient bmsClient = BMSClient.getInstance();
  bmsClient.initialize(getApplicationContext(), AppID.REGION_UK);

  AppIDAuthorizationManager appIdAuthMgr = new AppIDAuthorizationManager(AppID.getInstance())
  bmsClient.setAuthorizationManager(appIdAuthMgr);

  Request request = new Request("<your protected resource url>", Request.GET);
  request.send(this, new ResponseListener() {
  @Override
		public void onSuccess (Response response) {
     //code handling the response here
  }
  @Override
		public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
      //code handling the failure here
  });
  ```
  {: codeblock}
