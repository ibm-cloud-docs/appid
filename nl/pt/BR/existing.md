---

copyright:
  years: 2017
lastupdated: "2017-06-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# Incluindo o {{site.data.keyword.appid_short_notm}} em um app existente

É possível usar o {{site.data.keyword.appid_full}} com seu aplicativo existente para autenticar e armazenar as informações de perfil sobre seus usuários.


## Pré-requisitos

* Um aplicativo existente iOS Swift, Android, Node.js ou Swift.
* Uma instância existente do {{site.data.keyword.appid_short_notm}}.


## Incluindo o {{site.data.keyword.appid_short_notm}} em um app Android existente

É possível incluir o serviço App ID nos aplicativos Android existentes.

1. Inclua o repositório do JitPack no arquivo raiz build.gradle.

  ```gradle
  allprojects {
      		repositories {
         	 ...
         	 maven { url 'https://jitpack.io' }
	    }
  }
  ```
  {: pre}

2. Abra o arquivo build.gradle de seu aplicativo, localize a seção de dependências do arquivo e inclua uma dependência de compilação para o SDK do cliente do {{site.data.keyword.appid_short_notm}}.

  ```gradle
  dependencies {
      compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:1.+'
   }
  ```
  {: pre}

3. Localize a seção defaultConfig e inclua a linha de código a seguir.

  ```gradle
  defaultConfig {
                         ...
            manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
  ```
  {: pre}

4. Sincronizar seu projeto com o Gradle.
5. Inicialize o SDK do cliente passando os parâmetros de contexto, ID do locatário e região para o método de inicialização. Um local comum, mas não obrigatório, para colocar o código de inicialização está no método onCreate da atividade principal em seu aplicativo Android.

  ```Java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, <AppID.REGION>);
  ```
  {: pre}

  <table>
  <caption> Tabela 1. Componentes de comando explicados</caption>
    <tr>
      <th> Componentes </th>
      <th> Descrição </th>
    </tr>
    <tr>
      <td> <i> tenantID </i> </td>
      <td> É possível localizar esse valor clicando em **Visualizar credenciais** na guia de **credenciais de serviço** de seu painel de serviço.</td>
    </tr>
    <tr>
      <td> <i> AppID.REGION </i> </td>
      <td> É possível localizar a sua região na UI. As opções são `AppID.REGION_US_SOUTH`, `AppID.REGION_UK` ou `AppID.REGION_Sydney`. </td>
    </tr>
  </table>

6. Após o SDK do cliente do {{site.data.keyword.appid_short_notm}} ser inicializado, será possível autenticar os seus usuários executando o widget de login.

  ```Java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launch(this, new AuthorizationListener() {
          @Override
          public void onAuthorizationFailure (AuthorizationException exception) {
          }

          @Override
          public void onAuthorizationCanceled () {
          }

          @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
          }
        });
  ```
  {: pre}

  <table>
  <caption> Tabela 2. Componentes de comando explicados</caption>
    <tr>
      <th> Componentes </th>
      <th> Descrição </th>
    </tr>
    <tr>
      <td> <i> onAuthorizationFailure </i> </td>
      <td> Ocorreu uma exceção. </td>
    </tr>
    <tr>
      <td> <i> onAuthorizationCanceled </i> </td>
      <td> O processo de autenticação foi cancelado pelo usuário.</td>
    </tr>
    <tr>
      <td> <i> onAuthorizationSuccess </i> </td>
      <td> O usuário foi autenticado. </td>
    </tr>
  </table>

## Incluindo o {{site.data.keyword.appid_short_notm}} em um app iOS Swift existente

1. Abra o arquivo pod no diretório do projeto.
2. No destino do projeto, inclua uma dependência para o pod 'BluemixAppID'. Certifique-se de que o comando `use_frameworks!` também esteja sob o seu destino.
3. Para fazer download da dependência `BluemixAppID`, execute o comando a seguir.

  ```
  pod install --repo-update
  ```
  {: pre}

4. Abra o seu projeto Xcode e ative o compartilhamento de keychain. Sob **Configurações de projeto**, clique
em **Recursos** >
**Compartilhamento de Keychain**.
5. Em **Configurações do projeto** > **Informações** > **Tipos de URL**, inclua um **Tipo de URL**. Preencha ambas as caixas de texto **Identificador** e **Esquema URL** com o valor a seguir.

  ```
  $(PRODUCT_BUNDLE_IDENTIFIER)
  ```
  {: pre}

6. Inclua a importação a seguir no arquivo AppDelegate.swift.

  ```swift
  import BluemixAppID
  import BMSCore
  ```
  {: pre}

