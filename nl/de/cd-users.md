---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-09"

keywords: Authentication, authorization, identity, app security, secure, directory, registry, passwords, languages, lockout

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


# Benutzer verwalten
{: #cd-users}

Mit Cloud Directory können Sie Benutzer in einer skalierbaren Registry mithilfe vordefinierter Funktionen verwalten, die die Sicherheit und den Self-Service erhöhen.
{: shortdesc}

Ein Cloud Directory-Benutzer ist nicht identisch mit einem {{site.data.keyword.appid_short_notm}}-Benutzer. Benutzer können sich unter Verwendung der von Ihnen konfigurierten Identitätsprovideroptionen bei der App registrieren; alternativ können Sie sie zum Verzeichnis hinzufügen. Die Benutzer, die auf dieser Seite genannt werden, sind diejenigen, die Cloud Directory als Identitätsprovider zugeordnet sind.
{: note}

## Benutzerinformationen anzeigen
{: #cd-user-info}

Sie können alle Informationen, die zu allen Cloud Directory-Benutzer vorhanden sind, mithilfe der APIs oder des Dashboards als JSON-Objekt anzeigen. 
{: shortdesc}


### Mit der GUI

Sie können im {{site.data.keyword.appid_short_notm}}-Dashboard Details zu den App-Benutzern anzeigen. 

1. Navigieren Sie zur Registerkarte **Cloud Directory > Benutzer** der {{site.data.keyword.appid_short_notm}}-Instanz.

2. Durchsuchen Sie die Tabelle oder suchen Sie mithilfe einer E-Mail-Adresse, um den Benutzer zu finden, für den Sie die Informationen anzeigen möchten.

3. Klicken Sie im Überlaufmenü in der Zeile des Benutzers auf **Benutzerdetails anzeigen**. Es wird eine Seite geöffnet, auf der die Informationen des Benutzers enthalten sind. In der folgenden Tabelle sehen Sie, welche Informationen angezeigt werden.

<table>
  <tr>
    <th colspan="2">Benutzerdetails</th>
  </tr>
  <tr>
    <td>Benutzer-ID</td>
    <td>Die Benutzer-ID hängt vom Typ der Benutzeranmeldung ab, die Sie konfiguriert haben. Wenn Sie einen Ablauf für E-Mail und Kennwort konfiguriert haben, ist die ID die Benutzer-E-Mail. Wenn Sie den Ablauf mit Benutzername und Kennwort verwenden, ist der Benutzername der, der bei der Anmeldung angegeben wurde. </td>
  </tr>
  <tr>
    <td>E-Mail</td>
    <td>Die primäre E-Mail-Adresse, die dem Benutzer zugeordnet ist.</td>
  </tr>
    <tr>
    <td>Vor- und Nachname</td>
    <td>Der Vor- und Nachname des Benutzers, wie er während der Anmeldung angegeben wurde. </td>
  </tr>
  <tr>
    <td>Letzte Anmeldung</td>
    <td>Die Zeitmarke des letzten Zeitpunkts, an dem sich der Benutzer an der Anwendung angemeldet hat. Hinweis: Wenn Sie Ihre Benutzer über das Dashboard hinzugefügt haben, ist die Anmeldung leer, bis der Benutzer sich selbst bei Ihrer App anmeldet. Wenn die Anmeldung erfolgt, werden die Benutzer ebenfalls App-ID-Benutzer. </td>
  </tr>
  <tr>
    <td>ID</td>
    <td>Die ID, die dem Benutzer von {{site.data.keyword.appid_short_notm}} zugeordnet wird. Sie wird in der Benutzerschnittstelle angezeigt, aber Sie können den Wert kopieren und in einem Texteditor einfügen, um den Wert anzuzeigen. </td>
  </tr>
  <tr>
    <td>Vordefinierte Attribute</td>
    <td>Vordefinierte Attribute sind Daten, die über einen Benutzer auf der Basis von SCIM bekannt sind.</td>
  </tr>
  <tr>
    <td>Angepasste Attribute</td>
    <td>Angepasste Attribute sind zusätzliche Informationen, die zu einem Profil hinzugefügt werden oder die während der Interaktion des Benutzers mit der Anwendung erfasst werden.</td>
  </tr>
  <tr>
    <td>Zusammenfassung</td>
    <td>Alle Attribute werden kompiliert, um ein Profil zu bilden, mit dem Sie einen kompletten Überblick über Ihre Cloud Directory-Benutzer erhalten. Weitere Informationen finden Sie unter [Benutzerprofile](/docs/services/appid?topic=appid-profiles).</td>
  </tr>
</table>

</br>

### Mit der API

Sie können in der {{site.data.keyword.appid_short_notm}}-API Details zu den App-Benutzern anzeigen. 

1. Rufen Sie Ihre Tenant-ID von der Instanz des Service ab.

2. Suchen Sie die App ID-Benutzer mithilfe einer Abfrage, mit der sich diese identifizieren lassen, zum Beispiel über eine E-Mail-Adresse, um die Benutzer-ID zu finden.

  ```
  curl -X GET "https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/cloud_directory/Users?query={identifying-search-query}" -H "accept: application/json" -H "authorization: Bearer {token}"
  ```
  {: codeblock}

  Beispiel:

  ```
  curl -X GET https://us-south.appid.cloud.ibm.com/management/v4/e19a2778-3262-4986-8875-8khjafsdkhjsdafkjh/cloud_directory/Users?query=example@email.com -H "accept: application/json" -H "authorization: Bearer eyJraWQiOiIyMDE3MTEyOSIsImFsZ...."
  ```
  {: screen}

3. Erstellen Sie mithilfe der im vorherigen Schritt abgerufenen ID eine GET-Anforderung für den Endpunkt `cloud_directory/users`, um das vollständige Benutzerprofil anzuzeigen.

  ```
  curl -X GET "https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/cloud_directory/Users/{user-ID}" -H "accept: application/json" -H "authorization: Bearer {token}"
  ```
  {: codeblock}

  Beispielantwort:

  ```
  {
    sub: "c155c0ff-337a-46d3-a22a-a8f2cca08995",
    name: "Test User",
    email: "testuser@test.com",
    identities: [
      {
        provider: "cloud_directory",
        id: "f1772fcc-ff70-4d88-81a0-07dd7a3d988f",
        idpUserInfo: {
          displayName: "Test User",
          active: true,
          mfaContext: {},
          emails: [
            {
              value: "testuser@test.com",
              primary: true
            }
          ],
          meta: {
            lastLogin: "2019-05-20T16:33:20.699Z",
            created: "2019-05-20T16:25:13.019Z",
            location: "/v1/6b8ab644-1d4a-4b3e-bcd9-777ba8430a51/Users/f1772fcc-ff70-4d88-81a0-07dd7a3d988f",
            lastModified: "2019-05-20T16:33:20.707Z",
            resourceType: "User"
          },
          scemas: [
            "urn:ietf:params:scim:schemas:core:2.0:User"
          ],
          name: {
            givenName: "Test",
            familyName: "User",
            formatted: "Test User"
            },
          id: "f1772fcc-ff70-4d88-81a0-07dd7a3d988f",
          status: "CONFIRMED",
          idpType: "cloud_directory"
        }
      }
    ]
  }
  ```
  {: screen}

  Um die vollständigen Daten eines Benutzers anzuzeigen, für den {{site.data.keyword.appid_short_notm}} Unterstützung bietet, machen Sie sich mit dem [SCIM-Kernschema](https://tools.ietf.org/html/rfc7643#section-8.2) vertraut.
  {: tip}


## Benutzer hinzufügen und löschen
{: #add-delete-users}

Sie können die Cloud Directory-Benutzer über das {{site.data.keyword.appid_short_notm}}-Dashboard oder die APIs verwalten.
{: shortdesc}

Wenn sich ein Benutzer bei der Anmeldung registriert, wird diese Anmeldung über einen Self-Service-Workflow durchgeführt, von dem automatisch E-Mails ausgelöst werden, zum Beispiel Willkommens- oder Verifizierungsanforderungen. Wenn Sie als Administrator einen Benutzer zu Ihrer App hinzufügen, wird kein Self-Service-Workflow eingeleitet, was bedeutet, dass Benutzer keine E-Mails von Ihrer Anwendung erhalten. Wenn Sie möchten, dass Benutzer weiterhin dann benachrichtigt werden, wenn Sie hinzugefügt werden, können Sie die Nachrichtenweiterleitungen über die [Management-API der App-ID](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.set_cloud_directory_email_dispatcher) auslösen.


### Benutzer hinzufügen
{: #add-users}

Wenn sich ein Benutzer bei der Anmeldung registriert, wird er als Benutzer hinzugefügt. Zu Testzwecken können Sie einen Benutzer über das {{site.data.keyword.appid_short_notm}}-Dashboard oder die API hinzufügen.

Wenn Sie die Self-Service-Anmeldung inaktivieren oder einen Benutzer in seinem Namen hinzufügen, erhält der Benutzer keine Willkommens- oder Bestätigungsnachricht, wenn er hinzugefügt wird.
{: tip}



**Gehen Sie wie folgt vor, um einen Benutzer mit der GUI hinzuzufügen:**

1. Wechseln Sie auf die Registerkarte **Cloudverzeichnis > Benutzer** im {{site.data.keyword.appid_short_notm}}-Dashboard.

2. Klicken Sie auf **Benutzer hinzufügen**. Ein Formular wird geöffnet.

3. Geben Sie einen Wert für **Vorname**, **Nachname**, **E-Mail** und **Kennwort** ein. Vergewissern Sie sich, dass die E-Mail-Adresse, die Sie zur Registrierung verwenden wollen, nicht bereits von einem anderen Benutzer benutzt wird. Um sicherzustellen, dass Sie Ihr Kennwort korrekt eingegeben haben, bestätigen Sie dies durch Eingabe in das Feld **Kennwort erneut eingeben**. 

4. Klicken Sie auf **Speichern**. Daraufhin wird ein Cloud Directory-Benutzer erstellt.

</br>


**Gehen Sie wie folgt vor, um einen Benutzer mit der API hinzuzufügen: **

Am folgenden Ablauf wird erläutert, wie ein Benutzer mit einer E-Mail und einem Kennwort hinzugefügt wird. Sie können ferner auswählen, dass ein Ablauf mit Benutzername und Kennwort verwendet wird. 

1. Rufen Sie den Wert für `tenantID` von der Anwendung oder die Serviceberechtigungsnachweise ab.

2. Rufen Sie das {{site.data.keyword.cloud_notm}}-IAM-Token ab.

  ```
  curl --X GET "https://iam.cloud.ibm.com/oidc/token" -H "accept: application/x-www-form-urlencoded"
  ```
  {: codeblock}

3. Erstellen Sie mit dem Token, das Sie in Schritt 2 erhalten haben, eine POST-Anforderung an den Endpunkt `cloud-directory/users`. Dieses Beispiel verwendet den Ablauf mit E-Mail und Kennwort. Sie können auch den Ablauf für Benutzername und Kennwort verwenden.

  ```
  curl --X POST "https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/cloud_directory/Users"
  -H "accept: application/json"
  -H "content-type: application/json"
  -H "authorization: Bearer {token}"
  -d {
    "displayName": "Test User",
    "password": "{App-ID-Cloud-Directory-User-Password}",
    "active": true,
    "emails": [
      {
        "value": "{App-ID-Cloud-Directory-User-Email}",
        "primary": true
      }
    ]
  }
  ```
  {: codeblock}

</br>


### Benutzer löschen
{: #delete-users}

Wenn Sie einen Benutzer aus dem Verzeichnis entfernen möchten, können Sie den Benutzer in der grafischen Benutzerschnittstelle oder mithilfe der APIs löschen.
{: shortdesc}

**Gehen Sie wie folgt vor, um einen Benutzer in der grafischen Benutzerschnittstelle zu löschen:**

1. Wechseln Sie auf die Registerkarte **Cloudverzeichnis > Benutzer** im {{site.data.keyword.appid_short_notm}}-Dashboard.

2. Klicken Sie auf das Kontrollkästchen neben dem Benutzer, den Sie löschen möchten. Ein Feld wird angezeigt. 

3. Klicken Sie in dem Feld auf **Löschen**. Daraufhin wird eine Anzeige geöffnet.

4. Bestätigen Sie, dass Sie wissen, dass das Löschen eines Benutzers nicht rückgängig gemacht werden kann, indem Sie auf **Löschen** klicken. Wenn die Aktion fälschlicherweise ausgeführt wurde, dann können Sie den Benutzer erneut zu Ihrem Verzeichnis hinzufügen, die zuvor zu dem betreffenden Benutzer vorhandenen Daten sind jedoch nicht mehr verfügbar.

</br>

**Gehen Sie wie folgt vor, um einen Benutzer mithilfe der APIs zu löschen:**

1. Rufen Sie Ihre Tenant-ID ab.

2. Durchsuchen Sie mithilfe der E-Mail-Adresse, die dem Benutzer zugeordnet ist, das Verzeichnis nach der ID des Benutzers.

  ```
  curl -X GET "https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/users?email={user-email}" -H "accept: application/json"
  ```
  {: codeblock}

3. Löschen Sie den Benutzer.

  ```
  curl --X DELETE "https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/cloud_directory/Users/{user-GUID}"
  -H "accept: application/x-www-form-urlencoded"
  ```
  {: codeblock}



## Benutzer migrieren
{: #user-migration}

Gelegentlich müssen Sie vielleicht eine Instanz von {{site.data.keyword.appid_short_notm}} hinzufügen. Wenn Sie mit Cloud Directory arbeiten, müssen Ihre Benutzer auf die neue Instanz migriert werden. Um die Migration zu unterstützen, können Sie die Management-APIs verwenden.
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
    <td>Eine angepasste Zeichenfolge, die zur Ver- und Entschlüsselung eines hashverschlüsselten Benutzerkennworts verwendet wird. </td>
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
    <td>Stellen Sie sicher, dass Sie über <code>manager</code>-Berechtigungen verfügen, bevor Sie das Token anfordern. Hilfe beim Abrufen eines IAM-Tokens finden Sie in den <a href="/docs/iam?topic=iam-iamtoken_from_apikey#iamtoken_from_apikey" target="_blank">Dokumenten <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>.</td>
  </tr>
</table>

So führen Sie das Script aus:

1. Klonen Sie das <a href="https://github.com/ibm-cloud-security/appid-sample-code-snippets/tree/master/export-import-cloud-directory-users" target="_blank">Repository <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>.
2. Öffnen Sie die Konsole und wechseln Sie in den Ordner, in den Sie das Repository geklont haben. 
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
