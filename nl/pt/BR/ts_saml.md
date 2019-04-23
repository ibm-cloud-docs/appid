---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-10"

keywords: authentication, authorization, identity, app security, secure, development, idp, troubleshooting, redirected, validation

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
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}

# Configurações do provedor de identidade
{: #troubleshooting-idp}

Se você tiver problemas quando estiver configurando os provedores de identidade para trabalhar com o
{{site.data.keyword.appid_full}}, considere estas técnicas para solucionar problemas e obter ajuda.
{: shortdesc}


## Um usuário não é redirecionado para o provedor de identidade
{: #ts-saml-redirect}

{: tsSymptoms}
Um usuário tenta se conectar ao seu aplicativo, mas a página de conexão não é exibida quando solicitada.

{: tsCauses}
O provedor de identidade pode falhar por várias razões:

* Sua URL de redirecionamento configurada está incorreta.
* O provedor de identidade não reconhece a solicitação de autenticação.
* O provedor de identidade espera uma ligação HTTP-POST.
* O provedor de identidade espera um authnRequest assinado.

{: tsResolve}
É possível tentar algumas destas soluções:

* Atualize sua URL de conexão. Essa URL é enviada como parte do authnRequest e deve ser exata.
* Certifique-se de que seus metadados do {{site.data.keyword.appid_short_notm}} estejam definidos corretamente em suas configurações de provedor de identidade.
* Configure seu provedor de identidade para aceitar o authnRequest no HTTP-Redirect.
* O {{site.data.keyword.appid_short_notm}} não suporta assinatura de authnRequests.

Se nenhuma das soluções funcionar, possivelmente você terá um problema de conexão.
{: tip}


## Problemas comuns do SAML
{: #ts-common-saml}

Revise a tabela a seguir para obter explicações e soluções para os problemas mais comuns encontrados ao
trabalhar com o SAML.

<table summary="Cada linha da tabela deve ser lida da esquerda para a direita, com o estado do cluster na coluna um e uma descrição na coluna dois.">
  <thead>
    <th>Mensagem</th>
    <th>Descrição</th>
  </thead>
  <tbody>
    <tr>
      <td><code>Could not parse assertion xml.</code></td>
      <td>A resposta do SAML foi malformada.</td>
    </tr>
    <tr>
      <td><code>Invalid attribute without name. Entre em contato com seu administrador do provedor de identidade.</code></td>
      <td>Há um <code>&lt;saml:Attribute&gt;</code> sem um valor definido. Entre em contato com o administrador do provedor de identidade</td>
    </tr>
    <tr>
      <td><code>SAML response body must contain the RelayState parameter.</code></td>
      <td>O parâmetro não foi incluído no corpo de resposta do SAML. O {{site.data.keyword.appid_short_notm}} fornece o parâmetro para o provedor de identidade como parte da solicitação e o parâmetro exato deve ser retornado na resposta. Se o parâmetro for modificado, será possível entrar em contato com o seu administrador do provedor de identidade. </td>
    </tr>
    <tr>
      <td><code>SAML Configuration must have certificates, entityID and signInUrl of the IdP.</code></td>
      <td>O provedor de identidade do SAML não está <a href="/docs/services/appid?topic=appid-enterprise#enterprise" target="_blank">configurado corretamente</a>. Valide sua configuração.</td>
    </tr>
    <tr>
      <td><code>Error in assertion validation. SAML Assertion signature check failed! Certificate .. may be invalid.</code></td>
      <td>Uma assinatura e uma compilação válidas devem ser incluídas na asserção. A assinatura deve ser criada usando a chave
privada associada ao certificado que é fornecido na configuração do SAML. A chave secundária ou primária pode ser usada. <strong>Nota</strong>: o {{site.data.keyword.appid_short_notm}} não suporta a asserção criptografada. Se seu provedor de identidade criptografa a asserção SAML, desative a criptografia.</td>
    </tr>
  </tbody>
</table>



## Erros de validação de resposta do SAML
{: #ts-saml-response}

O {{site.data.keyword.appid_short_notm}} impõe os seguintes requisitos de validade para as asserções. Todos os atributos são nós XML de resposta SAML obrigatórios, a menos que especificado de outra forma.
{: shortdesc}


<table summary="Toda linha da tabela deve ser lida da esquerda para a direita, com o elemento de resposta na coluna um e uma descrição na coluna dois.">
  <thead>
    <th>Elemento de resposta</th>
    <th>Descrição</th>
  </thead>
  <tbody>
    <tr>
      <td><code>samlp:Response</code></td>
      <td>O elemento de resposta deve ser incluído no XML de resposta.</td>
    </tr>
    <tr>
      <td><code>SAML version</code></td>
      <td>O {{site.data.keyword.appid_short_notm}} aceita apenas <code>SAML version 2.0</code>.</td>
    </tr>
    <tr>
      <td><code>InResponseTo</code></td>
      <td>O {{site.data.keyword.appid_short_notm}} verifica se o elemento de resposta <code>InResponseTo</code> retornado
na asserção corresponde ao ID de solicitação salvo da solicitação SAML.</td>
    </tr>
    <tr>
      <td><code>saml:issuer</code></td>
      <td>O emissor que é especificado em uma asserção deve corresponder ao emissor que é especificado na configuração do provedor
de identidade do {{site.data.keyword.appid_short_notm}}.</td>
    </tr>
    <tr>
      <td><code>ds:Signature</code></td>
      <td>Uma assinatura e uma compilação válidas devem ser incluídas na asserção. A assinatura deve ser criada usando a chave privada que está associada ao certificado fornecido na configuração SAML. A compilação é validada usando o
<code>CanonicalizationMethod</code> e o <code>Transforms</code> especificados. <strong>Nota</strong>: o {{site.data.keyword.appid_short_notm}} não valida a expiração do certificado. Para
obter ajuda para o gerenciamento de seus certificados, experimente o
[Gerenciador de certificado](/docs/services/certificate-manager?topic=certificate-manager-getting-started#getting-started).</td>
    </tr>
    <tr>
      <td><code>saml:subject</code></td>
      <td>O assunto ou <code>name_id</code> da asserção deve ser o e-mail de federação do usuário.</td>
    </tr>
    <tr>
      <td><code>saml:AttributeStatement</code></td>
      <td>Declara que determinados atributos estão associados a um usuário autenticado específico.</td>
    </tr>
    <tr>
      <td><code>saml:Conditions</code></td>
      <td><strong>Opcional</strong>: quando uma instrução de condições é incluída em uma asserção, ela também deve conter um
registro de data e hora válido. O {{site.data.keyword.appid_short_notm}} honra o período de validade que é
especificado em uma asserção. Para verificar, o serviço procura as restrições <code>NotBefore</code> e <code>NotOnOrAfter</code> que devem ser definidas e válidas.</td>
    </tr>
  </tbody>
</table>

O {{site.data.keyword.appid_short_notm}} não suporta asserção criptografada. Se o seu provedor de identidade
estiver configurado para criptografar sua asserção, desative a criptografia. A asserção deve estar em um formato não criptografado.
{: tip}
