---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:tip: .tip}

# Identificando a experiência de conexão com a marca 
{: #branding}

É possível exibir suas próprias telas customizadas e aproveitar os recursos de autenticação e autorização do {{site.data.keyword.appid_full}}. Com o diretório da nuvem como seu provedor de identidade, os usuários são capazes de interagir com seu app com menos ajuda de você. Eles poderão se conectar sem pedir ajuda.
{: shortdesc}

Quando você usa suas próprias telas, o [Fluxo de credenciais de senha do proprietário do recurso](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html) é usado para fornecer tokens de acesso e de identidade.


## Exibindo telas customizadas com o SDK Android
{: #branded-ui-android}

Com o diretório da nuvem ativado, é possível chamar telas customizadas com o SDK Android.  <a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="blank">Veja este blog! <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>
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
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
            //User authenticated
        }
         });
  ```
  {: pre}

</br>
</br>

## Exibindo telas customizadas com o SDK iOS Swift
{: #branded-ui-ios-swift}

Com o diretório da nuvem ativado, é possível chamar telas customizadas com o SDK iOS Swift. 
{: shortdesc}

</br>
**Conectar**

1. Na guia de provedor de identidade na GUI, configure o diretório da nuvem para **Ligado**.
2. Efetue login usando a senha do proprietário do recurso. Tokens de acesso e identidade são obtidos quando um usuário tenta efetuar login usando seu nome de usuário e senha.
  ```swift
  class delegate : TokenResponseDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
      //User authenticated
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
      //Exception occurred
      }
  }

  AppID.sharedInstance.obtainTokensWithROP(username: username, password: password, delegate: delegate())
  ```
  {: pre}


</br>
</br>

## Exibindo telas customizadas com o SDK Node.js
{: #branded-ui-nodejs}

Com o diretório da nuvem ativado, é possível chamar telas customizadas com o SDK Node.js. 
{: shortdesc}

**Conectar**
1. Configure o diretório da nuvem para **Ligado** em suas configurações de provedor de identidade e especifique um terminal de retorno de chamada.
2. Inclua uma rota de post para seu app que possa ser chamada com os parâmetros de nome do usuário e senha e efetue login usando a senha do proprietário do recurso.
    ```javascript
    app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
    	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true // allow flash messages
  }));
    ```
    {: pre}
    `WebAppStrategy` permite que os usuários se conectem aos seus aplicativos da web com um nome de usuário e senha. Após um login bem-sucedido, o token de acesso de um usuário é armazenado na sessão HTTP e fica disponível durante a sessão. Quando a sessão HTTP for destruída ou expirar, o token será invalidado.
    {: tip}

