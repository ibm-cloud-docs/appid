---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}


# Autenticação de Diversos Fatores
{: #mfa}

A autenticação de diversos fatores (MFA) é um método de confirmação da identidade de um
usuário que exige que ele use algo que tenha além de alguma coisa conhecida para
verificar que ele é quem diz ser. Por exemplo, com o {{site.data.keyword.appid_full}} é possível fazer o
usuário inserir um código único que é enviado para seu e-mail após a inserção de seu e-mail e senha.
{: shortdesc}

A MFA está disponível somente para usuários do Cloud Directory. Se você estiver usando a conexão corporativa com o SAML
2.0 ou o login social, será possível ativar a MFA no provedor de identidade que estiver sendo usado.
{: note}

Quando a MFA está ativada, o widget de login requer a MFA toda vez que um novo usuário tenta se conectar. Depois
que o usuário tiver inserido com êxito suas credenciais, uma senha descartável será enviada para o endereço de e-mail
que ele registrou quando criou sua conta. Cada código tem seis caracteres com uma expiração de cinco minutos. Se um
usuário não receber seu código, ele poderá solicitar o envio de outro código, mas o prazo de expiração não
será reconfigurado. Depois que um código expirar, o usuário será forçado a repetir o processo de login inteiro.

Se um e-mail do usuário ainda não tiver sido confirmado por meio de APIs de gerenciamento ou por meio de verificação de
e-mail na conexão, ele será confirmado quando uma verificação de código da MFA for bem-sucedida. Se for necessário
mudar o endereço de e-mail de um usuário, um administrador poderá usar as
[APIs de gerenciamento](https://appid-management.ng.bluemix.net/swagger-ui/#!/Cloud_Directory_Users/updateCloudDirectoryUser).

A MFA está disponível para as instâncias do {{site.data.keyword.appid_short_notm}} que estão no
[plano de precificação de camada graduada](faq.html#pricing).
{: note}

## Entendendo o fluxo
{: #understanding}



1. A IU de conexão padrão do {{site.data.keyword.appid_short_notm}} é mostrada ao usuário.

2. O usuário insere suas credenciais de usuário do Cloud Directory, como seu e-mail ou nome de usuário e senha.

3. As credenciais são validadas e o formulário MFA é retornado. O formulário solicita ao usuário que cole o código enviado
por e-mail.

4. O usuário recebe uma senha descartável em seu endereço de e-mail e a insere na IU da MFA padrão.

5. O código da MFA é validado e redirecionado para o aplicativo cliente com o código de autorização para continuar o fluxo
do OAuth 2.


</br>

## Configurando a MFA
{: #configuration}

A MFA do {{site.data.keyword.appid_short_notm}} é suportada como parte do fluxo de códigos de autorização
do OAuth 2.0 para usuários do Cloud Directory por meio do widget de login.
{: shortdesc}

Para configurar a MFA por meio da GUI, consulte o [Cloud Directory](cloud-directory.html)
{: note}

### Configurando com a API

É possível configurar a MFA usando as APIs de gerenciamento.
{: shortdesc}

**Antes de iniciar**

Certifique-se de que você tenha os pré-requisitos a seguir:

* O seu ID do locatário da instância do {{site.data.keyword.appid_short_notm}}. Isso pode ser localizado na seção **Credenciais de serviço** do painel.
* O seu token de Gerenciamento de identidade e acesso (IAM). Para obter ajuda para obter um token do IAM, efetue o registro de saída dos [docs do IAM](/docs/iam/apikey_iamtoken.html).


1. Ative a MFA fazendo uma solicitação PUT para o terminal `/config/mfa` com a configuração da MFA
para configurar `isActive` como `true`.

  Header:
  ```
  PUT {management-url}/management/v4/{tenantId}/config/mfa
       Host: <management-server-url>
       Authorization: Bearer <IAM_TOKEN>
       Content-Type: application/json
  ```
  {: pre}

  Corpo:
  ```
   {
       "isActive": true }
  ```
  {: pre}

  Solicitação de exemplo:
  ```
  $ curl -X PUT --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'Authorization: Bearer <IAM_TOKEN>' -d '{
          "isActive": true }'
    }'
    '{management-url}/management/v4/{tenantId}/config/mfa'
  ```
  {: screen}

2. Ative o canal da MFA fazendo uma solicitação PUT para o terminal `/mfa/channels/{channelType}` com a
sua configuração da MFA. Quando `isActive` é configurado como `true`, seu canal da MFA está ativado.

  Header:
  ```
  PUT /management/v4/{tenantId}/mfa/channels/{channelType}
       Host: <management-server-url>
       Authorization: Bearer <IAM_TOKEN>
       Content-Type: application/json
  ```
  {: pre}

  <table>
    <thead>
      <th colspan=3>Tipos de canal suportados</th>
    </thead>
    <tbody>
      <tr>
        <td>`E-mail
`</td>
      </tr>
    </tbody>
  </table>

  Corpo:
  ```
   {
       "isActive": true }
  ```
  {: pre}

  Solicitação de exemplo:
  ```
  $ curl -X PUT --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'Authorization: Bearer <IAM_TOKEN>' -d '{
          "isActive": true }'
    }'
    '{management-url}/management/v4/{tenantId}/mfa/channels/{channelType}'
  ```
  {: screen}

</br>
