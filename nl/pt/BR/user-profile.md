---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-03"

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
partes de informações sobre os usuários que interagem com o aplicativo. Há dois tipos de atributos que podem ser obtidos: `predefinidos` e `customizados`.

** Quais são os atributos predefinidos? **

Os atributos predefinidos são retornados pelo provedor de identidade quando o usuário se conecta ao aplicativo. Os
atributos podem incluir o nome do usuário, a idade ou o gênero.

** O que são atributos customizados? **

Os atributos customizados são aprendidos sobre os usuários conforme eles interagem com o aplicativo. Eles podem ser o tamanho
da fonte usada ou os itens que foram colocados em um carrinho de compras. Os atributos customizados podem ser editados.

## Acessando atributos do usuário
{: #access}

Há diferentes maneiras pelas quais é possível acessar as informações de perfil do usuário. Após uma autenticação do usuário
bem-sucedida, o aplicativo recebe os tokens de acesso e de identidade. O token de identidade contém um subconjunto normalizado de
atributos do usuário que é retornado por um provedor de identidade. Para obter a lista completa de atributos do usuário, é
possível usar o terminal `/userinfo` do OIDC. Para gerenciar os atributos customizados, é possível usar a `API
de REST`. Os terminais userinfo e de atributo customizado são protegidos pelo token de acesso gerado pelo
{{site.data.keyword.appid_short_notm}} no término do processo de autenticação.



![{} user profile architecture](/images/user-profile1.png)

Figura. Fluxo de informações do perfil do usuário

Para ver os atributos customizados, é possível usar a
<a href="https://appid-profiles.ng.bluemix.net/swagger-ui/index.html#/Attributes" target="_blank">API de REST
<img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.

</br>
</br>
