---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-09"

keywords: Authentication, authorization, identity, app security, secure, access, platform, management, permissions

subcollection: appid

---

{:external: target="_blank" .external}
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


# Servicezugriff verwalten
{: #service-access-management}

Mit {{site.data.keyword.appid_full}} und {{site.data.keyword.cloud_notm}} können IAM-Kontoeigner (IAM, Identity and Access Management) den Benutzerzugriff in Ihrem Konto verwalten.
{: shortdesc}

Als Kontoeigner können Sie in Ihrem Konto Richtlinien festlegen, um unterschiedliche Zugriffsebenen für unterschiedliche Benutzer zu erstellen. Bestimmte Benutzer können zum Beispiel über **Lesezugriff** auf eine Instanz verfügen und über **Schreibzugriff** für eine andere Instanz. Sie können entscheiden, wer berechtigt ist, Instanzen von {{site.data.keyword.appid_short_notm}} zu erstellen, zu aktualisieren und zu löschen.

Weitere Informationen zu IAM finden Sie in [IAM-Zugriff](/docs/iam?topic=iam-userroles).

## Benutzerrollen
{: #iam-roles}

Der Bereich einer Zugriffsrichtlinie basiert auf einer zugeordneten Benutzerrolle.
{: shortdesc}

Richtlinien ermöglichen es, Zugriff auf verschiedenen Ebenen zu gewähren. Einige der Optionen umfassen.
<ul><ul>
  <li>Zugriff über alle Instanzen eines Service in Ihrem Konto</li>
  <li>Zugriff auf eine einzelne Serviceinstanz in Ihrem Konto</li>
  <li>Zugriff auf eine bestimmte Ressource innerhalb einer Instanz</li>
  <li>Zugriff auf alle für IAM aktivierten Services in Ihrem Konto</li>
</ul></ul>

### Plattformrollen
{: #iam-platform-roles}

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

### Servicezugriffsrollen
{: #iam-service-roles}
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
    <td><i>Leseberechtigter oder Manager</i></td>
    <td>{{site.data.keyword.appid_short_notm}}-Instanz anzeigen und ändern.</td>
    <td>Kann alle Aktionen eines Leseberechtigten ausführen und die Serviceinstanz bearbeiten, also zum Beispiel die Konfiguration des Identitätsproviders bearbeiten. </li></ul></td>
  </tr>
</table>

Weitere Informationen zur Zuordnung von Benutzerrollen in der Benutzerschnittstelle finden Sie in [IAM-Zugriff verwalten](/docs/iam?topic=iam-iammanidaccser#iammanidaccser).


## {{site.data.keyword.appid_short_notm}}-Zugriffsrichtlinien
{: #iam-access}

Jedem Benutzer, der auf den {{site.data.keyword.appid_short_notm}}-Service in Ihrem Konto zugreift, muss eine Zugriffsrichtlinie mit einer definierten IAM-Benutzerrolle zugeordnet worden sein. Diese Richtlinie bestimmt, welche Aktionen der Benutzer innerhalb des Kontexts des Service oder der von Ihnen ausgewählten Instanz ausführen kann.
{: shortdesc}

Die Aktionen werden vom {{site.data.keyword.cloud_notm}}-Service angepasst und als Operationen definiert, die im Service ausgeführt werden dürfen. Die Aktionen werden dann zu IAM-Benutzerrollen zugeordnet. Einige der ausgeführten Aktionen können mit dem Service '{{site.data.keyword.cloudaccesstrailshort}}' verfolgt werden. Die Zuordnung zwischen den Aktionen und den für {{site.data.keyword.appid_short_notm}} erforderlichen Berechtigungen können Sie der folgenden Tabelle entnehmen.

<table>
  <tr>
    <th>Aktion</th>
    <th>Erläuterung</th>
    <th>Erforderliche Rolle</th>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-redirect-uris</code></td>
    <td>Zeigt die Weiterleitungs-URLs von post-authentication an.</td>
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
    <td>Legt ein Bild im Anmeldewidget des SAML-Identitätsproviders fest oder aktualisiert es.</td>
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
    <td>Widerruft ein Aktualisierungstoken eines Benutzers mit der zugehörigen Benutzer-ID.</td>
    <td>Schreibberechtigter, Manager</td>
  </tr>
</table>

</br>

## Beispiel: Einem anderen Benutzer Zugriff auf eine Instanz von {{site.data.keyword.appid_short_notm}} gewähren
{: #iam-example}

In diesem Szenario erstellte ein Administrator eine Instanz von {{site.data.keyword.appid_short_notm}} und muss einem anderen Teammitglied die Berechtigung zur Anzeige erteilen.
{: shortdesc}

Vorbereitungen:

* Installieren Sie die [{{site.data.keyword.cloud_notm}}-CLI](/docs/cli?topic=cloud-cli-getting-started).

Der Administrator führt die folgenden Schritte aus, um die Zugriffsberechtigungen zu aktualisieren:

1. Melden Sie sich bei der {{site.data.keyword.cloud_notm}}-Konsole an.

2. Erteilen Sie dem Mitarbeiter die Berechtigung zum Anzeigen, indem Sie die Schritte ausführen, die in der [IAM-Dokumentation](/docs/iam?topic=iam-iammanidaccser) erläutert werden.

3. Navigieren Sie zur Registerkarte **Serviceberechtigungsnachweise** des {{site.data.keyword.appid_short_notm}}-Dashboards. Klicken Sie auf **Berechtigungsnachweise anzeigen** und kopieren Sie die **tentantID**.

4. Melden Sie sich an der {{site.data.keyword.cloud_notm}}-CLI in Ihrem Terminal an.

    ```
    ibmcloud login -api -a https://api.{region}.cloud.ibm.com
    ```
    {: codeblock}

    <table>
      <tr>
        <th>Region</th>
        <th>Endpunkt</th>
      </tr>
      <tr>
        <td>Dallas</td>
        <td><code>us-south</code></td>
      </tr>
      <tr>
        <td>Frankfurt</td>
        <td><code>eu-de</code></td>
      </tr>
      <tr>
        <td>Sydney</td>
        <td><code>au-syd</code></td>
      </tr>
      <tr>
        <td>London</td>
        <td><code>eu-gb</code></td>
      </tr>
      <tr>
        <td>Tokio</td>
        <td><code>jp-tok</code></td>
      </tr>
    </table>

5. Rufen Sie ein IAM-Token ab und notieren Sie es.

    ```
    ibmcloud iam oauth-tokens
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
    'https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/config/idps/facebook'
    ```
    {: codeblock}

    Das Ergebnis ist eine 403 Nachricht über fehlende Berechtigung.

Zur Anzeige der {{site.data.keyword.appid_short_notm}}-Konfigurationen über die CLI führt das Teammitglied folgende Schritte aus:

1. Melden Sie sich über die {{site.data.keyword.cloud_notm}}-CLI in Ihrem Terminal an.

    ```
    ibmcloud login -a api.<region>.console.cloud.ibm.com
    ```
    {: codeblock}

2. Rufen Sie ein IAM-Token ab und notieren Sie es.

    ```
    ibmcloud iam oauth-tokens
    ```
    {: codeblock}

3. Zeigen Sie die Konfiguration des Identitätsproviders für Facebook mithilfe der cURL an.

    ```
    curl -X GET --header 'Accept: application/json' --header 'Authorization: <IAM token value>' \  'https://us-south.appid.cloud.ibm.com/management/v4/<tenant-ID>/config/idps/facebook'
    ```
    {: codeblock}

    Das Ergebnis ist eine 200 Nachricht, die die Identitätsproviderdaten enthält.

