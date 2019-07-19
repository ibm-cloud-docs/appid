---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-09"

keywords: Authentication, authorization, identity, app security, secure, access management, roles, attributes, users

subcollection: appid

---

{:external: target="_blank" .external}
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


# Tutorial: configurando funções de usuário
{: #tutorial-roles}

Assegurar que as pessoas certas tenham o acesso correto no momento certo pode ser difícil quando você está codificando seu aplicativo. Para ajudar com esse processo, é possível usar o {{site.data.keyword.appid_full}} para definir um atributo customizado, como `role`, que permite designar diferentes tipos de usuários. Em seguida, é possível usar seu aplicativo para impor níveis variados de permissões para cada tipo de usuário. Usando esse guia passo a passo, você pode aprender a configurar atributos, atualizá-los e injetá-los em um token usando as APIs do {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

As APIs são uma novidade para você? Experimente com essa [Coleção do Postman](https://github.com/ibm-cloud-security/appid-postman).
{: tip}

## Cenário
{: #roles-scenario}

Você é um desenvolvedor de um parque temático fictício. Você é designado com o gerenciamento de acesso para o [aplicativo da web](/docs/services/appid?topic=appid-web-apps) e sente que a maneira mais fácil de fazer isso é configurando funções para cada tipo de usuário. Você tem vários tipos diferentes de funções, como equipe do parque e visitantes, que precisam de níveis diferentes de permissões. Você deseja ser capaz de aperfeiçoar o processo e assegurar que os usuários tenham a função correta designada a partir da primeira vez que eles se conectem ao aplicativo.  
{: shortdesc}

Sem problemas! É possível usar o [recurso de atributos customizados](/docs/services/appid?topic=appid-profiles) do {{site.data.keyword.appid_short_notm}} para armazenar qualquer tipo de informações relacionadas ao usuário. Portanto, como você está trabalhando com o controle de acesso baseado na função, é possível criar um atributo que é chamado `role` e designar valores diferentes para especificar um tipo de função. Por exemplo, o parque temático pode ter `visitors` ou `staff` que podem ser valores diferentes para o atributo `role`. Em seguida, é possível assegurar que seu código do aplicativo imponha as políticas de acesso e os privilégios que você designou.

Embora este tutorial seja gravado especificamente com apps da web e o Cloud Directory em mente, os atributos podem ser usados em um sentido muito mais amplo. Os atributos customizados podem ser qualquer coisa que você deseja que eles sejam. Desde que você fique abaixo dos atributos de 100k e os formate como um objeto JSON simples, é possível armazenar todos os tipos de informações.
{: note}


## Antes de iniciar
{: #roles-before}

Pronto? Vamos começar.

Certifique-se de que você tenha os pré-requisitos a seguir antes de iniciar:
- Uma instância do serviço do {{site.data.keyword.appid_short_notm}}
- Um conjunto de credenciais de serviço
- Um endereço de e-mail que você pode acessar e validar


## Etapa 1: Configurando a instância do {{site.data.keyword.appid_short_notm}}
{: #roles-configure-app}

Antes de poder iniciar a inclusão de atributos para os usuários do Cloud Land, é necessário configurar a sua instância do {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

1. Na guia **Provedores de identidade** do painel de serviço, ative o **Cloud Directory**. Embora esse tutorial use o [Cloud Directory](/docs/services/appid?topic=appid-cloud-directory), também é possível que você escolha usar qualquer um dos outros IdPs como [SAML](/docs/services/appid?topic=appid-enterprise), [Facebook](/docs/services/appid?topic=appid-social#facebook), [Google](/docs/services/appid?topic=appid-social#google) ou um [provedor customizado](/docs/services/appid?topic=appid-custom-identity).

2. Na guia **Cloud Directory > Verificação de e-mail**, ative a verificação e configure **Permitir que os usuários se conectem ao seu aplicativo sem primeiro verificar seu endereço de e-mail** para **Não**. Ao usar atributos customizados para configurar funções relacionadas a permissões, certifique-se de que os usuários devem validar sua identidade antes que assumam os atributos que você configurou.

3. Na guia **Perfis**, configure **Alterar atributos customizados a partir do app**para **Desativado**.

  Por padrão, os atributos customizados podem ser mudados por qualquer pessoa com um token de acesso. Para assegurar a segurança do aplicativo, você deve configurar o {{site.data.keyword.appid_short_notm}}para que os atributos customizados possam ser alterados apenas pelo administrador ou proprietário do aplicativo. Isso evita que os usuários mudem seus próprios atributos customizados e concedam a si mesmos permissões que não deveriam ter.
  {: important}

Excelente! Seu painel está configurado e você está pronto para iniciar a configuração de funções.


## Etapa 2: configurando funções em nome de outro usuário antes da conexão
{: #roles-set-before}

O Cloud Land tem um novo membro de equipe. Você conhece todas as informações dele, mas ele não começará nos próximos dias. É possível [pré-registrar essas informações](/docs/services/appid?topic=appid-preregister) criando um usuário do {{site.data.keyword.appid_short_notm}} e um perfil que contém os atributos, como a função `staff`.
{: shortdesc}

Esse processo não finaliza o registro do Cloud Directory. O usuário ainda deverá se conectar para que o aplicativo herde o atributo no perfil que você criar.
{: tip}

1. Efetue login no {{site.data.keyword.cloud_notm}} usando a CLI.

  ```
  ibmcloud login
  ```
  {: codeblock}

2. Obtenha um token de acesso do IAM.

  ```
  ibmcloud iam oauth-tokens
  ```
  {: codeblock}

3. Faça uma solicitação de POST para criar um perfil do usuário para o novo usuário que contém o atributo `staff`. Certifique-se de que é possível acessar e validar o e-mail que você usa.

  ```
  curl --request POST \
  https://us-south.appid.cloud.ibm.com/management/v4/{{APPID_TENANT_ID}}/users \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  - d '{
    "idp": "cloud_directory",
    "idp-identity": "user@email.com ",
    "perfil": {
      "attributes" : {
        “role”: “staff”
      }
    }
  }'
  ```
  {: codeblock}

  Saída de resposta bem-sucedida:

  ```
  {
      "id": "5ty78b09-1356-4py8-l45p-808l633101zz"
  }
  ```
  {: screen}

6. Valide se o perfil foi criado com a função `staff`.

  ```
  curl --request GET \
  https://us-south.appid.cloud.ibm.com/management/v4/<tenant-ID>/users?email=<user-email> \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  ```
  {: codeblock}

  Corpo de resposta bem-sucedido:

  ```
  {
      "users": [
          {
              "idp": "nominated_cloud_directory",
              "id": "5ty78b09-1356-4py8-l45p-808l633101zz"
          }
      ]
  }
  ```
  {: screen}

Ótimo trabalho! Você pré-registrou um usuário para o seu aplicativo. Agora, quando ele se conectar ao seu aplicativo com o identificador que você usou para o pré-registro, um usuário do Cloud Directory será criado e ele herdará o perfil do usuário do {{site.data.keyword.appid_short_notm}}. Em seguida, aprenda como atualizar os atributos.


## Etapa 3: Atualizando atributos do usuário
{: #roles-update-attributes}

O Cloud Land está crescendo. Para acompanhar o crescimento, sua empresa está contratando pessoas. O usuário `staff` da etapa dois agora é gerente. É possível atualizar seu perfil [designando uma nova função](/docs/services/appid?topic=appid-profiles#profile-set-custom).
{: shortdesc}

1. Atualize o perfil.

  ```
  curl --request PUT \
  https://us-south.appid.cloud.ibm.com/management/v4/<tenant-id>/users/<user-id>/profile \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  - d '{
    "profile": {
      "attributes" : {
        “role”: “manager”
      }
    }
  }'
  ```
  {: codeblock}

3. Visualize o perfil para verificar se ele foi atualizado corretamente.

  ```
  curl -- request POST \
  GET https://us-south.appid.cloud.ibm.com/management/v4/{{APPID_TENANT_ID}}/users/{{user_profile_id}}/profile \
  -- header 'Authorization: Bearer < iam-access-token>' \
  -- header 'Content-Type: application / json' \
  ```
  {: codeblock}

  Saída de resposta bem-sucedida:

  ```
  {
      "id": "5ce78e09-1356-4ef8-a45d-808b633101db",
      "identities": [],
      "attributes": {
          "role": "manager"
      }
  }
  ```
  {: screen}

Ótimo trabalho!


## Etapa 4: Injetando atributos em tokens
{: #roles-map-claims}

Cada vez mais popular, o parque temático continua a crescer. Com tantos visitantes e membros da equipe novos, você deseja limitar o número de solicitações que são feitas. Para obter melhor desempenho, é possível mapear os atributos do perfil do usuário para as suas solicitações de token de acesso e de identidade. Ao mapear solicitações customizadas, você é capaz de armazenar os atributos customizados nos próprios tokens.
{: shortdesc}

A [configuração do token](/docs/services/appid?topic=appid-customizing-tokens#customizing-tokens) é global, o que significa que ela se aplica a cada usuário com um atributo `role`, independentemente da função real designada a ele.
{: tip}


1. Faça uma solicitação para o terminal de configuração do token.

  ```
  curl --request PUT \
  https://us-south.appid.cloud.ibm.com/management/v4/{{APPID_TENANT_ID}}/config/tokens \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  - d '{
      "access": {
          "expires_in": 3601
      },
      "refresh": {
          "enabled": false,
          "expires_in": 2592001
      },
      "anonymousAccess": {
          "expires_in": 2592001
      },
      "accessTokenClaims": [
      {
      "source": "attributes",
      "sourceClaim": "role"
      }
      ]
  }'
  ```
  {: codeblock}

  <table>
    <tr>
      <th>Variável</th>
      <th>Descrição</th>
    </tr>
    <tr>
      <td><code>tenant-id</code></td>
      <td>Um ID do locatário é como sua instância de {{site.data.keyword.appid_short_notm}}é identificada na solicitação. É possível localizar seu ID na guia <em>Credenciais de serviço</em> do painel. Se você não tiver um conjunto, será possível seguir as etapas na GUI para criar credenciais.</td>
    </tr>
    <tr>
      <td><code>source</code></td>
      <td>Para <code>accessTokenClaim</code> e <code>idTokenClaims</code>, configure a origem para <code>attribute</code>.</td>
    </tr>
    <tr>
      <td><code>sourceClaim</code></td>
      <td>Para <code>accessTokenClaim</code> e <code>idTokenClaims</code>, configure a solicitação de origem para <code>role</code>.</td>
    </tr>
    <tr>
      <td><code>expires_in</code></td>
      <td>Esse valor se aplica a cada tipo de token e deve ser configurado em cada solicitação. Se você configurou anteriormente o valor na GUI e, em seguida, executar essa solicitação, os valores na solicitação substituirão os valores configurados anteriormente. Certifique-se de configurar a expiração para o valor correto para a sua configuração.</td>
    </tr>
  </table>

  Saída de resposta bem-sucedida:

  ```
  {
      "access": {
          "expires_in": 3601
      },
      "refresh": {
          "enabled": false,
          "expires_in": 2592001
      },
      "anonymousAccess": {
          "expires_in": 2592001
      },
      "accessTokenClaims": [
      {
      "source": "attributes",
      "sourceClaim": "role"
      }
      ]
  }
  ```
  {: screen}


## Etapa 5: Visualizando o token de acesso
{: #roles-view-token}

Opcionalmente, é possível verificar se a etapa 4 foi bem-sucedida, visualizando um token de acesso.
{: shortdesc}

1. Para propósitos de teste, crie um usuário do Cloud Directory usando a GUI do {{site.data.keyword.appid_short_notm}}.

  1. Na guia **Usuários**, clique em **Incluir usuário**. Um formulário é exibido.
  2. Insira um primeiro nome e um sobrenome, um e-mail e uma senha.
  3. Clique em **Salvar**.

2. Codifique o ID e o segredo do cliente.

  1. Na guia **Credenciais de serviço**da GUI do {{site.data.keyword.appid_short_notm}}, copie o ID do cliente e o Segredo.
  2. Use um codificador Base64 para codificar suas informações de autorização.
  3. Copie a saída a ser usada no comando a seguir.

4. Conecte-se usando as APIs para obter as informações do token de acesso. O token que é retornado está codificado.

  ```
  curl --request PUT \
  https://appid.cloud.ibm.com/oauth/v4/<tenant-ID>/token \
  --header 'Authorization: Basic <encoded-clientID>:<encoded-client-secret>' \
  --header 'Content-Type: application/x-www-form-urlencoded' \
  --header `Accept: application/json`
  - d 'grant_type=password&username=<user-email>%40<user-email-domain>&password=<user-password>
  ```
  {: codeblock}

5. Decodifique o token de acesso.
  1. Copie o token na saída de resposta do comando anterior.
  2. Em um navegador, navegue para https://jwt.io/.
  3. Cole o token na caixa rotulada **Codificado**.

6. Na seção **Decodificado**, verifique se é possível ver a função.

  ```
  {
    "iss": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61",
    "exp": 1551903163,
    "aud": [
      "968c2306-9aef-4109-bc06-4f5ed6axi24a"
    ],
    "sub": "2b96cc04-eca5-4122-a8de-6e07d14c13a5",
    "email_verified": true,
    "amr": [
      "cloud_directory"
    ],
    "iat": 1551899553,
    "tenant": "39a37f57-a227-4bfe-a044-93b6e6050a61",
    "scope": "openid appid_default appid_readprofile appid_readuserattr appid_writeuserattr appid_authenticated"
    "role": "manager"
  }
  ```
  {: screen}



## Próximas Etapas
{: #roles-next}

Ótimo trabalho! Você concluiu o tutorial. Em seguida, é possível tentar configurar a [autenticação de múltiplos fatores](/docs/services/appid?topic=appid-cd-mfa) ou configurar [sua própria GUI de marca](/docs/services/appid?topic=appid-branded).
