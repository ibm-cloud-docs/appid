---

copyright:
  years: 2017, 2018
lastupdated: "2018-10-18"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}

# SAML
{: #enterprise}


Security Assertion Markup Language (SAML) é um padrão aberto para troca de dados de autenticação e de autorização entre
um provedor de identidade que afirma a identidade do usuário e um provedor de serviços que consome as informações de
identidade do usuário.
{: shortdesc}

O {{site.data.keyword.appid_short_notm}} funciona como um provedor de serviços e inicia um login de conexão única (SSO) para um provedor de terceiros como o Active Directory Federation Services. O protocolo <a href="http://saml.xml.org/saml-specifications" target="blank">SAML <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> suporta diferentes perfis e opções de ligação. O {{site.data.keyword.appid_short_notm}} suporta o perfil SSO do navegador da web com a ligação de Post HTTP.

Para obter as etapas sobre como usar um provedor de identidade SAML específico, consulte essas postagens de
blog sobre a configuração do {{site.data.keyword.appid_short_notm}} com o [Ping One
![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-ping-one/),
[um Azure Active Directory
![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-azure-active-directory/) ou
[um Active Directory Federation Service ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-active-directory-federation-service/).
{: tip}


## Asserções SAML e solicitações de token de identidade

Uma asserção SAML é um pacote de informações que contêm uma ou mais instruções. A asserção contém a decisão de autorização e pode conter informações de identificação sobre o usuário.

Quando um usuário se conecta com um provedor de identidade, esse provedor envia uma asserção para o {{site.data.keyword.appid_short_notm}}. O {{site.data.keyword.appid_short_notm}} propaga as informações de identificação do usuário que são retornadas na asserção SAML para seu app como solicitações de token OIDC. O atributo SAML deve corresponder a uma das solicitações OIDC a seguir para ser incluído no token de identidade.

As solicitações a seguir podem ser incluídas:
* `nome`
* `E-mail
`
* `locale`
* `picture`

Os elementos de atributo SAML restantes que não correspondem a nenhum dos nomes padrão são ignorados. Observe que se um ou
mais desses valores mudarem no lado do provedor, os novos valores estarão disponíveis somente após o usuário efetuar login novamente.


Procurando um exemplo? Consulte <a href="https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-azure-active-directory/" target="_blank">Configurando o {{site.data.keyword.appid_long}} com o seu Azure Active Directory <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> ou <a href="https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-ping-one/" target="_blank">Configurando o {{site.data.keyword.appid_long}} com o Ping One <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.

## Fornecendo metadados para seu provedor de identidade
{: #provide-idp}

Para configurar seu app, você precisa fornecer informações para um provedor de identidade compatível com SAML. As informações são trocadas por meio de um arquivo XML de metadados que também contém dados de configuração que são usados para estabelecer confiança.
{: shortdesc}

1. Na guia **Gerenciar** do painel {{site.data.keyword.appid_short_notm}}, configure **SAML 2.0** para **Ligado**. Em seguida, clique em **Editar** para definir suas configurações de SAML.
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

3. Forneça os dados para seu provedor de identidade. Se seu provedor de identidade suporta upload do arquivo de metadados, é possível fazer isso. Se não, configure as propriedades manualmente. Nem todo provedor de identidade usará as mesmas propriedades, então, se você não usar todas elas, tudo bem.

Os nomes da propriedade podem diferir entre os provedores de identidade.
{: tip}

## Fornecendo metadados para o {{site.data.keyword.appid_short_notm}}
{: #provide-appid}

Obtenha dados de seu provedor de identidade e forneça-os ao {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

**Fornecendo metadados com a GUI**

1. Navegue para a guia **SAML 2.0** do painel {{site.data.keyword.appid_short_notm}}. Insira os metadados a seguir que você obteve do provedor de identidade na seção **Fornecer metadados do SAML IdP**.
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
</br>

**Fornecendo metadados com a API**

1. Obtenha seus metadados SAML fazendo uma solicitação GET para o terminal da API [/getSamlMetadata](https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/getSamlMetadata).

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
terminal da API [/set_saml_idp](https://appid-management.ng.bluemix.net/swagger-ui/#!/Identity_Providers/set_saml_idp).

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
{: #testing}

É possível testar a configuração entre seu Provedor de Identidade SAML e o {{site.data.keyword.appid_short_notm}}.

1. Certifique-se de que você salvou sua configuração.
2. Navegue para a guia **SAML 2.0** do painel {{site.data.keyword.appid_short_notm}} e clique em **Testar**. Uma nova guia é aberta.
3. Efetue login com um usuário que seu provedor de identidade já tenha autenticado.
4. Depois de concluir o formulário, você é redirecionado para outra página.
  * Autenticação bem-sucedida: a conexão entre o {{site.data.keyword.appid_short_notm}} e o Provedor de Identidade está funcionando corretamente. A
página exibe os [tokens de acesso e de identidade](/docs/services/appid/authorization.html#tokens)
válidos.
  * Autenticação com falha: a conexão está quebrada. A página exibe os erros e o arquivo XML de resposta SAML.


Tendo problemas? Consulte [Solucionando problemas de
configurações do provedor de identidade](/docs/services/appid/ts_saml.html)
{: tip}
