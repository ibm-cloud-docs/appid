---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-19"

---

{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:pre: .pre}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# Exibindo o widget de login
{: #login-widget}

O {{site.data.keyword.appid_full}} fornece um widget de login que permite fornecer opções de conexão segura aos seus usuários.
{: shortdesc}

Quando seu aplicativo estiver configurado para usar um provedor de identidade, os visitantes do seu aplicativo serão
direcionados a uma tela de conexão pelo widget de login. Com o widget de login, é possível exibir telas pré-configuradas
para seus fluxos de conexão. Como um bônus, é possível atualizar seu fluxo de conexão a qualquer momento sem
mudar seu código-fonte de nenhuma maneira.

Deseja criar uma experiência que seja exclusiva do seu aplicativo? É possível  [ trazer suas próprias telas ](/docs/services/appid/branded.html)!
{: tip}

## Entendendo o widget de login
{: #understanding}

É possível obter vantagem do {{site.data.keyword.appid_short_notm}}, mesmo sem suas próprias telas de IU,
exibindo o widget de login.
{: shortdesc}

**Qual é o padrão?**

Quando mais de um provedor de identidade é configurado, um usuário é redirecionado para o widget de login ao tentar se
conectar ao aplicativo. Usando o widget de login, os usuários podem escolher o provedor com o qual desejam
verificar sua identidade. Mas, quando apenas um provedor é configurado como **Ativado**, os
visitantes são redirecionados para a tela de autenticação de provedores de identidade.

**Quanta informação o {{site.data.keyword.appid_short_notm}} obtém de um provedor de identidade?**

Ao usar provedores de identidade sociais ou corporativos, o {{site.data.keyword.appid_short_notm}} tem acesso de
leitura aos dados da conta dos usuários. O serviço usa um token e as asserções que são retornados pelo provedor de
identidade para verificar se um usuário é quem eles dizem que são. Como o serviço nunca tem acesso de gravação às informações, os usuários devem passar por seu provedor de identidade escolhido para executar ações, como reconfigurar
a senha. Por exemplo, se um usuário se conectar ao seu aplicativo com o Facebook e, em seguida, desejar mudar sua
senha, ele deverá ir para www.facebook.com para fazer isso.

Quando você usa o [Cloud Directory](/docs/services/appid/cloud-directory.html), o {{site.data.keyword.appid_short_notm}} é o provedor de identidade. O serviço usa seu registro para verificar a
identidade dos usuários. Como o {{site.data.keyword.appid_short_notm}} é o provedor, os usuários podem tirar
vantagem da funcionalidade avançada, como reconfigurar sua senha, diretamente em seu aplicativo.

**Que tipo de telas podem ser exibidas para cada tipo de provedor?**

Verifique a tabela a seguir para ver quais telas podem ser exibidas para cada tipo de provedor de identidade.

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

</br>
</br>

## Customizando o widget de login
{: #customize}

O {{site.data.keyword.appid_short_notm}} fornece uma tela de login padrão que poderá ser chamada se você não tiver suas próprias telas de IU para exibir. É possível customizar a tela para exibir o logotipo e as cores de sua escolha.
{: shortdesc}

Para customizar a tela:

1. Abra o painel
de serviço {{site.data.keyword.appid_short_notm}}.
2. Selecione a seção **Customização de login**. É possível modificar a aparência do widget de login para
que se alinhe com a marca de sua empresa.
3. Faça upload do logotipo da sua empresa selecionando um arquivo PNG ou JPG em seu sistema local. O tamanho da imagem recomendado é 320 x 320 pixels. O tamanho máximo do arquivo é 100 Kb.
4. Selecione uma cor de cabeçalho para o widget no selecionador de cor ou insira o código hexadecimal para outra cor.
5. Inspecione a área de janela de visualização e clique em **Salvar mudanças** quando estiver satisfeito com as suas customizações. Uma mensagem de confirmação será exibida.
6. Em seu navegador, atualize sua página de login para verificar suas mudanças.

Não se esqueça. É possível aproveitar o {{site.data.keyword.appid_short_notm}} com outros idiomas também. Se
você não vir um SDK para o idioma no qual está trabalhando, sempre será possível usar as APIs. Consulte
<a href="https://www.ibm.com/blogs/bluemix/tag/app-id/" target="blank">nossos
blogs<img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.
{: tip}


## Exibindo o widget de login com o SDK do Android
{: #android}

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

**Inscrever**

1. Configure as [definições](cloud-directory.html#cd-settings) do Cloud Directory na GUI. Ambos **Permitir que os usuários se conectem ao seu app** e **Permitir que os usuários gerenciem a sua conta por meio do seu app** devem ser configurados como **Ativado**.
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
  {: pre}

</br>

**Esqueci a senha**

1. Configure as [definições](cloud-directory.html#cd-settings) do Cloud Directory na GUI. **Permitir que os usuários gerenciem a sua conta por meio de seu app** deve ser configurado como **Ativado**.
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

**Detalhes da mudança**

1. Configure as [definições](cloud-directory.html#cd-settings) do Cloud Directory na GUI. Ambos **Permitir que os usuários se conectem ao seu app** e **Permitir que os usuários gerenciem a sua conta por meio do seu app** devem ser configurados como **Ativado**.
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

**Mudar senha**

1. Configure as [definições](cloud-directory.html#cd-settings) do Cloud Directory na GUI. Ambos **Permitir que os usuários se conectem ao seu app** e **Permitir que os usuários gerenciem a sua conta por meio do seu app** devem ser configurados como **Ativado**.
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


</br>
</br>

## Exibindo o widget de login com o SDK do iOS Swift
{: #ios-swift}

É possível chamar telas pré-configuradas com o [SDK do cliente iOS Swift](https://github.com/ibm-cloud-security/appid-clientsdk-swift).
{: shortdesc}

Coloque o comando a seguir em seu código.

  ```swift
  import BluemixAppID
  class delegate : AuthorizationDelegate {
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

**Inscrever**

1. Configure as [definições](cloud-directory.html#cd-settings) do Cloud Directory na GUI. Ambos **Permitir que os usuários se conectem ao seu app** e **Permitir que os usuários gerenciem a sua conta por meio do seu app** devem ser configurados como **Ativado**.
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

**Esqueci a senha**

1. Configure as [definições](cloud-directory.html#cd-settings) do Cloud Directory na GUI. **Permitir que os usuários gerenciem a sua conta por meio de seu app** deve ser configurado como **Ativado**.
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

**Detalhes da mudança**

1. Configure as [definições](cloud-directory.html#cd-settings) do Cloud Directory na GUI. Ambos **Permitir que os usuários se conectem ao seu app** e **Permitir que os usuários gerenciem a sua conta por meio do seu app** devem ser configurados como **Ativado**.
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

**Mudar senha**

1. Configure as [definições](cloud-directory.html#cd-settings) do Cloud Directory na GUI. Ambos **Permitir que os usuários se conectem ao seu app** e **Permitir que os usuários gerenciem a sua conta por meio do seu app** devem ser configurados como **Ativado**.
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

</br>
</br>

## Exibindo o widget de login com o SDK do Node.js
{: #nodejs}

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

**Inscrever**

1. Configure as [definições](cloud-directory.html#cd-settings) do Cloud Directory na GUI. Ambos **Permitir que os usuários se conectem ao seu app** e **Permitir que os usuários gerenciem a sua conta por meio do seu app** devem ser configurados como **Ativado**.
2. Coloque o código a seguir em seu aplicativo. Quando um usuário tentar se conectar com o seu aplicativo, o widget de login será chamado e exibirá a sua página de conexão customizada.

  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: codeblock}

</br>

**Esqueci a senha**

1. Configure as [definições](cloud-directory.html#cd-settings) do Cloud Directory na GUI. **Permitir que os usuários gerenciem a sua conta por meio de seu app** deve ser configurado como **Ativado**.
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

**Detalhes da mudança**

1. Configure as [definições](cloud-directory.html#cd-settings) do Cloud Directory na GUI. Ambos **Permitir que os usuários se conectem ao seu app** e **Permitir que os usuários gerenciem a sua conta por meio do seu app** devem ser configurados como **Ativado**.
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

**Mudar senha**

1. Configure as [definições](cloud-directory.html#cd-settings) do Cloud Directory na GUI. Ambos **Permitir que os usuários se conectem ao seu app** e **Permitir que os usuários gerenciem a sua conta por meio do seu app** devem ser configurados como **Ativado**.
2. Na guia **Senha mudada** do painel de serviço, configure **E-mail mudado por senha** como
3. Coloque o código a seguir em seu aplicativo para passar a propriedade *show* para `WebAppStrategy.FORGOT_PASSWORD` para ativar o formulário de detalhes de mudança.

  ```javascript
  app.get("/change_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_PASSWORD
  }));
  ```
  {: codeblock}

</br>
