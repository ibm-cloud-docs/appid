---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

keywords: authentication, authorization, identity, app security, secure, development, user information, attributes, profiles, 

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

# Attribute vor Benutzeranmeldung hinzufügen
{: #preregister}

Mit {{site.data.keyword.appid_full}} können Sie mit dem Erstellen eines Profils für Benutzer beginnen, von denen Sie wissen, dass sie Zugriff auf Ihre App benötigen werden, bevor sie sich zum ersten Mal anmelden.
{: shortdesc}

Weitere Informationen zu den Typen von Attributen finden Sie unter [Informationen zu Benutzerprofilen](/docs/services/appid?topic=appid-user-profile). Weitere Informationen zu angepassten Attributen und deren Sicherheitsaspekten finden Sie unter [Angepasste Attribute](/docs/services/appid?topic=appid-custom-attributes).
{: tip}

## Informationen zur Vorabregistrierung
{: #preregister-understand}

### Welche Gründe sprechen für die Verwendung der Vorabregistrierung?
{: #preregister-why}

Angenommen, Sie haben eine Anwendung, in der Sie {{site.data.keyword.appid_short_notm}} verwenden, um vorhandene Benutzer von Ihrem SAML-Identitätsprovider einzubinden. Möglicherweise gibt es bestimmte Benutzer, die schon beim ersten Anmelden `Admin`-Zugriff auf die Anwendung erhalten sollen. Um dies zu ermöglichen, können Sie den Endpunkt für die Vorabregistrierung verwenden, um ein angepasstes `admin`-Attribut für diese Benutzer festzulegen und ihnen den Zugriff auf die Administrationskonsole zu gewähren, ohne dass Sie weitere Aktionen hierfür ausführen müssen. Stellen Sie sicher, dass Sie mögliche [Sicherheitsprobleme](/docs/services/appid?topic=appid-custom-attributes#custom-attributes) berücksichtigen, die sich durch das Ändern der Standardeinstellung ergeben können.

### Wie werden Benutzer identifiziert?
{: #preregister-identify-user}

Sie können Ihre Benutzer wie folgt identifizieren:

* Mit der eindeutigen ID des Benutzers, die als **GUID** bezeichnet wird (im Identitätsprovider). Auch wenn diese ID immer vorhanden und garantiert eindeutig ist, ist sie nicht immer leicht verfügbar oder leicht verständlich. Beispielsweise verwendet Cloud Directory eine nach dem Zufallsprinzip generierte 16-Byte-GUID.
* Mit der **E-Mail-Adresse** des Benutzers (falls verfügbar).

### Welche Informationen stellen Identitätsprovider bereit?
{: #preregister-idp-provide}

In der folgenden Tabelle sehen Sie, welche Identitätsinformationen Sie verwenden können.

<table>
  <thead>
    <tr>
      <th>Identitätsprovider</th>
      <th>GUID</th>
      <th>E-Mail</th>
      <th>Sub</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Cloud Directory</td>
      <td><img src="images/confirm.png" width="32" alt="Funktion verfügbar" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="Funktion verfügbar" style="width:32px;" /></td>
      <td> </td>
    </tr>
    <tr>
      <td>Facebook</td>
      <td><img src="images/confirm.png" width="32" alt="Funktion verfügbar" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="Funktion verfügbar" style="width:32px;" /></td>
      <td> </td>
    </tr>
    <tr>
      <td>Google</td>
      <td><img src="images/confirm.png" width="32" alt="Funktion verfügbar" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="Funktion verfügbar" style="width:32px;" /></td>
      <td> </td>
    </tr>
    <tr>
      <td>SAML</td>
      <td></td>
      <td><img src="images/confirm.png" width="32" alt="Funktion verfügbar" style="width:32px;" /></td>
      <td> </td>
    </tr>
    <tr>
      <td>Angepasst</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Funktion verfügbar" style="width:32px;" /></td>
    </tr>
  </tbody>
</table>

### Wie wird Cloud Directory behandelt?
{: #preregister-cd}


Um die Integrität der vorab registrierten Benutzerattribute sicherzustellen, stellt Cloud Directory zusätzliche Anforderungen an die Benutzer. Die Vorabregistrierung kann nur stattfinden, wenn die E-Mail-Validierung aktiviert und validiert wurde. Wenn Sie einen Cloud Directory-Benutzer mit bestimmten Attributen vorab registrieren, sind diese Attribute für eine bestimmte Person vorgesehen. Wenn die E-Mail nicht zuerst verifiziert wird, kann ein anderer Benutzer die E-Mail-Adresse und alle Attribute, die ihr zugeordnet sind, beanspruchen.

1. Versetzen Sie Cloud Directory in den E-Mail- und Kennwortmodus. Dies können Sie über die UI in den allgemeinen Einstellungen auf der Registerkarte **Cloud Directory** tun. Sie können die Festlegung auch über die [Management-APIs](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.createCloudDirectoryUser) vornehmen.

2. Überprüfen Sie die E-Mail-Adresse der Benutzer, um ihre Identität auf eine der folgenden Arten zu bestätigen:

  * Wenn Sie eine Benutzeridentität per E-Mail überprüfen möchten, setzen Sie **E-Mail-Verifizierung** auf der Registerkarte **Cloud Directory** des Service-Dashboards auf **Ein**. Wenn ein Benutzer von Ihnen hinzugefügt wird und sich in Ihrer App anmeldet, ohne vorher seine E-Mail zu verifizieren, wird die Anmeldung erfolgreich abgeschlossen, aber das vordefinierte Attribut wird gelöscht.
  * Um die Benutzer manuell zu verifizieren, müssen Sie ein Administrator sein und die [Management-APIs](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.createCloudDirectoryUser) von Cloud Directory verwenden. Wenn Sie einen Benutzer erstellen oder aktualisieren, müssen Sie das Feld `Status` explizit in den Nutzdaten Ihrer Benutzerdaten auf `CONFIRMED` setzen.

**Gibt es etwas Besonderes, das ich bei der Verwendung eines angepassten Identitätsproviders tun muss?**

Wenn Sie Ihrer Anwendung Benutzerinformationen vorab hinzufügen, können Sie jede eindeutige ID verwenden, die vom Authentifizierungsablauf bereitgestellt wird. Die ID muss mit dem `sub` (Subjekt) des signierten JSON Web Token, das während der Autorisierungsanforderung gesendet wird, _exakt_ übereinstimmen. Wenn die ID nicht übereinstimmt, wird das Profil, das hinzugefügt werden soll, nicht erfolgreich verknüpft.



## Benutzerinformationen zu Ihrer App hinzufügen
{: #preregister-add-info}

Nachdem Sie sich nun über den Prozess und die Auswirkungen auf die Sicherheit informiert haben, versuchen Sie, einen Benutzer hinzuzufügen.

**Vorbereitungen:**

Wenn Sie angepasste Attribute für einen bestimmten Benutzer mit dem [Management-API-Endpunkt /users](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Users/mgmt.users_search_user_profile) hinzufügen möchten, benötigen Sie die folgenden Informationen:

* Den Identitätsprovider, den der Benutzer verwenden möchte, um sich anzumelden.
* Die eindeutige ID des Benutzers, die vom Identitätsprovider bereitgestellt wird.

Wenn sich ein Benutzer zum ersten Mal bei Ihrer App anmeldet, sucht {{site.data.keyword.appid_short_notm}} nach dem Benutzer. Wenn er gefunden wird, übernimmt der Benutzer die Identität, die Sie zugeordnet haben. Wenn der Benutzer nicht gefunden wird, wird ein neuer Benutzer auf der Basis der vom Identitätsprovider zur Verfügung gestellten Informationen erstellt.

**So fügen Sie einen Benutzer hinzu:**

1. Melden Sie sich bei IBM Cloud an.
  ```
  ibmcloud login
  ```
  {: pre}

2. Suchen Sie Ihr IAM-Token, indem Sie den folgenden Befehl ausführen.
  ```
  ibmcloud iam oauth-tokens
  ```
  {: pre}

3. Stellen Sie eine POST-Anforderung an den Endpunkt `/users`, der eine Beschreibung des Benutzers und der Attribute enthält, die Sie als JSON-Objekt festlegen möchten.

  Header:
  ```
  POST {management-url}/management/v4/{tenantId}/users
       Host: <management-server-url>
       Authorization: 'Bearer <IAM_TOKEN>'
       Content-Type: application/json
  ```
  {: pre}

  Hauptteil:
  ```
   {
       "idp": "<Identity Provider>",
       "idp-identity": "<User's unique identifier>",
       "profile": {
           "attributes": {
             "mealPreference":"vegeterian"
           }
       }
   }
  ```
  {: pre}

  <table>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Informationen zu den Komponenten</th>
    </thead>
    <tbody>
      <tr>
        <td><code><em>idp</em></code></td>
        <td>Der Identitätsprovider, mit dem sich der Benutzer authentifiziert. Mögliche Optionen: `saml`, `cloud_directory`, `facebook`, `google`, `appid_custom`, `ibmid`.</td>
      </tr>
      <tr>
        <td><code><em>idp-identity</em></code></td>
        <td>Die eindeutige ID, die vom Identitätsprovider bereitgestellt wird.</td>
      </tr>
      <tr>
        <td><code><em>profile</em></code></td>
        <td>Das Profil des Benutzers, das die JSON-Zuordnung des angepassten Attributs enthält.</td>
      </tr>
    </tbody>
  </table>

  Beispielanforderung:
  ```
  $ curl --request POST \
       --url 'https://{Management_URI}/users \
       --header 'Authorization: Bearer {IAM_TOKEN}' \
       --header 'Content-Type: application/json' \
       --data '{"idp": "saml", "idp-identity": "user@ibm.com", "profile": { "attributes": { "role": "admin",
       "frequent_flyer_points": 1000 }}}'
  ```
  {: screen}

3. Stellen Sie mit einer der folgenden Methoden sicher, dass die Registrierung erfolgreich war:
  * Überprüfen Sie, ob die Benutzer-ID in der Antwort enthalten ist.
    ```
    {
        "id": "<{{site.data.keyword.appid_short_notm}} User Id>"
    }
    ```
    {: screen}
  * Überprüfen Sie, ob das Benutzerprofil erstellt wurde.

Beachten Sie, dass die vordefinierten Attribute eines Benutzers bis zur ersten Authentifizierung leer sind, der Benutzer aber für alle Zwecke ein vollständig authentifizierter Benutzer ist. Sie können ihre eindeutige ID genauso verwenden wie jemand, der bereits angemeldet ist. Beispielsweise können Sie das Profil ändern, suchen oder löschen.

Nachdem Sie nun einem Benutzer bestimmte Attribute zugeordnet haben, versuchen Sie, auf [Attribute zuzugreifen oder Attribute zu aktualisieren](/docs/services/appid?topic=appid-custom-attributes).


</br>
