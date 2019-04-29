---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

keywords: authentication, authorization, identity, app security, secure, custom, proprietary, 

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

# Angepasste Identität in Ihrer App verwenden
{: #custom-auth}

Wenn Sie sich authentifizieren, können Sie Ihren eigenen angepassten Identitätsprovider verwenden. Ihr Identitätsprovider kann jedem Authentifizierungsmechanismus entsprechen, der nicht speziell von {{site.data.keyword.appid_full}} unterstützt wird (einschließlich proprietärer oder traditioneller Provider).
{: shortdesc}

## Übersicht
{: #custom-auth-overview}

Wenn Sie einen eigenen Identitätsprovider verwenden, können Sie einen angepassten Authentifizierungsablauf erstellen, der Ihre eigenen Protokolle verwendet. Sie haben dann mehr Kontrolle, z. B. Informationen, die Sie gemeinsam nutzen möchten, oder Informationen, die gespeichert werden.
{: shortdesc}

Stellen Sie sicher, dass Sie [Ihren angepassten Provider konfigurieren](/docs/services/appid?topic=appid-custom-identity), bevor Sie ihn Ihrer Anwendung hinzufügen.
{: tip}

### Wann kann ich diesen Ablauf einsetzen?
{: #custom-auth-when}

Wenn {{site.data.keyword.appid_short_notm}} keine direkte Unterstützung für einen bestimmten Identitätsprovider bereitstellt, können Sie den angepassten Identitätsablauf verwenden, um das Authentifizierungsprotokoll mit dem vorhandenen Authentifizierungsablauf von {{site.data.keyword.appid_short_notm}} zu verbinden. Beispiel: Sie möchten GitHub oder LinkedIn verwenden, um Ihren Benutzern die Anmeldung zu ermöglichen. Sie können das vorhandene SDK des Identitätsproviders verwenden, um die Benutzerauthentifizierungsinformationen zu vereinfachen, bevor sie mit {{site.data.keyword.appid_short_notm}} gepackt und ausgetauscht werden.

Es gibt zahlreiche Szenarios, in denen ein anderer Authentifizierungsablauf erforderlich ist:

 - Proprietäre interne Identitätsprovider
 - Identitätsprovider anderer Anbieter
 - Komplexe Authentifizierungsabläufe, zu denen auch proprietäre Mehrfaktormechanismen gehören können

Gelegentlich verwendet ein traditioneller Provider sein eigenes Authentifizierungsprotokoll. Da der angepasste Identitätsablauf die Authentifizierung vollständig von der Autorisierung entkoppelt, können Sie jedes Authentifizierungsverfahren Ihrer Wahl anwenden und dann die resultierenden Authentifizierungsdaten für {{site.data.keyword.appid_short_notm}} bereitstellen. Dazu sind keine Benutzerberechtigungsnachweise erforderlich.

</br>

### Wie funktioniert dieser Ablauf in technischer Hinsicht?
{: #custom-auth-tech}

Der Workflow für die angepasste Identität basiert auf dem "JWT-Bearer"-Grant-Typ, der in Assertion Framework for OAuth 2.0 Authorization Grants [[RFC7521]](https://tools.ietf.org/html/rfc7523#section-2.1) definiert ist. Um Benutzerinformationen für {{site.data.keyword.appid_short_notm}}-Tokens auszutauschen, stellt Ihre Authentifizierungsarchitektur eine Vertrauensbeziehung mit {{site.data.keyword.appid_short_notm}} her und verwendet dafür ein asymmetrisches RSA-Schlüsselpaar. Sobald die Vertrauensbeziehung hergestellt ist, können Sie den "JWT-Bearer"-Grant-Typ verwenden, um verifizierte Benutzerinformationen in einem signierten JWT für {{site.data.keyword.appid_short_notm}}-Tokens auszutauschen.

### Wie sieht der Ablauf aus?
{: #custom-auth-flow}

Wie bei allen Authentifizierungsabläufen erfordert die angepasste Identität, dass die Anwendung in der Lage ist, eine Vertrauensbeziehung zu {{site.data.keyword.appid_short_notm}} herzustellen, um die Integrität der Benutzerinformationen des Identitätsproviders sicherzustellen. Die angepasste Identität verwendet ein asymmetrisches RSA-Paar aus öffentlichem und privatem Schlüssel, um die Vertrauensbeziehung aufzubauen. Abhängig von Ihren Architekturanforderungen unterstützt die angepasste Identität zwei Vertrauensmodelle, die sich nur in der Speicherposition und der Verwendung des privaten Schlüssels unterscheiden.

![Anforderungsablauf für die angepasste Authentifizierung](images/customauth.png)
Abbildung. Die Anforderungsabläufe für die angepasste Authentifizierung

<dl>
  <dt>1. Signierung durch Identitätsprovider</dt>
    <dd>Wie bei herkömmlichen OAuth 2.0-Abläufen erstellt das sicherste Vertrauensmodell eine Beziehung zwischen Ihrem Identitätsprovider und dem Autorisierungsserver (in diesem Fall {{site.data.keyword.appid_short_notm}} direkt). Bei diesem Modell ist Ihr Identitätsprovider für das Speichern des privaten Schlüssels und das Signieren der JWT-Zusicherungen verantwortlich. Wenn diese Zusicherungen an {{site.data.keyword.appid_short_notm}} übergeben werden, werden sie mit dem übereinstimmenden öffentlichen Schlüssel validiert. Dadurch wird sichergestellt, dass die Benutzerinformationen des Identitätsproviders während der Übertragung nicht unbefugt geändert wurden.</dd>
  <dt>2. Signierung durch Anwendung</dt>
    <dd>Alternativ kann Ihr Vertrauensmodell auf der Beziehung zwischen Ihrer App und {{site.data.keyword.appid_short_notm}} basieren. In diesem Workflow wird Ihr privater Schlüssel in Ihrer serverseitigen Anwendung gespeichert. Nach einer erfolgreichen Authentifizierung ist Ihre App für das Konvertieren der Antwort des Identitätsproviders in ein JWT und das Signieren mit dem privaten Schlüssel verantwortlich, bevor die App das Token an {{site.data.keyword.appid_short_notm}} sendet. Da dieser Identitätsprovider keine Beziehung zu {{site.data.keyword.appid_short_notm}} hat, wird durch diese Architektur ein schwächeres Vertrauensmodell erstellt. Auch wenn {{site.data.keyword.appid_short_notm}} den Informationen vertrauen kann, die von der serverseitigen Anwendung gesendet werden, kann nicht davon ausgegangen werden, dass es sich um die Daten handelt, die ursprünglich vom Identitätsprovider gesendet wurden.</dd>
</dl>


## JSON Web Token generieren
{: #generating-jwts}

Sie können Ihre überprüften Benutzerdaten in ein JWT mit angepasster Identität konvertieren, indem Sie ein <a href="https://tools.ietf.org/html/rfc7515" target="blank">JSON Web Token <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> generieren. Das Token muss mit dem privaten Schlüssel signiert werden, der mit dem vorkonfigurierten öffentlichen Schlüssel übereinstimmt. Eine Liste der Tokensignierbibliotheken finden Sie unter <a href="https://jwt.io/" target="blank">jwt.io <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>.
{: shortdesc}

### Beispiel für ein JWT-Format
{: #jwts-example}

Token-Header:
  ```
  {
  "alg": "RS256",
  "typ": "JOSE"
  }
  ```
  {: screen}

Tokennutzdaten:
  ```
  {
    // Erforderlich
    iss: String, // Muss auf Ihren Identitätsprovider verweisen
    aud: String, // Muss der URL-Name des OAuth-Servers sein
    exp: Int,    // Muss ein Wert mit kurzer Lebensdauer sein
    sub: String, // Mus eine eindeutige Benutzer-ID sein, die von Ihrem Identitätsprovider angegeben wird

    // Normalisierte Anforderungen (Claims) (optional)
    name: String
    email: String
    locale: String
    picture: String
    gender: String

    // Angepasste Bereiche (Scopes), die dem Zugriffstoken hinzugefügt werden (optional)
    scope="custom_scope1 custom_scope2"

    // Andere angepasste Claims (optional)
    role="admin"
  }
  ```
  {: screen}

  <table>
  <thead>
    <th colspan=2><img src="images/idea.png" alt="Symbol für weitere Informationen"/> JWS-Felder</th>
  </thead>
  <tbody>
    <tr>
      <td><code>iss</code></td>
      <td>Muss einen Verweis auf Ihren Identitätsprovider enthalten.</td>
    </tr>
    <tr>
      <td><code>aud</code></td>
      <td>Die URL des OAuth-Servers. Format: https://{region}.appid.cloud.ibm.com/oauth/v4/{tenantId}.</td>
    </tr>
    <tr>
      <td><code>exp</code></td>
      <td>Die Zeitdauer, für die das Token gültig ist. Aus Sicherheitsgründen sollte das Token eine kurze Lebensdauer haben und spezifisch sein.</td>
    </tr>
    <tr>
      <td><code>sub</code></td>
      <td>Die eindeutige Benutzer-ID, die vom Identitätsprovider bereitgestellt wird.</td>
    </tr>
    <tr>
      <td>Normalisierte Anforderungen (Claims)</td>
      <td>Alle [normalisierten Anforderungen](/docs/services/appid?topic=appid-tokens#tokens) (sog. Claims) werden in dem Identitätstoken bereitgestellt, das als Antwort auf diese Anforderung zurückgegeben wird. Weitere angepasste Claims können mithilfe des Endpunkts [`/userinfo` lokalisiert werden](/docs/services/appid?topic=appid-custom-attributes#custom-attributes).</td>
    </tr>
    <tr>
      <td>Bereich (Scope)</td>
      <td>Standardmäßig enthalten alle {{site.data.keyword.appid_short_notm}}-Tokens eine Gruppe voreingestellter Bereiche (Scopes). Sie können zusätzliche Bereiche anfordern, indem Sie einen der folgenden Schritte ausführen:<ul><li> Geben Sie den Bereich in dem Bereichsfeld des JWS-Tokens an.</li> <li>Geben Sie den Bereich über den 'url-form'-Bereichsparameter der Anforderung `/token` an.</li></ul></td>
    </tr>
  </tbody>
  </table>

## {{site.data.keyword.appid_short_notm}}-Tokens abrufen
{: #exchanging-jwts}

Um die Verbindung zwischen Ihrem angepassten Provider und {{site.data.keyword.appid_short_notm}} zu ermöglichen, müssen Sie über {{site.data.keyword.appid_short_notm}}-Tokens verfügen. Um Service-Tokens abzurufen, tauschen Sie Ihre verifizierten Benutzerinformationen mithilfe des Endpunkts [`/token` aus](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Authorization_Server_V4/token).
{: shortdesc}

  ```
  Post /token
  Content-Type: application/x-www-from-urlencoded
  grant_type=urn:ietf:params:oauth:grant-type:jwt-bearer
  assertion=<payload>
  scope="<space separated scope array>"
  ```
  {: codeblock}
  <table>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="Symbol für weitere Informationen"/> Erstellung anfordern</th>
    </thead>
    <tbody>
      <tr>
        <td>Content-type</td>
        <td><code>applications/x-www-from-urlencoded</code></td>
      </tr>
      <tr>
        <td>grant_type</td>
        <td><code>urn:ietf:params:oauth:grant-type:jwt-bearer</code></td>
      </tr>
      <tr>
        <td>assertion</td>
        <td>Eine JWS-Nutzdatenzeichenfolge.</td>
      </tr>
      <tr>
        <td>scope</td>
        <td>Eine Liste der angepassten Bereiche (durch Leerzeichen getrennt).</td>
      </tr>
    </tbody>
  </table>
