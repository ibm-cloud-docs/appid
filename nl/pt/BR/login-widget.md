---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-06"

keywords: Authentication, authorization, identity, app security, secure, development, sign in, sign up, password, social, enterprise

subcollection: appid

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}


# Usando o Widget de login
{: #login-widget}

Com o {{site.data.keyword.appid_full}}, é possível usar uma IU padrão, chamada de Widget de login, para permitir que os usuários do aplicativo escolham o provedor de identidade ao qual desejam se conectar. Se você estiver usando o Cloud Directory, o Widget de login também fornecerá IUs adicionais para funcionalidades extras, como inscrever-se, esquecer a senha, autenticação de diversos fatores e mais.
{: shortdesc}


## Entendendo o widget de login
{: #widget-understanding}

Uma das melhores partes do Widget de login é que você pode iniciar usando o {{site.data.keyword.appid_short_notm}} antes de implementar qualquer uma de suas próprias IUs de autenticação, o que torna a experiência de integração do desenvolvedor muito mais fácil.

### Qual é o comportamento padrão do Widget de login?
{: #widget-default}

Por padrão, o Widget de login é ativado para usar o Facebook, o Google e o Cloud Directory. É possível mudar o comportamento a qualquer momento escolhendo quais provedores de identidade você deseja configurar como uma opção. Quando mais de um provedor de identidade é ativado, o Widget de login apresenta uma tela na qual o usuário pode fazer sua seleção de provedor de identidade. Mas, se você tiver um único provedor ativado, os usuários não verão a tela de seleção supramencionada. Eles serão levados diretamente para o provedor de identidade para iniciar o processo de conexão.

Por exemplo, se você estiver usando o padrão, Facebook, Google e Cloud Directory, os usuários verão a tela. Se você ativar apenas o Facebook, os usuários serão levados diretamente para o Facebook para autenticação.



### Quais telas podem ser exibidas para cada provedor?
{: #widget-options}

Quando você usa o Cloud Directory, o {{site.data.keyword.appid_short_notm}} é capaz de fornecer a funcionalidade estendida de gerenciamento de usuário. A funcionalidade estendida também se aplica aos recursos de Widgets de login. Os usuários armazenados no Cloud Directory podem aproveitar a funcionalidade, como inscrever-se ou reconfigurar sua senha, diretamente no Widget de login. Verifique a tabela a seguir para ver quais telas podem ser exibidas para cada tipo de provedor de identidade.

<table>
  <thead>
    <tr>
      <th>Tela do widget de login</th>
      <th>Provedor de identidade social</th>
      <th>Provedor de identidade corporativa</th>
      <th>Cloud Directory</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Conectar</td>
      <td><img src="images/confirm.png" width="32" alt="Recurso Disponível" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="Recurso Disponível" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="Recurso Disponível" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Inscrever</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Recurso Disponível" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Senha esquecida</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Recurso Disponível" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Mudar senha</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Recurso Disponível" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Detalhes da conta</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Recurso Disponível" style="width:32px;" /></td>
    </tr>
  </tbody>
</table>


## Customizando o widget de login
{: #widget-customize}

O Widget de Login é dinâmico. É possível customizar a aparência ou a configuração do provedor de identidade e as mudanças são aplicadas imediatamente. Não é necessário atualizar seu código do aplicativo nem reimplementar seu app de nenhuma maneira.
{: shortdesc}

Você precisa de mais customização do que o Widget de login fornece? É possível implementar sua própria IU totalmente customizada para conexão, inscrição, reconfiguração de senha do usuário e outros fluxos para criar uma experiência que seja exclusiva para seu app. Para iniciar, verifique [marcando seu app](/docs/services/appid?topic=appid-branded).
{: tip}

Para customizar a tela:

1. Abra o painel
de serviço {{site.data.keyword.appid_short_notm}}.
2. Selecione a seção **Customização de login**. É possível modificar a aparência do widget de login para
que se alinhe com a marca de sua empresa.
3. Faça upload do logotipo da sua empresa selecionando um arquivo PNG ou JPG em seu sistema local. O tamanho da imagem recomendado é 320 x 320 pixels. O tamanho máximo do arquivo é 100 Kb.
4. Selecione uma cor de cabeçalho para o widget no selecionador de cor ou insira o código hexadecimal para outra cor.
5. Inspecione a área de janela de visualização e clique em **Salvar mudanças** quando estiver satisfeito com as suas customizações. Uma mensagem de confirmação será exibida.
6. Em seu navegador, atualize sua página de login para verificar suas mudanças.


## Exibindo o widget de login com o SDK do Android
{: #widget-display-android}

É possível chamar telas pré-configuradas com o [SDK do cliente Android](https://github.com/ibm-cloud-security/appid-clientsdk-android).
{: shortdesc}

Coloque o comando a seguir em seu código.

  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launch(this, new AuthorizationListener() {
        @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //Exception occurred
        }

        @Override
        public void onAuthorizationCanceled () {
          //Authentication canceled by the user
        }

        @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
          //User authenticated
        }
      });
  ```
{: codeblock}

</br>

### Inscrever
{: #widget-android-signup}

1. Configure as [definições](/docs/services/appid?topic=appid-cloud-directory#cd-settings) do Cloud Directory na GUI. Ambos **Permitir que os usuários se conectem ao seu app** e **Permitir que os usuários gerenciem a sua conta por meio do seu app** devem ser configurados como **Ativado**.
2. Inclua o código a seguir em seu app. Quando um usuário se inscreve para o aplicativo por meio da tela customizada, o
fluxo de inscrição é iniciado. A chamada a seguir não apenas registra o usuário, como também pode enviar um e-mail de
verificação para concluir o registro, dependendo das configurações do Cloud Directory.

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
  {: codeblock}

</br>

### Senha esquecida
{: #widget-android-forgot-password}

1. Configure as [definições](/docs/services/appid?topic=appid-cloud-directory#cd-settings) do Cloud Directory na GUI. **Permitir que os usuários gerenciem a sua conta por meio de seu app** deve ser configurado como **Ativado**.
2. Na guia **Reconfigurar senha** do painel de serviço, certifique-se de que **E-mail de senha esquecida** esteja configurado como **Ativado**.
3. Inclua o código a seguir em seu app. Quando um usuário clica em "esqueci a senha" no aplicativo, o SDK chama a API
forgot_password para enviar um e-mail ao usuário que permite a ele reconfigurar sua senha.

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
  {: codeblock}

</br>

### Mudar detalhes
{: #widget-android-change-details}

1. Configure as [definições](/docs/services/appid?topic=appid-cloud-directory#cd-settings) do Cloud Directory na GUI. Ambos **Permitir que os usuários se conectem ao seu app** e **Permitir que os usuários gerenciem a sua conta por meio do seu app** devem ser configurados como **Ativado**.
2. Na guia **Senha mudada** do painel de serviço, configure **E-mail mudado por senha** como
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
  {: codeblock}

</br>

### Mudar senha
{: #widget-android-change-password}

1. Configure as [definições](/docs/services/appid?topic=appid-cloud-directory#cd-settings) do Cloud Directory na GUI. Ambos **Permitir que os usuários se conectem ao seu app** e **Permitir que os usuários gerenciem a sua conta por meio do seu app** devem ser configurados como **Ativado**.
2. Coloque o código a seguir em seu app para iniciar o fluxo de mudança de senha.

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
  {: codeblock}



## Exibindo o widget de login com o SDK do iOS Swift
{: #widget-display-ios-swift}

É possível chamar telas pré-configuradas com o [SDK do cliente iOS Swift](https://github.com/ibm-cloud-security/appid-clientsdk-swift).
{: shortdesc}

Coloque o comando a seguir em seu código.

  ```swift
  importar IBMCloudAppID
  delegado de classe: AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, refreshToken: RefreshToken?) {
          //User authenticated
      }

      public func onAuthorizationCanceled() {
          //Authentication canceled by the user
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          //Exception occurred
      }
  }

  AppID.sharedInstance.loginWidget?.launch(delegate: delegate())
  ```
  {: codeblock}

</br>

### Inscrever
{: #widget-ios-signup}

1. Configure as [definições](/docs/services/appid?topic=appid-cloud-directory#cd-settings) do Cloud Directory na GUI. Ambos **Permitir que os usuários se conectem ao seu app** e **Permitir que os usuários gerenciem a sua conta por meio do seu app** devem ser configurados como **Ativado**.
2. Coloque o código a seguir em seu aplicativo. Quando um usuário tentar se conectar com o seu aplicativo, o widget de login será chamado e exibirá a sua página de conexão customizada.

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
  {: codeblock}

</br>

### Senha esquecida
{: #widget-ios-forgot-password}

1. Configure as [definições](/docs/services/appid?topic=appid-cloud-directory#cd-settings) do Cloud Directory na GUI. **Permitir que os usuários gerenciem a sua conta por meio de seu app** deve ser configurado como **Ativado**.
2. Na guia **Reconfigurar senha** do painel de serviço, certifique-se de que **E-mail de senha esquecida** esteja configurado como **Ativado**.
3. Coloque o código a seguir em seu aplicativo. Quando um de seus usuários do aplicativo solicita que sua senha seja
atualizada, o widget de login é chamado e o processo é iniciado.

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
  {: codeblock}

</br>

### Mudar detalhes
{: #widget-ios-change-details}

1. Configure as [definições](/docs/services/appid?topic=appid-cloud-directory#cd-settings) do Cloud Directory na GUI. Ambos **Permitir que os usuários se conectem ao seu app** e **Permitir que os usuários gerenciem a sua conta por meio do seu app** devem ser configurados como **Ativado**.
2. Na guia **Senha mudada** do painel de serviço, configure **E-mail mudado por senha** como
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
  {: codeblock}

</br>

### Mudar senha
{: #widget-ios-change-password}

1. Configure as [definições](/docs/services/appid?topic=appid-cloud-directory#cd-settings) do Cloud Directory na GUI. Ambos **Permitir que os usuários se conectem ao seu app** e **Permitir que os usuários gerenciem a sua conta por meio do seu app** devem ser configurados como **Ativado**.
2. Coloque o código a seguir em seu app para iniciar o fluxo de mudança de senha.

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
  {: codeblock}


## Exibindo o widget de login com o SDK do Node.js
{: #widget-display-nodejs}

É possível chamar telas pré-configuradas com o [SDK do servidor Node.js](https://github.com/ibm-cloud-security/appid-serversdk-nodejs).
{: shortdesc}

Inclua uma rota de post para seu app que possa ser chamada com os parâmetros de nome do usuário e senha e efetue login usando a senha do proprietário do recurso.

  ```javascript
  app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true // allow flash messages
  }));
  ```
  {: codeblock}

`WebAppStrategy` permite que os usuários se conectem aos seus aplicativos da web com um nome de usuário e senha. Após um login bem-sucedido, o token de acesso de um usuário é armazenado na sessão HTTP e fica disponível durante a sessão. Após a sessão HTTP ser destruída ou expirada, o token é invalidado.
{: tip}

</br>

### Inscrever
{: #widget-nodejs-signup}

1. Configure as [definições](/docs/services/appid?topic=appid-cloud-directory#cd-settings) do Cloud Directory na GUI. Ambos **Permitir que os usuários se conectem ao seu app** e **Permitir que os usuários gerenciem a sua conta por meio do seu app** devem ser configurados como **Ativado**.
2. Coloque o código a seguir em seu aplicativo. Quando um usuário tentar se conectar com o seu aplicativo, o widget de login será chamado e exibirá a sua página de conexão customizada.

  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: codeblock}

</br>

### Senha esquecida
{: #widget-nodejs-forgot-password}

1. Configure as [definições](/docs/services/appid?topic=appid-cloud-directory#cd-settings) do Cloud Directory na GUI. **Permitir que os usuários gerenciem a sua conta por meio de seu app** deve ser configurado como **Ativado**.
2. Na guia **Reconfigurar senha** do painel de serviço, certifique-se de que **E-mail de senha esquecida** esteja configurado como **Ativado**.
3. Coloque o código a seguir em seu aplicativo para passar a propriedade *show* para `WebAppStrategy.FORGOT_PASSWORD`. Quando
um usuário solicita que sua senha para seu aplicativo seja atualizada, o widget de login é chamado e o processo é
iniciado.

  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: codeblock}

</br>

### Mudar detalhes
{: #widget-nodejs-change-details}

1. Configure as [definições](/docs/services/appid?topic=appid-cloud-directory#cd-settings) do Cloud Directory na GUI. Ambos **Permitir que os usuários se conectem ao seu app** e **Permitir que os usuários gerenciem a sua conta por meio do seu app** devem ser configurados como **Ativado**.
2. Na guia **Senha mudada** do painel de serviço, configure **E-mail mudado por senha** como
3. Coloque o código a seguir em seu aplicativo para passar a propriedade *show* para `WebAppStrategy.FORGOT_PASSWORD` para ativar o formulário de detalhes de mudança.

  ```javascript
  app.get("/change_details", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_DETAILS
  }));
  ```
  {: codeblock}

</br>

### Mudar senha
{: #widget-nodejs-change-password}

1. Configure as [definições](/docs/services/appid?topic=appid-cloud-directory#cd-settings) do Cloud Directory na GUI. Ambos **Permitir que os usuários se conectem ao seu app** e **Permitir que os usuários gerenciem a sua conta por meio do seu app** devem ser configurados como **Ativado**.
2. Na guia **Senha mudada** do painel de serviço, configure **E-mail mudado por senha** como
3. Coloque o código a seguir em seu aplicativo para passar a propriedade *show* para `WebAppStrategy.FORGOT_PASSWORD` para ativar o formulário de detalhes de mudança.

  ```javascript
  app.get("/change_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_PASSWORD
  }));
  ```
  {: codeblock}
