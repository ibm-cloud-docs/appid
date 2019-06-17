---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-20"

keywords: authentication, authorization, identity, app security, secure, development, identity provider, tokens, customization, lifetime

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


# Gerenciando autenticações
{: #managing-idp}

Os provedores de identidade (IdPs) incluem um nível de segurança para seus aplicativos móveis e da web por meio de
autenticação. Com o {{site.data.keyword.appid_full}}, é possível configurar um ou vários provedores de
identidade para criar uma experiência de conexão customizada para seus usuários.
{: shortdesc}


O {{site.data.keyword.appid_short_notm}} interage com provedores de identidade usando múltiplos protocolos,
como a conexão OpenID, o SAML e mais. Por exemplo, a conexão OpenID é o protocolo usado com muitos provedores sociais, como
o Facebook e o Google. Provedores corporativos, como o <a href="https://www.ibm.com/cloud/blog/setting-ibm-cloud-app-id-azure-active-directory" target="_blank">Azure Active Directory <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> ou o <a href="https://www.ibm.com/cloud/blog/setting-ibm-cloud-app-id-active-directory-federation-service" target="_blank">Active Directory Federation Service <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>, geralmente usam SAML como seu protocolo de identidade. Para o [Cloud Directory](/docs/services/appid?topic=appid-cloud-directory), o serviço
usa o SCIM para verificar as informações de identidade.

Ao usar provedores de identidade sociais ou corporativos, o {{site.data.keyword.appid_short_notm}} tem acesso de
leitura aos dados da conta dos usuários. O serviço usa um token e as asserções que são retornados pelo provedor de
identidade para verificar se um usuário é quem eles dizem que são. Como o serviço nunca tem acesso de gravação às informações, os usuários devem passar por seu provedor de identidade escolhido para executar ações, como reconfigurar
a senha. Por exemplo, se um usuário se conectar ao seu app com o Facebook e, em seguida, desejar mudar sua senha, ele deverá ir para `www.facebook.com` para fazer isso.

Quando você usa o [Cloud Directory](/docs/services/appid?topic=appid-cloud-directory), o {{site.data.keyword.appid_short_notm}} é o provedor de identidade. O serviço usa seu registro para verificar a
identidade dos usuários. Como o {{site.data.keyword.appid_short_notm}} é o provedor, os usuários podem tirar
vantagem da funcionalidade avançada, como reconfigurar sua senha, diretamente em seu aplicativo.

Trabalhando com identidade do aplicativo? Consulte a [Identidade do aplicativo](/docs/services/appid?topic=appid-app).
{: tip}

O serviço pode ser configurado para usar vários provedores. Consulte a tabela a seguir para saber mais sobre suas opções.

<table>
  <tr>
    <th>Provedor</th>
    <th>Tipo</th>
    <th>Descrição</th>
  </tr>
  <tr>
    <td>[Cloud Directory](/docs/services/appid?topic=appid-cloud-directory)</td>
    <td>Registro gerenciado</td>
    <td>É possível manter seu próprio registro do usuário na nuvem. Quando um usuário se inscreve em seu aplicativo, ele é
incluído em seu diretório de usuários. Essa opção fornece aos usuários mais liberdade para gerenciar sua própria conta
em seu aplicativo.</td>
  </tr>
  <tr>
    <td>[SAML](/docs/services/appid?topic=appid-enterprise#enterprise)</td>
    <td>As</td>
    <td>É possível criar uma experiência de conexão única para os usuários finais.</td>
  </tr>
  <tr>
    <td>[Facebook](/docs/services/appid?topic=appid-social#facebook)</td>
    <td>Social</td>
    <td>Os usuários finais podem se conectar em seu app usando suas credenciais do Facebook.</td>
  </tr>
  <tr>
    <td>[Google+](/docs/services/appid?topic=appid-social#google)</td>
    <td>Social</td>
    <td>Os usuários finais podem se conectar em seu app usando suas credenciais do Google.</td>
  </tr>
  <tr>
    <td>[Customizado](/docs/services/appid?topic=appid-custom-identity#custom-identity)</td>
    <td> </td>
    <td>Se nenhuma das opções fornecidas se ajustar à sua necessidade específica, será possível configurar seu próprio fluxo de
identidade para trabalhar com o {{site.data.keyword.appid_short_notm}}.</td>  
  </tr>
</table>

## Gerenciando provedores
{: #managing-providers}

Um provedor de identidade cria e gerencia informações sobre uma entidade, tal como um usuário, um ID funcional ou um
aplicativo. O provedor verifica a identidade da entidade usando credenciais, tais como uma senha. Em seguida, o IdP
envia as informações de identidade para outro provedor de serviços. Como o provedor de identidade autentica a entidade,
o {{site.data.keyword.appid_short_notm}} é capaz de autorizá-la e conceder acesso aos seus aplicativos.
{: shortdesc}

Para gerenciar seus provedores de identidade:

1. Navegue para o seu painel de serviço.
2. Na seção **Provedores de identidade** da navegação, selecione a página **Gerenciar**.
3. Na guia **Provedores de identidade**, configure os provedores que deseja usar para **Ativado**.
4. Opcional: decida se desativará **Usuários anônimos** ou deixará o padrão, que é
**Ativado**. Quando configurado como **Ativado**, os atributos do usuário são associados com o usuário por meio do momento em que começam a interagir com seu app. Para obter mais informações sobre o caminho para se tornar um usuário identificado, consulte [Autenticação progressiva](/docs/services/appid?topic=appid-anonymous#progressive)

O {{site.data.keyword.appid_short_notm}} fornece credenciais padrão para ajudar com a configuração inicial do
Facebook e do Google+. Você tem o limite de 100 usos das
credenciais por instância, por dia. Como são credenciais da IBM, elas devem ser usadas apenas para desenvolvimento. Antes de publicar o seu app, atualize a configuração para as suas próprias credenciais.
{: tip}


## Incluindo URIs de redirecionamento
{: #add-redirect-uri}

Um URI de redirecionamento é o terminal de retorno de chamada de seu app. Durante o fluxo no de conexão, o {{site.data.keyword.appid_short_notm}} valida os URIs antes de permitir que os clientes participem do fluxo de trabalho de autorização que ajuda a evitar ataques de phishing e vazamento de código de concessão. Ao registrar seu URI, você está dizendo ao {{site.data.keyword.appid_short_notm}} que o URI é confiável e que está tudo bem redirecionar seus usuários.

Certifique-se de registrar somente URIs de aplicativos em que você confia.
{: note}


1. Clique em **Configurações de Autenticação**para ver suas opções de configuração de URI e de token.

2. No campo **Incluir URI de redirecionamento da web**, digite o URI. Cada URI deve iniciar com `http://` ou `https://` e deve incluir o caminho completo, incluindo qualquer parâmetro de consulta para que o redirecionamento seja bem-sucedido. Precisa de ajuda para formatar seu URI? Consulte a tabela a seguir para obter alguns exemplos.

  <table>
    <tr>
      <th>Tipo</th>
      <th>URI de exemplo</th>
    </tr>
    <tr>
      <td>Domínio customizado</td>
      <td><code>http://mydomain.net/myapp2path/appid_callback</code></td>
    </tr>
    <tr>
      <td>Subdomínio de ingresso</td>
      <td><code>https://mycluster.us-south.containers.appdomain.cloud/myapp1path/appid_callback</code></td>
    </tr>
    <tr>
      <td>Efetuar logout</td>
      <td><code>http://mydomain.net/myapp2path/appid_logout</code></td>
    </tr>  
  </table>

3. Clique no símbolo **+** na caixa **Incluir URIs de redirecionamento da web**.

4. Repita as etapas uma a três até que todos os URIs possíveis sejam incluídos em sua lista.



Não tem certeza de onde seu URI de redirecionamento vem? Assista ao vídeo curto a seguir para ver onde obtê-lo e como incluí-lo em sua lista.

<iframe class="embed-responsive-item" id="redirecturi" title="{{site.data.keyword.appid_short_notm}}: Como corrigir URI de redirecionamento inválido" type="text/html" width="640" height="390" src="//www.youtube.com/embed/6hxqbvpc054?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>



## Configurando o tempo de vida do token
{: #idp-token-lifetime}

O tempo de vida do token começa novamente em cada conexão do usuário. Por exemplo, você
configura o tempo de vida de seu token de atualização para dez dias. Um token de acesso e um token de atualização são
criados quando o usuário se conecta pela primeira vez. Se o usuário retornar para seu aplicativo alguns dias depois,
três dias especificamente, ele não precisará se conectar novamente. Mas, se o usuário esperou 12 dias após sua
conexão inicial e, em seguida, retornou para seu aplicativo, ele precisará se conectar novamente e um conjunto de tokens será
associado ao usuário. Para obter mais informações sobre tokens, consulte [Entendendo os tokens](/docs/services/appid?topic=appid-tokens#tokens).

1. Para permitir a conexão sem a necessidade de interação com o usuário, configure **tokens de atualização** como **Ativado**.

2. Configure o seu tempo de vida do token de atualização. A expiração é configurada em dias e pode ser qualquer valor no intervalo de 1 a 90. Quanto menor o número, mais frequentemente um usuário deverá se conectar.

3. Configure o seu tempo de vida do token de acesso. A expiração é configurada em minutos e pode estar no intervalo de 5 a 1440. Quanto menor o valor, maior a proteção que você tem em casos de roubo de token.

4. Configure o seu tempo de vida do token anônimo. Um [token anônimo](/docs/services/appid?topic=appid-anonymous#progressive) é designado aos usuários no momento em que eles começam a interagir com o seu app. Quando um usuário se conectar, as informações no token anônimo serão, então, transferidas para o token associado ao usuário. A expiração é configurada em dias e pode ser qualquer valor entre 1 e 90.


Quando você configurar uma expiração de token, ela se aplicará a todos os provedores que você configurou, incluindo sociais e corporativos.
{: tip}
