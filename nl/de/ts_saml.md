---

copyright:
  years: 2017, 2018
lastupdated: "2018-06-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tip: .tip}

# Identitätsproviderkonfigurationen
{: #troubleshooting-idp}

Wenn bei der Konfiguration von Identitätsprovidern für {{site.data.keyword.appid_full}} Probleme auftreten, ziehen Sie die folgenden Verfahren zur Fehlerbehebung und zum Abrufen von Hilfe in Betracht.
{: shortdesc}


## Es gibt nach der Anmeldung keine Weiterleitung an die App
{: #signin-fail}

{: tsSymptoms}
Ein Benutzer meldet sich bei Ihrer Anwendung über die Anmeldeseite eines Identitätsproviders an. Entweder passiert nichts oder die Registrierung schlägt fehl.

{: tsCauses}
Die Anmeldung kann aus folgenden Gründen fehlschlagen:

* Die Weiterleitungs-URL wurde nicht ordnungsgemäß zur [Whitelist](identity-providers.html#redirect) hinzugefügt.
* Der Benutzer ist nicht berechtigt.
* Der Benutzer versuchte, sich mit falschen Berechtigungsnachweisen anzumelden.

{: tsResolve}
Damit eine Weiterleitung stattfindet, führen Sie folgende Schritte aus:

* Überprüfen Sie, dass Ihre Weiterleitungs-URL richtig ist. Sie muss exakt sein, damit die Weiterleitung funktioniert.
* Stellen Sie sicher, dass der Benutzer sich mit den korrekten Berechtigungsnachweisen anmeldet.
* Überprüfen Sie, dass die Benutzer in den Benutzereinstellungen des Identitätsproviders konfiguriert sind.


## Allgemeine Probleme bei der Arbeit mit SAML
{: #common-saml}

In der folgenden Tabelle finden Sie Erläuterungen und Lösungen für die meisten allgemeinen Probleme, die bei der Arbeit mit SAML auftreten können.

<table summary="Jede Tabellenzeile sollte von links nach rechts gelesen werden, wobei der Clusterstatus in der ersten Spalte und eine Beschreibung in der zweiten Spalte angegeben ist.">
  <thead>
    <th>Nachricht</th>
    <th>Beschreibung</th>
  </thead>
  <tbody>
    <tr>
      <td><code>Could not parse assertion xml.</code> (Es konnte kein Parsing für assertion xml durchgeführt werden.)</td>
      <td>Die Antwort von SAML war fehlerhaft.</td>
    </tr>
    <tr>
      <td><code>Invalid attribute without name. Contact your identity provider administrator.</code> (Ungültiges Attribut ohne Namen. Wenden Sie sich an den Administrator des Identitätsproviders.) </td>
      <td>Es gibt ein Attribut <code>&lt;saml:Attribute&gt;</code> ohne definierten Wert. Wenden Sie sich an den Administrator des Identitätsproviders. </td>
    </tr>
    <tr>
      <td><code>SAML response body must contain RelayState.</code> (SAML-Antworthauptteil muss RelayState enthalten.)</td>
      <td>Der Parameter RelayState war nicht im SAML-Antworthauptteil enthalten. {{site.data.keyword.appid_short_notm}} stellt den Parameter dem Identitätsprovider als Teil der Anforderung zur Verfügung und der exakte Parameter muss in der Antwort zurückgegeben werden. Falls der Parameter geändert wurde, können Sie den Administrator des Identitätsproviders kontaktieren. </td>
    </tr>
    <tr>
      <td><code>SAML Configuration must have certificates, entityID and signInUrl of the IdP.</code> (SAML-Konfiguration muss über Zertifikate, Entitäts-ID und signInUrl des Identitätsproviders (IdP) verfügen.)</td>
      <td>Der SAML-Identitätsprovider wurde nicht richtig konfiguriert. Überprüfen Sie die Konfiguration. Hilfe finden Sie in <a href="enterprise.html#configuring-saml" target="_blank">App für die Arbeit mit einem externen SAML-Identitätsprovider konfigurieren</a></td>
    </tr>
    <tr>
      <td><code>Error in assertion validation. SAML Assertion signature check failed! Certificate .. may be invalid.</code> (Fehler bei der Validierung der Zusicherung. Signaturprüfung der SAML-Zusicherung ist fehlgeschlagen! Zertifikat .. ist möglicherweise ungültig.)</td>
      <td>Eine gültige Signatur und ein gültiger Fingerabdruck muss in der Zusicherung enthalten sein. Die Signatur muss mithilfe des privaten Schlüssels erstellt werden, der dem Zertifikat zugeordnet ist, das in der SAML-Konfiguration bereitgestellt wird; es kann das sekundäre oder das primäre verwendet werden. <strong>Hinweis</strong>: {{site.data.keyword.appid_short_notm}} unterstützt keine verschlüsselte Zusicherung. Wenn Ihr Identitätsprovider dies mit Ihrer SAML-Zusicherung macht, inaktivieren Sie die Verschlüsselung.</td>
    </tr>
  </tbody>
</table>


## Es gibt keine Weiterleitung an den Identitätsprovider
{: #saml-redirect}

{: tsSymptoms}
Ein Benutzer versucht, sich bei Ihrer Anwendung anzumelden, aber die Anmeldeseite wird nicht angezeigt, wenn die Systemanfrage erfolgt.

{: tsCauses}
Der Identitätsprovider kann aus folgenden Gründen fehlschlagen:

* Die von Ihnen konfigurierte Weiterleitungs-URL ist falsch.
* Der Identitätsprovider erkennt die Authentifizierungsanforderung nicht.
* Der Identitätsprovider erwartet eine HTTP-POST-Bindung.
* Der Identitätsprovider erwartet eine signierte authnRequest.

{: tsResolve}
Sie können eine der folgenden Lösungen ausprobieren:

* Aktualisieren Sie Ihre Anmelde-URL. Diese URL wird als Teil der authnRequest gesendet und muss exakt sein.
* Stellen Sie sicher, dass Ihre {{site.data.keyword.appid_short_notm}}-Metadaten in den Einstellungen des Identitätsproviders korrekt definiert sind.
* Konfigurieren Sie Ihren Identitätsprovider so, dass er die authnRequest in der HTTP-Weiterleitung (HTTP-Redirect) akzeptiert.
* {{site.data.keyword.appid_short_notm}} unterstützt die Signierung von authnRequests nicht.

Falls keine dieser Lösungen Abhilfe bringt, liegt möglicherweise ein Verbindungsproblem vor.
{: tip}

## Ein Attribut zeigt den falschen Wert an
{: #saml-attribute}

{: tsSymptoms}
Ein Attributwert ist in einem Benutzerprofil vorhanden, er ist jedoch nicht mit dem korrekten Attribut verbunden.

{: tsCauses}
Das Benutzerprofilattribut ist nicht richtig zugeordnet.

{: tsResolve}
Ordnen Sie das Attribut in den Einstellungen Ihres Identitätsproviders zu. {{site.data.keyword.appid_short_notm}} erwartet die folgenden Attribute:
* `Name`
* `E-Mail`
* `Ländereinstellung`
* `Bild`


