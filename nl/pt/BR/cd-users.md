---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

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

Quando você ativa o Cloud Directory, os usuários podem se conectar ao seu aplicativo usando um e-mail ou nome de usuário e senha.
{: shortdesc}


Um usuário do Cloud Directory não é a mesma coisa que um usuário do {{site.data.keyword.appid_short_notm}}. Os usuários podem se conectar ao seu aplicativo usando diferentes opções do provedor de identidade que você configurou. Os usuários mencionados neste tópico são aqueles que optaram por usar a opção do Diretório de Nuvem ao se inscrever para seu app.
{: note}


## Incluindo e excluindo usuários
{: #add-delete-users}

É possível gerenciar os usuários do Cloud Directory por meio do painel do {{site.data.keyword.appid_short_notm}} ou usando as APIs.
{: shortdesc}

Para ver os dados completos para um usuário específico, é possível usar as APIs para retornar as informações do usuário do Cloud Directory como um objeto JSON. Para ver o conjunto de dados do usuário completo que o {{site.data.keyword.appid_short_notm}} suporta, consulte o [esquema principal do SCIM](https://tools.ietf.org/html/rfc7643#section-8.2).

### Incluindo usuários
{: #add-users}

É possível usar as etapas a seguir para incluir um usuário por meio do painel do {{site.data.keyword.appid_short_notm}}.

Para propósitos de teste, é possível incluir um usuário por meio do painel do {{site.data.keyword.appid_short_notm}}.

1. Navegue para a guia **Cloud Directory > Usuários** do painel do {{site.data.keyword.appid_short_notm}}.

2. Clique em **Incluir usuário**. Um formulário é exibido.

3. Insira um **Nome**, **Sobrenome**, **E-mail** e **Senha**. Certifique-se de que o e-mail que você tenta registrar não esteja já tomado por outro usuário. Para ter certeza de que você digitou sua senha corretamente, confirme-a inserindo-a no campo **Reinserir senha**.

4. Clique em **Salvar**. Um usuário do Diretório de Nuvem é criado.


### Excluindo usuários
{: #delete-users}

Se você deseja remover um usuário de seu diretório, será possível excluir o usuário por meio da GUI.

1. Navegue para a guia **Cloud Directory > Usuários** do painel do {{site.data.keyword.appid_short_notm}}.

2. Clique na caixa de seleção ao lado do usuário que você deseja excluir. Uma caixa é exibida.

3. Na caixa, clique em **Excluir**. Uma tela é exibida.

4. Confirme que você entende que a exclusão de um usuário não pode ser desfeita clicando em **Excluir**. Se a ação for um erro, será possível incluir o usuário em seu diretório novamente, mas qualquer informação sobre esse usuário não estará mais disponível.


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
    <td>Certifique-se de ter as permissões de <code>manager</code> antes de obter o token. Para ajuda para obter um token do IAM, consulte <a href="https://cloud.ibm.com/docs/iam/apikey_iamtoken.html#iamtoken_from_apikey" target="_blank">os docs <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.</td>
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
