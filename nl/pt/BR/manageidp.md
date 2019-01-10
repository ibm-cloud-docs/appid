---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}


# Gerenciando
{: #managing}

Os provedores de identidade (IdPs) incluem um nível de segurança para seus aplicativos móveis e da web por meio de
autenticação. Com o {{site.data.keyword.appid_full}}, é possível configurar um ou vários provedores de
identidade para criar uma experiência de conexão customizada para seus usuários.
{: shortdesc}


**O que é um provedor de identidade?**

Um provedor de identidade cria e gerencia informações sobre uma entidade, tal como um usuário, um ID funcional ou um
aplicativo. O provedor verifica a identidade da entidade usando credenciais, tais como uma senha. Em seguida, o IdP
envia as informações de identidade para outro provedor de serviços. Como o provedor de identidade autentica a entidade,
o {{site.data.keyword.appid_short_notm}} é capaz de autorizá-la e conceder acesso aos seus aplicativos.

</br>

**Quais são os provedores de identidade para os quais o {{site.data.keyword.appid_short_notm}} fornece uma integração?**

Há vários provedores para os quais o serviço é pré-configurado para uso.

<table>
  <tr>
    <th>Provedor</th>
    <th>Tipo</th>
    <th>Descrição</th>
  </tr>
  <tr>
    <td>[Cloud Directory](/docs/services/appid/cloud-directory.html)</td>
    <td>Registro gerenciado</td>
    <td>É possível manter seu próprio registro do usuário na nuvem. Quando um usuário se inscreve em seu aplicativo, ele é
incluído em seu diretório de usuários. Essa opção fornece aos usuários mais liberdade para gerenciar sua própria conta
em seu aplicativo.</td>
  </tr>
  <tr>
    <td>[SAML](/docs/services/appid/enterprise.html)</td>
    <td>As</td>
    <td>É possível criar uma experiência de conexão única para seus usuários finais.</td>
  </tr>
  <tr>
    <td>[Facebook ](/docs/services/appid/identity-providers.html#facebook)</td>
    <td>Social</td>
    <td>Os usuários finais podem efetuar login em seu aplicativo usando suas credenciais do Facebook.</td>
  </tr>
  <tr>
    <td>[Google+](/docs/services/appid/identity-providers.html#google)</td>
    <td>Social</td>
    <td>Os usuários finais podem efetuar login em seu aplicativo usando suas credenciais do Google+.</td>
  </tr>
  <tr>
    <td>[Customizado ](/docs/services/appid/custom.html)</td>
    <td> </td>
    <td>Se nenhuma das opções fornecidas se ajustar à sua necessidade específica, será possível configurar seu próprio fluxo de
identidade para trabalhar com o {{site.data.keyword.appid_short_notm}}.</td>
  </tr>
  
</table>

</br>

**Como o {{site.data.keyword.appid_short_notm}} interage com um provedor de identidade?**

O {{site.data.keyword.appid_short_notm}} interage com provedores de identidade usando múltiplos protocolos,
como a conexão OpenID, o SAML e mais. Por exemplo, a conexão OpenID é o protocolo usado com muitos provedores sociais, como
o Facebook e o Google. Provedores corporativos como o <a href="https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-azure-active-directory/" target="_blank">Azure
Active Directory <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> ou o <a href="https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-active-directory-federation-service/" target="_blank">Active
Directory Federation Service <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>, geralmente usam
o SAML como seu protocolo de identidade. Para o [Cloud Directory](cloud-directory.html), o serviço
usa o SCIM para verificar as informações de identidade.

Trabalhando com identidade do aplicativo? Consulte [Identidade do
aplicativo](app-to-app.html).
{: tip}

</br>
</br>

## Definindo as configurações
{: #configuring}

É possível decidir quais provedores que você deseja usar, suas URLs de redirecionamento e as informações de token para seu
aplicativo. As definições configuradas são aplicadas a todos os provedores de identidade nessa instância do serviço. Por
exemplo: quando você configura a expiração do token, ela se aplica a todos os provedores que você configurou, sejam eles
sociais ou corporativos.

</br>

**Para configurar seus provedores:**

1. Navegue para o seu painel de serviço.
2. Na seção **Provedores de identidade** da navegação, selecione a página **Gerenciar**.
3. Na guia **Provedores de identidade**, configure os provedores que deseja usar para **Ativado**.
4. Opcional: decida se desativará **Usuários anônimos** ou deixará o padrão, que é
**Ativado**. Quando configurado como **Ativado**, os atributos do usuário customizados são associados ao
usuário a partir do momento em que começam a interagir com seu aplicativo. Para obter mais informações sobre o caminho para se
tornar um usuário identificado, consulte [Autenticação progressiva](progressive.html#progressive).

O {{site.data.keyword.appid_short_notm}} fornece credenciais padrão para ajudar com a configuração inicial do
Facebook e do Google+. Você tem o limite de 100 usos das
credenciais por instância, por dia. Como são credenciais da IBM, elas devem ser usadas apenas para desenvolvimento. Antes de publicar o seu app, atualize a configuração para as suas próprias credenciais.
{: tip}

</br>

**Para configurar suas definições:**

1. Inclua suas URLs de redirecionamento. Uma URL de redirecionamento é o terminal de retorno de chamada de seu app. Para
evitar ataques de phishing, o {{site.data.keyword.appid_short_notm}} valida as URLs com relação à lista de
desbloqueio.
  1. No campo **Incluir URL de redirecionamento da web**, digite a URL e clique no ícone **+**.
  2. Repita a etapa 1 até que todas as URLs de redirecionamento possíveis sejam incluídas na lista.

  Não inclua quaisquer parâmetros de consulta em sua URL. Eles são ignorados no processo de validação. Por exemplo:
`http://host:[port]/path`
  {: tip}

2. Configure seus tokens. O tempo de vida do token começa novamente em cada conexão do usuário. Por exemplo, você
configura o tempo de vida de seu token de atualização para dez dias. Um token de acesso e um token de atualização são
criados quando o usuário se conecta pela primeira vez. Se o usuário retornar para seu aplicativo alguns dias depois,
três dias especificamente, ele não precisará se conectar novamente. Mas, se o usuário esperou 12 dias após sua
conexão inicial e, em seguida, retornou para seu aplicativo, ele precisará se conectar novamente e um conjunto de tokens será
associado ao usuário.
  1. Para permitir a conexão sem a necessidade de interação com o usuário, configure **tokens de atualização** como **Ativado**.
  2. Configure o seu tempo de vida do token de atualização. A expiração é configurada em dias e pode ser qualquer valor no intervalo de 1 a 90. Quanto menor o número, mais frequentemente um usuário deverá se conectar.
  3. Configure o seu tempo de vida do token de acesso. A expiração é configurada em minutos e pode estar no intervalo de 5 a 1440. Quanto menor o valor, maior a proteção que você tem em casos de roubo de token.
  4. Configure o seu tempo de vida do token anônimo. Um [token anônimo](/docs/services/appid/progressive.html#anonymous) é designado aos usuários no momento em que eles começam a interagir com o seu app. Quando um usuário se conectar, as informações no token anônimo serão, então, transferidas para o token associado ao usuário. A expiração é configurada em dias e pode ser qualquer valor entre 1 e 90.

</br>
</br>
