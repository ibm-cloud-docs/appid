---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

keywords: authentication, authorization, identity, app security, secure, custom, service provider, identity provider, enterprise, assertions

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

# SAML
{: #enterprise}

Security Assertion Markup Language (SAML) é um padrão aberto para troca de dados de autenticação e de autorização entre
um provedor de identidade que afirma a identidade do usuário e um provedor de serviços que consome as informações de
identidade do usuário.
{: shortdesc}

{{site.data.keyword.appid_short_notm}}funciona como um provedor de serviços e inicia um login de conexão única (SSO) para um provedor de terceiro, como o Active Directory Federation Services. O protocolo <a href="http://saml.xml.org/saml-specifications" target="blank">SAML <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> suporta diferentes perfis e opções de ligação. O {{site.data.keyword.appid_short_notm}} suporta o perfil SSO do navegador da web com a ligação de Post HTTP.

Para obter as etapas sobre como usar um provedor de identidade SAML específico, consulte essas postagens de
blog sobre a configuração do {{site.data.keyword.appid_short_notm}} com o [Ping One
![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-ping-one/),
[um Azure Active Directory
![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-azure-active-directory/) ou
[um Active Directory Federation Service ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-active-directory-federation-service/).
{: tip}



## Entendendo as asserções
{: #saml-assertions}

Uma asserção SAML é semelhante a um [atributo do usuário](/docs/services/appid?topic=appid-user-profile#user-profile). É uma instrução ou parte de informações sobre um usuário que é retornado para o {{site.data.keyword.appid_short_notm}} por um provedor de identidade quando um usuário efetua login com êxito em seu app. Dependendo da configuração do aplicativo e do provedor de identidade que você usa, as informações podem incluir um nome de usuário, e-mail ou outro campo que pode ser especificado.
{: shortdesc}

Quando as asserções são retornadas para o {{site.data.keyword.appid_short_notm}}, o serviço federa a identidade do usuário. Se a asserção SAML corresponder a uma das solicitações OIDC a seguir, ela será incluída automaticamente no token de identidade.  Se um ou mais desses valores mudarem no lado do provedor, os novos valores estarão disponíveis apenas após o usuário efetuar login novamente.

 * `nome`
 * `E-mail
`
 * `locale`
 * `picture`

As asserções que não correspondem a nenhum dos nomes padrão são ignoradas por padrão, mas se o provedor SAML retornar outras asserções, será possível obter as informações quando um usuário efetuar login. Ao criar uma matriz das asserções que você deseja usar, é possível [injetar as informações em seus tokens](/docs/services/appid?topic=appid-customizing-tokens#customizing-tokens). Mas certifique-se de não incluir mais informações do que o necessário em seus tokens. Os tokens são geralmente enviados em cabeçalhos HTTP e cabeçalhos têm limite de tamanho.
{: tip}

### Como o {{site.data.keyword.appid_short_notm}} espera que uma asserção SAML se pareça?
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


### Quais tipos de algoritmos são suportados pelo {{site.data.keyword.appid_short_notm}}?
{: #saml-signatures}

O {{site.data.keyword.appid_short_notm}} usa o algoritmo <a href="http://www.w3.org/2001/04/xmldsig-more#rsa-sha256" target="_blank">RSA-SHA256 <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> para processar assinaturas digitais XML.




## Fornecendo metadados para seu provedor de identidade
{: #saml-provide-idp}

Para configurar seu app, você precisa fornecer informações para um provedor de identidade compatível com SAML. As informações são trocadas por meio de um arquivo XML de metadados que também contém dados de configuração que são usados para estabelecer confiança.
{: shortdesc}

Não é possível ativar o SAML até depois de configurá-lo como um provedor de identidade.
{: tip}

1. Na guia **Gerenciar** do painel do {{site.data.keyword.appid_short_notm}}, clique em **Editar** na linha **SAML** para definir as suas configurações.
2. Clique em **Fazer download do arquivo de metadados do SAML**. Seu provedor de identidade espera as informações a seguir do arquivo.
  <table>
    <tr>
      <th> Variável </th>
      <th> Descrição </th>
    </tr>
    <tr>
      <td><code>EntityID</code></td>
      <td>O identificador que permite que o provedor de identidade saiba que o {{site.data.keyword.appid_short_notm}} emitiu a solicitação SAML.</td>
    </tr>
    <tr>
      <td><code>Location URL</code></td>
      <td>O local para o qual o provedor de identidade envia as asserções SAML após autenticar com êxito um usuário.</td>
    </tr>
    <tr>
      <td><code>Binding</code></td>
      <td>As instruções sobre como o provedor de identidade deve enviar a resposta SAML.</td>
    </tr>
    <tr>
      <td><code>NameID Format</code></td>
      <td>A maneira na qual o provedor de identidade sabe qual formato de identificador ele precisa enviar no assunto de uma asserção. A maneira na qual o {{site.data.keyword.appid_short_notm}} identifica usuários.</td>
    </tr>
    <tr>
      <td><code>WantAssertionsSigned</code></td>
      <td>A maneira na qual um provedor de identidade verifica se ele precisa assinar a asserção. O serviço espera que a asserção seja assinada, mas não suporta asserções criptografadas.</td>
    </tr>
  </table>

3. Forneça os dados para seu provedor de identidade. Se seu provedor de identidade suporta upload do arquivo de metadados, é possível fazer isso. Se não, configure as propriedades manualmente. Nem todo provedor de identidade usa as mesmas propriedades, portanto, você pode não usar todas elas.

  Os nomes da propriedade podem diferir entre os provedores de identidade.
  {: tip}

4. Alterne **Federação SAML 2.0** para **Ativado**.

## Fornecendo metadados para o {{site.data.keyword.appid_short_notm}}
{: #saml-provide-appid}

É possível obter dados de seu provedor de identidade e fornecê-los para o {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

### Fornecendo metadados com a GUI
{: #saml-provide-gui}

1. Navegue para a guia **SAML 2.0** do painel {{site.data.keyword.appid_short_notm}}. Insira os metadados a seguir obtidos a partir do provedor de identidade na seção **Fornecer Metadados da SAML IdP**.
  <table>
    <tr>
      <th> Variável </th>
      <th> Descrição </th>
    </tr>
    <tr>
      <td><code>Sign-in URL</code></td>
      <td>A URL para a qual o usuário é redirecionado para autenticação. Ela é hospedada por seu provedor de identidade SAML.</td>
    </tr>
    <tr>
      <td><code>Entity ID</code></td>
      <td>O nome globalmente exclusivo para um provedor de identidade SAML.</td>
    </tr>
    <tr>
      <td><code>Signing certificate</code></td>
      <td>O certificado emitido por seu provedor de identidade SAML. Ele é usado para assinar e validar asserções SAML. Todos os provedores são diferentes, mas você pode ser capaz de fazer download do certificado de assinatura do seu provedor de identidade. O certificado deve estar no formato <code>.pem</code>.</td>
    </tr>
  </table>

2. Opcional: forneça um **Certificado secundário** que é usado se a validação da assinatura falha no certificado primário. Se a chave de assinatura permanece a mesma, o {{site.data.keyword.appid_short_notm}} não bloqueia a autenticação para certificados expirados.
3. Atualize o **Nome do provedor** e clique em **Salvar**. O nome padrão é SAML.

Deseja configurar um contexto de autenticação? É possível fazer isso por meio da API.
{: tip}


### Fornecendo Metadados com a API
{: #saml-provide-api}

1. Obtenha seus metadados SAML fazendo uma solicitação GET para o terminal da API [/getSamlMetadata](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.get_saml_idp).

  Código de exemplo:
  ```
  <?xml version="1.0"?>
  <getSamlMetadata>
    <?xml version="1.0"?> <EntityDescriptor> <SPSSODescriptor> <NameIDFormat> </NameIDFormat> <AssertionConsumerService /> </SPSSODescriptor>
   </EntityDescriptor>
    </getSamlMetadata>
  ```
  {: codeblock}

  Saída de exemplo:
  ```
    {
    "isActive": true, "config": {
      "entityID": "https://example.com/saml2/metadata/706634", "signInUrl": "https://example.com/saml2/sso-redirect/706634", "certificates": [
        "certificate-example-pem-format"
      ],
      "displayName": "my saml example",
      "authnContext": {
        "class": [
          "urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport"
        ],
        "comparison": "exact"
      }
    },
    "validation_data": {
      "certificates": [
        {
          "certificate_index": 0,
          "expiration_timestamp": 1674473996,
          "warning": "Your certificate will expire in 18 days."
        }
      ]
    }
  }
  ```
  {: screen}

2. Configure sua solicitação de POST para o
terminal da API [/set_saml_idp](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp).

  1. No exemplo de metadados a seguir, substitua as variáveis por suas próprias informações.

    ```
    Put {Management URI}/config/idps/saml Content-Type: application/json {
      "isActive": true, "config": {
        "entityID": "https://example.com/saml2/metadata/706634", "signInUrl": "https://example.com/saml2/sso-redirect/706634", "certificates": [
          "primary-certificate-example-pem-format"
        ], "displayName": "meu exemplo de saml" }
    }
    ```
    {: codeblock}

    <table>
      <tr>
        <th> Variável </th>
        <th> Descrição </th>
      </tr>
      <tr>
        <td><code>Sign-in URL</code></td>
        <td>A URL para a qual o usuário é redirecionado para autenticação. Ela é hospedada por seu provedor de identidade SAML.</td>
      </tr>
      <tr>
        <td><code>Entity ID</code></td>
        <td>O nome globalmente exclusivo para um provedor de identidade SAML.</td>
      </tr>
      <tr>
        <td><code>Signing certificate</code></td>
        <td>O certificado emitido por seu provedor de identidade SAML. Ele é usado para assinar e validar asserções SAML. Todos os provedores são diferentes, mas você pode ser capaz de fazer download do certificado de assinatura do seu provedor de identidade. O certificado deve estar no formato <code>.pem</code>.</td>
      </tr>
    </table>

  2. Opcional: inclua um certificado secundário na matriz de certificados depois do certificado primário. O certificado
secundário será usado se a validação de assinatura falhar com o certificado primário. Se a chave de assinatura permanece a mesma, o {{site.data.keyword.appid_short_notm}} não bloqueia a autenticação para certificados expirados.

    Exemplo:
    ```
    {
      "isActive": true, "config": {
        ...
        "certificates": [
          "primary-certificate-example-pem-format",
          "secondary-certificate-example-pem-format"
        ],
        ...
      }
    }
    ```
    {: screen}
  {: #configuring-saml-new}
  3. Opcional: Inclua um contexto de autenticação incluindo uma matriz de classe e uma sequência de comparação em seu
código. Certifique-se de atualizar os parâmetros `class` e `comparison` com seus valores. Um
contexto de autenticação é usado para verificar a qualidade da autenticação e das asserções SAML.

    Exemplo:
    ```
    {
      "isActive": true, "config": {
        ...
        "authnContext": {
          "class": [
            "urn:oasis:names:tc:SAML:2.0:ac:classes:YourChosenClassValue", "urn:oasis:names:tc:SAML:2.0:ac:classes:YourOtherChosenClassValue"
          ],
          "comparison": "sampleComparisonValue"
        }
      }
    }
    ```
    {: screen}

3. Faça a solicitação. Se você optar por incluir os valores opcionais, sua solicitação deverá ser semelhante ao exemplo a
seguir.

  ```
  Put {Management URI}/config/idps/saml Content-Type: application/json {
    "isActive": true, "config": {
      ...
      "authnContext": {
        "class": [
          "urn:oasis:names:tc:SAML:2.0:ac:classes:YourChosenClassValue", "urn:oasis:names:tc:SAML:2.0:ac:classes:YourOtherChosenClassValue"
        ],
        "comparison": "sampleComparisonValue"
      "entityID": "https://example.com/saml2/metadata/706634",
      "signInUrl": "https://example.com/saml2/sso-redirect/706634",
      "certificates": [
        "primary-certificate-example-pem-format"
        "secondary-certificate-example-pem-format"
      ], "displayName": "meu exemplo de saml" }
  }
  ```
  {: codeblock}


## Testando sua configuração
{: #saml-testing}

É possível testar a configuração entre seu Provedor de Identidade SAML e o {{site.data.keyword.appid_short_notm}}.

1. Certifique-se de que você salvou sua configuração.
2. Navegue para a guia **SAML 2.0** do painel {{site.data.keyword.appid_short_notm}} e clique em **Testar**. Uma nova guia é aberta.
3. Efetue login com um usuário que seu provedor de identidade já tenha autenticado.
4. Depois de concluir o formulário, você é redirecionado para outra página.
  * Autenticação bem-sucedida: a conexão entre o {{site.data.keyword.appid_short_notm}} e o Provedor de Identidade está funcionando corretamente. A página exibe [tokens de acesso e de identidade](/docs/services/appid?topic=appid-tokens#tokens) válidos.
  * Autenticação com falha: a conexão está quebrada. A página exibe os erros e o arquivo XML de resposta SAML.


Tendo problemas? Consulte [Solucionando problemas de
configurações do provedor de identidade](/docs/services/appid?topic=appid-troubleshooting-idp#troubleshooting-idp)
{: tip}
