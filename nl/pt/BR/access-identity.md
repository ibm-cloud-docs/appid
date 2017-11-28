---

copyright:
  years: 2017
lastupdated: "2017-11-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Tokens de acesso e de identidade

O {{site.data.keyword.appid_short}} usa dois tipos de tokens: de acesso e de identidade. Os tokens são formatados como
<a href="https://jwt.io/introduction/" target="_blank">Tokens da web da JSON <img src="../../icons/launch-glyph.svg" alt="ícone de Link externo"></a>.
{:shortdesc}


## Token de Acesso
{: #access-tokens}

O token de acesso permite a comunicação com os [recursos de backend](/docs/services/appid/protecting-resources.html) que são protegidos
pelos filtros de autorização do {{site.data.keyword.appid_short_notm}}. O token adequa-se às especificações do JavaScript Object Signing and Encryption (JOSE) e tem o formato a seguir:

```
Header: {
    "typ": "JOSE",
    "alg": "RS256",
}
Payload: {
    "iss": "appid-oauth.ng.bluemix.net",
    "exp": "1495562664",
    "aud": "a3b87400-f03b-4956-844e-a52103ef26ba",
    "amr": "facebook",
    "sub": "de6a17d2-693d-4a43-8ea2-2140afd56a22",
    "iat": "1495559064",
    "tenant": "9781974b-6a1c-46c3-aebf-32b7e9bbbaee",
    "scope": "appid_default appid_readprofile appid_readuserattr appid_writeuserattr",
}
```
{:screen}

<table>
<caption> Tabela 1. Componentes de token de acesso explicados </caption>
  <tr>
    <th> Componente </th>
    <th> Descrição </th>
  </tr>
  <tr>
    <td> <i> typ </i> </td>
    <td> O tipo de cabeçalho, especificado como "JOSE". </td>
  </tr>
  <tr>
    <td> <i> alg </i> </td>
    <td> O algoritmo usado, especificado como "RS256". </td>
  </tr>
  <tr>
    <td> <i> iss </i> </td>
    <td> O servidor {{site.data.keyword.appid_short}} que emitiu o token; especificado como uma sequência ou uma URL. </td>
  </tr>
  <tr>
    <td> <i> sub </i> </td>
    <td> O ID do usuário para quem o token é emitido. </td>
  </tr>
  <tr>
    <td> <i> aud </i> </td>
    <td> O identificador de cliente para o qual o token se destina. </td>
  </tr>
  <tr>
    <td> <i> exp </i> </td>
    <td> O horário em que o registro de data e hora expira, especificado no tempo da época. </td>
  </tr>
  <tr>
    <td> <i> iat </i> </td>
    <td> O horário em que o registro de data e hora é emitido, especificado no tempo da época. </td>
  </tr>
  <tr>
    <td> <i> tenant </i> </td>
    <td> O ID do locatário para o qual o token é emitido. </td>
  </tr>
  <tr>
    <td> <i> amr </i> </td>
    <td> O provedor de identidade usado para autenticação. Essa variável pode ser <i>appid_facebook</i> ou <i>appid_google</i>. </td>
  </tr>
  <tr>
    <td> <i> scope </i> </td>
    <td> O escopo para o qual o token é emitido. </td>
  </tr>
</table>


## Token de identidade
{: #identity-tokens}

O token de identidade contém informações sobre o usuário, incluindo nome, e-mail, sexo, foto e local.

```
Header: {
    "typ": "JOSE",
    "alg": "RS256",
}
Payload: {
    "iss": "appid-oauth.ng.bluemix.net",
    "aud": "a3b87400-f03b-4956-844e-a52103ef26ba",
    "exp: "1495562664",
    "tenant": "9781974b-6a1c-46c3-aebf-32b7e9bbbaee",
    "iat": "1495559064",
    "name": "John Smith",
    "email": "js@mail.com",
    "gender", "male",
    "locale": "en",
    "picture": "https://url.to.photo",
    "sub": "de6a17d2-693d-4a43-8ea2-2140afd56a22",
    "identities": [
        "provider": "facebook"
        "id": "377440159275659",
        "amr: "facebook",
    ],
    "oauth_client":{
      "name": "BluemixApp",
      "type": "serverapp",
      "software_id": "cb638f8f-e24b-41d3-b770-23be158dd8e6.2b94e6bb-bac4-4455-8712-a43fa804d5cc.a3b87400-f03b-4956-844e-a52103ef26ba",
      "software_version": "1.0.0",
    }
}
```
{:screen}


<table>
<caption> Tabela 2. Componentes de token de identidade explicados </caption>
  <tr>
    <th> Componente </th>
    <th> Descrição </th>
  </tr>
  <tr>
    <td> <i>name</i> </td>
    <td> O nome completo do usuário, conforme relatado pelo provedor de identidade. Isso deve ser retornado. </td>
  </tr>
  <tr>
    <td> <i> email </i> </td>
    <td> O e-mail do usuário, conforme relatado pelo provedor de identidade. Retornado somente quando disponível. </td>
  </tr>
  <tr>
    <td> <i> gender </i> </td>
    <td> O sexo do usuário, conforme relatado pelo provedor de identidade, quando disponível. </td>
  </tr>
  <tr>
    <td> <i> locale </i> </td>
    <td> O código de idioma do usuário, conforme relatado pelo provedor de identidade. </td>
  </tr>
  <tr>
    <td> <i> picture </i> </td>
    <td> A URL para a foto de um usuário, se disponível. </td>
  </tr>
  <tr>
    <td> <i> identities: </br> <ul><li> provider <li> id <li> amr </ul></i></td>
    <td> </br><ul><li> O provedor de identidade usado para autenticação. Essa variável pode ser <code>appid_facebook</code> ou <code>appid_google</code> e deve ser retornada. </li><li> Um ID de usuário exclusivo, conforme relatado por um provedor de identidade. </li><li> Um objeto JSON que deve ser retornado pelo provedor de identidade. </li></ul></td>
  </tr>
  <tr>
    <td> <i> oauth_client: </br> <ul><li> type <li> name <li> software_id <li> software_version</ul></i> </td>
    <td> </br><ul><li> O tipo de aplicativo determinado durante o registro do cliente. A variável pode ser <i>serverapp</i> ou <i>mobileapp</i>. <li> O nome do cliente, conforme relatado durante o registro do cliente. <li> O ID do software, conforme relatado durante o registro do cliente. <li> A versão de software usada durante o registro do cliente. </ul></td>
  </tr>
</table>
