---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}

# Berechtigung und Authentifizierung
{: #authorization}

Mit {{site.data.keyword.appid_full}} können Benutzer Token und Berechtigungsfilter nutzen, um den Schutz ihrer Apps sicherzustellen. Bevor ein Benutzer einer App Berechtigungen erteilen kann, muss ein Identitätsprovider dessen Identität authentifizieren.
{: shortdesc}


## Zentrale Konzepte
{: #key-concepts}

Diese Schlüsselbegriffe können Ihnen dabei helfen, die Aufgliederung des Berechtigungs- und Authentifizierungsprozesses durch den Service im Detail nachzuvollziehen.

<dl>
  <dt>OAuth 2</dt>
    <dd><a href="https://tools.ietf.org/html/rfc6749" target="_blank">OAuth 2 <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> ist ein Open-Standard-Protokoll, das für die Bereitstellung von App-Berechtigungsfunktionen verwendet wird.</dd>
  <dt>Open ID Connect (OIDC)</dt>
    <dd><p><a href="http://openid.net/developers/specs/" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> ist eine Authentifizierungsebene, die auf OAuth 2 aufbaut.</p>
    <p>Wenn Sie OIDC und {{site.data.keyword.appid_short_notm}} verwenden, sind Ihre Serviceberechtigungsnachweise beim Konfigurieren der OAUTH-Endpunkte hilfreich. Wenn Sie das SDK verwenden, werden die Endpunkt-URLs automatisch erstellt. Sie können die URLs jedoch auch selbst unter Verwendung Ihrer Serviceberechtigungsnachweise erstellen. Orientieren Sie sich beim Zusammenstellen der URL an dem folgenden Beispiel und Tabelleninhalt: </p>
    <pre class="codeblock">
    <code>{
      "version": 3,
      "clientId": "e8ac1132-5151-4d8a-934e-0141de8e2b34",
      "secret": "XYZ5ZYXzXYZtNyz5Yi00YzQ2LXYwMZctXyM5ODA4NjFhYxYZ",
      "tenantId": "3x176051-a23x-40y4-9645-804943z660q0",
      "oauthServerUrl": "https://appid-oauth.ng.bluemix.net/oauth/v3/3x176051-a23x-40y4-9645-804943z660q0",
      "profilesUrl": "https://appid-profiles.ng.bluemix.net/"
    }</code></pre>
    <table>
      <tr>
        <th>Endpunkt</th>
        <th>Format</th>
      </tr>
      <tr>
        <td>Authorization</td>
        <td>{oauthServerUrl}/authorization</td>
      </tr>
      <tr>
        <td>Token</td>
        <td>{oauthServerUrl}/token</td>
      </tr>
      <tr>
        <td>Userinfo</td>
        <td>{oauthServerUrl}/userinfo</td>
      </tr>
      <tr>
        <td>JWKS</td>
        <td>{oauthServerUrl}/publickeys</td>
      </tr>
    </table>
    <p><strong>Hinweis</strong>: Wenn Sie das SDK verwenden, werden die Endpunkt-URLs automatisch erstellt. </p></dd>
  <dt>Token</dt>
    <dd>Der Service verwendet drei verschiedene Arten von Token für die Authentifizierung. Zugriffstoken stellen die Berechtigung dar und ermöglichen die Kommunikation mit [Back-End-Ressourcen](/docs/services/appid/protecting-resources.html), die durch Berechtigungsfilter geschützt sind, die von {{site.data.keyword.appid_short}} festgelegt werden. Identitätstoken stellen die Authentifizierung dar und enthalten Informationen zum Benutzer. Ein Aktualisierungstoken stellt ein Zugriffstoken mit einer verlängerten Lebensdauer dar. Mithilfe von Aktualisierungstoken können Benutzer dafür sorgen, dass ihre Informationen von der Anwendung gespeichert werden und somit bei Bedarf verfügbar sind. Auf diese Weise bleiben die Benutzer angemeldet. </dd>
  <dt>Berechtigungsheader</dt>
    <dd><p>{{site.data.keyword.appid_short}} entspricht den <a href="https://tools.ietf.org/html/rfc6750" target="blank">Trägertokenpezifikationen<img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> und verwendet eine Kombination aus Zugriffs- und Identitätstoken, die als HTTP-Berechtigungsheader gesendet werden. Der Berechtigungsheader enthält drei verschiedene Teile, die durch Leerzeichen getrennt sind. Die Token sind mit einer Base64-Codierung codiert. Das Identitätstoken ist optional.</br>
    Beispiel:</p>
    <pre><code>Authorization=Bearer {access_token} [{id_token}]</pre></code></dd>
  <dt>API-Strategie</dt>
    <dd><p>Die API-Strategie erwartet Anforderungen, die einen Autorisierungsheader mit einem gültigen Zugriffstoken enthalten. Die Anforderung kann auch ein Identitätstoken enthalten, dies ist jedoch nicht erforderlich. Wenn ein Token ungültig oder abgelaufen ist, gibt die API-Strategie einen HTTP 401-Fehler zurück, der den folgenden HTTP-Header enthält:</p> <pre><code>Www-Authenticate=Bearer scope="{scope}" error="{error}"</code></pre>
    <p>Wenn die Anforderung ein gültiges Token zurückgibt, wird die Steuerung an die nächste Middleware übergeben und die Eigenschaft <code>appIdAuthorizationContext</code> wird in das Anforderungsobjekt eingefügt. Diese Eigenschaft enthält die ursprünglichen Zugriffs- und Identitätstoken sowie die decodierten Nutzdaten als einfache JSON-Objekte.</dd>
  <dt>Web-App-Strategie</dt>
    <dd>Wenn die Web-App-Strategie nicht berechtigte Versuche, auf geschützte Ressourcen zuzugreifen, feststellt, wird der Benutzerbrowser automatisch zur Authentifizierungsseite umgeleitet. Diese kann durch {{site.data.keyword.appid_short}} bereitgestellt werden. Nach der erfolgreichen Authentifizierung kehrt der Benutzer zur Callback-URL der Web-App zurück. Die Web-App-Strategie ruft Zugriffs- und Identitätstoken ab und speichert sie in einer HTTP-Sitzung unter <code>WebAppStrategy.AUTH_CONTEXT</code>. Der Benutzer kann entscheiden, ob die Zugriffs- und Identitätstoken in der App-Datenbank gespeichert werden sollen.</dd>
  <dt>Datentrennung und -verschlüsselung</dt>
    <dd><p>{{site.data.keyword.appid_short_notm}} speichert und verschlüsselt die Attribute von Benutzerprofilen. Als Multi-Tenant-Service besitzt jeder Tenant einen designierten Verschlüsselungsschlüssel. Die Benutzerdaten in jedem Tenant werden nur mit dem Schlüssel des Tenants verschlüsselt.</p>
    <p>{{site.data.keyword.appid_short_notm}} stellt sicher, dass die privaten Daten vor dem Speichern verschlüsselt werden.</p></dd>
</dl>

</br>

## Funktionsweise des Prozesses
{: #process}

Beim Codieren von Apps bildet die Sicherheit eine der zentralen Problemstellungen. Wie kann sichergestellt werden, dass nur Benutzer mit den korrekten Zugriffsberechtigungen Ihre App verwenden? Dafür müssen Sie einen Berechtigungsprozess implementieren. In den meisten Prozessen sind Autorisierung und Authentifizierung miteinander gekoppelt, was dazu führen kann, dass Änderungen an Ihren Sicherheitsrichtlinien und Identitätsprovidern kompliziert sind. Bei {{site.data.keyword.appid_short}} sind der Berechtigungsprozess und der Authentifizierung separate Prozesse.
{: shortdesc}

Wenn Sie Social Media-Identitätsprovider wie z. B. Facebook konfigurieren, wird der [Oauth2-Berechtigungserteilungsablauf](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html) verwendet, um das Anmeldewidget aufzurufen. Wenn Sie Cloud Directory als Identitätsprovider einsetzen, wird der [Ablauf für Kennwortberechtigungsnachweise von Ressourceneignern](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html) verwendet, um Zugriffs- und Identitätstoken bereitzustellen.

![Pfad für das Einrichten eines identifizierten Benutzers.](/images/authenticationtrail.png)

Wenn ein Benutzer sich für eine Anmeldung entscheidet, wird er zu einem identifizierten Benutzer. Der Identitätsprovider gibt Zugriffs- und Identitätstoken mit Informationen zum Benutzer an {{site.data.keyword.appid_short}} zurück. Der Service verwendet die bereitgestellten Token und stellt fest, ob ein Benutzer über die erforderlichen Berechtigungsnachweise für den Zugriff auf eine App verfügt. Wenn die Token validiert sind, autorisiert der Service den Benutzerzugriff. Die Authentifizierungsdaten sind dem Datensatz der Benutzer zugeordnet, nachdem diese autorisiert wurden. Von jedem Client aus, der mit derselben Identität authentifiziert wird, kann auf den Benutzerdatensatz und dessen Attribute zugegriffen werden.

### Progressive Authentifizierung

Mit {{site.data.keyword.appid_short_notm}} kann sich ein anonymer Benutzer entscheiden, ein identifizierter Benutzer zu werden.

Wie funktioniert das?

Wenn sich ein Benutzer entscheidet, sich nicht sofort anzumelden, wird er als anonymer Benutzer betrachtet. Ein Benutzer könnte beispielsweise sofort mit dem Hinzufügen von Artikeln zu einem Warenkorb beginnen, ohne dass er sich anmeldet. Für anonyme Benutzer erstellt {{site.data.keyword.appid_short_notm}} einen Ad-hoc-Benutzerdatensatz und ruft die OAuth-Anmelde-API auf, die Zugriffs- und Identitätstoken für den anonymen Zugriff zurückgibt. Mithilfe dieser Token kann die App im Benutzerdatensatz gespeicherte Attribute erstellen, lesen, aktualisieren und löschen.

![Pfad für das Einrichten eines identifizierten Benutzers, der zu Anfang ein anonymer Benutzer war.](/images/anon-authenticationtrail.png)

Wenn sich ein anonymer Benutzer anmeldet, wird sein Zugriffstoken an die Anmelde-API weitergeleitet. Der Service authentifiziert den Aufruf mit einem Identitätsprovider. Der Service verwendet das Zugriffstoken, um den anonymen Datensatz zu suchen, und ordnet ihm die Identität zu. Die neuen Zugriffs- und Identitätstoken enthalten die öffentlichen Informationen, die vom Identitätsprovider geteilt werden. Nachdem ein Benutzer identifiziert ist, wird sein anonymes Token ungültig. Der Benutzer kann jedoch weiterhin auf seine Attribute zugreifen, da dies mit dem neuen Token möglich ist.

Eine Identität kann nur dann einem anonymen Datensatz zugewiesen werden, wenn sie nicht bereits einem anderen Benutzer zugewiesen wurde.
{: tip}

Ist die Identität bereits einem anderen {{site.data.keyword.appid_short_notm}}-Benutzer zugewiesen, enthalten die Token Informationen zu diesem Benutzerdatensatz und ermöglichen den Zugriff auf die zugehörigen Attribute. Auf die Attribute des vorherigen anonymen Benutzers kann mit dem neuen Token nicht zugegriffen werden. Solange das Token noch nicht abgelaufen ist, kann auf die Informationen über das anonyme Zugriffstoken zugegriffen werden. Während des Entwicklungsprozesses kann ausgewählt werden, wie die anonymen Attribute mit dem bekannten Benutzer zusammengeführt werden sollen.
