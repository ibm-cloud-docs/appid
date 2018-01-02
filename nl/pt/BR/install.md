---
copyright:
  years: 2017
lastupdated: "2017-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Configurando os SDKs
{: #configuring}


## Configurando o SDK do Android
{: #android-setup}

Construa os seus apps Android com o SDK do cliente do {{site.data.keyword.appid_short}}, inicialize o SDK, autentique usuários e faça solicitações
para recursos protegidos e desprotegidos.
{:shortdesc}


### Antes de iniciar

As seguintes informações são necessárias:
  * Uma instância de um serviço do {{site.data.keyword.appid_short_notm}}.
  * O seu ID do locatário. Na guia **Credenciais de serviço** de seu painel de serviço, clique em **Visualizar credenciais**. Seu ID do locatário é exibido no campo **tenantID**. Esse é um identificador exclusivo que é usado para inicializar seu app.
  * A sua região do {{site.data.keyword.Bluemix}}. É possível localizar a sua região procurando na UI. O valor é usado para inicializar o seu app.
    <table> <caption> Tabela 1. Regiões e valores do SDK correspondentes do {{site.data.keyword.Bluemix_notm}} </caption>
    <tr>
      <th> Região do Bluemix </th>
      <th> Valor do SDK </th>
    </tr>
    <tr>
      <td> Sul dos Estados Unidos </td>
      <td> AppID.REGION_US_SOUTH </td>
    </tr>
    <tr>
      <td> Sydney </td>
      <td> AppID.REGION_SYDNEY </td>
    </tr>
    <tr>
      <td> United Kingdom </td>
      <td> AppID.REGION_UK </td>
    </tr>
  </table>

  * Um <a href="https://developers.google.com/web/tools/setup/" target="_blank">Projeto do Android
Studio<img src="../../icons/launch-glyph.svg" alt="ícone de Link externo"></a>, configurado para trabalhar com o Gradle.

### Instalando o SDK do cliente

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

3. Abra o arquivo `build.gradle` para o seu aplicativo.

    **Nota**: certifique-se de abrir o arquivo para o seu app, não o arquivo `build.gradle` do projeto.
4. Localize a seção de dependências do arquivo e inclua uma dependência de compilação para o SDK do cliente do {{site.data.keyword.appid_short_notm}}.

  ```gradle
   dependencies {
       compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:1.+'
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

6. Sincronize seu projeto com o Gradle. Clique em **Ferramentas** > **Android** > **Projeto de sincronização
com Arquivos do Gradle**.

### Inicializando o client SDK

Inicialize o SDK do cliente passando os parâmetros de contexto, ID do locatário e região para o método de inicialização. Um local comum, mas não obrigatório, para colocar o código de inicialização está no método onCreate da atividade principal em seu aplicativo Android.

  ```java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, AppID.REGION_UK);
  ```
  {: codeblock}

1. Substitua *tenantId* por seu serviço tenantId.
2. Substitua o *AppID.REGION_UK* por sua região do {{site.data.keyword.Bluemix_notm}}.

Para obter mais informações, consulte o <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">{{site.data.keyword.appid_short_notm}} repositório GitHub Android <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.

## Configurando o iOS Swift SDK
{: #ios-setup}

Construa os seus apps Swift com o SDK do cliente do {{site.data.keyword.appid_short}}, inicialize o SDK, autentique usuários e faça solicitações
para recursos protegidos e desprotegidos.
{:shortdesc}


### Antes de iniciar

As seguintes informações são necessárias:
  * Uma instância de {{site.data.keyword.appid_short_notm}}.
  * O seu ID do locatário. Na guia **Credenciais de serviço** de seu painel de serviço, clique em **Visualizar credenciais**. O seu ID do
locatário é exibido no campo **TenantID**. Esse é um identificador exclusivo que é usado para inicializar seu app.
  * A sua região do {{site.data.keyword.Bluemix_notm}}.
  É possível localizar a sua região procurando na UI. O valor é usado para inicializar o seu app.
    <table> <caption> Tabela 1. Regiões e valores do SDK correspondentes do {{site.data.keyword.Bluemix_notm}} </caption>
    <tr>
      <th> Região do Bluemix </th>
      <th> Valor do SDK </th>
    </tr>
    <tr>
      <td> Sul dos Estados Unidos </td>
      <td> AppID.REGION_US_SOUTH </td>
    </tr>
    <tr>
      <td> Sydney </td>
      <td> AppID.REGION_SYDNEY </td>
    </tr>
    <tr>
      <td> United Kingdom </td>
      <td> AppID.REGION_UK </td>
    </tr>
  </table>

  * Um projeto Xcode (versão 8.1 ou superior).
  * CocoaPods (versão 1.1.0 ou superior).


### Instalando o SDK do cliente

O SDK do cliente do {{site.data.keyword.appid_short_notm}} é distribuído com o CocoaPods, um gerenciador de dependência para projetos Swift e
Objective-C Cocoa. O CocoaPods faz download de artefatos e os torna disponíveis para o seu projeto.

1. Crie um projeto Xcode ou abra um projeto existente.
2. Abra ou crie o arquivo pod no diretório do projeto.
3. Sob o seu destino de projeto inclua uma dependência para o pod 'BluemixAppID'. Certifique-se de que o comando `use_frameworks!` também
esteja sob o seu destino.

  Por exemplo:

  ```swift
  target '<yourTarget>' do
     use_frameworks!
     pod 'BluemixAppID'
  end
  ```
  {: codeblock}

4. Para fazer download da dependência `BluemixAppID`, execute o comando a seguir.

  ```swift
  pod install --repo-update
  ```
  {: codeblock}

6. Abra o seu projeto Xcode e ative o compartilhamento de keychain. Em **Configurações do projeto**, clique em **Recursos > Compartilhamento de keychain**.
7. Em **Configurações do projeto > Informações > Tipos de URL**, inclua um **Tipo de URL**. Preencha a caixa de texto **Identificador** e a caixa de texto **Esquema de URL** com este valor: `$(PRODUCT_BUNDLE_IDENTIFIER)`


### Inicializando o client SDK

1. Inclua a importação a seguir em seu arquivo `AppDelegate.swift`.

  ```swift
  import BluemixAppID
  ```
  {: codeblock}

2. Inicialize o SDK cliente passando os parâmetros de ID e de região do locatário para o método de inicialização. Um lugar comum, mas não obrigatório, para colocar o código de inicialização é no método `application:didFinishLaunchingWithOptions` do AppDelegate em seu aplicativo Swift.

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, bluemixRegion: AppID.Region_UK)
  ```
  {: codeblock}

  * Substitua *tenantId* com o ID do locatário para seu serviço.
  * Substitua AppID.REGION_UK pela sua região do {{site.data.keyword.appid_short_notm}}.

3. Inclua o código a seguir em seu arquivo AppDelegate.

  ```swift
  func application(_ application: UIApplication, open url: URL, options :[UIApplicationOpenURLOptionsKey : Any]) -> Bool {
          return AppID.sharedInstance.application(application, open: url, options: options)
      }
  ```
  {: codeblock}

Para obter mais informações, consulte o <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">{{site.data.keyword.appid_short_notm}} repositório GitHub iOS<img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.

## Configurando o SDK do Node.js
{: #nodejs-setup}

### Antes de iniciar

* Familiarize-se com o desenvolvimento de aplicativos Node.js no {{site.data.keyword.Bluemix_notm}}.
* O SDK do servidor {{site.data.keyword.appid_short_notm}} requer que o seu servidor Node.js seja implementado com a
<a href="http://expressjs.com/" target="_blank">estrutura Express <img src="../../icons/launch-glyph.svg" alt="ícone de Link externo"></a>.

**Nota**: outras estruturas usam estruturas `Express`, como LoopBack. É possível usar o SDK do servidor
{{site.data.keyword.appid_short_notm}} com qualquer uma dessas estruturas.


### Instalando o SDK do servidor


1. Usando a linha de comandos, abra o diretório como seu app Node.js.
2. Execute os comandos a seguir.

  ```
  npm install -save express
  npm install -save passport
  npm install -save bluemix-appid
  ```
  {: codeblock}

Para obter mais informações, consulte o <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">{{site.data.keyword.appid_short_notm}} repositório do GitHub Node.js <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.

## Configurando o SDK Swift
{: #swift-setup}

### Antes de iniciar

* Familiarize-se com o desenvolvimento de aplicativos Swift no {{site.data.keyword.Bluemix}}.
* Instale o Swift 3.0.2
* Instale o Kitura 1.6


### Instalando o SDK

1. Abra o arquivo `Package.swift` no diretório de seu app Swift e inclua a dependência `appid-serversdk-swift`. Por exemplo:

  ```swift
  import PackageDescription

  let package = Package(
      dependencies: [
          .Package(url: "https://github.com/ibm-cloud-security/appid-serversdk-swift.git", majorVersion: 1)
      ]
  )
  ```
  {: codeblock}

Para obter mais informações, consulte o <a href="https://github.com/ibm-cloud-security/appid-serversdk-swift" target="_blank">{{site.data.keyword.appid_short_notm}} repositório GitHub do Swift <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.
