---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-20"

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

Quando você tiver um provedor de identidade baseado em SAML, será possível configurar o {{site.data.keyword.appid_short_notm}} para agir como um provedor de serviços que inicia um login de conexão única (SSO) com um provedor de terceiro. Durante o fluxo de conexão, seus usuários podem ser facilmente autenticados e podem obter tokens de segurança do {{site.data.keyword.appid_short_notm}} que permitem que eles acessem seus apps e APIs protegidas.
{: shortdesc}

 
Trabalhando com um provedor de identidade SAML específico? Verifique uma dessas postagens de blog na configuração do {{site.data.keyword.appid_short_notm}} com [Ping One ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/cloud/blog/setting-ibm-cloud-app-id-ping-one), [um Azure Active Directory ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/cloud/blog/setting-ibm-cloud-app-id-azure-active-directory) ou [um Active Directory Federation Service ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/cloud/blog/setting-ibm-cloud-app-id-active-directory-federation-service).
{: tip}


## Entendendo o SAML
{: #saml-understanding}

Security Assertion Markup Language (SAML) é um padrão aberto para troca de dados de autenticação e de autorização entre
um provedor de identidade que afirma a identidade do usuário e um provedor de serviços que consome as informações de
identidade do usuário.
{: shortdesc}

O protocolo <a href="http://saml.xml.org/saml-specifications" target="blank">SAML <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> suporta diferentes perfis e opções de ligação. O {{site.data.keyword.appid_short_notm}} suporta o perfil SSO do navegador da web com a ligação de Post HTTP.

### Qual é a base técnica de fluxos?
{: #saml-tech-basis}

O SAML 2.0 é uma das estruturas mais estabelecidas para padrões de autenticação e autorização. Ele é um protocolo baseado em XML entre um provedor de serviços ({{site.data.keyword.appid_short_notm}}) e um provedor de identidade. Quando um provedor de identidade autentica um usuário, ele cria tokens SAML, que contêm asserções ou instruções, sobre o usuário. As instruções podem conter:

- informações sobre autenticação, como o modo como o usuário foi autenticado - uma senha, MFA, etc. ...
- atributos associados ao usuário - a que grupo eles pertencem.
- decisões de autorização que declaram se o usuário tem permissão para executar uma ação específica em um recurso específico.

Quando as asserções são retornadas para o {{site.data.keyword.appid_short_notm}}, o serviço federa a identidade do usuário e os tokens apropriados são gerados. Se a asserção SAML corresponder a uma das solicitações OIDC a seguir, ela será incluída automaticamente no token de identidade.  Se um ou mais desses valores mudarem no lado do provedor, os novos valores estarão disponíveis apenas após o usuário efetuar login novamente.

 * `nome`
 * `E-mail
`
 * `locale`
 * `picture`

As asserções que não correspondem a nenhum dos nomes padrão são ignoradas por padrão, mas se o provedor SAML retornar outras asserções, será possível obter as informações quando um usuário efetuar login. Ao criar uma matriz das asserções que você deseja usar, é possível [injetar as informações em seus tokens](/docs/services/appid?topic=appid-customizing-tokens#customizing-tokens). Mas certifique-se de não incluir mais informações do que o necessário em seus tokens. Os tokens são geralmente enviados em cabeçalhos HTTP e cabeçalhos têm limite de tamanho.
{: tip}

### Qual é a aparência desse fluxo?
{: #saml-flow}

Embora o {{site.data.keyword.appid_short_notm}} e seu provedor de identidade usem a estrutura SAML para autenticar o usuário, o {{site.data.keyword.appid_short_notm}} ainda usa a estrutura OAuth 2.0/OIDC mais moderna para trocar tokens de segurança com o aplicativo. Verifique a imagem a seguir para ver um fluxo detalhado de informações.

![Fluxo de autenticação corporativa SAML](/images/ibmid-flow.png)

1. Um usuário acessa a página de login ou o recurso restrito em seu aplicativo, que inicia uma solicitação para o terminal `/authorization` do {{site.data.keyword.appid_short_notm}} por meio de um SDK ou de uma API do {{site.data.keyword.appid_short_notm}}. Se o usuário não estiver autorizado, o fluxo de autenticação começará com um redirecionamento para o {{site.data.keyword.appid_short_notm}}.
2. O {{site.data.keyword.appid_short_notm}} gera uma solicitação de autenticação SAML (AuthNRequest) e o navegador redireciona automaticamente o usuário para o provedor de identidade SAML.
3. O provedor de identidade analisa a solicitação SAML, autentica o usuário e gera uma resposta SAML com suas asserções.
4. O provedor de identidade redireciona o usuário e a resposta de volta para o {{site.data.keyword.appid_short_notm}} com a resposta SAML.
5. Se a autenticação for bem-sucedida, o {{site.data.keyword.appid_short_notm}} criará tokens de acesso e de identidade que representam a autorização e a autenticação de um usuário e os retornará para o app. Se a autenticação falhar, o {{site.data.keyword.appid_short_notm}} retornará o código de erro do provedor de identidade para o app.
6. O usuário tem acesso concedido ao app ou aos recursos protegidos.



### A SSO muda o fluxo?
{: #saml-sso-flow}

O perfil SSO do navegador da web implementado pelo {{site.data.keyword.appid_short_notm}} é o provedor de serviços iniciado, o que significa que o {{site.data.keyword.appid_short_notm}} deve enviar uma solicitação SAML para o provedor de identidade iniciar a sessão de autenticação. 

O {{site.data.keyword.appid_short_notm}} não suporta atualmente fluxos iniciados pelo provedor de identidade e eles não devem ser usados com o serviço neste momento.
{: note}

Se o seu provedor de identidade suportar SSO, será possível que a autenticação SAML use a sessão de SSO já estabelecida para autenticar o usuário. Caso contrário, o usuário será redirecionado para uma página de login. Eles poderão ser redirecionados se o seu provedor de identidade não puder corresponder aos requisitos de autenticação definidos na solicitação de autenticação do {{site.data.keyword.cloud_notm}}, usados para estabelecer a SSO. Por exemplo, se o seu provedor de identidade estabelecer uma sessão de SSO do usuário usando biometria, o contexto de autenticação padrão do {{site.data.keyword.appid_short_notm}} deverá ser mudado. Por padrão, o {{site.data.keyword.appid_short_notm}} espera que os usuários sejam autenticados por senha por meio de HTTPS: `urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport`.



## Configurando o SAML para trabalhar com o {{site.data.keyword.appid_short_notm}}
{: #saml-configure}

É possível configurar o SAML para trabalhar com o {{site.data.keyword.appid_short_notm}} fornecendo metadados do {{site.data.keyword.appid_short_notm}} para seu provedor de identidade e metadados de seu provedor de identidade para o {{site.data.keyword.appid_short_notm}}.



### Fornecendo metadados para seu provedor de identidade
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
      <td>A maneira pela qual o provedor de identidade sabe qual formato de identificador ele precisa enviar no assunto de uma asserção e como o {{site.data.keyword.appid_short_notm}} identifica usuários. O ID deve assumir o formato a seguir: <code><saml:NameID Format="urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress"/></code></td>
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



### Fornecendo metadados para o {{site.data.keyword.appid_short_notm}}
{: #saml-provide-appid}

É possível obter dados de seu provedor de identidade e fornecê-los para o {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

**Fornecendo metadados com a GUI** 

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

</br>

**Fornecendo metadados com a API**

1. Visualize sua configuração de SAML atual, incluindo seu contexto de autenticação e certificados, fazendo uma solicitação GET para o [terminal de API `/saml`](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.get_saml_idp).

  Código de exemplo:
  ```
  curl --request GET \
  https://us-south.appid.cloud.ibm.com/management/v4/<tenant-ID>/config/idps/saml \
  --header `Accept: application/json`
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
    }
  }
  ```
  {: screen}

2. Crie sua configuração SAML substituindo os valores no exemplo a seguir pelas informações de seu provedor. Os valores mostrados no exemplo são necessários, mas é possível optar por incluir mais informações, conforme mostrado na tabela.

  ```
  "config": {
    "authnContext": {
      "class": [
        "urn:oasis:names:tc:SAML:2.0:ac:classes:YourChosenClassValue", "urn:oasis:names:tc:SAML:2.0:ac:classes:YourOtherChosenClassValue"
      ],
      "comparison": "sampleComparisonValue"}
    "entityID": "https://example.com/saml2/metadata/706634",
    "signInUrl": "https://example.com/saml2/sso-redirect/706634",
    "certificates": [
      "primary-certificate-example-pem-format"
        "secondary-certificate-example-pem-format"
    ], "displayName": "my saml example", }
  ```
  {: codeblock}
  {: #configuring-saml-new}

  <table>
    <tr>
      <th> Variável </th>
      <th> Descrição </th>
    </tr>
    <tr>
      <td><code>signInUrl</code></td>
      <td>A URL para a qual o usuário é redirecionado para autenticação. Ela é hospedada por seu provedor de identidade SAML.</td>
    </tr>
    <tr>
      <td><code>entityID</code></td>
      <td>O nome globalmente exclusivo para um provedor de identidade SAML.</td>
    </tr>
    <tr>
      <td><code>displayName</code></td>
      <td>O nome designado à sua configuração SAML.</td>
    </tr>
    <tr>
      <td><code>primary-certificate-example-pem-format</code></td>
      <td>O certificado emitido por seu provedor de identidade SAML. Ele é usado para assinar e validar asserções SAML. Todos os provedores são diferentes, mas você pode ser capaz de fazer download do certificado de assinatura do seu provedor de identidade. O certificado deve estar no formato <code>.pem</code>.</td>
    </tr>
    <tr>
      <td>Opcional: <code>secondary-certificate-example-pem-format</code></td>
      <td>O certificado de backup emitido por seu provedor de identidade SAML. Ele será usado se a validação de assinatura falhar com o certificado primário. <strong>Nota</strong>: se a chave de assinatura permanecer a mesma, o {{site.data.keyword.appid_short_notm}} não bloqueará a autenticação para certificados expirados.</td>
    </tr>
    <tr>
      <td>Opcional: <code>authnContext</code></td>
      <td>O contexto de autenticação é usado para verificar a qualidade das asserções de autenticação e SAML. É possível incluir um contexto de autenticação, incluindo uma matriz de classe e uma sequência de comparação no código. Certifique-se de atualizar os parâmetros <code>class</code> e <code>comparison</code> com seus valores. Por exemplo, um parâmetro <code>class</code> pode parecer semelhante a <code>urn:oasis:names:tc:SAML:2.0:ac:classes:YourChosenClassValue</code>.</td>
    </tr>
  </table>

3. Faça uma solicitação PUT para o [terminal de API `/saml`](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp) fornecer a configuração criada na etapa 2 para o {{site.data.keyword.appid_short_notm}}. Verifique o exemplo a seguir para ver como sua solicitação pode parecer.

  ```
  curl --request PUT \
  https://us-south.appid.cloud.ibm.com/management/v4/<tenant-ID>/config/idps/saml \
  --header `Accept: application/json` \
  --data \
  {
    "isActive": true, "config": {
      "entityID": "https://example.com/saml2/metadata/706634", "signInUrl": "https://example.com/saml2/sso-redirect/706634", "certificates": [
        "primary-certificate-example-pem-format"
      ], "displayName": "my saml example", }
  }
  ```
  {: screen}



## Testando sua configuração
{: #saml-testing}

É possível testar a configuração entre seu Provedor de Identidade SAML e o {{site.data.keyword.appid_short_notm}}.

1. Certifique-se de que você salvou sua configuração.
2. Navegue para a guia **SAML 2.0** do painel {{site.data.keyword.appid_short_notm}} e clique em **Testar**. Uma nova guia é aberta.
3. Efetue login com um usuário que seu provedor de identidade já tenha autenticado.
4. Depois de concluir o formulário, você é redirecionado para outra página.
  * Autenticação bem-sucedida: a conexão entre o {{site.data.keyword.appid_short_notm}} e o Provedor de Identidade está funcionando corretamente. A página exibe [tokens de acesso e de identidade](/docs/services/appid?topic=appid-tokens#tokens) válidos.
  * Autenticação com falha: a conexão está quebrada. A página exibe os erros e o arquivo XML de resposta SAML.


Tendo problemas? Verifique [Resolução de problemas: SAML](/docs/services/appid?topic=appid-troubleshooting-idp#troubleshooting-idp).
{: tip}




## FAQ de SAML
{: #saml-assertions}

As asserções SAML podem ser retornadas de diferentes maneiras. Verifique os exemplos a seguir para ver a maneira na qual o {{site.data.keyword.appid_short_notm}} espera que a resposta seja formatada.
{: shortdesc}


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

