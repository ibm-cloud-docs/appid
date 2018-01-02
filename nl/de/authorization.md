---

copyright:
  years: 2017
lastupdated: "2017-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


# Berechtigung und Authentifizierung
{: authorization}

Bei der Berechtigung handelt es sich um den Prozess, mit dem Sie Zugriff auf Ihre Apps erteilen. Der {{site.data.keyword.appid_short}}-Service verwendet Tokens, Filter und einen Header zur Authentifizierung von Benutzern.
{: shortdesc}


## OAuth-Identität
{: #oauth}

Wenn der Service die OAuth-Anmelde-API aufruft, verwendet {{site.data.keyword.appid_short_notm}} OAuth 2.0- und OpenID Connect-Protokolle (OIDC-Protokolle), um den Aufrufenden mithilfe eines ausgewählten Identitätsproviders zu berechtigen und zu authentifizieren. Nach der Authentifizierung wird die Identität einem {{site.data.keyword.appid_short_notm}}-Benutzerdatensatz zugeordnet. {{site.data.keyword.appid_short_notm}} gibt ein Zugriffstoken, mit dem auf die Benutzerattribute zugegriffen werden kann, sowie ein Identitätstoken zurück, das die Identitätsinformationen enthält, die vom Identitätsprovider bereitgestellt werden. Von jedem Client aus, der mit derselben Identität authentifiziert wird, kann auf denselben Benutzerdatensatz mit dessen Attributen zugreifen.

## Zugriffs- und Identitätstoken

{{site.data.keyword.appid_short}} verwendet zwei Typen von Token: Zugriffs- und Identitätstoken.
{:shortdesc}

**Hinweis**: Die Tokens sind als <a href="https://jwt.io/introduction/" target="_blank">JSON-Web-Tokens <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> formatiert.

### Zugriffstoken
{: #access-tokens}

Zugriffstokens ermöglichen die Kommunikation mit [Back-End-Ressourcen](/docs/services/appid/protecting-resources.html), die durch Berechtigungsfilter geschützt sind, die von App ID gesendet werden. Das Token entspricht den JOSE-Spezifikationen (JavaScript Object Signing and Encryption).

Beispieltoken:

```
Header: {
    "typ": "JOSE",
    "alg": "RS256",
}
Payload: {
    "iss": "appid-oauth.ng.bluemix.net",
    "exp": "1495562664",
    "aud": "a3b87400-f03b-4956-844e-a52103ef26ba",
    "amr": ["facebook"],
    "sub": "de6a17d2-693d-4a43-8ea2-2140afd56a22",
    "iat": "1495559064",
    "tenant": "9781974b-6a1c-46c3-aebf-32b7e9bbbaee",
    "scope": "appid_default appid_readprofile appid_readuserattr appid_writeuserattr",
}
```
{:screen}

<table>
<caption> Tabelle 1. Erklärungen für Komponenten der Zugriffstoken </caption>
  <tr>
    <th> Komponente </th>
    <th> Beschreibung </th>
  </tr>
  <tr>
    <td><i> typ </i></td>
    <td> Der Headertyp, angegeben ist "JOSE". </td>
  </tr>
  <tr>
    <td><i> alg </i></td>
    <td> Der verwendete Algorithmus, angegeben ist "RS256". </td>
  </tr>
  <tr>
    <td><i> iss </i></td>
    <td> Der {{site.data.keyword.appid_short}}-Server, von dem das Token ausgegeben wurde; wird als Zeichenfolge oder URL angegeben. </td>
  </tr>
  <tr>
    <td><i> sub </i></td>
    <td> Die ID des Benutzers, an den das Token ausgegeben wird. </td>
  </tr>
  <tr>
    <td><i> aud </i></td>
    <td> Die Client-ID, für die das Token vorgesehen ist. </td>
  </tr>
  <tr>
    <td><i> exp </i></td>
    <td> Der Zeitpunkt, an dem die Zeitmarke abläuft, angegeben in Epochenzeit. </td>
  </tr>
  <tr>
    <td><i> iat </i></td>
    <td> Der Zeitpunkt, an dem die Zeitmarke ausgegeben wird, angegeben in Epochenzeit. </td>
  </tr>
  <tr>
    <td><i> tenant </i></td>
    <td> Die eindeutige Benutzer-ID, die mit dem Token ausgegeben wird. </td>
  </tr>
  <tr>
    <td><i> amr </i></td>
    <td> Der Identitätsprovider, der für die Authentifizierung verwendet wird. Als Wert für diese Variable kann <i>appid_facebook</i>,  <i>appid_google</i> oder <i>cloud_directory</i> verwendet werden. </td>
  </tr>
  <tr>
    <td><i> scope </i></td>
    <td> Der Bereich, für den das Token ausgegeben wird. </td>
  </tr>
</table>


### Identitätstokens
{: #identity-tokens}

Ein Identitätstoken enthält Informationen über den Benutzer. Es kann Angaben zum Namen des Benutzers, zur E-Mail-Adresse, zum Geschlecht und zum Standort enthalten. Ein Token kann darüber hinaus eine URL für ein Bild des Benutzers zurückgeben.

Beispieltoken:

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
        "id": "377440159275659"
    ],
    "amr": ["facebook"],
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
<caption> Tabelle 2. Erklärungen für Komponenten der Identitätstoken </caption>
  <tr>
    <th> Komponente </th>
    <th> Beschreibung </th>
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
    <td> <i> identities: </br> <ul><li> provider <li> id </ul></i></td>
    <td> </br><ul><li> Der Identitätsprovider, der für die Authentifizierung verwendet wird. Für diese Variable kann entweder <code>appid_facebook</code>, <code>appid_google</code> oder <code>cloud_directory</code> angegeben werden;  diese Variable muss zurückgegeben werden. <li> Eine eindeutige Benutzer-ID, wie sie von einem Identitätsprovider bereitgestellt wird. <li> Ein JSON-Objekt, das vom Identitätsprovider zurückgegeben werden muss. </ul></li></td>
  </tr>
  <tr>
    <td> <i> oauth_client: </br> <ul><li> type </br><li> name <li> software_id <li> software_version<li> device_id <li>device_model<li>device_os<li>device_os_version </ul></i> </td>
    <td> </br><ul><li> Der Typ der App, der während der Clientregistrierung bestimmt wird. Die Variable kann <em>serverapp</em> oder <em>mobileapp</em> lauten. <li> Der Clientname, wie er während der Clientregistrierung dokumentiert wurde. <li> Die Software-ID, wie sie während der Clientregistrierung dokumentiert wurde. <li> Die Version der Software, die während der Clientregistrierung verwendet wurde. <li> Die Geräte-ID des mobilen Clients. <li> Das Modell des mobilen Clients. <li> Das Betriebssystem des mobilen Clientgeräts. <li> Die Betriebssystemversion des mobilen Clientgeräts. </ul></td>
  </tr>
</table>

## Header
{: #auth-header}

Ein Berechtigungsheader besteht aus der Kombination der zurückgegebenen Tokens. Für {{site.data.keyword.appid_short}} besteht der Berechtigungsheader aus drei verschiedenen Tokens, die durch Leerzeichen getrennt sind: Träger-, Zugriffs- und Identitätstoken. Träger- und Zugriffstoken sind erforderlich, um den Zugriff auf Ihre Apps zu erteilen. Ein Identitätstoken ist optional und wird in erster Linie dazu vewendet, Informationen zu den Nutzern Ihrer App zu speichern.

Beispiel für eine Headerstruktur:

```
Authorization=Bearer {access_token} [{id_token}]
```
{: screen}


## Filter
{: #auth-filter}

Das {{site.data.keyword.appid_short}}-Server-SDK bietet Strategien zum Schutz von zwei Arten von Ressourcen an: APIs und Webanwendungen.
{:shortdesc}

Die API-Schutzstrategie gibt eine HTTP 401-Antwort mit einer Liste von Geltungsbereichen zurück, um die Autorisierung für einen nicht authentifizierten Client anzufordern. Die Schutzstrategie der Web-App gibt eine HTTP 302-Umleitung zurück. Die Umleitung sendet je nach Konfiguration einen nicht authentifizierten Client zur Anmeldeseite, die vom {{site.data.keyword.appid_short_notm}}-Service gehostet wird, oder direkt zur Anmeldeseite des Identitätsproviders.



### API-Strategie
{: #api}

Die API-Strategie erwartet Anforderungen, die einen Autorisierungsheader mit einem gültigen Zugriffstoken enthalten. Die Antwort kann auch ein Identitätstoken enthalten, dies ist jedoch nicht erforderlich.

Wenn ein Token ungültig oder abgelaufen ist, gibt die API-Strategie einen HTTP 401-Fehler zurück, der die folgende Information enthält: Www-Authenticate=Bearer scope="{scope}" error="{error}". Die `error`-Komponente ist optional.

Wenn die Anforderung ein gültiges Token zurückgibt, wird die Steuerung an die nächste Middleware übergeben und die Eigenschaft `appIdAuthorizationContext` wird in das Anforderungsobjekt eingefügt. Diese Eigenschaft enthält die ursprünglichen Zugriffs- und Identitätstoken sowie die decodierten Nutzdaten als einfache JSON-Objekte.


### Web-App-Strategie
{: #web}

Wenn die Web-App-Strategieklasse nicht authentifizierte Versuche, auf geschützte Ressourcen zuzugreifen, aufdeckt, wird der Benutzerbrowser zur Authentifizierungsseite automatisch umgeleitet. Nach der erfolgreichen Authentifizierung kehrt der Benutzer zur Callback-URL der Web-App zurück. Der Service nutzt die Web-App-Strategieklasse, um die Zugriffs- und Identitätstoken anzufordern. Nach Erhalt dieser Token werden diese von der Web-App-Strategieklasse in einer HTTP-Sitzung unter `WebAppStrategy.AUTH_CONTEXT` gespeichert. Der Benutzer kann entscheiden, ob die Zugriffs- und Identitätstoken in der App-Datenbank gespeichert werden sollen.


## Progressive Authentifizierung
{: #oauth}

{{site.data.keyword.appid_short_notm}} verwendet OAuth 2.0- und OIDC-Protokolle für die Benutzerberechtigung und -authentifizierung. Nach der Authentifizierung wird die Identität einem Benutzerdatensatz zugeordnet. Der Service gibt ein Zugriffstoken für den Zugriff auf die Attribute des Benutzers sowie ein Identitätstoken mit den vom Identitätsprovider bereitgestellten Informationen zum Benutzer zurück. Von jedem Client aus, der mit derselben Identität authentifiziert wird, kann auf den Benutzerdatensatz und dessen Attribute zugegriffen werden. 

Wie ist die Vorgehensweise, wenn die Anmeldung optional sein soll? {{site.data.keyword.appid_short_notm}} verwendet die sogenannte progressive Authentifizierung, um [Benutzerprofile](/docs/services/appid/user-profile.html) zu erstellen, auch wenn diese anonym sind. Sie können diese Informationen dann an ein bekanntes Benutzerprofil übertragen, nachdem sich ein Benutzer angemeldet hat.

![Darstellung des Pfads für das Einrichten eines identifizierten Benutzers.](/images/authenticationtrail.png)

Abbildung 2. Darstellung des Pfads für das Einrichten eines identifizierten Benutzers

Wenn ein Benutzer anonym bleiben möchte, erstellt {{site.data.keyword.appid_short_notm}} einen Ad-hoc-Benutzerdatensatz und ruft die OAuth-Anmelde-API auf, die anonyme Zugriffs- und Identitätstokens zurückgibt. Mithilfe dieser Tokens kann die App im Benutzerdatensatz gespeicherte Attribute erstellen, lesen, aktualisieren und löschen. Ein Benutzer könnte beispielsweise sofort mit dem Hinzufügen von Artikeln zu einem Warenkorb beginnen, ohne dass er sich bei einer App anmelden muss.


Wenn ein Benutzer sich für eine Anmeldung bei einer App entscheidet, wird er ein identifizierter Benutzer. Informationen zu diesem Benutzer werden vom Identitätsprovider abgerufen, den er für die Anmeldung ausgewählt hat. Sie erhalten Zugriffs- und Identitätstokens mit Informationen zum Benutzer.

Ein anonymer Benutzer kann sich entscheiden, ein identifizierter Benutzer zu werden. Die Vorgehensweise ist im Folgenden beschrieben.

Das Token für den anonymen Zugriff wird an die Anmelde-API übergeben. Der Service authentifiziert den Aufruf mit einem Identitätsprovider. Der Service verwendet das Zugriffstoken, um den anonymen Datensatz zu suchen, und ordnet ihm die Identität zu. Die neuen Zugriffsidentitätstokens enthalten die öffentlichen Informationen, die vom Identitätsprovider geteilt werden. Nachdem ein Benutzer identifiziert ist, werden seine anonymen Tokens ungültig. Der Benutzer kann jedoch weiterhin auf seine Attribute zugreifen, da dies mit dem neuen Token möglich ist.

**Hinweis**: Eine Identität kann nur dann einem anonymen Datensatz zugewiesen werden, wenn sie nicht bereits einem anderen Benutzer zugewiesen wurde. Ist die Identität bereits einem anderen {{site.data.keyword.appid_short_notm}}-Benutzer zugewiesen, enthalten die Tokens Informationen zu diesem Benutzerdatensatz und ermöglichen den Zugriff auf die zugehörigen Attribute. Auf die Attribute des vorherigen anonymen Benutzers kann mit dem neuen Token nicht zugegriffen werden. Solange das Token noch nicht abgelaufen ist, kann auf die Informationen über das anonyme Zugriffstoken zugegriffen werden. Während des Entwicklungsprozesses kann ausgewählt werden, wie die anonymen Attribute mit dem bekannten Benutzer zusammengeführt werden sollen.
