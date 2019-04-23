---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

keywords: authentication, authorization, identity, app security, secure, user profiles, personalized apps, attributes, 

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

# Entendendo perfis do usuário
{: #user-profile}

Com o {{site.data.keyword.appid_full}}, é possível construir experiências de aplicativo personalizadas acessando as
informações sobre os usuários armazenadas pelo {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

## Conceitos-chave
{: #profile-concepts}

** O que é um perfil do usuário? **

Um perfil do usuário é uma coleção de atributos armazenados pelo {{site.data.keyword.appid_short_notm}}. Atributos são
partes de informações sobre os usuários que interagem com o aplicativo. É possível obter dois tipos de atributos:
`predefined` e `custom`.



** Quais são os atributos predefinidos? **

Os atributos predefinidos são retornados pelo provedor de identidade quando seu usuário se conecta ao seu aplicativo. Os
atributos podem incluir o nome do usuário, a idade ou o gênero.



** O que são atributos customizados? **

Os atributos customizados são aprendidos sobre os usuários conforme eles interagem com o aplicativo. Os atributos
customizados também podem ser configurados por você antes que o usuário se conecte ao seu aplicativo pela primeira vez. Um
exemplo pode ser o tamanho da fonte que o usuário prefere ou os itens que coloca em um carrinho de compras. Os atributos customizados podem ser editados. Certifique-se de verificar as [implicações de segurança](/docs/services/appid?topic=appid-custom-attributes) que podem ocorrer
ao permitir que os usuários editem seus atributos antes de mudar o padrão.


## Acessando atributos do usuário
{: #profile-access}

Há maneiras diferentes pelas quais é possível acessar os atributos [predefinidos](/docs/services/appid?topic=appid-predefined-attributes) e
[customizados](/docs/services/appid?topic=appid-custom-attributes). Após uma autenticação do usuário bem-sucedida, seu aplicativo
recebe os tokens de acesso e de identidade. O token de identidade contém um subconjunto normalizado de
atributos do usuário que é retornado por um provedor de identidade. Para obter a lista completa de atributos do usuário,
é possível usar o terminal
[`/userinfo`
do OIDC](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Authorization_Server_V4/userInfo). Para gerenciar os atributos customizados, é possível usar a API
de REST`. Ambas as informações do usuário e os terminais de atributos customizados são protegidos pelo token de acesso que é gerado pelo {{site.data.keyword.appid_short_notm}} no término do processo de autenticação.

Para obter mais informações sobre os tokens de identidade e de acesso, consulte
[Entendendo os tokens](/docs/services/appid?topic=appid-tokens#tokens) ou
[Validando os tokens](/docs/services/appid?topic=appid-token-validation).

![Arquitetura do perfil do usuário do {{site.data.keyword.appid_short_notm}}](images/user-profile1.png)

Figura. Fluxo de informações do perfil do usuário

Para ver atributos customizados, é possível usar a <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Attributes" target="_blank">API de REST <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.

