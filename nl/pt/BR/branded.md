---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-10"

keywords: Authentication, authorization, identity, app security, secure, customizing apps, directory, registry, 

subcollection: appid

---

{:external: target="_blank" .external}
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

# Marcando seu app
{: #branded}

É possível exibir suas próprias telas customizadas, usar seus próprios fluxos e aproveitar dos recursos de autenticação e autorização do {{site.data.keyword.appid_full}}. Usando o Cloud Directory como seu
provedor de identidade, os usuários conseguem interagir com o seu aplicativo com menos ajuda sua. Eles são capazes de conectar-se, inscrever-se, mudar a senha e muito mais, sem pedir ajuda.
{: shortdesc}


## Entendendo a reutilização de tela
{: #branded-understand}

Quando você reutiliza suas IUs existentes, é possível criar um fluxo de conexão coesa para seu app. Ao usar as mesmas
imagens, cores e marca, seus usuários são mais propensos a reconhecer sua marca, mesmo quando não interagem
diretamente com seu aplicativo.

### Há algum requisito para minhas próprias telas?
{: #branded-requirements}


Para exibir suas próprias IUs, deve-se usar o [Cloud Directory](/docs/services/appid?topic=appid-cloud-directory) como seu provedor de identidade. O Cloud Directory pode ser configurado de várias maneiras diferentes. É possível decidir os tipos de mensagens que você deseja enviar e customizar o conteúdo e o design. Não sabe o que dizer? Não é um problema. Consulte a GUI para obter mensagens de exemplo que podem ser usadas.


Deseja usar um [idioma](/docs/services/appid?topic=appid-cd-messages#cd-languages) diferente do inglês? É possível escolher outro idioma usando as [APIs de gerenciamento de idiomas](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Config/updateLocalization){: external} para exibir seu próprio conteúdo traduzido.
{: tip}




### Posso usar algumas telas próprias e algumas telas padrão?
{: #branded-hybrid}

Sim! É possível criar um fluxo híbrido que usa algumas de suas telas e algumas das telas padrão. No entanto, é possível usar apenas uma opção por fluxo. Como um exemplo, é possível usar a sua própria tela de conexão e também usar a tela de conexão padrão. Mas, se você optar por usar a tela de inscrição padrão, deverá continuar a usar o padrão em todo o fluxo de inscrição, incluindo na verificação de inscrição.

### Como os fluxos se diferenciam tecnicamente?
{: #branded-technically}

O serviço usa os fluxos de concessão OAuth 2.0 para mapear o processo de autorização. Quando você configura os provedores de identidade social, como o Facebook, o [Fluxo de concessão de autorização](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html){: external} é usado para chamar o Widget de login. Quando você usa suas próprias telas, o [fluxo de Credenciais de senha do proprietário do recurso](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html){: external} é usado para fornecer tokens de acesso e identidade que podem ser utilizados para chamar suas telas.



### Exemplos
{: #branded-examples}

Sim! Consulte qualquer um dos exemplos a seguir para ver o Cloud Directory em ação:

* [Usar sua própria IU de marca para a conexão do usuário com o {{site.data.keyword.appid_short_notm}}](https://www.ibm.com/cloud/blog/use-branded-ui-user-sign-app-id){: external}
* [Usar sua própria IU e seus fluxos para inscrição e conexão do usuário com o {{site.data.keyword.appid_short_notm}}](https://www.ibm.com/cloud/blog/use-ui-flows-user-sign-sign-app-id){: external}
* [Usar uma página de login customizada com o {{site.data.keyword.appid_short_notm}}](https://www.ibm.com/cloud/blog/custom-login-page-app-id-integration){: external}


## Inserindo uma marca no aplicativo com o SDK do Android
{: #branded-ui-android}

Com o Cloud Directory ativado, é possível chamar telas customizadas com o SDK do Android. É possível escolher a combinação das telas com as quais você gostaria que seus usuários fossem capazes de interagir. Para obter um exemplo detalhado, [confira este blog](https://www.ibm.com/cloud/blog/use-branded-ui-user-sign-app-id){: external}.
{: shortdesc}



### Conectar
{: #branded-android-sign-in}

1. Configure as [definições](/docs/services/appid?topic=appid-cloud-directory#cd-settings) do Cloud Directory na GUI.
2. Inclua o código a seguir no aplicativo. O fluxo de conexão é acionado quando um usuário clica em se conectar em sua tela customizada. Você obtém tokens de acesso, identidade e atualização fornecendo o nome de usuário e a senha do usuário.

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
  {: codeblock}

</br>
</br>

## Inserindo uma marca no aplicativo com o SDK do iOS Swift
{: #branded-ui-ios-swift}

Com o Cloud Directory ativado, é possível chamar suas próprias telas com marca com o [SDK do iOS Swift](https://github.com/ibm-cloud-security/appid-clientsdk-swift){: external}.
{: shortdesc}

</br>

### Conectar
{: #branded-ios-sign-in}

1. Configure as [definições](/docs/services/appid?topic=appid-cloud-directory#cd-settings) do Cloud Directory na GUI.
2. Coloque o código a seguir em seu aplicativo. Quando um usuário tenta se conectar, sua tela customizada é chamada e o processo de autorização e autenticação é iniciado com a sua página de conexão customizada.

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
  {: codeblock}


## Inserindo uma marca no aplicativo com o SDK do Node.js
{: #branding-ui-nodejs}

Com o Cloud Directory ativado, é possível chamar as telas customizadas com o SDK do Node.js.
{: shortdesc}

### Conectar
{: #branded-node-sign-in}

Ao usar `WebAppStrategy`, os usuários podem se conectar aos apps da web com seus nomes de usuário e senhas. Depois que
um usuário se conecta com sucesso ao aplicativo, o token de acesso dele é persistido em uma sessão HTTP, desde que ela seja mantida
ativa. Após a sessão HTTP ser fechada ou expirada, o token de acesso também é destruído.


1. Configure as [definições](/docs/services/appid?topic=appid-cloud-directory#cd-settings) do Cloud Directory na GUI.
2. Coloque o código a seguir em seu aplicativo. Quando um usuário tenta se conectar, sua tela customizada é chamada e o processo de autorização e autenticação é iniciado.

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

**Nota**: se você enviar a solicitação em HTML, será possível usar o middleware [body parser](https://www.npmjs.com/package/body-parser){: external}. Para ver a mensagem de erro retornada, é possível usar [connect-flash](https://www.npmjs.com/package/connect-flash){: external}. Para vê-lo em ação, confira a [amostra de app da web](https://github.com/ibm-cloud-security/appid-serversdk-nodejs/blob/master/samples/web-app-sample.js){: external}.



## Inserindo uma marca no aplicativo com a API
{: #branded-ui-api}

É possível exibir suas próprias telas customizadas e aproveitar os recursos de autenticação e autorização do {{site.data.keyword.appid_short_notm}}. Com o Cloud Directory como o provedor de identidade, os usuários são capazes de interagir com o seu app com menos ajuda sua. Eles são capazes de conectar-se, inscrever-se, reconfigurar suas senhas e muito mais sem pedir ajuda.
{: shortdesc}

Para tornar isso possível, o {{site.data.keyword.appid_short_notm}} expõe as APIs de REST. É possível usar as
APIs de REST para construir um servidor de back-end que atenda a seus aplicativos da web ou para interagir com um
aplicativo móvel com suas próprias telas customizadas.

A API de gerenciamento é protegida com tokens gerados pelo IBM Cloud Identity and Access Management, o que significa que os proprietários da conta podem especificar o nível de acesso para cada instância de serviço de cada um dos integrantes da equipe. Para mais informações sobre como o IAM e o {{site.data.keyword.appid_short_notm}} trabalham juntos, consulte [Gerenciamento de acesso de serviço](/docs/services/appid?topic=appid-service-access-management).

Depois de configurar suas [configurações](/docs/services/appid?topic=appid-cloud-directory#cd-settings), é possível chamar os terminais a seguir para exibir cada tela.

### Inscrever
{: #branded-api-signup}

É possível usar o terminal `/sign_up` para permitir que os usuários se conectem ao seu aplicativo.
Forneça os seguintes dados no corpo da solicitação:
  * Seu tenantID.
  * Dados do usuário do Cloud Directory. Veja [Representação do usuário integral do SCIM](https://tools.ietf.org/html/rfc7643#section-8.2){: external} para obter mais detalhes.
    * Um atributo `password`.
    * Na matriz de e-mail com um atributo `primary` configurado como `true`, deve-se ter pelo menos um endereço de e-mail.

Dependendo da sua [configuração de e-mail](/docs/services/appid?topic=appid-cd-messages), um usuário pode receber uma solicitação para verificação, um e-mail que dá as boas-vindas quando ele se inscreve em seu app ou ambos. Ambos os tipos de e-mails são acionados quando um usuário se inscreve para seu app. O
e-mail de verificação contém um link que o usuário pode clicar para confirmar sua identidade. Uma tela é exibida
agradecendo pela verificação ou confirmando que sua verificação está concluída.  

Para apresentar sua própria página de verificação de postagem:

1. Navegue para o provedor de identidade do Cloud Directory no painel do {site.data.keyword.appid_short_notm}}.
2. Clique na guia **Verificação de e-mail**.
3. Na **URL da página de verificação customizada**, insira a URL para a página inicial.

Quando esse valor for fornecido, o {{site.data.keyword.appid_short_notm}} chamará a URL junto com uma consulta de `context`. Quando você chama o terminal `/sign_up/confirmation_result` e passa o parâmetro `context` recebido, o resultado informa se seu usuário verificou a conta. Se sim, será possível exibir sua página customizada.


### Senha esquecida
{: #branded-api-forgot-password}

É possível usar o terminal `/forgot_password` para permitir que os usuários recuperem suas senhas se as esqueceram.

Forneça os seguintes dados no corpo da solicitação:
  * O seu ID do locatário.
  * O e-mail do usuário do Cloud Directory.

Quando o terminal é chamado, um e-mail de reconfiguração de senha é enviado para o usuário. O e-mail contém um botão **Reconfigurar**. Depois de pressionar o botão, uma tela é exibida pelo {{site.data.keyword.appid_short_notm}} em que é possível reconfigurar a sua senha.

É possível apresentar a sua própria página de reconfiguração de senha de post:

1. Configure as [definições](/docs/services/appid?topic=appid-cloud-directory#cd-settings) do Cloud Directory na GUI. **Permitir que os usuários gerenciem a sua conta por meio de seu app** deve ser configurado como **Ativado**.
2. Na guia **Reconfigurar senha** do painel de serviço, certifique-se de que **E-mail de senha esquecida** esteja configurado como **Ativado**.
3. Insira a URL para a página inicial na **URL para a página de reconfiguração de senha customizada**  

Quando esse valor for fornecido, o {{site.data.keyword.appid_short_notm}} chamará a URL junto com uma consulta de `context`. O parâmetro `context` é usado para receber o resultado quando `/forgot_password/confirmation_result` é chamado. Se o resultado for bem-sucedido, será possível exibir sua página customizada.

Inclua uma sequência aleatória em sua página customizada de reconfiguração de senha e passe-a ao seu backend quando a solicitação for enviada. Deixe o manipulador validar a sequência e chame o terminal `/change_password` somente se ele for válido. Ao fazer isso, é possível reduzir a vulnerabilidade do seu terminal de senha de reconfiguração de back-end.
{: tip}


### Mudar senha
{: #branded-api-change-password}

É possível usar o terminal `/change_password` de duas maneiras. Quando um usuário envia uma solicitação de reconfiguração ou quando um usuário está conectado ao seu app e deseja atualizar sua senha.

Forneça os dados a seguir no corpo da solicitação para atualizar a senha após uma solicitação de reconfiguração:
  * Seu tenantID.
  * A nova senha do usuário.
  * O UUID do usuário do Cloud Directory.
  * Opcional: o endereço IP por meio do qual a reconfiguração de senha foi executada. Se você escolher passar o endereço IP, o item temporário `%{passwordChangeInfo.ipAddress}` estará disponível para o modelo de e-mail de mudança de senha.

Dependendo de sua configuração, quando uma senha é mudada, o {{site.data.keyword.appid_short_notm}} envia um e-mail para o usuário para que ele saiba que uma mudança foi feita.


Para permitir que os usuários mudem suas senhas enquanto conectados a seu app:

Forneça os seguintes dados no corpo da solicitação:
  * Seu tenantID.
  * A nova senha do usuário.
  * O UUID do usuário do Cloud Directory.

Sua página de mudança de senha deve solicitar que o usuário insira sua senha atual e sua nova senha.
{: tip}

Seu backend valida a senha atual do usuário com a API do ROP e, se válida, chama o terminal com a nova senha. Dependendo da sua configuração, quando uma senha mudar, o {{site.data.keyword.appid_short_notm}} poderá enviar um e-mail para informar isso ao usuário.


### Reenviar
{: #branded-api-resend}

É possível usar o `/resend/{templateName}` para reenviar um e-mail quando um usuário não o recebe por algum
motivo.

Forneça os seguintes dados no corpo da solicitação:
  * O tenantID.
  * O nome de modelo
  * O UUID do usuário do Cloud Directory.

### Mudar detalhes
{: #branded-api-change-details}

Quando um usuário está conectado ao seu app, ele pode atualizar algumas das suas informações. É possível usar o `/Users/{userId}` para obter e atualizar suas informações.

Quando os detalhes do usuário são atualizados, o terminal obtém os dados do usuário atualizados no corpo da solicitação no [formato SCIM](https://tools.ietf.org/html/rfc7643#section-8.2){: external}. Certifique-se de que mudar somente os detalhes relevantes.

Seu endereço de e-mail não pode ser mudado.
{: tip}
