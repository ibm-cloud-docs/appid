---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

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
    <td>Sie können eine {{site.data.keyword.appid_short_notm}}-Instanz im Katalog erstellen oder aus diesem löschen. </td>
  </tr>
  <tr>
    <td><i>Administrator</i></td>
    <td>Alle Managementaktionen für alle Services im Konto. </td>
    <td>Sie können alle Bedieneraktionen ausführen und haben die Möglichkeit anderen Benutzern Richtlinien zuzuordnen. </td>
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

Die Aktionen werden vom {{site.data.keyword.Bluemix_notm}}-Service angepasst und als Operationen definiert, die im Service ausgeführt werden dürfen. Die Aktionen werden dann zu IAM-Benutzerrollen zugeordnet. Für {{site.data.keyword.appid_short_notm}} gibt es die folgenden Rollen: 

<table>
  <tr>
    <th>Befehl</th>
    <th>Erläuterung</th>
    <th>Rolle</th>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-redirect-uris</code></td>
    <td>Zeigt die Weiterleitungs-URLs von post-authentication an. </td>
    <td>Leseberechtigter, Schreibberechtigter, Manager</td>
  </tr>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-redirect-uris</code></td>
    <td>Fügt die Weiterleitungs-URLs von post-authentication hinzu oder aktualisiert diese. </td>
    <td>Leseberechtigter, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-idps</code></td>
    <td>Aktualisiert die Konfiguration Ihres Identitätsproviders. </td>
    <td>Leseberechtigter, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-idps</code></td>
    <td>Zeigt die Konfiguration Ihres Identitätsproviders an. </td>
    <td>Leseberechtigter, Schreibberechtigter, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-recent-activities</code></td>
    <td>Zeigt alle aktuellen Authentifizierungsereignisse in einer Liste an. </td>
    <td>Leseberechtigter, Schreibberechtigter, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-ui-config</code></td>
    <td>Zeigt die Konfiguration des Anmeldewidgets wie beispielsweise Logo und Farben an, </td>
    <td>Leseberechtigter, Schreibberechtigter, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-ui-config</code></td>
    <td>Aktualisiert die Konfiguration des Anmeldewidgets.</td>
    <td>Leseberechtigter, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-user-profile-config</code></td>
    <td>Zeigt die Konfiguration des Benutzerprofils an. </td>
    <td>Leseberechtigter, Schreibberechtigter, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-user-profile-config</code></td>
    <td>Ändert die Konfiguration des Benutzerprofils. </td>
    <td>Leseberechtigter, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-cd-users</code></td>
    <td>Zeigt die Konfiguration des Benutzerprofils an. </td>
    <td>Leseberechtigter, Schreibberechtigter, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-add-cd-user</code></td>
    <td>Fügt neue Benutzer zum Cloudverzeichnis hinzu. </td>
    <td>Leseberechtigter, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-cd-user</code></td>
    <td>Aktualisiert die Details eines Cloudverzeichnisbenutzers. </td>
    <td>Leseberechtigter, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-delete-cd-user</code></td>
    <td>Löscht einen Benutzer aus dem Cloudverzeichnis. </td>
    <td>Leseberechtigter, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-email-template</code></td>
    <td>Zeigt die E-Mail-Vorlagen des Cloudverzeichnisses an. </td>
    <td>Leseberechtigter, Schreibberechtigter, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-update-email-template</code></td>
    <td>Aktualisiert die E-Mail-Vorlage mit Ihrem eigenen Inhalt. </td>
    <td>Leseberechtigter, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-delete-email-template</code></td>
    <td>Löscht eine E-Mail-Vorlage des Cloudverzeichnisses. </td>
    <td>Leseberechtigter, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-send-email-cd</code></td>
    <td>Sendet auf Grundlage einer Vorlage eine E-Mail an einen Benutzer. </td>
    <td>Leseberechtigter, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-sender-details-cd</code></td>
    <td>Zeigt die Senderdetails für die Email an. </td>
    <td>Leseberechtigter, Schreibberechtigter, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-sender-details-cd</code></td>
    <td>Aktualisiert die Senderdetails. </td>
    <td>Leseberechtigter, Manager</td>
  </tr>
</table>




## Beispiel: Gewährt einem anderen Benutzer Zugriff auf eine Instanz von {{site.data.keyword.appid_short_notm}}
{: #example}

In diesem Szenario erstellte ein Administrator eine Instanz von {{site.data.keyword.appid_short_notm}} und muss einem anderen Teammitglied die Berechtigung zur Anzeige erteilen.
{: shortdesc}

Vorbereitungen:
* Installieren Sie die [{{site.data.keyword.Bluemix_notm}}-CLI](/docs/cli/reference/bluemix_cli/get_started.html).

Der Administrator führt die folgenden Schritte aus, um die Zugriffsberechtigungen zu aktualisieren: 

1. Melden Sie sich bei der {{site.data.keyword.Bluemix_notm}}-Konsole an.
2. Erteilen Sie dem Mitarbeiter die Berechtigung zum Anzeigen, indem Sie die Schritte ausführen, die in der [IAM-Dokumentation](/docs/iam/iamusermanage.html#iamusermanage) erläutert werden.
3. Navigieren Sie zur Registerkarte **Serviceberechtigungsnachweise** des {{site.data.keyword.appid_short_notm}}-Dashboards. Klicken  Sie auf **Berechtigungsnachweise anzeigen** und kopieren Sie die **tentantID**.
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
    'https://appid-management.stage1.ng.bluemix.net/management/v4/<tenantId>/config/idps/facebook'
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
