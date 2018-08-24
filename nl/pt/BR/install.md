---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}

# Incluindo o  {{site.data.keyword.appid_short}}  em seu app
{: #configuring}

Inicie com o {{site.data.keyword.appid_short}} configurando o serviço no aplicativo.
{: shortdesc}


## Configurando o SDK do Android
{: #android-setup}

Construa os seus apps Android com o SDK do cliente do {{site.data.keyword.appid_short}}, inicialize o SDK, autentique usuários e faça solicitações
para recursos protegidos e desprotegidos.
{:shortdesc}


### Antes de iniciar
{: #before-android}

As seguintes informações são necessárias:
  * Uma instância de um serviço do {{site.data.keyword.appid_short_notm}}.
  * O seu ID do locatário. O seu ID do locatário é um identificador exclusivo que é usado para inicializar o seu app e pode ser localizado na guia **Credenciais de serviço** de seu painel de serviço.
  * A sua região do {{site.data.keyword.Bluemix}}. É possível localizar a sua região procurando na UI. O valor é usado para inicializar o seu app.
    <table><caption> Tabela 1. Regiões e valores do SDK correspondentes do {{site.data.keyword.Bluemix_notm}}</caption>
    <tr>
      <th>{{site.data.keyword.Bluemix}} Região</th>
      <th>Valor do SDK</th>
    </tr>
    <tr>
      <td>Sul dos Estados Unidos</td>
      <td><code>AppID.REGION_US_SOUTH</code> </td>
    </tr>
    <tr>
      <td>Sydney</td>
      <td><code>AppID.REGION_SYDNEY </code></td>
    </tr>
    <tr>
      <td>United Kingdom</td>
      <td><code>AppID.REGION_UK </code></td>
    </tr>
    <tr>
      <td>Alemanha</td>
      <td><code>AppID.REGION_GERMANY</code></td>
    </tr>
  </table>

  * Um <a href="https://developers.google.com/web/tools/setup/" target="_blank">Projeto do Android
Studio<img src="../../icons/launch-glyph.svg" alt="ícone de Link externo"></a>, configurado para trabalhar com o Gradle.

### Instalando o SDK
{: #install-android}

1. Crie um projeto Android Studio ou abra um projeto existente.
2. Inclua o repositório do JitPack em seu arquivo raiz `build.gradle`.

  ```gradle
    allprojects {
	    repositories {
		    ...
		    maven { url 'https://jitpack.io' }
	    }
    }
  ```
  {: codeblock}

3. Localize a seção de dependências do arquivo `build.gradle` para o aplicativo e inclua uma
dependência de compilação para o SDK do cliente do {{site.data.keyword.appid_short_notm}}. **Nota**: certifique-se de abrir o arquivo para o seu app, não o arquivo `build.gradle` do projeto.

  ```gradle
   dependencies {
       compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:4.+'
   }
  ```
  {: codeblock}

5. Localize a seção `defaultConfig` e inclua as seguintes linhas de código.

  ```gradle
  defaultConfig {
  ...
  manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
  ```
  {: codeblock}

6. Sincronize seu projeto com o Gradle. Clique em **Ferramentas > Android > Sincronizar projeto com arquivos Gradle**.

### Inicializando o SDK
{: #initialize-android}

Inicialize o SDK do cliente passando os parâmetros de contexto, ID do locatário e região para o método de inicialização. Um local comum, mas não obrigatório, para colocar o código de inicialização está no método onCreate da atividade principal em seu aplicativo Android.

  ```java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, AppID.REGION_UK);
  ```
  {: codeblock}

  <table>
  <caption> Tabela. Componentes de comando explicados </caption>
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
      <td> É possível localizar a sua região na UI. As opções são `AppID.REGION_US_SOUTH`, `AppID.REGION_UK`, `AppID.REGION_Sydney` ou `AppID.REGION_Germany`. </td>
    </tr>
  </table>

Agora você está pronto para configurar os seus provedores de identidade e começar a autenticar usuários. Para obter mais informações, consulte o <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">{{site.data.keyword.appid_short_notm}} repositório GitHub Android <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.


</br>

## Configurando o iOS Swift SDK
{: #ios-setup}

Construa os seus apps Swift com o SDK do cliente do {{site.data.keyword.appid_short}}, inicialize o SDK, autentique usuários e faça solicitações
para recursos protegidos e desprotegidos.
{:shortdesc}


### Antes de iniciar
{: #before-ios}

As seguintes informações são necessárias:
  * Uma instância de {{site.data.keyword.appid_short_notm}}.
  * O seu ID do locatário. O seu ID do locatário é um identificador exclusivo que é usado para inicializar o seu app e pode ser localizado na guia **Credenciais de serviço** de seu painel de serviço.
  * A sua região do {{site.data.keyword.Bluemix_notm}}.
  É possível localizar a sua região procurando na UI. O valor é usado para inicializar o seu app.
  <table> <caption> Tabela. {{site.data.keyword.Bluemix_notm}}  regiões e valores de SDK correspondentes </caption>
    <tr>
      <th>{{site.data.keyword.Bluemix}} Região</th>
      <th>Valor do SDK</th>
    </tr>
    <tr>
      <td>Sul dos Estados Unidos</td>
      <td><code>AppID.REGION_US_SOUTH</code></td>
    </tr>
    <tr>
      <td>Sydney</td>
      <td><code>AppID.REGION_SYDNEY </code></td>
    </tr>
    <tr>
      <td>United Kingdom</td>
      <td><code>AppID.REGION_UK </code></td>
    </tr>
    <tr>
      <td>Alemanha</td>
      <td><code>AppID.REGION_GERMANY</code></td>
    </tr>
  </table>

  * Um projeto Xcode (versão 9.0.1 ou superior).
  * CocoaPods (versão 1.1.0 ou superior).


### Instalando o SDK
{: #install-ios}

O SDK do cliente do {{site.data.keyword.appid_short_notm}} é distribuído com o CocoaPods, um gerenciador de dependência para projetos Swift e
Objective-C Cocoa. O CocoaPods faz download de artefatos e os torna disponíveis para o seu projeto.

1. Crie um projeto Xcode ou abra um projeto existente.
2. Abra ou crie o arquivo pod no diretório do projeto.
3. Seguindo o destino do seu projeto, inclua uma dependência para o pod 'IBMCloudAppID' e o `use_frameworks!` .

  ```swift
  target '<yourTarget>' do
     use_frameworks!
     pod 'IBMCloudAppID ' end
  ```
  {: codeblock}

4. Faça download da dependência 'IBMCloudAppID'.

  ```swift
  pod install --repo-update
  ```
  {: codeblock}

6. Ative o compartilhamento de keychain no projeto Xcode. Navegue para **Configurações do projeto > Recursos > Compartilhamento de keychain** e selecione **Ativar compartilhamento de keychain**.
7. Abra **Configurações do projeto > Informações > Tipos de URL** e inclua um **Tipo de URL**. Coloque o valor a seguir nas duas caixas de texto: **Identificador** e **Esquema URL**.
  ```
  $(PRODUCT_BUNDLE_IDENTIFIER)
  ```
  {: codeblock}


### Inicializando o SDK
{: #initialize-ios}

1. Inicialize o SDK do cliente passando os parâmetros de ID e de região do locatário para o método de inicialização. Um lugar comum, mas não obrigatório, para colocar o código de inicialização é no método `application:didFinishLaunchingWithOptions` do AppDelegate em seu aplicativo Swift.

  ```swift
  AppID.sharedInstance.initialize (tenantId: < tenantId>, region: AppID.Region_UK)
  ```
  {: codeblock}

  <table>
  <caption> Tabela. Componentes de comando explicados </caption>
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
      <td> É possível localizar a sua região na UI. As opções são `AppID.REGION_US_SOUTH`, `AppID.REGION_UK`, `AppID.REGION_Sydney` ou `AppID.REGION_Germany`.</td>
    </tr>
  </table>

2. Inclua a importação a seguir em seu arquivo `AppDelegate`.

    ```swift
    import IBMCloudAppID
    ```
    {: codeblock}

3. Inclua o código a seguir em seu arquivo AppDelegate.

  ```swift
  func application( application: UIApplication, open url: URL, options :[UIApplicationOpenURLOptionsKey : Any]) -> Bool {
          return AppID.sharedInstance.application(application, open: url, options: options)
      }
  ```
  {: codeblock}

Agora você está pronto para configurar os seus provedores de identidade e começar a autenticar usuários. Para obter mais informações sobre o SDK do iOS, consulte o <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">{{site.data.keyword.appid_short_notm}}repositório GitHub do iOS<img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.

</br>

## Configurando o SDK do Node.js
{: #nodejs-setup}

### Antes de iniciar
{: #before-nodejs}

Verifique se os pré-requisitos a seguir estão prontos:
1. Instale a  [ CLI do IBM Cloud ](../cli/index.html).
2. Implemente o seu servidor do Node.js com a <a href="http://expressjs.com/" target="_blank">Estrutura Express<img src="../icons/launch-glyph.svg" alt="Ícone de link externo"></a>. Para instalar a estrutura Express, use a linha de comandos para abrir o diretório com o aplicativo Node.js e execute o comando a seguir:
  ```
  npm install -- save express
  ```
  {: codeblock}
3. Instale o Passport. Use a linha de comandos para abrir o diretório com o aplicativo Node.js e execute o comando a seguir:
  ```
  npm install -- save passport
  ```
  {: codeblock}

**Nota**: outras estruturas usam estruturas `Express`, como LoopBack. É possível usar o SDK do servidor
{{site.data.keyword.appid_short_notm}} com qualquer uma dessas estruturas.


### Instalando o SDK
{: #install-nodejs}

1. Usando a linha de comandos, abra o diretório como seu app Node.js.
2. Instale o serviço do  {{site.data.keyword.appid_short_notm}} .
  ```
  npm install -- save ibmcloud-appid
  ```
  {: codeblock}

### Inicializando o SDK
{: #initialize}

1. Inclua as definições `require` no arquivo `server.js`.
    ```
    const express = require('express');
    const session = require('express-session')
    const passport = require('passport');
    const WebAppStrategy = require("ibmcloud-appid").WebAppStrategy;
    const CALLBACK_URL = "/ibm/cloud/appid/callback";
    ```
    {: codeblock}

2. Configurar seu app express para usar o middleware express-session. **Nota**: deve-se configurar o middleware com o armazenamento de sessão adequado para ambientes de produção. Para obter mais informações, consulte o <a href="https://github.com/expressjs/session" target="_blank">expressjs docs <img src="../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.
    ```
    const app = express();
    app.use(session({
        secret: "123456",
        resave: true,
        saveUninitialized: true
        }));
    app.use(passport.initialize());
    app.use(passport.session());
    ```
    {: codeblock}

3. Passe o ID do locatário e as credenciais para inicializar o SDK.
    ```
    passport.use(new WebAppStrategy({
    	  tenantId: "{tenant-id}",
   	    clientId: "{client-id}",
      	secret: "{secret}",
      	oauthServerUrl: "{oauth-server-url}",
      	redirectUri: "{app-url}" + CALLBACK_URL
      }));
    ```
    {: codeblock}

 <table summary="Command components: Node.js apps">
  <caption>Componentes de comando para apps Node.js</caption>
    <tr>
      <th>Componentes</th>
      <th>Descrição</th>
    </tr>
    <tr>
      <td><i> tenantID </i></td>
      <td>O ID do locatário é um identificador exclusivo usado para inicializar o aplicativo. É possível localizar o valor no painel de serviço do {{site.data.keyword.appid_short_notm}} clicando em **Visualizar credenciais** na guia **Credenciais de serviço**.</td>
    </tr>
    <tr>
      <td><i>clientID</i> </br> <i>secret</i> </br> <i>oauth-server-url</i> </br> </td>
      <td>É possível localizar esses valores clicando em **Visualizar credenciais** na guia **Credenciais de serviço** do painel de serviço.</td>
    </tr>
    <tr><td><i> redirectUri </i></td>
    <td>O valor redirectUri pode ser fornecido de três formas:</br>
        1. Manualmente em novo WebAppStrategy({redirectUri: "...."})</br>
        2. Como variável de ambiente chamada  ` redirectUri `</br>
        3. Se nenhuma das formas acima tiver sido fornecida, o SDK do ID do App tentará recuperar o application_uri do aplicativo que estiver em execução no IBM Cloud e anexará um sufixo padrão "/ibm/cloud/appid/callback"</td>
    </tr>
    <tr>
      <td><i> CALLBACK_URL </i></td>
      <td>A URL para a página que os usuários verão após efetuarem login.</td>
    </tr>
  </table>

4. Configure o passaporte com serialização e desserialização. Essa etapa de configuração é necessária para a persistência de sessão autenticada nas solicitações de HTTP. Para obter mais informações, consulte os <a href="http://passportjs.org/docs" target="_blank">documentos de passaporte<img src="../icons/launch-glyph.svg" alt="Ícone de link externo"> </a>.

  ```
  passport.serializeUser (function (user, cb) {
    cb(null, user);
    });

  passport.deserializeUser(function(obj, cb) {
    cb(null, obj);
    });
  ```
  {: codeblock}

5. Inclua o código a seguir em seu arquivo `server.js` para emitir os redirecionamentos de serviço:
   ```
   app.get(CALLBACK_URL, passport.authenticate(WebAppStrategy.STRATEGY_NAME));
   app.get('/protected', passport.authenticate(WebAppStrategy.STRATEGY_NAME)), function(req, res)
        res.json(req.user);
   });
   ```
   {: codeblock}

   **Nota**: o serviço redireciona na ordem a seguir:
    1. A URL original da solicitação que acionou o processo de autenticação, conforme persistido na sessão HTTP sob a chave `WebAppStrategy.ORIGINAL_URL`.
    2. Um redirecionamento bem-sucedido, conforme especificado em `passport.authenticate(name, {successRedirect: "...."}).`
    3. Raiz do aplicativo ("/")

6. Reimplemente seu aplicativo.

Para obter mais informações, consulte o
<a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">{{site.data.keyword.appid_short_notm}}
repositório GitHub do Node.js <img src="../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.

## Configurando o SDK Swift
{: #swift-setup}

Proteja seus backends e APIs com o SDK do servidor do {{site.data.keyword.appid_short}}.
{:shortdesc}


### Antes de iniciar
{: #before-swift}

Antes de trabalhar com o SDK Swift, deve-se ter os pré-requisitos a seguir:

* MacOS ou Linux
* OpenSSL 1.0.2 no Linux
* Instale o Swift 3.0.2
* Instale o Kitura 1.6


### Instalando o SDK
{: #install-swift}

1. Abra o arquivo `Package.swift` no diretório de seu app Swift e inclua a dependência `appid-serversdk-swift`.

  ```swift
  let package = Package(
      name: “myApp",
      dependencies: [
          .package(url: "https://github.com/ibm-cloud-security/appid-serversdk-swift.git", .upToNextMinor(from: “4.0.0")),
      ],
      targets: [
          .target(
              name: "myApp",
              dependencies: ["IBMCloudAppID"]),
      ]
  )
  ```
  {: codeblock}

2. Para MacOS: quando você constrói na linha de comandos, todos os pacotes devem incluir as sinalizações a seguir.
  ```
  swift build -Xlinker -L/usr/local/opt/openssl/lib -Xcc -I/usr/local/opt/openssl/include
  ```
  {: pre}

3. Use o comando a seguir quando criar um xcodeproject:
  ```
  swift package generate-xcodeproj --xcconfig-overrides openssl.xcconfig
  ```
  {: pre}

  É possível copiar o openssl.xcconfig do <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">{{site.data.keyword.appid_short_notm}} GitHub do Swift <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>  {: tip}

4. Inclua o código a seguir no aplicativo Swift para:
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
    import IBMCloudAppID
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

5. Reimplemente seu aplicativo.

</br>

## Configurando o SDK do Liberty for Java
{: #lfj-setup}

É possível configurar o {{site.data.keyword.appid_short_notm}} para trabalhar com os aplicativos da web Liberty for Java.
{:shortdesc}

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

4. Em seu arquivo `server.xml`, defina seu tipo de assunto especial como ALL_AUTHENTICATED_USERS.

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

5. Em seu elemento `<application-bnd>`, <a href="https://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_authorization.html?cp=SSAW57_8.5.5&cm_mc_uid=18498555367014888859884&cm_mc_sid_50200000=1494855872" target="_blank">defina as funções <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> conforme localizadas
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

6. Obtenha um certificado.

    a. Em seu painel do {{site.data.keyword.appid_short_notm}}, clique em Credenciais de serviço.

    b. Clique em **Visualizar credenciais** e copie a `oauthServerUrl`.

    c. Inclua `/token` na URL. Use o Firefox para navegar na URL de saída
e obter o certificado. É possível usar a URL a seguir como um exemplo.

    ```
    https://appid-oauth.ng.bluemix.net/oauth/v3/5d12852e-b0a0-46a3-9547-67a4a33a7164/token
    ```
    {: screen}

    d. Na barra de endereço do Firefox, clique no ícone de bloqueio > **seta para a direita** > **mais informações** > **visualizar certificado**.

    e. Na guia **Segurança**, clique em **Visualizar certificado** > **Detalhes**.

    f. Exporte o certificado e salve-o em sua unidade local como um arquivo PEM.

7. Inclua o certificado em seu arquivo truststore.jks do Liberty for Java usando o <a href="https://www.ibm.com/support/knowledgecenter/SSYKE2_6.0.0/com.ibm.java.security.component.60.doc/security-component/keytoolDocs/keytool_overview.html" target="_blank">Liberty Keytool <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> e inclua uma referência no alias de certificado no elemento OIDC. Seu `.jks file` está
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

    **Nota**: o certificado pode ser expirado/mudado; nesse caso, é necessário atualizar o trustore com o novo certificado.

8. Em seu arquivo `manifest.yml`, defina sua instância do {{site.data.keyword.appid_short_notm}}.

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

  ```
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
         authFilterid="myAuthFilter"/>
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



</br>

## Incluindo o {{site.data.keyword.appid_short_notm}} em um aplicativo existente que não seja executado no {{site.data.keyword.Bluemix_notm}}
{: #existing}

É possível incluir o {{site.data.keyword.appid_short_notm}} em aplicativos que não são executados no {{site.data.keyword.Bluemix_notm}}. É possível ver alguns exemplos nesse tópico, mas estes não são os únicos idiomas com os quais é possível usar o serviço.

</br>

**Node.js **

No app Node.js, substitua `passport.use(new WebAppStrategy());` pelo código a seguir.

  ```
  passport.use(new WebAppStrategy({
    	  tenantId: "{tenant-id}",
   	    clientId: "{client-id}",
      	secret: "{secret}",
      	oauthServerUrl: "{oauth-server-url}",
      	redirectUri: "{app-url}" + CALLBACK_URL
      }));
  ```
  {: codeblock}

  <table>
  <caption> Tabela. Componentes de comando para apps Node.js explicados </caption>
    <tr>
      <th> Componentes </th>
      <th> Descrição </th>
    </tr>
    <tr>
      <td><code>tenant-id</code> </br> <code> clientID </code> </br> <code> secret </code> </br> <code> oauth-server-url </code> </br></td>
      <td> É possível localizar esses valores clicando em **Visualizar credenciais** na guia **Credenciais de serviço** do painel de serviço. </td>
    </tr>
    <tr>
      <td><code> app-url </code></td>
      <td>A URL do aplicativo.</td>
    </tr>
    <tr>
      <td><code> CALLBACK_URL </code></td>
      <td> A URL que os usuários da página verão depois de efetuarem login. </td>
    </tr>
  </table>

</br>

**Swift

 **

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
  <caption>Tabela. Componentes de comando para apps Swift explicados</caption>
    <tr>
      <th> Componentes </th>
      <th> Descrição </th>
    </tr>
    <tr>
      <td><code>tenant-id</code> </br> <code> clientID </code> </br> <code> secret </code> </br> <code> oauth-server-url </code> </br></td>
      <td> É possível localizar esses valores clicando em **Visualizar credenciais** na guia **Credenciais de serviço** do painel de serviço. </td>
    </tr>
    <tr>
      <td><code> app-url </code></td>
      <td>A URL do aplicativo.</td>
    </tr>
    <tr>
      <td><code> CALLBACK_URL </code></td>
      <td> A URL que os usuários da página verão depois de efetuarem login. </td>
    </tr>
  </table>


</br>

**Liberty for Java**

Nos aplicativos Liberty for Java, conclua as etapas em [Configurando o SDK do Liberty for Java](#lfj-setup), mas substitua as variáveis de elemento do cliente OIDC pelo código a seguir.

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
  <caption>Tabela. Variáveis do elemento OIDC para os aplicativos Liberty for Java</caption>
    <tr>
      <th> Componente </th>
      <th> Descrição </th>
    </tr>
    <tr>
    <td><code> clientID </code> </br> <code> secret </code> </br> <code> oauth-server-url </code> </br></td>
    <td>É possível localizar esses valores clicando em **Visualizar credenciais** na guia **Credenciais de serviço** do painel de serviço.</td>
    </tr>
    <tr>
      <td><code> authorizationEndpointURL </code></td>
      <td> Inclua `/authorization` no final da oauthServerURL.</td>
    </tr>
    <tr>
      <td><code> tokenEndpointUrl </code></td>
      <td>Inclua `/token` no final da oauthServerURL.</td>
    </tr>
    <tr>
      <td><code> jwkEndpointUrl </code></td>
      <td>Inclua `/publickeys` no final da oauthServerURL.</td>
    </tr>
    <tr>
      <td><code> issuerIdentifier </code></td>
      <td>Muda com base em sua região. Ele pode ser um dos seguintes: </br><ul><li>issuerIdentifier="appid-oauth.ng.bluemix.net" </br><li> issuerIdentifier="appid-oauth.eu-gb.bluemix.net" </br><li>issuerIdentifier="appid-oauth.au-syd.bluemix.net"</ul></td>
    </tr>
    <tr>
      <td><code> tokenEndpointAuthMethod </code></td>
      <td>Especificado como "basic".</td>
    </tr>
    <tr>
      <td><code> signatureAlgorithm </code></td>
      <td>Especificado como "RS256".</td>
    </tr>
    <tr>
      <td><code>authFilterid</code></td>
      <td>A lista dos recursos a serem protegidos.</td>
    </tr>
    <tr>
      <td><code> trustAliasName </code></td>
      <td>O nome de seu certificado em seu armazenamento confiável.</td>
    </tr>
  </table>
