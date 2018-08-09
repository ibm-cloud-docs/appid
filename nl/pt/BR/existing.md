---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Incluindo o {{site.data.keyword.appid_short_notm}} em um app existente

É possível usar o {{site.data.keyword.appid_full}} com seu aplicativo existente para autenticar e armazenar as informações de perfil sobre seus usuários.


## Pré-requisitos
{: prereq}

* Um aplicativo iOS Swift, Android, Node.js, Swift ou Liberty for Java existente.
* Uma instância existente do {{site.data.keyword.appid_short_notm}}.


## Incluindo o {{site.data.keyword.appid_short_notm}} em um app Android existente
{: #existing-android}

É possível incluir o serviço {{site.data.keyword.appid_short_notm}} em seus aplicativos
Android existentes.

1. Inclua o repositório do JitPack em seu arquivo raiz `build.gradle`.

  ```gradle
  allprojects {
      		repositories {
         	 ...
         	 maven { url 'https://jitpack.io' }
	    }
  }
  ```
  {: codeblock}

2. Abra o arquivo `build.gradle` de seu aplicativo, localize a seção de dependências do arquivo e inclua uma dependência de compilação para o SDK do cliente do {{site.data.keyword.appid_short_notm}}.

  ```gradle
  dependencies {
      compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:1.+'
   }
  ```
  {: codeblock}

3. Localize a seção defaultConfig e inclua a linha de código a seguir.

  ```gradle
  defaultConfig {
                         ...
            manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
  ```
  {: codeblock}

4. Sincronizar seu projeto com o Gradle.
5. Inicialize o SDK do cliente passando os parâmetros de contexto, ID do locatário e região para o método de inicialização. Um local comum, mas não obrigatório, para colocar o código de inicialização está no método onCreate da atividade principal em seu aplicativo Android.

  ```Java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, <AppID.REGION>);
  ```
  {: codeblock}

    <table>
    <caption> Tabela 1. Componentes de comando explicados </caption>
      <tr>
        <th> Componentes </th>
        <th> Descrição </th>
      </tr>
      <tr>
        <td> <i> tenantID </i> </td>
        <td> É possível localizar esse valor clicando em **Visualizar credenciais** na guia de **credenciais de serviço** de seu painel de serviço. </td>
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
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          }
        });
  ```
  {: codeblock}

    <table>
    <caption> Tabela 2. Componentes de comando explicados </caption>
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
        <td> O processo de autenticação foi cancelado pelo usuário. </td>
      </tr>
      <tr>
        <td> <i> onAuthorizationSuccess </i> </td>
        <td> O usuário foi autenticado. </td>
      </tr>
    </table>

## Incluindo o {{site.data.keyword.appid_short_notm}} em um app iOS Swift existente
{: #existing-ios}

1. Abra o arquivo pod no diretório do projeto.
2. No destino do projeto, inclua uma dependência para o pod 'BluemixAppID'. Certifique-se
de que o `use_frameworks!` também
esteja sob o seu destino.
3. Para fazer download da dependência `BluemixAppID`, execute o comando a seguir.

  ```
  pod install --repo-update
  ```
  {: codeblock}

4. Abra o seu projeto Xcode e ative o compartilhamento de keychain. Sob **Configurações de projeto**, clique
em **Recursos** >
**Compartilhamento de Keychain**.
5. Em **Configurações do projeto** > **Informações** > **Tipos de URL**, inclua um **Tipo de URL**. Preencha ambas as caixas de texto **Identificador** e **Esquema URL** com o valor a seguir.

  ```
  $(PRODUCT_BUNDLE_IDENTIFIER)
  ```
  {: codeblock}

6. Inclua a importação a seguir em seu arquivo `AppDelegate.swift`.

  ```swift
  import BluemixAppID
  import BMSCore
  ```
  {: codeblock}

7. Inicialize o SDK do cliente passando os parâmetros de ID do locatário e região para o método de inicialização. Um local comum, mas não obrigatório, para colocar o código de inicialização está no método application:didFinishLaunchingWithOptions: do AppDelegate em seu aplicativo.

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, bluemixRegion: <AppID.Region>)
  ```
  {: codeblock}

    <table>
    <caption> Tabela 3. Componentes de comando explicados </caption>
      <tr>
        <th> Componentes </th>
        <th> Descrição </th>
      </tr>
      <tr>
        <td> <i> tenantID </i> </td>
        <td> É possível localizar esse valor clicando em **Visualizar credenciais** na guia de **credenciais de serviço** de seu painel de serviço. </td>
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
     public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, refreshToken: RefreshToken? response:Response?) {
     }

     public func onAuthorizationCanceled() {
     }

     public func onAuthorizationFailure(error: AuthorizationError) {
     }
  }

  AppID.sharedInstance.loginWidget?.launch(delegate: delegate())
  ```
  {: codeblock}

    <table>
    <caption> Tabela 4. Componentes de comando explicados </caption>
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
        <td> O processo de autenticação foi cancelado pelo usuário. </td>
      </tr>
      <tr>
        <td> <i> onAuthorizationFailure </i> </td>
        <td> Ocorreu uma exceção. </td>
      </tr>
    </table>

## Incluindo o {{site.data.keyword.appid_short_notm}} em um app da web Node.js existente
{: #existing-node}

1. Inclua o módulo `bluemix-appid` em seu aplicativo Node.js.

  ```javaScript
  npm install --save bluemix-appid
  ```
  {: codeblock}

2. Instale os módulos a seguir se eles ainda não estiverem instalados.

  ```javaScript
  npm install --save express
  npm install --save passport
  npm install --save express-session
  ```
  {: codeblock}

3. Inclua o código a seguir em seu arquivo `app.js` para:
    * Configurar seu app express para usar o middleware express-session. **Nota**: deve-se configurar o middleware com o armazenamento de sessão adequado para ambientes de produção. Para obter mais informações, consulte o <a href="https://github.com/expressjs/session" target="_blank">expressjs docs <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.
    * Configurar passportjs com serialização e desserialização. Isso é necessário para persistência de sessão autenticada em solicitações de HTTP. Para obter mais informações, veja os <a href="http://passportjs.org/docs" target="_blank">docs do passportjs <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.  
    * Recupere tokens de acesso e de identidade do serviço {{site.data.keyword.appid_short_notm}}
executando um comando get na URL de retorno de chamada.

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
  app.get("/protected", passport.authenticate(WebAppStrategy.STRATEGY_NAME)), function(req, res)
    		res.json(req.user);
    });
  ```
  {: codeblock}

    **Nota**: o serviço redireciona na ordem a seguir:
    1. A URL original da solicitação que acionou o processo de autenticação, conforme persistido na sessão HTTP sob a chave `WebAppStrategy.ORIGINAL_URL`.
    2. Um redirecionamento bem-sucedido, conforme especificado em `passport.authenticate(name, {successRedirect: "...."}).`
    3. Raiz do aplicativo ("/")

