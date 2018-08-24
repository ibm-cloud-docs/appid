---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-09"

---

{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:pre: .pre}
{:new_window: target="blank"}
{:shortdesc: .shortdesc}


# Exibindo as telas padrão
{: #default}

O {{site.data.keyword.appid_full}} fornece um widget de login que permite fornecer a seus usuários opções de conexão segura.
{: shortdesc}

Quando seu app é configurado para usar um provedor de identidade, os visitantes em seu app são direcionados para uma tela de conexão pelo widget de login. 
Como padrão, quando apenas um provedor está configurado como **Ativado**, os visitantes são redirecionados para
essa tela de autenticação de provedores de identidade. Com o widget de login, é possível exibir uma tela de conexão padrão ou, com o diretório da nuvem, é possível reutilizar as IUs existentes. 
E, como uma bonificação incluída, é possível atualizar o fluxo de conexão em qualquer momento, sem mudar o código-fonte de
forma alguma!


O serviço usa tipos de concessão do OAuth 2 para mapear o processo de autorização. Quando você configura provedores de identidade social, como o Facebook, o [Fluxo de concessão de autorização Oauth2](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html) é usado para chamar o widget de login.

Deseja criar uma experiência que seja exclusiva do seu aplicativo? É possível  [ trazer suas próprias telas ](/docs/services/appid/branded.html)!
{: tip}


## Customizando a tela de conexão padrão
{: #login-widget}

É possível customizar a tela de conexão pré-configurada para exibir o logotipo e as cores de sua escolha.
{: shortdesc}

Para customizar a tela:

1. Abra o painel
de serviço {{site.data.keyword.appid_short_notm}}.
2. Selecione a seção **Customização de login**. É possível modificar a aparência do widget de login para alinhar com a marca da sua empresa.
3. Faça upload do logotipo da sua empresa selecionando um arquivo PNG ou JPG em seu sistema local. O tamanho da imagem recomendado é 320 x 320 pixels. O tamanho máximo do arquivo é 100 Kb.
4. Selecione uma cor de cabeçalho para o widget no selecionador de cor ou insira o código hexadecimal para outra cor.
5. Inspecione a área de janela de visualização e clique em **Salvar mudanças** quando estiver satisfeito com as suas customizações. Uma mensagem de confirmação será exibida.
6. Em seu navegador, atualize sua página de login para verificar suas mudanças.


## Planejando quais telas exibir
{: #plan}

O {{site.data.keyword.appid_short_notm}} fornece uma tela de login padrão que poderá ser chamada se você não tiver suas próprias telas de IU para exibir.
{: shortdesc}

Dependendo da configuração do provedor sua identidade, as telas que podem ser exibidas são diferentes. O serviço não fornece funcionalidade avançada para provedores de identidade social porque não temos acesso às informações de contas dos usuários. Os usuários precisam acessar o provedor de identidade para gerenciar suas informações. Por exemplo, se eles desejassem mudar sua senha do Facebook, eles precisariam acessar www.facebook.com.

Verifique a tabela a seguir para ver quais telas podem ser exibidas para cada tipo de provedor de identidade.

<table>
  <thead>
    <tr>
      <th>Tela de exibição</th>
      <th>Provedor de identidade social</th>
      <th>Provedor de identidade corporativa</th>
      <th>Diretório da nuvem</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Conectar</td>
      <td><img src="images/confirm.png" width="32" alt="Recurso Disponível" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="Recurso Disponível" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="Recurso Disponível" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Inscrever</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Recurso Disponível" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Senha esquecida</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Recurso Disponível" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Mudar senha</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Recurso Disponível" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Detalhes da conta</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Recurso Disponível" style="width:32px;" /></td>
    </tr>
  </tbody>
</table>

Depois de ter definido suas configurações para [provedores de identidade social](/docs/services/appid/identity-providers.html) e [diretório da nuvem](/docs/services/appid/cloud-directory.html), clique na linguagem de sua escolha na imagem a seguir para começar a implementar o código.


Clique na imagem para usar um dos SDKs fornecidos ou as APIs. Não se esqueça de que é possível tirar vantagem do ID
do app com outros idiomas também. Usando as nossas APIs, é possível configurar um diretório de nuvem em qualquer aplicativo. Para
obter ajuda com os idiomas que não estão listados na imagem, confira os
<a href="https://www.ibm.com/blogs/bluemix/tag/app-id/" target="_blank">nossos
blogs<img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"> </a>.
{: shortdesc}

</br>

## Exibindo as telas padrão com o SDK Android
{: #android}

É possível chamar as telas pré-configuradas com o SDK Android.
{: shortdesc}

</br>

**Conectar**
1. Coloque o comando a seguir em seu código.
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
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
            //User authenticated
        }
        });
    ```
  {: pre}

</br>
**Inscrever**

1. Configure **Permitir que os usuários se inscrevam e reconfigurem sua senha** para **Ligado** nas configurações para o diretório da nuvem.
2. Chame o LoginWidget para iniciar o fluxo de inscrição.
  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
 loginWidget.launchSignUp(this, new AuthorizationListener() {
  		 @Override
          public void onAuthorizationFailure (AuthorizationException exception) {
          }

  		 @Override
          public void onAuthorizationCanceled () {
          }

  		 @Override
  		 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
  			 if (accessToken != null && identityToken != null) {
  			 } else {
  			 }

  		 }
  	 });
  ```
  {: pre}

</br>
**Esqueci a senha**

1. Configure **Permitir que os usuários se inscrevam e reconfigurem sua senha** e **E-mail de Esqueci a senha** para **Ligado** nas configurações para o diretório da nuvem.
2. Chame o LoginWidget para iniciar o fluxo Esqueci a senha.
    ```java
    LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launchForgotPassword(this, new AuthorizationListener() {
   			 @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
   			 }

   			 @Override
        public void onAuthorizationCanceled () {
   			 }

   			 @Override 			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) { 			 }
   		 });
    ```
    {: pre}

</br>
**Detalhes da conta**

1. Configure **Permitir que os usuários se inscrevam e reconfigurem sua senha** para **Ligado** nas configurações para o diretório da nuvem.
2. Chame o LoginWidget para iniciar o fluxo de detalhes de mudança.
   ```java
   LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
   loginWidget.launchChangeDetails(this, new AuthorizationListener() {
  			 @Override
          public void onAuthorizationFailure (AuthorizationException exception) {
          }

  			 @Override
          public void onAuthorizationCanceled () {
          }

  			 @Override 			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) { 			 }
  		 });
   ```
   {: pre}

</br>
**Mudar senha**

1. Configure **Permitir que os usuários se inscrevam e reconfigurem sua senha** para **LIGADO**, nas configurações para o diretório da nuvem.
2. Chame o LoginWidget para iniciar o fluxo de mudança de senha.
   ```java
    LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launchChangePassword(this, new AuthorizationListener() {
   			 @Override
          public void onAuthorizationFailure (AuthorizationException exception) {
          }

   			 @Override
          public void onAuthorizationCanceled () {
          }

   			 @Override 			 public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) { 			 }
   		 });
   ```
   {: pre}
</br>
</br>

## Exibindo as telas padrão com o SDK iOS Swift
{: #ios-swift}

É possível chamar as telas pré-configuradas com o SDK iOS Swift.
{: shortdesc}

</br>
**Conectar**

1. Coloque o comando a seguir em seu código.
  ```swift
  import BluemixAppID
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, refreshToken: RefreshToken?) {
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
  {: pre}


</br>
**Inscrever**

1. Configure **Permitir que os usuários se inscrevam e reconfigurem sua senha** para **Ligado**, nas configurações para o diretório da nuvem.
2. Chame o LoginWidget para iniciar o fluxo de inscrição.
  ```swift
  class delegate : AuthorizationDelegate {
    public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?) {
       if accessToken == nil && identityToken == nil {
        //email verification is required
        return
       }
     //User authenticated
      }

      public func onAuthorizationCanceled() {
        //Sign up canceled by the user
    }

    public func onAuthorizationFailure(error: AuthorizationError) {
        //Exception occurred
    }
  }

  AppID.sharedInstance.loginWidget?.launchSignUp(delegate: delegate())
  ```
  {: pre}

</br>
**Esqueci a senha**

1. Configure **Permitir que os usuários se inscrevam e reconfigurem sua senha** e **E-mail de Esqueci a senha** para **Ligado** nas configurações para o diretório da nuvem.
2. Chame o LoginWidget para iniciar o fluxo Esqueci a senha.
  ```swift
  class delegate : AuthorizationDelegate {
     public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?) {
        //forgot password finished, in this case accessToken and identityToken will be null.
     }

     public func onAuthorizationCanceled() {
         //forgot password canceled by the user
     }

     public func onAuthorizationFailure(error: AuthorizationError) {
         //Exception occurred
     }
  }

  AppID.sharedInstance.loginWidget?.launchForgotPassword(delegate: delegate())
  ```
  {: pre}

</br>
**Detalhes da conta**

1. Configure **Permitir que os usuários se inscrevam e reconfigurem sua senha** para **Ligado** nas configurações para o diretório da nuvem.
2. Chame o LoginWidget para iniciar o fluxo de detalhes de mudança.
  ```swift

   class delegate : AuthorizationDelegate {
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?) {
       }

       public func onAuthorizationCanceled() {
     }

       public func onAuthorizationFailure(error: AuthorizationError) {
     }
   }

   AppID.sharedInstance.loginWidget?.launchChangeDetails(delegate: delegate())
  ```
  {: pre}

</br>
**Mudar senha**

1. Configure **Permitir que os usuários se inscrevam e reconfigurem sua senha** para **Ligado** nas configurações para o diretório da nuvem.
2. Chame o LoginWidget para iniciar o fluxo de mudança de senha.
  ```swift
   class delegate : AuthorizationDelegate {
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?) {
       }

       public func onAuthorizationCanceled() {
     }

       public func onAuthorizationFailure(error: AuthorizationError) {
     }
    }

    AppID.sharedInstance.loginWidget?.launchChangePassword(delegate: delegate())
  ```
  {: pre}
</br>
</br>

## Exibindo as telas padrão com o SDK Node.js
{: #nodejs}

É possível chamar as telas pré-configuradas com o SDK Node.js.
{: shortdesc}

</br>
**Conectar**
1. Configure o diretório da nuvem para **Ligado** em suas configurações de provedor de identidade e especifique um terminal de retorno de chamada.
2. Inclua uma rota de post para seu app que possa ser chamada com os parâmetros de nome do usuário e senha e efetue login usando a senha do proprietário do recurso.
    ```javascript
    app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
    	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true // allow flash messages
  }));
    ```
    {: pre}
    `WebAppStrategy` permite que os usuários se conectem aos seus aplicativos da web com um nome de usuário e senha. Após um login bem-sucedido, o token de acesso de um usuário é armazenado na sessão HTTP e fica disponível durante a sessão. Quando a sessão HTTP for destruída ou expirar, o token será invalidado.
    {: tip}

</br>
**Inscrever**

1. Configure **Permitir que os usuários se inscrevam e reconfigurem sua senha** como **Ativado** nas configurações do Cloud Directory. Se configurado para "não", o processo termina sem recuperar os tokens de acesso e de identidade.
2. Passe a propriedade de WebAppStrategy `show` e configure-a para `WebAppStrategy.SIGN_UP`.
  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: pre}

</br>
**Esqueci a senha**

1. Configure **Permitir que os usuários se inscrevam e reconfigurem sua senha** e **E-mail de Esqueci a senha** para **LIGADO** nas configurações do diretório da nuvem. Se configurado para "não", o processo termina sem recuperar os tokens de acesso e de identidade.
2. Passe a propriedade de WebAppStrategy `show` e configure-a para `WebAppStrategy.FORGOT_PASSWORD`.
  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: pre}

</br>
**Detalhes da conta**
1. Configure **Permitir que os usuários se inscrevam e reconfigurem sua senha** para **Ligado** nas configurações do diretório da nuvem
2. Passe a propriedade de WebAppStrategy `show` e configure-a para `WebAppStrategy.CHANGE_DETAILS`.
  ```javascript
  app.get("/change_details", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_DETAILS
  }));
  ```
  {: pre}

</br>
**Mudar senha**
1. Configure **Permitir que os usuários se inscrevam e reconfigurem sua senha** como **Ativado** nas configurações do Cloud Directory.
2. Passe a propriedade de WebAppStrategy `show` e configurá-a para `WebAppStrategy.CHANGE_PASSWORD`.
  ```javascript
  app.get("/change_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_PASSWORD
  }));
  ```
  {: pre}

</br>
</br>

## Exibindo as telas padrão com o SDK do Swift
{: #swift}

Com os provedores de identidade social ativados, é possível chamar a tela de conexão pré-configurada com o SDK Swift.
{: shortdesc}

1. O código a seguir demonstra como usar WebAppKituraCredentialsPlugin em um app Kitura para proteger o terminal `/protected`.

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
</br>
</br>



