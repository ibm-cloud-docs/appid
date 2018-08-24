---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Sobre
{: #about}

A segurança do aplicativo pode ser muito complicada. Para a maioria dos desenvolvedores, é uma das partes mais difíceis da criação de um app. Como você pode garantir que está protegendo as informações do usuário? Ao integrar o {{site.data.keyword.appid_full}} em seus aplicativos, é possível proteger os recursos e incluir a autenticação, mesmo quando você não tem muita experiência em segurança.
{:shortdesc}


## Razões para usar o serviço
{: #reasons}

O {{site.data.keyword.appid_short_notm}} ajuda os desenvolvedores a incluir facilmente a autenticação nos aplicativos móveis e da web com poucas linhas de código e a proteger os aplicativos e os serviços nativos de nuvem no {{site.data.keyword.Bluemix_notm}}. Ao requerer que os usuários se conectem ao seu aplicativo, é possível armazenar os dados do usuário, como as preferências do aplicativo ou as informações de perfis sociais públicos e, então, aproveitar esses dados para customizar a experiência de cada usuário dentro do aplicativo. O {{site.data.keyword.appid_short_notm}} fornece uma estrutura de login, mas também é possível trazer as suas telas de conexão de marca para usar com o diretório da nuvem.
{: shortdesc}

Por que você deseja usar o {{site.data.keyword.appid_short_notm}}? Confira os cenários a seguir para ver se algum deles se aplica a você.

<table>
  <tr>
    <th>Cenário</th>
    <th>Solução</th>
  </tr>
  <tr>
    <td>É necessário incluir [autorização e autenticação](/docs/services/appid/authorization.html) em seus apps móveis e da web, mas não há um plano de fundo de segurança.</td>
    <td>O {{site.data.keyword.appid_short_notm}} facilita a inclusão de uma etapa de autenticação em seus apps. É possível incluir a conexão por e-mail ou por nome do usuário, a conexão social ou a conexão corporativa nos aplicativos com as APIs, os SDKs, as UIs pré-construídas ou as suas próprias UIs de marca.</td>
  </tr>
  <tr>
    <td>Você deseja limitar o acesso aos seus apps e recursos de backend.</td>
    <td>É possível proteger facilmente os aplicativos, os recursos de backend e as APIs usando a autenticação baseada em padrões fornecida pelo {{site.data.keyword.appid_short_notm}}.</td>
  </tr>
  <tr>
    <td>Você deseja construir experiências de app personalizadas para seus usuários.</td>
    <td>Com o {{site.data.keyword.appid_short_notm}}, é possível [armazenar dados do usuário](/docs/services/appid/user-profile.html) como preferências de app ou informações de seus perfis sociais públicos e, em seguida, usar esses dados para customizar cada experiência de seu app.</td>
  </tr>
  <tr>
    <td>Você deseja gerenciar os usuários de uma maneira escalável.</td>
    <td> O {{site.data.keyword.appid_short_notm}} permite criar um [Cloud Directory](/docs/services/appid/cloud-directory.html), que possibilita incluir a inscrição e a conexão do usuário nos aplicativos. O Cloud Directory fornece a estrutura para manter um registro do usuário que pode escalar com a sua base de usuários. Com a funcionalidade pré-construída para autoatendimento, como verificação de e-mail e reconfigurações de senha, é possível ter certeza que seu app está autenticando usuários com segurança.</td>
  </tr>
</table>


## Integrações
{: #integrations}

É possível usar o {{site.data.keyword.appid_short_notm}} com outras ofertas do {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}


<dl>
  <dt>{{site.data.keyword.containerlong_notm}}</dt>
    <dd>Configurando o ingresso em um cluster padrão, é possível proteger seus apps no nível do cluster. Consulte a postagem do blog <a href="/docs/containers/cs_annotations.html#appid-auth">{{site.data.keyword.appid_short_notm}}Anotação de ingresso de autenticação</a> ou <a href="https://www.ibm.com/blogs/bluemix/2018/05/announcing-app-id-integration-ibm-cloud-kubernetes-service/">Anunciando a integração do ID do app no IBM Cloud Kubernetes Service <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> para obter uma introdução.</dd>
  <dt>{{site.data.keyword.openwhisk}} e API Connect</dt>
    <dd>Quando você cria suas APIs com o [{{site.data.keyword.openwhisk_short}}](/docs/openwhisk/index.html) e o [API Connect](/docs/apis/management/manage_apis.html), é possível proteger seus aplicativos no gateway em vez de em seu código de app. Para ver a integração em ação, veja <a href="https://www.youtube.com/watch?v=Fa9YD2NGZiE" target="_blank">Login social simples e rápido OAUTH com APIC e {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.</dd>
  <dt>Cloud Foundry</dt>
    <dd>Experimente um dos nossos aplicativos de amostra do Cloud Foundry para ver como é possível integrar o
{{site.data.keyword.appid_short_notm}} em seus aplicativos.</dd>
  <dt>Guia de Programação do iOS</dt>
    <dd>Você desenvolve apps para a Apple? Experimente o <a href="https://console.bluemix.net/docs/swift/index.html#overview" target="_blank">Guia de programação do iOS<img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"> </a> para aprender, experimentar e aprimorar os aplicativos iOS existentes com o {{site.data.keyword.Bluemix_notm}}.</dd>
  <dt>{{site.data.keyword.cloudaccesstrailshort}}</dt>
    <dd>É possível monitorar a atividade administrativa realizada no {{site.data.keyword.appid_short_notm}}, como as mudanças na configuração do painel, usando o serviço [{{site.data.keyword.cloudaccesstrailshort}} ](/docs/services/cloud-activity-tracker/index.html).</dd>
  <dt>Guia de programação do Node.js</dt>
    <dd>Você desenvolve apps em Node.js? Experimente o <a href="https://console.bluemix.net/docs/node/index.html#getting-started-tutorial" target="_blank">Guia de programação do Node.js<img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> para aprender, experimentar e aprimorar os aplicativos Node.js existentes com o {{site.data.keyword.Bluemix_notm}}.</dd>
</dl>


## Software
{: #architecture}

Com o {{site.data.keyword.appid_short_notm}}, é possível incluir um nível de segurança em seus apps requerendo que os usuários se conectem. Também é possível usar o SDK ou as APIs do servidor para proteger os recursos de backend.
{: shortdesc}

![{{site.data.keyword.appid_short_notm}} diagrama de arquitetura](/images/appid_architecture1.png)

<dl>
  <dt>Aplicativo</dt>
    <dd><strong>SDK do servidor</strong>: é possível proteger seus recursos de backend que estão hospedados no {{site.data.keyword.Bluemix_notm}} e seus apps da web usando o SDK do servidor. Ele extrai o token de acesso de uma solicitação e o valida com o {{site.data.keyword.appid_short_notm}}. </br>
    <strong>SDK do cliente</strong>: é possível proteger seus apps móveis com o SDK do cliente Android ou iOS. O SDK cliente se comunica com seus recursos em nuvem para iniciar o processo de autenticação quando ele detecta um desafio de autorização.</dd>
  <dt>{{site.data.keyword.Bluemix_notm}}</dt>
    <dd><strong>{{site.data.keyword.appid_short_notm}}</strong>: após a autenticação bem-sucedida, o {{site.data.keyword.appid_short_notm}} retorna tokens de acesso e de identidade para seu app.</br>
    <strong>Diretório da nuvem</strong>: os usuários podem se inscrever para seu serviço com seus e-mails e uma senha. É possível, então, gerenciar seus usuários em uma visualização de lista por meio da UI. Com o diretório da nuvem, o {{site.data.keyword.appid_short_notm}} funciona como seu provedor de identidade.</dd>
  <dt>Externo (terceiro)</dt>
    <dd><strong>Provedores de identidade social e corporativa</strong>: o {{site.data.keyword.appid_short_notm}} suporta o Facebook, o Google+ e a Federação SAML 2.0 como as opções de provedor de identidade. O serviço determina um redirecionamento para o provedor de identidade e verifica os tokens de autenticação retornados. Se os tokens forem válidos, o serviço concederá acesso a seu app sem ter acesso à passphrase real.</dd>
</dl>


## Fluxo de Pedido
{: #request}

Enquanto o fluxo de solicitação pode variar dependendo da configuração de aplicativo, há três fluxos principais que podem ser encontrados ao trabalhar com o ID do app. É possível criar um fluxo de aplicativo móvel, um fluxo de aplicativo da web ou proteger os recursos com um fluxo diferente. Confira alguns dos fluxos de exemplo para ver se você consegue iniciar lá ao configurar o aplicativo.
{: shortdesc}

### Fluxo de solicitação do aplicativo da web
{: #web-flow}

![{{site.data.keyword.appid_short_notm}} fluxo de solicitação](/images/web_flow1.png)

1. Usando um navegador, um usuário executa uma ação que aciona uma solicitação para o SDK do ID do app.
2. Se o usuário estiver desautorizado, um redirecionamento para o ID do app será iniciado.
3. O ID do app ativa o widget de login e envia-o para o navegador.
4. O usuário escolhe um provedor de identidade com o qual se autenticar e conclui o processo de conexão.
5. O provedor de identidade redireciona de volta para o SDK do ID do app com um token de identidade.
6. O SDK do ID do app obtém tokens de acesso do serviço do ID do app.
7. Os tokens são salvos pelo SDK do ID do app e ocorre um redirecionamento.
8. O usuário tem acesso concedido ao aplicativo.

### Fluxo de solicitação móvel
{: #mobile-flow}

![{{site.data.keyword.appid_short_notm}} fluxo de solicitação](/images/mobile_flow.png)

1. Um usuário executa uma ação que aciona uma solicitação pelo aplicativo cliente para o SDK do ID do app.
2. Se o usuário não tiver tokens de acesso válidos, o SDK do ID do app iniciará o processo de autorização.
3. O widget de login é exibido para o usuário.
4. Usando um dos provedores de identidade configurados, o usuário é autenticado.
5. Depois que o usuário tem um token de identidade, o SDK obtém um token de acesso do serviço do ID do app.
6. Com os dois tokens, o SDK executa a solicitação novamente.
7. Se os tokens forem válidos, será concedido ao usuário o acesso ao aplicativo.

### Fluxo de solicitação de recurso protegido
{: #pr-flow}

![{{site.data.keyword.appid_short_notm}} fluxo de solicitação](/images/pr_flow.png)

1. Antes que uma solicitação para o recurso possa ser feita, um aplicativo cliente deve ter um conjunto de chaves públicas.
2. Com as chaves públicas, uma solicitação é feita por um aplicativo cliente.
3. Se não houver um token de acesso válido, o aplicativo receberá um erro.
4. Depois de obter um token válido, o aplicativo do cliente pode fazer a solicitação novamente. Mas desta vez, inclua o token.
5. Quando o aplicativo pode validar as permissões que são concedidas pelo token de acesso, é concedido ao aplicativo o acesso ao recurso protegido.
