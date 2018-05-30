---

copyright:
  years: 2017, 2018
lastupdated: "2018-05-2"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}

# Autorização e autenticação
{: #authorization}

Com o {{site.data.keyword.appid_full}}, os usuários podem alavancar tokens e filtros de autorização para assegurar que seus apps sejam protegidos. Antes de um usuário ser capaz de conceder autorização para um app, um provedor de identidade deve autenticar sua identidade.
{: shortdesc}


## Conceitos-chave
{: #key-concepts}

Estes termos chave podem ajudá-lo a entender a maneira como o serviço divide o processo de autorização e autenticação.

<dl>
  <dt>OAuth 2</dt>
    <dd><a href="https://tools.ietf.org/html/rfc6749" target="_blank">OAuth 2 <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> é o protocolo de padrão aberto usado para fornecer autorização de app.</dd>
  <dt>Open ID Connect (OIDC)</dt>
    <dd><a href="http://openid.net/developers/specs/" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> é uma camada de autenticação que funciona em cima de OAuth 2.</dd>
  <dt>Tokens de acesso</dt>
    <dd><p>Os tokens de acesso representam a autorização e permitem a comunicação com os [recursos de backend](/docs/services/appid/protecting-resources.html) que são protegidos por filtros de autorização configurados pelo {{site.data.keyword.appid_short}}. O token adequa-se às especificações do JavaScript Object Signing and Encryption (JOSE). Os tokens são formatados como
<a href="https://jwt.io/introduction/" target="blank">Tokens da web da JSON <img src="../../icons/launch-glyph.svg" alt="ícone de Link externo"></a>.</br>
    Exemplo:</p>
    <pre><code>Header: {
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
    </code></pre></dd>
  <dt>Tokens de identidade</dt>
    <dd><p>Os tokens de identidade representam a autenticação e contêm informações sobre o usuário. Ele pode fornecer informações sobre seu nome, e-mail, sexo e local. Um token também pode retornar uma URL para uma imagem do usuário.</br>
    Exemplo:</p>
    <pre><code>Header: {
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
    </pre></code></dd>
  <dt>Token de atualização</dt>
      <dd><p>O {{site.data.keyword.appid_short}} suporta a capacidade de adquirir novos tokens de acesso e de identidade sem autenticação, conforme definido em <a href="http://openid.net/specs/openid-connect-core-1_0.html#RefreshTokens" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.
      Ao conectar-se com um token de atualização, um usuário não tem que tomar nenhuma ação, como fornecer credenciais. Geralmente, os tokens de atualização são configurados para terem um tempo de vida mais longo do que um token de acesso regular.</p><p>
      Para aproveitamento total de tokens de atualização, persista os tokens por tempo de vida integral. Um usuário não pode acessar recursos diretamente com apenas um token de atualização, o que os torna muito mais seguros para persistir do que um token de acesso. Para obter exemplos de como trabalhar com tokens de atualização e como usá-los para implementar uma funcionalidade *lembrar-me*, veja os exemplos de introdução.</p><p>Como uma melhor prática, os tokens de atualização devem ser armazenados com segurança pelo cliente que os recebeu e somente devem ser enviados para o servidor de autorização que os emitiu.</p></dd>
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

## Como o processo funciona
{: #process}

Ao codificar apps, uma das maiores preocupações é a segurança. Como é possível assegurar que somente usuários com o acesso correto estão usando seu app? Você usa um processo de autorização. Na maioria dos processos, a autorização e a autenticação estão atreladas, o que pode tornar a mudança de suas políticas de segurança e provedores de identidade complicada. Com o {{site.data.keyword.appid_short}}, a autorização e a autenticação são processos separados.
{: shortdesc}

Ao configurar provedores de identidade social como o Facebook, o [Fluxo de concessão de autorização Oauth2](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html) é usado para chamar o widget de login. Com o diretório da nuvem como seu provedor de identidade, o [Fluxo de credenciais de senha do proprietário do recurso](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html) é usado para fornecer tokens de acesso e de identidade.

![O caminho para se tornar um usuário identificado.](/images/authenticationtrail.png)

Quando um usuário escolhe conectar-se, ele se torna um usuário identificado. O provedor de identidade retorna tokens de acesso e de identidade para o {{site.data.keyword.appid_short}} que contêm informações sobre o usuário. O serviço usa os tokens fornecidos e determina se um usuário tem as credenciais adequadas para acessar um app. Se os tokens são validados, o serviço autoriza o acesso de usuários. As informações sobre autenticação são associadas ao registro do usuário após ele ser autorizado. O registro e seus atributos poderão ser acessados novamente de qualquer cliente que se autentique com a mesma identidade.

### Autenticação progressiva

Com o {{site.data.keyword.appid_short_notm}}, um usuário anônimo pode escolher se tornar um usuário identificado.

Mas como isso funciona?

Quando um usuário escolhe não se conectar imediatamente, ele é considerado um usuário anônimo. Como um exemplo, um usuário pode começar imediatamente a incluir itens em um carrinho de compras sem se conectar. Para usuários anônimos, o {{site.data.keyword.appid_short_notm}} cria um registro do usuário ad hoc e chama a API de login do OAuth que retorna tokens de acesso anônimo e de identidade. Usando esses tokens, o app pode criar, ler, atualizar e excluir os atributos que são armazenados no registro do usuário.

![O caminho para se tornar um usuário identificado quando ele inicia como anônimo.](/images/anon-authenticationtrail.png)

Quando um usuário anônimo se conecta, seu token de acesso é passado para a API de login. O serviço autentica a chamada com um provedor de identidade. O serviço usa o token de acesso para localizar o registro anônimo e anexa a identidade nele. Os novos tokens de acesso e de identidade contêm as informações públicas que são compartilhadas pelo provedor de identidade. Depois que um usuário é identificado, seu token anônimo torna-se inválido. No entanto, um usuário ainda será capaz de acessar seus atributos porque eles são acessíveis com o novo token.

Uma identidade poderá ser designada a um registro anônimo somente se ele ainda não estiver designado a outro usuário.
{: tip}

Se a identidade já está associada a outro usuário do {{site.data.keyword.appid_short_notm}}, os tokens contêm informações desse registro do usuário e fornecem acesso aos seus atributos. Os atributos de usuários anônimos anteriores não são acessíveis por meio do novo token. Até o token expirar, as informações ainda poderão ser acessadas através do token de acesso anônimo. Durante o desenvolvimento, é possível escolher como mesclar os atributos anônimos para o usuário conhecido.
