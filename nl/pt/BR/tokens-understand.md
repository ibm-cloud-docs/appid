---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-05"

keywords: authentication, authorization, identity, app security, secure, access, tokens

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



# Entendendo os tokens
{: #tokens}

Quando um usuário é autenticado com êxito, o aplicativo recebe tokens do {{site.data.keyword.appid_short_notm}}. O serviço usa três tipos principais de tokens para concluir o processo de autenticação.
{: shortdesc}


## Tokens de acesso
{: #access}

Os tokens de acesso representam a autorização e permitem a comunicação com os [recursos de backend](/docs/services/appid?topic=appid-backend) que são protegidos por filtros de autorização configurados pelo {{site.data.keyword.appid_short}}. O token adequa-se às especificações do JavaScript Object Signing and Encryption (JOSE). O token é formatado como <a href="https://jwt.io/introduction/" target="blank">Tokens da Web de JSON <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> são assinados com uma Chave da Web de JSON que usa o algoritmo RS256.

Token de exemplo:
  ```
  Header: {
    "alg": "RS256",
    "typ": "JWT",
    "kid": "appId-39a37f57-a227-4bfe-a044-93b6e6050a61-2018-08-02T11:57:43.401",
    "ver": 4
  }
  Payload: {
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
  }
  ```
  {: screen}

## O que são tokens de identidade?
{: #identity}

Os tokens de identidade representam a autenticação e contêm informações sobre o usuário. Ele pode fornecer informações sobre seu nome, e-mail, sexo e local. Um token também pode retornar uma URL para uma imagem do usuário. O token é formatado como <a href="https://jwt.io/introduction/" target="blank">Tokens da Web de JSON <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> são assinados com uma Chave da Web de JSON que usa o algoritmo RS256.

Token de exemplo:
  ```
  Header: {
    "alg": "RS256",
    "typ": "JWT",
    "kid": "appId-39a37f57-a227-4bfe-a044-93b6e6050a61-2018-08-02T11:57:43.401",
    "ver": 4
  }
  Payload: {
    "iss": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61",
    "aud": [
      "968c2306-9aef-4109-bc06-4f5ed6axi24a"
    ],
    "exp": 1551903163,
    "tenant": "39a37f57-a227-4bfe-a044-93b6e6050a61",
    "iat": 1551899553,
    "email": "appid155@mailinator.com",
    "name": "appid155@mailinator.com",
    "sub": "2b96cc04-eca5-4122-a8de-6e07d14c13a5",
    "email_verified": true,
    "identities": [
      {
        "provider": "cloud_directory",
        "id": "118c0278-3526-4954-876b-cf70eb88efa2"
      }
    ],
    "amr": [
      "cloud_directory"
    ]
  }
  ```
  {: screen}


Os tokens de identidade contêm apenas informações parciais sobre o usuário. Para ver todas as informações que são fornecidas pelo provedor de identidade, é possível usar o [terminal /userinfo](/docs/services/appid?topic=appid-profiles#profile-predefined-api).

## O que são tokens de atualização?
{: #refresh}

O {{site.data.keyword.appid_short}} suporta a capacidade de adquirir novos tokens de acesso e de identidade sem autenticação, conforme definido em <a href="https://openid.net/specs/openid-connect-core-1_0.html#RefreshTokens" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>. Um token de atualização pode ser usado para renovar o token de acesso para que um usuário não tenha que executar nenhuma ação para se conectar, como fornecer credenciais. Semelhante
aos tokens de acesso, os tokens de atualização contêm dados que permitem ao
{{site.data.keyword.appid_short_notm}} determinar se você está autorizado. No entanto, esses tokens são opacos.

Os tokens de atualização são configurados para ter um tempo de vida mais longo do que um token de acesso regular,
portanto, quando um token de acesso expirar, o token de atualização ainda será válido e poderá ser usado para renovar o token de acesso. Os tokens de atualização do {{site.data.keyword.appid_short_notm}} podem ser configurados para durar de 1 a 90 dias. Para
tirar total proveito dos tokens de atualização, persista os tokens para seu tempo de vida integral ou até que
sejam renovados. Um usuário não pode acessar recursos diretamente com apenas um token de atualização, o que os torna muito mais seguros para persistir do que um token de acesso. Como
melhor prática, os tokens de atualização devem ser armazenados com segurança pelo cliente que os recebeu e enviados
apenas para o servidor de autorizações que os emitiu.

Para maior conveniência, o {{site.data.keyword.appid_short_notm}} também renova seu token de atualização
e a sua data de expiração quando o token de acesso é renovado, permitindo que o usuário permaneça com login efetuado
desde que esteja ativo em algum ponto antes da expiração do token de atualização atual. Por outro lado, se você
quiser usar os tokens de atualização e ainda forçar o usuário a efetuar login periodicamente, seu aplicativo somente
poderá usar os tokens de atualização retornados quando o usuário efetuar login inserindo suas credenciais. No entanto, recomendamos sempre usar o token de atualização mais recente recebido do {{site.data.keyword.appid_short_notm}}, conforme descrito pelas <a href="https://tools.ietf.org/html/rfc6749#page-47" target="_blank">especificações do OAuth 2.0 <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.


Embora esses tokens possam dinamizar o processo de login, seu aplicativo não deve depender deles, pois eles podem ser revogados a qualquer momento, como quando você acredita que seus tokens de atualização foram comprometidos. Caso seja necessário revogar um token de atualização, há dois métodos de revogação de um token de atualização. Se
você tiver o token de atualização, será possível revogá-lo com base no <a href="https://tools.ietf.org/html/rfc7009#section-2" target="_blank">RFC7009 <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>. Alternativamente, se você tiver o ID do usuário, será possível revogar o token de atualização usando <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/" target="_blank">a API de gerenciamento <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>. Para
obter mais informações sobre como acessar a API de gerenciamento, consulte
[gerenciando o acesso de serviço](/docs/services/appid?topic=appid-service-access-management#service-access-management).

Para obter exemplos de como trabalhar com tokens de atualização e como usá-los para implementar uma funcionalidade Lembrar-me, consulte as [amostras de introdução](/docs/services/appid?topic=appid-getting-started#getting-started).


## De onde vêm os tokens?
{: #where}

Os tokens são emitidos por meio do servidor OAuth do {{site.data.keyword.appid_short_notm}} e são formatados como [JSON Web Tokens (JWT)](https://jwt.io/introduction/). Os tokens foram assinados com um [JSON Web Key (JWK)](https://tools.ietf.org/html/rfc7517) com o algoritmo RS256.

## O que acontece com as informações que o token contém?
{: #contains}

O token de acesso contém um conjunto de solicitações JWT padrão e um conjunto de solicitações específicas do {{site.data.keyword.appid_short_notm}}, como um ID do locatário. O token de identidade contém informações específicas do usuário. As informações nos tokens são armazenadas como solicitações como parte de um [perfil do usuário](/docs/services/appid?topic=appid-profiles).

## Como os tokens são recebidos?
{: #received}

Os tokens são recebidos por seu aplicativo após uma autenticação bem-sucedida. Seu aplicativo pode usar os tokens para
recuperar informações sobre a autorização e a autenticação do usuário. O token de acesso pode ser usado para obter acesso a recursos protegidos enviando uma solicitação para o recurso. Na solicitação, o token de acesso é descrito no [Esquema de autenticação de portador](https://tools.ietf.org/html/rfc6750#page-5). Para extrair os tokens, o aplicativo deve analisar o cabeçalho.

Solicitação de exemplo:

  ```
  GET /resource HTTP/1.1
  Host: server.example.com
  Authorization: Bearer  mF_9.B5f-4.1JqM mF_9.B5f-4.1JqM
  ```
  {: screen}

## Como os tokens são configurados?
{: #set}

As configurações de token podem ser ativadas e desativadas por meio do painel do {{site.data.keyword.appid_short_notm}}. Para obter mais informações sobre suas opções de configuração, consulte [Gerenciando tokens](/docs/services/appid?topic=appid-managing-idp#managing-idp).