7. Inicialize o SDK do cliente passando os parâmetros de ID do locatário e região para o método de inicialização. Um local comum, mas não obrigatório, para colocar o código de inicialização está no método application:didFinishLaunchingWithOptions: do AppDelegate em seu aplicativo.

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, bluemixRegion: <AppID.Region>)
  ```
  {: pre}

  <table>
  <caption> Tabela 3. Componentes de comando explicados</caption>
    <tr>
      <th> Componentes </th>
      <th> Descrição </th>
    </tr>
    <tr>
      <td> <i> tenantID </i> </td>
      <td> É possível localizar esse valor clicando em **Visualizar credenciais** na guia de **credenciais de serviço** de seu painel de serviço.</td>
    </tr>
    <tr>
      <td> <i> AppID.REGION </i> </td>
      <td> É possível localizar a sua região na UI. As opções são `AppID.REGION_US_SOUTH`, `AppID.REGION_UK` ou `AppID.REGION_Sydney`. </td>
    </tr>
  </table>

8. Inclua o código a seguir em seu arquivo AppDelegate.

  ```swift
  func application(_ application: UIApplication, open url: URL, options :[UIApplicationOpenURLOptionsKey : Any]) -> Bool {
         	return AppID.sharedInstance.application(application, open: url, options: options)
      }
  class delegate : AuthorizationDelegate {
     public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, response:Response?) {
     }

     public func onAuthorizationCanceled() {
     }

     public func onAuthorizationFailure(error: AuthorizationError) {
     }
  }

  AppID.sharedInstance.loginWidget?.launch(delegate: delegate())
  ```
  {: pre}
  <table>
  <caption> Tabela 4. Componentes de comando explicados</caption>
    <tr>
      <th> Componentes </th>
      <th> Descrição </th>
    </tr>
    <tr>
      <td> <i> onAuthorizationSuccess </i> </td>
      <td> O usuário foi autenticado. </td>
    </tr>
    <tr>
      <td> <i> onAuthorizationCanceled </i> </td>
      <td> O processo de autenticação foi cancelado pelo usuário.</td>
    </tr>
    <tr>
      <td> <i> onAuthorizationFailure </i> </td>
      <td> Ocorreu uma exceção. </td>
    </tr>
  </table>

## Incluindo o {{site.data.keyword.appid_short_notm}} em um app da web Node.js existente

1. Inclua o módulo `bluemix-appid` em seu aplicativo Node.js.

  ```javaScript
  npm install --save bluemix-appid
  ```
  {: pre}

2. Instale os módulos a seguir se eles ainda não estiverem instalados.

  ```javaScript
  npm install --save express
  npm install --save passport
  npm install --save express-session
  ```
  {: pre}

3. Inclua o código a seguir no arquivo app.js para:
    * Configurar seu app express para usar o middleware express-session. **Nota**: deve-se configurar o middleware com o armazenamento de sessão adequado para ambientes de produção. Para obter mais informações, veja os [docs de expressjs](https://github.com/expressjs/session).
    * Configurar passportjs com serialização e desserialização. Isso é necessário para persistência de sessão autenticada em solicitações de HTTP. Para obter mais informações, veja os [docs de passportjs](http://passportjs.org/docs).
    * Recuperar tokens de acesso e de identidade do serviço App ID executando um comando get na URL de retorno de chamada.

  ```javaScript
  const express = require("express");
  const session = require("express-session");
  const passport = require("passport");
  const WebAppStrategy = require("bluemix-appid").WebAppStrategy;
  const app = express();
  const CALLBACK_URL = "/ibm/bluemix/appid/callback";
  app.use(session({
      secret: "123456",
      resave: true,
      saveUninitialized: true
    }));
  app.use(passport.initialize());
    app.use(passport.session());

    passport.use(new WebAppStrategy());
  passport.serializeUser(function(user, cb) {
      cb(null, user);
    });

    passport.deserializeUser(function(obj, cb) {
      cb(null, obj);
    });
  app.get(CALLBACK_URL, passport.authenticate(WebAppStrategy.STRATEGY_NAME));
  app.get("/protected", passport.authenticate(WebAppStrategy.STRATEGY_NAME), function(req, res)
    		res.json(req.user);
    });
  ```
  {: pre}

    **Nota**: o serviço redireciona na ordem a seguir:
    1. A URL original da solicitação que acionou o processo de autenticação, conforme persistido na sessão HTTP sob a chave `WebAppStrategy.ORIGINAL_URL`.
    2. Um redirecionamento bem-sucedido, conforme especificado em `passport.authenticate(name, {successRedirect: "...."}).`
    3. Raiz do aplicativo ("/")

4. Reimplemente seu aplicativo.


## Incluindo o {{site.data.keyword.appid_short_notm}} em um aplicativo da web Swift existente

1. Abra o arquivo `Package.swift` no diretório de seu app Swift e inclua a dependência `appid-serversdk-swift`.
  Por exemplo:

    ```swift
    import PackageDescription

    let package = Package(
      dependencies: [
           	.Package(url: "https://github.com/ibm-cloud-security/appid-serversdk-swift.git", majorVersion: 1)
      ]
    )
    ```
    {: pre}

2. Inclua o código a seguir no aplicativo Swift para:
    * Configurar o Kitura para usar o middleware de sessão. **Nota**: deve-se configurar o Kitura com o armazenamento de sessão adequado para ambientes de produção. Para obter mais informações, veja os [docs de Kitura](https://github.com/IBM-Swift/Kitura-Session).
    * Recuperar tokens de acesso e de identidade do serviço App ID executando um comando get na URL de retorno de chamada.

  ```swift
  import Foundation
  import Kitura
  import KituraSession
  import Credentials
  import SwiftyJSON
  import BluemixAppID
  let router = Router()
  let session = Session(secret: "Some secret")
  router.all(middleware: session)
  let webappKituraCredentialsPlugin = WebAppKituraCredentialsPlugin()
  let kituraCredentials = Credentials()
  kituraCredentials.register(plugin: webappKituraCredentialsPlugin)
  router.get(CALLBACK_URL,
    handler: kituraCredentials.authenticate(credentialsType: webappKituraCredentialsPlugin.name,
      successRedirect: LANDING_PAGE_URL,
      failureRedirect: LANDING_PAGE_URL
      ))
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
  ```
  {: pre}

  <table>
  <caption> Tabela 6. Componentes de comando explicados</caption>
    <tr>
      <th> Componentes </th>
      <th> Descrição </th>
    </tr>
    <tr>
      <td> <i> var CALLBACK_URL </i> </td>
      <td> /ibm/bluemix/appid/callback </td>
    </tr>
    <tr>
      <td> <i> var LANDING_PAGE_URL </i> </td>
      <td> /index.html </td>
    </tr>
    </table>

5. Reimplemente seu aplicativo.



## Incluindo o {{site.data.keyword.appid_short_notm}} em um aplicativo existente que não seja executado no {{site.data.keyword.Bluemix_notm}}


Se você tiver um aplicativo Node.js ou Swift que não seja executado no Bluemix, será possível configurar o WebAppStrategy ou o WebAppKituraCredentialsPlugin para trabalhar remotamente.


No app Node.js, substitua `passport.use(new WebAppStrategy());` pelo código a seguir.

  ```javaScript
  passport.use(new WebAppStrategy({
    	  tenantId: "{tenant-id}",
   	    clientId: "{client-id}",
      	secret: "{secret}",
      	oauthServerUrl: "{oauth-server-url}",
      	redirectUri: "{app-url}" + CALLBACK_URL
      }));
  ```
{: pre}

No app Swift, substitua `let webappKituraCredentialsPlugin = WebAppKituraCredentialsPlugin()` pelo código a seguir.

  ```swift
  let options = [
        "clientId": "{client-id}",
  	"secret": "{secret}",
  	"tenantId": "{tenant-id}",
  	"oauthServerUrl": "{oauth-server-url}",
  	"redirectUri": "{app-url}" + CALLBACK_URL
  ]
    let webappKituraCredentialsPlugin = WebAppKituraCredentialsPlugin(options: options)
  ```
  {: pre}

<table>
<caption> Tabela 7. Componentes de comando para apps Swift e Node.js explicados </caption>
  <tr>
    <th> Componentes </th>
    <th> Descrição </th>
  </tr>
  <tr>
    <td> <i> tenantID </i> </br> <i> clientID </i> </br> <i> secret </i> </br> <i> oauth-server-url </i> </br> </td>
    <td> É possível localizar esses valores clicando em **Visualizar credenciais** na guia de **credenciais de serviço** de seu painel de serviço.</td>
  </tr>
  <tr>
    <td> <i> app-url </i> </td>
    <td> A URL do aplicativo. </td>
  </tr>
  <tr>
    <td> <i> CALLBACK_URL </i> </td>
    <td> A URL que os usuários da página verão depois de efetuarem login.</td>
  </tr>
</table>
