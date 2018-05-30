---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

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

Um evento de autenticação ocorre quando um novo token do {{site.data.keyword.appid_short_notm}} é emitido. Para usuários identificados, cada novo token é válido por 1 hora. Os tokens anônimos são válidos por 1 mês. Após o token expirar, deve-se criar um novo token para acessar recursos protegidos. Quando você usa o {{site.data.keyword.appid_short_notm}} para autenticação móvel, os tokens do usuário são armazenados em `key-store/key-chain` e são incluídos em cada solicitação futura. Os tokens são acessíveis usando o SDK Swift Android ou iOS do {{site.data.keyword.appid_short_notm}}. Ao usar o serviço para autenticação da web, <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">armazene o token do usuário <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> nos cookies de sessão.

### Usuários autorizados

Um usuário autorizado é um usuário exclusivo que efetua login com seu serviço, direta ou indiretamente. Você é cobrado por um usuário autorizado toda vez que um novo usuário efetua login de cada provedor de identidade, incluindo usuários anônimos. Por exemplo, se um usuário efetuar login com o Facebook e depois efetuar login usando o Google, ele será considerado como dois usuários autorizados separados.

Para obter mais informações sobre precificação de camada graduada, veja os [docs de precificação do {{site.data.keyword.Bluemix_notm}}](/docs/billing-usage/how_charged.html#services).

</br>

## Que tipo de atividade é monitorada pelo {{site.data.keyword.appid_short_notm}}?
{: #activity-monitor}

É possível rastrear a atividade que foi gerada no app que está ligado à instância de serviço. Também é possível monitorar a atividade administrativa que é feita no {{site.data.keyword.appid_short_notm}} usando o serviço {{site.data.keyword.cloudaccesstrailshort}}.

Para visualizar a atividade que é gerada por seu app:

1. Efetue login em sua conta do {{site.data.keyword.Bluemix_notm}}.
2. No painel, selecione sua instância do {{site.data.keyword.appid_short_notm}}.
3. Clique na guia **Visão geral**.
4. Visualize a atividade que está listada no **Log de atividades**.

</br>
Para monitorar a atividade administrativa:

1. Efetue login em sua conta do {{site.data.keyword.Bluemix_notm}}. Navegue para a organização e o espaço nos quais sua instância do {{site.data.keyword.appid_short_notm}} é provisionada.
2. No catálogo, provisione uma instância do serviço {{site.data.keyword.cloudaccesstrailshort}}. Certifique-se de que você esteja no mesmo espaço que sua instância do {{site.data.keyword.appid_short_notm}}.
3. No painel {{site.data.keyword.cloudaccesstrailshort}}, clique na guia **Gerenciar**.
4. Na lista suspensa, selecione as configurações a seguir para procurar eventos que foram gerados pelo {{site.data.keyword.appid_short_notm}}.
<table>
  <tr>
    <th> Campo </th>
    <th> Configuração </th>
  </tr>
  <tr>
    <td>Visualizar Logs</td>
    <td>Logs de espaço</td>
  </tr>
  <tr>
    <td>Procurar</td>
    <td>target.name</td>
  </tr>
  <tr>
    <td>Filtro</td>
    <td>appid</td>
  </tr>
</table>
5. Clique em **Filtrar**.

Veja os [docs do {{site.data.keyword.cloudaccesstrailshort}}](/docs/services/cloud-activity-tracker/index.html) para obter mais informações sobre como o serviço funciona.

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
