---

copyright:
  years: 2017, 2018
lastupdated: "2018-01-02"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


# Protegendo recursos de backend

É possível usar os SDKs do servidor {{site.data.keyword.appid_short_notm}} para proteger recursos em seu app Node.js. Também é possível usar os SDKs do cliente para acessar recursos protegidos.

**Observação**: chamar um recurso protegido iniciará o widget de login, se necessário. Se um token válido já tiver sido obtido, o widget de login não será iniciado e o recurso será acessado diretamente.

## Protegendo recursos no Liberty for Java
{: #protecting-liberty}

É possível usar o {{site.data.keyword.appid_short_notm}} para proteger terminais em
seus apps IBM Liberty for Java. O Liberty for Java tem a capacidade integrada de manipular solicitações
do Open ID Connect (OIDC).

Antes de iniciar:
* Você precisa de um [App IBM Liberty for Java](https://console.bluemix.net/catalog/starters/liberty-for-java) existente, desvinculado. Para se familiarizar com o desenvolvimento de
apps Liberty for Java, veja [os docs](/docs/runtimes/liberty/index.html).
* Certifique-se de ter o [Apache Maven](https://maven.apache.org/download.cgi) instalado.
* Aprenda sobre como o OIDC funciona com o Liberty for Java.

Para proteger seus recursos:

1. Faça download da amostra do Liberty for Java na UI. A amostra contém um arquivo zip com
os arquivos Liberty padrão.
2. Abra o terminal no diretório no qual você extraiu a amostra.
3. Efetue login no {{site.data.keyword.Bluemix_notm}} usando a linha de comandos do
Cloud Foundry. Quando solicitado, insira suas credenciais.

  ```
  cf login
  ```
  {: codeblock}

4. Implemente o app. Executar o comando a seguir cria uma instância do Liberty for Java com um nome relacionado ao tenantid.

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


## Acessando recursos protegidos com o SDK do Swift iOS
{: #requesting-swift}

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
