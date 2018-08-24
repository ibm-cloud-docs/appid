---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}

# Unternehmensidentitätsprovider konfigurieren
{: #enterprise}

Falls Sie bereits über ein vorhandenes Benutzerrepository und eine zertifizierte Möglichkeit zur Authentifizierung von Benutzern bei Ihren internen Systemen verfügen, können Sie den {{site.data.keyword.appid_full}}-Service für die Verwendung eines Unternehmensidentitätsproviders konfigurieren.
{: shortdesc}

## Einführung in SAML
{: #saml}

SAML ist ein offener Standard für den Austausch von Authentifizierungs- und Autorisierungsdaten zwischen einem Identitätsprovider, der die Benutzeridentität bestätigt, und einem Service-Provider, der die Benutzeridentitätsinformationen verarbeitet.
{: shortdesc}

Funktionsweise

{{site.data.keyword.appid_short_notm}} funktioniert als ein Service-Provider und initiiert eine SSO-Anmeldung (Single Sign On) bei einem anderen Anbieter wie beispielsweise Active Directory Federation Services (Active Directory-Verbunddienste). Das <a href="http://saml.xml.org/saml-specifications" target="_blank">SAML-Protokoll <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> unterstützt unterschiedliche Profile und Bindeoptionen. {{site.data.keyword.appid_short_notm}} unterstützt das SSO-Profil des Web-Browsers mit HTTP-POST-Bindung. 

### SAML-Zusicherung und Anforderungen von Identitätstoken

Eine SAML-Zusicherung ist ein Paket mit Informationen, das mindestens eine Anweisung enthält. Die Zusicherung enthält die Berechtigungsentscheidung und möglicherweise Identitätsinformationen zum Benutzer.

Wenn ein Benutzer sich bei einem Identitätsprovider anmeldet, sendet dieser Provider eine Zusicherung an {{site.data.keyword.appid_short_notm}}. {{site.data.keyword.appid_short_notm}} leitet Benutzeridentitätsinformationen weiter, die in der SAML-Zusicherung als OIDC-Tokenanforderung an Ihre App zurückgegeben wurden. Das SAML-Attribut muss mit einer der folgenden OIDC-Anforderungen übereinstimmen, um zu Identitätstoken hinzugefügt zu werden.

Die folgenden Anforderungen können hinzugefügt werden:
* `Name`
* `E-Mail`
* `Ländereinstellung`
* `Bild`

Die übrigen SAML-Attributelemente, die keinem der Standardnamen entsprechen, werden ignoriert. Dabei ist zu beachten, dass nach einer Änderung von Werten auf der Providerseite die neuen Werte erst nach einer erneuten Anmeldung des Benutzers verfügbar sind. 

## App für die Arbeit mit einem externen SAML-Identitätsprovider konfigurieren
{: #configuring-saml}

Sie können den {{site.data.keyword.appid_short_notm}}-Service so konfigurieren, dass er den SAML-Identitätsprovider (SAML, Security Assertion Markup Language) verwendet.
{: shortdesc}

Eine Anleitung zur Verwendung eines bestimmten SAML-Identitätsproviders finden Sie in den Blogbeiträgen zum Einrichten von {{site.data.keyword.appid_short_notm}} mit [Ping One ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-ping-one/), [Azure Active Directory ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-azure-active-directory/) oder [Active Directory Federation Service ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-active-directory-federation-service/).
{: tip}

### Dem Identitätsprovider Metadaten zur Verfügung stellen

Sie müssen einem SAML-kompatiblen Identitätsprovider Informationen zur Verfügung stellen, um Ihre App zu konfigurieren. Die Informationen werden über eine Metadaten-XML-Datei ausgetauscht, die außerdem Konfigurationsdaten enthält, die für die Herstellung einer Vertrauensbeziehung erforderlich sind.

1. Legen Sie auf der Registerkarte **Verwalten** des {{site.data.keyword.appid_short_notm}}-Dashboards für **SAML 2.0** die Einstellung **Ein** fest. Klicken Sie anschließend auf **Bearbeiten**, um Ihre SAML-Einstellungen zu konfigurieren. 
2. Klicken Sie auf die Option, mit der Sie **SAML-Metadatendatei herunterladen** können. Ihr Identitätsprovider erwartet die folgenden Informationen von der Datei.
  <table>
    <tr>
      <th> Variable </th>
      <th> Beschreibung </th>
    </tr>
    <tr>
      <td><code>EntityID</code></td>
      <td>Die Entitäts-ID ermöglicht dem Identitätsprovider die Kenntnis darüber, dass {{site.data.keyword.appid_short_notm}} die SAML-Anforderung ausgegeben hat.</td>
    </tr>
    <tr>
      <td><code>Location URL</code></td>
      <td>Die URL des Standorts, den der Identitätsprovider an die SAML-Zusicherung sendet, nachdem ein Benutzer erfolgreich authentifiziert wurde.</td>
    </tr>
    <tr>
      <td><code>Binding</code></td>
      <td>Die Anweisungen dafür, wie der Identitätsprovider die SAML-Antwort senden soll.</td>
    </tr>
    <tr>
      <td><code>NameID Format</code></td>
      <td>Die Art und Weise, auf die der Identitätsprovider erfährt, welches ID-Format zum Senden im Betreff einer Zusicherung erforderlich ist. Die Art und Weise, auf die {{site.data.keyword.appid_short_notm}} Benutzer identifiziert.</td>
    </tr>
    <tr>
      <td><code>WantAssertionsSigned</code></td>
      <td>Die Art und Weise, auf die ein Identitätsprovider überprüft, ob er die Zusicherung signieren muss. Der Service erwartet, dass die Zusicherung signiert ist, unterstützt aber keine verschlüsselten Zusicherungen.</td>
    </tr>
  </table>

3. Stellen Sie Ihrem Identitätsprovider die Daten zur Verfügung. Falls Ihr Identitätsprovider das Hochladen der Metadatendatei unterstützt, können Sie dies tun. Falls er das Hochladen nicht unterstützt, konfigurieren Sie die Eigenschaften manuell. Nicht alle Identitätsprovider verwenden dieselben Eigenschaften, so dass es in Ordnung ist, wenn Sie nicht alle Eigenschaften verwenden.

Die Eigenschaftsnamen können je nach Identitätsprovider variieren.
{: tip}

### Das Bereitstellen von Metadaten für {{site.data.keyword.appid_short_notm}}

Sie müssen Daten vom Identitätsprovider abrufen und {{site.data.keyword.appid_short_notm}} zur Verfügung stellen.

1. Navigieren Sie zur Registerkarte **SAML 2.0** des {{site.data.keyword.appid_short_notm}}-Dashboards. Geben Sie die folgenden Metadaten, die Sie vom Identitätsprovider erhalten haben, im Abschnitt zum Thema **Metadaten vom SAML-Identitätsprovider (IdP) bereitstellen** ein.
  <table>
    <tr>
      <th> Variable </th>
      <th> Beschreibung </th>
    </tr>
    <tr>
      <td><code>Sign-in URL</code></td>
      <td>Die URL, an die der Benutzer zur Registrierung weitergeleitet wird. Diese URL ist bei Ihrem SAML-Identitätsprovider gehostet.</td>
    </tr>
    <tr>
      <td><code>Entity ID</code></td>
      <td>Die Entitäts-ID ist der globale eindeutige Name für einen SAML-Identitätsprovider.</td>
    </tr>
    <tr>
      <td><code>Signing certificate</code></td>
      <td>Das Signaturzertifikat wird von Ihrem SAML-Identitätsprovider ausgegeben. Es wird für die Registrierung und für die Überprüfung der SAML-Zusicherungen verwendet. Alle Provider sind unterschiedlich, möglicherweise können Sie das Signaturzertifikat von Ihrem Identitätsprovider herunterladen. Das Zertifikat muss das Format <code>.pem</code> aufweisen.</td>
    </tr>
  </table>

2. Optional: Stellen Sie ein **sekundäres Zertifikat** zur Verfügung, das verwendet wird, falls die Signaturvalidierung mit dem primären Zertifikat fehlschlägt. Falls der Signierschlüssel gleich bleibt, blockiert {{site.data.keyword.appid_short_notm}} die Authentifizierung für abgelaufene Zertifikate nicht.

3. Aktualisieren Sie den **Providernamen** und klicken Sie auf **Speichern**. Der Standardname ist SAML.


### Testen Sie Ihre Konfiguration

Sie können die Konfiguration zwischen Ihrem SAML-Identitätsprovider und {{site.data.keyword.appid_short_notm}} testen.

1. Stellen Sie sicher, dass Sie Ihre Konfiguration gespeichert haben.
2. Navigieren Sie zur Registerkarte **SAML 2.0** des {{site.data.keyword.appid_short_notm}}-Dashboards und klicken Sie auf **Testen**. Eine neue Registerkarte wird angezeigt.
3. Melden Sie sich als ein Benutzer an, den Ihr Identitätsprovider bereits authentifiziert hat.
4. Nachdem Sie das Formular ausgefüllt haben, werden Sie auf eine andere Seite weitergeleitet.
  * Erfolgreiche Authentifizierung: Die Verbindung zwischen {{site.data.keyword.appid_short_notm}} und dem Identitätsprovider funktioniert korrekt. Die Seite zeigt gültige [Zugriffs- und Identitätstoken](/docs/services/appid/authorization.html#key-concepts) an.
  * Fehlgeschlagene Authentifizierung: Die Verbindung ist unterbrochen. Die Seite zeigt die Fehler und die SAML-XML-Antwortdatei an.
