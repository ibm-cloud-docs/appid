---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:pre: .pre}
{:tip: .tip}
{:screen: .screen}

# Entendendo perfis do usuário
{: #user-profile}

Com o {{site.data.keyword.appid_full}}, é possível construir experiências de aplicativo personalizadas acessando as
informações sobre os usuários armazenadas pelo {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

## Conceitos-chave
{: #key-concepts}

** O que é um perfil do usuário? **

Um perfil do usuário é uma coleção de atributos armazenados pelo {{site.data.keyword.appid_short_notm}}. Atributos são
partes de informações sobre os usuários que interagem com o aplicativo. É possível obter dois tipos de atributos:
`predefined` e `custom`.

</br>

** Quais são os atributos predefinidos? **

Os atributos predefinidos são retornados pelo provedor de identidade quando seu usuário se conecta ao seu aplicativo. Os
atributos podem incluir o nome do usuário, a idade ou o gênero.

</br>

** O que são atributos customizados? **

Os atributos customizados são aprendidos sobre os usuários conforme eles interagem com o aplicativo. Os atributos
customizados também podem ser configurados por você antes que o usuário se conecte ao seu aplicativo pela primeira vez. Um
exemplo pode ser o tamanho da fonte que o usuário prefere ou os itens que coloca em um carrinho de compras. Os atributos customizados podem ser editados. Certifique-se de verificar as [implicações de segurança](custom-attributes.html) que podem ocorrer
ao permitir que os usuários editem seus atributos antes de mudar o padrão.

</br>
</br>

## Acessando atributos do usuário
{: #access}

Há maneiras diferentes pelas quais é possível acessar os atributos [predefinidos](predefined.html) e
[customizados](custom-attributes.html). Após uma autenticação do usuário bem-sucedida, seu aplicativo
recebe os tokens de acesso e de identidade. O token de identidade contém um subconjunto normalizado de
atributos do usuário que é retornado por um provedor de identidade. Para obter a lista completa de atributos do usuário,
é possível usar o terminal
[`/userinfo`
do OIDC](https://appid-oauth.ng.bluemix.net/swagger-ui/#!/Authorization_Server_V3/userInfo). Para gerenciar os atributos customizados, é possível usar a API
de REST`. Os terminais de informações sobre o usuário e de atributo customizado são protegidos pelo token de
acesso gerado pelo {{site.data.keyword.appid_short_notm}} no término do processo de autenticação.

Para obter mais informações sobre os tokens de identidade e de acesso, consulte
[Entendendo os tokens](/docs/services/appid/authorization.html#tokens) ou
[Validando os tokens](/docs/services/appid/tokens.html).

![Arquitetura do perfil do usuário do {{site.data.keyword.appid_short_notm}}](images/user-profile1.png)

Figura. Fluxo de informações do perfil do usuário

Para ver os atributos customizados, é possível usar a
<a href="https://appid-profiles.ng.bluemix.net/swagger-ui/index.html#/Attributes" target="_blank">API de REST
<img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.


</br>
</br>
