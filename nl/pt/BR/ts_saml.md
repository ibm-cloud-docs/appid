---

copyright:
  years: 2017, 2018
lastupdated: "2018-06-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tip: .tip}

# Configurações do provedor de identidade
{: #troubleshooting-idp}

Se você tiver problemas ao configurar os provedores de identidade para trabalhar com o {{site.data.keyword.appid_full}},
considere essas técnicas para resolução de problemas e obtenção de ajuda.
{: shortdesc}


## Não há redirecionamento para o app após a conexão
{: #signin-fail}

{: tsSymptoms}
Um usuário conecta-se a seu aplicativo por meio da página de conexão de um provedor de identidade e nada acontece ou a conexão falha.

{: tsCauses}
A conexão pode falhar pelas razões a seguir:

* Sua URL de redirecionamento não foi incluída corretamente [na lista de desbloqueio](identity-providers.html#redirect).
* O usuário não está autorizado.
* O usuário tentou conectar-se com as credenciais erradas.

{: tsResolve}
Para que um redirecionamento ocorra:

* Verifique se a sua URL de redirecionamento está correta. Ela deve ser exata para que o redirecionamento funcione.
* Certifique-se de que o usuário esteja conectando-se com as credenciais certas
* Verifique se elas estão definidas em suas configurações do usuário do provedor de identidade.


## Problemas comuns ao trabalhar com SAML
{: #common-saml}

Revise a tabela a seguir para explicações e resoluções para os problemas mais comuns que são encontrados ao trabalhar com SAML.

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
      <td><code>SAML response body must contain RelayState.</code></td>
      <td>O parâmetro RelayState não foi incluído no corpo de resposta SAML. O {{site.data.keyword.appid_short_notm}} fornece o parâmetro para o provedor de identidade como parte da solicitação e o parâmetro exato deve ser retornado na resposta. Se o parâmetro for modificado, será possível entrar em contato com o seu administrador do provedor de identidade. </td>
    </tr>
    <tr>
      <td><code>SAML Configuration must have certificates, entityID and signInUrl of the IdP.</code></td>
      <td>O provedor de identidade SAML não está configurado corretamente. Valide sua configuração. Para obter ajuda, veja <a href="enterprise.html#configuring-saml" target="_blank">Configurando seu app para trabalhar com um provedor de identidade SAML externo.</a></td>
    </tr>
    <tr>
      <td><code>Error in assertion validation. SAML Assertion signature check failed! Certificate .. may be invalid.</code></td>
      <td>Uma assinatura e uma compilação válidas devem ser incluídas na asserção. A assinatura deve ser criada usando a chave privada associada ao certificado que é fornecido na configuração SAML; secundário ou primário pode ser usado. <strong>Nota</strong>: o {{site.data.keyword.appid_short_notm}} não suporta a asserção criptografada. Se seu provedor de identidade faz isso com sua asserção SAML, desative a criptografia.</td>
    </tr>
  </tbody>
</table>


## Não há redirecionamento para o provedor de identidade
{: #saml-redirect}

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

## Um atributo está mostrando o valor incorreto
{: #saml-attribute}

{: tsSymptoms}
Um valor de atributo existe em um perfil do usuário, mas não está conectado ao atributo correto.

{: tsCauses}
O Atributo de perfil do usuário não está mapeado corretamente.

{: tsResolve}
Mapeie o atributo em suas configurações do provedor de identidade. O {{site.data.keyword.appid_short_notm}} espera os atributos a seguir:
* `nome`
* `E-mail
`
* `locale`
* `picture`


