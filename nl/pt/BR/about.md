---

copyright:
  years: 2017
lastupdated: "2017-11-09"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


# Sobre
{: #about}

O {{site.data.keyword.appid_full}} fornece a você a capacidade de gerenciar o acesso
aos seus aplicativos de forma fácil e simples.
{:shortdesc}


## Razões para usar o serviço
{: #reasons}

Por que você deseja usar o {{site.data.keyword.appid_short_notm}}? Confira os cenários
a seguir para ver se algum deles se aplica a você.
{: shortdesc}

<table>
  <tr>
    <th> Cenário </th>
    <th> Motivo</th>
  </tr>
  <tr>
    <td> Você deseja incluir segurança em seus aplicativos móveis e da web. </td>
    <td> O {{site.data.keyword.appid_short_notm}} facilita a inclusão de uma etapa de autenticação
em seus aplicativos. É possível usar o serviço para se comunicar com os provedores de identidade para
gerenciar o acesso aos seus aplicativos. </td>
  </tr>
  <tr>
    <td> Você deseja limitar o acesso aos seus apps e recursos de backend. </td>
    <td> O serviço fornece a você a capacidade de proteger seus recursos para usuários autenticados e anônimos. </td>
  </tr>
  <tr>
    <td> Você deseja construir experiências de app personalizadas para seus usuários. </td>
    <td> O {{site.data.keyword.appid_short_notm}} permite armazenar dados do usuário, como
preferências de app ou informações de seus perfis sociais públicos. É possível usar esses dados para
assegurar que seus usuários tenham uma experiência que seja customizada para eles. </td>
  </tr>
</table>

**Nota**: os protocolos implementados são totalmente compatíveis com o OpenID Connect (OIDC).


## Software
{: #architecture}

Com o {{site.data.keyword.appid_short_notm}} é possível incluir um nível de segurança em seus aplicativos solicitando aos usuários para se conectarem. Também
é possível usar o servidor SDK para proteger os seus recursos de backend.

O diagrama a seguir mostra uma visão geral de como o serviço do {{site.data.keyword.appid_short_notm}} funciona.


![{{site.data.keyword.appid_short_notm}} diagrama de arquitetura](/images/appid_architecture2.png)

Figura 1. Diagrama de arquitetura do {{site.data.keyword.appid_short_notm}}



<dl>
  <dt> Aplicativo </dt>
    <dd> O SDK do cliente fornece uma classe de solicitação para se comunicar com os seus recursos em nuvem. O SDK do cliente automaticamente inicia o processo de
autenticação quando ele detecta um desafio de autorização. </dd>
  <dt> {{site.data.keyword.Bluemix_notm}} </dt>
    <dd>  O SDK do servidor extrai o token de acesso da solicitação e a valida com o {{site.data.keyword.appid_short_notm}}. Após a autenticação bem-sucedida, o {{site.data.keyword.appid_short_notm}} retorna tokens de acesso e de identidade para o seu aplicativo. </dd>
  <dt> Provedores de identidade </dt>
    <dd> O serviço organiza um redirecionamento para o provedor de identidade e verifica a autenticação
para fornecer acesso a seu aplicativo. O {{site.data.keyword.appid_short_notm}} verifica as
credenciais sem ter acesso à passphrase real. </dd>
</dl>


## Fluxo de Pedido
{: #request}

O diagrama a seguir descreve como uma solicitação flui do SDK do cliente para seu aplicativo backend e provedores de identidade.

![{{site.data.keyword.appid_short_notm}} fluxo de solicitação](/images/appidrequestflow.png)

Figura 2. Fluxo de solicitação do {{site.data.keyword.appid_short_notm}}


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


## Componentes
{: #components}

O serviço é composto dos componentes a seguir.

<dl>
  <dt> Painel </dt>
    <dd> No painel de serviço, é possível fazer download de amostras de migração, ver os logs de atividade e configurar provedores de autenticação e identidade. </dd>
  <dt> Client SDK </dt>
    <dd> É possível usar o SDK do cliente com seus apps móveis e da web para implementar a autenticação do usuário. </br></br>
    Pré-requisitos para Android:
    <ul><ul><li> API 25 ou superior </li>
    <li> Java 8.x </li>
    <li> Ferramentas Android SDK 25.2.5 ou superior </li>
    <li> Ferramentas da plataforma Android SDK 25.0.3 ou superior </li>
    <li> Ferramentas de construção Android versão 25.0.2 ou superior </li></ul></ul></br>
    Pré-requisitos para o iOS:
    </br>
    <ul><ul><li> iOS9 ou superior </li>
    <li> MacOS 10.11.5 </li>
    <li>Xcode 8.2</li></ul></ul></dd>
  <dt> SDK do servidor </dt>
    <dd> É possível proteger seus recursos de backend hospedados no {{site.data.keyword.Bluemix_notm}} </br>
    Tempos de execução suportados:
    <ul><ul><li> Node.js </li>
    <li> Liberty for Java </li>
    <li> Swift </li></ul></ul></dd>
</dl>
