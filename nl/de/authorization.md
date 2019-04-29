---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

keywords: authentication, authorization, identity, app security, secure, access, tokens

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

# Zentrale Konzepte
{: #key-concepts}

Möchten Sie mehr über die Unterschiede zwischen Autorisierung und Authentifizierung erfahren? Kein Problem! Im Folgenden erhalten Sie Informationen zur Terminologie, zu den Prozessen und zu der Art und Weise, wie der Service Tokens verwendet.
{: shortdesc}


## Terminologie
{: #terms}

Diese Schlüsselbegriffe können Ihnen dabei helfen, die Aufgliederung des Autorisierungs- und Authentifizierungsprozesses durch den Service im Detail nachzuvollziehen.

<dl>
  <dt>OAuth 2</dt>
    <dd><a href="https://tools.ietf.org/html/rfc6749" target="_blank">OAuth 2 <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> ist ein Open-Standard-Protokoll, das für die Bereitstellung von App-Autorisierungsfunktionen verwendet wird.</dd>
  <dt>Open ID Connect (OIDC)</dt>
    <dd><p><a href="http://openid.net/developers/specs/" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> ist eine Authentifizierungsebene, die auf OAuth 2 aufbaut.</p>
    <p>Wenn Sie OIDC und {{site.data.keyword.appid_short_notm}} verwenden, sind Ihre Anwendungsberechtigungsnachweise beim Konfigurieren der OAuth-Endpunkte hilfreich. Wenn Sie das SDK verwenden, werden die Endpunkt-URLs automatisch erstellt. Sie können die URLs jedoch auch selbst unter Verwendung Ihrer Serviceberechtigungsnachweise erstellen.</p> <p>Die URL hat das folgende Format: {{site.data.keyword.appid_short_notm}}-Serviceendpunkt + "/oauth/v4" + /tenantID.</p>
    <p><pre class="codeblock">
    <code>{
      "clientId": "7eba72ef-b913-47b0-b3b6-54358bb69035",
      "tenantId": "8f5aa500-357e-443a-aab6-bf878f852b5a",
      "secret": "OWEzZGM4M2UtZjhlYS00MDI2LTkwNGItNDJmYzViMmU2YzIz",
      "name":testing",
      "oAuthServerUrl": "https://us-south.appid-oauth.cloud.ibm.com/oauth/v4/8f5aa500-357e-443a-aab6-bf878f852b5a",
      "profilesUrl": "https://us-south.appid.cloud.ibm.com",
      "discoveryEndpoint": "https://us-south.appid-oauth.cloud.ibm.com/oauth/v4/8f5aa500-357e-443a-aab6-bf878f852b5a/.well-known/openid-configuration"
    }</code></pre></p>
    <p>Im vorliegenden Beispiel lautet die URL <code>https://us-south.appid.cloud.ibm.com/oauth/v4/3x176051-a23x-40y4-9645-804943z660q0</code>. Anschließend fügen Sie den Endpunkt hinzu, an den Sie eine Anforderung stellen wollten. In der folgenden Tabelle sind verschiedene Beispiele für Endpunkte aufgeführt.</p>
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
        <td>User information</td>
        <td>{oauthServerUrl}/userinfo</td>
      </tr>
      <tr>
        <td>JWKS</td>
        <td>{oauthServerUrl}/publickeys</td>
      </tr>
    </table>
    <p><strong>Hinweis</strong>: Wenn Sie das SDK verwenden, werden die Endpunkt-URLs automatisch erstellt.</p></dd>
  <dt>Token</dt>
    <dd>Der Service verwendet drei verschiedene Arten von Token. Zugriffstokens stellen die Autorisierung dar und ermöglichen die Kommunikation mit [Back-End-Ressourcen](/docs/services/appid?topic=appid-backend), die durch Autorisierungsfilter geschützt sind, die von {{site.data.keyword.appid_short}} festgelegt werden. Identitätstokens stellen die Authentifizierung dar und enthalten Informationen zum Benutzer. Ein Aktualisierungstoken kann verwendet werden, um ein neues Zugriffstoken abzurufen, ohne den Benutzer erneut zu authentifizieren. Mithilfe von Aktualisierungstokens können Benutzer dafür sorgen, dass ihre Informationen von der Anwendung gespeichert werden und somit bei Bedarf verfügbar sind. Auf diese Weise bleiben die Benutzer angemeldet. Tokens werden unter <b>Identitätsprovider > Verwalten</b> im {{site.data.keyword.appid_short}}-Dashboard festgelegt. Weitere Informationen zu Tokens und dazu, wie sie in {{site.data.keyword.appid_short}} verwendet werden, finden Sie in [Tokens verwalten](/docs/services/appid?topic=appid-tokens#tokens).
  </dd>
  <dt>Berechtigungsheader</dt>
    <dd><p>{{site.data.keyword.appid_short}} entspricht den <a href="https://tools.ietf.org/html/rfc6750" target="blank">Trägertokenspezifikationen<img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> und verwendet eine Kombination aus Zugriffs- und Identitätstoken, die als HTTP-Berechtigungsheader gesendet werden. Der Berechtigungsheader enthält drei verschiedene Teile, die durch Leerzeichen getrennt sind. Die Tokens sind mit einer Base64-Codierung codiert. Das Identitätstoken ist optional.</br>
    Beispiel:</p>
    <pre><code>Authorization=Bearer {access_token} [{id_token}]
</code></pre></dd>
  <dt>API-Strategie</dt>
    <dd><p>Die API-Strategie erwartet Anforderungen, die einen Autorisierungsheader mit einem gültigen Zugriffstoken enthalten. Die Anforderung kann auch ein Identitätstoken enthalten, dies ist jedoch nicht erforderlich. Wenn ein Token ungültig oder abgelaufen ist, gibt die API-Strategie einen HTTP 401-Fehler zurück, der den folgenden HTTP-Header enthält:</p> <pre><code>Www-Authenticate=Bearer scope="{scope}" error="{error}"</code></pre>
    <p>Wenn die Anforderung ein gültiges Token zurückgibt, wird die Steuerung an die nächste Middleware übergeben und die Eigenschaft <code>appIdAuthorizationContext</code> wird in das Anforderungsobjekt eingefügt. Diese Eigenschaft enthält die ursprünglichen Zugriffs- und Identitätstokens sowie die entschlüsselten Nutzdaten als einfache JSON-Objekte.</dd>
  <dt>Web-App-Strategie</dt>
    <dd>Wenn die Web-App-Strategie nicht berechtigte Versuche, auf geschützte Ressourcen zuzugreifen, feststellt, wird der Benutzerbrowser automatisch zur Authentifizierungsseite weitergeleitet. Diese kann durch {{site.data.keyword.appid_short}} bereitgestellt werden. Nach der erfolgreichen Authentifizierung kehrt der Benutzer zur Callback-URL der Web-App zurück. Die Web-App-Strategie ruft Zugriffs- und Identitätstokens ab und speichert sie in einer HTTP-Sitzung unter <code>WebAppStrategy.AUTH_CONTEXT</code>. Der Benutzer kann entscheiden, ob die Zugriffs- und Identitätstokens in der App-Datenbank gespeichert werden sollen.</dd>
  <dt>Datentrennung und -verschlüsselung</dt>
    <dd><p>{{site.data.keyword.appid_short_notm}} speichert und verschlüsselt die Attribute von Benutzerprofilen. Als Multi-Tenant-Service besitzt jeder Tenant einen designierten Verschlüsselungsschlüssel. Die Benutzerdaten in jedem Tenant werden nur mit dem Schlüssel des Tenants verschlüsselt.</p>
    <p>{{site.data.keyword.appid_short_notm}} stellt sicher, dass die privaten Daten vor dem Speichern verschlüsselt werden.</p></dd>
  <dt>Weiterleitungs-URIs</dt>
    <dd><p>{{site.data.keyword.appid_short_notm}} verwendet eine Liste vollständig qualifizierter, genehmigter URIs, um Ihre Benutzer nach einer Interaktion mit Ihrer App weiterzuleiten. Nachdem sich ein Benutzer z. B. erfolgreich angemeldet hat, leitet {{site.data.keyword.appid_short_notm}} den Benutzer zur Homepage Ihrer App oder zu einer anderen Seite weiter, die von Ihnen angegeben wurde. Das Format Ihres URI kann sich abhängig von Ihrer Anwendung ändern. Weitere Informationen zu diesem Thema finden Sie in [Weiterleitungs-URIs hinzufügen](/docs/services/appid?topic=appid-managing-idp#add-redirect-uri).</p></dd>
  <dt>JSON Web Key Set (JWKS)</dt>
    <dd>Ein JWKS stellt eine Gruppe von Verschlüsselungsschlüsseln dar. {{site.data.keyword.appid_short_notm}} verwendet JWKS, um die Authentizität der Tokens zu überprüfen, die vom Service generiert werden. Durch Verwendung der Schlüssel-ID bei der Überprüfung der Signatur kann sichergestellt werden, dass das Token von einer vertrauenswürdigen Quelle ({{site.data.keyword.appid_short_notm}}) stammt und dass die Informationen im Token zu keiner Zeit geändert wurden.</dd>
</dl>

