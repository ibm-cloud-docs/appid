---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-11"

keywords: authentication, authorization, identity, app security, secure, directory, registry, passwords, languages, lockout

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

# Customizando e-mails
{: #cd-types}

Quando um usuário interage com seu aplicativo, há momentos em que você pode desejar enviar uma resposta ou solicitar uma verificação. O {{site.data.keyword.appid_short_notm}} fornece modelos padrão que podem ser usados para as interações. Também é possível usar os modelos como um guia e customizar seu sistema de mensagens para se ajustar à sua marca.
{: shortdesc}

O
{{site.data.keyword.appid_short_notm}} usa o <a href="https://www.sendgrid.com" target="_blank">SendGrid
<img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> como um serviço de entrega de e-mail. Todos os e-mails são enviados com uma única conta SendGrid.
{: note}

## Modelos de e-mail
{: #cd-messages}

Quando você envia mensagens para seus usuários, é possível usar qualquer combinação dos modelos a seguir. Ou, é possível editar os modelos para customizar sua mensagem.
{: shortdesc}

Além dos tipos de mensagens a seguir, também é possível aproveitar os modelos [SSO](/docs/services/appid?topic=appid-cd-sso#cd-sso) e [MFA](/docs/services/appid?topic=appid-cd-mfa#cd-mfa).
{: tip}

É possível usar parâmetros em suas mensagens para customizar ainda mais as mensagens. Efetue o registro de saída da tabela a seguir para ver os parâmetros que podem ser usados em todos os tipos de mensagens.

<table>
  <tr>
    <th colspan=2><img src="images/idea.png" alt="ícone Mais informações"/> todos os parâmetros de mensagem </th>
  </tr>
  <tr>
    <td><code>%{display.logo}</code></td>
    <td> Exibe a imagem que você configurou para o widget de login.</td>
  </tr>
  <tr>
    <td><code>%{user.displayName}</code></td>
    <td> Exibe o nome da tela que um usuário escolheu usar ao interagir com o app.</td>
  </tr>
  <tr>
    <td><code>%{user.email}</code></td>
    <td> Exibe o endereço de e-mail do usuário registrado.</td>
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
</table>


### E-mail: Bem-vindo
{: #cd-messages-welcome}

Quando um usuário se conecta a seu aplicativo, você pode desejar enviar a eles uma mensagem que os recebe em seu app.
{: shortdesc}

1. Navegue para a guia **Modelos de Fluxo de Trabalho >E-mail de Boas-vindas**do painel de serviço.

2. Configure **E-mail de boas-vindas** para **Ativado**.

3. Customize o conteúdo de sua mensagem. É possível incluir parâmetros e inserir imagens usando a IU. Para mudar o [idioma](/docs/services/appid?topic=appid-cd-messages#cd-languages) da mensagem, é possível usar <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">as APIs <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> para configurar o idioma. No entanto, você é responsável pelo conteúdo e pela tradução da mensagem. Consulte a tabela a seguir para ver a lista de tabelas que podem ser usadas nessa mensagem e todas as outras mensagens que podem ser enviadas. Se um usuário não fornecer as informações extraídas pelo parâmetro, elas aparecerão em branco.

4. Clique em **Salvar**.


### E-mail: Verificação
{: #cd-messages-verification}

Quando um usuário se conecta a seu aplicativo usando seu e-mail, é possível enviar um e-mail solicitando que ele confirme sua identidade. Ao solicitar uma verificação, você limita o número de contas falsas que podem se inscrever para seu app. É possível restringir o acesso ao seu app até que um usuário verifique seu e-mail ou o use como uma maneira de gerenciar para quais usuários você cria perfis. Observe
que os usuários que são incluídos manualmente por meio do painel do {{site.data.keyword.appid_short_notm}} ou da API de criação de usuário não recebem automaticamente esse e-mail.
{: shortdesc}


1. Navegue para a guia **Modelos de fluxo de trabalho > Verificação de e-mail** do painel de serviço.

2. Configure **Verificação de e-mail** para **Ativado**.

3. Configure **Permitir que os usuários se conectem ao seu aplicativo sem primeiro verificar seu endereço de e-mail** como **Sim**. Quando configurado como sim, os usuários são capazes de interagir com seu aplicativo após se conectarem, mas antes de terem verificado seu endereço de e-mail. A configuração padrão é não.

4. Customize o conteúdo de sua mensagem. É possível incluir parâmetros e inserir imagens usando a IU. Para mudar o [idioma](/docs/services/appid?topic=appid-cd-messages#cd-languages) da mensagem, é possível usar <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">as APIs <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> para configurar o idioma. No entanto, você é responsável pelo conteúdo e pela tradução da mensagem. Consulte a tabela a seguir para ver os diferentes parâmetros que podem ser usados nessa mensagem. Se um usuário não fornecer as informações extraídas pelo parâmetro, elas aparecerão em branco.

  <table>
    <tr>
      <th colspan=2><img src="images/idea.png" alt="More information icon"/>  Parâmetros de mensagem de verificação</th>
    </tr>
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
  </table>

  Também é possível usar os parâmetros de mensagem listados na seção [Mensagem de boas-vindas](/docs/services/appid?topic=appid-cd-messages#cd-messages-welcome).
  {: tip}

5. Defina um prazo de expiração para a URL de ação. A expiração da URL é a quantidade de tempo, em minutos, que um usuário tem que concluir a ação antes que o link de verificação expire. Essa configuração também afeta a quantidade de tempo que seu link de reconfiguração de senha é válido.
 
6. Insira uma URL para a página que você deseja exibir após um usuário verificar seu e-mail na caixa **URL da página de agradecimento**. Se você optar por deixar esse campo em branco, uma página {{site.data.keyword.appid_short_notm}} padrão será exibida.

7. Clique em **Salvar**. 


### E-mail: Reconfigurar senha
{: #cd-messages-reset}

Quando um usuário interage com seu aplicativo, eles podem esquecer sua senha ou ter outra necessidade de atualizá-lo. É possível customizar a resposta de e-mail para sua solicitação. Quando um usuário solicita uma mudança em sua senha, a senha permanece inalterada até que ele clique no link nesse e-mail.
{: shortdesc}


1. Navegue para a guia **Modelos de fluxo de trabalho > Reconfigurar senha** do painel de serviço.

2. Configure **E-mail de senha esquecida** para **Ativado**.

3. Customize o conteúdo de sua mensagem. É possível incluir parâmetros e inserir imagens usando a IU. Para mudar o [idioma](/docs/services/appid?topic=appid-cd-messages#cd-languages) da mensagem, é possível usar <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">as APIs <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> para configurar o idioma. No entanto, você é responsável pelo conteúdo e pela tradução da mensagem. Consulte a tabela a seguir para ver os diferentes parâmetros que podem ser usados nessa mensagem. Se um usuário não fornecer as informações extraídas pelo parâmetro, elas aparecerão em branco.

  <table>
    <tr>
      <th colspan=2><img src="images/idea.png" alt="Ícone de mais informações"/> Esqueci os parâmetros de senha</th>
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
      <td> Exibe uma senha descartável como parte da URL. Isso significa que cada pessoa teria um código diferente. Exemplo: <code>https://us-south.appid.cloud.ibm.com/wfm/verify/6574839563478</code></td>
    </tr>
    <tr>
      <td><code>%{resetPassword.link}</code></td>
      <td> Exibe o link em que um usuário clica para reconfigurar sua senha.</td>
    </tr>
  </table>

  Também é possível usar os parâmetros de mensagem listados na seção [Mensagem de boas-vindas](/docs/services/appid?topic=appid-cd-messages#cd-messages-welcome).
  {: tip}

4. Defina um prazo de expiração para a URL de ação. A expiração da URL é a quantidade de tempo, em minutos, que um usuário tem que concluir a ação antes que o link de verificação expire. Essa configuração também afeta a quantidade de tempo que seu link de reconfiguração de senha é válido.
 
5. Insira uma URL para a página que você deseja exibir após um usuário verificar seu e-mail na caixa **URL da página de reconfiguração de senha**. Se você optar por deixar esse campo em branco, uma página {{site.data.keyword.appid_short_notm}} padrão será exibida.

6. Clique em **Salvar**.


### E-mail: mudança de senha
{: #cd-messages-password-change}

É possível informar um usuário quando a senha é atualizada. Isso é útil se eles não solicitaram que suas senhas fossem mudadas. Eles podem tomar as medidas adequadas para reafirmar sua conta.
{: shortdesc}

1. Navegue para a guia **Modelos de fluxo de trabalho > Mudança de senha** do painel de serviço.

2. Configure **E-mail de senha mudada** para **Ativado**.

3. Customize o conteúdo de sua mensagem. É possível incluir parâmetros e inserir imagens usando a IU. Para mudar o [idioma](/docs/services/appid?topic=appid-cd-messages#cd-languages) da mensagem, é possível usar <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">as APIs <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> para configurar o idioma. No entanto, você é responsável pelo conteúdo e pela tradução da mensagem. Consulte a tabela a seguir para ver os diferentes parâmetros que podem ser usados nessa mensagem. Se um usuário não fornecer as informações extraídas pelo parâmetro, elas aparecerão em branco.

  <table>
    <tr>
      <th colspan=2><img src="images/idea.png" alt="More information icon"/>  Parâmetros de mudança de senha</th>
    </tr>
    <tr>
      <td><code>%{passwordChangeInfo.time}</code></td>
      <td> Exibe a hora em que uma nova senha entrou em vigor. </td>
    </tr>
    <tr>
      <td><code>%{passwordChangeInfo.ipAddress}</code></td>
      <td> Exibe o endereço IP do qual a mudança de senha foi solicitada. </td>
    </tr>
  </table>

  Também é possível usar os parâmetros de mensagem listados na seção [Mensagem de boas-vindas](/docs/services/appid?topic=appid-cd-messages#cd-messages-welcome).
  {: tip}

4. Clique em **Salvar**.




## Usando um remetente de e-mail customizado
{: #cd-custom-email}

Com o {{site.data.keyword.appid_short_notm}}, é possível definir um ponto de extensão customizado para enviar suas mensagens de e-mail do Cloud Directory. Ao definir um ponto de extensão, você tem o controle total de como os e-mails são enviados e é possível usar seu próprio nome de domínio. Por padrão, o {{site.data.keyword.appid_short_notm}} usa o <a href="https://www.sendgrid.com" target="_blank">SendGrid <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> como um serviço de entrega de mensagem.
 {: shortdesc}

Você pode desejar usar um remetente de e-mail customizado pelos motivos a seguir:

- **Domínio personalizado**
Configurando um dispatcher de e-mail customizado, você tem controle total sobre como as mensagens de e-mail são
enviadas. Isso inclui a customização do domínio de e-mail que pode reduzir ainda mais as chances de os e-mails serem
filtrados como spam. Também é possível aprimorar ainda mais a experiência de marca para os usuários do app.

- **Insights e resolução de problemas**
Obtenha insights de seu provedor de e-mail, como: o número de pessoas que abriram os e-mails ou quais mensagens não foram entregues. Como é possível rastrear mensagens individuais e ver estatísticas gerais, isso pode ajudar a resolver problemas.

Depois que o ponto de extensão for configurado, ele será chamado pelo {{site.data.keyword.appid_short_notm}}
sempre que uma mensagem de e-mail precisar ser enviada. O ponto de extensão contém todas as informações sobre a mensagem, incluindo o conteúdo final do corpo do e-mail.



### Configurando o remetente customizado
{: #cd-messages-configure-custom-sender}

Para configurar seu remetente de e-mail customizado, deve-se usar a <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.set_cloud_directory_email_dispatcher" target="_blank">API de gerenciamento</a> do Cloud Directory.


1. Forneça a URL. Além disso, é possível fornecer informações de autorização. Os tipos de autorização suportados são: `Basic authorization` ou `constant authorization header value`.

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

3. O corpo enviado do {{site.data.keyword.appid_short_notm}} está no formato a seguir: `{"jws": "jws-format-string"}`. Após decodificar e verificar a carga útil, o conteúdo será uma sequência JSON.

  ```
    {
      "tenant": "tenant-id",
      "iss" : "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61", 
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

  <table>
    <tr>
      <th>Variável</th>
      <th>Descrição</th>
    </tr>
    <tr>
      <td><code> tenant </code></td>
      <td>O ID do locatário de sua instância do {{site.data.keyword.appid_short_notm}}.</td>
    </tr>
    <tr>
      <td><code> iat </code></td>
      <td>O registro de data e hora de quando a mensagem enviada.</td>
    </tr>
    <tr>
      <td><code>jss</code></td>
      <td>O princípio que emitiu o token JWS.</td>
    </tr>
    <tr>
      <td><code>jti</code></td>
      <td>O ID da transação exclusivo.</td>
    </tr>
    <tr>
      <td><code>message: to</code></td>
      <td>O endereço de e-mail do destinatário da mensagem.</td>
    </tr>
    <tr>
      <td><code>mensagem: de</code></br><code>nome</code></br><code>endereço</code></td>
      <td></br>O nome do emissor da mensagem.</br>O endereço de email do remetente.</td>
    </tr>
    <tr>
      <td><code>Opcional: message: reply to</code></br><code>name</code></br><code>address</code></td>
      <td></br>O nome que está anexado ao endereço de email de resposta.</br>O endereço de e-mail para o qual um usuário pode responder.</td>
    </tr>
  </table>

  É possível verificar se a sua solicitação foi bem-sucedida verificando o código de status de resposta. Qualquer coisa no intervalo de 200 a 299 é considerada um sucesso. Se você receber qualquer outra resposta, tente fazer sua
solicitação novamente.
  {: tip}

4. Cada carga útil HTTP que é enviada do {{site.data.keyword.appid_short_notm}} é automaticamente assinada de
acordo com o padrão JWS usando um par de chaves assimétricas.
Para cada instância do {{site.data.keyword.appid_short_notm}}, uma chave privada e uma pública não
compartilhadas entre outras instâncias são geradas. A chave privada é usada para assinar a carga útil HTTP e será
possível usar a chave pública para verificar se a carga útil é gerada pelo {{site.data.keyword.appid_short_notm}} e não alterada por um terceiro, <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#!/Authorization_Server_V4/publicKeys" target="_blank">Terminal de chaves públicas </a>.

5. Código de exemplo para o ponto de extensão (JavaScript).
  ```
  const sgMail = require('@sendgrid/mail');
  const {promisify} = require('bluebird');
  const request = promisify(require('request'));
  const jwtVerify = promisify(require('jsonwebtoken').verify);
  const jwtDecode = require('jsonwebtoken').decode;
  const jwkToPem = require('jwk-to-pem');

  async function obtainPublicKeys() {
  	// Seu ID do locatário da instância do {{site.data.keyword.appid_short_notm}}
  	const tenantId = '<TENANT-ID>';

  	// Enviar solicitação para o terminal de chaves públicas do {{site.data.keyword.appid_short_notm}}
  	const keysOptions = {
  		method: 'GET',
  		url: `https://<REGION>.appid.cloud.ibm.com/oauth/v4/${tenantId}/publickeys`
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
  {: screen}

6. Verifique se a configuração está corretamente configurada testando seu dispatcher de e-mail. Use a <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Config/post_email_dispatcher_test" target="_blank">API de teste</a> para acionar uma solicitação para o remetente de e-mail customizado configurado.

Para obter o exemplo de trabalho completo, consulte <a href="https://www.ibm.com/blogs/bluemix/2018/10/use-ibm-cloud-app-id-and-your-email-provider-to-brand-mails-sent-to-app-users/" target="_blank">Usar seu próprio provedor para e-mail enviado com o {{site.data.keyword.appid_full}}</a>.



## Idiomas Suportados
{: #cd-languages}

É possível usar <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">as APIs de gerenciamento de idioma <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> para configurar o idioma no qual a comunicação do usuário pode ser escrita. No entanto, somente o inglês está prontamente disponível para uso. Você é responsável pela tradução das mensagens. Depois de definir a configuração com a API, a GUI é atualizada para que você possa mudar o texto do modelo.
{: shortdesc}

<table>
  <col width="20%">
  <col width="25%">
  <col width="35%">
  <tr>
    <th>Código</th>
    <th>idioma</th>
    <th>Região</th>
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
    <td>Marrocos</td>
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
    <td>Macao SAR do PRC</td>
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
    <td>Macao SAR do PRC</td>
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
