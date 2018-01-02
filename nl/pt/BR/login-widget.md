---

copyright:
  years: 2017
lastupdated: "2017-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Gerenciando o log em experiência
É possível obter um fluxo de conexão funcionando em minutos com o widget de login. É possível atualizar seu widget ou tema em qualquer momento sem incluir, remover ou mudar o sinal no código-fonte.
{: shortdesc}



## Customizando o widget de login
{: #login-widget}

É possível configurar o seu widget de login para exibir o logotipo e as cores de sua preferência.
{: shortdesc}

Quando o serviço do {{site.data.keyword.appid_short}} estiver configurado com dois ou mais provedores de identidade, o usuário poderá selecionar um
provedor de identidade no widget de login. É possível customizar o seu widget de login concluindo as etapas a seguir:

1. Abra o painel
de serviço {{site.data.keyword.appid_short_notm}}.
2. Selecione a seção **Customização de login**, na qual é possível modificar a aparência do widget de login para alinhar com a marca da sua
empresa.
3. Faça upload do logotipo da sua empresa selecionando um arquivo PNG ou JPG em seu sistema local. O tamanho da imagem recomendado é 320 x 320 pixels. O tamanho máximo do arquivo é 100 Kb.
4. Selecione uma cor de cabeçalho para o widget no selecionador de cor ou insira o código hexadecimal para outra cor.
5. Inspecione a área de janela de visualização e clique em **Salvar mudanças** quando estiver satisfeito com as suas customizações. Uma mensagem de confirmação será exibida.

**Nota**: não será necessário reconstruir o seu aplicativo. A imagem é armazenada no banco de dados do {{site.data.keyword.appid_short}} e é exibida no próximo login.

## Executando o widget de login com o SDK Android
{: #authenticate-android}

Quando você configura mais de um provedor de identidade, os usuários exibem um widget de login ao visitar seu app. Como padrão, se você configurar somente um, o usuário será redirecionado para a tela de autenticação de provedores de identidade configurados.


Após o SDK do cliente do {{site.data.keyword.appid_short_notm}} ser inicializado, será possível autenticar os seus usuários executando o widget de login.

  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launch(this, new AuthorizationListener() {
        @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //Exception occurred
        }

        @Override
        public void onAuthorizationCanceled () {
          //Authentication canceled by the user
        }

        @Override
        public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
          //User authenticated
        }
      });
  ```
  {: codeblock}

## Executando o widget de login com o SDK iOS
{: #authenticate-ios}

Quando você configura mais de um provedor de identidade, os usuários exibem um widget de login ao visitar seu app. Como padrão, se você configurar somente um, o usuário será redirecionado para a tela de autenticação de provedores de identidade configurados.


1. Inclua a importação a seguir no arquivo no qual você deseja usar o SDK.

  ```swift
  import BluemixAppID
  ```
  {: codeblock}

2. Execute o comando a seguir para ativar o widget.

  ```swift
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, response:Response?) {
          //User authenticated
      }

      public func onAuthorizationCanceled() {
          //Authentication canceled by the user
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          //Exception occurred
      }
  }

  AppID.sharedInstance.loginWidget?.launch(delegate: delegate())
  ```
  {: codeblock}

## Executando o widget de login com o SDK Node.js
{: #authenticate-nodejs}

É possível usar `WebAppStrategy` para proteger recursos de aplicativo da web.

  ```JavaScript

  var express = require('express');
  var passport = require('passport');
  var WebAppStrategy = require('bluemix-appid').WebAppStrategy;
  ```
  {: codeblock}


## Executando o widget de login com o SDK Swift
{: #authenticate-swift}

O WebAppKituraCredentialsPlugin é baseado no fluxo de concessão authorization_code do OAuth2 e deve ser usado para aplicativos da web que usam navegadores. O
plug-in fornece ferramentas para implementar fluxos de autenticação e de autorização. O plug-in também fornece mecanismos para detectar tentativas não autenticadas
para acessar recursos protegidos e automaticamente redireciona um navegador do usuário para a página de autenticação. Após a autenticação bem-sucedida, um usuário é
levado para a URL de retorno de chamada do aplicativo da web, que usa o plug-in para obter tokens de acesso e a identidade do
{{site.data.keyword.appid_short_notm}}. Após obter esses tokens, o plug-in os armazena em uma sessão de HTTP sob WebAppKituraCredentialsPlugin.AuthContext.

O código a seguir demonstra como usar o WebAppKituraCredentialsPlugin em um aplicativo Kitura para proteger o terminal `/protected`.

  ```swift
  import Foundation
  import Kitura
  import KituraSession
  import Credentials
  import SwiftyJSON
  import BluemixAppID

  // The following URLs will be used for AppID OAuth flows
  var LOGIN_URL = "/ibm/bluemix/appid/login"
  var CALLBACK_URL = "/ibm/bluemix/appid/callback"
  var LOGOUT_URL = "/ibm/bluemix/appid/logout"
  var LANDING_PAGE_URL = "/index.html"

  // Setup Kitura to use session middleware
  // Must be configured with proper session storage for production
  // environments. See https://github.com/IBM-Swift/Kitura-Session for
  // additional documentation
  let router = Router()
  let session = Session(secret: "Some secret")
  router.all(middleware: session)

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

  // Explicit login endpoint
  router.get(LOGIN_URL,
  		   handler: kituraCredentials.authenticate(credentialsType: webappKituraCredentialsPlugin.name,
  												   successRedirect: LANDING_PAGE_URL,
  												   failureRedirect: LANDING_PAGE_URL
  ))

  // Callback to finish the authorization process. Will retrieve access and identity tokens from AppID
  router.get(CALLBACK_URL,
  		   handler: kituraCredentials.authenticate(credentialsType: webappKituraCredentialsPlugin.name,
  												   successRedirect: LANDING_PAGE_URL,
  												   failureRedirect: LANDING_PAGE_URL
  ))

  // Logout endpoint. Clears authentication information from session
  router.get(LOGOUT_URL, handler:  { (request, response, next) in
  	kituraCredentials.logOut(request: request)
  	webappKituraCredentialsPlugin.logout(request: request)
  	_ = try? response.redirect(LANDING_PAGE_URL)
  })

  // Protected area
  router.get("/protected", handler: kituraCredentials.authenticate(credentialsType: webappKituraCredentialsPlugin.name), { (request, response, next) in
      let appIdAuthContext:JSON? = request.session?[WebAppKituraCredentialsPlugin.AuthContext]
      let identityTokenPayload:JSON? = appIdAuthContext?["identityTokenPayload"]

      guard appIdAuthContext?.dictionary != nil, identityTokenPayload?.dictionary != nil else {
          response.status(.unauthorized)
          return next()
      }

      response.send(json: identityTokenPayload!)
      next()
  })
  var port = 3000
  if let portString = ProcessInfo.processInfo.environment["PORT"]{
      port = Int(portString)!
  }
  print("Starting on \(port)")

  // Add an HTTP server and connect it to the router
  Kitura.addHTTPServer(onPort: port, with: router)

  // Start the Kitura runloop (this call never returns)
  Kitura.run()
  ```
  {: codeblock}
