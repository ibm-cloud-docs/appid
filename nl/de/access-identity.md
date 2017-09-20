---

copyright:
  years: 2017
lastupdated: "2017-06-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Zugriffs- und Identitätstoken
{: #access-and-identity}

{{site.data.keyword.appid_short}} verwendet zwei Typen von Token: Zugriffs- und Identitätstoken. Die Token sind als <a href="https://jwt.io/introduction/" target="_blank">JSON-Web-Token <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> formatiert.
{:shortdesc}


## Zugriffstoken
{: #access-tokens}

Das Zugriffstoken ermöglicht die Kommunikation mit [Back-End-Ressourcen](/docs/services/appid/protecting-resources.html), die durch die {{site.data.keyword.appid_short_notm}}-Berechtigungsfilter geschützt sind. Das Token entspricht den JOSE-Spezifikationen (JOSE = JavaScript Object Signing and Encryption) und weist das folgende Format auf: 

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
<caption> Tabelle 1. Erklärungen für Komponenten der Zugriffstoken</caption>
  <tr>
    <th> Komponente</th>
    <th> Beschreibung</th>
  </tr>
  <tr>
    <td> <i> typ </i> </td>
    <td> Der Headertyp, angegeben ist "JOSE". </td>
  </tr>
  <tr>
    <td> <i> alg </i> </td>
    <td> Der verwendete Algorithmus, angegeben ist "RS256". </td>
  </tr>
  <tr>
    <td> <i> iss </i> </td>
    <td> Der {{site.data.keyword.appid_short}}-Server, von dem das Token ausgegeben wurde; wird als Zeichenfolge oder URL angegeben. </td>
  </tr>
  <tr>
    <td> <i> sub </i> </td>
    <td> Die ID des Benutzers, an den das Token ausgegeben wird. </td>
  </tr>
  <tr>
    <td> <i> aud </i> </td>
    <td> Die Client-ID, für die das Token vorgesehen ist. </td>
  </tr>
  <tr>
    <td> <i> exp </i> </td>
    <td> Der Zeitpunkt, an dem die Zeitmarke abläuft, angegeben in Epochenzeit. </td>
  </tr>
  <tr>
    <td> <i> iat </i> </td>
    <td> Der Zeitpunkt, an dem die Zeitmarke ausgegeben wird, angegeben in Epochenzeit. </td>
  </tr>
  <tr>
    <td> <i> tenant </i> </td>
    <td> Die Tenant-ID, für die das Token ausgegeben wird. </td>
  </tr>
  <tr>
    <td> <i> amr </i> </td>
    <td> Der Identitätsprovider, der für die Authentifizierung verwendet wird. Als Wert für diese Variable kann <i>appid_facebook</i> oder <i>appid_google</i> verwendet werden. </td>
  </tr>
  <tr>
    <td> <i> scope </i> </td>
    <td> Der Bereich, für den das Token ausgegeben wird. </td>
  </tr>
</table>


## Identitätstoken
{: #identity-tokens}

Das Identitätstoken enthält Informationen über den Benutzer, einschließlich Name, E-Mail-Adresse, Geschlecht, Foto und Ort.

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
<caption> Tabelle 2. Erklärungen für Komponenten der Identitätstoken</caption>
  <tr>
    <th> Komponente</th>
    <th> Beschreibung</th>
  </tr>
  <tr>
    <td> <i> name </i> </td>
    <td> Der vollständige Name des Benutzers, wie er vom Identitätsprovider bereitgestellt wird. Diese Angabe muss zurückgegeben werden. </td>
  </tr>
  <tr>
    <td> <i> email </i> </td>
    <td> Die E-Mail des Benutzers, wie sie vom Identitätsprovider bereitgestellt wird. Wird nur bei Verfügbarkeit zurückgegeben. </td>
  </tr>
  <tr>
    <td> <i> gender </i> </td>
    <td> Das Geschlecht des Benutzers, wie es vom Identitätsprovider bereitgestellt wird (sofern verfügbar). </td>
  </tr>
  <tr>
    <td> <i> locale </i> </td>
    <td> Die Ländereinstellung des Benutzers, wie sie vom Identitätsprovider bereitgestellt wird. </td>
  </tr>
  <tr>
    <td> <i> picture </i> </td>
    <td> Die URL zu einem Bild des Benutzers (sofern verfügbar). </td>
  </tr>
  <tr>
    <td> <i> identities: </br> <ul><li> provider <li> id <li> amr </ul></i></td>
    <td> </br><ul><li> Der Identitätsprovider, der für die Authentifizierung verwendet wird. Für diese Variable kann entweder <code>appid_facebook</code>, <code>appid_google</code> oder <code>appid_ibmid</code> angegeben werden; ein Wert für diese Variable muss zurückgegeben werden.
<li> Eine eindeutige Benutzer-ID, wie sie von einem Identitätsprovider bereitgestellt wird.
<li> Ein JSON-Objekt, das vom Identitätsprovider zurückgegeben werden muss. </ul></i></td>
  </tr>
  <tr>
    <td> <i> oauth_client: </br> <ul><li> type <li> name <li> software_id <li> software_version</ul></i> </td>
    <td> </br><ul><li> Der Typ der Anwendung, ermittelt während der Clientregistrierung. Die Variable kann <i>serverapp</i> oder <i>mobileapp</i> lauten.
<li> Der Clientname, wie er während der Clientregistrierung dokumentiert wurde.
<li> Die Software-ID, wie sie während der Clientregistrierung dokumentiert wurde.
<li> Die Version der Software, die während der Clientregistrierung verwendet wurde. </ul></td>
  </tr>
</table>
