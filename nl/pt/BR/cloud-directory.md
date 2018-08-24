---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-09"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Configurando o diretório da nuvem
{: #cd}

Os usuários podem se inscrever e se conectar nos aplicativos móveis e da web usando um e-mail ou um nome de usuário e uma senha. Um diretório da nuvem é um registro do usuário mantido na nuvem. Quando um usuário se inscreve no aplicativo, ele é incluído no seu diretório de usuários. Com esse recurso, os usuários têm a liberdade de gerenciar suas próprias contas dentro de seus apps.
{: shortdesc}

</br>

## Gerenciando configurações de diretório
{: #cd-settings}

É possível configurar as notificações e o nível de controle do usuário para seu app. A configuração de seu diretório da nuvem pode ser feita rapidamente, conforme mostrado na imagem a seguir. Essas configurações podem ser atualizadas a qualquer momento por meio do painel de serviço.
{: shortdesc}


![Configurando o Cloud Directory](/images/cloud-directory.png)
Figura. A jornada de configuração para o Cloud Directory


1. Certifique-se de que o Cloud Directory esteja ativado como um provedor de identidade e configure **Permitir que os usuários se inscrevam e reconfigurem a sua senha ** para **Ativado**. Se configurado para **Desligado**, ainda é possível incluir usuários por meio do console para propósitos de desenvolvimento.
2. Escolha se os usuários serão autenticados com um nome do usuário especificado ou um e-mail. Esse campo é usado para a inscrição, a conexão e os fluxos de senha esquecida. Se você permitir que os usuários se conectem com um nome do usuário e senha, o nome do usuário deverá ter pelo menos 8 caracteres e não poderá conter espaços, vírgulas ou barras. **Nota:** é possível alternar entre as opções somente quando não há usuários no Cloud Directory.
3. Configure os detalhes do emissor. Especifique o endereço de e-mail do qual as mensagens parecem ser provenientes, o remetente e para quem seus usuários podem responder.
  Ao configurar sua URL de ação, certifique-se de que você dê tempo suficiente para um usuário clicar no link. Um usuário deve verificar seu e-mail para ter algumas opções, como a capacidade de solicitar uma reconfiguração de sua senha.
  {: tip}
4. Determine os tipos de e-mails que um usuário recebe e as informações do remetente.
5. Com os modelos fornecidos, customize suas mensagens com sua marca ou mensagens personalizadas. Para obter mais informações, veja [Gerenciando mensagens](/docs/services/appid/cloud-directory.html#cd-messages).
6. Veja quem se inscreveu para seu app na guia **Usuários** da GUI.

Um único usuário pode se conectar até 5 vezes por minuto. Se uma sexta tentativa for feita, um erro será exibido.
{: tip}

</br>

## Gerenciando mensagens
{: #cd-messages}

Um modelo é um exemplo de um e-mail que você pode enviar para seus usuários. É possível customizar o modelo atualizando o conteúdo e o layout da mensagem.
{: shortdesc}

1. Na guia **Provedores de identidade > Cloud Directory > Configurações** do painel, configure as mensagens que você deseja enviar para **Ativado**.

2. Opcional: use <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/updateLocalization" target="_blank">as APIs de gerenciamento de idioma <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> para configurar outro idioma que deseja usar nos modelos de mensagens. Para obter uma lista de códigos de idioma suportados, consulte [Idiomas suportados](#languages).

3. Selecione um **Tipo de mensagem**.

4. Customize sua mensagem mudando o conteúdo e o design da mensagem. É possível utilizar parâmetros para personalizar suas mensagens. Não se esqueça de salvar suas mudanças!

### Tipos de mensagens

É possível enviar vários tipos de mensagens para os usuários. É possível escolher enviar a mensagem de exemplo que está programada para a IU ou customizar o conteúdo para uma experiência mais pessoal do app.

<dl>
  <dt>Bem-vindo</dt>
    <dd><p>Depois que eles se registraram, é possível dar as boas-vindas a um usuário para seu aplicativo via e-mail. Para receber e reter seus usuários, torne sua mensagem a mais atrativa possível.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="ícone Mais informações"/> todos os parâmetros de mensagem </th>
      </thead>
      <tbody>
        <tr>
          <td><code>%{display.logo}</code></td>
          <td> Exibe a imagem que você configurou para seu widget de login. </td>
        </tr>
        <tr>
          <td><code>%{user.displayName}</code></td>
          <td> Exibe o nome da tela que um usuário escolheu usar ao interagir com o app. </td>
        </tr>
        <tr>
          <td><code>%{user.email}</code></td>
          <td> Exibe o endereço de e-mail do usuário registrado. </td>
        </tr>
        <tr>
          <td><code>%{user.username}</code></td>
          <td> Exibe o nome do usuário especificado quando o método de autenticação é configurado para o nome do usuário e a senha. </td>
        </tr>
        <tr>
          <td><code>%{user.firstName}</code></td>
          <td> Exibe o nome especificado do usuário. </td>
        </tr>
        <tr>
          <td><code>%{user.formattedName}</code></td>
          <td> Exibe o nome completo do usuário. </td>
        </tr>
        <tr>
          <td><code>%{user.lastName}</code></td>
          <td> Exibe o sobrenome especificado do usuário. </td>
        </tr>
      </tbody>
    </table>
    <p>**Observação**: se um usuário não fornecer a informação extraída pelo parâmetro, ela aparecerá em branco.</p></dd>
  <dt>Senha esquecida</dt>
    <dd><p>Um usuário pode pedir para ter sua senha reconfigurada se ele a esqueceu ou precisa atualizá-la por qualquer razão. É possível customizar a resposta de e-mail para sua solicitação. Quando um usuário solicita uma mudança, a senha permanece como era até que ele clique no link neste e-mail.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="More information icon"/>  Parâmetros de mudança de senha </th>
      </thead>
      <tbody>
        <tr>
          <td><code>%{linkExpiration.hours}</code></td>
          <td> Exibe o número de horas em que o link é válido. </td>
        </tr>
        <tr>
          <td><code>%{linkExpiration.minutes}</code></td>
          <td> Exibe o número de minutos em que o link é válido. </td>
        </tr>
        <tr>
          <td><code>%{resetPassword.code}</code></td>
          <td> Exibe uma senha descartável como parte da URL. Isso significa que cada pessoa teria um código diferente. Exemplo: <code>https://appid-wfm.bluemix.net/verify/6574839563478 </code> </td>
        </tr>
        <tr>
          <td><code>%{resetPassword.link}</code></td>
          <td> Exibe o link em que um usuário clica para reconfigurar sua senha. </td>
        </tr>
       </tbody>
    </table>
    </dd>
  <dt>Verificação</dt>
    <dd><p>É possível solicitar que um usuário verifique sua conta via e-mail. Ao solicitar uma verificação, você limita o número de contas falsas que podem se inscrever para seu app. É possível restringir o acesso ao seu app até que um usuário verifique seu e-mail ou o use como uma maneira de gerenciar para quais usuários você cria perfis.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="More information icon"/>  Parâmetros de mensagem de verificação </th>
      </thead>
      <tbody>
        <tr>
          <td><code>%{linkExpiration.hours}</code></td>
          <td> Exibe o número de horas em que o link é válido. </td>
        </tr>
        <tr>
          <td><code>%{linkExpiration.minutes}</code></td>
          <td> Exibe o número de minutos em que o link é válido. </td>
        </tr>
        <tr>
          <td><code>%{verify.code}</code></td>
          <td> Exibe uma URL de verificação descartável. </td>
        </tr>
        <tr>
          <td><code>%{verify.link}</code></td>
          <td> Exibe a URL de ação que você especificou nas configurações. </td>
        </tr>
      </tbody>
    </table>
    </dd>
  <dt>Mudança de senha</dt>
    <dd><p>É possível informar um usuário quando a senha é atualizada. Isso é útil se eles não solicitaram que suas senhas fossem mudadas. Eles podem tomar as medidas adequadas para reafirmar sua conta.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="More information icon"/>  Parâmetros de mudança de senha </th>
      </thead>
      <tbody>
        <tr>
          <td><code>%{passwordChangeInfo.time}</code></td>
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

## Gerenciando a força da
{: #strength}

É possível configurar os requisitos para as senhas que podem ser usadas com o Cloud Directory.
{: shortdesc}

Uma senha forte torna difícil ou mesmo improvável que alguém adivinhe a senha por meio de uma maneira manual ou automatizada. A força da senha é configurada como uma sequência de expressão regular.

Alguns exemplos comuns de força da senha:

- Deve ter pelo menos 8 caracteres. Exemplo de regex: `^.{8,}$`
- Deve conter um número, uma letra minúscula e uma letra maiúscula. Exemplo de regex: `^(?:(?=.*\\d)(?=.*[a-z])(?=.*[A-Z]).*)$`
- Deve conter somente letras e números em inglês. Exemplo de regex: `^[A-Za-z0-9]*$`
- Deve ter pelo menos um caractere exclusivo. Exemplo de regex: `^(\w)\w*?(?!\1)\w+$`

Deve-se usar <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/set_cloud_directory_password_regex" target="_blank">as APIs de gerenciamento <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> para configurar os requisitos.

</br>



</br>

## Idiomas Suportados
{: #languages}

É possível usar <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/updateLocalization" target="_blank">as APIs de gerenciamento de idioma <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> para configurar o idioma no qual a comunicação do usuário pode ser escrita. No entanto, somente o inglês está prontamente disponível para uso. Você é responsável pela tradução das mensagens. Depois de definir a configuração com a API, a GUI é atualizada para que você possa mudar o texto do modelo.
{: shortdesc}

<table>
  <col width="20%">
  <col width="25%">
  <col width="35%">
  <tr>
    <th>Código</th>
    <th>idioma</th>
    <th>região</th>
  </tr>
  <tr>
    <td><code> af-ZA </code></td>
    <td>Afrikaans</td>
    <td>África do Sul</td>
  </tr>
  <tr>
    <td><code> sq-AL </code></td>
    <td>Albanês</td>
    <td>Albânia</td>
  </tr>
  <tr>
    <td><code> am-ET </code></td>
    <td>amálico</td>
    <td>Etiópia</td>
  </tr>
  <tr>
    <td><code> ar-DZ </code></td>
    <td>Arábico</td>
    <td>Argélia</td>
  </tr>
  <tr>
    <td><code>ar-BH</code></td>
    <td>Arábico</td>
    <td>Bahrein</td>
  </tr>
  <tr>
    <td><code> ar-EG </code></td>
    <td>Arábico</td>
    <td>Egito</td>
  </tr>
  <tr>
    <td><code> ar-IQ </code></td>
    <td>Arábico</td>
    <td>Iraque</td>
  </tr>
  <tr>
    <td><code> ar-JO </code></td>
    <td>Arábico</td>
    <td>Jordânia</td>
  </tr>
  <tr>
    <td><code> ar-KW </code></td>
    <td>Arábico</td>
    <td>Kuait</td>
  </tr>
  <tr>
    <td><code> ar-LB </code></td>
    <td>Arábico</td>
    <td>Líbano</td>
  </tr>
  <tr>
    <td><code> ar-LY </code></td>
    <td>Arábico</td>
    <td>Líbia</td>
  </tr>
  <tr>
    <td><code> ar-MR </code></td>
    <td>Arábico</td>
    <td>Mauritânia</td>
  </tr>
  <tr>
    <td><code> ar-MA </code></td>
    <td>Arábico</td>
    <td>Morroco</td>
  </tr>
  <tr>
    <td><code> ar-OM </code></td>
    <td>Arábico</td>
    <td>Oman</td>
  </tr>
  <tr>
    <td><code>ar-QA</code></td>
    <td>Arábico</td>
    <td>Catar</td>
  </tr>
  <tr>
    <td><code> ar-SA </code></td>
    <td>Arábico</td>
    <td>Arábia Saudita</td>
  </tr>
  <tr>
    <td><code> ar-SY </code></td>
    <td>Arábico</td>
    <td>Síria</td>
  </tr>
  <tr>
    <td><code> ar-YE </code></td>
    <td>Arábico</td>
    <td>Tunísia</td>
  </tr>
  <tr>
    <td><code> ar-AE </code></td>
    <td>Arábico</td>
    <td>Emirados Árabes Unidos</td>
  </tr>
  <tr>
    <td><code> ar-YE </code></td>
    <td>Arábico</td>
    <td>Iemen</td>
  </tr>
  <tr>
    <td><code> hy-AM </code></td>
    <td>Arménio</td>
    <td>Armênia</td>
  </tr>
  <tr>
    <td><code> como-IN </code></td>
    <td>Assamese</td>
    <td>Índia</td>
  </tr>
  <tr>
    <td><code> az-AZ </code></td>
    <td>Azerbaijano</td>
    <td>Azerbaijão</td>
  </tr>
  <tr>
    <td><code> eu-ES </code></td>
    <td>basco</td>
    <td>Espanha</td>
  </tr>
  <tr>
    <td><code> be-BY </code></td>
    <td>bielorrusso</td>
    <td>Bielorússia</td>
  </tr>
  <tr>
    <td><code> bn-BD </code></td>
    <td>Bengalês</td>
    <td>Bangladesh</td>
  </tr>
  <tr>
    <td><code> be-BY </code></td>
    <td>bielorrusso</td>
    <td>Bielorússia</td>
  </tr>
  <tr>
    <td><code> bn-BD </code></td>
    <td>Bengalês</td>
    <td>Bangladesh</td>
  </tr>
  <tr>
    <td><code> bn-IN </code></td>
    <td>Bengalês</td>
    <td>Índia</td>
  </tr>
  <tr>
    <td><code> bs-Latn-BA </code></td>
    <td>Bósnio</td>
    <td>Bósnia</td>
  </tr>
  <tr>
    <td><code> bg-BG </code></td>
    <td>Búlgaro</td>
    <td>Bulgária</td>
  </tr>
  <tr>
    <td><code> my-MM </code></td>
    <td>Burmese</td>
    <td>Mianmar</td>
  </tr>
  <tr>
    <td><code> ca-ES </code></td>
    <td>Catalão</td>
    <td>Espanha</td>
  </tr>
  <tr>
    <td><code> zh-Hans-CN </code></td>
    <td>Chinês Simplificado</td>
    <td>China</td>
  </tr>
  <tr>
    <td><code>zh-Hans-SG</code></td>
    <td>Chinês Simplificado</td>
    <td>Singapura</td>
  </tr>
  <tr>
    <td><code> zh-Hant-HK </code></td>
    <td>Chinês-tradicional</td>
    <td>Hong Kong R.A.E. da China</td>
  </tr>
  <tr>
    <td><code> zh-Hant-MO </code></td>
    <td>Chinês-tradicional</td>
    <td>Macau</td>
  </tr>
  <tr>
    <td><code>zh-Hant-TW</code></td>
    <td>Chinês-tradicional</td>
    <td>Taiwan</td>
  </tr>
  <tr>
    <td><code> hr-HR </code></td>
    <td>Croata</td>
    <td>Croácia</td>
  </tr>
  <tr>
    <td><code> cs-CZ </code></td>
    <td>tcheco</td>
    <td>República Tcheca</td>
  </tr>
  <tr>
    <td><code> da-DK </code></td>
    <td>Dinamarquês</td>
    <td>Dinamarca</td>
  </tr>
  <tr>
    <td><code> nl-BE </code></td>
    <td>Holandês</td>
    <td>Bélgica</td>
  </tr>
  <tr>
    <td><code> nl-NL </code></td>
    <td>Holandês</td>
    <td>Países Baixos</td>
  </tr>
  <tr>
    <td><code> en-AU </code></td>
    <td>Inglês</td>
    <td>Austrália</td>
  </tr>
  <tr>
    <td><code> eu-BE </code></td>
    <td>Inglês</td>
    <td>Bélgica</td>
  </tr>
  <tr>
    <td><code> en-CM </code></td>
    <td>Inglês</td>
    <td>Camarões</td>
  </tr>
  <tr>
    <td><code> eu-CA </code></td>
    <td>Inglês</td>
    <td>Canadá</td>
  </tr>
  <tr>
    <td><code>en-GH</code></td>
    <td>Inglês</td>
    <td>Ghana</td>
  </tr>
  <tr>
    <td><code> eu-HK </code></td>
    <td>Inglês</td>
    <td>Hong Kong R.A.E. da China</td>
  </tr>
  <tr>
    <td><code> en-IN </code></td>
    <td>Inglês</td>
    <td>Índia</td>
  </tr>
  <tr>
    <td><code>en-IE</code></td>
    <td>Inglês</td>
    <td>Irlanda</td>
  </tr>
  <tr>
    <td><code> en-KE </code></td>
    <td>Inglês</td>
    <td>Quénia</td>
  </tr>
  <tr>
    <td><code> en-MU </code></td>
    <td>Inglês</td>
    <td>Ilhas Maurício</td>
  </tr>
  <tr>
    <td><code> en-NZ </code></td>
    <td>Inglês</td>
    <td>Nova Zelândia</td>
  </tr>
  <tr>
    <td><code> en-NG </code></td>
    <td>Inglês</td>
    <td>Nigéria</td>
  </tr>
  <tr>
    <td><code> en-PH </code></td>
    <td>Inglês</td>
    <td>Filipinas</td>
  </tr>
  <tr>
    <td><code> en-SG </code></td>
    <td>Inglês</td>
    <td>Singapura</td>
  </tr>
  <tr>
    <td><code> en-ZA </code></td>
    <td>Inglês</td>
    <td>África do Sul</td>
  </tr>
  <tr>
    <td><code> en-TZ </code></td>
    <td>Inglês</td>
    <td>Tanzânia</td>
  </tr>
  <tr>
    <td><code> en-GB </code></td>
    <td>Inglês</td>
    <td>United Kingdom</td>
  </tr>
  <tr>
    <td><code> en-US </code></td>
    <td>Inglês</td>
    <td>Estados Unidos</td>
  </tr>
  <tr>
    <td><code> en-ZM </code></td>
    <td>Inglês</td>
    <td>Zâmbia</td>
  </tr>
  <tr>
    <td><code> en </code></td>
    <td>Inglês</td>
    <td> </td>
  </tr>
  <tr>
    <td><code> et-EE </code></td>
    <td>Estoniano</td>
    <td>Estônia</td>
  </tr>
  <tr>
    <td><code>fil-PH</code></td>
    <td>Filipino</td>
    <td>Filipinas</td>
  </tr>
  <tr>
    <td><code> fi-FI </code></td>
    <td>Finlandês</td>
    <td>Finlândia</td>
  </tr>
  <tr>
    <td><code> fr-DZ </code></td>
    <td>Francês</td>
    <td>Argélia</td>
  </tr>
  <tr>
    <td><code> fr-CM </code></td>
    <td>Francês</td>
    <td>Camarões</td>
  </tr>
  <tr>
    <td><code> fr-CD </code></td>
    <td>Francês</td>
    <td>República Democrática do Congo</td>
  </tr>
  <tr>
    <td><code> fr-BE </code></td>
    <td>Francês</td>
    <td>Bélgica</td>
  </tr>
  <tr>
    <td><code> fr-CA </code></td>
    <td>Francês</td>
    <td>Canadá</td>
  </tr>
  <tr>
    <td><code>fr-FR</code></td>
    <td>Francês</td>
    <td>França</td>
  </tr>
  <tr>
    <td><code> fr-CI </code></td>
    <td>Francês</td>
    <td>Costa do Marfim (Côte d' Ivoire)</td>
  </tr>
  <tr>
    <td><code> fr-LU </code></td>
    <td>Francês</td>
    <td>Luxemburgo</td>
  </tr>
  <tr>
    <td><code> fr-MR </code></td>
    <td>Francês</td>
    <td>Mauritânia</td>
  </tr>
  <tr>
    <td><code> fr-MU </code></td>
    <td>Francês</td>
    <td>Ilhas Maurício</td>
  </tr>
  <tr>
    <td><code> fr-MA </code></td>
    <td>Francês</td>
    <td>Marrocos</td>
  </tr>
  <tr>
    <td><code> fr-SN </code></td>
    <td>Francês</td>
    <td>Senegal</td>
  </tr>
  <tr>
    <td><code> fr-CH </code></td>
    <td>Francês</td>
    <td>Suiça</td>
  </tr>
  <tr>
    <td><code> fr-TN </code></td>
    <td>Francês</td>
    <td>Tunísia</td>
  </tr>
  <tr>
    <td><code> gl-ES </code></td>
    <td>Galiciano</td>
    <td>Espanha</td>
  </tr>
  <tr>
    <td><code>lg-UG</code></td>
    <td>Ganda</td>
    <td>Uganda</td>
  </tr>
  <tr>
    <td><code> ka-GE </code></td>
    <td>georgiano</td>
    <td>Geórgia</td>
  </tr>
  <tr>
    <td><code> de-AT </code></td>
    <td>Alemão</td>
    <td>Áustria</td>
  </tr>
  <tr>
    <td><code> de-DE </code></td>
    <td>Alemão</td>
    <td>Alemanha</td>
  </tr>
  <tr>
    <td><code> de-LU </code></td>
    <td>Alemão</td>
    <td>Luxemburgo</td>
  </tr>
  <tr>
    <td><code> de-CH </code></td>
    <td>Alemão</td>
    <td>Suiça</td>
  </tr>
  <tr>
    <td><code> el-GR </code></td>
    <td>Grego</td>
    <td>Grécia</td>
  </tr>
  <tr>
    <td><code>gu-IN</code></td>
    <td>Gujarati</td>
    <td>Índia</td>
  </tr>
  <tr>
    <td><code> ha-NG </code></td>
    <td>Hausa</td>
    <td>Nigéria</td>
  </tr>
  <tr>
    <td><code> he-IL </code></td>
    <td>Hebraico</td>
    <td>Israel</td>
  </tr>
  <tr>
    <td><code> hi-IN </code></td>
    <td>Hindi</td>
    <td>Índia</td>
  </tr>
  <tr>
    <td><code> hu-HU </code></td>
    <td>Húngaro</td>
    <td>Hungria</td>
  </tr>
  <tr>
    <td><code> is-IS </code></td>
    <td>Islandês</td>
    <td>Islândia</td>
  </tr>
  <tr>
    <td><code> ig-NG </code></td>
    <td>Igbo</td>
    <td>Nigéria</td>
  </tr>
  <tr>
    <td><code> id-ID </code></td>
    <td>Indonésio</td>
    <td>Indonésia</td>
  </tr>
  <tr>
    <td><code> it-IT </code></td>
    <td>Italiano</td>
    <td>Itália</td>
  </tr>
  <tr>
    <td><code> it-CH </code></td>
    <td>Italiano</td>
    <td>Suiça</td>
  </tr>
  <tr>
    <td><code>ja-JP</code></td>
    <td>Japonês</td>
    <td>Japão</td>
  </tr>
  <tr>
    <td><code> kn-IN </code></td>
    <td>Canarês</td>
    <td>Índia</td>
  </tr>
  <tr>
    <td><code> kk-KZ </code></td>
    <td>Casakh</td>
    <td>Casaquistão</td>
  </tr>
  <tr>
    <td><code> km-KH </code></td>
    <td>Khmer</td>
    <td>Cambodja</td>
  </tr>
  <tr>
    <td><code> rw-RW </code></td>
    <td>kinyarwanda</td>
    <td>Ruanda</td>
  </tr>
  <tr>
    <td><code> kok-IN </code></td>
    <td>Konkani</td>
    <td>Índia</td>
  </tr>
  <tr>
    <td><code> ko-KR </code></td>
    <td>Coreano</td>
    <td>Coreia do Sul</td>
  </tr>
  <tr>
    <td><code> lo-LA </code></td>
    <td>lituano</td>
    <td>Lituânia</td>
  </tr>
  <tr>
    <td><code> lv-LV </code></td>
    <td>letão</td>
    <td>Látvia</td>
  </tr>
  <tr>
    <td><code> lt-LT </code></td>
    <td>Khmer</td>
    <td>Cambodja</td>
  </tr>
  <tr>
    <td><code>mk-MK</code></td>
    <td>Macedoniano</td>
    <td>Macedônia</td>
  </tr>
  <tr>
    <td><code> ms-Latn-MY </code></td>
    <td>Malaio-Latim</td>
    <td>Malásia</td>
  </tr>
  <tr>
    <td><code> ml-IN </code></td>
    <td>Malaiano</td>
    <td>Índia</td>
  </tr>
  <tr>
    <td><code> mt-MT </code></td>
    <td>Maltês</td>
    <td>Malta</td>
  </tr>
  <tr>
    <td><code> mr-IN </code></td>
    <td>Marathi</td>
    <td>Índia</td>
  </tr>
  <tr>
    <td><code> mn-Cyrl-MN </code></td>
    <td>Mongólia-cirílico</td>
    <td>Mongólia</td>
  </tr>
  <tr>
    <td><code> ne-IN </code></td>
    <td>nepalês</td>
    <td>Índia</td>
  </tr>
  <tr>
    <td><code> ne-NP </code></td>
    <td>nepalês</td>
    <td>Nepal</td>
  </tr>
  <tr>
    <td><code> nb-NO </code></td>
    <td>Norueguês Bokmål</td>
    <td>Noruega</td>
  </tr>
  <tr>
    <td><code> nn-NO </code></td>
    <td>Norueguês (Nynor</td>
    <td>Noruega</td>
  </tr>
  <tr>
    <td><code>or-IN</code></td>
    <td>Oriya (Odia)</td>
    <td>Índia</td>
  </tr>
  <tr>
    <td><code> om-ET </code></td>
    <td>Oromo</td>
    <td>Etiópia</td>
  </tr>
  <tr>
    <td><code> pl-PL </code></td>
    <td>Polonês</td>
    <td>Polonia</td>
  </tr>
  <tr>
    <td><code> pt-AO </code></td>
    <td>Português</td>
    <td>Angola</td>
  </tr>
  <tr>
    <td><code> pt-BR </code></td>
    <td>Português</td>
    <td>Brasil</td>
  </tr>
  <tr>
    <td><code> pt-MO </code></td>
    <td>Português</td>
    <td>Macau</td>
  </tr>
  <tr>
    <td><code> pt-MZ </code></td>
    <td>Português</td>
    <td>Moçambique</td>
  </tr>
  <tr>
    <td><code> pt-PT </code></td>
    <td>Português</td>
    <td>Portugal</td>
  </tr>
  <tr>
    <td><code> pa-IN </code></td>
    <td>Punjabe</td>
    <td>Índia</td>
  </tr>
  <tr>
    <td><code> ro-ro </code></td>
    <td>Romeno</td>
    <td>Romênia</td>
  </tr>
  <tr>
    <td><code>ru-RU</code></td>
    <td>Russo</td>
    <td>Rússia</td>
  </tr>
  <tr>
    <td><code> sr-Cyrl-RS </code></td>
    <td>Sérvio-Cirílico</td>
    <td>Sérvia</td>
  </tr>
  <tr>
    <td><code> sr-Latn-ME </code></td>
    <td>Sérvio-Latino</td>
    <td>Montenegro</td>
  </tr>
  <tr>
    <td><code> sr-Latn-RS </code></td>
    <td>Sérvio-Latino</td>
    <td>Sérvia</td>
  </tr>
  <tr>
    <td><code> si-LK </code></td>
    <td>Sinhala</td>
    <td>Sri Lanka</td>
  </tr>
  <tr>
    <td><code> sk-SK </code></td>
    <td>eslovaco</td>
    <td>Eslováquia</td>
  </tr>
  <tr>
    <td><code> sl-SI </code></td>
    <td>Esloveno</td>
    <td>Eslovênia</td>
  </tr>
  <tr>
    <td><code> es-AR </code></td>
    <td>Espanhol</td>
    <td>Argentina</td>
  </tr>
  <tr>
    <td><code> es-BO </code></td>
    <td>Espanhol</td>
    <td>Bolívia</td>
  </tr>
  <tr>
    <td><code> es-CL </code></td>
    <td>Espanhol</td>
    <td>Chile</td>
  </tr>
  <tr>
    <td><code>es-CO</code></td>
    <td>Espanhol</td>
    <td>Colômbia</td>
  </tr>
  <tr>
    <td><code> es-CR </code></td>
    <td>Espanhol</td>
    <td>Costa Rica</td>
  </tr>
  <tr>
    <td><code> es-DO </code></td>
    <td>Espanhol</td>
    <td>República Dominicana</td>
  </tr>
  <tr>
    <td><code> es-EC </code></td>
    <td>Espanhol</td>
    <td>Equador</td>
  </tr>
  <tr>
    <td><code> es-SV </code></td>
    <td>Espanhol</td>
    <td>El Salvador</td>
  </tr>
  <tr>
    <td><code> es-GT </code></td>
    <td>Espanhol</td>
    <td>Guatemala</td>
  </tr>
  <tr>
    <td><code> es-HN </code></td>
    <td>Espanhol</td>
    <td>Honduras</td>
  </tr>
  <tr>
    <td><code> es-MX </code></td>
    <td>Espanhol</td>
    <td>México</td>
  </tr>
  <tr>
    <td><code> es-NI </code></td>
    <td>Espanhol</td>
    <td>Nicarágua</td>
  </tr>
  <tr>
    <td><code> es-PA </code></td>
    <td>Espanhol</td>
    <td>Panamá</td>
  </tr>
  <tr>
    <td><code>es-PY</code></td>
    <td>Espanhol</td>
    <td>Paraguai</td>
  </tr>
  <tr>
    <td><code> es-PE </code></td>
    <td>Espanhol</td>
    <td>Peru</td>
  </tr>
  <tr>
    <td><code> es-PR </code></td>
    <td>Espanhol</td>
    <td>Porto Rico</td>
  </tr>
  <tr>
    <td><code> es-ES </code></td>
    <td>Espanhol</td>
    <td>Espanha</td>
  </tr>
  <tr>
    <td><code> es-EUA </code></td>
    <td>Espanhol</td>
    <td>Estados Unidos</td>
  </tr>
  <tr>
    <td><code> es-UY </code></td>
    <td>Espanhol</td>
    <td>Uruguai</td>
  </tr>
  <tr>
    <td><code> es-VE </code></td>
    <td>Espanhol</td>
    <td>Venezuela</td>
  </tr>
  <tr>
    <td><code> sw-KE </code></td>
    <td>Swahili</td>
    <td>Quénia</td>
  </tr>
  <tr>
    <td><code> sw-TZ </code></td>
    <td>Swahili</td>
    <td>Tanzânia</td>
  </tr>
  <tr>
    <td><code> sv-SE </code></td>
    <td>Sueco</td>
    <td>Suécie</td>
  </tr>
  <tr>
    <td><code>ta-IN</code></td>
    <td>Tamil</td>
    <td>Índia</td>
  </tr>
  <tr>
    <td><code> te-IN </code></td>
    <td>Telugu</td>
    <td>Índia</td>
  </tr>
  <tr>
    <td><code> th-TH </code></td>
    <td>Tailandês</td>
    <td>Tailândia</td>
  </tr>
  <tr>
    <td><code> tr-TR </code></td>
    <td>Turco</td>
    <td>Turquia</td>
  </tr>
  <tr>
    <td><code> uk-UA </code></td>
    <td>Ucraniano</td>
    <td>Ucrânia</td>
  </tr>
  <tr>
    <td><code> ur-IN </code></td>
    <td>Urdu</td>
    <td>Índia</td>
  </tr>
  <tr>
    <td><code> ur-PK </code></td>
    <td>Urdu</td>
    <td>Paquistão</td>
  </tr>
  <tr>
    <td><code> uz-Cyrl-UZ </code></td>
    <td>Uzbek-Cirílico</td>
    <td>Usbequistão</td>
  </tr>
  <tr>
    <td><code> uz-Latn-UZ </code></td>
    <td>Uzbeque-Latim</td>
    <td>Usbequistão</td>
  </tr>
  <tr>
    <td><code> vi-VN </code></td>
    <td>Vietnamita</td>
    <td>Vietnã</td>
  </tr>
  <tr>
    <td><code>cy-GB</code></td>
    <td>galês</td>
    <td>United Kingdom</td>
  </tr>
  <tr>
    <td><code> yo-NG </code></td>
    <td>Ioruba</td>
    <td>Nigéria</td>
  </tr>
  <tr>
    <td><code> zu-ZA </code></td>
    <td>zulu</td>
    <td>África do Sul</td>
  </tr>
</table>
