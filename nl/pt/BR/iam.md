---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# Gerenciando o acesso de serviço
{: #service-access-management}

Com o {{site.data.keyword.appid_full}} e {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM), os proprietários da conta podem gerenciar o acesso de usuário em sua conta.
{: shortdesc}

Como um proprietário da conta, é possível configurar políticas dentro de sua conta para criar diferentes níveis de acesso para diferentes usuários. Por exemplo, alguns usuários podem ter acesso **Somente leitura** para uma instância, mas acesso de **Gravação** para outra. É possível decidir quem pode criar, atualizar e excluir instâncias do {{site.data.keyword.appid_short_notm}}.

Para obter mais informações sobre o IAM, veja [Acesso IAM](/docs/iam/users_roles.html).

## Funções de usuário
{: #roles}

O escopo de uma política de acesso é baseado em uma função designada ao usuário.
{: shortdesc}

As políticas permitem que o acesso seja concedido em diferentes níveis. Algumas das opções incluem:
<ul><ul>
  <li>Acesso em todas as instâncias do serviço em sua conta</li>
  <li>Acesso a uma instância de serviço individual em sua conta</li>
  <li>Acesso a um recurso específico dentro de uma instância</li>
  <li>Acesso a todos os serviços ativados para o IAM em sua conta</li>
</ul></ul>

As funções de gerenciamento de plataforma permitem que os usuários executem tarefas em recursos de serviço no nível de plataforma. Por exemplo, as funções podem ser designadas para determinar quem pode criar ou excluir IDs, criar instâncias e ligar instâncias a apps. A tabela a seguir detalha as ações da forma que se correlacionem às funções de gerenciamento de plataforma.

<table>
  <tr>
    <th>Função da plataforma</th>
    <th>Permissões</th>
    <th>Exemplo de ações</th>
  </tr>
  <tr>
    <td><i>Visualizador</i></td>
    <td>Visualizar instâncias do {{site.data.keyword.appid_short_notm}}.</td>
    <td>É possível ver os dados de um usuário do Diretório da nuvem ou a configuração do provedor de identidade.</td>
  </tr>
  <tr>
    <td><i>Editor
</i></td>
    <td>Visualizar e ligar instâncias do {{site.data.keyword.appid_short_notm}}.</td>
    <td>É possível ligar aplicativos a uma instância do {{site.data.keyword.appid_short_notm}}.</td>
  </tr>
  <tr>
    <td><i>Operador</i></td>
    <td>Criar, excluir, editar, suspender, continuar, visualizar ou ligar instâncias do {{site.data.keyword.appid_short_notm}}.</td>
    <td>É possível criar ou excluir uma instância do {{site.data.keyword.appid_short_notm}} do catálogo.</td>
  </tr>
  <tr>
    <td><i>Administrador</i></td>
    <td>Todas as ações de gerenciamento para todos os serviços na conta.</td>
    <td>É possível executar todas as ações do operador e a capacidade de designar políticas para outros usuários.</td>
  </tr>
</table>

</br>
</br>
A tabela a seguir detalha as ações que são mapeadas para as funções de acesso de serviço. As funções de acesso de serviço permitem que os usuários acessem o {{site.data.keyword.appid_short_notm}} bem como a capacidade de chamar a API do {{site.data.keyword.appid_short_notm}}.


<table>
  <tr>
    <th>Função de serviço</th>
    <th>Permissões</th>
    <th>Exemplo de ações</th>
  </tr>
  <tr>
    <td><i>Reader </i></td>
    <td>Visualizar dados de instância do {{site.data.keyword.appid_short_notm}}.</td>
    <td>Pode visualizar os detalhes da instância de serviço, como dados do usuário ou informações do provedor de identidade.</td>
  </tr>
  <tr>
    <td> <i>Gravador ou gerenciador</i></td>
    <td>Visualizar e mudar uma instância do {{site.data.keyword.appid_short_notm}}.</td>
    <td>Pode executar todas as ações do Leitor e editar a instância de serviço, como editar a configuração do provedor de identidade. </li></ul></td>
  </tr>
</table>

Para obter mais informações sobre como designar funções de usuário na IU, veja [Gerenciando o acesso ao IAM](/docs/iam/mngiam.html#iammanidaccser).


## Políticas de acesso do {{site.data.keyword.appid_short_notm}}
{: #access}

A todo usuário que acessa o serviço {{site.data.keyword.appid_short_notm}} em sua conta deve ser designada uma política de acesso com uma função de usuário do IAM definida. Essa política determina quais ações o usuário pode executar dentro do contexto do serviço ou instância que você seleciona.
{: shortdesc}

As ações são customizadas e definidas pelo serviço {{site.data.keyword.Bluemix_notm}} como operações que podem ser executadas no serviço. As ações são então mapeadas para as funções de usuário do IAM. 
É possível controlar algumas das ações tomadas com o serviço {{site.data.keyword.cloudaccesstrailshort}}. Na tabela a
seguir, as ações e as permissões necessárias para o {{site.data.keyword.appid_short_notm}} são mapeadas.

<table>
  <tr>
    <th>Ação</th>
    <th>Explicação</th>
    <th>Função requerida</th>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-redirect-uris</code></td>
    <td>Visualize as URLs de redirecionamento de pós-autenticação.</td>
    <td>Leitor, Gravador, Gerenciador</td>
  </tr>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-redirect-uris</code></td>
    <td>Inclua ou atualize as URLs de redirecionamento de pós-autenticação.</td>
    <td>Gravador, Gerenciador</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-idps</code></td>
    <td>Atualize a configuração do provedor de identidade.</td>
    <td>Gravador, Gerenciador</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-idps</code></td>
    <td>Visualize a configuração do provedor de identidade.</td>
    <td>Leitor, Gravador, Gerenciador</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-recent-activities</code></td>
    <td>Visualize quaisquer eventos de autenticação recente como uma lista.</td>
    <td>Leitor, Gravador, Gerenciador</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-ui-config</code></td>
    <td>Visualize a configuração do widget de login, como logotipo e cores.</td>
    <td>Leitor, Gravador, Gerenciador</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-ui-config</code></td>
    <td>Atualize a configuração do widget de login.</td>
    <td>Gravador, Gerenciador</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-user-profile-config</code></td>
    <td>Visualize a configuração de perfil do usuário.</td>
    <td>Leitor, Gravador, Gerenciador</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-user-profile-config</code></td>
    <td>Mude a configuração de perfil do usuário.</td>
    <td>Gravador, Gerenciador</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-cd-users</code></td>
    <td>Visualize a configuração de perfil do usuário.</td>
    <td>Leitor, Gravador, Gerenciador</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-add-cd-user</code></td>
    <td>Inclua novos usuários no diretório da nuvem.</td>
    <td>Gravador, Gerenciador</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-cd-user</code></td>
    <td>Atualize os detalhes de um usuário do diretório da nuvem.</td>
    <td>Gravador, Gerenciador</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-delete-cd-user</code></td>
    <td>Exclua um usuário do diretório da nuvem.</td>
    <td>Gravador, Gerenciador</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-email-template</code></td>
    <td>Visualize os modelos de e-mail do diretório da nuvem.</td>
    <td>Leitor, Gravador, Gerenciador</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-update-email-template</code></td>
    <td>Atualize o modelo de e-mail com seu próprio conteúdo.</td>
    <td>Gravador, Gerenciador</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-delete-email-template</code></td>
    <td>Excluir um modelo de e-mail do diretório da nuvem.</td>
    <td>Gravador, Gerenciador</td>
  </tr>
  <tr>
    <td><code> appid-mgmt-get-saml-metadata </code></td>
    <td>Visualize os metadados do provedor de serviços (SP) SAML do diretório da nuvem.</td>
    <td>Leitor, Gravador, Gerenciador</td>
  </tr>
  <tr>
    <td><code> appid-mgmt-post-saml-logotipo </code></td>
    <td>Configure ou atualize a imagem no widget de login para o provedor de identidade SAML.</td>
    <td>Gravador, Gerenciador</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-send-email-cd</code></td>
    <td>Envie um e-mail para um usuário com base em um modelo.</td>
    <td>Gravador, Gerenciador</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-sender-details-cd</code></td>
    <td>Visualize os detalhes do remetente para o e-mail.</td>
    <td>Leitor, Gravador, Gerenciador</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-sender-details-cd</code></td>
    <td>Atualize os detalhes do remetente.</td>
    <td>Gravador, Gerenciador</td>
  </tr>
  <tr>
    <td><code> appid-mgmt-revoke-refresh-token </code></td>
    <td>Revogue o token de atualização de um usuário com o ID do usuário dele.</td>
    <td>Gravador, Gerenciador</td>
  </tr>
</table>

## Rastreando mudanças em suas instâncias do  {{site.data.keyword.appid_short_notm}}
{: #tracking}

É possível visualizar, gerenciar e auditar a atividade de configuração que é feita em sua instância do {{site.data.keyword.appid_short_notm}} usando o serviço {{site.data.keyword.cloudaccesstrailshort}}.
{: shortdesc}

Para monitorar a atividade administrativa:

1. Efetue login em sua conta do {{site.data.keyword.Bluemix_notm}}.
2. No catálogo, forneça uma instância do serviço {{site.data.keyword.cloudaccesstrailshort}} na mesma
conta da sua instância do {{site.data.keyword.appid_short_notm}}.
3. No painel {{site.data.keyword.cloudaccesstrailshort}}, clique na guia **Gerenciar**.
4. Na lista suspensa, faça as configurações a seguir para procurar os eventos que são gerados pelo {{site.data.keyword.appid_short_notm}}.
    * Para  ** Visualizar logs **, selecione  ** Registros de contas **.
    * Para  ** Procurar **, selecione  ** target. Management **.
    * Para  ** Filtro **, insira  ** appid **.
5. Clique em **Filtrar**.


Confira a tabela a seguir para obter uma lista dos eventos enviados para o {{site.data.keyword.cloudaccesstrailshort}}.

<table>
  <tr>
    <th>Ação</th>
    <th>Descrição</th>
    <th>Local da UI</th>
  </tr>
  <tr>
    <td><code> read.recentActivity </code></td>
    <td>Visualizar atividade recente.</td>
    <td>Pode ser localizado na caixa <strong>Log de atividades</strong> na guia <strong>Visão geral</strong>.</td>
  </tr>
  <tr>
    <td><code> read.idpConfig </code></td>
    <td>Visualize a configuração do provedor de identidade.</td>
    <td>Pode ser localizado na guia <strong>Fornecedores de identidade > Gerenciar</strong>.</td>
  </tr>
  <tr>
    <td><code> update.idpConfig </code></td>
    <td>Atualize a configuração do provedor de identidade.</td>
    <td>Pode ser atualizado na guia <strong>Provedores de identidade > Gerenciar</strong>.</td>
  </tr>
  <tr>
    <td><code> read.tokensConfig </code></td>
    <td>Visualize a configuração de expiração do token.</td>
    <td>Pode ser localizado na guia <strong>Provedores de identidade > Expiração de token</strong>.</td>
  </tr>
  <tr>
    <td><code> read.isProfilesActive </code></td>
    <td>Visualize a configuração de armazenamento de perfil do usuário.</td>
    <td>Pode ser localizado no <strong>Log de atividades</strong> na guia <strong>Visão geral</strong>.</td>
  </tr>
  <tr>
    <td><code> update.isProfilesActive </code></td>
    <td>Atualize a configuração de armazenamento de perfil do usuário.</td>
    <td>Pode ser localizado na guia <strong>Perfis</strong>.</td>
  </tr>
  <tr>
    <td><code> read.themeColor </code></td>
    <td>Visualize a cor do tema do cabeçalho do widget de login.</td>
    <td>Pode ser localizado na guia <strong>Customização de login</strong>.</td>
  </tr>
  <tr>
    <td><code>update.themeColor</code></td>
    <td>Atualize a cor do tema do cabeçalho do widget de login.</td>
    <td>Pode ser atualizado na guia <strong>Customização de login</strong>.</td>
  </tr>
  <tr>
    <td><code> read.media </code></td>
    <td>Visualize a imagem que é exibida no widget de login.</td>
    <td>Pode ser localizado na guia <strong>Customização de login</strong>.</td>
  </tr>
  <tr>
    <td><code> update.media </code></td>
    <td>Atualize a imagem que é exibida no widget de login.</td>
    <td>Pode ser atualizado na guia <strong>Customização de login</strong>.</td>
  </tr>
  <tr>
    <td><code> read.uiConfiguration </code></td>
    <td>Visualize a configuração da UI do widget de login incluindo a cor do cabeçalho e a imagem.</td>
    <td>Pode ser localizado na guia <strong>Customização de login</strong>.</td>
  </tr>
  <tr>
    <td><code> read.uiLanguages </code></td>
    <td>Visualizar uma lista de idiomas suportados.</td>
    <td>Deve ser visualizado a partir da API.</td>
  </tr>
  <tr>
    <td><code> update.uiLanguages </code></td>
    <td>Atualize seus idiomas suportados.</td>
    <td>Deve ser atualizado por meio da API.</td>
  </tr>
  <tr>
    <td><code> read.samlMetadata </code></td>
    <td>Visualize os metadados do SAML do ID do app.</td>
    <td>Pode ser localizado na guia <strong>Provedores de identidade > Federação SAML 2.0</strong>.</td>
  </tr>
  <tr>
    <td><code> read.cloudDirectoryUser </code></td>
    <td>Visualizar um usuário do Cloud Directory.</td>
    <td>Pode ser localizado na guia <strong>Usuários</strong>.</td>
  </tr>
  <tr>
    <td><code> update.cloudDirectoryUser </code></td>
    <td>Atualizar um usuário do Cloud Directory.</td>
    <td>Pode ser atualizado na guia <strong>Usuários</strong>.</td>
  </tr>
  <tr>
    <td><code>delete.cloudDirectoryUser</code></td>
    <td>Excluir um usuário do Cloud Directory.</td>
    <td>Pode ser excluído na guia <strong>Usuários</strong>.</td>
  </tr>
  <tr>
    <td><code> read.cloudDirectoryUsers </code></td>
    <td>Visualize uma lista de usuários do Cloud Directory.</td>
    <td>Pode ser localizado na guia <strong>Usuários</strong>.</td>
  </tr>
  <tr>
    <td><code> update.cloudDirectoryUsers </code></td>
    <td>Atualize a lista de usuários do Cloud Directory.</td>
    <td>Pode ser atualizado na guia <strong>Usuários</strong>.</td>
  </tr>
  <tr>
    <td><code> delete.cloudDirectoryUsers </code></td>
    <td>Exclua uma lista de usuários do Cloud Directory.</td>
    <td>Pode ser excluído na guia <strong>Usuários</strong>.</td>
  </tr>
  <tr>
    <td><code> read.emailTemplate </code></td>
    <td>Visualizar um modelo de e-mail.</td>
    <td>Pode ser localizado na guia <strong>Provedores de identidade > Cloud Directory > Modelos</strong>.</td>
  </tr>
  <tr>
    <td><code> update.emailTemplate </code></td>
    <td>Atualizar um modelo de e-mail.</td>
    <td>Pode ser localizado na guia <strong>Provedores de identidade > Cloud Directory > Modelos</strong>.</td>
  </tr>
  <tr>
    <td><code> delete.emailTemplate </code></td>
    <td>Exclua um modelo de e-mail para reconfigurar para o padrão.</td>
    <td>Pode ser localizado na guia <strong>Provedores de identidade > Cloud Directory > Modelos</strong>.</td>
  </tr>
  <tr>
    <td><code> read.senderDetails </code></td>
    <td>Visualize os detalhes do emissor.</td>
    <td>Pode ser localizado na guia <strong>Provedores de identidade > Cloud Directory > Configurações</strong>.</td>
  </tr>
  <tr>
    <td><code> update.senderDetails </code></td>
    <td>Atualizar os Detalhes do Remetente</td>
    <td>Pode ser localizado na guia <strong>Provedores de identidade > Cloud Directory > Configurações</strong>.</td>
  </tr>
  <tr>
    <td><code> update.resendNotification </code></td>
    <td>Reenviar notificações do usuário.</td>
    <td>Pode ser localizado na guia <strong>Provedores de identidade > Cloud Directory > Configurações</strong>.</td>
  </tr>
  <tr>
    <td><code> update.selfForgotPassword </code></td>
    <td>Atualize o processo de senha esquecida.</td>
    <td>Pode ser localizado na guia <strong>Provedores de identidade > Cloud Directory > Configurações</strong>.</td>
  </tr>
  <tr>
    <td><code> update.forgotPasswordResult </code></td>
    <td>Visualize o resultado de confirmação de senha esquecida.</td>
    <td>Deve ser feito por meio da API.</td>
  </tr>
  <tr>
    <td><code> update.selfSignUp </code></td>
    <td>Atualize o processo de conexão.</td>
    <td>Pode ser localizado na guia <strong>Provedores de identidade > Cloud Directory > Configurações</strong>.</td>
  </tr>
  <tr>
    <td><code> update.signUpResult </code></td>
    <td>Visualize a confirmação do resultado da assinatura.</td>
    <td>Deve ser feito por meio da API.</td>
  </tr>
  <tr>
    <td><code> read.action_url </code></td>
    <td>Visualize a URL customizada chamada quando uma ação é executada.</td>
    <td>Pode ser localizada na guia <strong>Provedores de identidade > Cloud Directory > Páginas de entrada customizada</strong>.</td>
  </tr>
  <tr>
    <td><code>update.action_url</code></td>
    <td>Atualize a URL customizada chamada quando uma ação é executada.</td>
    <td>Pode ser localizado na guia <strong>Provedores de identidade > Cloud Directory > Configurações</strong>.</td>
  </tr>
  <tr>
    <td><code> update.changePassword </code></td>
    <td>Altere a senha do usuário do Cloud Directory.</td>
    <td>Pode ser localizado na guia <strong>Provedores de identidade > Cloud Directory > Configurações</strong>.</td>
  </tr>
  <tr>
    <td><code> read.loginWidgetConfig </code></td>
    <td>Visualize a configuração do seu widget de login.</td>
    <td>Pode ser localizado na guia <strong>Customização de login</strong>.</td>
  </tr>
  <tr>
    <td><code> update.loginWidgetConfig </code></td>
    <td>Atualize a configuração do seu widget de login.</td>
    <td>Pode ser atualizado na guia <strong>Customização de login</strong>.</td>
  </tr>
</table>


Para obter mais informações sobre como o serviço funciona, consulte os
[docs do {{site.data.keyword.cloudaccesstrailshort}}](/docs/services/cloud-activity-tracker/index.html).

</br>
</br>

## Exemplo: fornecendo a outro usuário acesso a uma instância do {{site.data.keyword.appid_short_notm}}
{: #example}

Neste cenário, um administrador criou uma instância do {{site.data.keyword.appid_short_notm}} e precisa conceder acesso de visualizador para outro membro da equipe.
{: shortdesc}

Antes de iniciar:
* Instale a CLI do [{{site.data.keyword.Bluemix_notm}}](/docs/cli/index.html).

Para atualizar permissões de acesso, o administrador conclui as etapas a seguir:

1. Efetue login no console do
{{site.data.keyword.Bluemix_notm}}.
2. Forneça ao funcionário acesso de visualização seguindo as etapas que estão definidas na [documentação do IAM](/docs/iam/iamusermanage.html#iamusermanage).
3. Navegue para a guia **Credenciais de serviço** no painel {{site.data.keyword.appid_short_notm}}. Clique em **Visualizar credenciais** e copie o **tentantID**.
4. Conecte-se com a CLI do {{site.data.keyword.Bluemix_notm}} em seu terminal.
    ```
    bx login -a api.<region>.bluemix.net
    ```
    {: codeblock}
5. Obtenha um token IAM e tome nota disso.
    ```
    bx iam oauth-tokens
    ```
    {: codeblock}
6. Verifique se o membro da equipe não pode fazer mudanças.
    ```
    curl -X PUT --header 'Content-Type: application/json' \
    --header 'Accept: application/json' \
    --header 'Authorization: <IAM token value>' \
    -d '{
     "isActive": false,
     "config": {
       "idpId": "appID",
       "secret": "appsecret"
     }
    }' \
    'https://appid-management.ng.bluemix.net/management/v4/ < tenantId> /config/idps/facebook '
    ```
    {: codeblock}

    O resultado é uma mensagem 403 desautorizada.

Para visualizar as configurações do {{site.data.keyword.appid_short_notm}} da CLI, o membro da equipe conclui as etapas a seguir:

1. Usando a CLI do {{site.data.keyword.Bluemix_notm}} em seu terminal, conecte-se.
    ```
    bx login -a api.<region>.bluemix.net
    ```
    {: codeblock}
2. Obtenha um token IAM e tome nota disso.
    ```
    bx iam oauth-tokens
    ```
    {: codeblock}
3. Visualize a configuração do provedor de identidade para o Facebook usando cURL.
    ```
    curl -X GET --header 'Accept: application/json' --header 'Authorization: <IAM token value>' \  'https://appid-management.ng.bluemix.net/management/v4/<tenantId>/config/idps/facebook'
    ```
    {: codeblock}
    O resultado é uma mensagem 200 que contém as informações do provedor de identidade.
