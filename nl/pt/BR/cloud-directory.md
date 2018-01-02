---

copyright:
  years: 2017
lastupdated: "2017-12-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Gerenciando o Cloud Directory
{: #cd}

É possível configurar o {{site.data.keyword.appid_short_notm}} para usar o Cloud Directory como um provedor de identidade. Quando o usuário se conecta ao e-mail usando uma senha, ele é incluído no seu diretório. É possível gerenciar os usuários na GUI do serviço.
{: shortdesc}

<!--- What is a cloud directory? --->

## Gerenciando configurações de diretório

É possível configurar as notificações e o nível de controle do usuário para seu app. Na guia **Configurações de diretório** da GUI, é possível decidir o quanto de autoatendimento seus usuários poderão fazer.

1. Para permitir que os usuários usem um e-mail para se inscrever, deve-se configurar **Permitir que usuários se inscrevam e reconfigurem sua senha** para **Ativado**. É possível ainda incluir usuários por meio do console quando configurado como **Desativado**, mas apenas para propósitos de desenvolvimento.
2. Configure os detalhes do emissor. Especifique o e-mail que enviará as mensagens, quem aparecerá como o remetente e para quem seus usuários poderão responder.
  **Observação**: certifique-se ao configurar a URL de ação que você dê tempo suficiente para que um usuário clique no link. Um usuário deve verificar seu e-mail para ter algumas opções, como a capacidade de solicitar uma reconfiguração de sua senha.
3. Determine os tipos de e-mails que um usuário recebe e as informações do remetente.



## Gerenciando mensagens

Um modelo é um exemplo de uma mensagem de e-mail que você pode enviar para seus usuários. É possível customizar o modelo atualizando o conteúdo e o layout da mensagem. É possível configurar essas mensagens para **Ativado** ou **Desativado** na guia Configurações do diretório.

1. Selecione um **Tipo de mensagem**.
2. Customize sua mensagem mudando o conteúdo e o design da mensagem. É possível utilizar parâmetros para personalizar suas mensagens. Não se esqueça de salvar suas mudanças!

### Tipos de mensagens

<dl>
  <dt> Bem-vindo </dt>
    <dd>Você pode receber um usuário para seu aplicativo por meio de e-mail, depois de ele já ter se registrado. Para receber e reter seus usuários, torne sua mensagem a mais atrativa possível.
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> Parâmetros que podem ser usados em qualquer tipo de mensagem </th>
      </thead>
      <tbody>
        <tr>
          <td> %{display.logo} </td>
          <td> Exibe a imagem que você configurou para seu widget de login. </td>
        </tr>
	 <tr>
          <td> %{display.headerColor} </td>
          <td> Exibe a cor do cabeçalho configurada para o seu widget de login. </td>
        </tr>
        <tr>
          <td> %{user.displayName} </td>
          <td> Exibe o nome da tela que um usuário escolheu usar ao interagir com o app. </td>
        </tr>
        <tr>
          <td> %{user.email} </td>
          <td> Exibe o endereço de e-mail do usuário registrado. </td>
        </tr>
        <tr>
          <td> %{user.firstName} </td>
          <td> Exibe o nome do usuário especificado. </td>
        </tr>
        <tr>
          <td> %{user.formattedName} </td>
          <td> Exibe o nome completo de um usuário. </td>
        </tr>
        <tr>
          <td> %{user.lastName} </td>
          <td> Exibe o sobrenome do usuário especificado. </td>
        </tr>
      </tbody>
    </table>

    **Observação**: se um usuário não fornecer a informação extraída pelo parâmetro, ela aparecerá em branco.</dd>
  <dt> Senha esquecida </dt>
    <dd> Um usuário esquecer a senha ou precisar atualizá-la por qualquer motivo, ele poderá solicitar a reconfiguração de senha. É possível customizar a resposta de e-mail para sua solicitação. Quando um usuário solicita uma mudança, a senha permanece como era até que ele clique no link neste e-mail.

    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> Parâmetros de mudança de senha </th>
      </thead>
      <tbody>
        <tr>
          <td> %{linkExpiration.hours} </td>
          <td> Exibe o número de horas em que o link é válido. </td>
        </tr>
        <tr>
          <td> %{linkExpiration.minutes} </td>
          <td> Exibe o número de minutos em que o link é válido. </td>
        </tr>
        <tr>
          <td> %{resetPassword.code} </td>
          <td> Exibe uma senha descartável como parte da URL. Isso significa que cada pessoa tem um código diferente. Exemplo: <code>https://appid-wfm.bluemix.net/verify/6574839563478 </code> </td>
        </tr>
        <tr>
          <td> %{resetPassword.link} </td>
          <td> Exibe o link em que um usuário clica para reconfigurar sua senha. </td>
        </tr>
       </tbody>
    </table></dd>
  <dt> Verificação </dt>
    <dd> É possível solicitar que um usuário verifique sua conta via e-mail. Ao solicitar uma verificação, você limita o número de contas falsas que podem se inscrever para seu app. É possível restringir o acesso ao seu app até que um usuário verifique seu e-mail ou o use como uma maneira de gerenciar para quais usuários você cria perfis.
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> Parâmetros da mensagem de verificação </th>
      </thead>
      <tbody>
        <tr>
          <td> %{linkExpiration.hours} </td>
          <td> Exibe o número de horas em que o link é válido. </td>
        </tr>
        <tr>
          <td> %{linkExpiration.minutes} </td>
          <td> Exibe o número de minutos em que o link é válido. </td>
        </tr>
        <tr>
          <td> %{verify.code} </td>
          <td> Exibe uma URL de verificação descartável. </td>
        </tr>
        <tr>
          <td> %{verify.link} </td>
          <td> Exibe a URL de ação que você especificou nas configurações. </td>
        </tr>
      </tbody>
    </table></dd>
  <dt> Mudança de senha </dt>
    <dd> É possível informar um usuário quando a senha é atualizada. Isso é útil caso você não tenha solicitado a mudança de senha. Eles podem tomar as medidas adequadas para reafirmar sua conta.

    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> Parâmetros de mudança de senha </th>
      </thead>
      <tbody>
        <tr>
          <td> %{passwordChangeInfo.time} </td>
          <td> Exibe a hora em que uma nova senha entrou em vigor. </td>
        </tr>
        <tr>
          <td> %{passwordChangeInfo.ipAddress} </td>
          <td> Exibe o endereço IP do qual a mudança de senha foi solicitada. </td>
        </tr>
      </tbody>
    </table></dd>
</dl>



## Gerenciando o Cloud Directory com o SDK Android
{: #managing-android}

Certifique-se de configurar o **Provedor de identidade Cloud Directory** para **ATIVADO** ao usar as seguintes APIs.

### Efetue login usando a Senha do proprietário do recurso
É possível obter um token de acesso e de ID fornecendo o nome de usuário e a senha do usuário final.

 ```java
 AppID.getInstance().obtainTokensWithROP(getApplicationContext(), username, password,
         new TokenResponseListener() {
         @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
             //Exception occurred
      }

          @Override
        public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
            //User authenticated
        }
         });
 ```
 {: codeblock}

### Inscrever

Certifique-se de configurar **Permitir que os usuários se inscrevam e reconfigurem suas senhas** como **ATIVADO** nas configurações para o diretório da nuvem.

 Use a classe LoginWidget para iniciar o fluxo de inscrição.
 ```java
 LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
 loginWidget.launchSignUp(this, new AuthorizationListener() {
			 @Override
		public void onAuthorizationFailure(AuthorizationException exception) {
				 //Exception occurred
		}

			 @Override
        public void onAuthorizationCanceled () {
				 //Sign up canceled by the user
			 }

			 @Override
		public void onAuthorizationSuccess(AccessToken accessToken, IdentityToken identityToken) {
				 if (accessToken != null && identityToken != null) {
				     //User authenticated
				 } else {
				     //email verification is required
				 }

			 }
		 });
 ```
 {: codeblock}

### Esqueceu a senha
Certifique-se de configurar **Permitir que os usuários se inscrevam e reconfigurem sua senha** e **Esqueceu a senha de e-mail** para **ATIVADO** nas configurações do Cloud Directory.

Use a classe LoginWidget para iniciar o fluxo Esqueci a senha.
  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launchForgotPassword(this, new AuthorizationListener() {
 			 @Override
		public void onAuthorizationFailure(AuthorizationException exception) {
 				 //Exception occurred
		}

 			 @Override
        public void onAuthorizationCanceled () {
 				 //forogt password canceled by the user
 			 }

 			 @Override
		public void onAuthorizationSuccess(AccessToken accessToken, IdentityToken identityToken) {
 				 //forgot password finished, in this case accessToken and identityToken will be null.

 			 }
 		 });
  ```
  {: codeblock}

### Mudar detalhes
Certifique-se de configurar **Permitir que os usuários se inscrevam e reconfigurem sua senha** para **ATIVADO** nas configurações do Cloud Directory.Use a classe LoginWidget para iniciar o fluxo de detalhes de mudança. Essa API pode ser usada somente quando o usuário efetua login usando o diretório da nuvem como seu provedor de identidade.
   ```java
   LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
   loginWidget.launchChangeDetails(this, new AuthorizationListener() {
  			 @Override
		public void onAuthorizationFailure(AuthorizationException exception) {
  				 //Exception occurred
		}

  			 @Override
        public void onAuthorizationCanceled () {
  				 //changed details canceled by the user
  			 }

  			 @Override
		public void onAuthorizationSuccess(AccessToken accessToken, IdentityToken identityToken) {
  				 //User authenticated, and fresh tokens received 			 }
  		 });
   ```
   {: codeblock}

### Mudar senha
Certifique-se de configurar **Permitir que os usuários se inscrevam e reconfigurem suas senhas** como **ATIVADO** nas configurações para o diretório da nuvem.

Use a classe LoginWidget para iniciar o fluxo de mudança de senha. Essa API pode ser usada apenas quando o usuário efetua login usando o Cloud Directory como seu provedor de identidade.

   ```java
    LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
    loginWidget.launchChangePassword(this, new AuthorizationListener() {
   			 @Override
		public void onAuthorizationFailure(AuthorizationException exception) {
   				 //Exception occurred
		}

   			 @Override
        public void onAuthorizationCanceled () {
   				 //change password canceled by the user
   			 }

   			 @Override
		public void onAuthorizationSuccess(AccessToken accessToken, IdentityToken identityToken) {
   				   //User authenticated, and fresh tokens received 			 }
   		 });
   ```
   {: codeblock}

## Gerenciando o Cloud Directory com o SDK Swift do iOS


### Efetue login usando a Senha do proprietário do recurso

É possível obter um token de acesso e de ID fornecendo o nome de usuário e a senha do usuário final.
  ```swift
  class delegate : TokenResponseDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
      //User authenticated
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
      //Exception occurred
      }
  }

  AppID.sharedInstance.obtainTokensWithROP(username: username, password: password, delegate: delegate())
  ```
  {: codeblock}

### Inscrever

Certifique-se de configurar **Permitir que os usuários se inscrevam e reconfigurem suas senhas** como **ATIVADO** nas configurações para o diretório da nuvem.

Use a classe LoginWidget para iniciar o fluxo de inscrição.
  ```swift
  class delegate : AuthorizationDelegate {
    public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
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
  {: codeblock}

### Esqueceu a senha
Certifique-se de configurar **Permitir que os usuários se inscrevam e reconfigurem sua senha** e **Esqueceu a senha de e-mail** para **ATIVADO** nas configurações do Cloud Directory.

Use a classe LoginWidget para iniciar o fluxo Esqueci a senha.
  ```swift
  class delegate : AuthorizationDelegate {
     public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
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
  {: codeblock}

### Mudar detalhes

Certifique-se de configurar **Permitir que os usuários se inscrevam e reconfigurem suas senhas** como **ATIVADO** nas configurações para o diretório da nuvem.

Use a classe LoginWidget para iniciar o fluxo de detalhes de mudança. Essa API pode ser usada somente quando o usuário efetua login usando o diretório da nuvem como seu provedor de identidade.
  ```swift

   class delegate : AuthorizationDelegate {
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
          //User authenticated, and fresh tokens received } public func onAuthorizationCanceled() {
           //changed details canceled by the user
       }

       public func onAuthorizationFailure(error: AuthorizationError) {
           //Exception occurred
      }
   }

   AppID.sharedInstance.loginWidget?.launchChangeDetails(delegate: delegate())
  ```
  {: codeblock}

### Mudar senha

Certifique-se de configurar **Permitir que os usuários se inscrevam e reconfigurem suas senhas** como **ATIVADO** nas configurações para o diretório da nuvem.

Use a classe LoginWidget para iniciar o fluxo de mudança de senha. Essa API pode ser usada apenas quando o usuário efetua login usando o Cloud Directory como um provedor de identidade.
  ```swift
   class delegate : AuthorizationDelegate {
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
           //User authenticated, and fresh tokens received } public func onAuthorizationCanceled() {
           //change password canceled by the user
       }

       public func onAuthorizationFailure(error: AuthorizationError) {
            //Exception occurred
      }
    }

    AppID.sharedInstance.loginWidget?.launchChangePassword(delegate: delegate())
  ```
  {: codeblock}


## Gerenciando o Cloud Directory com o SDK Node.js
Certifique-se de que o provedor de identidade Cloud Directory seja configurado como **ATIVADO** e inclua o terminal de retorno de chamada.

### Efetue login usando o fluxo da senha do proprietário do recurso
WebAppStrategy permite que os usuários efetuem login em seu aplicativo da web usando um nome de usuário e uma senha.
Após um login bem-sucedido, o token de acesso do usuário é persistido na sessão HTTP e está disponível, desde que a sessão HTTP seja mantida ativa. Quando a sessão HTTP é destruída ou expirada o token é destruído também.

Para permitir que o usuário efetue login usando um nome de usuário e uma senha, inclua em seu app uma rota de postagem que será chamada com os parâmetros de nome de usuário e senha.

  ```javascript
  app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true // allow flash messages
  }));
  ```
  {: codeblock}

  <table>
    <thead>
      <th colspan=2><img src="images/idea.png"/> Entendendo esses componentes de comando </th>
    </thead>
    <tbody>
      <tr>
        <td><code> successRedirect </code></td>
        <td> Configure esse valor para a URL para a qual você deseja redirecionar um usuário após a autenticação bem-sucedida. O padrão é a URL de solicitação original. Exemplo: <code>/form/submit</code> </td>
      </tr>
      <tr>
        <td><code> failureRedirect </code></td>
        <td> Configure esse valor para a URL para a qual você deseja redirecionar um usuário se sua autenticação falhar. O padrão é a URL de solicitação original.</td>
      </tr>
      <tr>
        <td><code> failureFlash </code></td>
        <td> Configure esse valor para <code>true</code> para receber uma mensagem de erro que é retornada do Cloud Directory. O valor padrão é false </td>
      </tr>
     </tbody>
  </table>


**Nota**:
  * Se você enviar a solicitação utilizando um formulário HTML, utilize o middleware [body-parser](https://www.npmjs.com/package/body-parser).
  * Use [connect-flash](https://www.npmjs.com/package/connect-flash) para obter a mensagem de erro retornada. Consulte o `web-app-sample-server.js`.

### Inscrever
Para ativar o formulário de inscrição do {{site.data.keyword.appid_short_notm}}, passe a propriedade "show" do WebAppStrategy e configure-a como `WebAppStrategy.SIGN_UP`.
  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: codeblock}

    **Nota**:
    * Se, em suas configurações de diretório da nuvem, **Permitir que os usuários se conectem sem verificação de e-mail** está configurado como **Não**, o processo termina sem recuperar o acesso e os tokens de ID do {{site.data.keyword.appid_short_notm}}.
    * Certifique-se de configurar **Permitir que os usuários se inscrevam e reconfigurem suas senhas** para **ATIVADO** nas configurações do diretório da nuvem.


### Esqueceu a senha
Para ativar o formulário de senha esqucida do {{site.data.keyword.appid_short_notm}}, passe a propriedade `show` do WebAppStrategy e configure-a como `WebAppStrategy.FORGOT_PASSWORD`.
  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: codeblock}

**Nota**:
* Se, em suas configurações de diretório da nuvem, **Permitir que os usuários se conectem sem verificação de e-mail** está configurado como **Não**, o processo termina sem recuperar o acesso e os tokens de ID do {{site.data.keyword.appid_short_notm}}.
* Certifique-se de configurar **Permitir que usuários se inscrevam e reconfigurem sua senha** e **Esqueceu a senha de e-mail** para **ATIVADO** nas configurações do Cloud Directory.

### Mudar detalhes
Para ativar o formulário de detalhes de mudança do {{site.data.keyword.appid_short_notm}}, passe a propriedade `show` do WebAppStrategy e configure-a como `WebAppStrategy.CHANGE_DETAILS`.
  ```javascript
  app.get("/change_details", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_DETAILS
  }));
  ```
  {: codeblock}

**Nota**:
* Um usuário deve ser autenticado usando o diretório da nuvem como o provedor de identidade.
* Certifique-se de configurar **Permitir que os usuários se inscrevam e reconfigurem suas senhas** para **ATIVADO** nas configurações do diretório da nuvem.


### Mudar senha
Para ativar o formulário de senha de mudança do {{site.data.keyword.appid_short_notm}}, passe a propriedade `show` do WebAppStrategy e configure-a como `WebAppStrategy.CHANGE_PASSWORD`.
  ```javascript
  app.get("/change_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_PASSWORD
  }));
  ```
  {: codeblock}

**Nota**:
* Um usuário deve ser autenticado usando o diretório da nuvem como o provedor de identidade.
* Certifique-se de configurar **Permitir que os usuários se inscrevam e reconfigurem suas senhas** para **ATIVADO** nas configurações do diretório da nuvem.
