---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:pre: .pre}
{:tip: .tip}
{:screen: .screen}
{:codeblock: .codeblock}


# Apps da web
{: #adding-web}

Com o {{site.data.keyword.appid_full}}, é possível construir rapidamente uma camada de autenticação para seus
aplicativos da web.
{: shortdesc}

## Entendendo o fluxo
{: #understanding}

**Quando esse fluxo seria útil?**

Ao desenvolver um aplicativo da web, é possível usar o fluxo da web do {{site.data.keyword.appid_short}} para
autenticar os usuários com segurança. Os usuários podem, então, acessar o conteúdo protegido do lado do
servidor em seus aplicativos da web.

**Qual é a base técnica do fluxo?**

Os apps da web frequentemente requerem que os usuários sejam autenticados para que possam acessar conteúdo protegido. O
{{site.data.keyword.appid_short_notm}} usa o fluxo de código de autorização do OIDC para autenticar os usuários com
segurança. Com esse fluxo, quando o usuário é autenticado, o aplicativo recebe um código de autorização. Em seguida, o
código é trocado por um token de acesso, de identidade e de atualização. No código, a etapa de troca de tokens sempre é
enviada por meio de um canal de retorno seguro entre o aplicativo e o servidor OIDC. Isso fornece uma camada extra de
segurança, pois o invasor não é capaz de interceptar os tokens. Esses tokens podem ser enviados diretamente para o
aplicativo de hospedagem do servidor da web para autenticação do usuário.

**Como esse fluxo funciona?**

![{{site.data.keyword.appid_short_notm}} fluxo de solicitação](images/web-flow.png)

1. Um usuário inicia o fluxo de autorização enviando uma solicitação para o terminal `/authorization` por
meio do SDK ou API do {{site.data.keyword.appid_short_notm}}.

2. Se o usuário estiver desautorizado, o fluxo de autenticação será iniciado com um redirecionamento para o {{site.data.keyword.appid_short_notm}}.

3. Dependendo dos parâmetros de solicitação `/authorization` do usuário ou da configuração do
provedor de identidade, ele ativa o widget de login no navegador do usuário.

4. O usuário escolhe um provedor de identidade com o qual se autenticar e conclui o processo de conexão.

5. O provedor de identidade é redirecionado para o aplicativo cliente com o código de autorização.

6. O SDK do {{site.data.keyword.appid_short_notm}} troca o código de autorização para os tokens de acesso,
de identidade e, opcionalmente, de atualização por meio do serviço do {{site.data.keyword.appid_short_notm}}.

7. Os tokens são salvos pelo SDK do {{site.data.keyword.appid_short_notm}} e ocorre um redirecionamento para o
aplicativo cliente.

8. O usuário tem acesso concedido ao aplicativo.

</br>
</br>

## Configurando o SDK do Node.js
{: #configuring-nodejs}

É possível configurar o {{site.data.keyword.appid_short_notm}} para trabalhar com os aplicativos da web
Node.js.
{: shortdesc}

**Antes de iniciar**

Deve-se ter os pré-requisitos a seguir:

* Uma instância do serviço do {{site.data.keyword.appid_short_notm}}
* Um conjunto de credenciais de serviço
* NPM versão 4 ou superior
* Node versão 6 ou superior
* Seu URI de redirecionamento configurado no painel de serviço do {{site.data.keyword.appid_short_notm}}


### Instalando o SDK do Node.js

1. Usando a linha de comandos, mude para o diretório que contém o aplicativo Node.js.

2. Instale o serviço do  {{site.data.keyword.appid_short_notm}} .
  ```bash
  npm install -- save ibmcloud-appid
  ```
  {: codeblock}

### Inicializando o SDK do Node.js

1. Inclua as definições `require` no arquivo `server.js`.

    ```javascript
    const express = require('express');
    const session = require('express-session')
    const passport = require('passport');
    const WebAppStrategy = require("ibmcloud-appid").WebAppStrategy;
    const CALLBACK_URL = "/ibm/cloud/appid/callback";
    ```
    {: codeblock}

2. Configurar seu app express para usar o middleware express-session. **Nota**: deve-se configurar o middleware com o armazenamento de sessão adequado para ambientes de produção. Para obter mais informações, consulte o <a href="https://github.com/expressjs/session" target="_blank">expressjs docs <img src="../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.

    ```javascript
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

3. Transmita as credenciais de serviço para inicializar o SDK.

  ```javascript
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
          <td><i>tenantId</i> </br> <i>clientId</i> </br> <i>secret</i> </br> <i>oauth-server-url</i> </br> </td>
          <td>É possível localizar esses valores clicando em **Visualizar credenciais** na guia **Credenciais de serviço** do painel de serviço.</td>
      </tr>
      <tr>
        <td><i> redirectUri </i></td>
        <td>O valor do URI de redirecionamento pode ser fornecido de três maneiras:</br>
            1. Manualmente no novo `WebAppStrategy({redirectUri: "...."})`</br>
            2. Como variável de ambiente chamada  ` redirectUri `</br>
            3. Se nenhuma dessas opções for fornecida, o SDK do {{site.data.keyword.appid_short_notm}} tentará recuperar o `application_uri` do aplicativo que estiver em execução no {{site.data.keyword.Bluemix_notm}} e
anexará um sufixo padrão `/ibm/cloud/appid/callback`.
        </td>
      </tr>
    </table>

4. Configure o passaporte com serialização e desserialização. Essa etapa de configuração é necessária para a persistência de sessão autenticada nas solicitações de HTTP. Para obter mais informações, consulte os <a href="http://passportjs.org/docs" target="_blank">documentos de passaporte<img src="../icons/launch-glyph.svg" alt="Ícone de link externo"> </a>.

  ```javascript
  passport.serializeUser (function (user, cb) {
    cb(null, user);
    });

  passport.deserializeUser(function(obj, cb) {
    cb(null, obj);
    });
  ```
  {: codeblock}

5. Inclua o código a seguir em seu arquivo `server.js` para emitir os redirecionamentos de serviço.

   ```javascript
   app.get(CALLBACK_URL, passport.authenticate(WebAppStrategy.STRATEGY_NAME));
   ```
   {: codeblock}

6. Registre seu terminal protegido.

   ```javascript
   app.get(‘/protected’, passport.authenticate(WebAppStrategy.STRATEGY_NAME)), function(req, res) res.json(req.user); });
   ```
   {: codeblock}

Para obter mais informações, consulte o
<a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">{{site.data.keyword.appid_short_notm}}
repositório GitHub do Node.js <img src="../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.

</br>
</br>

## Configurando o SDK do Liberty for Java
{: #configuring-liberty}

É possível configurar o {{site.data.keyword.appid_short_notm}} para trabalhar com os aplicativos da web Liberty for Java.
{:shortdesc}

**Antes de iniciar**

Deve-se ter os pré-requisitos a seguir:
* Uma instância do serviço do {{site.data.keyword.appid_short_notm}}
* Um conjunto de credenciais de serviço
* Apache Maven 3.5 ou superior
* Java 1.8
* Um aplicativo da web Liberty for Java

### Instalando o SDK do Liberty for Java

1. Inclua um recurso de conexão OpenID em seu `server.xml`.

  ```xml
  <featureManager>
      <feature>ssl-1.0</feature>
      <feature>appSecurity-2.0</feature>
      <feature>openidConnectClient-1.0</feature>
  </featureManager>
  ```
  {: codeblock}

2. Crie um recurso cliente da conexão OpenID e defina os itens temporários a seguir. Use as credenciais de serviço para
preencher os itens temporários.

  ```xml
  <openidConnectClient
    clientId='App ID client_ID'
    clientSecret='App ID Secret'
    authorizationEndpointUrl='oauthServerUrl/authorization'
    tokenEndpointUrl='oauthServerUrl/token'
    jwkEndpointUrl='oauthServerUrl/publickeys'
    issuerIdentifier='Changed according to the region'
    tokenEndpointAuthMethod="basic"
    signatureAlgorithm="RS256"
    authFilterid="myAuthFilter"
    trustAliasName="my.bluemix.certificate"
  />
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

### Inicializando o SDK do Liberty for Java

1. Em seu arquivo `server.xml`, defina um filtro de autorização para especificar os recursos
protegidos. Se um filtro não for
<a href="https://www.ibm.com/support/knowledgecenter/en/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/rwlp_auth_filter.html" target="_blank">definido
<img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"> </a>, o serviço protegerá todos os
recursos.

  ```xml
  <authFilter id="myAuthFilter">
             <requestUrl id="myRequestUrl" urlPattern="/protected" matchType="contains"/>
    </authFilter>
  ```
  {: codeblock}

2. Defina seu tipo de assunto especial como `ALL_AUTHENTICATED_USERS`.

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

3. Faça download do arquivo `libertySample-1.0.0.war` por meio do
<a href="https://github.com/ibm-cloud-security/appid-sample-code-snippets/tree/master/liberty-for-java" target="_blank">GitHub
<img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> e coloque-o na pasta de
aplicativos do servidor. Por exemplo, se seu servidor for denominado defaultServer, o arquivo war irá para `target/liberty/wlp/usr/servers/defaultServer/apps/`.

4. Configure o SSL incluindo o seguinte em seu arquivo `server.xml`. Você também precisará criar um
armazenamento confiável.

```xml
  <keyStore id="defaultKeyStore" password="myPassword"/>
  <keyStore id="appidtruststore" password="Liberty" location="${server.config.dir}/mytruststore.jks"/>
  <ssl id="defaultSSLConfig" keyStoreRef="defaultKeyStore" trustStoreRef="appidtruststore"/>
```
{: codeblock}

Por padrão, a configuração do SSL requer que o armazenamento confiável seja configurado para a conexão OpenID. Saiba mais sobre como <a href="https://www.ibm.com/support/knowledgecenter/en/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/twlp_config_oidc_rp.html" target="_blank">configurar
um cliente da conexão OpenID no Liberty <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>
{: tip}

</br>
</br>

## Configurando o SDK do Spring Boot for Java
{: #configuring-spring-boot}

É possível configurar o {{site.data.keyword.appid_short_notm}} para trabalhar com seus aplicativos Spring
Boot.
{:shortdesc}

**Antes de iniciar**

Deve-se ter os pré-requisitos a seguir:

* Uma instância do serviço do {{site.data.keyword.appid_short_notm}}
* Um conjunto de credenciais de serviço
* Um projeto Java + Maven
* Apache Maven 3.5 ou superior
* Java 1.8
* Spring Boot 2.0 e Security OAuth 2.0 ou mais recente


### Inicializando a estrutura da Boot Spring

1. Inclua o seguinte entre as tags `<project> </project>` no arquivo `pom.xml` do Maven.

  ```xml
  <parent>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-parent</artifactId>
      <version>2.0.2.RELEASE</version>
      <relativePath/>
  </parent>
  ```
  {: codeblock}

2. Inclua as dependências a seguir em seu arquivo `pom.xml` do Maven.

  ```xml
  <dependencies>
      <dependency>
          <groupId>org.springframework.boot</groupId>
          <artifactId>spring-boot-starter-web</artifactId>
      </dependency>
      <dependency>
          <groupId>org.springframework.boot</groupId>
          <artifactId>spring-boot-starter-security</artifactId>
      </dependency>
      <dependency>
          <groupId>org.springframework.security.oauth.boot</groupId>
          <artifactId>spring-security-oauth2-autoconfigure</artifactId>
          <version>2.0.0.RELEASE</version>
      </dependency>
  </dependencies>
  ```
  {: codeblock}

3. No mesmo arquivo, inclua o plug-in do Maven.

  ```xml
  <plugin>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-maven-plugin</artifactId>
  </plugin>
  ```
  {: codeblock}

### Inicializando o OAuth2

1. Inclua as anotações a seguir em seu arquivo Java.

  ```java
  @SpringBootApplication
  @EnableOAuth2Sso
  ```
  {: codeblock}

2. Estenda a classe com `WebSecurityConfigurerAdapter`.
3. Substitua qualquer configuração de segurança e registre seu terminal protegido.

  ```java
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.authorizeRequests()
                .antMatchers("/protectedResource").authenticated()
                .and().logout().logoutSuccessUrl("/").permitAll();
    }
  ```
  {: codeblock}


### Incluindo credenciais

1. Inclua um arquivo de configuração `application.yml` no diretório `/springbootsample/src/main/resources/`. É possível concluir sua configuração com as informações de suas credenciais de serviço.

  ```
  security:
  oauth2:
    client:
      clientId: {client ID}
      clientSecret: {client Secret}
      accessTokenUri: {oauthServerUrl}/token
      userAuthorizationUri: {oauthServerUrl}/authorization
    resource:
      userInfoUri: {oauthServerUrl}/userinfo
  ```
  {: codeblock}


Para obter um exemplo passo a passo, consulte <a href="https://www.ibm.com/blogs/bluemix/2018/06/creating-spring-boot-applications-app-id/" target="_blank">este
blog</a>.

</br>
</br>

## Usando o {{site.data.keyword.appid_short_notm}} com outros idiomas
{: #other}

Com um SDK de cliente compatível com OIDC, é possível usar o {{site.data.keyword.appid_short_notm}} com outros
idiomas. Consulte uma lista de <a href="https://openid.net/developers/certified/">bibliotecas
certificadas</a> para obter mais informações.


</br>
</br>

## Próximas Etapas
{: #next}

Com o {{site.data.keyword.appid_short_notm}} instalado em seu aplicativo, você está quase pronto para começar a autenticar os usuários! Tente executar uma das atividades a seguir em seguida:

* Configure os seus [provedores de identidade](/docs/services/appid/identity-providers.html)
* Customize e configure [o Widget de login](/docs/services/appid/login-widget.html)
* Saiba mais sobre o <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">SDK do Node.js<img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>
