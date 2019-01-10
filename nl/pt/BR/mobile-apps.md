---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:pre: .pre}
{:tip: .tip}
{:screen: .screen}

# Apps móveis
{: #adding-mobile}

Com o {{site.data.keyword.appid_full}}, é possível construir rapidamente uma camada de autenticação para seu
aplicativo móvel nativo ou híbrido.
{: shortdesc}

## Entendendo o fluxo
{: #understanding}

**Quando esse fluxo seria útil?**

Um fluxo móvel é útil quando você está desenvolvendo um aplicativo que deve ser instalado no dispositivo de um usuário
(um aplicativo nativo). Usando esse fluxo, é possível autenticar com segurança os usuários em seu aplicativo para
fornecer experiências de usuário personalizadas nos dispositivos.

**Qual é a base técnica do fluxo?**

Como os aplicativos nativos são instalados diretamente no dispositivo de um usuário, as informações privadas do usuário
e as credenciais do aplicativo podem ser extraídas por terceiros com relativa facilidade. Por padrão, esses tipos de
aplicativos são conhecidos como clientes não confiáveis, já que não podem armazenar credenciais globais ou tokens de
atualização do usuário. Como resultado, clientes não confiáveis requerem que os usuários insiram suas credenciais
toda vez que seus tokens de acesso expiram.

Para converter seu aplicativo em um cliente confiável, o {{site.data.keyword.appid_short}} aproveita o
[Registro de cliente dinâmico](https://tools.ietf.org/html/rfc7591). Antes de uma instância do
aplicativo começar a autenticar usuários, ele registra primeiro como um cliente OAuth2 com o {{site.data.keyword.appid_short}}. Como
resultado do registro do cliente, seu aplicativo recebe um identificador de cliente específico da instalação que pode ser
assinado digitalmente e usado para autorizar solicitações com o {{site.data.keyword.appid_short}}. Como o {{site.data.keyword.appid_short}} armazena a chave pública correspondente do aplicativo, ela pode validar sua
assinatura de solicitação que permite que seu aplicativo seja visualizado como um cliente confidencial. Esse processo
minimiza o risco de seu aplicativo de expor credenciais indefinidamente e aprimora muito a experiência do usuário,
permitindo a atualização automática do token.

Após o registro, seus usuários são autenticados usando os fluxos de
[concessão de autorização](https://tools.ietf.org/html/rfc6749#section-1.3) `authorization
code` ou `resource owner password` do OAuth2 para autenticar os usuários.

**Qual é o aspecto desse fluxo?**

![Fluxo de aplicativo para aplicativo do {{site.data.keyword.appid_short_notm}}](images/mobile-flow.png)

**Registro do cliente dinâmico**

1. Um usuário executa uma ação que aciona uma solicitação pelo aplicativo cliente para o SDK do {{site.data.keyword.appid_short}}.
2. Se o aplicativo ainda não estiver registrado como um cliente móvel, o SDK iniciará um fluxo de registro dinâmico.
3. Em um registro bem-sucedido, o {{site.data.keyword.appid_short}} retorna seu identificador de cliente específico
da instalação.

**Fluxo de autorização**

1. O SDK do {{site.data.keyword.appid_short}} inicia o processo de autorização usando o terminal
`/authorization` do {{site.data.keyword.appid_short_notm}}.
2. O widget de login é exibido para o usuário.
3. O usuário é autenticado usando um dos provedores de identidade configurados.
4. O {{site.data.keyword.appid_short}} retorna uma concessão de autorização.
5. A concessão de autorização é trocada para tokens de acesso, identidade e atualização por meio do terminal
`/token` do {{site.data.keyword.appid_short_notm}}.


## Configurando seu aplicativo móvel com os SDKs do {{site.data.keyword.appid_short}}
{: #configuring}

Introdução ao {{site.data.keyword.appid_short}} com nossos SDKs.
{: shortdesc}

**Antes de iniciar**

As seguintes informações são necessárias:

* Uma instância do {{site.data.keyword.appid_short_notm}}

* O ID do locatário da instância. Isso pode ser localizado na guia **Credenciais de serviço** de seu painel de serviço.

* A região do {{site.data.keyword.Bluemix}} de implementação de sua instância. É possível localizar sua região
verificando no console.

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

## Autenticando com o SDK do Android
{: #android-setup}

**Antes de iniciar**

Deve-se ter os pré-requisitos a seguir antes de iniciar:

  * API 27 ou mais recente
  * Java 8.x
  * Android SDK Tools 26.1.1+
  * Android SDK Platform Tools 27.0.1+
  * Android Build Tools versão 27.0.0+

</br>

**Instalando o SDK**

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

3. Localize o arquivo `build.gradle` do aplicativo. **Nota**: certifique-se de abrir o arquivo para o seu app, não o arquivo `build.gradle` do projeto.

  1. Inclua o SDK do cliente do {{site.data.keyword.appid_short_notm}} na seção de dependências.

    ```gradle
    dependencies {
       compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:4.+'
   }
    ```
    {: codeblock}

  2. Na seção `defaultConfig`, configure o esquema de redirecionamento.

    ```gradle
    defaultConfig {
      ...
      manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
    ```
    {: codeblock}

6. Sincronize seu projeto com o Gradle. Clique em **Ferramentas > Android > Sincronizar projeto com arquivos Gradle**.

</br>

**Inicializando o SDK**


1. Transmita os parâmetros de contexto, ID do locatário e região para o método de inicialização para configurar o SDK.

    Um local comum, mas não obrigatório, para colocar o código de inicialização está no método onCreate da atividade principal em seu aplicativo Android.
    {: tip}

    ```java
    AppID.getInstance().initialize(getApplicationContext(), <tenantId>, <region>);
    ```
    {: codeblock}

</br>
</br>

## Autenticando com o SDK do iOS Swift
{: #ios-setup}

Proteja seus aplicativos móveis usando o SDK do cliente do {{site.data.keyword.appid_short}}.
{:shortdesc}

</br>
**Antes de iniciar**

Deve-se ter os pré-requisitos a seguir antes de iniciar:

  * Xcode 9.0 ou mais recente
  * CocoaPods 1.1.0 ou mais recente
  * iOS 10.0 ou superior

</br>

**Instalando o SDK**

O SDK do cliente do {{site.data.keyword.appid_short_notm}} é distribuído com o CocoaPods, um gerenciador de dependência para projetos Swift e
Objective-C Cocoa. O CocoaPods faz download de artefatos e os torna disponíveis para o seu projeto.

1. Crie um projeto Xcode ou abra um existente.

2. Crie um novo ou abra seu `Podfile` existente no diretório do projeto.

3. Inclua o pod `IBMCloudAppID` e o comando `use_frameworks!` para as dependências de seu destino

  ```swift
  target '<yourTarget>' do
     use_frameworks!
     pod 'IBMCloudAppID ' end
  ```
  {: codeblock}

4. Instale suas dependências por meio da linha de comandos dentro do diretório do projeto.

  ```swift
  $ pod install --repo-update
  ```
  {: codeblock}

5. Após a instalação, abra o arquivo `<your app>.xcworkspace` que contém seu projeto Xcode e suas
dependências vinculadas

6. Ative o compartilhamento de keychain no projeto Xcode. Navegue para **Configurações do projeto > Recursos > Compartilhamento de keychain** e selecione **Ativar compartilhamento de keychain**.

7. Abra **Configurações do projeto > Informações > Tipos de URL** e inclua um **Tipo de URL**. Coloque o valor a seguir nas duas caixas de texto: **Identificador** e **Esquema URL**.

  ```
  $(PRODUCT_BUNDLE_IDENTIFIER)
  ```
  {: codeblock}

</br>

**Inicializando o SDK**

1. Inicialize o SDK do cliente passando os parâmetros de ID e de região do locatário para o método de inicialização.

  ```swift
    AppID.sharedInstance.initialize(tenantId: <tenantId>, region: <region>)
  ```
  {: codeblock}

  Um local comum, embora não obrigatório, para colocar o código de inicialização é no método
`application:didFinishLaunchingWithOptions` do arquivo AppDelegate do aplicativo Swift.
  {: tip}

2. Importe o SDK do {{site.data.keyword.appid_short}} para seu arquivo `AppDelegate`.

  ```swift
  import IBMCloudAppID
  ```
  {: codeblock}

3. Configure seu aplicativo para processar redirecionamentos por meio do {{site.data.keyword.appid_short}}.

  ```swift
  func application( application: UIApplication, open url: URL, options :[UIApplicationOpenURLOptionsKey : Any]) -> Bool {
      return AppID.sharedInstance.application(application, open: url, options: options)
      }
  ```
  {: codeblock}

</br>
</br>

## Acessando as APIs protegidas
{: #accessing-protected-apis}

Depois de um fluxo de login bem-sucedido, é possível usar seus tokens de acesso e de identidade para chamar recursos de
back-end protegidos que usam o SDK ou uma biblioteca de rede de sua escolha.

</br>

### Acessando as APIs protegidas com o SDK do Swift

1.  Inclua as importações a seguir no arquivo no qual você deseja chamar uma solicitação de recurso protegido:

  ```swift
  import BMSCore
  import IBMCloudAppID
  ```
  {: codeblock}

2. Chame seu recurso protegido

   ```swift
  BMSClient.sharedInstance.initialize(region: <region>)
  BMSClient.sharedInstance.authorizationManager = AppIDAuthorizationManager(appid: AppID.sharedInstance)

  let request =  Request(url: "<your protected resource url>")

  request.send { (response: Response?, error: Error?) em

      guard let response = response, error == null else {
          print("An error occurred invoking a protected resources", error?.localizedDescription ?? "No response was received")
          return;
      }
      // use your response object
  })
  ```
  {: codeblock}

</br>

### Acessando APIs protegidas com o SDK do Android

1. Inclua as importações a seguir no arquivo no qual você deseja chamar uma solicitação de recurso protegido:
  ```java
  import com.ibm.mobilefirstplatform.clientsdk.android.core.api.BMSClient;
  import com.ibm.cloud.appid.android.api.AppIDAuthorizationManager;
  ```

2. Chame seu recurso protegido
   ```java
   BMSClient bmsClient = BMSClient.getInstance();
   bmsClient.initialize(getApplicationContext(), <region>);

   AppIDAuthorizationManager appIdAuthMgr = new AppIDAuthorizationManager(AppID.getInstance())
  bmsClient.setAuthorizationManager(appIdAuthMgr);

   Request request = new Request("<your protected resource url>", Request.GET);
  request.send(this, new ResponseListener() {

   @Override
		public void onSuccess (Response response) {
       Log.d("My app", "onSuccess :: " + response.getResponseText());
   }

   @Override
		public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
       if (null != t) {
           Log.d("My app", "onFailure :: " + t.getMessage());
       } else if (null != extendedInfo) {
           Log.d("My app", "onFailure :: " + extendedInfo.toString());
       } else {
           Log.d("My app", "onFailure :: " + response.getResponseText());
           }
       }
   });
  ```
  {: codeblock}

</br>

### Acessando APIs protegidas sem um SDK

Com a biblioteca de sua escolha, configure o cabeçalho da solicitação de `Autorização` para usar o esquema de autenticação de `Portador` para transmitir o token de acesso.
Formato de solicitação de exemplo:
  ```
  GET /resource HTTP/1.1
  Host: server.example.com
  Authorization: Bearer <access token> <optional identity token>
  ```
  {: screen}

</br>
</br>

## Próximas etapas
{: #next}

Com o {{site.data.keyword.appid_short}} instalado em seu aplicativo, você está quase pronto para começar a autenticar usuários. Tente executar uma das atividades a seguir em seguida:

* Configure os seus [provedores de identidade](/docs/services/appid/identity-providers.html)
* Customize e configure [o widget de login](/docs/services/appid/login-widget.html)
* Saiba mais sobre o <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">SDK do Android<img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>
* Saiba mais sobre o <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">SDK do iOS<img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>
