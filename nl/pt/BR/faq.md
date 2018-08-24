---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}


# Perguntas mais frequentes

Esta Pergunta mais frequente fornece respostas às perguntas comuns sobre o serviço {{site.data.keyword.appid_full}}.
{: shortdesc}


## Como o {{site.data.keyword.appid_short_notm}} calcula os preços?
{: #pricing}

Com o {{site.data.keyword.appid_short_notm}}, você paga menos à medida que usa mais recursos.
{: shortdesc}

O plano de camada graduado consiste em duas partes: o número de eventos de autenticação e o número de usuários autorizados. Você é cobrado a cada mês, com base no resumo das duas partes. O preço total é o encargo acumulativo para cada nível de uso, consistindo em sua quantidade multiplicada pelo preço unitário na respectiva camada.

### Eventos de autenticação

Um evento de autenticação ocorre quando um novo token de acesso, regular ou anônimo, é emitido. Para usuários identificados,
cada novo token de acesso é válido por padrão por uma hora (seja por meio de autenticação de usuário real ou por meio de tokens de
atualização). Por padrão. os tokens anônimos são válidos por um mês. Após o token expirar, deve-se criar um novo token para acessar recursos protegidos. 
É possível atualizar o tempo de expiração dos tokens do {{site.data.keyword.appid_short_notm}} na página
**Expiração de conexão** no painel do {{site.data.keyword.appid_short_notm}}.

Ao usar o {{site.data.keyword.appid_short_notm}} em aplicativos móveis, os tokens são armazenados no
armazenamento de chaves ou na keychain e são incluídos em cada solicitação futura. Os tokens são acessíveis usando o SDK do iOS ou
do Android do ID do app. Ao usar o {{site.data.keyword.appid_short_notm}} em aplicativos da web, é recomendado
armazenar os tokens em cookies de sessão de aplicativo.


### Usuários autorizados

Um usuário autorizado é um usuário exclusivo que efetua login com seu serviço, direta ou indiretamente. Você é cobrado por um usuário autorizado toda vez que um novo usuário efetua login de cada provedor de identidade, incluindo usuários anônimos. Por exemplo, se um usuário efetuar login com o Facebook e depois efetuar login usando o Google, ele será considerado como dois usuários autorizados separados.

Para obter mais informações sobre precificação de camada graduada, veja os [docs de precificação do {{site.data.keyword.Bluemix_notm}}](/docs/billing-usage/how_charged.html#services).

</br>


## Como a criptografia funciona no  {{site.data.keyword.appid_short_notm}}?
{: #encryption}

Verifique a tabela a seguir para obter respostas para as perguntas mais comuns sobre a criptografia.

<table>
  <thead>
    <th colspan=2><img src="images/idea.png" alt="Ícone de Mais informações"/>  </th>
  </thead>
  <tbody>
    <tr>
      <td>Por que você usa criptografia?</td>
      <td>O serviço criptografa os dados do cliente em repouso.</td>
    </tr>
    <tr>
      <td>Você construiu seus próprios algoritmos? Quais são os que você usa em seu código?</td>
      <td>Nós não construímos os nossos; o serviço usa o <code>AES</code> e o <code>SHA-256</code> com salting.</td>
    </tr>
    <tr>
      <td>Você usa módulos ou provedores de criptografia de origem pública ou de software livre? Você já expõe funções de criptografia? </td>
      <td>O serviço usa as bibliotecas Java <code>javax.crypto</code>, mas nunca expõe as funções de criptografia.</td>
    </tr>
    <tr>
      <td>Como você armazena as chaves?</td>
      <td>As chaves são geradas e, em seguida, armazenadas localmente depois de criptografadas por meio do uso de uma chave mestra
específica para cada região. As chaves mestras são armazenadas no  {{site.data.keyword.keymanagementserviceshort}}.</td>
    </tr>
    <tr>
      <td>Qual é a segurança da chave que você usa?</td>
      <td>O serviço usa 16 bytes.</td>
    </tr>
    <tr>
      <td>Você chama quaisquer APIs remotas que expõem os recursos de criptografia?</td>
      <td>Não, não temos.</td>
    </tr>
  </tbody>
</table>

</br>

## Como o {{site.data.keyword.appid_short_notm}} espera que uma asserção SAML se pareça?
{: #saml-example}

O serviço espera que uma asserção SAML se pareça ao exemplo a seguir.

```
<samlp:Response xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol" ID="s2202bbbbafa9d270d1c15990b738f4ab36139d463" InResponseTo="_e4a78780-35da-012e-8ea7-0050569200d8" Version="2.0" IssueInstant="2011-03-21T11:22:02Z" Destination="https://example.example.com/">
  <saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">idp_entityId</saml:Issuer>
  <samlp:Status xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <samlp:StatusCode  xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol"Value="urn:oasis:names:tc:SAML:2.0:status:Success"/>
  </samlp:Status>
  <saml:Assertion xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="2.0" ID="pfx539c9774-de5c-5f52-0c3f-b1c2e2697a89" IssueInstant="2018-01-29T13:02:58Z" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <saml:Issuer>idp_entityId</saml:Issuer>
    <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      <ds:SignedInfo>
        <ds:CanonicalizationMethod Algorithm="one_of_supported_algo"/>
        <ds:SignatureMethod Algorithm="one_of_supported_algo"/>
        <ds:Reference URI="#pfx539c9774-de5c-5f52-0c3f-b1c2e2697a89">
          <ds:Transforms>
            <ds:Transform Algorithm="one_of_supported_algo"/>
            <ds:Transform Algorithm="one_of_supported_algo"/>
          </ds:Transforms>
          <ds:DigestMethod Algorithm="one_of_supported_algo"/>
          <ds:DigestValue>huywDPPfOEGyyzE7d5hjOG97p7FDdGrjoSfes6RB19g=</ds:DigestValue>
        </ds:Reference>
      </ds:SignedInfo>
 <ds:SignatureValue>BAwNZFgWF2oxD1ux0WPfeHnzL+IWYqGhkM9DD28nI9v8XtPN8tqmIb5y4bomaYknmNpWYn7TgNO2Rn/XOq+N9fTZXO2RybaC49iF+zWibRIcNwFKCCpDL6H6jA5eqJX2YKBR+K6Yt2JPoUIRLmqdgm2lMr4Nwq1KYcSzQ/yoV5W0SN/V5t8EfctFoaXVPdtfHVXkwqHeufo+L4gobFt9NRTzXB0SQEClA1L8hQ+/LhY4l46k1D0c34iWjVLZr+ecQyubf7rekOG/R7DjWCFMTke822dR+eJTPWFsHGSPWCDDHFYqB4QMinTvUnsngjY3AssPqIOjeUxjL3p+GXn8IQ==</ds:SignatureValue>
    </ds:Signature>
    <saml:Subject>
      <saml:NameID Format="urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress">JohnDoe@gmail.com</saml:NameID>
    </saml:Subject>
    <saml:Conditions NotBefore="2018-01-29T12:59:58Z" NotOnOrAfter="2018-01-29T13:05:58Z">
    </saml:Conditions>
</samlp:Response>
```
{: screen}

</br>

## Quais tipos de algoritmos são suportados para assinaturas SAML?
{: #saml-signatures}

É possível usar qualquer um dos algoritmos a seguir para processar assinaturas digitais XML.

<table>
  <tr>
    <th> Tipo de algoritmo </th>
    <th> Opções de algoritmo </th>
  </tr>
  <tr>
    <td>Algoritmos de canonicalização e transformação com e sem comentários</td>
    <td><ul><li><a href="http://www.w3.org/TR/2001/REC-xml-c14n-20010315" target="_blank">Canonicalização <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></li>
    <li><a href="http://www.w3.org/2001/10/xml-exc-c14n#" target="_blank">Canonicalização exclusiva com e sem comentários <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></li>
    <li><a href=" http://www.w3.org/2000/09/xmldsig#enveloped-signature" target="_blank">Transformação de assinatura envelopada <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></li></ul></td>
  </tr>
  <tr>
    <td>Algoritmos hash</td>
    <td><ul><li><a href="http://www.w3.org/2000/09/xmldsig#sha1" target="_blank">Compilações SHA1 <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmlenc#sha256" target="_blank">Compilações SHA256 <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmlenc#sha512" target="_blank">Compilações SHA512 <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></li></ul></td>
  </tr>
  <tr>
    <td>Algoritmos de assinatura</td>
    <td><ul><li><a href="http://www.w3.org/2000/09/xmldsig#rsa-sha1" target="_blank">RSA-SHA1 <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmldsig-more#rsa-sha256" target="_blank">RSA-SHA256 <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmldsig-more#rsa-sha512" target="_blank">RSA-SHA512 <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></li>
    <li><a href="http://www.w3.org/2000/09/xmldsig#hmac-sha1" target="_blank">HMAC-SHA1 <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></li></ul></td>
  </tr>
</table>

Para obter mais informações sobre como usar um provedor de identidade SAML, veja [Configurando provedores de identidade corporativa](enterprise.html).
