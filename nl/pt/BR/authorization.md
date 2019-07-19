---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-09"

keywords: Authentication, authorization, identity, app security, secure, access, tokens

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

# Conceitos-chave
{: #key-concepts}

Confuso sobre as diferenças entre autorização e autenticação? Você não está sozinho. Confira as informações a seguir para aprender sobre a terminologia específica, os processos e a forma que o serviço usa tokens.
{: shortdesc}

Quer saber mais sobre alguns dos conceitos básicos de autorização e autenticação? Não procure mais. No vídeo a seguir, é possível aprender sobre o OAuth 2.0, os tipos de concessão, o OIDC e mais.

<iframe class="embed-responsive-item" id="about-appid-basics" title="Sobre o {{site.data.keyword.appid_short_notm}}" type="text/html" width="640" height="390" src="//www.youtube.com/embed/ndlk-ZhKGXM?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>


## Terminologia
{: #terms}

Estes termos chave podem ajudá-lo a entender a maneira como o serviço divide o processo de autorização e autenticação.

### OAuth 2
{: #term-oauth}
O [OAuth 2.0](https://tools.ietf.org/html/rfc6749){: external} é um protocolo de padrão aberto que é usado para fornecer autorização de app.


### Open ID Connect (OIDC)
{: #term-oidc}

O [OIDC](https://openid.net/developers/specs/){: external} é uma camada de autenticação que funciona com o OAuth 2. Quando você usa o OIDC e o {{site.data.keyword.appid_short_notm}} juntos, suas credenciais de aplicativo ajudam a configurar seus terminais OAuth. Se você usar o SDK, as URLs do terminal serão construídas automaticamente. Mas, também é possível construir
as URLs você mesmo usando as suas credenciais de serviço. A URL assume o seguinte formato: {{site.data.keyword.appid_short_notm}} service endpoint + "/oauth/v4" + /tenantID.

Exemplo:

```
{
  "clientId": "7eba72ef-b913-47b0-b3b6-54358bb69035",
  "tenantId": "8f5aa500-357e-443a-aab6-bf878f852b5a",
  "secret": "OWEzZGM4M2UtZjhlYS00MDI2LTkwNGItNDJmYzViMmU2YzIz",
  "name":testing",
  "oAuthServerUrl": "https://us-south.appid.cloud.ibm.com/oauth/v4/8f5aa500-357e-443a-aab6-bf878f852b5a",
  "profilesUrl": "https://us-south.appid.cloud.ibm.com",
  "discoveryEndpoint": "https://us-south.appid.ibm.cloud.com/oauth/v4/8f5aa500-357e-443a-aab6-bf878f852b5a/.well-known/openid-configuration"
}
```
{: screen}

Usando este exemplo, a URL seria `https://us-south.appid.cloud.ibm.com/oauth/v4/3x176051-a23x-40y4-9645-804943z660q0`. Em seguida, você anexaria o terminal para o qual deseja fazer uma solicitação. Consulte a tabela a seguir para ver alguns terminais de exemplo.

<table>
  <tr>
    <th>Ponto de Extremidade</th>
    <th>Formato</th>
  </tr>
  <tr>
    <td>Autorização</td>
    <td>{ /authorization</td>
  </tr>
  <tr>
    <td>Símbolo</td>
    <td>{oauthServerUrl}/token</td>
  </tr>
  <tr>
    <td>Informações do usuário</td>
    <td>{ /userinfo</td>
  </tr>
  <tr>
    <td>JWKS</td>
    <td>{ /publickeys</td>
  </tr>
</table>

Ao usar o SDK, as URLs de terminal serão construídas automaticamente.
{: note}

### Tokens
{: #term-token}

O serviço usa três tipos diferentes de tokens. Os tokens são configurados nos **Provedores de identidade > Gerenciar** do painel do {{site.data.keyword.appid_short}}. Para obter mais informações sobre tokens e como eles são usados no {{site.data.keyword.appid_short}}, consulte [Gerenciando tokens](/docs/services/appid?topic=appid-tokens).

* Tokens de acesso: representam a autorização e permitem a comunicação com os [recursos de back-end](/docs/services/appid?topic=appid-backend) protegidos. Os recursos são protegidos por filtros de autorização que são configurados pelo {{site.data.keyword.appid_short}}.

* Tokens de identidade: representam a autenticação e contêm informações sobre o usuário.

* Tokens de atualização: podem ser usados para obter um novo token de acesso sem autenticar novamente o usuário. Ao usar tokens de atualização, os usuários podem permitir que suas informações sejam lembradas pelo aplicativo, o que significa que eles podem permanecer conectados. 

### Cabeçalhos de autorização
{: #term-auth-header}

O {{site.data.keyword.appid_short}} está em conformidade com a [especificação de portador de token](https://tools.ietf.org/html/rfc6750){: external} e usa uma combinação de tokens de acesso e identidade que são enviadas como um cabeçalho de Autorização HTTP. O Cabeçalho de autorização tem três partes diferentes que são separadas por espaços em branco. Os tokens são codificados em base64. O token de identidade é opcional.

Exemplo:

```
Authorization=Bearer {access_token} [{id_token}]
```
{: screen}


### Estratégia de API
{: #term-api-strategy}

A estratégia de API espera que as solicitações contenham um cabeçalho de autorização com um token de acesso válido. A solicitação também pode incluir um token de identidade, mas ele não é necessário. Se um token for inválido ou estiver expirado, a estratégia de API retornará um erro HTTP 401 que contém o cabeçalho de HTTP a seguir:
```
Www-Authenticate=Bearer scope="{scope}" error="{error}"
```
{: screen}

Se a solicitação retornar um token válido, o controle será transmitido para o próximo middleware e a propriedade `appIdAuthorizationContext`
será injetada no objeto de solicitação. Essa propriedade contém tokens de acesso e identidade originais, além de informações de carga útil decodificadas como objetos JSON simples.

### Estratégia de aplicativo da web
{: #term-web-strategy}

Quando a estratégia de app da web detecta tentativas não autorizadas para acessar um recurso protegido, ela redireciona automaticamente o navegador de um usuário para a página de autenticação, que pode ser fornecida pelo {{site.data.keyword.appid_short}}. Após a autenticação bem-sucedida, o usuário é retornado à URL de retorno de chamada do aplicativo da web. A estratégia de app da web obtém tokens de acesso e de identidade e os armazena em uma sessão de HTTP sob `WebAppStrategy.AUTH_CONTEXT`. Cabe ao usuário decidir se deseja armazenar tokens de acesso e de identidade no banco de dados do app.

### Separação e criptografia de dados
{: #term-data-encryption}

O {{site.data.keyword.appid_short_notm}} armazena e criptografa atributos de perfil do usuário. Como um serviço de múltiplos locatários, cada locatário
tem uma chave de criptografia designada e os dados do usuário em cada locatário são criptografados com apenas essa chave do locatário.

O {{site.data.keyword.appid_short_notm}} assegura que as informações privadas sejam criptografadas antes de serem armazenadas.
{: note}


### URIs de redirecionamento
{: #term-redirect}

O{{site.data.keyword.appid_short_notm}}usa uma lista de URIs totalmente qualificados e aprovados para redirecionar seus usuários após uma interação com seu app. Por exemplo, se o usuário se conecta com êxito, o {{site.data.keyword.appid_short_notm}} redirecionará o usuário para a página inicial de seu aplicativo ou para outra página que você especificar. O formato de seu URI pode mudar, dependendo de seu aplicativo. Consulte [Incluindo URIs de redirecionamento](/docs/services/appid?topic=appid-managing-idp#add-redirect-uri) para obter mais informações.


### Conjunto de chaves da web JSON (JWKS)
{: #term-jwks}

Um JWKS representa um conjunto de chaves criptográficas. O {{site.data.keyword.appid_short_notm}} usa um JWKS para verificar a autenticidade dos tokens que são gerados pelo serviço. Usando o ID de chave para verificar a assinatura, podemos assegurar que o token foi emitido por uma fonte confiável, {{site.data.keyword.appid_short_notm}}, e que as informações no token nunca foram mudadas.


