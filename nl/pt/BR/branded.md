---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:tip: .tip}

# Marcando seu app
{: #branding}

É possível exibir suas próprias telas customizadas e aproveitar os recursos de autenticação e autorização do {{site.data.keyword.appid_full}}. 
Com o Cloud Directory como o provedor de identidade, os usuários são capazes de interagir com o seu app com menos ajuda sua. Eles são capazes de conectar-se, inscrever-se, mudar a senha e muito mais, sem pedir ajuda.
{: shortdesc}

Quando você usa suas próprias telas, o [Fluxo de credenciais de senha do proprietário do recurso](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html) é usado para fornecer tokens de acesso e de identidade.


## Inserindo uma marca no aplicativo com o SDK do iOS Swift
{: #branded-ui-ios-swift}

Com o Cloud Directory ativado, é possível chamar as suas próprias telas de marca com o SDK do iOS Swift.
{: shortdesc}

</br>
**Conectar**

1. Na guia do provedor de identidade da GUI, configure o Cloud Directory como **Ativado**.
2. Chame o widget de login para iniciar o fluxo de conexão. Os tokens de acesso e de identidade são obtidos quando um usuário
tenta efetuar login usando o nome de usuário ou e-mail e uma senha.
  ```swift
  class delegate : TokenResponseDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
      //User authenticated
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
      //Exception occurred
      }
  }

  AppID.sharedInstance.signinWithResourceOwnerPassword(username: username, password: password, delegate: delegate())
  ```
  {: pre}

</br>

**Inscrever**

1. Na guia do provedor de identidade na GUI, configure o Cloud Directory como **Ativado**.
2. Configure **Permitir que os usuários se inscrevam e reconfigurem sua senha** como **Ativado** nas configurações do Cloud Directory.
3. Chame o widget de login para iniciar o fluxo de inscrição.
  ```swift
  class delegate : AuthorizationDelegate {
    public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
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

1. Na guia do provedor de identidade na GUI, configure o Cloud Directory como **Ativado**.
2. Configure **Permitir que os usuários se inscrevam e reconfigurem sua senha** como **Ativado** nas configurações do Cloud Directory.
3. Chame o widget de login para iniciar o fluxo Esqueci a senha.
  ```swift
  class delegate : AuthorizationDelegate {
     public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
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

**Detalhes da mudança**

1. Na guia do provedor de identidade na GUI, configure o Cloud Directory como **Ativado**.
2. Configure **Permitir que os usuários se inscrevam e reconfigurem sua senha** como **Ativado** nas configurações do Cloud Directory.
3. Chame o widget de login para iniciar o fluxo de detalhes de mudança.
  ```swift
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
         //User authenticated, and fresh tokens received } public func onAuthorizationCanceled() {
          //changed details canceled by the user
       }

       public func onAuthorizationFailure(error: AuthorizationError) {
          //Exception occurred
      }
  }

   AppID.sharedInstance.loginWidget?.launchChangeDetails(delegate: delegate())
  ```
  {: pre}

</br>

**Mudar senha**

1. Na guia do provedor de identidade na GUI, configure o Cloud Directory como **Ativado**.
2. Configure **Permitir que os usuários se inscrevam e reconfigurem sua senha** como **Ativado** nas configurações do Cloud Directory.
3. Chame o widget de login para iniciar o fluxo de detalhes de mudança.
  ```swift
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
          //User authenticated, and fresh tokens received } public func onAuthorizationCanceled() {
          //change password canceled by the user
       }

       public func onAuthorizationFailure(error: AuthorizationError) {
           //Exception occurred
      }
   }

    AppID.sharedInstance.loginWidget?.launchChangePassword(delegate: delegate())
  ```
  {: pre}

</br>


## Inserindo uma marca no aplicativo com o SDK do Android
{: #branded-ui-android}

Com o diretório da nuvem ativado, é possível chamar telas customizadas com o SDK Android. É possível escolher a combinação das telas com as quais você gostaria que seus usuários fossem capazes de interagir.<a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="blank">Veja este blog<img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> para um exemplo detalhado!
{: shortdesc}

</br>

**Conectar**

1. Configure **Diretório da nuvem** para **Ligado** como um provedor de identidade.
2. Obtenha tokens de acesso, de identidade e de atualização fornecendo o nome do usuário e a senha do usuário final.
3. Chame o widget de login para iniciar o fluxo de conexão.
  ```java
  AppID.getInstance().signinWithResourceOwnerPassword(getApplicationContext(), username, password,
         new TokenResponseListener() {
      @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //Exception occurred
      }

      @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          //User authenticated
        }
  });
  ```
  {: pre}

</br>

**Inscrever**

1. Configure **Diretório da nuvem** para **Ligado** como um provedor de identidade.
2. Configure **Permitir que os usuários se inscrevam e reconfigurem sua senha** como **Ativado** nas configurações do Cloud Directory.
3. Chame o widget de login para iniciar o fluxo de inscrição.
  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
 loginWidget.launchSignUp(this, new AuthorizationListener() {
      @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //Exception occurred
      }

      @Override
        public void onAuthorizationCanceled () {
          //Sign up canceled by the user
			 }

      @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          if (accessToken != null && identityToken != null) {
              //User authenticated
				 } else {
              //email verification is required
				 }
      }
  });
  ```
  {: pre}

</br>


**Esqueci a senha**

1. Configure **Diretório da nuvem** para **Ligado** como um provedor de identidade.
2. Configure **Permitir que os usuários se inscrevam e reconfigurem sua senha** como **Ativado** nas configurações do Cloud Directory.
3. Chame o widget de login para iniciar o fluxo Esqueci a senha.
  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launchForgotPassword(this, new AuthorizationListener() {
      @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //Exception occurred
      }

      @Override
        public void onAuthorizationCanceled () {
          // Forogt password canceled by the user
      }
      @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          // Forgot password finished, in this case accessToken and identityToken will be null.
      }
  });
  ```
  {: pre}

</br>

**Detalhes da mudança**

1. Configure **Diretório da nuvem** para **Ligado** como um provedor de identidade.
2. Configure **Permitir que os usuários se inscrevam e reconfigurem sua senha** como **Ativado** nas configurações do Cloud Directory.
3. Chame o widget de login para iniciar o fluxo de detalhes de mudança.
  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
   loginWidget.launchChangeDetails(this, new AuthorizationListener() {
      @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          // ocorreu uma exceção }

      @Override
        public void onAuthorizationCanceled () {
          // Changed details canceled by the user
      }

      @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          //User authenticated, and fresh tokens received 			 }
  });
  ```
  {: pre}


</br>

**Mudar senha**

1. Configure **Diretório da nuvem** para **Ligado** como um provedor de identidade.
2. Configure **Permitir que os usuários se inscrevam e reconfigurem sua senha** como **Ativado** nas configurações do Cloud Directory.
3. Chame o widget de login para iniciar o fluxo de mudança de senha.
  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launchChangePassword(this, new AuthorizationListener() {
      @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          // ocorreu uma exceção }

      @Override
        public void onAuthorizationCanceled () {
          // Change password canceled by the user
      }

      @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          //User authenticated, and fresh tokens received 			 }
  });
  ```
  {: pre}

</br>
</br>


## Inserindo uma marca no aplicativo com o SDK do Node.js
{: #branded-ui-nodejs}

Com o Cloud Directory ativado, é possível chamar as telas customizadas com o SDK do Node.js.
{: shortdesc}

**Conectar**

Ao usar o WebAppStrategy, os usuários podem se conectar aos aplicativos da web com o nome de usuário e um senha. Depois que
um usuário se conecta com sucesso ao aplicativo, o token de acesso dele é persistido em uma sessão HTTP, desde que ela seja mantida
ativa. Após a sessão HTTP ser fechada ou expirada, o token de acesso também é destruído.

1. Defina o Cloud Directory como **On** em suas configurações do provedor de identidade e especifique um terminal de retorno de chamada.
2. Inclua uma rota de post em seu app que possa ser chamada com os parâmetros username e password e conecte-se com o fluxo de senha do proprietário do recurso.
  ```javascript
  app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true // allow flash messages
  }));
  ```
  {: pre}
  <table>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="More information icon"/>  Parâmetros de comando </th>
    </thead>
    <tbody>
      <tr>
        <td><code> successRedirect </code></td>
        <td>A URL para a qual você deseja redirecionar o usuário após uma autenticação bem-sucedida.</td>
      </tr>
      <tr>
        <td><code> failureRedirect </code></td>
        <td>A URL para a qual você deseja redirecionar o usuário se a autenticação falhar.</td>
      </tr>
      <tr>
        <td><code> failureFlash </code></td>
        <td>Quando configurado como <code>true</code>, uma mensagem de erro é retornada do serviço do Cloud Directory. Por padrão, o
valor é configurado como <code>false</code>.</td>
      </tr>
    </tbody>
  </table>

  1. Se você enviar a solicitação em formato HTML, será possível usar o
middleware do [analisador sintático de corpo](https://www.npmjs.com/package/body-parser).
  2. Para obter a mensagem de erro retornada, é possível usar o [connect-flash](https://www.npmjs.com/package/connect-flash). 
Para obter mais informações, consulte a
[amostra de
aplicativo da web](https://github.com/ibm-cloud-security/appid-serversdk-nodejs/blob/master/samples/web-app-sample.js).
  {: tip}

</br>
**Inscrever**

1. Defina o Cloud Directory como **On** em suas configurações do provedor de identidade e especifique um terminal de retorno de chamada.
2. Configure **Permitir que os usuários se inscrevam e reconfigurem sua senha** como **Ativado** nas configurações do Cloud Directory.
3. Configure **Permitir que os usuários se conectem sem verificação de e-mail** para **Não**. Se você não fizer isso, os tokens de acesso e de identidade do {{site.data.keyword.appid_short_notm}} não poderão ser recuperados.
4. Inclua uma rota de post em seu app que possa ser chamada com os parâmetros username e password e conecte-se com o fluxo de senha do proprietário do recurso.
  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: pre}

</br>

**Esqueci a senha**

1. Defina o Cloud Directory como **On** em suas configurações do provedor de identidade e especifique um terminal de retorno de chamada.
2. Configure **Permitir que os usuários se inscrevam e reconfigurem sua senha** como **Ativado** nas configurações do Cloud Directory.
3. Configure  ** Forgot password email **  para  ** ON **.
4. Passe a propriedade *show* para `WebAppStrategy.FORGOT_PASSWORD` para ativar o formulário de senha esquecida.
  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: pre}

</br>

**Detalhes da mudança**

1. Defina o Cloud Directory como **On** em suas configurações do provedor de identidade e especifique um terminal de retorno de chamada.
2. Configure **Permitir que os usuários se inscrevam e reconfigurem sua senha** como **Ativado** nas configurações do Cloud Directory.
3. Verifique se o usuário foi autenticado anteriormente com o {{site.data.keyword.appid_short_notm}}.
4. Passe a propriedade *show* para `WebAppStrategy.CHANGE_DETAILS` para ativar o formulário de senha esquecida.
  ```javascript
  app.get("/change_details", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_DETAILS
  }));
  ```
  {: pre}

</br>

## Inserindo uma marca no aplicativo com a API
{: #branded-ui-api}

É possível exibir suas próprias telas customizadas e aproveitar os recursos de autenticação e autorização do {{site.data.keyword.appid_short_notm}}. Com o Cloud Directory como o provedor de identidade, os usuários são capazes de interagir com o seu app com menos ajuda sua. Eles são capazes de conectar-se, inscrever-se, reconfigurar suas senhas e muito mais sem pedir ajuda.
{: shortdesc}

Para tornar isso possível, o {{site.data.keyword.appid_short_notm}} expõe as APIs de REST. É possível usar a API de REST para construir um servidor de backend que entrega seu apps da web ou para interagir com um app móvel com suas próprias telas customizadas.

O gerenciamento de API é assegurado pelos tokens gerados pelo IBM Cloud Identity e Access Management. Isso significa que os proprietários de conta podem especificar quem na equipe terá qual nível de acesso para cada instância de serviço. Para mais informações sobre como o IAM e o {{site.data.keyword.appid_short_notm}} trabalham juntos, consulte [Gerenciamento de acesso de serviço](/docs/services/appid/iam.html).

Após ter definido as [configurações](/docs/services/appid/cloud-directory.html), é possível
chamar os terminais a seguir para exibir cada tela.


**Inscrever-se**
É possível usar o terminal `/sign_up` para permitir que os usuários se inscrevam para seu app.
Forneça os seguintes dados no corpo da solicitação:
  * Seu tenantID.
  * Dados do usuário do diretório da nuvem. Veja [Representação do usuário integral do SCIM](https://tools.ietf.org/html/rfc7643#section-8.2) para obter mais detalhes.
    * Um atributo `password`.
    * Na matriz de e-mail com um atributo `primary` que é configurado para `true`, deve-se ter pelo menos 1 endereço de e-mail.

Dependendo da [configurações de e-mail](/docs/services/appid/cloud-directory.html), um usuário pode receber uma solicitação para verificação ou um e-mail que dá as boas-vindas quando eles se inscrevem para seu app. Ambos os tipos de e-mails são acionados quando um usuário se inscreve para seu app. O e-mail de verificação contém um botão **Verificar**. Depois que eles pressionam o botão e confirmam sua identidade, uma tela é exibida pelo {{site.data.keyword.appid_short_notm}} que os agradece por verificar.  

É possível apresentar sua própria página de verificação de post:

1. Navegue até a aba **Páginas de Entrada Customizadas** do painel {{site.data.keyword.appid_short_notm}}.
2. Insira a URL para a sua página de entrada na **URL para sua página de verificação customizada de endereço de e-mail**

Quando esse valor for fornecido, o {{site.data.keyword.appid_short_notm}} chamará a URL junto com uma consulta de `context`. Quando você chama o terminal `/sign_up/confirmation_result` e passa o parâmetro `context` recebido, o resultado indica se o usuário verificou sua conta. Se sim, será possível exibir sua página customizada.

</br>
**Esqueci a senha**

É possível usar o terminal `/forgot_password` para permitir que os usuários recuperem sua senha se a tiverem esquecido.

Forneça os seguintes dados no corpo da solicitação:
  * Seu tenantID.
  * O e-mail do usuário do diretório da nuvem.

Quando o terminal é chamado, um e-mail de reconfiguração de senha é enviado para o usuário. O e-mail contém um botão **Reconfigurar**. Depois que eles pressionam o botão, uma tela é exibida pelo {{site.data.keyword.appid_short_notm}} que permite que eles reconfigurem suas senhas.

É possível apresentar a sua própria página de reconfiguração de senha de post:

1. Navegue até a aba **Páginas de Entrada Customizadas** do painel {{site.data.keyword.appid_short_notm}}.
2. Insira a URL para a sua página de entrada na **URL para sua página customizada de reconfiguração de senha**  

Quando esse valor for fornecido, o {{site.data.keyword.appid_short_notm}} chamará a URL junto com uma consulta de `context`. O parâmetro `context` é usado para receber o resultado quando `/forgot_password/confirmation_result` é chamado. Se o resultado for bem-sucedido, será possível exibir sua página customizada.

Inclua uma sequência aleatória em sua página customizada de reconfiguração de senha e passe-a ao seu backend quando a solicitação for enviada. Deixe o manipulador validar a sequência e chame o terminal `/change_password` somente se ele for válido. Ao fazer isso, é possível reduzir a vulnerabilidade do terminal de reconfiguração de senha de backend.
{: tip}

</br>
**Mudar senha**

É possível usar o terminal `/change_password` de duas maneiras. Quando um usuário envia uma solicitação de reconfiguração ou quando um usuário está conectado ao seu app e deseja atualizar sua senha.

Forneça os dados a seguir no corpo da solicitação para atualizar a senha após uma solicitação de reconfiguração:
  * Seu tenantID.
  * A nova senha do usuário.
  * O UUID do usuário do diretório da nuvem.
  * Opcional: o endereço IP por meio do qual a reconfiguração de senha foi executada. Se você escolher passar o endereço IP, o item temporário `%{passwordChangeInfo.ipAddress}` estará disponível para o modelo de e-mail de mudança de senha.

Dependendo da sua configuração, quando uma senha mudar, o {{site.data.keyword.appid_short_notm}} poderá enviar um e-mail para informar isso ao usuário.

</br>
Para permitir que os usuários mudem suas senhas enquanto conectados a seu app:

Forneça os seguintes dados no corpo da solicitação:
  * Seu tenantID.
  * A nova senha do usuário.
  * O UUID do usuário do diretório da nuvem.

Sua página de mudança de senha deve solicitar ao usuário para inserir sua senha atual e sua nova senha.
{: tip}

Seu backend valida a senha atual do usuário com a API do ROP e, se válida, chama o terminal com a nova senha. Dependendo da sua configuração, quando uma senha mudar, o {{site.data.keyword.appid_short_notm}} poderá enviar um e-mail para informar isso ao usuário.

</br>
**Reenviar**

É possível usar o `/resend/{templateName}` para reenviar um e-mail quando um usuário não o recebe por algum
motivo.

Forneça os seguintes dados no corpo da solicitação:
  * O tenantID.
  * O nome de modelo
  * O UUID do usuário do diretório da nuvem.


**Detalhes da mudança**

Quando um usuário está conectado ao seu app, ele pode atualizar algumas das suas informações. É possível usar o `/Users/{userId}` para obter e atualizar suas informações.

Quando os detalhes do usuário são atualizados, o terminal obtém os dados do usuário atualizados no corpo da solicitação no [formato SCIM](https://tools.ietf.org/html/rfc7643#section-8.2). Certifique-se de que mudar somente os detalhes relevantes.

Seu endereço de e-mail não pode ser mudado.
{: tip}
