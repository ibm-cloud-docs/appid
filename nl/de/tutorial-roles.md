---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-09"

keywords: Authentication, authorization, identity, app security, secure, access management, roles, attributes, users

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


# Lernprogramm: Benutzerrollen festlegen
{: #tutorial-roles}

Beim Codieren Ihrer Anwendung ist die Aufgabe, die richtigen Personen auszuwählen und diesen die richtigen Zugriffsberechtigungen zum richtigen Zeitpunkt zuzuordnen, mitunter nicht einfach. Um Ihnen diesen Prozess zu erleichtern, können Sie {{site.data.keyword.appid_full}} verwenden, um ein angepasstes Attribut wie z. B. `role` zu definieren, das die Zuordnung unterschiedlicher Benutzertypen ermöglicht. Anschließend können Sie Ihre Anwendung benutzen, um die Verwendung verschiedener Berechtigungsebenen für jeden Benutzertyp durchzusetzen. Mithilfe dieser in einzelne Arbeitsschritte aufgegliederten Anleitung erlernen Sie das Festlegen von Benutzerattributen, deren Aktualisierung und die Einfügung dieser Attribute in ein Token mithilfe der {{site.data.keyword.appid_short_notm}}-APIs.
{: shortdesc}

Sie haben noch keine Kenntnisse in der API-Benutzung? Dann testen Sie sie mit dieser [Postman-Gruppe](https://github.com/ibm-cloud-security/appid-postman).
{: tip}

## Szenario
{: #roles-scenario}

Sie sind als Entwickler für einen fiktiven Themenpark tätig. Ihre Aufgabe ist die Zugriffsverwaltung für die [Webanwendung](/docs/services/appid?topic=appid-web-apps) und Sie sind der Überzeugung, dass diese Aufgabe am einfachsten durch das Festlegen von Rollen für jeden Benutzertyp ausgeführt werden kann. Sie verfügen über unterschiedliche Rollentypen wie beispielsweise Parkmitarbeiter und Besucher, die ganz unterschiedliche Berechtigungsstufen benötigen. Sie möchten den Prozess optimieren und sicherstellen, dass Ihren Benutzern schon bei der ersten Anmeldung bei Ihrer Anwendung die korrekte Rolle zugeordnet wird.  
{: shortdesc}

Kein Problem! Sie können die [Funktion für angepasste Attribute](/docs/services/appid?topic=appid-profiles) von {{site.data.keyword.appid_short_notm}} verwenden, um einen beliebigen Typ von benutzerbezogenen Informationen zu speichern. Da Sie mit der rollenbasierten Zugriffssteuerung arbeiten, können Sie ein Attribut erstellen, das die Bezeichnung `role` trägt und diesem Attribut unterschiedliche Werte zuordnen, um den Typ der Rolle anzugeben. Der Themenpark verfügt beispielsweise über die Rollen `visitors` (Besucher) oder `staff` (Mitarbeiter), die beide als unterschiedliche Werte für das Attribut `role` angegeben werden können. Anschließend können Sie sicherstellen, dass Ihr Anwendungscode die Verwendung der Zugriffsrichtlinien und Berechtigungen erzwingt, die Sie zugeordnet haben.

Obwohl dieses Lernprogramm speziell für Web-Apps und Cloud Directory geschrieben wurde, können die Attribute auch in anderen Bereichen eingesetzt werden. Angepasste Attribute können für jedes von Ihnen gewünschte Element erstellt werden. Solange Sie nicht mehr als 100000 Attribute definieren und sie als einfache JSON-Objekte formatieren, können Sie jeden beliebigen Informationstyp speichern!
{: note}


## Vorbereitungen
{: #roles-before}

Bereit? Jetzt kann es losgehen!

Vergewissern Sie sich, dass die folgenden vorausgesetzten Komponenten vorhanden sind, bevor Sie beginnen:
- Eine Instanz des {{site.data.keyword.appid_short_notm}}-Service
- Die erforderlichen Serviceberechtigungsnachweise
- Eine E-Mail-Adresse, auf die Sie zugreifen und die Sie validieren können


## Schritt 1: {{site.data.keyword.appid_short_notm}}-Instanz konfigurieren
{: #roles-configure-app}

Bevor Sie mit dem Hinzufügen von Attributen für Ihre Cloud Land-Benutzer beginnen können, müssen Sie Ihre Instanz von {{site.data.keyword.appid_short_notm}} konfigurieren.
{: shortdesc}

1. Aktivieren Sie auf der Registerkarte **Identitätsprovider** des Service-Dashboards die Option **Cloud Directory**. Obwohl dieses Lernprogramm mit [Cloud Directory](/docs/services/appid?topic=appid-cloud-directory) arbeitet, können Sie auch einen der anderen Identitätsprovider wie beispielsweise [SAML](/docs/services/appid?topic=appid-enterprise), [Facebook](/docs/services/appid?topic=appid-social#facebook), [Google](/docs/services/appid?topic=appid-social#google) oder einen [angepassten Provider](/docs/services/appid?topic=appid-custom-identity) verwenden.

2. Aktivieren Sie auf der Registerkarte **Cloud Directory > E-Mail-Verifizierung** die Verifizierung und legen Sie für **Benutzern die Anmeldung bei Ihrer App ohne vorherige Verifizierung ihrer E-Mail-Adresse erlauben** die Einstellung **Nein** fest. Wenn Sie angepasste Attribute verwenden, um berechtigungsbezogene Rollen festzulegen, dann stellen Sie sicher, dass Benutzer ihre Identität validieren müssen, bevor sie die Attribute verwenden können, die Sie festgelegt haben.

3. Legen Sie auf der Registerkarte **Profile** für **Angepasste Attribute in der App ändern** die Einstellung **Inaktiviert** fest.

  Standardmäßig können angepasste Attribute von jedem Benutzer mit einem Zugriffstoken geändert werden. Zur Sicherstellung der Anwendungssicherheit müssen Sie {{site.data.keyword.appid_short_notm}} so konfigurieren, dass angepasste Attribute nur vom Administrator oder vom Eigner der App geändert werden können. Dadurch wird verhindert, dass Benutzer eigene angepasste Attribute ändern und sich selbst die Berechtigungen erteilen können, die nicht für sie vorgesehen sind.
  {: important}

Ausgezeichnet! Ihr Dashboard ist konfiguriert und Sie sind bereit, um Rollen zu definieren.


## Schritt 2: Rollen im Namen eines anderen Benutzers vor dem Anmelden festlegen
{: #roles-set-before}

Cloud Land hat nun einen neuen Mitarbeiter! Sie verfügen über alle seine Daten, sein erster Arbeitstag ist jedoch erst in einigen Tagen. Sie können den neuen Mitarbeiter [vorab registrieren](/docs/services/appid?topic=appid-preregister), indem Sie einen {{site.data.keyword.appid_short_notm}}-Benutzer und ein entsprechendes Profil erstellen, das die Attribute wie z. B. die Rolle `staff` enthält.
{: shortdesc}

Bei diesem Prozess wird die Cloud Directory-Registrierung nicht abgeschlossen. Der Benutzer muss sich weiterhin für die App anmelden, um das Attribut in dem Profil zu übernehmen, das Sie erstellen.
{: tip}

1. Melden Sie sich über die Befehlszeilenschnittstelle bei {{site.data.keyword.cloud_notm}} an.

  ```
  ibmcloud login
  ```
  {: codeblock}

2. Fordern Sie ein IAM-Zugriffstoken an.

  ```
  ibmcloud iam oauth-tokens
  ```
  {: codeblock}

3. Setzen Sie eine POST-Anforderung ab, um ein Benutzerprofil für den neuen Benutzer zu erstellen, das das Attribut `staff` enthält. Vergewissern Sie sich, dass Sie auf die verwendete E-Mail-Adresse zugreifen und diese validieren können.

  ```
  curl --request POST \
  https://us-south.appid.cloud.ibm.com/management/v4/{{APPID_TENANT_ID}}/users \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  - d '{
    "idp": "cloud_directory",
    "idp-identity": “user@email.com“,
    "profile": {
      "attributes": {
        “role”: “staff”
      }
    }
  }'
  ```
  {: codeblock}

  Ausgabe für eine erfolgreiche Antwort:

  ```
  {
      "id": "5ty78b09-1356-4py8-l45p-808l633101zz"
  }
  ```
  {: screen}

6. Überprüfen Sie, ob das Profil mit der Rolle `staff` erstellt wurde.

  ```
  curl --request GET \
  https://us-south.appid.cloud.ibm.com/management/v4/<tenant-ID>/users?email=<user-email> \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  ```
  {: codeblock}

  Hauptteil für eine erfolgreiche Antwort:

  ```
  {
      "users": [
          {
              "idp": "nominated_cloud_directory",
              "id": "5ty78b09-1356-4py8-l45p-808l633101zz"
          }
      ]
  }
  ```
  {: screen}

Gut gemacht! Sie haben einen Benutzer für Ihre Anwendung vorab registriert. Wenn sich dieser neue Benutzer nun mit der von Ihnen für die Vorabregistrierung verwendeten ID anmeldet, dann wird ein Cloud Directory-Benutzer erstellt, der das {{site.data.keyword.appid_short_notm}}-Benutzerprofil übernimmt. Als Nächstes werden Sie erfahren, wie Attribute aktualisiert werden können.


## Schritt 3: Benutzerattribute aktualisieren
{: #roles-update-attributes}

Cloud Land expandiert! Um dem Wachstum gerecht zu werden, stellt Ihr Unternehmen neue Mitarbeiter ein. Der Benutzer mit der Rolle `staff` aus Schritt 2 ist nun Manager geworden. Sie können sein Profil aktualisieren, indem Sie eine [neue Rolle zuordnen](/docs/services/appid?topic=appid-profiles#profile-set-custom).
{: shortdesc}

1. Aktualisieren Sie das Profil.

  ```
  curl --request PUT \
  https://us-south.appid.cloud.ibm.com/management/v4/<tenant-id>/users/<user-id>/profile \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  - d '{
    "profile": {
      "attributes": {
        “role”: “manager”
      }
    }
  }'
  ```
  {: codeblock}

3. Zeigen Sie das Profil an, um sicherzustellen, dass es ordnungsgemäß aktualisiert wurde.

  ```
  curl --request POST \
  GET https://us-south.appid.cloud.ibm.com/management/v4/{{APPID_TENANT_ID}}/users/{{user_profile_id}}/profile \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  ```
  {: codeblock}

  Ausgabe für eine erfolgreiche Antwort:

  ```
  {
      "id": "5ce78e09-1356-4ef8-a45d-808b633101db",
      "identities": [],
      "attributes": {
          "role": "manager"
      }
  }
  ```
  {: screen}

Ganz hervorragend!


## Schritt 4: Attribute in Tokens einfügen
{: #roles-map-claims}

Der Themenpark wird immer beliebter und expandiert weiter! Aufgrund der großen Zahl neuer Besucher und Mitarbeiter möchten Sie die Anzahl der abgesetzten Anforderungen begrenzen. Um die Leistung zu verbessern, können Sie Ihren Claims für Zugriffs- und Identitätstokens Benutzerprofilattribute zuordnen. Durch die Zuordnung angepasster Claims können Sie die angepassten Attribute direkt in den Tokens speichern.
{: shortdesc}

Die [Tokenkonfiguration](/docs/services/appid?topic=appid-customizing-tokens#customizing-tokens) gilt global. Dies bedeutet, dass sie für jeden Benutzer angewendet wird, der über das Attribut `role` verfügt, und zwar unabhängig von der tatsächlichen Rolle, die zugeordnet wurde.
{: tip}


1. Setzen Sie eine Anforderung an den Endpunkt für die Tokenkonfiguration ab.

  ```
  curl --request PUT \
  https://us-south.appid.cloud.ibm.com/management/v4/{{APPID_TENANT_ID}}/config/tokens \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  - d '{
      "access": {
          "expires_in": 3601
      },
      "refresh": {
          "enabled": false,
          "expires_in": 2592001
      },
      "anonymousAccess": {
          "expires_in": 2592001
      },
      "accessTokenClaims": [
      {
      "source": "attributes",
      "sourceClaim": "role"
      }
      ]
  }'
  ```
  {: codeblock}

  <table>
    <tr>
      <th>Variable</th>
      <th>Beschreibung</th>
    </tr>
    <tr>
      <td><code>tenant-id</code></td>
      <td>Eine Tenant-ID dient zur Identifikation Ihrer {{site.data.keyword.appid_short_notm}}-Instanz in der Anforderung. Sie finden Ihre ID auf der Registerkarte <em>Serviceberechtigungsnachweise</em> des Dashboards. Wenn Sie nicht über eine entsprechende Gruppe verfügen, dann können Sie die Schritte in der GUI ausführen, um die Berechtigungsnachweise zu erstellen.</td>
    </tr>
    <tr>
      <td><code>source</code></td>
      <td>Legen Sie sowohl für <code>accessTokenClaim</code> als auch für <code>idTokenClaims</code> als Quelle <code>attribute</code> fest.</td>
    </tr>
    <tr>
      <td><code>sourceClaim</code></td>
      <td>Legen Sie sowohl für <code>accessTokenClaim</code> als auch für <code>idTokenClaims</code> als Claimquelle <code>role</code> fest.</td>
    </tr>
    <tr>
      <td><code>expires_in</code></td>
      <td>Dieser Wert gilt für jeden Tokentyp und muss in jeder Anforderung festgelegt werden. Wenn Sie den Wert zuvor in der GUI festgelegt und dann diese Anforderung ausgeführt haben, dann überschreiben die Werte in der Anforderung die zuvor festgelegten Werte. Beachten Sie hierbei unbedingt, dass für das Ablaufdatum der korrekte Wert für Ihre Konfiguration festgelegt werden muss.</td>
    </tr>
  </table>

  Ausgabe für eine erfolgreiche Antwort:

  ```
  {
      "access": {
          "expires_in": 3601
      },
      "refresh": {
          "enabled": false,
          "expires_in": 2592001
      },
      "anonymousAccess": {
          "expires_in": 2592001
      },
      "accessTokenClaims": [
      {
      "source": "attributes",
      "sourceClaim": "role"
      }
      ]
  }
  ```
  {: screen}


## Schritt 5: Zugriffstoken anzeigen
{: #roles-view-token}

Optional können Sie überprüfen, ob Schritt 4 erfolgreich war, indem Sie ein Zugriffstoken anzeigen.
{: shortdesc}

1. Erstellen Sie zu Testzwecken mit der GUI von {{site.data.keyword.appid_short_notm}} einen Cloud Directory-Benutzer.

  1. Klicken Sie auf der Registerkarte **Benutzer** auf **Benutzer hinzufügen**. Daraufhin wird ein Formular angezeigt.
  2. Geben Sie einen Vor- und Nachnamen, eine E-Mail-Adresse sowie ein zugehöriges Kennwort ein.
  3. Klicken Sie auf **Speichern**.

2. Verschlüsseln Sie die Client-ID und den geheimen Schlüssel.

  1. Kopieren Sie auf der Registerkarte **Serviceberechtigungsnachweise** der GUI von {{site.data.keyword.appid_short_notm}} Ihre Client-ID und den geheimen Schlüssel.
  2. Verwenden Sie einen Base64-Encoder, um Ihre Autorisierungsinformationen zu verschlüsseln.
  3. Kopieren Sie die zu verwendende Ausgabe in den folgenden Befehl.

4. Melden Sie sich über die APIs an, um die Informationen für das Zugriffstoken abzurufen. Das zurückgegebene Token ist verschlüsselt.

  ```
  curl --request PUT \
  https://appid.cloud.ibm.com/oauth/v4/<tenant-ID>/token \
  --header 'Authorization: Basic <encoded-clientID>:<encoded-client-secret>' \
  --header 'Content-Type: application/x-www-form-urlencoded' \
  --header `Accept: application/json`
  - d 'grant_type=password&username=<user-email>%40<user-email-domain>&password=<user-password>
  ```
  {: codeblock}

5. Entschlüsseln Sie Ihr Zugriffstoken.
  1. Kopieren Sie das Token in die Antwortausgabe des vorherigen Befehls.
  2. Navigieren Sie in einem Browser zu https://jwt.io/.
  3. Fügen Sie das Token in das Feld **Verschlüsselt** ein.

6. Überprüfen Sie im Abschnitt **Entschlüsselt**, ob die Rolle angezeigt wird.

  ```
  {
    "iss": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61",
    "exp": 1551903163,
    "aud": [
      "968c2306-9aef-4109-bc06-4f5ed6axi24a"
    ],
    "sub": "2b96cc04-eca5-4122-a8de-6e07d14c13a5",
    "email_verified": true,
    "amr": [
      "cloud_directory"
    ],
    "iat": 1551899553,
    "tenant": "39a37f57-a227-4bfe-a044-93b6e6050a61",
    "scope": "openid appid_default appid_readprofile appid_readuserattr appid_writeuserattr appid_authenticated"
    "role": "manager"
  }
  ```
  {: screen}



## Nächste Schritte
{: #roles-next}

Gute Arbeit! Sie haben das Lernprogramm abgeschlossen. Als Nächstes können Sie versuchen, die [Mehrfaktorauthentifizierung](/docs/services/appid?topic=appid-cd-mfa) zu konfigurieren oder eine eigene [angepasste GUI Ihres Unternehmens](/docs/services/appid?topic=appid-branded) einzurichten.
