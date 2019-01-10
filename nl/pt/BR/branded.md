---

copyright:
  years: 2017, 2018
lastupdated: "2018-10-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:tip: .tip}

# Marcando seu app
{: #branding}

É possível exibir suas próprias telas customizadas, usar seus próprios fluxos de conexão e tirar vantagem das
capacidades de autenticação e autorização do {{site.data.keyword.appid_full}}. Usando o Cloud Directory como seu
provedor de identidade, os usuários conseguem interagir com o seu aplicativo com menos ajuda sua. Eles são capazes de conectar-se, inscrever-se, mudar a senha e muito mais, sem pedir ajuda.
{: shortdesc}

**Por que eu desejaria exibir minhas próprias telas?**

Ao reutilizar suas IUs existentes, é possível criar um fluxo de conexão coeso para o seu aplicativo. Ao usar as mesmas
imagens, cores e marca, seus usuários são mais propensos a reconhecer sua marca, mesmo quando não interagem
diretamente com seu aplicativo.

</br>

**Que tipo de configuração é necessário para exibir minhas próprias telas?**

Para exibir suas próprias IUs, deve-se usar [Cloud Directory(/docs/services/appid/cloud-directory.html)] como o seu
provedor de identidade. Há várias maneiras diferentes como o Cloud Directory pode ser
[configurado](cloud-directory.html). É possível decidir os tipos de mensagens que você deseja enviar e customizar o conteúdo e o design. Não sabe o que dizer? Não é um problema. Há mensagens de exemplo na GUI que podem ser usadas.

Deseja usar um [idioma](cloud-directory.html#languages) diferente do inglês? É possível escolher outro
idioma usando as
<a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/updateLocalization" target="_blank">APIs de
gerenciamento de idioma <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>, para exibir seu próprio conteúdo traduzido.
{: tip}

</br>



**Como os fluxos são tecnicamente diferentes?**

O serviço usa os fluxos de concessão OAuth2 para mapear o processo de autorização. Quando você configura provedores de
identidade sociais, como o Facebook, o <a href="https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html" target="_blank">Fluxo de concessão de autorização <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> é usado para chamar o widget de login. Quando
você usa suas próprias telas, o
<a href="https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html" target="_blank">Fluxo de credenciais de
senha do proprietário do recurso <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> é usado para
fornecer os tokens de acesso e de identidade que permitem chamar suas telas de conexão.

</br>

**Você tem algum aplicativo de exemplo que mostra como isso funciona?**

Sim! Consulte qualquer um dos exemplos a seguir para ver o Cloud Directory em ação:

* <a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="_blank">Use a sua própria IU de marca para a conexão do usuário com o {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>
* <a href="https://www.ibm.com/blogs/bluemix/2018/06/use-ui-flows-user-sign-sign-app-id/" target="_blank">Use sua própria
IU e fluxos para inscrição do usuário e inscrição com o {{site.data.keyword.appid_short_notm}}
<img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>
* <a href="https://www.ibm.com/blogs/bluemix/2018/06/custom-login-page-app-id-integration/" target="_blank">Use uma página de login customizada com o {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>

</br>
</br>

## Inserindo uma marca no aplicativo com o SDK do Android
{: #branded-ui-android}

Com o Cloud Directory ativado, é possível chamar telas customizadas com o SDK do Android. É possível escolher a combinação das telas com as quais você gostaria que seus usuários fossem capazes de interagir.<a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="blank">Veja este blog<img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> para um exemplo detalhado!
{: shortdesc}

</br>

**Conectar**

1. Configure as [definições](cloud-directory.html#cd-settings) do Cloud Directory na GUI.
2. Inclua o código a seguir no aplicativo. O fluxo de conexão é acionado quando um usuário clica em Conectar em sua tela customizada. Você
obtém os tokens de acesso, de identidade e de atualização fornecendo o nome de usuário e a senha do usuário final.

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
</br>

## Inserindo uma marca no aplicativo com o SDK do iOS Swift
{: #branded-ui-ios-swift}

Com o Cloud Directory ativado, é possível chamar suas próprias telas com marca com o [SDK do iOS Swift](https://github.com/ibm-cloud-security/appid-clientsdk-swift).
{: shortdesc}

</br>

**Conectar**

1. Configure as [definições](cloud-directory.html#cd-settings) do Cloud Directory na GUI.
2. Coloque o código a seguir em seu aplicativo. Quando um usuário tentar se conectar, a sua tela de conexão será chamada e o processo de autorização e autenticação iniciará com a sua página de conexão customizada.

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


1. Configure as [definições](cloud-directory.html#cd-settings) do Cloud Directory na GUI.
2. Coloque o código a seguir em seu aplicativo. Quando um usuário tentar se conectar, a sua tela de conexão será chamada e o processo de autorização e autenticação iniciará com a sua página de conexão customizada.

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

**Nota**: se você enviar a solicitação em HTML, será possível usar o middleware do <a href="https://www.npmjs.com/package/body-parser" target="blank">analisador de corpo <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>. Para ver a mensagem de erro retornada, é possível usar <a href="https://www.npmjs.com/package/connect-flash" target="blank">connect-flash <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>. Para
vê-lo em ação, consulte a <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs/blob/master/samples/web-app-sample.js" target="blank">amostra do aplicativo da web <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.

</br>
</br>

## Inserindo uma marca no aplicativo com a API
{: #branded-ui-api}

É possível exibir suas próprias telas customizadas e aproveitar os recursos de autenticação e autorização do {{site.data.keyword.appid_short_notm}}. Com o Cloud Directory como o provedor de identidade, os usuários são capazes de interagir com o seu app com menos ajuda sua. Eles são capazes de conectar-se, inscrever-se, reconfigurar suas senhas e muito mais sem pedir ajuda.
{: shortdesc}

Para tornar isso possível, o {{site.data.keyword.appid_short_notm}} expõe as APIs de REST. É possível usar as
APIs de REST para construir um servidor de back-end que atenda a seus aplicativos da web ou para interagir com um
aplicativo móvel com suas próprias telas customizadas.

O gerenciamento de API é assegurado pelos tokens gerados pelo IBM Cloud Identity e Access Management. Isso significa que os proprietários de conta podem especificar quem na equipe terá qual nível de acesso para cada instância de serviço. Para mais informações sobre como o IAM e o {{site.data.keyword.appid_short_notm}} trabalham juntos, consulte [Gerenciamento de acesso de serviço](/docs/services/appid/iam.html).

Após ter definido as [configurações](/docs/services/appid/cloud-directory.html), é possível
chamar os terminais a seguir para exibir cada tela.

**Inscrever**

É possível usar o terminal `/sign_up` para permitir que os usuários se conectem ao seu aplicativo.
Forneça os seguintes dados no corpo da solicitação:
  * Seu tenantID.
  * Dados do usuário do Cloud Directory. Veja [Representação do usuário integral do SCIM](https://tools.ietf.org/html/rfc7643#section-8.2) para obter mais detalhes.
    * Um atributo `password`.
    * Na matriz de e-mail com um atributo `primary` que é configurado para `true`, deve-se ter pelo menos 1 endereço de e-mail.

Dependendo de sua [configuração de e-mail](/docs/services/appid/cloud-directory.html), um usuário pode
receber uma solicitação de verificação e/ou um e-mail de boas-vindas ao se inscrever ao seu aplicativo. Ambos os tipos de e-mails são acionados quando um usuário se inscreve para seu app. O
e-mail de verificação contém um link que o usuário pode clicar para confirmar sua identidade. Uma tela é exibida
agradecendo pela verificação ou confirmando que sua verificação está concluída.  

Para apresentar sua própria página de verificação de postagem:

1. Navegue para o provedor de identidade do Cloud Directory no painel do {site.data.keyword.appid_short_notm}}.
2. Clique na guia **Verificação de e-mail**.
3. Na **URL da página de verificação customizada**, insira a URL para sua página inicial.

Quando esse valor for fornecido, o {{site.data.keyword.appid_short_notm}} chamará a URL junto com uma consulta de `context`. Quando você chama o terminal `/sign_up/confirmation_result` e passa o parâmetro `context` recebido, o resultado indica se o usuário verificou sua conta. Se sim, será possível exibir sua página customizada.

</br>
**Esqueci a senha**

É possível usar o terminal `/forgot_password` para permitir que os usuários recuperem sua senha se a tiverem esquecido.

Forneça os seguintes dados no corpo da solicitação:
  * Seu tenantID.
  * O e-mail do usuário do Cloud Directory.

Quando o terminal é chamado, um e-mail de reconfiguração de senha é enviado para o usuário. O e-mail contém um botão **Reconfigurar**. Depois que eles pressionam o botão, uma tela é exibida pelo {{site.data.keyword.appid_short_notm}} que permite que eles reconfigurem suas senhas.

É possível apresentar a sua própria página de reconfiguração de senha de post:

1. Configure as [definições](cloud-directory.html#cd-settings) do Cloud Directory na GUI. **Permitir que os usuários gerenciem a sua conta por meio de seu app** deve ser configurado como **Ativado**.
2. Na guia **Reconfigurar senha** do painel de serviço, certifique-se de que **E-mail de senha esquecida** esteja configurado como **Ativado**.
3. Insira a URL para a sua página de entrada na **URL para sua página customizada de reconfiguração de senha**  

Quando esse valor for fornecido, o {{site.data.keyword.appid_short_notm}} chamará a URL junto com uma consulta de `context`. O parâmetro `context` é usado para receber o resultado quando `/forgot_password/confirmation_result` é chamado. Se o resultado for bem-sucedido, será possível exibir sua página customizada.

Inclua uma sequência aleatória em sua página customizada de reconfiguração de senha e passe-a ao seu backend quando a solicitação for enviada. Deixe o manipulador validar a sequência e chame o terminal `/change_password` somente se ele for válido. Ao fazer isso, é possível reduzir a vulnerabilidade do terminal de reconfiguração de senha de backend.
{: tip}

</br>
**Mudar senha**

É possível usar o terminal `/change_password` de duas maneiras. Quando um usuário envia uma solicitação de reconfiguração ou quando um usuário está conectado ao seu app e deseja atualizar sua senha.

Forneça os dados a seguir no corpo da solicitação para atualizar a senha após uma solicitação de reconfiguração:
  * Seu tenantID.
  * A nova senha do usuário.
  * O UUID do usuário do Cloud Directory.
  * Opcional: o endereço IP por meio do qual a reconfiguração de senha foi executada. Se você escolher passar o endereço IP, o item temporário `%{passwordChangeInfo.ipAddress}` estará disponível para o modelo de e-mail de mudança de senha.

Dependendo da sua configuração, quando uma senha mudar, o {{site.data.keyword.appid_short_notm}} poderá enviar um e-mail para informar isso ao usuário.

</br>
Para permitir que os usuários mudem suas senhas enquanto conectados a seu app:

Forneça os seguintes dados no corpo da solicitação:
  * Seu tenantID.
  * A nova senha do usuário.
  * O UUID do usuário do Cloud Directory.

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
  * O UUID do usuário do Cloud Directory.

**Detalhes da mudança**

Quando um usuário está conectado ao seu app, ele pode atualizar algumas das suas informações. É possível usar o `/Users/{userId}` para obter e atualizar suas informações.

Quando os detalhes do usuário são atualizados, o terminal obtém os dados do usuário atualizados no corpo da solicitação no [formato SCIM](https://tools.ietf.org/html/rfc7643#section-8.2). Certifique-se de que mudar somente os detalhes relevantes.

Seu endereço de e-mail não pode ser mudado.
{: tip}
