---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-05"

keywords: authentication, authorization, identity, app security, secure, application identity, app to app, access token, activity

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


# Eventos do {{site.data.keyword.cloudaccesstrailshort}}
{: #at-events}

É possível visualizar, gerenciar e analisar atividades iniciadas pelo usuário feitas em sua instância de serviço do {{site.data.keyword.appid_full}}
usando o serviço {{site.data.keyword.cloudaccesstrailshort}}.
{: shortdesc}



Para obter mais informações sobre como o serviço funciona, consulte os [docs do {{site.data.keyword.cloudaccesstrailshort}}](/docs/services/cloud-activity-tracker/reference?topic=cloud-activity-tracker-getting-started-with-cla#getting-started-with-cla).


## Visualizando eventos administrativos
{: #at-monitor-admin}

É possível visualizar, gerenciar e analisar a atividade de configuração que é feita em sua instância do {{site.data.keyword.appid_short_notm}} usando o serviço {{site.data.keyword.cloudaccesstrailshort}}.
{: shortdesc}

Para monitorar a atividade administrativa:

1. Efetue login em sua conta do {{site.data.keyword.cloud_notm}}.
2. No catálogo, forneça uma instância do serviço {{site.data.keyword.cloudaccesstrailshort}} na mesma
conta da sua instância do {{site.data.keyword.appid_short_notm}}.
3. No painel {{site.data.keyword.cloudaccesstrailshort}}, clique na guia **Gerenciar**.
4. Na lista suspensa, faça as configurações a seguir para procurar os eventos que são gerados pelo {{site.data.keyword.appid_short_notm}}.
    * Para  ** Visualizar logs **, selecione  ** Registros de contas **.
    * Para  ** Procurar **, selecione  ** target. Management **.
    * Para **Filtro**, insira **appid**.
5. Clique em **Filtrar**.

</br>

## Lista de eventos administrativos
{: #at-events-admin}

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
    <td>Visualize a imagem que é mostrada no widget de login.</td>
    <td>Pode ser localizado na guia <strong>Customização de login</strong>.</td>
  </tr>
  <tr>
    <td><code> update.media </code></td>
    <td>Atualize a imagem que é mostrada no widget de login.</td>
    <td>Pode ser atualizado na guia <strong>Customização de login</strong>.</td>
  </tr>
  <tr>
    <td><code> read.uiConfiguration </code></td>
    <td>Visualize a configuração da IU do widget de login que inclui a cor e a imagem do cabeçalho.</td>
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
    <td>Visualize os metadados do {{site.data.keyword.appid_short_notm}} SAML.</td>
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
    <td>Visualize os detalhes do remetente.</td>
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
    <td>Visualize a confirmação do resultado da conexão.</td>
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



