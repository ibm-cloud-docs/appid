---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-09"

keywords: Authentication, authorization, identity, app security, secure, troubleshooting, help, support, requests, uri

subcollection: appid

---

{:external: target="_blank" .external}
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

# Resolução de problemas: geral
{: #troubleshooting}

Se você tiver problemas enquanto está trabalhando com o {{site.data.keyword.appid_full}}, considere estas técnicas para resolução de problemas e obtenção de ajuda.
{: shortdesc}

## Obtendo ajuda e suporte
{: #ts-gettinghelp}

É possível obter ajuda procurando informações ou fazendo perguntas por meio de um fórum. Também é possível abrir um chamado de suporte. Quando estiver usando os fóruns para fazer uma pergunta, identifique sua pergunta para que ela seja vista pela equipe de
desenvolvimento do {{site.data.keyword.cloud_notm}}.
  * Se você tiver questões técnicas sobre o {{site.data.keyword.appid_short_notm}}, poste
a sua questão no <a href="https://stackoverflow.com/" target="_blank">Stack Overflow <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> e identifique-a com "ibm-appid".
  * Para perguntas sobre o serviço e instruções de introdução, use o fórum <a href="https://developer.ibm.com/" target="_blank">dW Answers <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>. Inclua a tag `appid`.

Para informações adicionais sobre como obter suporte, consulte [como obtenho o suporte de que preciso](/docs/get-support?topic=get-support-getting-customer-support#getting-customer-support).


## Um usuário não é redirecionado para o app após a conexão
{: #ts-signin-fail}

{: tsSymptoms}
Um usuário se conecta ao seu aplicativo por meio de uma página de conexão do provedor de identidade e nada acontece ou a conexão falha.

{: tsCauses}
A conexão pode falhar pelas razões a seguir:

* Sua URL de redirecionamento não foi incluída corretamente [na lista de desbloqueio](/docs/services/appid?topic=appid-faq#faq-redirect).
* O usuário não está autorizado.
* O usuário tentou conectar-se com as credenciais erradas.

{: tsResolve}
Para que um redirecionamento ocorra:

* Verifique se a sua URL de redirecionamento está correta. Ela deve ser exata para que o redirecionamento funcione.
* Certifique-se de que o usuário esteja conectando-se com as credenciais certas
* Verifique se elas estão definidas em suas configurações do usuário do provedor de identidade.



## Um URI customizado é rejeitado
{: #ts-custom-uri}

{: tsSymptoms}
Quando você insere uma URL de redirecionamento da web que usa um esquema de URL customizado, ela é rejeitada pelo
console do {{site.data.keyword.appid_short_notm}}.

{: tsCauses}
Sua URL pode ser rejeitada pelos motivos a seguir:

* A URL não segue um esquema `http` ou `https`
* A URL termina com `://`
* Há um erro tipográfico em sua URL

As limitações estão em vigor para fins de segurança.

{: tsResolve}
Para resolver o problema, verifique se a URL está correta. Se a sua URL não atender aos requisitos, será possível criar
um terminal HTTPS em seu aplicativo para redirecionar o código de concessão recebido para sua URL customizada. Especifique o
terminal criado como sua URL de redirecionamento no console do {{site.data.keyword.appid_short_notm}}. Para obter mais informações sobre URIs de redirecionamento, consulte [Incluindo URIs de redirecionamento](/docs/services/appid?topic=appid-managing-idp#add-redirect-uri)

## Um usuário não é redirecionado para o provedor de identidade
{: #ts-redirect}

{: tsSymptoms}
Um usuário tenta se conectar ao seu aplicativo, mas a página de conexão não é exibida quando solicitada.

{: tsCauses}
O provedor de identidade pode falhar por várias razões:

* Sua URL de redirecionamento configurada está incorreta.
* O provedor de identidade não reconhece a solicitação de autenticação.
* O provedor de identidade espera uma ligação HTTP-POST.
* O provedor de identidade espera uma AuthnRequest assinada.

{: tsResolve}
É possível tentar algumas destas soluções:

* Atualize sua URL de conexão. Essa URL é enviada como parte da AuthnRequest e deve ser exata.
* Certifique-se de que seus metadados do {{site.data.keyword.appid_short_notm}} estejam definidos corretamente em suas configurações de provedor de identidade.
* Configure seu provedor de identidade para aceitar a AuthnRequest no HTTP-Redirect.
* O {{site.data.keyword.appid_short_notm}} não suporta assinar AuthnRequests.

Se nenhuma das soluções funcionar, possivelmente você terá um problema de conexão.
{: tip}


## Um atributo está mostrando o valor incorreto
{: #ts-saml-attribute}

{: tsSymptoms}
Um valor de atributo existe em um perfil do usuário, mas ele não está associado ao atributo correto.

{: tsCauses}
O atributo do perfil do usuário não está mapeado corretamente.

{: tsResolve}
Mapeie o atributo em suas configurações do provedor de identidade. O {{site.data.keyword.appid_short_notm}} espera os atributos a seguir:
* `nome`
* `E-mail
`
* `locale`
* `picture`



## Erro: Excesso de solicitações
{: #ts-requests}

{: tsSymptoms}
Você tenta visualizar a página inicial de seu app, mas recebe o erro a seguir:

```
{ "error_code": "número excessivo de pedidos", "error_description": "excesso de pedidos" }
```
{: screen}

{: tsCauses}
Você poderá receber um erro "excesso de solicitações" se estiver executando o teste automatizado com apenas um usuário virtual. Cada usuário é limitado a cinco tentativas de conexão em uma amplitude de tempo de um minuto. As tentativas de conexão são limitadas para evitar DDoS de força bruta e outros tipos de ataques semelhantes.

{: tsResolve}
Para resolver o problema, você pode desejar usar múltiplos usuários virtuais ao executar o teste.
</br>
