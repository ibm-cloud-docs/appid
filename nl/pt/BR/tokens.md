---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-10"

keywords: authentication, authorization, identity, app security, secure, tokens, jwt, development

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


# Validando tokens
{: #token-validation}

A validação de token é uma parte importante do desenvolvimento de aplicativo moderno. Ao validar os tokens, é possível
proteger seu aplicativo ou APIs de usuários não autorizados. O {{site.data.keyword.appid_full}} usa os tokens de acesso e de identidade para assegurar que um usuário ou aplicativo seja autenticado antes de ter acesso concedido. Se você
estiver usando um dos SDKs fornecidos pelo {{site.data.keyword.appid_short_notm}}, a obtenção e a validação de
seus tokens serão feitas para você.
{: shortdesc}

Para obter mais informações sobre como os tokens são usados no {{site.data.keyword.appid_short_notm}}, consulte [Entendendo os tokens](/docs/services/appid?topic=appid-tokens#tokens).
{: tip}

Os tokens são usados para verificar se uma pessoa é quem diz ser. Eles confirmam quaisquer permissões de acesso que o
usuário pode manter por um período de tempo especificado. Quando um usuário se conectar ao seu aplicativo e receber um
token, seu aplicativo deverá validar o usuário antes que ele receba acesso.

</br>

**E se eu estiver trabalhando em um idioma para o qual o {{site.data.keyword.appid_short_notm}} não
tiver um SDK?**

Não se preocupe! Você tem três opções:

* Trabalhe com as APIs do {{site.data.keyword.appid_short_notm}}
* Implemente sua própria lógica de validação
* Usar qualquer SDK de software livre compatível com OIDC

Com base em feedback, a opção 1 normalmente é a maneira mais fácil.
{: tip}

</br>
</br>

## Usando as APIs do {{site.data.keyword.appid_short_notm}}
{: #remote-validation}

Usando a introspecção, é possível usar o {{site.data.keyword.appid_short_notm}} para validar seus tokens.
{: shortdesc}

1. Envie uma solicitação de POST para o terminal da API [/introspect](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Authorization%20Server%20-%20Authorization%20Server%20V4/oauth-server.token)
para validar seu token. A solicitação deve fornecer o token e um cabeçalho de autorização básico que contém o
identificador de cliente e o segredo.

  Solicitação de exemplo:

    ```
    POST /oauth/v4/{tenant_id}/introspect HTTP/1.1
    Host: us-south.appid.cloud.ibm.com
    Content-Type: application/x-www-form-urlencoded
    Authorization: Basic jdFlUaGlZUzAwTW0Tjk15TmpFMw==
    Cache-Control: no-cache

    token=XXXXX.YYYYY.ZZZZZ
    ```
    {: screen}

2. O servidor verifica a expiração e a assinatura do token e retorna um objeto JSON que informa se o token está ativo ou
inativo.

  Resposta de exemplo:

    ```
    {
      "active": true
    }
    ```
    {: screen}


## Validando tokens manualmente
{: #local-validation}

É possível validar seus tokens localmente analisando o token, verificando a assinatura do token e validando as
solicitações que estão armazenadas no token.
{: shortdesc}


1. Analisar os tokens. O [JSON Web Token (JWT)](https://tools.ietf.org/html/rfc7519) é uma maneira padrão
de passar informações com segurança. Ele consiste em três partes principais: cabeçalho, carga útil e assinatura. Elas
são codificadas em Base64URL e separadas por um ponto (.). É possível usar qualquer decodificador de Base64URL disponível
para analisar o token. Como alternativa, é possível usar qualquer uma das [bibliotecas que estão listadas](https://jwt.io/#libraries-io) para analisar o token.

  Token codificado de exemplo:

    ```
    eyJhbGciOiJSUzI1NiIsInR5cCI6IkpPU0UiLCJraWQiOiJhMmszIn0
    .eyJpc3MiOiJhcHBpZC1vYXV0aCIsImF1ZCI6ImFiYzEyMyIsImV4cCI6MTU2NDU2Nn0
    .IycnAGUmMHzpTWbe-qaRsx0B4Zi-SVav710Fb_8CTCQvLrHX9d42WuCZ5bW
    d-ikgEsf6waQxeBfhfwYxwHN87LZupApagVMZtylVAnXhG1pHu_32wbZsPvg6QjzNO
    j6ys2Lfl3qfb5Qrp9u4IsZltKPEN8HdfeOcKXxpw6UqP-8
    ```
    {: screen}

  Exemplo de cabeçalho decodificado:

    ```
    {
      "alg": "RS256",
      "typ": "JOSE",
      "kid": "a2k3"
    }
    ```
    {: screen}

  Carga útil decodificada:

    ```
    {
      "iss": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61",
      "aud": "abc123",
      "exp": 1564566
    }
    ```
    {: screen}

2. Faça uma chamada para o [terminal /publickeys](https://us-south.appid.cloud.ibm.com/swagger-ui/#!/Authorization_Server_V4/publicKeys) para recuperar suas chaves públicas. As chaves públicas que são retornadas são formatadas como [JSON Web Keys (JWK)](https://tools.ietf.org/html/rfc7517).

  Solicitação de exemplo:

    ```
    GET /oauth/v4/{tenant_id}/publickeys HTTP/1.1
    Host: us-south.appid.cloud.ibm.com
    Cache-Control: no-cache
    ```
    {: screen}

3. Armazene as chaves em seu cache do aplicativo para uso futuro. O armazenamento das chaves acelerará o processo e evitará
o atraso da rede se outra chamada for feita.

4. Importe os parâmetros de chave pública.

  Resposta de exemplo:

    ```
    {
      "keys": [
        {
          "kty": "RSA",
          "use": "sig",
          "n": "AsdaE",
          "e": "SDAasw",
          "kid": "ad123dCAz"
        }
      ]
    }
    ```
    {: screen}

  <table>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="Ícone de mais informações"/> Parâmetros de chave pública </th>
    </thead>
    <tbody>
      <tr>
        <td><code>kty</code></td>
        <td>Define o algoritmo usado.</td>
      </tr>
      <tr>
        <td><code>use</code></td>
        <td>Define o propósito da chave.</td>
      </tr>
      <tr>
        <td><code>kid</code></td>
        <td>Define o ID exclusivo da chave.</td>
      </tr>
      <tr>
        <td>Outro</td>
        <td>Pode haver outros parâmetros restantes que sejam específicos para seu algoritmo que também devem ser importados.</td>
      </tr>
    </tbody>
  </table>

5. Verifique a assinatura do token. O cabeçalho do token contém o algoritmo que foi usado para assinar o token e o ID da
chave ou a solicitação `kid` da chave pública correspondente. Como as chaves públicas não são
mudadas frequentemente, é possível armazenar em cache as chaves públicas em seu aplicativo e, ocasionalmente,
atualizá-las. Se a chave armazenada em cache estiver ausente da solicitação `kid`, será possível validar os tokens localmente.

  1. Faça com que seu aplicativo verifique se o conteúdo do cabeçalho do token recebido corresponde aos parâmetros da chave
pública.
  2. Verifique especificamente se os mesmos algoritmos foram usados e se seu cache de chave pública contém uma chave com o ID
de chave relevante.
  3. Assegure-se de que o valor do hash seja o mesmo que a assinatura do formato PEM da chave pública. Seu valor do hash pode
ser obtido combinando e realizando hashing do cabeçalho da carga útil do token. Como esse processo pode ser complexo para
implementar manualmente, pode ser útil usar uma das [bibliotecas listadas](https://jwt.io/) para
validar a assinatura.

6. Valide as solicitações que estão armazenadas nos tokens. Para conferir verificações futuras, é possível usar
[essa lista](http://openid.net/specs/openid-connect-core-1_0.html#IDTokenValidation).
  <table>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="Ícone de mais informações"/> Solicitações que devem ser validadas </th>
    </thead>
    <tbody>
      <tr>
        <td><code> iss </code></td>
        <td>O emissor deve ser o mesmo do servidor OAuth do {{site.data.keyword.appid_short_notm}}.</td>
      </tr>
      <tr>
        <td><code> exp </code></td>
        <td>O horário atual deve ser menor que o tempo de validade.</td>
      </tr>
      <tr>
        <td><code> aud </code></td>
        <td>O público deve conter o identificador de cliente de seu aplicativo.</td>
      </tr>
      <tr>
        <td><code> tenant </code></td>
        <td>O locatário deve conter o ID do locatário de seu aplicativo.</td>
      </tr>
      <tr>
        <td><code>scope</code></td>
        <td>O escopo de permissões que são concedidas para o usuário. Isso é específico para o token de acesso.</td>
      </tr>
    </tbody>
  </table>
