---

copyright:
  years: 2017
lastupdated: "2017-06-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Token di identità e accesso
{: #access-and-identity}

{{site.data.keyword.appid_short}} utilizza due tipi di token: accesso e identità. I token sono creati come <a href="https://jwt.io/introduction/" target="_blank">JSON Web Tokens <img src="../../icons/launch-glyph.svg" alt="icona link esterno"></a>.
{:shortdesc}


## Token di accesso
{: #access-tokens}

Il token di accesso abilita la comunicazione con le [risorse di back-end](/docs/services/appid/protecting-resources.html) protette dai filtri di autorizzazione {{site.data.keyword.appid_short_notm}}. Il token è conforme alle specifiche JavaScript Object Signing and Encryption (JOSE) ed ha il seguente formato:

```
Intestazione: {
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
<caption> Tabella 1. Componenti del token di accesso spiegati </caption>
  <tr>
    <th> Componente </th>
    <th> Descrizione </th>
  </tr>
  <tr>
    <td> <i> typ </i> </td>
    <td> Il tipo di intestazione, specificato come "JOSE". </td>
  </tr>
  <tr>
    <td> <i> alg </i> </td>
    <td> L'algoritmo utilizzato, specificato come "RS256". </td>
  </tr>
  <tr>
    <td> <i> iss </i> </td>
    <td> Il server {{site.data.keyword.appid_short}} che ha emesso il token; specificato come una stringa o un URL. </td>
  </tr>
  <tr>
    <td> <i> sub </i> </td>
    <td> L'ID dell'utente per cui viene emesso il token. </td>
  </tr>
  <tr>
    <td> <i> aud </i> </td>
    <td> L'ID del client a cui è destinato il token. </td>
  </tr>
  <tr>
    <td> <i> exp </i> </td>
    <td> L'ora in cui scade la data/ora, specificata come ora di eliminazione. </td>
  </tr>
  <tr>
    <td> <i> iat </i> </td>
    <td> L'ora in cui viene emessa la data/ora, specificata come ora di eliminazione. </td>
  </tr>
  <tr>
    <td> <i> tenant </i> </td>
    <td> L'ID tenant per cui viene emesso il token. </td>
  </tr>
  <tr>
    <td> <i> amr </i> </td>
    <td> Il provider di identità utilizzato per l'autenticazione. Questa variabile può essere <i>appid_facebook</i> o <i>appid_google</i>. </td>
  </tr>
  <tr>
    <td> <i> scope </i> </td>
    <td> L'ambito per cui viene emesso il token. </td>
  </tr>
</table>


## Token di identità
{: #identity-tokens}

l token di identità contiene informazioni sull'utente, inclusi nome, e-mail, sesso, foto e posizione.

```
Intestazione: {
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
<caption> Tabella 2. Componenti del token di identità spiegati </caption>
  <tr>
    <th> Componente </th>
    <th> Descrizione </th>
  </tr>
  <tr>
    <td> <i> name </i> </td>
    <td> Il nome completo dell'utente come riportato dal provider di identità. Questo deve essere restituito. </td>
  </tr>
  <tr>
    <td> <i> email </i> </td>
    <td> L'email dell'utente come riportato dal provider di identità. Restituito solo quando disponibile. </td>
  </tr>
  <tr>
    <td> <i> gender </i> </td>
    <td> Il sesso dell'utente come riportato dal provider di identità, quando disponibile. </td>
  </tr>
  <tr>
    <td> <i> locale </i> </td>
    <td> La locale dell'utente come riportato dal provider di identità. </td>
  </tr>
  <tr>
    <td> <i> picture </i> </td>
    <td> L'URL a una foto dell'utente, se disponibile. </td>
  </tr>
  <tr>
    <td> <i> identities: </br> <ul><li> provider <li> id <li> amr </ul></i></td>
    <td> </br><ul><li> Il provider di identità utilizzato per l'autenticazione. Questa variabile può essere <code>appid_facebook</code>, <code>appid_google</code> o <code>appid_ibmid</code> e deve essere restituita. <li> Un ID utente univoco come riportato da un provider di identità. <li> Un oggetto JSON che deve essere restituito dal provider di identità. </ul></i></td>
  </tr>
  <tr>
    <td> <i> oauth_client: </br> <ul><li> type <li> name <li> software_id <li> software_version</ul></i> </td>
    <td> </br><ul><li> Il tipo di applicazione determinato durante la registrazione client. La variabile può essere <i>serverapp</i> o <i>mobileapp</i>. <li> Il nome del client come riportato durante la registrazione client. <li> L'ID del software come riportato durante la registrazione client. <li> La versione del software utilizzata durante la registrazione client. </ul></td>
  </tr>
</table>
