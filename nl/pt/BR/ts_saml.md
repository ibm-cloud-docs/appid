---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-21"

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

# Resolução de problemas: SAML
{: #troubleshooting-idp}

Se tiver problemas quando estiver configurando o SAML para trabalhar com o {{site.data.keyword.appid_full}}, considere estas técnicas para solucionar problemas e obter ajuda.
{: shortdesc}


## Problemas comuns de configuração
{: #ts-common-saml}

A estrutura SAML suporta vários perfis, fluxos e configurações, o que significa que é essencial que sua configuração do provedor de identidade esteja definida corretamente. Verifique os tópicos a seguir para ajudar a resolver alguns dos problemas comuns que você pode encontrar ao trabalhar com o SAML.
{: shortdesc}


Para obter os códigos de erro e mensagens específicos de seu provedor de identidade que não são exibidos nesta página, será útil procurar a [especificação SAML](http://docs.oasis-open.org/security/saml/Post2.0/sstc-saml-tech-overview-2.0.html) para obter explicações detalhadas. Caso não localize o que está procurando, é possível entrar em contato com seu administrador de provedores de identidade para obter mais informações.
{: note}



### Parâmetro `RelayState` ausente
{: #ts-saml-relaystate}

**O que está acontecendo**

O parâmetro `RelayState` está ausente em sua resposta de autenticação.


**Por que isso está acontecendo?**

O {{site.data.keyword.appid_short_notm}} envia um parâmetro opaco conhecido como `RelayState` como parte da solicitação de autenticação. Se você não vir o parâmetro em sua resposta, seu provedor de identidade poderá não estar configurado para retorná-lo corretamente. O `RelayState` usa o formato a seguir.

```
https://idp.example.org/SAML2/SSO/Redirect?SAMLRequest=request&RelayState=token
```
{: screen}

**Como corrigir isso**

Verifique se o seu provedor SAML está configurado para retornar o parâmetro `RelayState` para o {{site.data.keyword.appid_short_notm}} sem modificá-lo de nenhuma maneira.


### Campo NameID ausente ou incorreto
{: #ts-saml-nameid}

**O que está acontecendo**

Ao enviar uma solicitação de autenticação, você recebe um erro sobre o `NameID`.

**Por que isso está acontecendo?**

O {{site.data.keyword.appid_short_notm}}, como o provedor de serviços, define a maneira com que os usuários são identificados pelo serviço e pelo provedor de identidade. Com o {{site.data.keyword.appid_short_notm}}, os usuários são identificados na solicitação de autenticação `NameID` no campo `NameID`, conforme mostrado no exemplo a seguir.

```
<NameIDFormat>urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress</NameIDFormat>
```
{: screen}

**Como corrigir isso**

Para resolver o problema, certifique-se de que seu provedor de identidade `NameID` seja formatado como um endereço de e-mail. Verifique se todos os usuários em seu registro de provedor de identidade têm um formato de endereço de e-mail válido. Em seguida, verifique se o campo `NameID` está definido apropriadamente para que um e-mail válido seja sempre retornado, mesmo se os usuários em seu registro tiverem vários e-mails.



### Falha na assinatura da resposta
{: #ts-saml-response-sign-fail}

**O que está acontecendo**

Ao enviar uma solicitação de autenticação, você recebe a mensagem de erro a seguir:

```
Could not verify SAML assertion signature. Ensure {{site.data.keyword.appid_short_notm}} is configurated with your SAML provider's signing certificate.
```
{: screen}

**Por que isso está acontecendo?**

O {{site.data.keyword.appid_short_notm}} espera todas as asserções SAML em sua resposta a serem assinadas. Se o serviço não puder localizar ou verificar a assinatura na resposta, o erro será retornado.

**Como corrigir isso**

Para resolver o problema, certifique-se de que:

* Você tenha extraído o certificado de assinatura de seu arquivo XML de metadados de provedores de identidade. Certifique-se de usar a chave com `<KeyDescriptor use="signing">`.
* Você tenha configurado o algoritmo de assinatura de resposta para ser XXX. 





### Falha ao decriptografar a resposta
{: #ts-saml-decrypt-fail}

**O que está acontecendo**

Você recebe uma das mensagens de erro a seguir em resposta à sua solicitação de autenticação.

Mensagem de erro 1:

```
Unexpectedly received an encrypted assertion. Please enable response encryption in your {{site.data.keyword.appid_short_notm}} SAML configuration.
```
{: screen}

Mensagem de erro 2: 

```
Could not decrypt SAML assertion. Ensure your SAML provider is configured with the {{site.data.keyword.appid_short_notm}} encryption 
```
{: screen}


**Por que isso está acontecendo?**

Se o seu provedor de identidade estiver configurado para criptografar, o {{site.data.keyword.appid_short_notm}} deverá ser configurado para assinar as solicitações de autenticação SAML (AuthnRequest). Em seguida, seu provedor de identidade deve ser configurado para esperar a configuração correspondente. Você pode receber esses erros por causa de uma das razões a seguir:

- O {{site.data.keyword.appid_short_notm}} não está configurado para esperar que a resposta SAML do provedor de identidade esteja criptografada.
- O {{site.data.keyword.appid_short_notm}} não pode decriptografar corretamente suas asserções.


**Como corrigir isso**

Se você receber a mensagem de erro 1, verifique se a configuração do SAML está definida para esperar uma resposta criptografada. Por padrão, o {{site.data.keyword.appid_short_notm}} não espera que a resposta seja criptografada. Para definir a criptografia, configure o parâmetro `encryptResponse` como **true** usando [a API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp).

Se você receber a mensagem de erro 2, assegure-se de que seu certificado esteja correto. É possível obter o certificado de assinatura do arquivo XML de metadados do {{site.data.keyword.appid_short_notm}}. Certifique-se de usar a chave com `<KeyDescriptor use="signing">`. Verifique se o seu provedor de identidade está configurado para usar `` como o algoritmo de assinatura. 


### Código de erro do respondente
{: #ts-saml-responder}

**O que está acontecendo**

Ao enviar uma solicitação de autenticação, você recebe a mensagem de erro genérica a seguir:

```
urn:oasis:names:tc:SAML:2.0:status:Responder
```
{: screen}

**Por que isso está acontecendo?**

Embora o {{site.data.keyword.appid_short_notm}} envie a solicitação de autenticação inicial, o provedor de identidade deve executar a autenticação do usuário e retornar a resposta. Há várias razões que podem fazer com que seu provedor de identidade lance essa mensagem de erro.

Você poderá ver a mensagem se seu provedor de identidade: 

* não puder localizar ou verificar o nome de usuário.
* não suportar o formato `NameID` definido na solicitação de autenticação (`AuthnRequest`).
* não suportar o contexto de autenticação.
* requerer que a solicitação de autenticação seja assinada ou use um algoritmo específico na assinatura.

**Como corrigir isso**

Para resolver o problema, verifique sua configuração e seu nome de usuário. Verifique se você tem o contexto de autenticação correto e as variáveis definidas. Verifique se a sua solicitação precisa ser assinada de uma maneira específica.




### Solicitação de autenticação não suportada
{: #ts-saml-unsupported-request}

**O que está acontecendo**

Você recebe uma mensagem em relação a uma solicitação de autenticação não suportada.

**Por que isso está acontecendo?**

Quando o {{site.data.keyword.appid_short_notm}} gera uma solicitação de autenticação, ele pode usar o contexto de autenticação para solicitar a qualidade das asserções de autenticação e SAML.

**Como corrigir isso**

Para resolver o problema, é possível atualizar seu contexto de autenticação. Por padrão, o {{site.data.keyword.appid_short_notm}} usa a classe de autenticação `urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport` e a comparação `exact`. É possível atualizar o parâmetro de contexto para ajustar seu caso de uso usando as APIs.




### Falha na assinatura da solicitação SAML
{: #ts-saml-request-sign-fail}

**O que está acontecendo**

Você recebe um erro que indica que uma solicitação de autenticação não pode ser verificada.

**Por que isso está acontecendo?**

O {{site.data.keyword.appid_short_notm}} pode ser configurado para assinar a solicitação de autenticação SAML (`AuthNRequest`), mas seu provedor de identidade deve ser configurado para esperar a configuração correspondente.

**Como corrigir isso**

Para resolver o problema:

* Verifique se o {{site.data.keyword.cloud_notm}} está configurado para assinar a solicitação de autenticação configurando o parâmetro `signRequest` como `true` usando a [API de set SAML IdP](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp). É possível verificar se a sua solicitação de autenticação está assinada, examinando a URL de solicitação. A assinatura é incluída como um parâmetro de consulta. Por exemplo: `https://idp.example.org/SAML2/SSO/Redirect?SAMLRequest=request&SigAlg=value&Signature=value&RelayState=token`

* Verifique se seu provedor de identidade está configurado com o certificado correto. Para obter o certificado de assinatura, verifique o arquivo XML de metadados do {{site.data.keyword.cloud_notm}} transferido por download do painel do {{site.data.keyword.cloud_notm}}. Assegure-se de usar a chave com `<KeyDescriptor use="signing">`.

* Verifique se seu provedor de identidade está configurado para usar `` como o algoritmo de assinatura.



## Depurando sua conexão
{: #ts-saml-debug-connection}

Tem a configuração correta, mas ainda apresenta erro? Verifique algumas das dicas úteis a seguir para depurar sua conexão SAML.
{: shortdesc}


### Como capturar minha solicitação e resposta de autenticação SAML?
{: #ts-saml-capture}

Há várias opções para plug-ins do navegador, como [Firefox](https://addons.mozilla.org/en-US/firefox/addon/saml-tracer/) e [Chrome](https://chrome.google.com/webstore/detail/saml-tracer/mpdajninpobndbfcldcmbpnnbhibjmch?hl=en), que podem ser usadas para capturar suas solicitações e respostas do SAML. Não quer usar um plug-in? Sem problemas. A Atlassian fornece instruções para uma [abordagem de extração mais manual](https://confluence.atlassian.com/jirakb/how-to-view-a-saml-responses-in-your-browser-for-troubleshooting-872129244.html).


### Não entendo as mensagens. Como posso decodificá-las?
{: #ts-saml-decode-messages}

Se ainda estiver tendo problemas depois de usar a ferramenta de depuração do SAML, tente usar as [ferramentas de desenvolvedor do SAML](https://www.samltool.com/online_tools.php) para obter mais ajuda ao decodificar suas mensagens. Não se esqueça. Dependendo de onde você intercepta suas mensagens SAML, sua solicitação poderá ser [codificada por URL](https://www.samltool.com/online_tools.php), [codificada e esvaziada com base 64](https://www.samltool.com/decode.php) ou [criptografada](https://www.samltool.com/decrypt.php).

Não use ferramentas on-line para decriptografar mensagens SAML como sua resposta SAML. As ferramentas precisam de acesso à chave privada de criptografia para decriptografar as informações. A chave deve ser mantida sob controle privado e de acesso. A ferramenta de decriptografia mencionada nesta seção deve ser usada apenas para propósitos de depuração.
{: important}

