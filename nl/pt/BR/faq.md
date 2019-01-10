---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:faq: data-hd-content-type='faq'}


# Perguntas mais frequentes
{: #faq}

Esta Pergunta mais frequente fornece respostas às perguntas comuns sobre o serviço {{site.data.keyword.appid_full}}.
{: shortdesc}


## Como o {{site.data.keyword.appid_short_notm}} calcula os preços?
{: #pricing}
{: faq}

Com o {{site.data.keyword.appid_short_notm}}, você paga menos à medida que usa mais recursos.
{: shortdesc}

O plano de camada graduada consiste em três partes: o número de eventos de autenticação, a segurança regular e avançada e o número de usuários autorizados. Você é cobrado a cada mês, com base no resumo das duas partes. O preço total é o encargo acumulativo para cada nível de uso, consistindo em sua quantidade multiplicada pelo preço unitário na respectiva camada.

Seus primeiros 1000 eventos de autenticação e os primeiros 1000 usuários autorizados são grátis a cada mês, com
exceção de quaisquer eventos de segurança avançados. Quaisquer eventos de segurança avançados incorrem em encargos
extras.

### Eventos de autenticação

Um evento de autenticação ocorre quando um novo token de acesso, regular ou anônimo, é emitido. Os tokens podem ser
emitidos como uma resposta a uma solicitação de conexão que é iniciada por um usuário ou em nome do usuário por um
aplicativo. Por padrão, os tokens de acesso são válidos por uma hora e os tokens anônimos são válidos por 30 dias. Após o token expirar, deve-se criar um novo token para acessar recursos protegidos. É
possível atualizar o prazo de expiração dos tokens do {{site.data.keyword.appid_short_notm}} na página
**Expiração de conexão** do painel de serviço.

#### Recursos de segurança avançados

Os recursos de segurança avançados fornecem a capacidade de fortalecer a segurança de seu aplicativo.
{: shortdesc}

<table>
  <tr>
    <th>Recurso</th>
    <th>Benefício</th>
  </tr>
  <tr>
    <td>Autenticação de Diversos Fatores</td>
    <td>A [MFA para Cloud Directory](mfa.html) confirma a identidade de um usuário ao exigir que ele insira uma
senha descartável que é enviada para seu e-mail, além de inserir seu e-mail e senha.</td>
  </tr>
  <tr>
    <td>Gerenciamento de política de senha</td>
    <td>Como proprietário da conta, é possível impor senhas mais seguras para o Cloud Directory configurando um
conjunto de regras às quais as senhas do usuário devem estar em conformidade. Exemplos incluem o número de tentativas de conexão
antes do bloqueio de acesso, prazos de expiração, amplitude de tempo mínimo entre as atualizações de senha ou o
número de vezes que uma senha não pode ser repetida. Para obter uma lista completa das opções e configurar as informações, consulte
[Gerenciamento de senha avançada](cloud-directory.html#advanced-password).</td>
  </tr>
</table>

Por padrão, os recursos de segurança avançados são desativados. Se você ativar o gerenciamento de política de
senha ou a autenticação de diversos fatores, você incorrerá em um encargo extra. Se você desativar todos os recursos avançados,
sua conta será revertida para a política de custo mais baixo. Por exemplo, se você obteve 10.000 tokens de acesso. Em
seguida, ativou a MFA e o gerenciamento de política de senha e obteve mais 10.000. Você pagaria por 20.000 eventos de
autenticação e 10.000 eventos de segurança avançados.

Esses recursos estão disponíveis apenas para as instâncias que estão no plano de precificação de camada graduada e que
foram criadas após 15 de março de 2018.
{: note}

### Usuários autorizados

Um usuário autorizado é um usuário exclusivo que se conecta com o seu serviço, direta ou indiretamente, incluindo
usuários anônimos. Você é cobrado por um usuário autorizado cada vez que um novo usuário se conecta a seu aplicativo,
incluindo usuários anônimos. Por exemplo, se um usuário se conectar com o Facebook e, posteriormente, se conectar usando o
Google, ele será considerado como dois usuários autorizados separados.

Para obter as informações de precificação mais atualizadas do {{site.data.keyword.appid_short_notm}}, consulte a
[calculadora
de precificação](https://console.cloud.ibm.com/pricing/configure/service/AdvancedMobileAccess-d6aece47-d840-45b0-8ab9-ad15354deeea).
{: important}

</br>


## Por que preciso inserir a minha URL de redirecionamento na lista de desbloqueio?
{: #redirect}
{: faq}

Uma URL de redirecionamento é o terminal de retorno de chamada de seu app. Para evitar ataques de phishing, o {{site.data.keyword.appid_short_notm}} valida a URL com relação à lista de desbloqueio de URLs de
redirecionamento. Quando ocorre phishing, existe a possibilidade de um invasor poder obter acesso aos tokens de usuário.

Para incluir sua URL na lista de desbloqueio:

1. Navegue para **Provedores > Gerenciar**.
2. No campo **Incluir URL de redirecionamento da web**, digite a URL e clique em **+**.

Não inclua quaisquer parâmetros de consulta em sua URL. Eles são ignorados no processo de validação. URL de exemplo: `http://host:[port]/path`
{: tip}

</br>

## Como a criptografia funciona no  {{site.data.keyword.appid_short_notm}}?
{: #encryption}
{: faq}

Verifique a tabela a seguir para obter respostas para as perguntas mais comuns sobre a criptografia.

<table>
  <thead>
    <th colspan=2><img src="images/idea.png" alt="Ícone de Mais informações"/>  </th>
  </thead>
  <tbody>
    <tr>
      <td>Por que você usa criptografia?</td>
      <td>Uma maneira de proteger as informações de nossos usuários é criptografar os dados do cliente em repouso. O serviço
criptografa os dados do cliente em repouso com as chaves por locatário.</td>
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
      <td>As chaves são geradas e criptografadas com uma chave mestra que é específica para cada região e, em seguida, armazenadas
localmente. As chaves mestras são armazenadas no  {{site.data.keyword.keymanagementserviceshort}}. Nos níveis de
armazenamento e de middleware, há criptografia de nível de serviço, o que significa que há uma chave para todos os
clientes. No nível do aplicativo, cada cliente tem sua própria chave de criptografia.</td>
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
{: faq}

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
{: faq}

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
