---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# Servicezugriff verwalten
{: #service-access-management}

Mit {{site.data.keyword.appid_full}} und {{site.data.keyword.Bluemix_notm}} können IAM-Kontoeigner (IAM, Identity and Access Management) den Benutzerzugriff in Ihrem Konto verwalten.
{: shortdesc}

Als Kontoeigner können Sie in Ihrem Konto Richtlinien festlegen, um unterschiedliche Zugriffsebenen für unterschiedliche Benutzer zu erstellen. Bestimmte Benutzer können zum Beispiel über **Lesezugriff** auf eine Instanz verfügen und über **Schreibzugriff** für eine andere Instanz. Sie können entscheiden, wer berechtigt ist, Instanzen von {{site.data.keyword.appid_short_notm}} zu erstellen, zu aktualisieren und zu löschen.

Weitere Informationen zu IAM finden Sie in [IAM-Zugriff](/docs/iam/users_roles.html).

## Benutzerrollen
{: #roles}

Der Bereich einer Zugriffsrichtlinie basiert auf einer zugeordneten Benutzerrolle.
{: shortdesc}

Richtlinien ermöglichen es, Zugriff auf verschiedenen Ebenen zu gewähren. Einige der Optionen umfassen.
<ul><ul>
  <li>Zugriff über alle Instanzen eines Service in Ihrem Konto</li>
  <li>Zugriff auf eine einzelne Serviceinstanz in Ihrem Konto</li>
  <li>Zugriff auf eine bestimmte Ressource innerhalb einer Instanz</li>
  <li>Zugriff auf alle für IAM aktivierten Services in Ihrem Konto</li>
</ul></ul>

Plattformmanagementrollen ermöglichen es Benutzern, Tasks mit Serviceressourcen auf Plattformebene auszuführen. Rollen können zum Beispiel zugeordnet werden, um zu bestimmen, wer IDs erstellen oder löschen kann und wer Instanzen an Apps binden kann. Die folgende Tabelle führt die Aktionen sowie die korrelierenden Plattformmanagementrollen im Detail auf.

<table>
  <tr>
    <th>Plattformrolle</th>
    <th>Berechtigungen</th>
    <th>Beispielaktionen</th>
  </tr>
  <tr>
    <td><i>Anzeigeberechtigter</i></td>
    <td>{{site.data.keyword.appid_short_notm}}-Instanzen anzeigen.</td>
    <td>Sie können Daten eines Cloud Directory-Benutzers oder die Konfiguration des Identitätsproviders ansehen.</td>
  </tr>
  <tr>
    <td><i>Editor</i></td>
    <td>{{site.data.keyword.appid_short_notm}}-Instanzen anzeigen und binden.</td>
    <td>Sie können Anwendungen an eine Instanz von {{site.data.keyword.appid_short_notm}} binden.</td>
  </tr>
  <tr>
    <td><i>Operator</i></td>
    <td>{{site.data.keyword.appid_short_notm}}-Instanzen erstellen, löschen, bearbeiten, aussetzen, wiederaufnehmen, anzeigen oder binden.</td>
    <td>Sie können eine {{site.data.keyword.appid_short_notm}}-Instanz im Katalog erstellen oder aus diesem löschen.</td>
  </tr>
  <tr>
    <td><i>Administrator</i></td>
    <td>Alle Managementaktionen für alle Services im Konto.</td>
    <td>Sie können alle Bedieneraktionen ausführen und haben die Möglichkeit anderen Benutzern Richtlinien zuzuordnen.</td>
  </tr>
</table>

</br>
</br>
Die folgende Tabelle führt die Aktionen detailliert auf, die zu Servicezugriffsrollen zugeordnet sind. Servicezugriffsrollen ermöglichen Benutzern den Zugriff auf {{site.data.keyword.appid_short_notm}} sowie den Aufruf der {{site.data.keyword.appid_short_notm}}-API.


<table>
  <tr>
    <th>Servicerolle</th>
    <th>Berechtigungen</th>
    <th>Beispielaktionen</th>
  </tr>
  <tr>
    <td><i>Leseberechtigter</i></td>
    <td>{{site.data.keyword.appid_short_notm}}-Instanzdaten anzeigen.</td>
    <td>Kann die Details der Serviceinstanz wie Benutzerdaten oder Identitätsproviderdaten anzeigen.</td>
  </tr>
  <tr>
    <td> <i>Leseberechtigter oder Manager</i></td>
    <td>{{site.data.keyword.appid_short_notm}}-Instanz anzeigen und ändern.</td>
    <td>Kann alle Aktionen eines Leseberechtigten ausführen und die Serviceinstanz bearbeiten, also zum Beispiel die Konfiguration des Identitätsproviders bearbeiten. </li></ul></td>
  </tr>
</table>

Weitere Informationen zur Zuordnung von Benutzerrollen in der Benutzerschnittstelle finden Sie in [IAM-Zugriff verwalten](/docs/iam/mngiam.html#iammanidaccser).


## {{site.data.keyword.appid_short_notm}}-Zugriffsrichtlinien
{: #access}

Jedem Benutzer, der auf den {{site.data.keyword.appid_short_notm}}-Service in Ihrem Konto zugreift, muss eine Zugriffsrichtlinie mit einer definierten IAM-Benutzerrolle zugeordnet worden sein. Diese Richtlinie bestimmt, welche Aktionen der Benutzer innerhalb des Kontexts des Service oder der von Ihnen ausgewählten Instanz ausführen kann.
{: shortdesc}

Die Aktionen werden vom {{site.data.keyword.Bluemix_notm}}-Service angepasst und als Operationen definiert, die im Service ausgeführt werden dürfen. Die Aktionen werden dann zu IAM-Benutzerrollen zugeordnet. Einige der ausgeführten Aktionen können mit dem Service '{{site.data.keyword.cloudaccesstrailshort}}' verfolgt werden. Die Zuordnung zwischen den Aktionen und den für {{site.data.keyword.appid_short_notm}} erforderlichen Berechtigungen können Sie der folgenden Tabelle entnehmen. 

<table>
  <tr>
    <th>Aktion</th>
    <th>Erläuterung</th>
    <th>Erforderliche Rolle</th>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-redirect-uris</code></td>
    <td>Zeigt die Weiterleitungs-URLs von post-authentication an. </td>
    <td>Leseberechtigter, Schreibberechtigter, Manager</td>
  </tr>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-redirect-uris</code></td>
    <td>Fügt die Weiterleitungs-URLs von post-authentication hinzu oder aktualisiert diese.</td>
    <td>Schreibberechtigter, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-idps</code></td>
    <td>Aktualisiert die Konfiguration Ihres Identitätsproviders.</td>
    <td>Schreibberechtigter, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-idps</code></td>
    <td>Zeigt die Konfiguration Ihres Identitätsproviders an.</td>
    <td>Leseberechtigter, Schreibberechtigter, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-recent-activities</code></td>
    <td>Zeigt alle aktuellen Authentifizierungsereignisse in einer Liste an.</td>
    <td>Leseberechtigter, Schreibberechtigter, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-ui-config</code></td>
    <td>Zeigt die Konfiguration des Anmeldewidgets wie beispielsweise Logo und Farben an.</td>
    <td>Leseberechtigter, Schreibberechtigter, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-ui-config</code></td>
    <td>Aktualisiert die Konfiguration des Anmeldewidgets.</td>
    <td>Schreibberechtigter, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-user-profile-config</code></td>
    <td>Zeigt die Konfiguration des Benutzerprofils an.</td>
    <td>Leseberechtigter, Schreibberechtigter, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-user-profile-config</code></td>
    <td>Ändert die Konfiguration des Benutzerprofils.</td>
    <td>Schreibberechtigter, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-cd-users</code></td>
    <td>Zeigt die Konfiguration des Benutzerprofils an.</td>
    <td>Leseberechtigter, Schreibberechtigter, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-add-cd-user</code></td>
    <td>Fügt neue Benutzer zum Cloudverzeichnis hinzu.</td>
    <td>Schreibberechtigter, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-cd-user</code></td>
    <td>Aktualisiert die Details eines Cloudverzeichnisbenutzers.</td>
    <td>Schreibberechtigter, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-delete-cd-user</code></td>
    <td>Löscht einen Benutzer aus dem Cloudverzeichnis.</td>
    <td>Schreibberechtigter, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-email-template</code></td>
    <td>Zeigt die E-Mail-Vorlagen des Cloudverzeichnisses an.</td>
    <td>Leseberechtigter, Schreibberechtigter, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-update-email-template</code></td>
    <td>Aktualisiert die E-Mail-Vorlage mit Ihrem eigenen Inhalt.</td>
    <td>Schreibberechtigter, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-delete-email-template</code></td>
    <td>Löscht eine E-Mail-Vorlage des Cloudverzeichnisses.</td>
    <td>Schreibberechtigter, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-saml-metadata</code></td>
    <td>Metadaten des SAML-Service-Providers (SP) in Cloud Directory</td>
    <td>Leseberechtigter, Schreibberechtigter, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-post-saml-logo</code></td>
    <td>Legt ein Bild im Anmeldewidget des SAML-Identitätsproviders fest oder aktualisiert es. </td>
    <td>Schreibberechtigter, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-send-email-cd</code></td>
    <td>Sendet auf Grundlage einer Vorlage eine E-Mail an einen Benutzer.</td>
    <td>Schreibberechtigter, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-sender-details-cd</code></td>
    <td>Zeigt die Absenderdetails für die Email an.</td>
    <td>Leseberechtigter, Schreibberechtigter, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-sender-details-cd</code></td>
    <td>Aktualisiert die Absenderdetails.</td>
    <td>Schreibberechtigter, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-revoke-refresh-token</code></td>
    <td>Widerruft ein Aktualisierungstoken eines Benutzers mit der zugehörigen Benutzer-ID. </td>
    <td>Schreibberechtigter, Manager</td>
  </tr>
</table>

## Änderungen an den {{site.data.keyword.appid_short_notm}}-Instanzen verfolgen
{: #tracking}

Sie können Konfigurationsaktivitäten in Ihrer {{site.data.keyword.appid_short_notm}}-Instanz mit dem Service '{{site.data.keyword.cloudaccesstrailshort}}' anzeigen, verwalten und überprüfen.
{: shortdesc}

Überwachen administrativer Aktivitäten:

1. Melden Sie sich bei Ihrem {{site.data.keyword.Bluemix_notm}}-Konto an.
2. Stellen Sie über den Katalog eine Instanz des {{site.data.keyword.cloudaccesstrailshort}}-Service in demselben Konto bereit, das auch für Ihre {{site.data.keyword.appid_short_notm}}-Instanz verwendet wird. 
3. Klicken Sie im {{site.data.keyword.cloudaccesstrailshort}}-Dashboard auf die Registerkarte **Verwalten**.
4. Nehmen Sie über die Dropdown-Liste die folgenden Konfigurationen vor, um nach Ereignissen zu suchen, die von {{site.data.keyword.appid_short_notm}} generiert werden. 
    * Wählen Sie für **Protokolle anzeigen** die Option **Kontoprotokolle** aus. 
    * Wählen Sie für **Durchsuchen** die Option **target.Management** aus. 
    * Geben Sie für **Filter** den Eintrag **appid** ein. 
5. Klicken Sie auf **Filtern**.


Die folgende Tabelle enthält eine Liste der Ereignisse, die an {{site.data.keyword.cloudaccesstrailshort}} gesendet werden. 

<table>
  <tr>
    <th>Aktion</th>
    <th>Beschreibung</th>
    <th>Position in der Benutzerschnittstelle</th>
  </tr>
  <tr>
    <td><code>read.recentActivity</code></td>
    <td>Vorherige Aktivität anzeigen </td>
    <td>Feld <strong>Aktivitätenprotokoll</strong> auf der Registerkarte <strong>Überblick</strong> </td>
  </tr>
  <tr>
    <td><code>read.idpConfig</code></td>
    <td>Konfiguration des Identitätsproviders anzeigen </td>
    <td>Registerkarte <strong>Identitätsprovider > Verwalten</strong> </td>
  </tr>
  <tr>
    <td><code>update.idpConfig</code></td>
    <td>Konfiguration des Identitätsproviders aktualisieren</td>
    <td>Registerkarte <strong>Identitätsprovider > Verwalten</strong> </td>
  </tr>
  <tr>
    <td><code>read.tokensConfig</code></td>
    <td>Konfiguration der Ablaufzeit der Token anzeigen</td>
    <td>Registerkarte <strong>Identitätsprovider > Ablaufzeit der Token</strong> </td>
  </tr>
  <tr>
    <td><code>read.isProfilesActive</code></td>
    <td>Speicherkonfiguration für Benutzerprofile anzeigen</td>
    <td>Feld <strong>Aktivitätenprotokoll</strong> auf der Registerkarte <strong>Überblick</strong> </td>
  </tr>
  <tr>
    <td><code>update.isProfilesActive</code></td>
    <td>Speicherkonfiguration für Benutzerprofile aktualisieren</td>
    <td>Registerkarte <strong>Profile</strong> </td>
  </tr>
  <tr>
    <td><code>read.themeColor</code></td>
    <td>Motivfarbe des Anmeldewidgettitels anzeigen</td>
    <td>Registerkarte <strong>Anpassung der Anmeldung</strong>  </td>
  </tr>
  <tr>
    <td><code>update.themeColor</code></td>
    <td>Motivfarbe des Anmeldewidgettitels aktualisieren</td>
    <td>Registerkarte <strong>Anpassung der Anmeldung</strong> </td>
  </tr>
  <tr>
    <td><code>read.media</code></td>
    <td>Bild im Anmeldewidget anzeigen</td>
    <td>Registerkarte <strong>Anpassung der Anmeldung</strong> </td>
  </tr>
  <tr>
    <td><code>update.media</code></td>
    <td>Bild im Anmeldewidget aktualisieren</td>
    <td>Registerkarte <strong>Anpassung der Anmeldung</strong> </td>
  </tr>
  <tr>
    <td><code>read.uiConfiguration</code></td>
    <td>Benutzerschnittstellenkonfiguration für Anmeldewidget inklusive Titelfarbe und Bild anzeigen</td>
    <td>Registerkarte <strong>Anpassung der Anmeldung</strong> </td>
  </tr>
  <tr>
    <td><code>read.uiLanguages</code></td>
    <td>Liste der unterstützten Sprachen anzeigen</td>
    <td>Anzeige über die API</td>
  </tr>
  <tr>
    <td><code>update.uiLanguages</code></td>
    <td>Von Ihrer App unterstützte Sprachen aktualisieren</td>
    <td>Aktualisierung über die API</td>
  </tr>
  <tr>
    <td><code>read.samlMetadata</code></td>
    <td>SAML-Metadaten von App ID anzeigen</td>
    <td>Registerkarte <strong>Identitätsprovider > SAML 2.0 Federation</strong></td>
  </tr>
  <tr>
    <td><code>read.cloudDirectoryUser</code></td>
    <td>Cloud Directory-Benutzer anzeigen</td>
    <td>Registerkarte <strong>Benutzer</strong> </td>
  </tr>
  <tr>
    <td><code>update.cloudDirectoryUser</code></td>
    <td>Cloud Directory-Benutzer aktualisieren</td>
    <td>Registerkarte <strong>Benutzer</strong> </td>
  </tr>
  <tr>
    <td><code>delete.cloudDirectoryUser</code></td>
    <td>Cloud Directory-Benutzer löschen</td>
    <td>Registerkarte <strong>Benutzer</strong> </td>
  </tr>
  <tr>
    <td><code>read.cloudDirectoryUsers</code></td>
    <td>Liste der Cloud Directory-Benutzer anzeigen</td>
    <td>Registerkarte <strong>Benutzer</strong> </td>
  </tr>
  <tr>
    <td><code>update.cloudDirectoryUsers</code></td>
    <td>Liste der Cloud Directory-Benutzer aktualisieren</td>
    <td>Registerkarte <strong>Benutzer</strong> </td>
  </tr>
  <tr>
    <td><code>delete.cloudDirectoryUsers</code></td>
    <td>Liste der Cloud Directory-Benutzer löschen</td>
    <td>Registerkarte <strong>Benutzer</strong> </td>
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
    <td>Benutzerbenachrichtigungen erneut senden </td>
    <td>Registerkarte <strong>Identitätsprovider > Cloud Directory > Einstellungen</strong></td>
  </tr>
  <tr>
    <td><code>update.selfForgotPassword</code></td>
    <td>Prozess für vergessenes Kennwort aktualisieren </td>
    <td>Registerkarte <strong>Identitätsprovider > Cloud Directory > Einstellungen</strong></td>
  </tr>
  <tr>
    <td><code>update.forgotPasswordResult</code></td>
    <td>Ergebnis der Bestätigung zu vergessenem Kennwort anzeigen</td>
    <td>Anzeige über die API</td>
  </tr>
  <tr>
    <td><code>update.selfSignUp</code></td>
    <td>Registrierungsprozess aktualisieren</td>
    <td>Registerkarte <strong>Identitätsprovider > Cloud Directory > Einstellungen</strong></td>
  </tr>
  <tr>
    <td><code>update.signUpResult</code></td>
    <td>Ergebnis der Registrierung anzeigen</td>
    <td>Anzeige über die API</td>
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
    <td>Registerkarte <strong>Anpassung der Anmeldung</strong> </td>
  </tr>
  <tr>
    <td><code>update.loginWidgetConfig</code></td>
    <td>Konfiguration des Anmeldewidgets aktualisieren</td>
    <td>Registerkarte <strong>Anpassung der Anmeldung</strong> </td>
  </tr>
</table>


Weitere Informationen zur Funktionsweise des Service finden Sie in der [Dokumentation zu {{site.data.keyword.cloudaccesstrailshort}}](/docs/services/cloud-activity-tracker/index.html). 

</br>
</br>

## Beispiel: Einem anderen Benutzer Zugriff auf eine Instanz von {{site.data.keyword.appid_short_notm}} gewähren
{: #example}

In diesem Szenario erstellte ein Administrator eine Instanz von {{site.data.keyword.appid_short_notm}} und muss einem anderen Teammitglied die Berechtigung zur Anzeige erteilen.
{: shortdesc}

Vorbereitungen:
* Installieren Sie die [{{site.data.keyword.Bluemix_notm}}-CLI](/docs/cli/index.html).

Der Administrator führt die folgenden Schritte aus, um die Zugriffsberechtigungen zu aktualisieren:

1. Melden Sie sich bei der {{site.data.keyword.Bluemix_notm}}-Konsole an.
2. Erteilen Sie dem Mitarbeiter die Berechtigung zum Anzeigen, indem Sie die Schritte ausführen, die in der [IAM-Dokumentation](/docs/iam/iamusermanage.html#iamusermanage) erläutert werden.
3. Navigieren Sie zur Registerkarte **Serviceberechtigungsnachweise** des {{site.data.keyword.appid_short_notm}}-Dashboards. Klicken Sie auf **Berechtigungsnachweise anzeigen** und kopieren Sie die **tentantID**.
4. Melden Sie sich an der {{site.data.keyword.Bluemix_notm}}-CLI in Ihrem Terminal an.
    ```
    bx login -a api.<region>.bluemix.net
    ```
    {: codeblock}
5. Rufen Sie ein IAM-Token ab und notieren Sie dieses.
    ```
    bx iam oauth-tokens
    ```
    {: codeblock}
6. Überprüfen Sie, dass die Teammitglieder keine Änderungen vornehmen können.
    ```
    curl -X PUT --header 'Content-Type: application/json' \
    --header 'Accept: application/json' \
    --header 'Authorization: <IAM token value>' \
    -d '{
     "isActive": false,
     "config": {
       "idpId": "appID",
       "secret": "appsecret"
     }
    }' \
    'https://appid-management.ng.bluemix.net/management/v4/<tenantId>/config/idps/facebook'
    ```
    {: codeblock}

    Das Ergebnis ist eine 403 Nachricht über fehlende Berechtigung.

Zur Anzeige der {{site.data.keyword.appid_short_notm}}-Konfigurationen über die CLI führt das Teammitglied folgende Schritte aus:

1. Melden Sie sich über die {{site.data.keyword.Bluemix_notm}}-CLI in Ihrem Terminal an.
    ```
    bx login -a api.<region>.bluemix.net
    ```
    {: codeblock}
2. Rufen Sie ein IAM-Token ab und notieren Sie dieses.
    ```
    bx iam oauth-tokens
    ```
    {: codeblock}
3. Zeigen Sie die Konfiguration des Identitätsproviders für Facebook mithilfe der cURL an.
    ```
    curl -X GET --header 'Accept: application/json' --header 'Authorization: <IAM token value>' \  'https://appid-management.ng.bluemix.net/management/v4/<tenantId>/config/idps/facebook'
    ```
    {: codeblock}
    Das Ergebnis ist eine 200 Nachricht, die die Identitätsproviderdaten enthält.
