---

copyright:
  years: 2017
lastupdated: "2017-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


# Autorização e autenticação
{: authorization}

Autorização é o processo pelo qual você concede acesso aos seus apps. O serviço {{site.data.keyword.appid_short}} usa tokens, filtros e um cabeçalho para autenticar usuários.
{: shortdesc}


## Identidade do OAuth
{: #oauth}

Quando o serviço chama a API de login do OAuth, o {{site.data.keyword.appid_short_notm}} usa os protocolos OAuth 2.0 e OpenID Connect (OIDC) para autorizar e autenticar o responsável pela chamada com um provedor de identidade selecionado. Após a autenticação, a identidade é associada a um registro do usuário do {{site.data.keyword.appid_short_notm}}. O {{site.data.keyword.appid_short_notm}} retorna um token de acesso que pode ser usado para acessar os atributos do usuário e um token de identidade que está retendo as informações de identidade fornecidas pelo provedor de identidade. O mesmo registro
do usuário e seus atributos poderão ser acessados novamente por meio de qualquer cliente que se autenticar com essa mesma identidade.

## Tokens de acesso e de identidade

O {{site.data.keyword.appid_short}} usa dois tipos de tokens: de acesso e de identidade.
{:shortdesc}

**Observação**: os tokens são formatados como <a href="https://jwt.io/introduction/" target="_blank">Tokens da web da JSON <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.

### Token de Acesso
{: #access-tokens}

Os tokens de acesso permitem a comunicação com [recursos de backend](/docs/services/appid/protecting-resources.html) que são protegidos por filtros de autorização que são configurados pelo ID do App. O token adequa-se às especificações do JavaScript Object Signing and Encryption (JOSE).

Token de exemplo:

```
Header: {
    "typ": "JOSE",
    "alg": "RS256",
}
Payload: {
    "iss": "appid-oauth.ng.bluemix.net",
    "exp": "1495562664",
    "aud": "a3b87400-f03b-4956-844e-a52103ef26ba",
    "amr": ["facebook"],
    "sub": "de6a17d2-693d-4a43-8ea2-2140afd56a22",
    "iat": "1495559064",
    "tenant": "9781974b-6a1c-46c3-aebf-32b7e9bbbaee",
    "scope": "appid_default appid_readprofile appid_readuserattr appid_writeuserattr",
}
```
{:screen}

<table>
<caption> Tabela 1. Componentes de token de acesso explicados </caption>
  <tr>
    <th> Componente </th>
    <th> Descrição </th>
  </tr>
  <tr>
    <td><i> typ </i></td>
    <td> O tipo de cabeçalho, especificado como "JOSE". </td>
  </tr>
  <tr>
    <td><i> alg </i></td>
    <td> O algoritmo usado, especificado como "RS256". </td>
  </tr>
  <tr>
    <td><i> iss </i></td>
    <td> O servidor {{site.data.keyword.appid_short}} que emitiu o token; especificado como uma sequência ou uma URL. </td>
  </tr>
  <tr>
    <td><i> sub </i></td>
    <td> O ID do usuário para quem o token é emitido. </td>
  </tr>
  <tr>
    <td><i> aud </i></td>
    <td> O identificador de cliente para o qual o token se destina. </td>
  </tr>
  <tr>
    <td><i> exp </i></td>
    <td> O horário em que o registro de data e hora expira, especificado no tempo da época. </td>
  </tr>
  <tr>
    <td><i> iat </i></td>
    <td> O horário em que o registro de data e hora é emitido, especificado no tempo da época. </td>
  </tr>
  <tr>
    <td><i> tenant </i></td>
    <td> O identificador de usuário exclusivo emitido com o token. </td>
  </tr>
  <tr>
    <td><i> amr </i></td>
    <td> O provedor de identidade usado para autenticação. Essa variável pode ser <i>appid_facebook</i>, <i>appid_google</i> ou <i>cloud_directory</i>. </td>
  </tr>
  <tr>
    <td><i> scope </i></td>
    <td> O escopo para o qual o token é emitido. </td>
  </tr>
</table>


### Tokens de identidade
{: #identity-tokens}

Um token de identidade contém informações sobre o usuário. Ele pode fornecer informações sobre seu nome, e-mail, sexo e local. Um token também pode retornar uma URL para uma imagem do usuário.

Token de exemplo:

```
Header: {
    "typ": "JOSE",
    "alg": "RS256",
}
Payload: {
    "iss": "appid-oauth.ng.bluemix.net",
    "aud": "a3b87400-f03b-4956-844e-a52103ef26ba",
    "exp: "1495562664",
    "tenant": "9781974b-6a1c-46c3-aebf-32b7e9bbbaee",
    "iat": "1495559064",
    "name": "John Smith",
    "email": "js@mail.com",
    "gender", "male",
    "locale": "en",
    "picture": "https://url.to.photo",
    "sub": "de6a17d2-693d-4a43-8ea2-2140afd56a22",
    "identities": [
        "provider": "facebook"
        "id": "377440159275659"
    ],
    "amr": ["facebook"],
    "oauth_client":{
      "name": "BluemixApp",
      "type": "serverapp",
      "software_id": "cb638f8f-e24b-41d3-b770-23be158dd8e6.2b94e6bb-bac4-4455-8712-a43fa804d5cc.a3b87400-f03b-4956-844e-a52103ef26ba",
      "software_version": "1.0.0",
    }
}
```
{:screen}


<table>
<caption> Tabela 2. Componentes de token de identidade explicados </caption>
  <tr>
    <th> Componente </th>
    <th> Descrição </th>
  </tr>
  <tr>
    <td> <i>name</i> </td>
    <td> O nome completo do usuário, conforme relatado pelo provedor de identidade. Isso deve ser retornado. </td>
  </tr>
  <tr>
    <td> <i> email </i> </td>
    <td> O e-mail do usuário, conforme relatado pelo provedor de identidade. Retornado somente quando disponível. </td>
  </tr>
  <tr>
    <td> <i> gender </i> </td>
    <td> O sexo do usuário, conforme relatado pelo provedor de identidade, quando disponível. </td>
  </tr>
  <tr>
    <td> <i> locale </i> </td>
    <td> O código de idioma do usuário, conforme relatado pelo provedor de identidade. </td>
  </tr>
  <tr>
    <td> <i> picture </i> </td>
    <td> A URL para a foto de um usuário, se disponível. </td>
  </tr>
  <tr>
    <td> <i> identities: </br> <ul><li> provider <li> id </ul></i></td>
    <td> </br><ul><li> O provedor de identidade usado para autenticação. Essa variável pode ser <code>appid_facebook</code>, <code>appid_google</code> ou <code>cloud_directory</code> e deve ser retornada. <li> Um ID de usuário exclusivo, conforme relatado por um provedor de identidade. <li> Um objeto JSON que deve ser retornado pelo provedor de identidade. </ul></li></td>
  </tr>
  <tr>
    <td> <i> oauth_client: </br> <ul><li> type </br><li> name <li> software_id <li> software_version<li> device_id <li>device_model<li>device_os<li>device_os_version </ul></i> </td>
    <td> </br><ul><li> O tipo de app determinado durante o registro do cliente. A variável pode ser <em>serverapp</em> ou <em>mobileapp</em>. <li> O nome do cliente, conforme relatado durante o registro do cliente. <li> O ID do software, conforme relatado durante o registro do cliente. <li> A versão de software usada durante o registro do cliente. <li> O ID do dispositivo de cliente móvel. <li> O modelo de dispositivo de cliente móvel. <li> O S.O. do dispositivo de cliente móvel. <li> A versão do S.O. de dispositivo de cliente móvel.</ul></td>
  </tr>
</table>

## Cabeçalhos
{: #auth-header}

Um cabeçalho de autorização é a combinação de tokens retornados. Para {{site.data.keyword.appid_short}}, o cabeçalho de autorização consiste em três tokens diferentes que são separados por espaço em branco: Bearer, Access e Identidade. Os tokens do portador e de acesso são necessários para conceder acesso aos seus apps. Um token de identidade é opcional e é utilizado principalmente para armazenar informações sobre ele usando seu app.

Estrutura do cabeçalho de exemplo:

```
Authorization=Bearer {access_token} [{id_token}]
```
{: screen}


## Filtros de parte
{: #auth-filter}

O SDK do servidor {{site.data.keyword.appid_short}} fornece estratégias para proteger dois tipos de recursos: APIs e aplicativos da web.
{:shortdesc}

A estratégia de proteção de API retorna uma resposta HTTP 401 com uma lista de escopos para obter autorização para um cliente não autenticado. A estratégia de proteção de app da web retorna um redirecionamento HTTP 302. O redirecionamento envia um cliente não autenticado para a página de conexão que é hospedada pelo serviço {{site.data.keyword.appid_short_notm}} ou diretamente para uma página de conexão do provedor de identidade, dependendo de sua configuração.



### Estratégia de API
{: #api}

A estratégia de API espera que as solicitações contenham um cabeçalho de autorização com um token de acesso válido. A resposta também pode incluir um token de identidade, mas ele não é necessário.

Se um token for inválido ou estiver expirado, a estratégia de API retornará um erro HTTP 401 que conterá as informações a seguir: Www-Authenticate=Bearer
scope="{scope}" error="{error}". O componente `error` é opcional.

Se a solicitação retornar um token válido, o controle será transmitido para o próximo middleware e a propriedade `appIdAuthorizationContext`
será injetada no objeto de solicitação. Essa propriedade contém tokens de acesso e identidade originais, além de informações de carga útil decodificadas como objetos JSON simples.


### Estratégia de aplicativo da web
{: #web}

Quando a classe de estratégia de aplicativo da web detectar tentativas não autenticadas para acessar um recurso protegido, ela automaticamente redirecionará um
navegador do usuário para a página de autenticação. Após a autenticação bem-sucedida, o usuário é retornado à URL de retorno de chamada do aplicativo da web. O
serviço usa a classe de estratégia de aplicativo da web para obter tokens de acesso e de identidade. Após obter esses tokens, a classe de estratégia de aplicativo da
web armazena-os em uma sessão de HTTP sob `WebAppStrategy.AUTH_CONTEXT`. Cabe ao usuário decidir se deseja armazenar tokens de acesso e de identidade no banco de dados do app.


## Autenticação progressiva
{: #oauth}

O {{site.data.keyword.appid_short_notm}} usa os protocolos OAuth 2.0 e OIDC para autorizar e autenticar um usuário. Após a autenticação, a identidade será associada a um registro do usuário. O serviço retorna um token de acesso que pode ser usado para acessar os atributos do usuário e um token de identidade que contém as informações sobre o usuário que foram fornecidas pelo provedor de identidade. O registro e seus atributos poderão ser acessados novamente de qualquer cliente que se autentique com a mesma identidade.

Agora você pode perguntar: "e se eu quiser me conectar como opcional?" O {{site.data.keyword.appid_short_notm}} usa o que é conhecido como autenticação progressiva para criar [perfis de usuário](/docs/services/appid/user-profile.html), mesmo quando eles são anônimos. É possível, então, transferir essas informações para um perfil de usuário conhecido após um usuário se conectar.

![Um mapa que mostra o caminho para se tornar um usuário identificado.](/images/authenticationtrail.png)

Figura 2. Um mapa mostrando o caminho para se tornar um usuário identificado

Quando um usuário escolhe permanecer anônimo, o {{site.data.keyword.appid_short_notm}} cria um registro de usuário ad hoc e chama a API de login do OAuth, que retorna o acesso anônimo e os tokens de identidade. Usando esses tokens, o app pode criar, ler, atualizar e excluir os atributos que são armazenados no registro do usuário. Como um exemplo, um usuário pode começar imediatamente a incluir itens em um carrinho de compras sem precisar de conexão com um app.


Quando um usuário escolhe se conectar a um app, ele se torna um usuário identificado. Informações sobre o usuário são obtidas do provedor de identidade em que ele escolhe se conectar. Eles recebem tokens de acesso e de identidade que contêm informações sobre o usuário.

Um usuário anônimo pode escolher se tornar um usuário identificado. Mas, como isso funciona?

O token de acesso anônimo é passado para a API de login. O serviço autentica a chamada com um provedor de identidade. O serviço usa o token de acesso para localizar o registro anônimo e anexa a identidade nele. Os novos tokens de identidade contêm as informações públicas que são compartilhadas pelo provedor de identidade. Depois que um usuário é identificado, seus tokens anônimos tornam-se inválidos. No entanto, um usuário ainda será capaz de acessar seus atributos porque eles são acessíveis com o novo token.

**Observação**: uma identidade poderá ser atribuída a um registro anônimo somente se ele ainda não tiver sido atribuído a outro usuário. Se a identidade já está associada a outro usuário do {{site.data.keyword.appid_short_notm}}, os tokens contêm informações sobre o registro do usuário e fornecem acesso aos seus atributos. Os atributos de usuários anônimos anteriores não são acessíveis por meio do novo token. Até o token expirar, as informações ainda poderão ser acessadas através do token de acesso anônimo. Durante o desenvolvimento, é possível escolher como mesclar os atributos anônimos para o usuário conhecido.
