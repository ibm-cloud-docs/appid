---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-31"

keywords: authentication, authorization, identity, app security, secure, custom, tokens, access, claim, attributes

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


# Tokens anpassen
{: #customizing-tokens}

Sie können ein {{site.data.keyword.appid_short_notm}}-Token so konfigurieren, dass es den spezifischen Anforderungen der Anwendung entspricht.
{: shortdesc}

## Informationen zur Anpassung
{: #understanding-customization}

{{site.data.keyword.appid_short_notm}} verwendet verschiedene Arten von Tokens zum Schutz Ihrer Anwendungen.

* Zugriffstokens - aktivieren die Kommunikation mit Back-End-Ressourcen, die durch Autorisierungsfilter geschützt sind. Wenn ein Zugriffstoken nicht einem bestimmten Benutzer zugeordnet ist, hat das Token eine eingeschränkte Funktionalität.
* Identitätstokens - enthalten persönliche Informationen und werden zur Authentifizierung eines Benutzers verwendet. Abhängig von Ihrer App-Konfiguration können Identitätstokens ausgegeben werden, bevor ein Benutzer authentifiziert wird. Auf diese Weise können Sie beginnen, Ihren Benutzern Attribute zuzuordnen, bevor sie sich bei Ihrer Anwendung anmelden.
* Aktualisierungstokens - können verwendet werden, um die Zeit zu verlängern, für die ein Benutzer ohne erneute Authentifizierung zugreifen kann.

Möchten Sie einen Authentifizierungskontext festlegen? Weitere Informationen hierzu finden Sie unter [Informationen zu Token](/docs/services/appid?topic=appid-tokens#tokens).
{: tip}


Sie können Ihre Tokens [in der GUI](/docs/services/appid?topic=appid-customizing-tokens#configuring-tokens-ui) oder mithilfe [der API](/docs/services/appid?topic=appid-customizing-tokens#configuring-tokens-api) anpassen, indem Sie die Gültigkeitsdauer festlegen oder angepasste Claims zu Ihren Tokens hinzufügen. Der folgenden Tabelle können Sie entnehmen, wie die Lebensdauer konfiguriert wird, oder lesen Sie weiter, um Informationen zur Zuordnung von angepassten Attributen zu erhalten.

<table>
  <tr>
    <th>Tokentyp</th>
    <th>Werttyp</th>
    <th>Standard</th>
    <th>Optionen</th>
  </tr>
  <tr>
    <td>Zugriffstoken</td>
    <td>Minuten</td>
    <td>60</td>
    <td>Beliebiger Wert zwischen 5 und 1440</td>
  </tr>
  <tr>
    <td>Identitätstoken</td>
    <td>Minuten</td>
    <td>60</td>
    <td>Beliebiger Wert zwischen 5 und 1440</td>
  </tr>
  <tr>
    <td>Aktualisierungstoken</td>
    <td>Tage</td>
    <td>30</td>
    <td>Beliebiger Wert zwischen 1 und 9</td>
  </tr>
  <tr>
    <td>Anonymes Token</td>
    <td>Tage</td>
    <td>30</td>
    <td>Beliebiger Wert zwischen 1 und 9</td>
  </tr>
</table>


Da Tokens verwendet werden, um Benutzer zu identifizieren und Ihre Ressourcen zu schützen, hat die Lebensdauer eines Tokens unterschiedliche Auswirkungen. Durch das Anpassen Ihrer Tokenkonfiguration können Sie sicherstellen, dass Ihre Anforderungen hinsichtlich Sicherheit und Bedienungskomfort erfüllt werden. Sollte ein Token aber in die falschen Hände geraten, hat ein unbefugter Benutzer mehr Zeit, Ihre Anwendung zu beeinträchtigen. Weitere Informationen zu Sicherheitsaspekten finden Sie in [Angepasste Attribute festlegen](/docs/services/appid?topic=appid-profiles#profile-set-custom).
{: important}


## Informationen zu angepassten Attributen und Anforderungen (Claims)
{: #custom-claims}

Sie können Benutzerprofilattribute Ihren Anforderungen (sog. Claims) für Zugriffs- und Identitätstokens zuordnen. Dies bedeutet, dass Sie nicht zum [Endpunkt /userinfo](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Authorization_Server_V4/userInfo) wechseln oder angepasste Attribute später extrahieren müssen, da sie bereits in den Tokens gespeichert sind.
{: shortdesc}

### Was ist ein Claim?
{: #custom-claims-defined}

Ein Claim ist eine Erklärung, die von einer Entität zu sich selbst oder für eine andere Person abgegeben wird. Wenn Sie sich beispielsweise bei einer Anwendung mithilfe eines Identitätsproviders angemeldet haben, dann sendet der Provider der Anwendung eine Gruppe von Claims oder Erklärungen zu Ihrer Person, die diese Anwendung zusammen mit den Informationen, die bereits für Sie gespeichert wurden, in eine Gruppe einordnen kann. Auf diese Weise wird die App bei Ihrer Anmeldung mit Ihren Informationen eingerichtet, und zwar in der Art und Weise, in der Sie sie konfiguriert haben. Im folgenden Beispiel wird dargestellt, wie das JSON-Objekt formatiert werden muss.

```
{
  "accessTokenClaims": [
            {
      "source": "saml",
      "sourceClaim": "moderator"
    }
  ],
       "idTokenClaims": [
           {
      "source": "saml",
      "sourceClaim": "moderator"
    }
  ],
  "access": {
    "expires_in": 3600
  },
  "refresh": {
    "expires_in": 2592000,
    "enabled": true
  },
  "anonymousAccess": {
    "expires_in": 2592000,
    "enabled": true
  }
}
```
{: screen}

Wenn Sie die Informationen zum Ablauf der Gültigkeit Ihres Tokens angepasst haben, dann müssen Sie sie in jeder Anforderung festlegen. Andernfalls überschreibt diese Anforderung Ihre aktuelle Konfiguration und für alle nicht definierten Elemente wird der Standardwert verwendet.
{: note}

### Warum sollte ich Claims zu meinen Tokens hinzufügen?
{: #why-custom-claims}

Zusätzliche Netzaufrufe sind nicht erforderlich, da alle Informationen, die Ihre App über einen Benutzer und seine Berechtigungen benötigt, bereits im Token enthalten sind. Wenn Sie nicht über sehr große Datenmengen verfügen, können Sie so effizienter arbeiten. Darüber hinaus können Sie die Integrität dieser zugeordneten Attribute sicherstellen, wenn sie über das Netz gesendet werden, weil sie in einem signierten Token gespeichert sind.


### Welche Arten von Claims kann ich definieren?
{: #custom-claim-types}

Die Claims, die von {{site.data.keyword.appid_short_notm}} zur Verfügung gestellt werden, lassen sich mehreren Kategorien zuordnen, die sich durch den Grad der Anpassung unterscheiden.

*Registrierte Claims*: Es gibt bestimmte Claims in den Zugriffs- und Identitätstokens, die von {{site.data.keyword.appid_short_notm}} definiert werden und nicht durch angepasste Zuordnungen überschrieben werden können. Wenn Ihr Claim eingeschränkt ist, wird er vom Service ignoriert. Die Claims sind `iss`, `aud`, `sub`, `iat`, `exp`, `amr` und `tenant`.

*Eingeschränkte Claims*: Abhängig von dem Token, dem die Claims zugeordnet sind, haben einige Claims nur eingeschränkte Anpassungsmöglichkeiten. Für ein Zugriffstoken ist `scope` der einzige eingeschränkte Claim. Eine Überschreibung durch angepasste Zuordnungen ist nicht möglich, er kann jedoch mit Ihren eigenen Bereichen (Scopes) erweitert werden. Wenn die Bereichsanforderung (sog. Scope Claim) einem Zugriffstoken zugeordnet wird, muss der Wert eine Zeichenfolge sein und darf nicht das Präfix `appid_` haben, da er sonst ignoriert wird. In Identitätstokens können die Claims `identities` und `oauth_clients` nicht geändert oder überschrieben werden.

*Normalisierte Claims*: Jedes Identitätstoken enthält eine Reihe von Claims, die von {{site.data.keyword.appid_short_notm}} als normalisierte Claims erkannt werden. Wenn sie verfügbar sind, werden sie dem Token direkt von Ihrem Identitätsprovider zugeordnet. Diese Claims können nicht explizit ausgelassen werden, sie können aber durch angepasste Claims im Token außer Kraft gesetzt werden. Die Claims umfassen `name`, `email`, `picture`, `local` und `gender`. Hinweis: Hierdurch wird nicht das Attribut geändert oder gelöscht, sondern die Informationen geändert, die im Token zur Laufzeit vorhanden sind.



### Wie werden Claims bestimmten Tokens zugeordnet?
{: #custom-claims-mapping}

Jede Zuordnung wird durch ein Datenquellenobjekt und einen Schlüssel definiert, der zum Abrufen des Claims verwendet wird. Die einzelnen angepassten Claims werden für jedes Token separat festgelegt und nacheinander angewendet. Sie können bis zu 100 Claims für jedes Token bis zu einem Nutzdatenmaximum von 100 KB registrieren.

<table>
    <thead>
      <th colspan=3><img src="images/idea.png" alt="Ideensymbol"/> Informationen zu Claimzuordnungsobjekten</th>
    </thead>
    <tbody>
      <tr>
        <td><code><em>source</em></code></td>
        <td>Erforderlich</td>
        <td>Definiert die Quelle des Claims. Dies kann sich auf die Benutzerinformationen des Identitätsproviders oder die angepassten {{site.data.keyword.appid_short_notm}}-Attribute des Benutzers beziehen. </br> Mögliche Optionen: `saml`, `cloud_directory`, `facebook`, `google`, `appid_custom`, `ibmid` und `attributes`.</td>
      </tr>
      <tr>
        <td><code><em>sourceClaim</em></code></td>
        <td>Erforderlich</td>
        <td>Definiert den Claim der Quellendaten. </td>
      </tr>
    </tbody>
  </table>

Sie können in Ihren Zuordnungen auf verschachtelte Anforderungen (sog. Nested Claims) verweisen, indem Sie die Punktsyntax verwenden. Beispiel: `nested.attribute`
{:tip}

</br>

## {{site.data.keyword.appid_short_notm}}-Tokens konfigurieren
{: #configuring-tokens}

Sie können Ihre {{site.data.keyword.appid_short_notm}}-Tokens unter Verwendung der GUI oder der Management-APIs konfigurieren.
{: shortdesc}


### Tokenlebensdauer mit der GUI konfigurieren
{: #configuring-tokens-ui}

1. Navigieren Sie zu Ihrem Service-Dashboard.
2. Wählen Sie im Abschnitt **Identitätsprovider** in der Navigation die Seite **Verwalten** aus.
3. Konfigurieren Sie die Tokens auf der Registerkarte **Einstellungen**.
  1. Um eine Anmeldung ohne Benutzerinteraktion zu ermöglichen, setzen Sie **Aktualisierungstoken** auf **Ein**.
  2. Legen Sie die Lebensdauer des Aktualisierungstokens fest. Die Ablaufzeit wird in Tagen festgelegt und kann ein beliebiger Wert im Bereich von 1 bis 90 sein. Je kleiner die Zahl ist, um so häufiger muss sich ein Benutzer anmelden.
  3. Legen Sie die Lebensdauer Ihres Zugriffstokens fest. Die Ablaufzeit wird in Minuten festgelegt und kann im Bereich von 5 bis 1440 liegen. Je kleiner der Wert ist, umso höher ist der Schutz, den Sie im Fall eines Tokendiebstahls haben.
  4. Legen Sie die Lebensdauer des anonymen Tokens fest. Ein [anonymes Token](/docs/services/appid?topic=appid-anonymous#anonymous) wird den Benutzern zugewiesen, sobald sie beginnen, mit Ihrer App zu interagieren. Wenn sich ein Benutzer anmeldet, werden die Informationen in dem anonymen Token an das Token übertragen, das dem Benutzer zugeordnet ist. Die Ablaufzeit wird in Tagen festgelegt und kann ein beliebiger Wert zwischen 1 und 90 sein.

</br>

### Tokens mit den Management-APIs konfigurieren
{: #configuring-tokens-api}

**Vorbereitungen**

Stellen Sie sicher, dass die folgenden Anforderungen erfüllt werden:

* Die Tenant-ID Ihrer {{site.data.keyword.appid_short_notm}}-Instanz. Diese finden Sie im Abschnitt **Serviceberechtigungsnachweise** der GUI.
* Ihr IAM-Token (Identity and Access Management). Hilfe zum Abrufen eines IAM-Tokens finden Sie in der [IAM-Dokumentation](/docs/iam?topic=iam-iamtoken_from_apikey).

**Claims zuordnen**

1. Stellen Sie eine PUT-Anforderung an den Endpunkt `/config/tokens` mit Ihrer Tokenkonfiguration.

  Header:
  ```
  PUT {management-url}/management/v4/{tenantId}/tokens
       Host: <management-server-url>
       Authorization: 'Bearer <IAM_TOKEN>'
       Content-Type: application/json
  ```
  {: codeblock}

  Hauptteil:
  ```
   {
       "access": {
           "expires_in": 3600,
       },
       "refresh": {
           "expires_in": 2592000,
           "enabled": true
       },
       "anonymous": {
           "expires_in": 2592000,
           "enabled": true
       },
       "accessTokenClaims": [
           {
              "source": "saml",
              "sourceClaim": "name_id"
           }
       ],
       "idTokenClaims": [
           {
              "source": "saml",
              "sourceClaim": "attributes.uid"
           }
       ]
   }
  ```
  {: codeblock}

  <table>
    <thead>
      <th colspan=3><img src="images/idea.png" alt="Ideensymbol"/> Informationen zur Tokenkonfiguration</th>
    </thead>
    <tbody>
      <tr>
        <td><code><em>access</em></code></td>
        <td>Optional</td>
        <td>Objekt mit der Ablaufzeit `expires_in` Ihres Zugriffs- und Identitätstokens (in Minuten). </br> </br> Die Standardablaufzeit beträgt 60 Minuten. </td>
      </tr>
      <tr>
          <td><code><em>refresh</em></code></td>
          <td>Optional</td>
          <td>Objekt, das die Ablaufzeit `expires_in` (in Tagen) des Aktualisierungstokens enthält. </br> </br> Die Standardablaufzeit beträgt 30 Tage. </td>
      </tr>
      <tr>
          <td><code><em>anonymousAccess</em></code></td>
          <td>Optional</td>
          <td>Objekt, das die Ablaufzeit `expires_in` (in Tagen) Ihres anonymen Zugriffs- und des Identitätstokens enthält. </br> </br> Die Standardablaufzeit beträgt 30 Tage.
      </tr>
      <tr>
          <td><code><em>accessTokenClaims</em></code></td>
          <td>Optional</td>
          <td>Ein Array, das die Objekte enthält, die erstellt werden, wenn Claims zugeordnet werden, die sich auf Zugriffstokens beziehen.</td>
      </tr>
      <tr>
          <td><code><em>idTokenClaims</em></code></td>
          <td>Optional</td>
          <td>Ein Array, das die Objekte enthält, die erstellt werden, wenn Claims zugeordnet werden, die sich auf Identitätstokens beziehen.</td>
      </tr>
    </tbody>
  </table>

  Beispielanforderung:
  ```
  $ curl -X PUT
    --header 'Content-Type: application/json'
    --header 'Accept: application/json'
    --header 'Authorization: <IAM Token'
    -d '{
          "accessTokenClaims": [
            {
              "source": "saml",
              "sourceClaim": "name_id"
            }
          ],
          "idTokenClaims": [
            {
              "source": "attributes",
              "sourceClaim": "theme"
            }
          ]
      }'
  }' '{management-url}/management/v4/{Tenant ID}/config/tokens'
  ```
  {: screen}
