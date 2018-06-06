---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-01"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Autorização e autenticação
{: authorization}

Com o {{site.data.keyword.appid_full}}, os usuários podem alavancar tokens e filtros de autorização para assegurar que seus apps sejam protegidos. Antes que um usuário possa conceder autorização, sua identidade deve ser autenticada por um provedor de identidade.
{: shortdesc}


## Conceitos-chave
{: key-concepts}

Para entender realmente a maneira como o serviço divide o processo de autorização e autenticação, você precisará ter um entendimento de alguns termos chave.

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
</dl>

</br>

## Como o processo funciona
{: #process}

Ao codificar apps, uma das maiores preocupações é a segurança. Como é possível assegurar que somente aqueles com o acesso correto estejam usando seu app? Você usa um processo de autorização. Na maioria dos aplicativos, o processo de autorização e autenticação está associado; tornando complicadas as mudanças em suas políticas de segurança e provedores de identidade. Com o {{site.data.keyword.appid_short}}, a autorização e a autenticação são processos separados.
{: shortdesc}

Ao configurar provedores de identidade social como o Facebook, o [Fluxo de concessão de autorização Oauth2](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html) é usado para chamar o widget de login. Com o diretório da nuvem como seu provedor de identidade, o [Fluxo de credenciais de senha do proprietário do recurso](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html) é usado para fornecer tokens de acesso e de identidade.

![O caminho para se tornar um usuário identificado.](/images/authenticationtrail.png)

Quando um usuário escolhe conectar-se, ele se torna um usuário identificado. As informações sobre o usuário são obtidas do provedor de identidade ao qual ele foi conectado. O provedor de identidade retorna tokens de acesso e de identidade para o {{site.data.keyword.appid_short}} que contêm informações sobre o usuário. O serviço usa os tokens fornecidos e determina se um usuário tem as credenciais adequadas para acessar um app. Se os tokens são validados, o serviço autoriza o acesso dos usuários. Depois que um usuário é autorizado, suas informações sobre autenticação são associadas a um registro do usuário. O registro e seus atributos poderão ser acessados novamente de qualquer cliente que se autentique com a mesma identidade.

### Autenticação progressiva

Com o {{site.data.keyword.appid_short_notm}}, um usuário anônimo pode escolher se tornar um usuário identificado.

Mas como isso funciona?

Quando um usuário escolhe não se conectar imediatamente, ele é considerado um usuário anônimo. Como um exemplo, um usuário poderia iniciar imediatamente a inclusão de itens em um carrinho de compras sem se conectar. Para usuários anônimos, o {{site.data.keyword.appid_short_notm}} cria um registro do usuário ad hoc e chama a API de login do OAuth, que retorna tokens de acesso e de identidade anônimos. Usando esses tokens, o app pode criar, ler, atualizar e excluir os atributos que são armazenados no registro do usuário.

![O caminho para se tornar um usuário identificado quando ele inicia como anônimo.](/images/anon-authenticationtrail.png)

Quando um usuário anônimo se conecta, o token de acesso anônimo é passado para a API de login. O serviço autentica a chamada com um provedor de identidade. O serviço usa o token de acesso para localizar o registro anônimo e anexa a identidade nele. Os novos tokens de acesso e de identidade contêm as informações públicas que são compartilhadas pelo provedor de identidade. Depois que um usuário é identificado, seus tokens anônimos tornam-se inválidos. No entanto, um usuário ainda será capaz de acessar seus atributos porque eles são acessíveis com o novo token.

**Observação**: uma identidade poderá ser atribuída a um registro anônimo somente se ele ainda não tiver sido atribuído a outro usuário. Se a identidade já está associada a outro usuário do {{site.data.keyword.appid_short_notm}}, os tokens contêm informações desse registro do usuário e fornecem acesso aos seus atributos. Os atributos de usuários anônimos anteriores não são acessíveis por meio do novo token. Até o token expirar, as informações ainda poderão ser acessadas através do token de acesso anônimo. Durante o desenvolvimento, é possível escolher como mesclar os atributos anônimos para o usuário conhecido.
