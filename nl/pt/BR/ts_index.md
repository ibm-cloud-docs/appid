---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}

# Resolução de problemas
{: #troubleshooting}

Se você tiver problemas enquanto está trabalhando com o {{site.data.keyword.appid_full}}, considere estas técnicas para resolução de problemas e obtenção de ajuda.
{: shortdesc}


## Obtendo ajuda e suporte
{: #gettinghelp}

É possível obter ajuda procurando informações ou fazendo perguntas por meio de um fórum. Também é possível abrir um chamado de suporte. Quando estiver usando os fóruns para fazer uma pergunta, identifique sua pergunta para que ela seja vista pela equipe de
desenvolvimento do {{site.data.keyword.Bluemix_notm}}.
  * Se você tiver questões técnicas sobre o {{site.data.keyword.appid_short_notm}}, poste
a sua questão no <a href="http://stackoverflow.com/search?q=ibm+" target="_blank">Stack Overflow <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> e identifique-a com "ibm-appid".
  * Para perguntas sobre o serviço e instruções de introdução, use o fórum <a href="https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=appid%20[bluemix]" target="_blank">dW Answers <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>. Inclua a tag `appid`.

Para obter mais informações sobre como obter suporte, veja [Como obter o suporte que eu preciso?](/docs/get-support/howtogetsupport.html#getting-customer-support).

</br>

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

</br>

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
      <td>Há um <code><saml:Attribute> sem um valor definido. Entre em contato com seu administrador do provedor de identidade.</code></td>
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
      <td>Uma assinatura e uma compilação válidas devem ser incluídas na asserção. A assinatura deve ser criada usando a chave privada associada ao certificado que é fornecido na configuração SAML; secundário ou primário pode ser usado. <em>Nota</em>: o {{site.data.keyword.appid_short_notm}} não suporta a asserção criptografada. Se seu provedor de identidade faz isso com sua asserção SAML, desative a criptografia.</td>
    </tr>
  </tbody>
</table>


## Não há redirecionamento para o provedor de identidade ao usar SAML
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

Caso nenhuma dessas soluções funcionar, é possível que você tenha um problema de conexão.

</br>

## Um atributo está mostrando o valor errado ao usar SAML
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