4. Reimplemente seu aplicativo.


## Incluindo o {{site.data.keyword.appid_short_notm}} em um aplicativo da web Swift existente
{: #existing-swift}

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
    {: codeblock}

2. Inclua o código a seguir no aplicativo Swift para:
    * Configurar o Kitura para usar o middleware de sessão. **Nota**: deve-se configurar o Kitura com o armazenamento de sessão adequado para ambientes de produção. Para obter mais
informações, veja os <a href="https://github.com/IBM-Swift/Kitura-Session" target="_blank">docs do Kitura <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.
    * Recupere tokens de acesso e de identidade do serviço {{site.data.keyword.appid_short_notm}}
executando um comando get na URL de retorno de chamada.

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
  {: codeblock}

  <table>
  <caption> Tabela 5. Componentes de comando explicados </caption>
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



## Incluindo o {{site.data.keyword.appid_short_notm}} em um app Liberty for Java existente
{: #existing-liberty}

É possível configurar o {{site.data.keyword.appid_short_notm}} para trabalhar com seus
aplicativos da web Liberty for Java existentes.

1. Inclua um <a href="https://www.ibm.com/support/knowledgecenter/en/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/twlp_config_oidc_rp.html" target="_blank">recurso OpenID Connect <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> em seu
`server.xml`.

  ```xml
  <feature manager>
  <feature>appSecurity-2.0</feature>
  <feature>openidConnectClient-1.0</feature>  
  ```
  {: codeblock}

2. Em seu recurso Open ID Connect Client, defina os itens temporários a seguir. Posteriormente,
eles serão preenchidos automaticamente pelo {{site.data.keyword.Bluemix_notm}}. A variável de
nome da instância deve corresponder exatamente ao nome da instância do seu {{site.data.keyword.appid_short_notm}}.

  ```
  clientId='${cloud.services.AppID-Instance-Name.credentials.clientId}'
  clientSecret='${cloud.services.AppID-Instance-Name.credentials.clientSecret}'
  authorizationEndpointUrl='${cloud.services.AppID-Instance-Name.credentials.authorizationEndpointUrl}'
  tokenEndpointUrl='${cloud.services.AppID-Instance-Name.credentials.tokenEndpointUrl}'
  jwkEndpointUrl='${cloud.services.AppID-Instance-Name.credentials.jwkEndpointUrl}'
  issuerIdentifier='appid-oauth.ng.bluemix.net'
  tokenEndpointAuthMethod="basic"
  signatureAlgorithm="RS256"
  authFilterid="myAuthFilter"
  ```
  {: codeblock}

  **Nota**: a variável issuerIdentifier muda de acordo com sua região. Ela
pode ser uma das variáveis a seguir:
  * issuerIdentifier="appid-oauth.ng.bluemix.net"
  * issuerIdentifier="appid-oauth.eu-gb.bluemix.net"
  * issuerIdentifier="appid-oauth.au-syd.bluemix.net"</ul> </td>

3. Defina um filtro de autorização para especificar os recursos protegidos. Se um filtro não for <a href="https://www.ibm.com/support/knowledgecenter/en/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/rwlp_auth_filter.html" target="_blank">definido
<img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>, o serviço protegerá todos os recursos.
  ```
  <authFilter id="myAuthFilter">
             <requestUrl id="myRequestUrl" urlPattern="/protected" matchType="contains"/>
    </authFilter>
  ```
  {: codeblock}

3. Em seu arquivo `server.xml`, defina seu tipo de assunto especial como ALL_AUTHENTICATED_USERS.

  ```xml
  <application type="war" id="ProtectedServlet" context-root="/appidSample"
  location="${server.config.dir}/apps/libertySample-1.0.0.war">
    <application-bnd>
        <security-role name="myrole">
        <special-subject type="ALL_AUTHENTICATED_USERS"/>
        </security-role>
            </application-bnd>
        </application>
  ```
  {: codeblock}

4. Em seu elemento `<application-bnd>`, <a href="https://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_authorization.html?cp=SSAW57_8.5.5&cm_mc_uid=18498555367014888859884&cm_mc_sid_50200000=1494855872" target="_blank">defina as funções <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> conforme localizadas
em seu app da web: `web.xml`.

  ```xml
  <security-role>
  <role-name>myrole</role-name>
  </security-role>

  <security-constraint>
  <web-resource-collection>
  <web-resource-name>ProtectedServlet</web-resource-name>
  <url-pattern>/ProtectedServlet/*</url-pattern>
  <http-method>GET</http-method>
  <http-method>PUT</http-method>
  <http-method>POST</http-method>
  <http-method>DELETE</http-method>
  </web-resource-collection>

  <auth-constraint>
  <role-name>myrole</role-name>
  </auth-constraint>
  <user-data-constraint>
  <transport-guarantee>NONE</transport-guarantee>
  </user-data-constraint>
  </security-constraint>
  ```
  {: codeblock}

5. Obtenha um certificado.

    a. Em seu painel do {{site.data.keyword.appid_short_notm}}, clique em Credenciais de serviço.

    b. Clique em **Visualizar credenciais** e copie a `oauthServerUrl`.

    c. Inclua `/token` na URL. Use o Firefox para navegar na URL de saída
e obter o certificado. É possível usar a URL a seguir como um exemplo.

    ```
    https://appid-oauth.eu-gb.bluemix.net/oauth/v3/5d12852e-b0a0-46a3-9547-67a4a33a7164/token
    ```
    {: screen}

    d. Na barra de endereço do Firefox, clique no ícone de bloqueio > **seta para a direita** > **mais informações** > **visualizar certificado**.

    e. Na guia **Segurança**, clique em **Visualizar certificado** > **Detalhes**.

    f. Exporte o certificado e salve-o em sua unidade local como um arquivo PEM.

6. Inclua o certificado em seu arquivo truststore.jks do Liberty for Java usando o <a href="https://www.ibm.com/support/knowledgecenter/SSYKE2_6.0.0/com.ibm.java.security.component.60.doc/security-component/keytoolDocs/keytool_overview.html" target="_blank">Liberty Keytool <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> e inclua uma referência no alias de certificado no elemento OIDC. Seu `.jks file` está
localizado em seu diretório do servidor: **resources** > **security** > **<i>truststore file name</i>** >
**`.jks file`**. É possível usar uma das opções a seguir
para incluir seu certificado no arquivo.

    * No terminal, acesse sua pasta de segurança do Liberty for Java: wlp > usr > servers > <i>servername</i> > resources > security
e use o comando a seguir para incluir o certificado.

      ```
      keytool -importcert -keystore ./trust.jks -file ~/Documents/secbluemix.cer`
      ```
      {: codeblock}      

      **Nota**: `~/Documents/[certificatename].cer` demonstra
o local do arquivo em sua unidade local.

    * É possível usar o <a href="http://keystore-explorer.org/index.html" target="_blank">KeyStore Explorer <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> para incluir o certificado. Abra o KeyStore Explorer e selecione **Abrir um KeyStore existente**.

7. Em seu arquivo `manifest.yml`, defina sua instância do {{site.data.keyword.appid_short_notm}}.

  ```yml
  services:
  - <appid service name>

  Manifest.yml file example:
  applications:
  - name: LibertyExampl
  buildpack: liberty-for-java
  instances: 1
  random-route: true
  memory: 512M
  disk_quota: 1024M
  timeout: 180
  services:
  - AppID-Instance-Name
  ```
  {: codeblock}

    Um arquivo `server.xml` de exemplo que está configurado para o {{site.data.keyword.appid_short_notm}}:

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <server description="sample server">

      <featureManager>
        <feature>ssl-1.0</feature>
        <feature>servlet-3.1</feature>
        <feature>appSecurity-2.0</feature>
        <feature>openidConnectClient-1.0</feature>  
      </featureManager>

      <openidConnectClient id="MyDefaultRP"
         clientId='${cloud.services.AppID-Instance-Name.credentials.clientId}'
         clientSecret='${cloud.services.AppID-Instance-Name.credentials.clientSecret}'
         authorizationEndpointUrl='${cloud.services.AppID-Instance-Name.credentials.authorizationEndpointUrl}'
         tokenEndpointUrl='${cloud.services.AppID-Instance-Name.credentials.tokenEndpointUrl}'
         jwkEndpointUrl='${cloud.services.AppID-Instance-Name.credentials.jwkEndpointUrl}'
         issuerIdentifier='${cloud.services.AppID-Instance-Name.credentials.appid-oauth.ng.bluemix.net}'
         tokenEndpointAuthMethod="basic"
         signatureAlgorithm="RS256"
         authFilterid="myAuthFilter"
         trustAliasName="my.bluemix.certificate "
      />
      <authFilter id="myAuthFilter">
               <requestUrl id="myRequestUrl" urlPattern="/protected" matchType="contains"/>
      </authFilter>

      <application type="war" id="ProtectedServlet" context-root="/appidSample" location="${server.config.dir}/apps/libertySample-1.0.0.war">
          <application-bnd>
              <security-role name="myrole">
                  <special-subject type="ALL_AUTHENTICATED_USERS" />
              </security-role>
          </application-bnd>
      </application>

   <applicationManager autoExpand="true"/>

  <keyStore id="defaultKeyStore" password="Password"/>
  <keyStore id="defaulttrustore" password="Liberty" location="<FileContainingCertificated>.jks"/>

  <ssl id="defaultSSLSettings" keyStoreRef="defaultKeyStore" trustStoreRef="defaulttrustore"/>
  <sslDefault sslRef="defaultSSLSettings"/>

      <httpEndpoint id="defaultHttpEndpoint" httpPort="9080" host="*" httpsPort="9443" />


      <applicationManager autoExpand="true"/>

  </server>
  ```
  {: codeblock}



## Incluindo o {{site.data.keyword.appid_short_notm}} em um aplicativo existente que não seja executado no {{site.data.keyword.Bluemix_notm}}
{: #existing}

Se você tiver um aplicativo Node.js ou Swift que não é executado no {{site.data.keyword.Bluemix_notm}}, será possível configurar o WebAppStrategy ou o WebAppKituraCredentialsPlugin para trabalhar remotamente. Para um app Liberty
for Java que não é executado no Bluemix, configure as variáveis do elemento OIDC.


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
  {: codeblock}

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
  {: codeblock}

  <table>
  <caption> Tabela 6. Componentes de comando para apps Swift e Node.js explicados </caption>
    <tr>
      <th> Componentes </th>
      <th> Descrição </th>
    </tr>
    <tr>
      <td> <i> tenantID </i> </br> <i> clientID </i> </br> <i> secret </i> </br> <i> oauth-server-url </i> </br> </td>
      <td> É possível localizar esses valores clicando em **Visualizar credenciais** na guia de **credenciais de serviço** de seu painel de serviço. </td>
    </tr>
    <tr>
      <td> <i> app-url </i> </td>
      <td> A URL do aplicativo. </td>
    </tr>
    <tr>
      <td> <i> CALLBACK_URL </i> </td>
      <td> A URL que os usuários da página verão depois de efetuarem login. </td>
    </tr>
  </table>

Em seus apps Liberty for Java, conclua as etapas em [Incluindo o {{site.data.keyword.appid_short_notm}} em um app Liberty for Java existente](/docs/services/appid/existing.html#existing-liberty),
mas substitua as variáveis do elemento do cliente OIDC pelo código a seguir.

  ```
  clientId='App ID client_ID'
  clientSecret='App Id Secret'      
  authorizationEndpointUrl='oauthServerUrl/authorization'       
  tokenEndpointUrl='oauthServerUrl/token'
  jwkEndpointUrl='oauthServerUrl/publickeys'
  issuerIdentifier='Changed according to the region'
  tokenEndpointAuthMethod="basic"
  signatureAlgorithm="RS256"
  authFilterid="myAuthFilter"
  trustAliasName="my.bluemix.certificate"
  ```
  {: codeblock}

  <table>
  <caption> Tabela 7. Variáveis do elemento OIDC para apps Liberty for Java que não são executados no Bluemix </caption>
    <tr>
      <th> Componente </th>
      <th> Descrição </th>
    </tr>
    <tr>
    <td> <i> clientID </i> </br> <i> secret </i> </br> <i> oauth-server-url </i> </br> </td>
    <td> É possível localizar esses valores clicando em **Visualizar credenciais** na guia de **credenciais de serviço** de seu painel de serviço. </td>
    </tr>
    <tr>
      <td> <i> authorizationEndpointURL </i> </td>
      <td> Inclua `/authorization` no final da oauthServerURL. </td>
    </tr>
    <tr>
      <td> <i> tokenEndpointUrl </i> </td>
      <td> Inclua `/token` no final da oauthServerURL. </td>
    </tr>
    <tr>
      <td> <i> jwkEndpointUrl </i> </td>
      <td> Inclua `/publickeys` no final da oauthServerURL. </td>
    </tr>
    <tr>
      <td> <i> issuerIdentifier </i> </td>
      <td> Muda com base em sua região. Ele pode ser um dos seguintes: </br><ul><li> issuerIdentifier="appid-oauth.ng.bluemix.net" </br><li> issuerIdentifier="appid-oauth.eu-gb.bluemix.net" </br><li> issuerIdentifier="appid-oauth.au-syd.bluemix.net" </ul></td>
    </tr>
    <tr>
      <td> <i> tokenEndpointAuthMethod </i> </td>
      <td> Especificado como "basic". </td>
    </tr>
    <tr>
      <td> <i> signatureAlgorithm </i> </td>
      <td> Especificado como "RS256". </td>
    </tr>
    <tr>
      <td> <i> authFilterid </i> </td>
      <td> A lista dos recursos a serem protegidos. </td>
    </tr>
    <tr>
      <td> <i> trustAliasName </i> </td>
      <td> O nome de seu certificado em seu armazenamento confiável. </td>
    </tr>
  </table>
