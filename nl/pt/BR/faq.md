---

copyright:
  years: 2017
lastupdated: "2017-12-12"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# Perguntas mais Frequentes

Esta FAQ fornece respostas às perguntas comuns sobre o serviço {{site.data.keyword.appid_full}}.
{: shortdesc}


## Como o {{site.data.keyword.appid_short_notm}} calcula os preços?
{: #pricing}

Com o {{site.data.keyword.appid_short_notm}}, você paga menos à medida que usa mais recursos.
{: shortdesc}

O plano de camada graduado consiste em duas partes: o número de eventos de autenticação e o número de usuários autorizados. Você é cobrado a cada mês, com base no resumo das duas partes. O preço total é o encargo acumulativo para cada nível de uso, consistindo em sua quantidade multiplicada pelo preço unitário na respectiva camada.

### Eventos de autenticação

Um evento de autenticação ocorre quando um novo token do {{site.data.keyword.appid_short_notm}} é emitido. Para usuários identificados, cada novo token é válido por uma hora. Os tokens são válidos por um mês para usuários anônimos. Após o token expirar, deve-se criar um novo token para acessar recursos protegidos. Quando você usa o ID do app para autenticação móvel, os tokens do usuário são armazenados em `key-store/key-chain` e são incluídos em cada solicitação futura. Os tokens são acessíveis usando o SDK Swift Android ou iOS do {{site.data.keyword.appid_short_notm}}. Ao usar o serviço para autenticação da web, <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">armazene o token do usuário <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> nos cookies de sessão.

### Usuários autorizados

Um usuário autorizado é um usuário exclusivo que efetua login com seu serviço, direta ou indiretamente. Você é cobrado por um usuário autorizado toda vez que um novo usuário efetua login de cada provedor de identidade, incluindo usuários anônimos. Por exemplo, se um usuário efetuar login com o Facebook e depois efetuar login usando o Google, ele será considerado como dois usuários autorizados separados.


Para obter mais informações sobre precificação de camada graduada, consulte os [ documentos de precificação do {{site.data.keyword.Bluemix_notm}}](/docs/pricing/index.html#pricing).
