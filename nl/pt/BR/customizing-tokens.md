---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

keywords: authentication, authorization, identity, app security, secure, custom, tokens, access, claim, attributes

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


# Customizando os tokens
{: #customizing-tokens}

É possível configurar seus tokens do {{site.data.keyword.appid_short_notm}} para atender às necessidades
específicas de seu aplicativo.
{: shortdesc}

## Entendendo a customização
{: #understanding-customization}

O {{site.data.keyword.appid_short_notm}} usa diferentes tipos de tokens para proteger seus aplicativos.

* Tokens de acesso: ative a comunicação com recursos de back-end que são protegidos pelos filtros de autorização. Se um
token de acesso não estiver associado a um usuário específico, ele terá recursos limitados.
* Tokens de identidade: contêm informações pessoais e são usadas para autenticar um usuário. Dependendo da configuração do
aplicativo, os tokens de identidade podem ser emitidos antes que um usuário seja autenticado. Isso permite que você inicie a
associação de atributos com seus usuários antes que eles se conectem ao seu aplicativo.
* Tokens de atualização: podem ser usados para estender a quantidade de tempo que um usuário pode permanecer sem
autenticar novamente.

Quer aprender mais sobre os tokens? Leia mais em [Entendendo os tokens](/docs/services/appid?topic=appid-tokens#tokens).
{: tip}


É possível customizar seus tokens [na GUI](/docs/services/appid?topic=appid-customizing-tokens#configuring-tokens-ui) ou usando [a API](/docs/services/appid?topic=appid-customizing-tokens#configuring-tokens-api), configurando a validade do ciclo de vida ou incluindo solicitações customizadas em seus tokens. Consulte a tabela a seguir para ver como o tempo de vida é configurado ou continue lendo
para aprender sobre o mapeamento de atributos customizados.

<table>
  <tr>
    <th>Tipo de token</th>
    <th>Tipo de valor</th>
    <th>Padrão</th>
    <th>Opções</th>
  </tr>
  <tr>
    <td>Acesso</td>
    <td>Minutos</td>
    <td>60</td>
    <td>Qualquer valor entre 5 e 1440</td>
  </tr>
  <tr>
    <td>Identidade</td>
    <td>Minutos</td>
    <td>60</td>
    <td>Qualquer valor entre 5 e 1440</td>
  </tr>
  <tr>
    <td>Atualizar</td>
    <td>Dias</td>
    <td>30</td>
    <td>Qualquer valor entre 1 e 9</td>
  </tr>
  <tr>
    <td>Anônimo</td>
    <td>Dias</td>
    <td>30</td>
    <td>Qualquer valor entre 1 e 9</td>
  </tr>
</table>


Como os tokens são usados para identificar usuários e proteger seus recursos, o tempo de vida de um token afeta
várias coisas diferentes. Ao customizar sua configuração de token, é possível assegurar que suas necessidades de
segurança e de experiência do usuário sejam atendidas. No entanto, caso um token seja comprometido, um usuário
malicioso terá mais tempo para afetar seu aplicativo. É possível saber mais sobre as considerações de segurança em [Atributos customizados](/docs/services/appid?topic=appid-custom-attributes).
{: important}


## Entendendo atributos e solicitações customizados
{: #custom-claims}

É possível mapear atributos de perfil do usuário para suas solicitações de token de acesso e de identidade. Isso
significa que você não precisa acessar o
[terminal /userinfo](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Authorization_Server_V4/userInfo) ou extrair atributos customizados posteriormente porque eles já estão armazenados nos tokens.
{: shortdesc}

### O que é uma solicitação?
{: #custom-claims-defined}

Uma solicitação é uma instrução que uma entidade faz sobre si mesmo ou em nome de outra pessoa. Por exemplo, se você se conectar a um aplicativo usando um provedor de identidade, o provedor enviará ao aplicativo um grupo de reclamações ou instruções sobre você para o app para que ele possa agrupar com informações que ele já sabe sobre você. Dessa forma, ao se conectar, o aplicativo é configurado com suas informações, da maneira que você o configurou. Efetue check-out do exemplo a seguir para ver como formatar o objeto JSON.

```
{
  "accessTokenClaims": [
            {
      "source": "saml",
      "sourceClaim": "moderator"
    }
  ], "idTokenClaims": [ {
      "source": "saml",
      "sourceClaim": "moderator"
    }
  ],
  "access": {
    "expires_in": 3600
  },
  "refresh": {
    "expires_in": 2592000,
    "enabled": true
  },
  "anonymousAccess": {
    "expires_in": 2592000,
    "enabled": true
  }
}
```
{: screen}

Se você tiver informações customizadas de expiração para seu token, deverá configurá-las em cada solicitação. Se você não fizer isso, essa solicitação substituirá sua configuração atual e o padrão será usado para qualquer coisa deixada indefinida.
{: note}

### Por que eu gostaria de incluir solicitações em meus tokens?
{: #why-custom-claims}

Sem precisar fazer chamadas de rede extras, tudo o que seu aplicativo pode precisar saber sobre um usuário ou o que ele
pode fazer já está no token. Desde que você não tenha quantidades enormes de dados, isso torna-o mais eficiente. Além disso,
é possível assegurar a integridade desses atributos mapeados quando eles são enviados pela rede porque eles são
armazenados em um token assinado.


### Quais tipos de solicitações posso definir?
{: #custom-claim-types}

As solicitações que são fornecidas pelo {{site.data.keyword.appid_short_notm}} se enquadram em várias
categorias que são diferenciadas por seu nível de customização.

*Solicitações registradas*: há algumas solicitações nos tokens de acesso e identidade que são
definidas pelo {{site.data.keyword.appid_short_notm}} e não podem ser substituídas por mapeamentos customizados. Se sua solicitação for restrita, ela será ignorada pelo serviço. As solicitações são `iss`,
`aud`, `sub`, `iat`, `exp`, `amr` e `tenant`.

*Solicitações restritas*: dependendo do token para o qual as solicitações são mapeadas, algumas
solicitações têm possibilidades de customização limitadas. Para um token de acesso, o `scope` é a
única solicitação restrita. Ele não pode ser substituído por mapeamentos customizados, mas pode ser estendido com
seus próprios escopos. Quando a solicitação de escopo é mapeada para um token de acesso, o valor deve ser uma sequência
e não pode ser prefixado por `appid_` ou ele será ignorado. Em tokens de identidade, as
solicitações `identities` e `oauth_clients` não podem ser modificadas nem
substituídas.

*Créditos normalizados*: cada token de identidade contém um conjunto de solicitações que são
reconhecidas pelo {{site.data.keyword.appid_short_notm}} como solicitações normalizadas. Quando elas estiverem
disponíveis, serão mapeadas diretamente do seu provedor de identidade para o token. Essas solicitações não podem
ser omitidas explicitamente, mas podem ser substituídas por mapeamentos de solicitação customizados. As solicitações incluem `name`, `email`, `picture`, `local` e `gender`.


### Como as reivindicações são mapeadas para os tokens?
{: #custom-claims-mapping}

Cada mapeamento é definido por um objeto de origem de dados e uma chave que é usada para recuperar a solicitação. Cada
solicitação customizada é configurada para cada token separadamente e é aplicada sequencialmente. É possível registrar
até 100 solicitações para cada token até uma carga útil máxima de 100 KB.

<table>
    <thead>
      <th colspan=3><img src="images/idea.png" alt="Ícone de ideia"/> Entendendo objetos de mapeamento de solicitação</th>
    </thead>
    <tbody>
      <tr>
        <td><code><em>source</em></code></td>
        <td>Necessário</td>
        <td>Define a origem da solicitação. Ela pode se referir às informações do usuário do provedor de identidade ou aos atributos customizados do {{site.data.keyword.appid_short_notm}} do usuário. </br> As opções incluem: `saml`,
`cloud_directory`, `facebook`, `google`,
`appid_custom`, `ibmid` e `attributes`.</td>
      </tr>
      <tr>
        <td><code><em>sourceClaim</em></code></td>
        <td>Necessário</td>
        <td>Define a solicitação dos dados de origem. </td>
      </tr>
    </tbody>
  </table>

É possível referenciar as solicitações aninhadas em seus mapeamentos usando a sintaxe de ponto. Exemplo:
`nested.attribute`
{:tip}

</br>

## Configurando os tokens do {{site.data.keyword.appid_short_notm}}
{: #configuring-tokens}

É possível configurar seus tokens do {{site.data.keyword.appid_short_notm}} usando a GUI ou as APIs de
gerenciamento.
{: shortdesc}


### Configurando o tempo de vida do token com a GUI
{: #configuring-tokens-ui}

1. Navegue para o seu painel de serviço.
2. Na seção **Provedores de identidade** da navegação, selecione a página **Gerenciar**.
3. Na guia **Configurações**, configure seus tokens.
  1. Para permitir a conexão sem a necessidade de interação com o usuário, configure **tokens de atualização** como **Ativado**.
  2. Configure o seu tempo de vida do token de atualização. A expiração é configurada em dias e pode ser qualquer valor no intervalo de 1 a 90. Quanto menor o número, mais frequentemente um usuário deverá se conectar.
  3. Configure o seu tempo de vida do token de acesso. A expiração é configurada em minutos e pode estar no intervalo de 5 a 1440. Quanto menor o valor, maior a proteção que você tem em casos de roubo de token.
  4. Configure o seu tempo de vida do token anônimo. Um [token anônimo](/docs/services/appid?topic=appid-anonymous#anonymous) é designado aos usuários no momento em que eles começam a interagir com o seu app. Quando um usuário se conectar, as informações no token anônimo serão, então, transferidas para o token associado ao usuário. A expiração é configurada em dias e pode ser qualquer valor entre 1 e 90.

</br>

### Configurando os tokens com as APIs de gerenciamento
{: #configuring-tokens-api}

**Antes de iniciar**

Certifique-se de que você tenha os pré-requisitos a seguir:

* O seu ID do locatário da instância do {{site.data.keyword.appid_short_notm}}. Isso pode ser localizado na seção **Credenciais de serviço** da GUI.
* O seu token de Gerenciamento de identidade e acesso (IAM). Para obter ajuda para obter um token do IAM, efetue o registro de saída dos [docs do IAM](/docs/iam?topic=iam-iamtoken_from_apikey).

**Mapeando suas solicitações**

1. Faça uma solicitação PUT para o terminal `/config/tokens` com a sua configuração de token.

  Header:
  ```
  PUT {management-url}/management/v4/{tenantId}/tokens
       Host: <management-server-url>
       Authorization: 'Bearer <IAM_TOKEN>'
       Content-Type: application/json
  ```
  {: pre}

  Corpo:
  ```
   {
       "access": {
           "expires_in": 3600,
       },
       "refresh": {
           "expires_in": 2592000,
           "enabled": true
       },
       "anonymous": {
           "expires_in": 2592000,
           "enabled": true
       },
       "accessTokenClaims": [
           {
              "source": "saml", "sourceClaim": "name_id" }
       ], "idTokenClaims": [ {
              "source": "saml",
              "sourceClaim": "attributes.uid"
           }
       ]
   }
  ```
  {: pre}

  <table>
    <thead>
      <th colspan=3><img src="images/idea.png" alt="Ícone de ideia"/> Entendendo a configuração do token</th>
    </thead>
    <tbody>
      <tr>
        <td><code><em>access</em></code></td>
        <td>Opcional</td>
        <td>Objeto que contém o tempo de expiração, `expires_in`, em minutos de seus tokens de acesso e de identidade.</br></br> A expiração padrão é 60 minutos. </td>
      </tr>
      <tr>
          <td><code><em>refresh</em></code></td>
          <td>Opcional</td>
          <td>Objeto que contém o tempo de expiração, `expires_in`, em dias de seu token de atualização.</br></br> A expiração padrão é 30 dias. </td>
      </tr>
      <tr>
          <td><code><em>anonymousAccess</em></code></td>
          <td>Opcional</td>
          <td>Objeto que contém o tempo de expiração, `expires_in`, em dias de seu acesso anônimo e tokens de identidade.</br></br> A expiração padrão é 30 dias.
      </tr>
      <tr>
          <td><code><em>accessTokenClaims</em></code></td>
          <td>Opcional</td>
          <td>Uma matriz que contém os objetos que são criados quando solicitações relacionadas a tokens de acesso são mapeadas.</td>
      </tr>
      <tr>
          <td><code><em>idTokenClaims</em></code></td>
          <td>Opcional</td>
          <td>Uma matriz que contém os objetos que são criados quando solicitações relacionadas a tokens de identidade são mapeadas.</td>
      </tr>
    </tbody>
  </table>

  Solicitação de exemplo:
  ```
  $ curl -X PUT
    --header 'Content-Type: application/json'
    --header 'Accept: application/json'
    --header 'Authorization: <IAM Token'
    -d '{
          "accessTokenClaims": [
            {
              "source": "saml", "sourceClaim": "name_id" }
          ], "idTokenClaims": [ {
              "source": "attributes",
              "sourceClaim": "theme"
            }
          ]
      }'
  }' '{management-url}/management/v4/{Tenant ID}/config/tokens'
  ```
  {: screen}
