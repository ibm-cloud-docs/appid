---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}




# Conceitos-chave
{: #key-concepts}

Confuso sobre as diferenças entre autorização e autenticação? Você não está sozinho. Consulte as informações nesta
página para saber sobre terminologia específica, os processos e a maneira como o serviço usa os tokens.
{: shortdesc}


## Terminologia
{: #terms}


Estes termos chave podem ajudá-lo a entender a maneira como o serviço divide o processo de autorização e autenticação.

<dl>
  <dt>OAuth 2</dt>
    <dd><a href="https://tools.ietf.org/html/rfc6749" target="_blank">OAuth 2 <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> é o protocolo de padrão aberto usado para fornecer autorização de app.</dd>
  <dt>Open ID Connect (OIDC)</dt>
    <dd><p><a href="http://openid.net/developers/specs/" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> é uma camada de autenticação que funciona em cima de OAuth 2.</p>
    <p>Ao usar o OIDC e o {{site.data.keyword.appid_short_notm}} juntos, as suas credenciais de serviço ajudam a
configurar os terminais OAuth. Ao usar o SDK, as URLs de terminal são construídas automaticamente. Mas, também é possível construir
as URLs você mesmo usando as suas credenciais de serviço. É possível ver como montar a URL no exemplo e na tabela a
seguir.</p>
    <pre class="codeblock">
    <code>{
      "version": 3,
      "clientId": "e8ac1132-5151-4d8a-934e-0141de8e2b34",
      "secret": "XYZ5ZYXzXYZtNyz5Yi00YzQ2LXYwMZctXyM5ODA4NjFhYxYZ",
      "tenantId": "3x176051-a23x-40y4-9645-80494 3z660q0",
      "oauthServerUrl": "https: //appid-oauth.ng.bluemix.net/oauth/v3/3x176051-a23x-40y4-9645-804943z660q0",
      "profilesUrl": "https: //appid-profiles.ng.bluemix.net /"
    }</code></pre>
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
        <td>Userinfo</td>
        <td>{ /userinfo</td>
      </tr>
      <tr>
        <td>JWKS</td>
        <td>{ /publickeys</td>
      </tr>
    </table>
    <p><strong>Nota</strong>: ao usar o SDK, as URLs de terminal são construídas automaticamente.</p></dd>
  <dt>Tokens</dt>
    <dd>O serviço usa três tipos diferentes de tokens. Os tokens de acesso representam a autorização e permitem a comunicação com os [recursos de backend](/docs/services/appid/backend-apps.html) que são protegidos por filtros de autorização configurados pelo {{site.data.keyword.appid_short}}. Os tokens de identidade representam a autenticação e contêm informações sobre o usuário. Um
token de atualização pode ser usado para obter um novo token de acesso sem autenticar novamente o usuário. Ao usar tokens de atualização, os usuários podem
permitir que as suas informações sejam lembradas pelo aplicativo. Dessa forma, eles podem permanecer conectados. Para
obter mais informações sobre os tokens e como eles são usados no {{site.data.keyword.appid_short}}, consulte
[Validando os tokens](tokens.html#remote-validation).
  </dd>
  <dt>Cabeçalhos de autorização</dt>
    <dd><p>O {{site.data.keyword.appid_short}} está em conformidade com a <a href="https://tools.ietf.org/html/rfc6750" target="blank">especificação de acesso de token <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> e usa uma combinação de tokens de acesso e de identidade que são enviados como um cabeçalho de Autorização HTTP. O cabeçalho de Autorização contém três partes diferentes que são separadas por espaço em branco. Os tokens são codificados em base64. O token de identidade é opcional.</br>
    Exemplo:</p>
    <pre><code>Authorization=Bearer {access_token} [{id_token}]</pre></code></dd>
  <dt>Estratégia de API</dt>
    <dd><p>A estratégia de API espera que as solicitações contenham um cabeçalho de autorização com um token de acesso válido. A solicitação também pode incluir um token de identidade, mas ele não é necessário. Se um token for inválido ou estiver expirado, a estratégia de API retornará um erro HTTP 401 que contém o cabeçalho de HTTP a seguir:</p> <pre><code>Www-Authenticate=Bearer scope="{scope}" error="{error}"</code></pre>
    <p>Se a solicitação retornar um token válido, o controle será transmitido para o próximo middleware e a propriedade <code>appIdAuthorizationContext</code>
será injetada no objeto de solicitação. Essa propriedade contém tokens de acesso e identidade originais, além de informações de carga útil decodificadas como objetos JSON simples.</dd>
  <dt>Estratégia de aplicativo da web</dt>
    <dd>Quando a estratégia de app da web detecta tentativas não autorizadas para acessar um recurso protegido, ela redireciona automaticamente o navegador de um usuário para a página de autenticação, que pode ser fornecida pelo {{site.data.keyword.appid_short}}. Após a autenticação bem-sucedida, o usuário é retornado à URL de retorno de chamada do aplicativo da web. A estratégia de app da web obtém tokens de acesso e de identidade e os armazena em uma sessão de HTTP sob <code>WebAppStrategy.AUTH_CONTEXT</code>. Cabe ao usuário decidir se deseja armazenar tokens de acesso e de identidade no banco de dados do app.</dd>
  <dt>Separação e criptografia de dados</dt>
    <dd><p>O {{site.data.keyword.appid_short_notm}} armazena e criptografa atributos de perfil do usuário. Como um serviço de múltiplos locatários, cada locatário
tem uma chave de criptografia designada e os dados do usuário em cada locatário são criptografados com apenas essa chave do locatário.</p>
    <p>O {{site.data.keyword.appid_short_notm}} assegura que as informações privadas sejam criptografadas antes de serem armazenadas.</p></dd>
</dl>

</br>
</br>


## Entendendo os tokens
{: #tokens}

Quando um usuário é autenticado com êxito, o aplicativo recebe tokens do {{site.data.keyword.appid_short_notm}}. O serviço usa três tipos principais de tokens para concluir o processo de autenticação.
{: shortdesc}


**O que é um token de acesso?**

Os tokens de acesso representam a autorização e permitem a comunicação com os [recursos de backend](/docs/services/appid/backend-apps.html) que são protegidos por filtros de autorização configurados pelo {{site.data.keyword.appid_short}}. O token adequa-se às especificações do JavaScript Object Signing and Encryption (JOSE). O token é formatado como <a href="https://jwt.io/introduction/" target="blank">Tokens da Web de JSON <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> são assinados com uma Chave da Web de JSON que usa o algoritmo RS256.

Token de exemplo:
  ```
  Header: {
      "typ": "JOSE",
    "alg": "RS256",
}
Payload: {
      "iss": "appid-oauth.ng.bluemix.net",
      "exp": "1495562664",
      "aud": "a3b87400-f03b-4956-844e-a52103ef26ba",
      "amr": ["facebook"],
      "sub": "de6a17d2-693d-4a43-8ea2-2140afd56a22",
      "iat": "1495559064",
      "tenant": "9781974b-6a1c-46c3-aebf-32b7e9bbbaee",
      "scope": "appid_default appid_readprofile appid_readuserattr appid_writeuserattr",
  ```
  {: screen}

**O que é um token de identidade?**

Os tokens de identidade representam a autenticação e contêm informações sobre o usuário. Ele pode fornecer informações sobre seu nome, e-mail, sexo e local. Um token também pode retornar uma URL para uma imagem do usuário. O token é formatado como <a href="https://jwt.io/introduction/" target="blank">Tokens da Web de JSON <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> são assinados com uma Chave da Web de JSON que usa o algoritmo RS256.

Token de exemplo:
  ```
  Header: {
      "typ": "JOSE",
    "alg": "RS256",
}
Payload: {
      "iss": "appid-oauth.ng.bluemix.net",
      "aud": "a3b87400-f03b-4956-844e-a52103ef26ba",
      "exp: "1495562664",
      "tenant": "9781974b-6a1c-46c3-aebf-32b7e9bbbaee",
      "iat": "1495559064",
      "name": "John Smith",
      "email": "js@mail.com",
      "gender", "male",
      "locale": "en",
      "picture": "<URL-to-photo>",
      "sub": "de6a17d2-693d-4a43-8ea2-2140afd56a22",
      "identities": [
          "provider": "facebook"
        "id": "377440159275659"
      ],
    "amr": ["facebook"],
    "oauth_client":{
        "name": "BluemixApp",
      "type": "serverapp",
      "software_id": "cb638f8f-e24b-41d3-b770-23be158dd8e6.2b94e6bb-bac4-4455-8712-a43fa804d5cc.a3b87400-f03b-4956-844e-a52103ef26ba",
      "software_version": "1.0.0",
    }
  }
  ```
  {: screen}

Os tokens de identidade contêm apenas informações parciais sobre o usuário. Para ver todas as informações que são
fornecidas pelo provedor de identidade, é possível usar o [terminal
de informações sobre o usuário](/docs/services/appid/predefined.html#api).

**O que é um token de atualização?**

O {{site.data.keyword.appid_short}} suporta a capacidade de adquirir novos tokens de acesso e de identidade sem autenticação, conforme definido em <a href="http://openid.net/specs/openid-connect-core-1_0.html#RefreshTokens" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>. Um token de atualização pode ser usado para renovar o token de acesso para que um usuário não tenha que executar nenhuma ação para se conectar, como fornecer credenciais. Semelhante
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
poderá usar os tokens de atualização retornados quando o usuário efetuar login inserindo suas credenciais. No entanto,
recomendamos sempre usar o token de atualização mais recente recebido do App ID, conforme descrito pelas <a href="https://tools.ietf.org/html/rfc6749#page-47" target="_blank">Especificações de Oauth <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.


Embora esses tokens possam dinamizar o processo de login, seu aplicativo não deve depender deles, pois eles podem ser revogados a qualquer momento, como quando você acredita que seus tokens de atualização foram comprometidos. Caso seja necessário revogar um token de atualização, há dois métodos de revogação de um token de atualização. Se
você tiver o token de atualização, será possível revogá-lo com base no <a href="https://tools.ietf.org/html/rfc7009#section-2" target="_blank">RFC7009 <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>. Alternativamente, se você tiver o ID do usuário, será possível revogar o token de atualização usando <a href="https://appid-management.ng.bluemix.net/swagger-ui/" target="_blank">a API de gerenciamento <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>. Para
obter mais informações sobre como acessar a API de gerenciamento, consulte
[gerenciando o acesso de serviço](iam.html#service-access-management).

Para obter exemplos de como trabalhar com tokens de atualização e como usá-los para implementar uma funcionalidade Lembrar-me, consulte as [amostras de introdução](index.html).


**De onde vêm os tokens?**

Os tokens são emitidos por meio do servidor OAuth do {{site.data.keyword.appid_short_notm}} e são formatados como [JSON Web Tokens (JWT)](https://jwt.io/introduction/). Os tokens foram assinados com um [JSON Web Key (JWK)](https://tools.ietf.org/html/rfc7517) com o algoritmo RS256.

**O que acontece com as informações que o token contém?**

O token de acesso contém um conjunto de solicitações JWT padrão e um conjunto de solicitações específicas do {{site.data.keyword.appid_short_notm}}, como um ID do locatário. O token de identidade contém informações específicas do usuário. As informações nos tokens são armazenadas como solicitações como parte de um [perfil do usuário](/docs/services/appid/user-profile.html).

**Como os tokens são recebidos?**

Os tokens são recebidos por seu aplicativo após uma autenticação bem-sucedida. Seu aplicativo pode usar os tokens para
recuperar informações sobre a autorização e a autenticação do usuário. O token de acesso pode ser usado para obter acesso a recursos protegidos enviando uma solicitação para o recurso. Na
solicitação, o token de acesso é descrito no [Esquema de
autenticação de portador](https://tools.ietf.org/html/rfc6750#page-5). Para extrair os tokens, o aplicativo deve analisar o cabeçalho.

Solicitação de exemplo:

  ```
  GET /resource HTTP/1.1
  Host: server.example.com
  Authorization: Bearer  mF_9.B5f-4.1JqM mF_9.B5f-4.1JqM
  ```
  {: screen}

</br>
</br>
