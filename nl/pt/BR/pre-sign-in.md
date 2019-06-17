---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-31"

keywords: authentication, authorization, identity, app security, secure, development, user information, attributes, profiles, 

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

# Incluindo atributos antes da conexão do usuário
{: #preregister}

Com o {{site.data.keyword.appid_full}}, é possível iniciar a construção de um perfil para os usuários que você
sabe que precisarão de acesso ao seu aplicativo antes de sua conexão inicial.
{: shortdesc}

Para saber mais sobre os tipos de atributos e as considerações de segurança que devem ser feitas ao trabalhar com atributos customizados, consulte [Armazenando e acessando perfis do usuário](/docs/services/appid?topic=appid-profiles).
{: tip}

## Entendendo o pré-registro
{: #preregister-understand}

### Por que eu desejaria usar o pré-registro?
{: #preregister-why}

Considere um aplicativo no qual você usa o {{site.data.keyword.appid_short_notm}} para federar usuários
existentes por meio de seu provedor de identidade SAML. Você pode desejar que determinados usuários tenham acesso de
`admin` imediatamente ao se conectarem ao aplicativo pela primeira vez. Para que isso aconteça, é possível usar o terminal de pré-registro para configurar um atributo `admin`
customizado para esses usuários e conceder a eles acesso ao console de administração sem qualquer ação adicional de sua
parte. Certifique-se de considerar os [problemas de segurança](/docs/services/appid?topic=appid-profiles#profile-set-custom) que podem surgir
ao mudar a configuração padrão.

### Como os usuários são identificados?
{: #preregister-identify-user}

É possível identificar seus usuários usando um dos seguintes:

* O ID exclusivo do usuário, chamado de **GUID**, no provedor de identidade. Embora esse identificador
sempre exista e sua exclusividade seja garantida, ele nem sempre está prontamente disponível ou é fácil
de entender. Por exemplo, o Cloud Directory usa um GUID de 16 bytes aleatórios.
* Se disponível, o **e-mail** do usuário.

### Quais informações os provedores de identidade fornecem?
{: #preregister-idp-provide}

Efetue o registro de saída da tabela a seguir para ver o tipo de informações de identidade que podem ser usadas.

<table>
  <thead>
    <tr>
      <th>Provedor de
identidade</th>
      <th>GUID</th>
      <th>E-mail</th>
      <th>Sub</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Cloud Directory</td>
      <td><img src="images/confirm.png" width="32" alt="Recurso Disponível" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="Recurso Disponível" style="width:32px;" /></td>
      <td> </td>
    </tr>
    <tr>
      <td>Facebook</td>
      <td><img src="images/confirm.png" width="32" alt="Recurso Disponível" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="Recurso Disponível" style="width:32px;" /></td>
      <td> </td>
    </tr>
    <tr>
      <td>Google</td>
      <td><img src="images/confirm.png" width="32" alt="Recurso Disponível" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="Recurso Disponível" style="width:32px;" /></td>
      <td> </td>
    </tr>
    <tr>
      <td>SAML</td>
      <td></td>
      <td><img src="images/confirm.png" width="32" alt="Recurso Disponível" style="width:32px;" /></td>
      <td> </td>
    </tr>
    <tr>
      <td>Customizado</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Recurso Disponível" style="width:32px;" /></td>
    </tr>
  </tbody>
</table>

### Como o Cloud Directory é manipulado?
{: #preregister-cd}


Para assegurar a integridade dos atributos do usuário pré-registrados, o Cloud Directory impõe requisitos
adicionais a seus usuários. O pré-registro somente pode ocorrer quando a validação de e-mail está
ativada e verificada. Se você pré-registrar um usuário do Cloud Directory com atributos específicos, eles serão destinados a uma pessoa específica. Se
o e-mail não for verificado primeiro, será possível que outro usuário solicite o
endereço de e-mail e quaisquer atributos designados a ele.

1. Configure o Cloud Directory para o modo de e-mail e senha. É possível fazer isso por meio da IU nas configurações
gerais na guia **Cloud Directory**. Também é possível configurá-lo por meio das [APIs de gerenciamento](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.createCloudDirectoryUser).

2. Verifique o endereço de e-mail dos usuários para confirmar sua identidade de uma das maneiras a seguir:

  * Para verificar uma identidade de usuário por meio de e-mail, configure **Verificação de e-mail**
para **Ativado** na guia **Cloud Directory** do painel de serviço. Se um usuário
for incluído por você e se conectar ao seu aplicativo sem primeiro passar pela verificação de e-mail, a conexão será
concluída com êxito, mas seu atributo predefinido será excluído.
  * Para verificar manualmente os usuários, deve-se ser um administrador e usar as [APIs
de gerenciamento](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.createCloudDirectoryUser) do Cloud Directory. Ao criar ou atualizar um usuário, é necessário configurar
explicitamente o campo `status` para `CONFIRMED` dentro da carga útil de dados do usuário.

**Há alguma ação especial que eu devo executar ao usar um provedor de identidade customizado?**

Ao incluir informações sobre o usuário em seu aplicativo antecipadamente, é possível usar qualquer identificador exclusivo
que seja fornecido pelo fluxo de autenticação. O identificador deve corresponder _exatamente_ ao
`sub` do JSON web token assinado que é enviado durante a solicitação de autorização. Se o
identificador não corresponder, então o perfil que você deseja incluir não será vinculado com êxito.



## Incluindo informações sobre o usuário em seu aplicativo
{: #preregister-add-info}

Agora que você aprendeu sobre o processo e considerou suas implicações de segurança, tente incluir um usuário.

**Antes de iniciar:**

Para incluir atributos customizados para um usuário específico com o [terminal da API de gerenciamento /users](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Users/mgmt.users_search_user_profile), deve-se conhecer as informações a seguir:

* Qual provedor de identidade o usuário usará para se conectar.
* O identificador exclusivo do usuário que é fornecido pelo provedor de identidade.

Quando um usuário se conecta ao seu aplicativo pela primeira vez, o {{site.data.keyword.appid_short_notm}} procura o usuário. Se
localizado, o usuário herdará a identidade que você designou. Se o usuário não for localizado, um novo usuário será
criado com base nas informações que são fornecidas pelo provedor de identidade.

**Para incluir um usuário:**

1. Efetue login no IBM Cloud.
  ```
  ibmcloud login
  ```
  {: codeblock}

2. Localize o token do IAM ao executar o comando a seguir.
  ```
  ibmcloud iam oauth-tokens
  ```
  {: codeblock}

3. Faça uma solicitação de POST para o terminal `/users` que contém uma descrição do usuário e os
atributos que você deseja configurar como um objeto JSON.

  Header:
  ```
  POST {management-url}/management/v4/{tenantId}/users
       Host: <management-server-url>
       Authorization: 'Bearer <IAM_TOKEN>'
       Content-Type: application/json
  ```
  {: codeblock}

  Corpo:
  ```
   {
       "idp": "<Identity Provider>",
       "idp-identity": "<User's unique identifier>",
       "profile": {
           "attributes" : {
             "mealPreference":"vegeterian"
           }
       }
   }
  ```
  {: codeblock}

  <table>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="Ícone de ideia"/> Entendendo os componentes</th>
    </thead>
    <tbody>
      <tr>
        <td><code><em>idp</em></code></td>
        <td>O provedor de identidade com o qual o usuário será autenticado. As opções incluem: `saml`,
`cloud_directory`, `facebook`, `google`,
`appid_custom` e `ibmid`.</td>
      </tr>
      <tr>
        <td><code><em>idp-identity</em></code></td>
        <td>O identificador exclusivo fornecido pelo provedor de identidade.</td>
      </tr>
      <tr>
        <td><code><em>profile</em></code></td>
        <td>O perfil do usuário contendo o mapeamento JSON de atributo customizado.</td>
      </tr>
    </tbody>
  </table>

  Solicitação de exemplo:
  ```
  $ curl --request POST \
       --url 'https://{Management_URI}/users \
       --header 'Authorization: Bearer {IAM_TOKEN}' \
       --header 'Content-Type: application/json' \
       --data '{"idp": "saml", "idp-identity": "user@ibm.com", "profile": { "attributes": { "role": "admin",
       "frequent_flyer_points": 1000 }}}'
  ```
  {: screen}

3. Verifique se o registro foi bem-sucedido de uma das seguintes maneiras:
  * Verifique o ID do usuário na resposta.
    ```
    {
        "id": "<{{site.data.keyword.appid_short_notm}} User Id>"
    }
    ```
    {: screen}
  * Verifique o perfil do usuário que foi criado.

Lembre-se de que os atributos predefinidos de um usuário estão vazios até sua primeira autenticação, mas o usuário é,
para todas as intenções e propósitos, um usuário totalmente autenticado. É possível usar seu ID exclusivo assim
como você faria com alguém que já tivesse se conectado. Por exemplo, é possível modificar, procurar ou excluir o perfil.

Agora que você associou um usuário a atributos específicos, tente [acessar ou atualizar atributos](/docs/services/appid?topic=appid-profiles).


</br>
