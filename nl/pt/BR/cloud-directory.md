---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Cloud Directory
{: #cd}

Com o {{site.data.keyword.appid_full}}, os usuários podem se inscrever e se conectar em seus
aplicativos móveis e da web usando um e-mail ou nome de usuário e uma senha. Um diretório da nuvem é um registro do usuário mantido na nuvem. Quando um usuário se inscreve no aplicativo, ele é incluído no seu diretório de usuários. Com esse recurso, os usuários têm a liberdade de gerenciar suas próprias contas dentro de seus apps.
{: shortdesc}

</br>

## Gerenciando configurações de diretório
{: #cd-settings}

É possível configurar as notificações e o nível de controle do usuário para seu app. A configuração do Cloud
Directory pode ser feita rapidamente, conforme mostrado na imagem a seguir. Essas configurações podem ser atualizadas a qualquer momento por meio do painel de serviço.
{: shortdesc}


![Configurando o Cloud Directory](images/cloud-directory.png)
Figura. A jornada de configuração para o Cloud Directory

1. Na guia **Gerenciar** do painel do {{site.data.keyword.appid_short_notm}}, certifique-se de que o Cloud Directory esteja configurado como **Ativado**.

2. Configure suas definições gerais.
  1. Decida se deseja que seus usuários criem um nome de usuário ou usem o e-mail ao se conectarem. Ambas as opções requerem uma senha. Depois que os usuários tiverem sido incluídos em seu diretório, não será mais possível alternar entre as opções.
  2. Clique em **Editar** na linha de critérios de senha para especificar quaisquer requisitos que você
deseja estabelecer. Os critérios de senha são fornecidos como expressão regular. Para ajudar a determinar a
força ou ver exemplos comuns, consulte [Gerenciando a força da senha](#strength). Clique em **Salvar** para colocar seus requisitos em ação.
  3. Configure **Permitir que os usuários se inscrevam em seu aplicativo** como **Sim**. Ainda
será possível incluir usuários por meio do console se ele estiver configurado como **Não**. No
entanto, é necessário incluir usuários por meio do console apenas para propósitos de desenvolvimento.
  4. Configure **Permitir que os usuários gerenciem suas contas por meio do aplicativo** para
**Sim** se você desejar que os usuários possam reconfigurar a senha, mudar a senha ou
reconfigurar os detalhes. Se quiser limitar o autoatendimento de seus usuários, configure o valor como **Não**.
  5. Clique em **Editar** na linha **Detalhes do remetente** para atualizar suas
configurações de e-mail. As
configurações de e-mail se aplicam a todas as comunicações que são enviadas por meio do {{site.data.keyword.appid_short_notm}}. Especifique
o endereço de e-mail que deve enviar o e-mail, seu nome e deixe um e-mail separado para os usuários enviarem uma resposta.
  6. Ative a **Política de senha avançada** para criar limitações e requisitos de tempo para suas senhas. Esse recurso requer faturamento adicional. Para obter mais informações sobre suas opções, consulte [Política de senha avançada](#advanced-password).
  6. Clique em **Salvar**.

3. Configure as definições de e-mail de verificação.
  1. Para que seus usuários verifiquem seu endereço de e-mail, configure **Verificação de e-mail** como
**Ativado**. Quando um usuário se inscreve em seu aplicativo, ele recebe um e-mail que
solicita a confirmação de que ele se inscreveu no aplicativo.
  2. Se você decidiu que deseja que os usuários verifiquem seus e-mails, sua próxima ação será decidir se os usuários
terão permissão para o seu aplicativo antes da verificação de seus endereços de e-mail. Dependendo da sua preferência, configure
**Permitir que os usuários se inscrevam no aplicativo sem primeiro verificar seu endereço de
e-mail** como **Sim** ou **Não**.
  3. Customize o conteúdo e projete a aparência de sua mensagem. Há um modelo para a mensagem, mas é possível atualizar o texto com sua própria mensagem. É possível usar um [idioma](/docs/services/appid/cloud-directory.html#languages) diferente do inglês, mas você é responsável pela tradução do texto. Para escolher outro idioma, use as <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/updateLocalization" target="_blank">APIs de gerenciamento de idioma <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.
  4. Forneça à URL de verificação um limite de prazo de expiração, especificado em minutos.  Quando esse horário é configurado aqui, ele também afeta o período de tempo em que seu link de reconfiguração de senha é válido.
  5. Insira sua própria URL da página de verificação se tiver uma página específica que queira que os usuários vejam ao clicarem no link. Se você deixar o campo **URL da página de verificação customizada** em branco, uma página de verificação padrão será fornecida pelo {{site.data.keyword.appid_short_notm}}.
  6. Clique em **Salvar**.

4. Defina as configurações de seu e-mail de boas-vindas.
  1. Para dar boas-vindas aos usuários por meio de e-mail quando eles se inscreverem no aplicativo, configure **E-mail de boas-vindas** como **Ativado**.
  2. Customize o conteúdo e projete a aparência de sua mensagem. Há uma mensagem de exemplo que você pode usar, mas é possível atualizar o texto com a sua própria mensagem. É possível usar um [idioma](#languages) diferente do inglês, mas você é responsável pela tradução do texto. Para escolher outro idioma, use as <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/updateLocalization" target="_blank">APIs de gerenciamento de idioma <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.
  3. Clique em **Salvar**.

5. Configure suas definições de reconfiguração de senha.
  1. Para permitir que os usuários solicitem uma reconfiguração de senha, defina **E-mail de senha esquecida** como **Ativado**. **Nota**: um usuário deve ter validado seu e-mail antes de reconfigurar sua senha. Isso
significa que se deve requerer a verificação de e-mail para permitir reconfigurações de senha.
  2. Customize o conteúdo e projete a aparência de sua mensagem. Há uma mensagem de exemplo que você pode usar, mas é possível atualizar o texto com a sua própria mensagem. É possível usar um [idioma](#languages) diferente do inglês, mas você é responsável pela tradução do texto. Para escolher outro idioma, use as <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/updateLocalization" target="_blank">APIs de gerenciamento de idioma <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.
  3. Forneça à URL de reconfiguração de senha um limite de prazo de expiração, especificado em minutos. Quando esse horário é
configurado aqui, ele também afeta o período de tempo em que seu link de verificação de e-mail é válido.
  4. Insira sua própria URL de reconfiguração de senha se você tiver uma página específica que deseja que seus usuários vejam ao clicarem no link. Se
você deixar o campo **Reconfigurar a URL da página de senha** em branco, uma página de reconfiguração
de senha padrão será fornecida pelo {{site.data.keyword.appid_short_notm}}.
  5. Clique em **Salvar**.

6. Configure suas definições de mudança de senha.
  1. Para notificar os usuários sobre quaisquer mudanças feitas em sua senha, configure **E-mail de senha mudada** para **Ativado**.
  2. Customize o conteúdo e projete a aparência de sua mensagem. Há uma mensagem de exemplo que você pode usar, mas é possível atualizar o texto com a sua própria mensagem. É possível usar um [idioma](#languages) diferente do inglês, mas você é responsável pela tradução do texto. Para escolher outro idioma, use as <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/updateLocalization" target="_blank">APIs de gerenciamento de idioma <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.
  3. Clique em **Salvar**.

7. Configure a autenticação de diversos fatores.
  1. Para requerer autenticação de diversos fatores na conexão do usuário, configure **Ativar autenticação de
diversos fatores de e-mail** como **Ativado**.
  2. Customize o conteúdo e o design de seu e-mail usando o modelo abaixo. É possível usar um [idioma](#languages) diferente do inglês, mas você é responsável pela tradução do texto. Para escolher outro idioma, use as <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/updateLocalization" target="_blank">APIs de gerenciamento de idioma <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.
  3. Clique em **Salvar**.

8. Na guia **Usuários**, é possível ver quem se inscreveu no seu aplicativo. Nota: um único usuário pode
tentar se inscrever até 5 vezes em 60 segundos. Se uma sexta tentativa for feita, um erro será exibido.

</br>
</br>

## Tipos de mensagens
{: #types}

É possível enviar vários tipos de mensagens para os usuários. É possível optar por enviar a mensagem de exemplo que é fornecida pelo serviço ou customizar o conteúdo para uma experiência de aplicativo mais pessoal. O
{{site.data.keyword.appid_short_notm}} usa o <a href="https://www.sendgrid.com" target="_blank">SendGrid
<img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> como um serviço de entrega de e-mail. Todos os e-mails são enviados com uma única conta SendGrid.
{: shortdesc}

Se um usuário não fornecer as informações extraídas pelo parâmetro, elas aparecerão em branco.
{: tip}

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
    </table></dd>
  <dt>Senha esquecida</dt>
    <dd><p>Um usuário pode pedir para ter sua senha reconfigurada se ele a esqueceu ou precisa atualizá-la por qualquer razão. É possível customizar a resposta de e-mail para sua solicitação. Quando um usuário solicita uma mudança, a senha permanece como era até que ele clique no link neste e-mail.</p>
    <table>
      <tr>
        <th colspan=2><img src="images/idea.png" alt="Ícone de mais informações"/> Esqueci os parâmetros de senha </th>
      </tr>
      <tr>
        <td><code>%{linkExpiration.hours}</code></td>
        <td> Exibe o número de horas em que o link é válido.</td>
      </tr>
      <tr>
        <td><code>%{linkExpiration.minutes}</code></td>
        <td>Exibe o número de minutos em que o link é válido.</td>
      </tr>
      <tr>
        <td><code>%{resetPassword.code}</code></td>
        <td> Exibe uma senha descartável como parte da URL. Isso significa que cada pessoa teria um código diferente. Exemplo: <code>https://appid.cloud.ibm.com/wfm/verify/6574839563478</code> </td>
      </tr>
      <tr>
        <td><code>%{resetPassword.link}</code></td>
        <td> Exibe o link em que um usuário clica para reconfigurar sua senha. </td>
      </tr>
     </tbody>
  </table></dd>
  <dt>Verificação</dt>
    <dd><p>É possível solicitar que um usuário verifique sua conta via e-mail. Ao solicitar uma verificação, você limita o número de contas falsas que podem se inscrever para seu app. É possível restringir o acesso ao seu app até que um usuário verifique seu e-mail ou o use como uma maneira de gerenciar para quais usuários você cria perfis. Observe
que os usuários que são incluídos manualmente por meio do painel do {{site.data.keyword.appid_short_notm}} ou da API de criação de usuário não recebem automaticamente esse e-mail.</p>
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
    </table></dd>
  <dt>Mudança de senha</dt>
    <dd><p>É possível informar um usuário quando a senha é atualizada. Isso é útil se eles não solicitaram que suas senhas fossem mudadas. Eles podem tomar as medidas adequadas para reafirmar sua conta.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="More information icon"/>  Parâmetros de mudança de senha</th>
      </thead>
      <tbody>
        <tr>
          <td><code>%{passwordChangeInfo.time}</code></td>
          <td> Exibe a hora em que uma nova senha entrou em vigor. </td>
        </tr>
        <tr>
          <td><code>%{passwordChangeInfo.ipAddress}</code></td>
          <td> Exibe o endereço IP do qual a mudança de senha foi solicitada. </td>
        </tr>
      </tbody>
    </table></dd>
    </dd>
    <dt>Código de verificação de MFA</dt>
      <dd><p>Quando a autenticação de diversos fatores é ativada, os usuários podem receber códigos de desafio como um meio
secundário de autenticação.</p>
      <table>
        <thead>
          <th colspan=2><img src="images/idea.png" alt="ícone Mais informações"/> todos os parâmetros de mensagem </th>
        </thead>
        <tbody>
          <tr>
            <td><code>%{mfa.code}</code></td>
            <td> Exibe um código de verificação de MFA único. </td>
          </tr>
        </tbody>
      </table></dd></dl>

</br>
</br>

## Gerenciando a força da
{: #strength}

É possível configurar os requisitos para as senhas que podem ser usadas com o Cloud Directory.
{: shortdesc}

Uma senha forte torna difícil, ou mesmo improvável para alguém adivinhar a senha de uma maneira manual ou automatizada. A força da senha é configurada como uma sequência de expressão regular.

Alguns exemplos comuns de força da senha:

- Deve ter pelo menos oito caracteres. Exemplo de regex: `^.{8,}$`
- Deve conter um número, uma letra minúscula e uma letra maiúscula. Exemplo de expressão regular: `^(?:(?=.*\d)(?=.*[a-z])(?=.*[A-Z]).*)$`
- Deve conter somente letras e números em inglês. Exemplo de regex: `^[A-Za-z0-9]*$`
- Deve ser pelo menos um caractere exclusivo. Exemplo de regex: `^(\w)\w*?(?!\1)\w+$`

A força da senha pode ser configurada na página de configurações do Cloud Directory no console do App ID ou usando <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/set_cloud_directory_password_regex" target="_blank">as APIs de gerenciamento <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.

</br>


## Política de senha avançada
{: #advanced-password}


É possível aprimorar a segurança de seu aplicativo impondo restrições de senha adicionais.
{: shortdesc}


A política de senha avançada consiste em cinco recursos que podem ser alternados separadamente.

 - Bloqueio de acesso após credenciais erradas repetidas
 - Evitar reutilização de senha
 - Expiração de senha
 - Período mínimo entre mudanças de senha
 - Assegure-se de que a senha não inclua o nome do usuário


 Se você ativar esse recurso, o faturamento adicional para recursos de segurança avançados será ativado. Para obter
informações adicionais, consulte a [Calculadora de precificação](faq.html#pricing).

</br>

### Evitar reutilização de senha
{: #avoid-reuse}

Quando os usuários estiverem mudando a senha, talvez você queira evitar que eles escolham uma senha usada
recentemente.
{: shortdesc}

Ao usar a GUI ou a API, é possível escolher o número de senhas que um usuário deve ter antes que possa repetir uma senha usada anteriormente. É possível selecionar qualquer valor inteiro entre 1 e 10.

Se essa opção estiver ativada e um de seus usuários tentar configurar a senha para uma que foi usada recentemente,
um erro será mostrado na conexão padrão na IU do widget e uma senha diferente será solicitada.

As senhas anteriores são armazenadas de forma segura da mesma maneira que a senha atual de um usuário.

</br>

### Bloqueio de acesso após credenciais erradas repetidas
{: #lockout}

Você pode querer proteger as contas de seus usuários bloqueando temporariamente a capacidade de conexão quando um
comportamento suspeito é detectado, como múltiplas tentativas de conexão consecutivas com uma senha incorreta. Essa
medida pode ajudar a evitar que uma parte maliciosa obtenha acesso à conta de um usuário supondo a sua senha.
{: shortdesc}

Usando a GUI ou a API, é possível configurar o número máximo de tentativas de conexão sem sucesso que um
usuário pode fazer antes que sua conta seja temporariamente bloqueada. Também é possível configurar o período de tempo
em que a conta ficará bloqueada. Você tem as opções a seguir:

* Número de tentativas: qualquer valor inteiro entre 1 e 10.
* Período de bloqueio de acesso: qualquer valor inteiro entre 1 minuto e 24 horas, especificado em minutos.

Se uma conta estiver bloqueada, os usuários não poderão se conectar ou executar nenhuma outra operação de
autoatendimento, como mudar sua senha, até que o período de bloqueio de acesso especificado tenha decorrido. Quando o
período de bloqueio de acesso terminar, o usuário será desbloqueado automaticamente.

É possível desbloquear um usuário antes que o período de bloqueio de acesso termine. Para ver se eles estão bloqueados,
veja se o campo `active` está configurado como `false`. Também é possível verificar se seu status na guia **Usuários** do painel de serviço está configurado como `disabled`. Para desbloquear um usuário, deve-se usar [a API](https://appid-management.ng.bluemix.net/swagger-ui/#!/Cloud_Directory_Users/updateCloudDirectoryUser) para configurar o campo `active` como `true`.

</br>

### Período mínimo entre mudanças de senha
{: #minimum-time}

Talvez você queira evitar que os usuários troquem de senha rapidamente configurando um período mínimo de
tempo que eles devem aguardar entre as mudanças de senha.
{: shortdesc}

Esse recurso é especialmente útil quando usado em conjunto com a política "Evitar reutilização de senha". Sem essa
limitação, um usuário poderia simplesmente mudar sua senha várias vezes em sucessão rápida para contornar a
limitação de reutilização de senhas recentes. É possível selecionar qualquer valor entre 1 hora e 30 dias, especificado em horas.

</br>

### Expiração de senha
{: #expiration}

Por motivos de segurança, talvez você queira impor uma política de rotação de senha de modo que seus usuários devam
mudar a senha após um período de tempo.
{: shortdesc}

Ao usar a GUI ou a API, é possível configurar um período de tempo para o qual as senhas do usuário permanecerão válidas. Depois
que a senha de um usuário expirar, eles serão forçados a reconfigurar a senha na próxima conexão. É possível selecionar qualquer número de dias completos entre 1 e 90.

O serviço fornece uma GUI padrão e uma experiência pronta com o widget de login. O usuário é direcionado para fornecer uma nova senha antes que a conexão seja concluída.

Se você estiver usando uma experiência de conexão customizada, um erro será acionado quando um usuário tentar se
conectar com uma senha expirada. É sua responsabilidade configurar o aplicativo para fornecer a experiência do usuário necessária. É possível chamar a API de mudança de senha para configurar a nova senha.

A resposta do terminal do token é semelhante ao seguinte:

```javascript
{
  "error" : "invalid_grant",
  "error_description" : "Password expired",
  "user_id" : "356e065e-49da-45f6-afa3-091a7b464f51"
}
```
{: screen}

Quando essa opção for configurada pela primeira vez, quaisquer senhas de usuário existentes não terão uma data de expiração. O
período de expiração começa para esses usuários quando a senha é mudada. Talvez você queira encorajar os usuários a
atualizar a senha depois de ativar esse recurso.
{: note}

</br>

### Assegure-se de que a senha não inclua o nome do usuário
{: #no-username}

Para senhas mais fortes, talvez você queira evitar os usuários que contenham seu nome de usuário ou a primeira
parte de seu endereço de e-mail.
{: shortdesc}

Essa restrição não faz distinção entre maiúsculas e minúsculas, o que significa que os usuários não podem alterar maiúsculas e minúsculas de alguns ou de todos os caracteres para usar informações pessoais. Para
configurar essa opção, mude o comutador para **ativo**.

</br>

## Usando um remetente de e-mail customizado
{: #custom-email}

Com o {{site.data.keyword.appid_short_notm}}, é possível definir um ponto de extensão customizado para enviar suas mensagens de e-mail do Cloud Directory. Ao definir um ponto de extensão, você tem o controle total de como os e-mails são enviados e é possível usar seu próprio nome de domínio.
 {: shortdesc}

**Por que eu desejaria usar um emissor de e-mail customizado?**

Por padrão, o {{site.data.keyword.appid_short_notm}} usa o SendGrid para entregar mensagens em seu nome. Ao
configurar seu próprio emissor de e-mail customizado, é possível aprimorar ainda mais a experiência com marca para os
usuários do seu aplicativo.

Alguns exemplos mais específicos:
- **Domínio personalizado**
Configurando um dispatcher de e-mail customizado, você tem controle total sobre como as mensagens de e-mail são
enviadas. Isso inclui a customização do domínio de e-mail que pode reduzir ainda mais as chances de os e-mails serem
filtrados como spam.
- **Insights e resolução de problemas**
Obtenha insights de seu provedor de e-mail, como: o número de pessoas que abriram os e-mails ou quais mensagens não foram entregues. Como é possível rastrear mensagens individuais e ver estatísticas gerais, isso pode ajudar a resolver problemas.

</br>

** Como ele funciona? **

Depois que o ponto de extensão for configurado, ele será chamado pelo {{site.data.keyword.appid_short_notm}}
sempre que uma mensagem de e-mail precisar ser enviada. O ponto de extensão contém todas as informações sobre a mensagem, incluindo o conteúdo final do corpo do e-mail.

</br>

**Para criar um emissor de e-mail customizado:**

1. Para configurar a instância do {{site.data.keyword.appid_short_notm}} para usar o dispatcher customizado, use <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/set_cloud_directory_email_dispatcher" target="_blank">a API de gerenciamento </a>.</br>
Deve-se fornecer a URL. Além disso, é possível fornecer informações de autorização. Os tipos de autorização suportados são: `Basic authorization` ou um `constant authorization header value`.

  Exemplos de configuração válida:
  ```
  {
    "custom": {
      "url": "https://example.com/send_mail"
    }
  }
  ```
  {: screen}

  ```
  {
    "custom": {
      "url": "https://example.com/send_mail", "authorization": {
        "type": "basic",
        "username": "username",
        "password": "password"
      }
    }
  }
  ```
  {: screen}

  ```
  {
    "custom": {
      "url": "https://example.com/send_mail", "authorization": {
        "type": "value",
        "value": "myApiKey"
      }
    }
  }
  ```
  {: screen}

2. Configure um ponto de extensão que possa atender à solicitação de post. Esse terminal deve ser capaz de ler a carga útil
que vem do {{site.data.keyword.appid_short_notm}} e enviar o e-mail com o emissor de e-mail customizado.

3. O corpo enviado do {{site.data.keyword.appid_short_notm}} está no formato a seguir: `{"jws": "jws-format-string"}`. </br> Após decodificar e verificar a carga útil, o conteúdo será uma sequência JSON.</br>
  ```
    {
      "tenant": "tenant-id",
      "iss" : "us-south.appid.cloud.ibm.com","iss" : "appid-oauth.ng.bluemix.net",
      "iat": 1539173126,
      "jti": "uniq-id",
      "message": {
          "to": "your@mail.com",
          "from": {
              "name": "My Awesome Service",
              "address": "no-reply@company.com"
          },
          "replyTo": {
              "name": "My Awesome Service",
              "address": "yes-reply@company.com"
          },
          "subject": "Welcome to My Awesome Service",
          "body": "<p>Hello<p><br/><p>Thanks for signing up John Doe</p>"
      }
    }
  ```
  {: screen}

  - tenant: ID do locatário da instância do App ID
  - iat: registro de data e hora de quando a mensagem foi enviada
  - iss: identifica o principal que emitiu o JWS.
  - jti: identificador de transação exclusivo
  - message: mensagem a enviar, consiste nos seguintes campos:
    - to: endereço de e-mail do destinatário
    - from: informações do remetente, consiste nos seguintes campos:
      - nome: opcional, nome do remetente
      - address: endereço do remetente
    - reply to: opcional, consiste nos campos a seguir:
      - nome: opcional, nome do remetente
      - address: opcional, endereço do remetente
    - subject: assunto do e-mail
    - body: corpo de e-mail, em formato HTML

  É possível verificar se a sua solicitação foi bem-sucedida verificando o código de status de resposta. Qualquer coisa no
intervalo de 200 a 299 é considerada um sucesso. Se você receber qualquer outra resposta, tente fazer sua
solicitação novamente.
  {: tip}

4. Cada carga útil HTTP que é enviada do {{site.data.keyword.appid_short_notm}} é automaticamente assinada de
acordo com o padrão JWS usando um par de chaves assimétricas.
Para cada instância do {{site.data.keyword.appid_short_notm}}, uma chave privada e uma pública não
compartilhadas entre outras instâncias são geradas. A chave privada é usada para assinar a carga útil HTTP e será
possível usar a chave pública para verificar se a carga útil é gerada pelo {{site.data.keyword.appid_short_notm}} e não alterada por um terceiro, <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#!/Authorization_Server_V3/publicKeys" target="_blank">Terminal de chaves públicas </a>.

5. Código de exemplo para o ponto de extensão (JavaScript)
  ```
  const sgMail = require('@sendgrid/mail');
  const {promisify} = require('bluebird');
  const request = promisify(require('request'));
  const jwtVerify = promisify(require('jsonwebtoken').verify);
  const jwtDecode = require('jsonwebtoken').decode;
  const jwkToPem = require('jwk-to-pem');

  async function obtainPublicKeys() {
  	// Your App ID instance tenant ID
  	const tenantId = '<TENANT-ID>';

  	// Send request to App ID's public keys endpoint
  	const keysOptions = {
  		method: 'GET',
  		url: `https://appid-oauth.<REGION>.bluemix.net/oauth/v3/${tenantId}/publickeys`
  	};
  	const keysResponse = await request(keysOptions);
  	return JSON.parse(keysResponse.body).keys;
  }

  async function verifySignature(keysArray, kid, jws) {
  	const keyJson = keysArray.find(key => key.kid === kid);
  	if (keyJson) {
  		const pem = jwkToPem(keyJson);
  		await jwtVerify(jws, pem);
  		return;
  	}
  	throw new Error ("Unable to verify signature");
  }

  async function verifyAndSendMail(jws) {
  	// The API key for Sendgrid
  	const sgApiKey = '<SENDGRID-API-KEY>';

  	// Init Sendgrind
  	sgMail.setApiKey(sgApiKey);

  	// Decode message to get information
  	const data = jwtDecode(jws, {complete: true});

  	// Extract kid from header
  	const kid = data.header.kid;

  	const keysArray = await obtainPublicKeys();

  	// Verify the signature of the payload with the public keys
  	await verifySignature(keysArray, kid ,jws);

  	// Send the email with Your Sendgrid account
  	const message = data.payload.message;
  	const msg = {
  		to: message.to,
  		from: message.from.address,
  		subject: message.subject,
  		html: message.body,
  	};
  	console.log(`Sending email to ${message.to}`);
  	let sendgridResponse = await sgMail.send(msg);

  	return {result : 'email_sent',sendgridResponse};
  }
  ```
  {: codeblock}

6. Verifique se a configuração está corretamente configurada testando seu dispatcher de e-mail. Use a <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/post_email_dispatcher_test" target="_blank">API de teste</a> para acionar uma solicitação para o remetente de e-mail customizado configurado.

Para obter o exemplo de trabalho completo, consulte <a href="https://www.ibm.com/blogs/bluemix/2018/10/use-ibm-cloud-app-id-and-your-email-provider-to-brand-mails-sent-to-app-users/" target="_blank">Usar seu próprio provedor para e-mail enviado com o {{site.data.keyword.appid_full}}</a>.

</br>
</br>


## Migrando usuários
{: #user-migration}

Ocasionalmente, pode ser necessário configurar uma nova instância do {{site.data.keyword.appid_short_notm}}. Se
você estiver usando o Cloud Directory, isso significará que seus usuários devem ser migrados para a nova instância. É possível usar as APIs de gerenciamento para ajudar com a migração.
{: shortdesc}

### Antes de iniciar

A [função do IAM](/docs/iam/quickstart.html) `Manager` deve estar designada a você para as duas instâncias do {{site.data.keyword.appid_short_notm}}.

</br>

**Exportando**

Antes de ser possível incluir os usuários na nova instância, é necessário exportá-los da instância atual. Para fazer isso, é possível usar a <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Cloud_Directory_Users/cloudDirectoryExport" target="_blank">API de gerenciamento de exportação <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.

Comando cURL de exemplo:

```
curl -X GET --header ‘Accept: application/json’ --header ‘Authorization: Bearer <iam-token>’ ’https://eu-gb.appid.cloud.ibm.com/management/v4/111c9bj3-xxxx-4b5b-zzzz-24ad9440k8j9/cloud_directory/export?encryption_secret=myCoolSecret'
```
{: codeblock}

<table>
  <tr>
    <th>Variável</th>
    <th>Descrição</th>
  </tr>
  <tr>
    <td><code>encryption_secret</code></td>
    <td>Uma sequência customizada que é usada para criptografar e decriptografar uma senha em hash do usuário.</td>
  </tr>
  <tr>
    <td><code> tenantID </code></td>
    <td>O ID do locatário de serviço pode ser localizado em suas credenciais de serviço. É possível localizar suas credenciais de serviço no painel do App ID.</td>
  </tr>
</table>

Somente os usuários do Cloud Directory e seus perfis são retornados. Os usuários de outros provedores de identidade não são.
{: note}

</br>

**Importando**

Agora que seus usuários estão prontos, é possível importar suas informações para a nova instância. Para fazer isso, é possível usar a <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Cloud_Directory_Users/cloudDirectoryImport" target="_blank">API de gerenciamento de importação <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.

Comando cURL de exemplo:

```
curl -X POST --header ‘Content-Type: application/json’ --header ‘Accept: application/json’ --header ‘Authorization: Bearer <iam-token>’ -d ‘{“users”: [
    {
      “scimUser”: {
        “originalId”: “3f3f6779-7978-4383-926f-a43aef3b724b”,
        “name”: {
          “givenName”: “<first-name>”,
          “familyName”: “<last-name>”,
          “formatted”: “<first-name> <last-name>”
        },
        “displayName”: “<first-name>”,
        “emails”: [
          {
            “value”: “<user>@gmail.com”,
            “primary”: true
          }
        ],
        “status”: “PENDING”
      },
      “passwordHash”: “<password hash here>“,
      “passwordHashAlg”: “<password hash algorithm>",
      “profile”: {
        “attributes”: {}
      }
    }
]}’ ‘https://eu-gb.appid.cloud.ibm.com/management/v4/111c9bj3-xxxx-4b5b-zzzz-24ad9440k8j9/cloud_directory/import?encryption_secret=myCoolSecret’
```
{: codeblock}

</br>

### Usando o script de migração

O {{site.data.keyword.appid_short_notm}} fornece um script de migração que pode ser usado por meio da CLI que pode ajudar a acelerar o processo de migração.

Antes de iniciar, certifique-se de ter as informações de parâmetro a seguir:

<table>
  <tr>
    <th>Parâmetro</th>
    <th>Descrição</th>
  </tr>
  <tr>
    <td><code>sourceTenantId</code></td>
    <td>O ID do locatário da instância do {{site.data.keyword.appid_short_notm}} da qual você planeja exportar os usuários.</td>
  </tr>
  <tr>
    <td><code>destinationTenantId</code></td>
    <td>O ID do locatário da instância do {{site.data.keyword.appid_short_notm}} para a qual você planeja importar os usuários.</td>
  </tr>
  <tr>
    <td>Região</td>
    <td>As opções atuais incluem: Sul do EUA: <code>ng</code>, Londres: <code>eu-gb</code>, Sydney: <code>au-syd</code>, Washington: <code>us-east</code> e Alemanha: <code>eu-de</code>.</td>
  </tr>
  <tr>
    <td>Token do IAM</td>
    <td>Certifique-se de ter as permissões de <code>manager</code> antes de obter o token. Para ajuda para obter um token do IAM, consulte <a href="https://console.bluemix.net/docs/iam/apikey_iamtoken.html#iamtoken_from_apikey" target="_blank">os docs <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.</td>
  </tr>
</table>

Para executar o script:

1. Clone o <a href="https://github.com/ibm-cloud-security/appid-sample-code-snippets/tree/master/export-import-cloud-directory-users" target="_blank">repositório <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.
2. Abra o terminal e navegue para a pasta na qual você clonou o repositório.
3. Execute o comando a seguir.

  ```
  npm install
  ```
  {: codeblock}

4. Com seus parâmetros, execute o comando a seguir.

  ```
  users_export_import 'sourceTenantId' 'destinationTenantId' 'region' 'iamToken'
  ```
  {: codeblock}

  Exemplo de comando:

  ```
  users_export_import e00a0366-53c5-4fcf-8fef-ab3e66b2ced8 73321c2b-d35a-497a-9845-15c580fdf58c ng eyJraWQiOiIyMDE3MTAyNS0xNjoyNzoxMCIsImFsZyI6IlJTMjU2In0.eyJpYW1faWQiOiJJQk1pZC0zMTAwMDBUNkZTIiwiaWQiOiJJQk1pZC0zMTAwMDBUNkZTIiwicmVhbG1pZCI6IklCTWlkIiwiaWRlbnRpZmllciI6IjMxMDAwMFQ2RlMiLCJnaXZlbl9uYW1lIjoiUm90ZW0iLCJmYW1pbHlfbmFtZSI6IkJyb3NoIiwibmFtZSI6IlJvdGVtIEJyb3NoIiwiZW1haWwiOiJyb3RlbWJyQGlsLmlibS5jb20iLCJzdWIiOiJyb3RlbWJyQGlsLmlibS5jb20iLCJhY2NvdW50Ijp7ImJzcyI6ImQ3OWM5YTk5NjJkYzc2Y2JkMDZlYTVhNzhjMjY0YzE5In0sImlhdCI6MTUzNzE3Mjg4NCwiZXhwIjoxNTM3MTc2NDg0LCJpc3MiOiJodHRwczovL2lhbS5zdGFnZTEuYmx1ZW1peC5uZXQvaWRlbnRpdHkiLCJncmFudF90eXBlIjoidXJuOmlibTpwYXJhbXM6b2F1dGg6Z3JhbnQtdHlwZTpwYXNzY29kZSIsInNjb3BlIjoiaWJtIG9wZW5pZCIsImNsaWVudF9pZCI6ImJ4IiwiYWNyIjoxLCJhbXIiOlsicHdkIl19.c4vLPzhvvNZLjaLy7znDa37qV4o-yuGmSKmJoQKrEQNZU8IC0NIjxwSo7W9kb0pDi3Yf_03_9ufTTGNfjtltzNWycSXjkNgoL-b9_nU61oHdgn0stY1KmNicqyBWfgUU--4xa904QN_QjRHBaUBeJf3XWEphPIMoF7mZeOxEZLnCMcQXSz9pImCMiP4SNT38cHLiI90Yx01rM7hpteepWULh5MYh-B2V03Gkgxfqvv951HF1LDg6eT4Q9in11laTQKtKuomripUju_4GIIjORVYw9NaAVKIJ9lKrPX0SKPhStsa59qGsC_7Uersms5EY1W1VbZVqOZPJbtp6tVf-Lw
  ```
  {: codeblock}

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
