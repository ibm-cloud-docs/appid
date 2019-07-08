---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-01"

keywords: authentication, authorization, identity, app security, secure, application identity, app to app, access token, activity

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


# {{site.data.keyword.cloudaccesstrailshort}}-Ereignisse
{: #at-events}

Sie können vom Benutzer initiierte Aktivitäten in Ihrer {{site.data.keyword.appid_full}}-Serviceinstanz mit dem Service '{{site.data.keyword.cloudaccesstrailshort}}' anzeigen, verwalten und analysieren.
{: shortdesc}





Weitere Informationen zur Funktionsweise des Service finden Sie in den [Dokumenten zu {{site.data.keyword.cloudaccesstrailshort}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started#getting-started).






## Verwaltungsereignisse anzeigen
{: #at-monitor-admin}

Sie können Konfigurationsaktivitäten in Ihrer {{site.data.keyword.appid_short_notm}}-Instanz mit dem Service '{{site.data.keyword.at_short}}' anzeigen, verwalten und analysieren.
{: shortdesc}

Gehen Sie wie folgt vor, um Verwaltungsaktivitäten zu überwachen:

1. Melden Sie sich bei Ihrem {{site.data.keyword.cloud_notm}}-Konto an.
2. Stellen Sie über den Katalog eine Instanz des Service '{{site.data.keyword.cloudaccesstrailshort}}' in demselben Konto bereit, das auch für Ihre {{site.data.keyword.appid_short_notm}}-Instanz verwendet wird.
3. Klicken Sie im {{site.data.keyword.cloudaccesstrailshort}}-Dashboard auf die Registerkarte **Verwalten**.
4. Nehmen Sie über die Dropdown-Liste die folgenden Konfigurationen vor, um nach Ereignissen zu suchen, die von {{site.data.keyword.appid_short_notm}} generiert werden.
    * Wählen Sie für **Protokolle anzeigen** die Option **Kontoprotokolle** aus.
    * Wählen Sie für **Durchsuchen** die Option **target.Management** aus.
    * Geben Sie für **Filter** die Option `appid` ein.
5. Klicken Sie auf **Filtern**.

</br>

## Liste der Verwaltungsereignisse
{: #at-events-admin}

Die folgende Tabelle enthält eine Liste der Ereignisse, die an {{site.data.cloudaccesstrailshort}} gesendet werden.

<table>
  <tr>
    <th>Aktion</th>
    <th>Beschreibung</th>
    <th>Position in der Benutzerschnittstelle</th>
  </tr>
  <tr>
    <td><code>read.recentActivity</code></td>
    <td>Vorherige Aktivität anzeigen</td>
    <td>Feld <strong>Aktivitätenprotokoll</strong> auf der Registerkarte <strong>Überblick</strong></td>
  </tr>
  <tr>
    <td><code>read.idpConfig</code></td>
    <td>Konfiguration des Identitätsproviders anzeigen</td>
    <td>Registerkarte <strong>Identitätsprovider > Verwalten</strong></td>
  </tr>
  <tr>
    <td><code>update.idpConfig</code></td>
    <td>Konfiguration des Identitätsproviders aktualisieren</td>
    <td>Registerkarte <strong>Identitätsprovider > Verwalten</strong> (Aktualisierung)</td>
  </tr>
  <tr>
    <td><code>read.tokensConfig</code></td>
    <td>Konfiguration der Ablaufzeit des Token anzeigen</td>
    <td>Registerkarte <strong>Identitätsprovider > Ablaufzeit des Tokens</strong></td>
  </tr>
  <tr>
    <td><code>read.isProfilesActive</code></td>
    <td>Speicherkonfiguration für Benutzerprofile anzeigen</td>
    <td>Feld <strong>Aktivitätenprotokoll</strong> auf der Registerkarte <strong>Überblick</strong></td>
  </tr>
  <tr>
    <td><code>update.isProfilesActive</code></td>
    <td>Speicherkonfiguration für Benutzerprofile aktualisieren</td>
    <td>Registerkarte <strong>Profile</strong></td>
  </tr>
  <tr>
    <td><code>read.themeColor</code></td>
    <td>Motivfarbe des Anmeldewidgettitels anzeigen</td>
    <td>Registerkarte <strong>Anpassung der Anmeldung</strong></td>
  </tr>
  <tr>
    <td><code>update.themeColor</code></td>
    <td>Motivfarbe des Anmeldewidgettitels aktualisieren</td>
    <td>Registerkarte <strong>Anpassung der Anmeldung</strong> (Aktualisierung)</td>
  </tr>
  <tr>
    <td><code>read.media</code></td>
    <td>Bild im Anmeldewidget anzeigen</td>
    <td>Registerkarte <strong>Anpassung der Anmeldung</strong></td>
  </tr>
  <tr>
    <td><code>update.media</code></td>
    <td>Bild im Anmeldewidget aktualisieren</td>
    <td>Registerkarte <strong>Anpassung der Anmeldung</strong> (Aktualisierung)</td>
  </tr>
  <tr>
    <td><code>read.uiConfiguration</code></td>
    <td>Benutzerschnittstellenkonfiguration für Anmeldewidget inklusive Titelfarbe und Bild anzeigen</td>
    <td>Registerkarte <strong>Anpassung der Anmeldung</strong></td>
  </tr>
  <tr>
    <td><code>read.uiLanguages</code></td>
    <td>Liste der unterstützten Sprachen anzeigen</td>
    <td>Anzeige über die API (obligatorisch)</td>
  </tr>
  <tr>
    <td><code>update.uiLanguages</code></td>
    <td>Von Ihrer App unterstützte Sprachen aktualisieren</td>
    <td>Aktualisierung über die API (obligatorisch)</td>
  </tr>
  <tr>
    <td><code>read.samlMetadata</code></td>
    <td>SAML-Metadaten für {{site.data.keyword.appid_short_notm}} anzeigen</td>
    <td>Registerkarte <strong>Identitätsprovider > SAML 2.0 Federation</strong></td>
  </tr>
  <tr>
    <td><code>read.cloudDirectoryUser</code></td>
    <td>Cloud Directory-Benutzer anzeigen</td>
    <td>Registerkarte <strong>Benutzer</strong></td>
  </tr>
  <tr>
    <td><code>update.cloudDirectoryUser</code></td>
    <td>Cloud Directory-Benutzer aktualisieren</td>
    <td>Registerkarte <strong>Benutzer</strong> (Aktualisierung)</td>
  </tr>
  <tr>
    <td><code>delete.cloudDirectoryUser</code></td>
    <td>Cloud Directory-Benutzer löschen</td>
    <td>Registerkarte <strong>Benutzer</strong> (Löschung)</td>
  </tr>
  <tr>
    <td><code>read.cloudDirectoryUsers</code></td>
    <td>Liste der Cloud Directory-Benutzer anzeigen</td>
    <td>Registerkarte <strong>Benutzer</strong></td>
  </tr>
  <tr>
    <td><code>update.cloudDirectoryUsers</code></td>
    <td>Liste der Cloud Directory-Benutzer aktualisieren</td>
    <td>Registerkarte <strong>Benutzer</strong> (Aktualisierung)</td>
  </tr>
  <tr>
    <td><code>delete.cloudDirectoryUsers</code></td>
    <td>Liste der Cloud Directory-Benutzer löschen</td>
    <td>Registerkarte <strong>Benutzer</strong> (Löschung)</td>
  </tr>
  <tr>
    <td><code>read.emailTemplate</code></td>
    <td>E-Mail-Vorlage anzeigen</td>
    <td>Registerkarte <strong>Identitätsprovider > Cloud Directory > Vorlagen</strong></td>
  </tr>
  <tr>
    <td><code>update.emailTemplate</code></td>
    <td>E-Mail-Vorlage aktualisieren</td>
    <td>Registerkarte <strong>Identitätsprovider > Cloud Directory > Vorlagen</strong></td>
  </tr>
  <tr>
    <td><code>delete.emailTemplate</code></td>
    <td>E-Mail-Vorlage löschen, um auf die Standard-E-Mail zurückzusetzen</td>
    <td>Registerkarte <strong>Identitätsprovider > Cloud Directory > Vorlagen</strong></td>
  </tr>
  <tr>
    <td><code>read.senderDetails</code></td>
    <td>Absenderdetails anzeigen</td>
    <td>Registerkarte <strong>Identitätsprovider > Cloud Directory > Einstellungen</strong></td>
  </tr>
  <tr>
    <td><code>update.senderDetails</code></td>
    <td>Absenderdetails aktualisieren</td>
    <td>Registerkarte <strong>Identitätsprovider > Cloud Directory > Einstellungen</strong></td>
  </tr>
  <tr>
    <td><code>update.resendNotification</code></td>
    <td>Benutzerbenachrichtigungen erneut senden</td>
    <td>Registerkarte <strong>Identitätsprovider > Cloud Directory > Einstellungen</strong></td>
  </tr>
  <tr>
    <td><code>update.selfForgotPassword</code></td>
    <td>Prozess für vergessenes Kennwort aktualisieren</td>
    <td>Registerkarte <strong>Identitätsprovider > Cloud Directory > Einstellungen</strong></td>
  </tr>
  <tr>
    <td><code>update.forgotPasswordResult</code></td>
    <td>Ergebnis der Bestätigung zu vergessenem Kennwort anzeigen</td>
    <td>Anzeige über die API (obligatorisch)</td>
  </tr>
  <tr>
    <td><code>update.selfSignUp</code></td>
    <td>Registrierungsprozess aktualisieren</td>
    <td>Registerkarte <strong>Identitätsprovider > Cloud Directory > Einstellungen</strong></td>
  </tr>
  <tr>
    <td><code>update.signUpResult</code></td>
    <td>Ergebnis der Registrierung anzeigen</td>
    <td>Anzeige über die API (obligatorisch)</td>
  </tr>
  <tr>
    <td><code>read.action_url</code></td>
    <td>Angepasste URL, die beim Ausführen einer Aktion aufgerufen wird, anzeigen</td>
    <td>Registerkarte <strong>Identitätsprovider > Cloud Directory > Angepasste Landing-Pages</strong></td>
  </tr>
  <tr>
    <td><code>update.action_url</code></td>
    <td>Angepasste URL, die beim Ausführen einer Aktion aufgerufen wird, aktualisieren</td>
    <td>Registerkarte <strong>Identitätsprovider > Cloud Directory > Einstellungen</strong></td>
  </tr>
  <tr>
    <td><code>update.changePassword</code></td>
    <td>Benutzerkennwort für Cloud Directory ändern</td>
    <td>Registerkarte <strong>Identitätsprovider > Cloud Directory > Einstellungen</strong></td>
  </tr>
  <tr>
    <td><code>read.loginWidgetConfig</code></td>
    <td>Konfiguration des Anmeldewidgets anzeigen</td>
    <td>Registerkarte <strong>Anpassung der Anmeldung</strong></td>
  </tr>
  <tr>
    <td><code>update.loginWidgetConfig</code></td>
    <td>Konfiguration des Anmeldewidgets aktualisieren</td>
    <td>Registerkarte <strong>Anpassung der Anmeldung</strong> (Aktualisierung)</td>
  </tr>
</table>



