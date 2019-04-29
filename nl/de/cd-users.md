---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

keywords: authentication, authorization, identity, app security, secure, directory, registry, passwords, languages, lockout

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


# Benutzer verwalten
{: #cd-users}

Wenn Sie Cloud Directory aktivieren, können Benutzer sich für Ihre Anwendung registrieren, indem Sie eine E-Mail-Adresse oder einen Benutzernamen und ein Kennwort verwenden.
{: shortdesc}


Ein Cloud Directory-Benutzer ist nicht identisch mit einem {{site.data.keyword.appid_short_notm}}-Benutzer. Benutzer können sich für Ihre App registrieren, indem Sie die unterschiedlichen Optionen für Identitätsprovider verwenden, die Sie konfiguriert haben. Bei den in diesem Abschnitt aufgeführten Benutzern handelt es sich um diejenigen Benutzer, die bei der Registrierung in Ihrer App die Cloud Directory-Option verwendet haben.
{: note}


## Benutzer hinzufügen und löschen
{: #add-delete-users}

Sie können die Cloud Directory-Benutzer über das {{site.data.keyword.appid_short_notm}}-Dashboard oder die APIs verwalten.
{: shortdesc}

Um alle Daten eines bestimmten Benutzers anzuzeigen, können Sie die APIs verwenden, um die Informationen zu einem Cloud Directory-Benutzer als JSON-Objekt zurückzugeben. Um die vollständigen Daten eines Benutzers anzuzeigen, für den {{site.data.keyword.appid_short_notm}} Unterstützung bietet, machen Sie sich mit dem [SCIM-Kernschema](https://tools.ietf.org/html/rfc7643#section-8.2) vertraut.

### Benutzer hinzufügen
{: #add-users}

Sie können die folgenden Schritte ausführen, um einen Benutzer über das {{site.data.keyword.appid_short_notm}}-Dashboard hinzuzufügen.

Zu Testzwecken können Sie einen Benutzer über das {{site.data.keyword.appid_short_notm}}-Dashboard hinzufügen.

1. Navigieren Sie zur Registerkarte **Cloud Directory > Benutzer** des {{site.data.keyword.appid_short_notm}}-Dashboards.

2. Klicken Sie auf **Benutzer hinzufügen**. Daraufhin wird ein Formular angezeigt.

3. Geben Sie einen Wert für **Vorname**, **Nachname**, **E-Mail** und **Kennwort** ein. Vergewissern Sie sich, dass die E-Mail-Adresse, die Sie zur Registrierung verwenden wollen, nicht bereits von einem anderen Benutzer benutzt wird. Um sicherzustellen, dass Ihnen bei der Kennworteingabe kein Fehler unterlaufen ist, müssen Sie das Kennwort bestätigen, indem Sie es im Feld **Kennwort erneut eingeben** ein zweites Mal eingeben.

4. Klicken Sie auf **Speichern**. Daraufhin wird ein Cloud Directory-Benutzer erstellt.


### Benutzer löschen
{: #delete-users}

Wenn Sie einen Benutzer aus Ihrem Verzeichnis entfernen möchten, können Sie den Benutzer über die GUI löschen.

1. Navigieren Sie zur Registerkarte **Cloud Directory > Benutzer** des {{site.data.keyword.appid_short_notm}}-Dashboards.

2. Klicken Sie auf das Kontrollkästchen neben dem Benutzer, den Sie löschen möchten. Daraufhin wird ein Feld angezeigt.

3. Klicken Sie in dem Feld auf **Löschen**. Daraufhin wird eine Anzeige aufgerufen.

4. Bestätigen Sie, dass Sie wissen, dass das Löschen eines Benutzers nicht rückgängig gemacht werden kann, indem Sie auf **Löschen** klicken. Wenn die Aktion fälschlicherweise ausgeführt wurde, dann können Sie den Benutzer erneut zu Ihrem Verzeichnis hinzufügen, die zuvor zu dem betreffenden Benutzer vorhandenen Daten sind jedoch nicht mehr verfügbar.


## Benutzer migrieren
{: #user-migration}

Es kann vorkommen, dass Sie eine neue Instanz von {{site.data.keyword.appid_short_notm}} einrichten müssen. Wenn Sie Cloud Directory verwenden, bedeutet dies, dass Ihre Benutzer auf die neue Instanz migriert werden müssen. Sie können die Management-APIs verwenden, die Sie bei der Migration unterstützen.
{: shortdesc}


Ihnen muss die [IAM-Rolle](/docs/iam?topic=iam-getstarted#getstarted) `Manager` für beide Instanzen von {{site.data.keyword.appid_short_notm}} zugeordnet sein.
{: note}


### Export ausführen
{: cd-export}

Bevor Sie Ihre Benutzer zur neuen Instanz hinzufügen können, müssen Sie sie aus Ihrer aktuellen Instanz exportieren. Dazu können Sie die <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryExport" target="_blank">Export-Management-API <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> verwenden.

Beispiel für cURL-Befehl:

```
curl -X GET --header ‘Accept: application/json’ --header ‘Authorization: Bearer <iam-token>’ ’https://us-south.appid.cloud.ibm.com/management/v4/111c9bj3-xxxx-4b5b-zzzz-24ad9440k8j9/cloud_directory/export?encryption_secret=myCoolSecret'
```
{: codeblock}

<table>
  <tr>
    <th>Variable</th>
    <th>Beschreibung</th>
  </tr>
  <tr>
    <td><code>encryption_secret</code></td>
    <td>Eine angepasste Zeichenfolge, die zum Verschlüsseln und Entschlüsseln eines hashverschlüsselten Benutzerkennworts verwendet wird.</td>
  </tr>
  <tr>
    <td><code>tenantID</code></td>
    <td>Die Service-Tenant-ID ist in Ihren Serviceberechtigungsnachweisen enthalten. Sie finden Ihre Serviceberechtigungsnachweise im {{site.data.keyword.appid_short_notm}}-Dashboard.</td>
  </tr>
</table>

Nur Ihre Cloud Directory-Benutzer und deren Profile werden zurückgegeben. Für die Benutzer anderer Identitätsprovider gilt dies nicht.
{: note}


### Import ausführen
{: #cd-import}

Ihre Benutzer sind nun bereit und Sie können ihre Informationen in die neue Instanz importieren. Dazu können Sie die <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryImport" target="_blank">Import-Management-API <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> verwenden.


Beispiel für cURL-Befehl:

```
curl -X POST --header ‘Content-Type: application/json’ --header ‘Accept: application/json’ --header ‘Authorization: Bearer <iam-token>’ -d ‘{“users”: [
    {
      “scimUser”: {
        “originalId”: “3f3f6779-7978-4383-926f-a43aef3b724b”,
        “name”: {
          “givenName”: “<first-name>”,
          “familyName”: “<last-name>”,
          “formatted”: “<first-name> <last-name>”
        },
        “displayName”: “<first-name>”,
        “emails”: [
          {
            “value”: “<user>@gmail.com”,
            “primary”: true
          }
        ],
        “status”: “PENDING”
      },
      “passwordHash”: “<password hash here>“,
      “passwordHashAlg”: “<password hash algorithm>",
      “profile”: {
        “attributes”: {}
      }
    }
]}’ ‘https://us-south.appid.cloud.ibm.com/management/v4/111c9bj3-xxxx-4b5b-zzzz-24ad9440k8j9/cloud_directory/import?encryption_secret=myCoolSecret’
```
{: codeblock}



### Migrationsscript
{: cd-migration-script}

{{site.data.keyword.appid_short_notm}} stellt ein Migrationsscript zur Verfügung, das Sie über die CLI verwenden und so den Migrationsprozess beschleunigen können.

Bevor Sie beginnen, stellen Sie sicher, dass Sie über die folgenden Parameterinformationen verfügen:

<table>
  <tr>
    <th>Parameter</th>
    <th>Beschreibung</th>
  </tr>
  <tr>
    <td><code>sourceTenantId</code></td>
    <td>Die Tenant-ID der Instanz von {{site.data.keyword.appid_short_notm}}, aus der Sie Benutzer exportieren wollen.</td>
  </tr>
  <tr>
    <td><code>destinationTenantId</code></td>
    <td>Die Tenant-ID der Instanz von {{site.data.keyword.appid_short_notm}}, in die Sie Benutzer exportieren wollen.</td>
  </tr>
  <tr>
    <td>Region</td>
    <td>Folgende Regionsoptionen sind verfügbar: <code>au-syd</code>, <code>eu-de</code>, <code>eu-gb</code>, <code>jp-tok</code> und <code>us-south</code>.</td>
  </tr>
  <tr>
    <td>IAM-Token</td>
    <td>Stellen Sie sicher, dass Sie über <code>manager</code>-Berechtigungen verfügen, bevor Sie das Token anfordern. Hilfe zum Anfordern eines IAM-Tokens finden Sie in der <a href="https://cloud.ibm.com/docs/iam/apikey_iamtoken.html#iamtoken_from_apikey" target="_blank">Dokumentation <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>.</td>
  </tr>
</table>

So führen Sie das Script aus:

1. Klonen Sie das <a href="https://github.com/ibm-cloud-security/appid-sample-code-snippets/tree/master/export-import-cloud-directory-users" target="_blank">Repository <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>.
2. Öffnen Sie das Terminal und navigieren Sie zu dem Ordner, in den Sie das Repository geklont haben.
3. Führen Sie den folgenden Befehl aus.

  ```
  npm install
  ```
  {: codeblock}

4. Führen Sie den folgenden Befehl mit Ihren Parametern aus.

  ```
  users_export_import 'sourceTenantId' 'destinationTenantId' 'region' 'iamToken'
  ```
  {: codeblock}

  Beispielbefehl:

  ```
  users_export_import e00a0366-53c5-4fcf-8fef-ab3e66b2ced8 73321c2b-d35a-497a-9845-15c580fdf58c ng eyJraWQiOiIyMDE3MTAyNS0xNjoyNzoxMCIsImFsZyI6IlJTMjU2In0.eyJpYW1faWQiOiJJQk1pZC0zMTAwMDBUNkZTIiwiaWQiOiJJQk1pZC0zMTAwMDBUNkZTIiwicmVhbG1pZCI6IklCTWlkIiwiaWRlbnRpZmllciI6IjMxMDAwIFQ2RlMiPCJnaXZlbl9uYW1lIjoiUm90ZW0iLCJmYW1pbHlfbmFtZSI6IkJyb3NoIiwibmFtZSI6IlJvdGVtIEJyb3NoIiwiZW1haWwiOiJyb3RlbWJyQGlsLmlibS5jb20iLCJzdWIiOiJyb3RlbWJyQGlsLmlibS5jb20iLCJhY2NvdW50Ijp7ImJzcyI6ImQ3OWM5YTk5NjJkYzc2Y2JkMDZlYTVhNzhjMjY0YzE5In0sImlhdCI6MTUzNrE3Mjg4NCwiZXhwIjoxNTM3MTc2NDg0LCJpc3MiOiJodHRwczovL2lhbS5zdGFnZTEuYmx1ZW1peC5uZXQvaWRlbnRpdHkiLCJncmFudF90eXBlIjoidXJuOmlibTpwYXJhbXM6b2F1dGg6Z3JhbnQtdHlwZTpwYXNzY29kZSIsInNjb3BlIjoiaWJtIG9wZW5pZCIsImNsaWVudF9pZCI6ImJ4IiwiYWNyIjoxLCJhbXIiOlsicHdkIl19.c4vLPzhvvNZLjaLy7znDa37qV4o-yuGmSKmJoQKrEQNZU8IC0NIjxwSo7W9kb0pDi3Yf_03_9ufTTGNfjtltzNWycSXjkNgoL-b9_nU61oHdgn0stY1KmNicqyBWfgUU--4xa904QN_QjRHBaUBeJf3XWEphPIMoF7mZeOxEZLnCMcQXSz9pImCMiP4SNT38cHLiI90Yx01rM7hpteepWULh5MYh-B2V03Gkgxfqvv951HF1LDg6eT4Q9in11laTQKtKuomripUju_4GIIjORVYw9NaAVKIJ9lKrPX0SKPhStsa59qGsC_7Uersms5EY1W1VbZVqOZPJbtp6tVf-Lw
  ```
  {: codeblock}
