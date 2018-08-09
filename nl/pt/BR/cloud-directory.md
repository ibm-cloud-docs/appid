---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Configurando o diretório da nuvem
{: #cd}

Os usuários podem se inscrever e se conectar ao seus apps móveis e da web usando um e-mail e uma senha. Um diretório da nuvem é um registro do usuário mantido na nuvem. Quando um usuário se inscreve para seu app com um e-mail e uma senha, ele é incluído em seu diretório de usuários. Com esse recurso, os usuários têm a liberdade de gerenciar suas próprias contas dentro de seus apps.
{: shortdesc}

</br>

## Gerenciando configurações de diretório
{: #cd-settings}

É possível configurar as notificações e o nível de controle do usuário para seu app. A configuração de seu diretório da nuvem pode ser feita rapidamente, conforme mostrado na imagem a seguir. Essas configurações podem ser atualizadas a qualquer momento por meio do painel de serviço.
{: shortdesc}

![Configurando o diretório da nuvem](/images/cloud-directory.png)

1. Certifique-se de que o diretório da nuvem seja ativado como um provedor de identidade e configure **Permitir que os usuários se inscrevam e reconfigurem sua senha** para **Ligado**. Se configurado para **Desligado**, ainda é possível incluir usuários por meio do console para propósitos de desenvolvimento.
2. Configure os detalhes do emissor. Especifique o endereço de e-mail do qual as mensagens parecem ser provenientes, o remetente e para quem seus usuários podem responder.
  Ao configurar sua URL de ação, certifique-se de que você dê tempo suficiente para um usuário clicar no link. Um usuário deve verificar seu e-mail para ter algumas opções, como a capacidade de solicitar uma reconfiguração de sua senha.
  {: tip}
3. Determine os tipos de e-mails que um usuário recebe e as informações do remetente.
4. Com os modelos fornecidos, customize suas mensagens com sua marca ou mensagens personalizadas. Para obter mais informações, veja [Gerenciando mensagens](/docs/services/appid/cloud-directory.html#cd-messages).
5. Veja quem se inscreveu para seu app na guia **Usuários** da GUI.

</br>

## Gerenciando mensagens
{: #cd-messages}

Um modelo é um exemplo de um e-mail que você pode enviar para seus usuários. É possível customizar o modelo atualizando o conteúdo e o layout da mensagem. É possível configurar essas mensagens para **Ativado** ou **Desativado** na guia Configurações do diretório.
{: shortdesc}

1. Selecione um **Tipo de mensagem**.
2. Customize sua mensagem mudando o conteúdo e o design da mensagem. É possível utilizar parâmetros para personalizar suas mensagens. Não se esqueça de salvar suas mudanças!

### Tipos de mensagens

É possível enviar vários tipos de mensagens para os usuários. É possível escolher enviar a mensagem de exemplo que está programada para a IU ou customizar o conteúdo para uma experiência mais pessoal do app.

<dl>
  <dt>Bem-vindo</dt>
    <dd><p>Depois que eles se registraram, é possível dar as boas-vindas a um usuário para seu aplicativo via e-mail. Para receber e reter seus usuários, torne sua mensagem a mais atrativa possível.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> Todos os parâmetros da mensagem </th>
      </thead>
      <tbody>
        <tr>
          <td> %{display.logo} </td>
          <td> Exibe a imagem que você configurou para seu widget de login. </td>
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
          <td> Exibe o nome especificado do usuário. </td>
        </tr>
        <tr>
          <td> %{user.formattedName} </td>
          <td> Exibe o nome completo de um usuário. </td>
        </tr>
        <tr>
          <td> %{user.lastName} </td>
          <td> Exibe o sobrenome especificado do usuário. </td>
        </tr>
      </tbody>
    </table>
    <p>**Observação**: se um usuário não fornecer a informação extraída pelo parâmetro, ela aparecerá em branco.</p></dd>
  <dt>Senha esquecida</dt>
    <dd><p>Um usuário pode pedir para ter sua senha reconfigurada se ele a esqueceu ou precisa atualizá-la por qualquer razão. É possível customizar a resposta de e-mail para sua solicitação. Quando um usuário solicita uma mudança, a senha permanece como era até que ele clique no link neste e-mail.</p>
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
          <td> Exibe uma senha descartável como parte da URL. Isso significa que cada pessoa teria um código diferente. Exemplo: <code>https://appid-wfm.bluemix.net/verify/6574839563478 </code> </td>
        </tr>
        <tr>
          <td> %{resetPassword.link} </td>
          <td> Exibe o link em que um usuário clica para reconfigurar sua senha. </td>
        </tr>
       </tbody>
    </table>
    </dd>
  <dt>Verificação</dt>
    <dd><p>É possível solicitar que um usuário verifique sua conta via e-mail. Ao solicitar uma verificação, você limita o número de contas falsas que podem se inscrever para seu app. É possível restringir o acesso ao seu app até que um usuário verifique seu e-mail ou o use como uma maneira de gerenciar para quais usuários você cria perfis.</p>
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
    </table>
    </dd>
  <dt>Mudança de senha</dt>
    <dd><p>É possível informar um usuário quando a senha é atualizada. Isso é útil se eles não solicitaram que suas senhas fossem mudadas. Eles podem tomar as etapas adequadas para tornar a proteger sua conta.</p>
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
    </table>
    </dd>
</dl>
</br>
**NOTA**: o {{site.data.keyword.appid_short_notm}} usa o <a href="https://www.sendgrid.com" target="_blank">SendGrid <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> como um serviço de entrega de mensagem. Todos os e-mails são enviados com uma única conta SendGrid.

</br>
## Próximas etapas
Agora que já configurou o diretório da nuvem, você está pronto para incluir o código para o widget de login em seu código de app. Clique em um ícone de linguagem do SDK na imagem a seguir para ver o que você precisa fazer.
{: shortdesc}

<img usemap="#options-map" border="0" class="image" id="options" src="images/options.png" width="750" alt="Clique em um ícone de linguagem do SDK para começar a usar o diretório da nuvem em seus apps." style="width:750px;" />
<map name="options-map" id="options-map">
<area href="login-widget.html#branded-ui-android" alt="Gerenciando a experiência de conexão com o SDK Android" shape="rect" coords="187, 6, 305, 120" />
<area href="login-widget.html#branded-ui-ios-swift" alt="Gerenciando a experiência de conexão com o SDK iOS Swift." shape="rect" coords="333, 6, 448, 125" />
<area href="login-widget.html#branded-ui-nodejs" alt="Gerenciando a experiência de conexão com o SDK Node.js." shape="rect" coords="472, 7, 590, 121" />
</map>
