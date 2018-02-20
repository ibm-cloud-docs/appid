---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-01"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Gerenciando a experiência de conexão

Com o widget de login, é possível atualizar seu fluxo de conexão a qualquer momento sem incluir, remover ou mudar o código-fonte. O funcionamento pode ocorrer em minutos usando o código fornecido em nossos aplicativos de amostra.
{: shortdesc}

**Nota**: ao configurar provedores de identidade social como o Facebook, o [Fluxo de concessão de autorização Oauth2](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html) é usado para chamar o widget de login.

</br>

## Customizando o código do aplicativo de amostra
{: #login-widget}

É possível customizar a tela de conexão pré-configurada para exibir o logotipo e as cores de sua escolha. Se você deseja exibir suas próprias UIs com marca, consulte [diretório da nuvem](/docs/services/appid/cloud-directory.html).
{: shortdesc}

![Exemplo de experiência de conexão customizada](/images/customize.gif)

Para customizar a tela:

1. Abra o painel
de serviço {{site.data.keyword.appid_short_notm}}.
2. Selecione a seção **Customização de login**, na qual é possível modificar a aparência do widget de login para alinhar com a marca da sua
empresa.
3. Faça upload do logotipo da sua empresa selecionando um arquivo PNG ou JPG em seu sistema local. O tamanho da imagem recomendado é 320 x 320 pixels. O tamanho máximo do arquivo é 100 Kb.
4. Selecione uma cor de cabeçalho para o widget no selecionador de cor ou insira o código hexadecimal para outra cor.
5. Inspecione a área de janela de visualização e clique em **Salvar mudanças** quando estiver satisfeito com as suas customizações. Uma mensagem de confirmação será exibida.
6. Verifique suas mudanças visitando seu app. Não é necessário reconstruir o seu app. Suas imagens serão armazenadas no banco de dados do {{site.data.keyword.appid_short}} e serão exibidas na próxima vez que o widget de login for chamado.


</br>

## Chamando o widget de login com o SDK Android
{: #android}

Com os provedores de identidade social ativados, é possível chamar a tela de conexão pré-configurada com o SDK Android.
{: shortdesc}

1. Configure seus provedores de identidade.
2. Coloque o comando a seguir em seu código.
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


</br>

## Chamando o widget de login com o SDK iOS Swift
{: ios-swift}

Com os provedores de identidade social ativados, é possível chamar a tela de conexão pré-configurada com o SDK iOS Swift.
{: shortdesc}

1. Configure seus provedores de identidade.
2. Inclua o comando a seguir em seu código de app.
  ```swift
  import BluemixAppID
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


</br>

## Chamando o widget de login com o SDK Node.js
{: #nodejs}

Com os provedores de identidade social ativados, é possível chamar a tela de conexão pré-configurada com o SDK Node.js.
{: shortdesc}

1. Configure seus provedores de identidade.
2. Inclua o comando a seguir em seu código.
    ```JavaScript

    var express = require('express');
  var passport = require('passport');
  var WebAppStrategy = require('bluemix-appid').WebAppStrategy;
    ```
    {: codeblock}


</br>

## Chamando o widget de login com o SDK Swift
{: #swift}

Com os provedores de identidade social ativados, é possível chamar a tela de conexão pré-configurada com o SDK Swift.
{: shortdesc}

O WebAppKituraCredentialsPlugin é baseado no fluxo de concessão de código de autorização OAuth2 e deve ser usado para aplicativos da web que usam navegadores. O
plug-in fornece ferramentas para implementar fluxos de autenticação e de autorização. O plug-in também fornece mecanismos para detectar tentativas não autenticadas
para acessar recursos protegidos e automaticamente redireciona um navegador do usuário para a página de autenticação. Após a autenticação bem-sucedida, um usuário é
levado para a URL de retorno de chamada do aplicativo da web, que usa o plug-in para obter tokens de acesso e a identidade do
{{site.data.keyword.appid_short_notm}}. Após obter esses tokens, o plug-in os armazena em uma sessão de HTTP sob WebAppKituraCredentialsPlugin.AuthContext.

O código a seguir demonstra como usar WebAppKituraCredentialsPlugin em um aplicativo Kitura para proteger o terminal `/protected`.

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
