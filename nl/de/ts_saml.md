---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-10"

keywords: authentication, authorization, identity, app security, secure, development, idp, troubleshooting, redirected, validation

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
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}

# Identitätsproviderkonfigurationen
{: #troubleshooting-idp}

Wenn bei der Konfiguration von Identitätsprovidern für {{site.data.keyword.appid_full}} Probleme auftreten, ziehen Sie die folgenden Verfahren zur Fehlerbehebung und zum Abrufen von Hilfe in Betracht.
{: shortdesc}


## Ein Benutzer wird nach dem Anmelden nicht an den Identitätsprovider weitergeleitet
{: #ts-saml-redirect}

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


## Gängige SAML-Probleme
{: #ts-common-saml}

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
      <td><code>Invalid attribute without name. Contact your identity provider administrator.</code> (Ungültiges Attribut ohne Namen. Wenden Sie sich an den Administrator des Identitätsproviders.)</td>
      <td>Es gibt ein Attribut <code>&lt;saml:Attribute&gt;</code> ohne definierten Wert. Wenden Sie sich an den Administrator des Identitätsproviders.</td>
    </tr>
    <tr>
      <td><code>SAML response body must contain the RelayState parameter.</code> (SAML-Antworthauptteil muss RelayState-Parameter enthalten.)</td>
      <td>Der Parameter war nicht im SAML-Antworthauptteil enthalten. {{site.data.keyword.appid_short_notm}} stellt den Parameter dem Identitätsprovider als Teil der Anforderung zur Verfügung und der exakte Parameter muss in der Antwort zurückgegeben werden. Falls der Parameter geändert wurde, können Sie den Administrator des Identitätsproviders kontaktieren. </td>
    </tr>
    <tr>
      <td><code>SAML Configuration must have certificates, entityID and signInUrl of the IdP.</code> (SAML-Konfiguration muss über Zertifikate, Entitäts-ID und signInUrl des Identitätsproviders (IdP) verfügen.)</td>
      <td>Der SAML-Identitätsprovider wurde nicht <a href="/docs/services/appid?topic=appid-enterprise#enterprise" target="_blank">richtig konfiguriert</a>. Überprüfen Sie die Konfiguration.</td>
    </tr>
    <tr>
      <td><code>Error in assertion validation. SAML Assertion signature check failed! Certificate .. may be invalid.</code> (Fehler bei der Validierung der Zusicherung. Signaturprüfung der SAML-Zusicherung ist fehlgeschlagen! Zertifikat .. ist möglicherweise ungültig.)</td>
      <td>Eine gültige Signatur und ein gültiger Fingerabdruck muss in der Zusicherung enthalten sein. Die Signatur muss mithilfe des privaten Schlüssels erstellt werden, der dem Zertifikat zugeordnet ist, das in der SAML-Konfiguration bereitgestellt wird, es kann das sekundäre oder das primäre verwendet werden. <strong>Hinweis</strong>: {{site.data.keyword.appid_short_notm}} unterstützt keine verschlüsselte Zusicherung. Wenn Ihr Identitätsprovider Ihre SAML-Zusicherung verschlüsselt, inaktivieren Sie die Verschlüsselung.</td>
    </tr>
  </tbody>
</table>



## Gültigkeitsfehler bei SAML-Antwort
{: #ts-saml-response}

{{site.data.keyword.appid_short_notm}} stellt die folgenden Gültigkeitsanforderungen an Zusicherungen. Alle Attribute sind obligatorische SAML-XML-Antwortknoten, sofern nichts anderes angegeben ist.
{: shortdesc}


<table summary="Jede Tabellenzeile sollte von links nach rechts gelesen werden, wobei das Antwortelement in der ersten Spalte und eine Beschreibung in der zweiten Spalte angegeben ist.">
  <thead>
    <th>Antwortelement</th>
    <th>Beschreibung</th>
  </thead>
  <tbody>
    <tr>
      <td><code>samlp:Response</code></td>
      <td>Das Antwortelement muss in der Antwort-XML enthalten sein.</td>
    </tr>
    <tr>
      <td><code>SAML-Version</code></td>
      <td>{{site.data.keyword.appid_short_notm}} akzeptiert nur <code>SAML Version 2.0</code>.</td>
    </tr>
    <tr>
      <td><code>InResponseTo</code></td>
      <td>{{site.data.keyword.appid_short_notm}} prüft, ob das in der Zusicherung zurückgegebene Antwortelement <code>InResponseTo</code> mit der gespeicherten Anforderungs-ID aus der SAML-Anforderung übereinstimmt.</td>
    </tr>
    <tr>
      <td><code>saml:issuer</code></td>
      <td>Der in einer Zusicherung angegebene Aussteller muss mit dem Aussteller übereinstimmen, der in der {{site.data.keyword.appid_short_notm}}-Identitätsproviderkonfiguration angegeben ist.</td>
    </tr>
    <tr>
      <td><code>ds:Signature</code></td>
      <td>Eine gültige Signatur und ein gültiger Fingerabdruck muss in der Zusicherung enthalten sein. Die Signatur muss mithilfe des privaten Schlüssels erstellt werden, der dem Zertifikat zugeordnet ist, das in der SAML-Konfiguration bereitgestellt wurde. Der Fingerabdruck wird mithilfe der Angaben für <code>CanonicalizationMethod</code> und <code>Transforms</code> validiert. <strong>Hinweis</strong>: {{site.data.keyword.appid_short_notm}} prüft nicht, wann das Zertifikat abläuft. Für das Zertifikatsmanagement können Sie  [Certificate Manager](/docs/services/certificate-manager?topic=certificate-manager-getting-started#getting-started) verwenden.</td>
    </tr>
    <tr>
      <td><code>saml:subject</code></td>
      <td>Der Betreff oder die <code>name_id</code> der Zusicherung muss die Federation-E-Mail des Benutzers sein.</td>
    </tr>
    <tr>
      <td><code>saml:AttributeStatement</code></td>
      <td>Stellt sicher, dass bestimmte Attribute einem bestimmten authentifizierten Benutzer zugeordnet werden.</td>
    </tr>
    <tr>
      <td><code>saml:Conditions</code></td>
      <td><strong>Optional</strong>: Wenn eine Bedingungsanweisung in einer Zusicherung enthalten ist, muss sie auch eine gültige Zeitmarke enthalten. {{site.data.keyword.appid_short_notm}} berücksichtigt den Gültigkeitszeitraum, der in einer Zusicherung angegeben ist. Zur Prüfung sucht der Service nach den Einschränkungen <code>NotBefore</code> and <code>NotOnOrAfter</code>, die definiert und gültig sein müssen.</td>
    </tr>
  </tbody>
</table>

{{site.data.keyword.appid_short_notm}} unterstützt keine verschlüsselte Zusicherung. Wenn Ihr Identitätsprovider so konfiguriert ist, dass er Ihre Zusicherung verschlüsselt, müssen Sie die Funktion inaktivieren. Die Zusicherung muss unverschlüsselt sein.
{: tip}
