---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Marcando a experiência de conexão
{: #branding}

É possível exibir suas próprias UIs customizadas enquanto aproveita os recursos de autenticação e autorização do {{site.data.keyword.appid_full}}. Com o diretório da nuvem como seu provedor de identidade, os usuários são capazes de interagir com seu app com menos ajuda de você. Eles são capazes de conectar-se, inscrever-se, mudar a senha e muito mais, sem pedir ajuda.
{: shortdesc}

Com o diretório da nuvem como seu provedor de identidade, o [Fluxo de credenciais de senha do proprietário do recurso](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html) é usado para fornecer tokens de acesso e de identidade.

**Nota**: você só é capaz de trazer páginas de conexão customizada quando o diretório da nuvem é a única opção configurada. Se você tem outros provedores de identidade configurados para **ligado**, a tela de conexão pré-configurada é exibida.

## Exibindo telas customizadas com o SDK Android
{: #branded-ui-android}

Com o diretório da nuvem ativado, é possível chamar telas customizadas com o SDK Android. É possível escolher a combinação das telas com as quais você gostaria que seus usuários fossem capazes de interagir. <a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="blank">Consulte o nosso blog! <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>
{: shortdesc}

</br>
**Conectar**

1. Configure **Diretório da nuvem** para **Ligado** como um provedor de identidade.
2. Coloque o comando a seguir em seu código.
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
		public void onAuthorizationSuccess(AccessToken accessToken, IdentityToken identityToken) {
  			 if (accessToken != null && identityToken != null) {
  			 } else {
  			 }

  		 }
  	 });
  ```
  {: codeblock}

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

   			 @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
          }
   		 });
    ```
    {: codeblock}

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

  			 @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
          }
  		 });
   ```
   {: codeblock}

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

   			 @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
          }
   		 });
   ```
   {: codeblock}

</br>
</br>

## Exibindo telas customizadas com o SDK iOS Swift
{: #branded-ui-ios-swift}

Com o diretório da nuvem ativado, é possível chamar telas customizadas com o SDK iOS Swift. É possível escolher a combinação das telas com as quais você gostaria que seus usuários fossem capazes de interagir.
{: shortdesc}

</br>
**Conectar**

1. Na guia de provedor de identidade na GUI, configure o diretório da nuvem para **Ligado**.
2. Efetue login usando a senha do proprietário do recurso. É possível obter um token de acesso e de ID fornecendo o nome de usuário e a senha do usuário final.
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

</br>
**Inscrever**

1. Configure **Permitir que os usuários se inscrevam e reconfigurem sua senha** para **Ligado**, nas configurações para o diretório da nuvem.
2. Chame o LoginWidget para iniciar o fluxo de inscrição.
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

</br>
**Esqueci a senha**

1. Configure **Permitir que os usuários se inscrevam e reconfigurem sua senha** e **E-mail de Esqueci a senha** para **Ligado** nas configurações para o diretório da nuvem.
2. Chame o LoginWidget para iniciar o fluxo Esqueci a senha.
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

</br>
**Detalhes da conta**

1. Configure **Permitir que os usuários se inscrevam e reconfigurem sua senha** para **Ligado** nas configurações para o diretório da nuvem.
2. Chame o LoginWidget para iniciar o fluxo de detalhes de mudança.
  ```swift

   class delegate : AuthorizationDelegate {
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
       }

       public func onAuthorizationCanceled() {
     }

       public func onAuthorizationFailure(error: AuthorizationError) {
     }
   }

   AppID.sharedInstance.loginWidget?.launchChangeDetails(delegate: delegate())
  ```
  {: codeblock}

</br>
**Mudar senha**

1. Configure **Permitir que os usuários se inscrevam e reconfigurem sua senha** para **Ligado** nas configurações para o diretório da nuvem.
2. Chame o LoginWidget para iniciar o fluxo de mudança de senha.
  ```swift
   class delegate : AuthorizationDelegate {
       public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
       }

       public func onAuthorizationCanceled() {
     }

       public func onAuthorizationFailure(error: AuthorizationError) {
     }
    }

    AppID.sharedInstance.loginWidget?.launchChangePassword(delegate: delegate())
  ```
  {: codeblock}

</br>

## Exibindo telas customizadas com o SDK Node.js
{: #branded-ui-nodejs}

Com o diretório da nuvem ativado, é possível chamar telas customizadas com o SDK Node.js. É possível escolher a combinação das telas com as quais você gostaria que seus usuários fossem capazes de interagir.
{: shortdesc}

**Conectar**
1. Configure o diretório da nuvem para **Ligado** em suas configurações de provedor de identidade e especifique um terminal de retorno de chamada.
2. Inclua uma rota de post para seu app que possa ser chamada com os parâmetros de nome do usuário e senha e efetue login usando a senha do proprietário do recurso.
    **Nota**: `WebAppStrategy` permite que os usuários efetuem login em seu apps da web com um nome do usuário e senha. Após o login bem-sucedido, o token de acesso de um usuário é armazenado na sessão HTTP e está disponível para a duração da sessão. Assim que a sessão HTTP for destruída ou tiver expirado, o token não será mais válido.
    ```javascript
    app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
    	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true // allow flash messages
  }));
    ```
    {: codeblock}

</br>
**Inscrever**

1. Configure **Permitir que os usuários se inscrevam e reconfigurem sua senha** para **Ligado** nas configurações do diretório da nuvem. Se isso for configurado para não, o processo terminará sem recuperar tokens de acesso e de identidade.
2. Passe a propriedade de WebAppStrategy `show` e configure-a para `WebAppStrategy.SIGN_UP`.
  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: codeblock}

</br>
**Esqueci a senha**

1. Configure **Permitir que os usuários se inscrevam e reconfigurem sua senha** e **E-mail de Esqueci a senha** para **LIGADO** nas configurações do diretório da nuvem. Se isso for configurado para não, o processo terminará sem recuperar tokens de acesso e de identidade.
2. Passe a propriedade de WebAppStrategy `show` e configure-a para `WebAppStrategy.FORGOT_PASSWORD`.
  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: codeblock}

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
  {: codeblock}

</br>
**Mudar senha**
1. Configure **Permitir que os usuários se inscrevam e reconfigurem sua senha** para **Ligado** nas configurações do diretório da nuvem. 
2. Passe a propriedade de WebAppStrategy `show` e configurá-a para `WebAppStrategy.CHANGE_PASSWORD`.
  ```javascript
  app.get("/change_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_PASSWORD
  }));
  ```
  {: codeblock}
