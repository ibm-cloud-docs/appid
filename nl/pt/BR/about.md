---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Sobre
{: #about}

É possível usar o {{site.data.keyword.appid_full}} para incluir a autenticação em seus apps e proteger seus recursos de backend.
{:shortdesc}

## Razões para usar o serviço
{: #reasons}

Por que você deseja usar o {{site.data.keyword.appid_short_notm}}? Confira os cenários
a seguir para ver se algum deles se aplica a você.
{: shortdesc}

<table>
  <tr>
    <th> Cenário </th>
    <th> Motivo </th>
  </tr>
  <tr>
    <td> É necessário incluir [autorização e autenticação](/docs/services/appid/authorization.html) em seus apps móveis e da web, mas não há um plano de fundo de segurança. </td>
    <td> O {{site.data.keyword.appid_short_notm}} facilita a inclusão de uma etapa de autenticação em seus apps. É possível usar o serviço para se comunicar com os [provedores de identidade](/docs/services/appid/identity-providers.html) para gerenciar o acesso aos seus apps. </td>
  </tr>
  <tr>
    <td> Você deseja limitar o acesso aos seus apps e recursos de backend. </td>
    <td> O serviço fornece a capacidade de [proteger seus recursos](/docs/services/appid/protecting-resources.html) para usuários autenticados e anônimos. </td>
  </tr>
  <tr>
    <td> Você deseja construir experiências de app personalizadas para seus usuários. </td>
    <td> Com o {{site.data.keyword.appid_short_notm}}, é possível [armazenar dados do usuário](/docs/services/appid/user-profile.html) como preferências de app ou informações de seus perfis sociais públicos e, em seguida, usar esses dados para customizar cada experiência de seu app. </td>
  </tr>
  <tr>
    <td> Você deseja fornecer aos usuários a capacidade de acessar seu app com seus e-mails e uma senha. </td>
    <td> O {{site.data.keyword.appid_short_notm}} fornece a capacidade de criar um [diretório da nuvem](/docs/services/appid/cloud-directory.html). Isso torna possível incluir a inscrição do usuário e conectar-se aos apps móveis e da web. O diretório da nuvem fornece a estrutura para manter um registro do usuário que pode escalar com sua base de usuários. Com a funcionalidade pré-construída para autoatendimento, como verificação de e-mail e reconfigurações de senha, é possível ter certeza que seu app está autenticando usuários com segurança. </td>
  </tr>
</table>


## Software
{: #architecture}

Com o {{site.data.keyword.appid_short_notm}}, é possível incluir um nível de segurança a seus apps, solicitando aos usuários que se conectem. Também é possível usar o SDK do servidor para proteger seus recursos de backend.
{: shortdesc}

![{{site.data.keyword.appid_short_notm}} diagrama de arquitetura](/images/appid_architecture.png)

<dl>
  <dt> Aplicativo </dt>
    <dd> SDK do servidor: é possível proteger seus recursos de backend que estão hospedados no {{site.data.keyword.Bluemix_notm}} e seus apps da web usando o SDK do servidor. Ele extrai o token de acesso de uma solicitação e o valida com o {{site.data.keyword.appid_short_notm}}. </br>
    SDK do cliente: é possível proteger seus apps móveis com o SDK do cliente Android ou iOS. O SDK cliente se comunica com seus recursos em nuvem para iniciar o processo de autenticação quando ele detecta um desafio de autorização.</dd>
  <dt> {{site.data.keyword.Bluemix_notm}} </dt>
    <dd> ID do app: após a autenticação bem-sucedida, o {{site.data.keyword.appid_short_notm}} retorna tokens de acesso e de identidade para seu app.</br>
    Cloud Directory: os usuários podem inscrever-se para o seu serviço com e-mail e senha. É possível, então, gerenciar seus usuários em uma visualização de lista por meio da UI. </dd>
  <dt> Externo (terceiros) </dt>
    <dd>  O {{site.data.keyword.appid_short_notm}} suporta dois provedores de identidade social: Facebook e Google+. O serviço organiza um redirecionamento para o provedor de identidade e fornece acesso a seu app após a verificação de autenticação. O {{site.data.keyword.appid_short_notm}} verifica as
credenciais sem ter acesso à passphrase real. </dd>
</dl>


## Fluxo de Pedido
{: #request}

O diagrama a seguir descreve como uma solicitação flui do SDK do cliente para seus recursos de backend e provedores de identidade.
{: shortdesc}

![{{site.data.keyword.appid_short_notm}} fluxo de solicitação](/images/appidrequestflow.png)


* O SDK do cliente {{site.data.keyword.appid_short_notm}} faz uma solicitação a
seus recursos de backend protegidos com o SDK do servidor {{site.data.keyword.appid_short_notm}}.
* O {{site.data.keyword.appid_short_notm}} SDK do servidor detecta uma solicitação não autorizada e retorna um HTTP 401 e escopo de autorização.
* O SDK do cliente detecta automaticamente o HTTP 401 e inicia o processo de autenticação.
* Quando o SDK do cliente entra em contato com o serviço, o SDK do servidor retorna o widget de login se mais de um provedor de identidade é configurado. {{site.data.keyword.appid_short_notm}} chama o provedor de identidade e apresenta o formulário de login para esse provedor ou retorna um código de concessão que permite autenticar se nenhum provedor de identidade é configurado.
* {{site.data.keyword.appid_short_notm}} solicita que o aplicativo do cliente autentique fornecendo um desafio de autenticação.
* Se um provedor de identidade estiver configurado quando o usuário efetuar login, a autenticação
será manipulada pelo respectivo fluxo de OAuth.
* Se a autenticação terminar com o mesmo código de concessão, o código será enviado para o terminal do token. O terminal retorna dois tokens: um de acesso e um de identidade. Desse ponto em diante, todas as solicitações feitas com o SDK do cliente terão um cabeçalho de autorização recém-obtido.
* O SDK do cliente reenvia automaticamente a solicitação original que acionou o fluxo de autorização.
* O SDK do servidor extrai o cabeçalho de autorização da solicitação, valida o cabeçalho com o serviço e concede acesso a um recurso de backend.

**Nota**: os protocolos implementados são totalmente compatíveis com o OpenID Connect (OIDC).
