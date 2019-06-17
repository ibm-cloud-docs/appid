---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-31"

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


# Gerenciando usuários
{: #cd-users}

Com o Cloud Directory, é possível gerenciar seus usuários em um registro escalável usando a funcionalidade pré-construída que aprimora a segurança e o autoatendimento.
{: shortdesc}

Um usuário do Cloud Directory não é a mesma coisa que um usuário do {{site.data.keyword.appid_short_notm}}. Os usuários podem inscrever-se para seu app usando as diferentes opções de provedor de identidade configuradas ou você pode incluí-las em seu diretório. Os usuários mencionados neste tópico são aqueles associados ao Cloud Directory como um provedor de identidade.
{: note}

## Visualizando informações sobre o usuário
{: #cd-user-info}

É possível ver todas as informações conhecidas sobre todos os usuários do Cloud Directory como um objeto JSON usando as APIs ou o painel.
{: shortdesc}


### Com a GUI

É possível usar o painel do {{site.data.keyword.appid_short_notm}} para visualizar detalhes sobre os usuários do app. 

1. Navegue para a guia **Cloud Directory > Usuários** de sua instância do {{site.data.keyword.appid_short_notm}}.

2. Examine a tabela ou procure usando um endereço de e-mail para localizar o usuário do qual você deseja ver as informações.

3. No menu overflow na linha do usuário, clique em **Visualizar detalhes do usuário**. É aberta uma página contendo as informações sobre o usuário. Verifique a tabela a seguir para ver quais informações você pode ver.

<table>
  <tr>
    <th colspan="2">Detalhes do Usuário</th>
  </tr>
  <tr>
    <td>Identificador de usuários</td>
    <td>O identificador de usuários depende do tipo de conexão de usuário que você configurou. Se você tiver um fluxo de e-mail e senha configurado, o identificador será o e-mail do usuário. Se você usar o nome de usuário e o fluxo de senha, o identificador será o nome de usuário fornecido na inscrição.</td>
  </tr>
  <tr>
    <td>E-mail</td>
    <td>O endereço de e-mail principal anexado ao usuário.</td>
  </tr>
    <tr>
    <td>Nome e sobrenome</td>
    <td>O nome e o sobrenome do usuário conforme fornecidos durante o processo de inscrição.</td>
  </tr>
  <tr>
    <td>Último login</td>
    <td>O registro de data e hora da última vez em que o usuário efetuou login em seu aplicativo. Nota: se você tiver incluído o usuário por meio do painel, o login ficará em branco até que o próprio usuário se conecte ao app. Quando a conexão ocorre, ele também se torna um usuário do App ID.</td>
  </tr>
  <tr>
    <td>ID</td>
    <td>O ID designado ao usuário pelo {{site.data.keyword.appid_short_notm}}. Na IU, ele não é mostrado, mas é possível copiar o valor e colá-lo em um editor de texto para ver o valor.</td>
  </tr>
  <tr>
    <td>Atributos predefinidos</td>
    <td>Atributos predefinidos são coisas conhecidas sobre um usuário com base no SCIM.</td>
  </tr>
  <tr>
    <td>Atributos customizados</td>
    <td>Atributos customizados são informações adicionais incluídas no perfil ou que são aprendidas sobre os usuários, à medida que eles interagem com seu aplicativo.</td>
  </tr>
  <tr>
    <td>Resumo</td>
    <td>Todos os atributos são compilados para formar um perfil que fornece uma visão geral completa de seu usuário do Cloud Directory. Para obter mais informações, consulte [perfis do usuário](/docs/services/appid?topic=appid-profiles).</td>
  </tr>
</table>

</br>

### Com a API

É possível usar a API do {{site.data.keyword.appid_short_notm}} para visualizar detalhes sobre os usuários do app. 

1. Obtenha seu ID de locatário em sua instância do serviço.

2. Procure os usuários do App ID com uma consulta de identificação, como um endereço de e-mail, para localizar o ID do usuário.

  ```
  curl -X GET "https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/cloud_directory/Users?query={identifying-search-query}" -H "accept: application/json" -H "authorization: Bearer {token}"
  ```
  {: codeblock}

  Exemplo:

  ```
  curl -X GET https://us-south.appid.cloud.ibm.com/management/v4/e19a2778-3262-4986-8875-8khjafsdkhjsdafkjh/cloud_directory/Users?query=example@email.com -H "accept: application/json" -H "authorization: Bearer eyJraWQiOiIyMDE3MTEyOSIsImFsZ...."
  ```
  {: screen}

3. Usando o ID obtido na etapa anterior, faça uma solicitação GET para o terminal `cloud_directory/users` para ver seu perfil do usuário inteiro.

  ```
  curl -X GET "https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/cloud_directory/Users/{user-ID}" -H "accept: application/json" -H "authorization: Bearer {token}"
  ```
  {: codeblock}

  Resposta de exemplo:

  ```
  {
    sub: "c155c0ff-337a-46d3-a22a-a8f2cca08995",
    name: "Test User",
    email: "testuser@test.com",
    identities: [
      {
        provider: "cloud_directory",
        id: "f1772fcc-ff70-4d88-81a0-07dd7a3d988f",
        idpUserInfo: {
          displayName: "Test User",
          active: true,
          mfaContext: {},
          emails: [
            {
              value: "testuser@test.com",
              primary: true
            }
          ],
          meta: {
            lastLogin: "2019-05-20T16:33:20.699Z",
            created: "2019-05-20T16:25:13.019Z",
            location: "/v1/6b8ab644-1d4a-4b3e-bcd9-777ba8430a51/Users/f1772fcc-ff70-4d88-81a0-07dd7a3d988f",
            lastModified: "2019-05-20T16:33:20.707Z",
            resourceType: "User"
          },
          scemas: [
            "urn:ietf:params:scim:schemas:core:2.0:User"
          ],
          name: {
            givenName: "Test",
            familyName: "User",
            formatted: "Test User"
            },
          id: "f1772fcc-ff70-4d88-81a0-07dd7a3d988f",
          status: "CONFIRMED",
          idpType: "cloud_directory"
        }
      }
    ]
  }
  ```
  {: screen}

  Para ver o conjunto de dados do usuário completo que o {{site.data.keyword.appid_short_notm}} suporta, consulte o [esquema principal do SCIM](https://tools.ietf.org/html/rfc7643#section-8.2).
  {: tip}


## Incluindo e excluindo usuários
{: #add-delete-users}

É possível gerenciar os usuários do Cloud Directory por meio do painel do {{site.data.keyword.appid_short_notm}} ou usando as APIs.
{: shortdesc}

Quando um usuário se inscreve em seu aplicativo, ele faz isso por meio de um fluxo de trabalho de autoatendimento que aciona automaticamente e-mails, como uma solicitação de boas-vindas ou de verificação. Quando você, como administrador, inclui um usuário em seu app, um fluxo de trabalho de autoatendimento não é iniciado, o que significa que os usuários não recebem nenhum e-mail de seu aplicativo. Se você quiser que seus usuários ainda sejam notificados de que foram incluídos, será possível acionar os fluxos de sistema de mensagens por meio da [API de gerenciamento do App ID](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.set_cloud_directory_email_dispatcher).


### Incluindo usuários
{: #add-users}

Quando um usuário se inscreve em seu aplicativo, ele é incluído como um usuário. Para propósitos de teste, é possível incluir um usuário por meio do painel do {{site.data.keyword.appid_short_notm}} ou usando a API.

Se você desativar a inscrição por autoatendimento ou incluir um usuário em seu nome, o usuário não receberá um e-mail de boas-vindas ou de verificação quando for incluído.
{: tip}



**Para incluir um novo usuário com a GUI:**

1. Navegue para a guia **Cloud Directory > Usuários** do painel do {{site.data.keyword.appid_short_notm}}.

2. Clique em **Incluir usuário**. Um formulário é exibido.

3. Insira um **Nome**, **Sobrenome**, **E-mail** e **Senha**. Certifique-se de que o e-mail que você tenta registrar não esteja já tomado por outro usuário. Para ter certeza de que você digitou sua senha corretamente, confirme-a inserindo-a no campo **Reinserir senha**.

4. Clique em **Salvar**. Um usuário do Diretório de Nuvem é criado.

</br>


**Para incluir um novo usuário com a API:**

O fluxo a seguir mostra como incluir um usuário com um e-mail e uma senha. Também é possível optar por usar um fluxo de nome de usuário e senha.

1. Obtenha seu `tenantID` de suas credenciais de aplicativo ou de serviço.

2. Obtenha um token do IAM do {{site.data.keyword.cloud_notm}}.

  ```
  curl --X GET "https://iam.cloud.ibm.com/oidc/token" -H "accept: application/x-www-form-urlencoded"
  ```
  {: codeblock}

3. Com o token obtido na etapa 2, faça uma solicitação de POST para o terminal `cloud-directory/users`. Observe que esse exemplo usa o fluxo de e-mail/senha. Também é possível usar o fluxo de nome de usuário/senha.

  ```
  curl --X POST "https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/cloud_directory/Users"
  -H "accept: application/json"
  -H "content-type: application/json"
  -H "authorization: Bearer {token}"
  -d {
    "displayName": "Test User",
    "password": "{App-ID-Cloud-Directory-User-Password}",
    "active": true,
    "emails": [
      {
        "value": "{App-ID-Cloud-Directory-User-Email}",
        "primary": true
      }
    ]
  }
  ```
  {: codeblock}

</br>


### Excluindo usuários
{: #delete-users}

Se quiser remover um usuário de seu diretório, será possível excluí-lo da GUI ou usando as APIs.
{: shortdesc}

**Para excluir um usuário por meio da GUI:**

1. Navegue para a guia **Cloud Directory > Usuários** do painel do {{site.data.keyword.appid_short_notm}}.

2. Clique na caixa de seleção ao lado do usuário que você deseja excluir. Uma caixa é exibida.

3. Na caixa, clique em **Excluir**. Uma tela é exibida.

4. Confirme que você entende que a exclusão de um usuário não pode ser desfeita clicando em **Excluir**. Se a ação for um erro, será possível incluir o usuário em seu diretório novamente, mas qualquer informação sobre esse usuário não estará mais disponível.

</br>

**Para excluir um usuário usando a API:**

1. Obtenha seu ID de locatário.

2. Usando o e-mail anexado ao usuário, procure seu diretório para localizar o ID do usuário.

  ```
  curl -X GET "https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/users?email={user-email}" -H "accept: application/json"
  ```
  {: codeblock}

3. Exclua o usuário.

  ```
  curl --X DELETE "https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/cloud_directory/Users/{user-GUID}"
  -H "accept: application/x-www-form-urlencoded"
  ```
  {: codeblock}



## Migrando usuários
{: #user-migration}

Ocasionalmente, pode ser necessário configurar uma nova instância do {{site.data.keyword.appid_short_notm}}. Se
você estiver usando o Cloud Directory, isso significará que seus usuários devem ser migrados para a nova instância. É possível usar as APIs de gerenciamento para ajudar com a migração.
{: shortdesc}


Deve-se estar designado à função `Gerenciador`[função do IAM](/docs/iam?topic=iam-getstarted#getstarted) para ambas as instâncias do {{site.data.keyword.appid_short_notm}}.
{: note}


### Exportando
{: cd-export}

Antes de ser possível incluir os usuários na nova instância, é necessário exportá-los da instância atual. Para fazer isso, é possível usar a <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryExport" target="_blank">API de gerenciamento de exportação <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.

Comando cURL de exemplo:

```
curl -X GET --header ‘Accept: application/json’ --header ‘Authorization: Bearer <iam-token>’ ’https://us-south.appid.cloud.ibm.com/management/v4/111c9bj3-xxxx-4b5b-zzzz-24ad9440k8j9/cloud_directory/export?encryption_secret=myCoolSecret'
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
    <td>O ID do locatário de serviço pode ser localizado em suas credenciais de serviço. É possível localizar suas credenciais de serviço no painel do {{site.data.keyword.appid_short_notm}}.</td>
  </tr>
</table>

Somente os usuários do Cloud Directory e seus perfis são retornados. Os usuários de outros provedores de identidade não são.
{: note}


### Importando
{: #cd-import}

Agora que seus usuários estão prontos, é possível importar suas informações para a nova instância. Para fazer isso, é possível usar a <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryImport" target="_blank">API de gerenciamento de importação <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.


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
]}’ ‘https://us-south.appid.cloud.ibm.com/management/v4/111c9bj3-xxxx-4b5b-zzzz-24ad9440k8j9/cloud_directory/import?encryption_secret=myCoolSecret’
```
{: codeblock}



### Script de migração
{: cd-migration-script}

O {{site.data.keyword.appid_short_notm}} fornece um script de migração que pode ser usado por meio da CLI que pode ajudar a acelerar o processo de migração.

Antes de iniciar, certifique-se de que você tenha as informações de parâmetro a seguir:

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
    <td>As opções de região incluem: <code>au-syd</code>, <code>eu-de</code>, <code>eu-gb</code>, <code>jp-tok</code> e <code>us-south</code>.</td>
  </tr>
  <tr>
    <td>Token do IAM</td>
    <td>Certifique-se de ter as permissões de <code>manager</code> antes de obter o token. Para ajuda para obter um token do IAM, consulte <a href="/docs/iam?topic=iam-iamtoken_from_apikey#iamtoken_from_apikey" target="_blank">os docs <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.</td>
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
  users_export_import e00a0366-53c5-4fcf-8fef-ab3e66b2ced8 73321c2b-d35a-497a-9845-15c580fdf58c ng 8 MCAGNS0xJpYI6IlJQiJQQ1ptZIQIJIQIJesG1tJyB3RlB3RlB3RlB3RlB3RlB3RlB3RlB3RlB3RlB3RlB3RlB3Rlb3RlB3Rlb3Rlb3Rlb3Rlb3Rlb3NjjYzc2YTz4NCwiz4NCwiz3MTc2NDg0NDg0LCJpc3MiOzovL2lhbS5zdGFnzTEuYmx1ZW1peC5uZXQvFudon FudF90eFudF90EZ3JhbnQNZIjx.G5QNZIjx.KMjxftjx3XWEphPIzphPIzphPIzphPIjxftzphPIjxftzphPzphPzphPzphPzphPzphPzphPzphl
  ```
  {: codeblock}
