---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-20"

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

# E-Mails anpassen
{: #cd-types}

Wenn ein Benutzer mit Ihrer Anwendung interagiert, kann es in bestimmten Situationen erforderlich sein, eine Antwort zu senden oder eine Verifizierung anzufordern. {{site.data.keyword.appid_short_notm}} stellt Standardvorlagen bereit, die Sie für die Interaktionen verwenden können. Außerdem können Sie die Vorlagen als Leitfaden und dazu verwenden, Ihre Nachrichtenübertragung an die individuellen Anforderungen Ihres Produktbereichs anzupassen.
{: shortdesc}

{{site.data.keyword.appid_short_notm}} verwendet <a href="https://www.sendgrid.com" target="_blank">SendGrid <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> als Mailzustellungsservice. Alle E-Mails werden über ein einzelnes SendGrid-Konto gesendet.
{: note}

## E-Mail-Vorlagen
{: #cd-messages}

Wenn Sie Nachrichten an Ihre Benutzer senden, können Sie eine beliebige Kombination der folgenden Vorlagen verwenden. Alternativ hierzu können Sie die Vorlagen bearbeiten, um Ihre Nachrichten anzupassen.
{: shortdesc}

Zusätzlich zu den folgenden Nachrichtentypen können Sie auch [SSO](/docs/services/appid?topic=appid-cd-sso#cd-sso)- und [MFA](/docs/services/appid?topic=appid-cd-mfa#cd-mfa)-Vorlagen nutzen.
{: tip}

Sie können Parameter in Ihren Nachrichten verwenden, um die Nachrichten weiter anzupassen. In der folgenden Tabelle finden Sie die Parameter, die Sie in den einzelnen Nachrichtentypen verwenden können.

<table>
  <tr>
    <th colspan=2><img src="images/idea.png" alt="Symbol für weitere Informationen"/> Alle Nachrichtenparameter </th>
  </tr>
  <tr>
    <td><code>%{display.logo}</code></td>
    <td> Zeigt das Bild an, das Sie für das Anmeldewidget konfiguriert haben.</td>
  </tr>
  <tr>
    <td><code>%{user.displayName}</code></td>
    <td> Zeigt den Anzeigenamen an, den ein Benutzer für die Interaktion mit der App ausgewählt hat.</td>
  </tr>
  <tr>
    <td><code>%{user.email}</code></td>
    <td> Zeigt die registrierte E-Mail-Adresse des Benutzers an.</td>
  </tr>
  <tr>
    <td><code>%{user.username}</code></td>
    <td> Zeigt den angegebenen Benutzernamen des Benutzers an, wenn die Verwendung von Benutzername und Kennwort als Authentifizierungsmethode festgelegt ist. </td>
  </tr>
  <tr>
    <td><code>%{user.firstName}</code></td>
    <td> Zeigt den angegebenen Vornamen des Benutzers an. </td>
  </tr>
  <tr>
    <td><code>%{user.formattedName}</code></td>
    <td> Zeigt den vollständigen Namen des Benutzers an. </td>
  </tr>
  <tr>
    <td><code>%{user.lastName}</code></td>
    <td> Zeigt den angegebenen Nachnamen des Benutzers an. </td>
  </tr>
</table>


### E-Mail: Willkommen
{: #cd-messages-welcome}

Wenn sich ein Benutzer für Ihre App registriert, dann möchten Sie ihm möglicherweise eine Nachricht senden, um ihn in Ihrer App willkommen zu heißen. 
{: shortdesc}

1. Navigieren Sie zur Registerkarte **Workflowvorlagen > Willkommens-E-Mail** des Service-Dashboards.

2. Legen Sie für **Willkommens-E-Mail** die Einstellung **Aktiviert** fest.

3. Passen Sie den Inhalt Ihrer Nachricht an. Über die Benutzerschnittstelle können Sie Parameter hinzu- und Bilder einfügen. Um die [Sprache](/docs/services/appid?topic=appid-cd-messages#cd-languages) der Nachricht zu ändern, können Sie über die <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">APIs <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> die gewünschte Sprache festlegen. Allerdings ist zu beachten, dass Sie für den Inhalt und die Übersetzung der Nachricht verantwortlich sind. In der folgenden Tabelle finden Sie die Liste der Tabellen, die Sie in dieser Nachricht und in allen anderen Nachrichten, die Sie senden können, verwenden können. Wenn ein Benutzer die vom Parameter abgefragte Information nicht angibt, wird im entsprechenden Feld kein Wert angezeigt.

4. Klicken Sie auf **Speichern**.


### E-Mail: Verifizierung
{: #cd-messages-verification}

Wenn sich ein Benutzer für Ihre Anwendung anhand seiner E-Mail-Adresse registriert, dann können Sie ihm eine Nachricht senden, um ihn zur Bestätigung seiner Identität aufzufordern. Indem Sie eine Verifizierung anfordern, begrenzen Sie die Anzahl der gefälschten Konten, die sich bei Ihrer App registrieren können. Sie können den Zugriff auf Ihre App einschränken, bis ein Benutzer seine E-Mail-Adresse verifiziert hat, oder Sie können auf diese Weise die Erstellung von Profilen für bestimmte Benutzer verwalten. Beachten Sie, dass Benutzer, die manuell über das {{site.data.keyword.appid_short_notm}}-Dashboard oder die API zum Erstellen von Benutzern hinzugefügt werden, diese E-Mail nicht automatisch erhalten.
{: shortdesc}


1. Navigieren Sie zur Registerkarte **Workflowvorlagen > E-Mail-Verifizierung** des Service-Dashboards.

2. Legen Sie für **E-Mail-Verifizierung** die Einstellung **Aktiviert** fest.

3. Legen Sie für **Benutzern die Anmeldung bei Ihrer App ohne vorheriges Verifizieren ihrer E-Mail-Adresse ermöglichen** die Einstellung **Ja** fest. Bei Verwendung der Einstellung 'Ja' können Benutzer mit Ihrer Anwendung interagieren, nachdem sie sich registriert, aber bevor sie ihre E-Mail-Adresse verifiziert haben. Die Standardeinstellung ist 'Nein'.

4. Passen Sie den Inhalt Ihrer Nachricht an. Über die Benutzerschnittstelle können Sie Parameter hinzu- und Bilder einfügen. Um die [Sprache](/docs/services/appid?topic=appid-cd-messages#cd-languages) der Nachricht zu ändern, können Sie über die <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">APIs <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> die gewünschte Sprache festlegen. Allerdings ist zu beachten, dass Sie für den Inhalt und die Übersetzung der Nachricht verantwortlich sind. In der folgenden Tabelle finden Sie die verschiedenen Parameter, die Sie in Ihrer Nachricht verwenden können. Wenn ein Benutzer die vom Parameter abgefragte Information nicht angibt, wird im entsprechenden Feld kein Wert angezeigt.

  <table>
    <tr>
      <th colspan=2><img src="images/idea.png" alt="Symbol für weitere Informationen"/> Parameter für Verifizierungsnachricht</th>
    </tr>
    <tr>
      <td><code>%{linkExpiration.hours}</code></td>
      <td> Zeigt die Anzahl der Stunden an, die der Link gültig ist. </td>
    </tr>
    <tr>
      <td><code>%{linkExpiration.minutes}</code></td>
      <td> Zeigt die Anzahl der Minuten an, die der Link gültig ist. </td>
    </tr>
    <tr>
      <td><code>%{verify.code}</code></td>
      <td> Zeigt eine einmalige Verifizierungs-URL an. </td>
    </tr>
    <tr>
      <td><code>%{verify.link}</code></td>
      <td> Zeigt die Aktions-URL an, die Sie in den Einstellungen angegeben haben. </td>
    </tr>
  </table>

  Sie können auch die Nachrichtenparameter verwenden, die im Abschnitt mit der [Willkommensnachricht](/docs/services/appid?topic=appid-cd-messages#cd-messages-welcome) aufgelistet werden.
  {: tip}

5. Definieren Sie eine Ablaufzeit für die Gültigkeit der Aktions-URL. Beim Ablauf der URL handelt es sich um die Zeitdauer (in Minuten), die ein Benutzer zur Verfügung hat, um die Aktion auszuführen, bevor die Gültigkeit des Verifizierungslinks abläuft. Diese Einstellung wirkt sich auch auf den Gültigkeitszeitraum Ihres Links zum Zurücksetzen des Kennworts aus.
 
6. Geben Sie eine URL für die Seite ein, die angezeigt werden soll, nachdem ein Benutzer seine E-Mail-Adresse im Feld für die **URL mit der Danke-Seite** verifiziert hat. Wenn Sie dieses Feld nicht ausfüllen, dann wird eine {{site.data.keyword.appid_short_notm}}-Standardseite angezeigt.

7. Klicken Sie auf **Speichern**. 


### E-Mail: Kennwort zurücksetzen
{: #cd-messages-reset}

Wenn ein Benutzer mit Ihrer App interagiert, dann vergisst er möglicherweise sein Kennwort oder es gibt andere Gründe, die eine Kennwortaktualisierung erforderlich machen. Sie können die E-Mail-Antwort auf diese Anforderung anpassen. Wenn ein Benutzer eine Kennwortänderung anfordert, wird das Kennwort erst dann geändert, wenn er auf den Link in dieser E-Mail klickt.
{: shortdesc}


1. Navigieren Sie zur Registerkarte **Workflowvorlagen > Kennwort zurücksetzen** des Service-Dashboards.

2. Legen Sie für **E-Mail für vergessenes Kennwort** die Einstellung **Aktiviert** fest.

3. Passen Sie den Inhalt Ihrer Nachricht an. Über die Benutzerschnittstelle können Sie Parameter hinzu- und Bilder einfügen. Um die [Sprache](/docs/services/appid?topic=appid-cd-messages#cd-languages) der Nachricht zu ändern, können Sie über die <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">APIs <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> die gewünschte Sprache festlegen. Allerdings ist zu beachten, dass Sie für den Inhalt und die Übersetzung der Nachricht verantwortlich sind. In der folgenden Tabelle finden Sie die verschiedenen Parameter, die Sie in Ihrer Nachricht verwenden können. Wenn ein Benutzer die vom Parameter abgefragte Information nicht angibt, wird im entsprechenden Feld kein Wert angezeigt.

  <table>
    <tr>
      <th colspan=2><img src="images/idea.png" alt="Symbol für weitere Informationen"/> Parameter für vergessenes Kennwort</th>
    </tr>
    <tr>
      <td><code>%{linkExpiration.hours}</code></td>
      <td> Zeigt die Anzahl der Stunden an, die der Link gültig ist.</td>
    </tr>
    <tr>
      <td><code>%{linkExpiration.minutes}</code></td>
      <td>Zeigt die Anzahl der Minuten an, die der Link gültig ist.</td>
    </tr>
    <tr>
      <td><code>%{resetPassword.code}</code></td>
      <td> Zeigt einen einmaligen Kenncode als Teil der URL an. Das bedeutet, dass jeder Person ein anderer Code zugeordnet ist. Beispiel: `https://us-south.appid.cloud.ibm.com/wfm/verify/6574839563478`</td>
    </tr>
    <tr>
      <td><code>%{resetPassword.link}</code></td>
      <td> Zeigt den Link an, auf den ein Benutzer klicken muss, um sein Kennwort zu ändern.</td>
    </tr>
  </table>

  Sie können auch die Nachrichtenparameter verwenden, die im Abschnitt mit der [Willkommensnachricht](/docs/services/appid?topic=appid-cd-messages#cd-messages-welcome) aufgelistet werden.
  {: tip}

4. Definieren Sie eine Ablaufzeit für die Gültigkeit der Aktions-URL. Beim Ablauf der URL handelt es sich um die Zeitdauer (in Minuten), die ein Benutzer zur Verfügung hat, um die Aktion auszuführen, bevor die Gültigkeit des Verifizierungslinks abläuft. Diese Einstellung wirkt sich auch auf den Gültigkeitszeitraum Ihres Links zum Zurücksetzen des Kennworts aus.
 
5. Geben Sie eine URL für die Seite ein, die angezeigt werden soll, nachdem ein Benutzer seine E-Mail-Adresse im Feld für die **URL der Seite zum Zurücksetzen des Kennworts** verifiziert hat. Wenn Sie dieses Feld nicht ausfüllen, dann wird eine {{site.data.keyword.appid_short_notm}}-Standardseite angezeigt.

6. Klicken Sie auf **Speichern**.


### E-Mail: Kennwortänderung
{: #cd-messages-password-change}

Sie können einen Benutzer über die Kennwortaktualisierung benachrichtigen. Dies ist nützlich, wenn die Anforderung zur Kennwortänderung nicht vom Benutzer ausging. Sie können die richtigen Schritte ausführen, um ihr Konto zu resichern.
{: shortdesc}

1. Navigieren Sie zur Registerkarte **Workflowvorlagen > Kennwortänderung** des Service-Dashboards.

2. Legen Sie für **E-Mail bei Kennwortänderung** die Einstellung **Aktiviert** fest.

3. Passen Sie den Inhalt Ihrer Nachricht an. Über die Benutzerschnittstelle können Sie Parameter hinzu- und Bilder einfügen. Um die [Sprache](/docs/services/appid?topic=appid-cd-messages#cd-languages) der Nachricht zu ändern, können Sie über die <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">APIs <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> die gewünschte Sprache festlegen. Allerdings ist zu beachten, dass Sie für den Inhalt und die Übersetzung der Nachricht verantwortlich sind. In der folgenden Tabelle finden Sie die verschiedenen Parameter, die Sie in Ihrer Nachricht verwenden können. Wenn ein Benutzer die vom Parameter abgefragte Information nicht angibt, wird im entsprechenden Feld kein Wert angezeigt.


  <table>
    <tr>
      <th colspan=2><img src="images/idea.png" alt="Symbol für weitere Informationen"/> Parameter für Kennwortänderung</th>
    </tr>
    <tr>
      <td><code>%{passwordChangeInfo.time}</code></td>
      <td> Zeigt den Zeitpunkt an, an dem ein neues Kennwort gültig wurde. </td>
    </tr>
    <tr>
      <td><code>%{passwordChangeInfo.ipAddress}</code></td>
      <td> Zeigt die IP-Adresse an, von der aus die Kennwortänderung angefordert wurde. </td>
    </tr>
  </table>

  Sie können auch die Nachrichtenparameter verwenden, die im Abschnitt mit der [Willkommensnachricht](/docs/services/appid?topic=appid-cd-messages#cd-messages-welcome) aufgelistet werden.
  {: tip}

4. Klicken Sie auf **Speichern**.




## Angepassten E-Mail-Absender verwenden
{: #cd-custom-email}

Mit {{site.data.keyword.appid_short_notm}} können Sie einen angepassten Erweiterungspunkt definieren, um Ihre Cloud Directory-E-Mail-Nachrichten zu senden. Wenn Sie einen Erweiterungspunkt definieren, haben Sie vollständige Kontrolle darüber, wie die E-Mails gesendet werden, und Sie können Ihren eigenen Domänennamen verwenden. Standardmäßig verwendet {{site.data.keyword.appid_short_notm}} als Mailzustellungsservice <a href="https://www.sendgrid.com" target="_blank">SendGrid <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>.
 {: shortdesc}

Aus den folgenden Gründen kann die Verendung eines angepassten E-Mail-Absenders sinnvoll sein:

- **Personalisierte Domäne** Wenn Sie einen angepassten E-Mail-Dispatcher konfigurieren, haben Sie vollständige Kontrolle darüber, wie die E-Mail-Nachrichten gesendet werden. Dies umfasst das Anpassen der E-Mail-Domäne, wodurch die Wahrscheinlichkeit verringert wird, dass E-Mails als Spam gefiltert werden. Außerdem können Sie die Markenkennzeichnung und damit die Wiedererkennung für Ihre App-Benutzer weiter verbessern.

- **Analyse und Fehlerbehebung** Ihr E-Mail-Provider kann Ihnen wichtige Informationen zur Verfügung stellen, z. B. wie viele Personen die E-Mails geöffnet haben oder welche Nachrichten nicht zugestellt wurden. Da Sie einzelne Nachrichten verfolgen und Zugriff auf die Gesamtstatistik erhalten, kann dies zur Behebung von Problemen beitragen.

Nachdem der Erweiterungspunkt konfiguriert wurde, wird er von {{site.data.keyword.appid_short_notm}} immer dann aufgerufen, wenn eine E-Mail-Nachricht gesendet werden muss. Der Erweiterungspunkt enthält alle Informationen zu der Nachricht, einschließlich des endgültigen Inhalts des E-Mail-Hauptteils.



### Angepassten Absender konfigurieren
{: #cd-messages-configure-custom-sender}

Zum Konfigurieren Ihres angepassten E-Mail-Absenders müssen Sie die <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.set_cloud_directory_email_dispatcher" target="_blank">Management-API</a> von Cloud Directory verwenden.


1. Geben Sie die URL an. Darüber hinaus können Sie Autorisierungsinformationen zur Verfügung stellen. Die unterstützten Autorisierungstypen sind die `Basisautorisierung` oder die Angabe eines `konstanten Wertes für den Autorisierungsheader`.

  Gültige Konfigurationsbeispiele:
  ```
  {
    "custom": {
      "url": "https://example.com/send_mail"
    }
  }
  ```
  {: screen}

  ```
  {
    "custom": {
      "url": "https://example.com/send_mail",
      "authorization": {
        "type": "basic",
        "username": "username",
        "password": "password"
      }
    }
  }
  ```
  {: screen}

  ```
  {
    "custom": {
      "url": "https://example.com/send_mail",
      "authorization": {
        "type": "value",
        "value": "myApiKey"
      }
    }
  }
  ```
  {: screen}

2. Konfigurieren Sie einen Erweiterungspunkt, der eine POST-Anforderungen überwachen kann. Dieser Endpunkt sollte in der Lage sein, die Nutzdaten zu lesen, die aus {{site.data.keyword.appid_short_notm}} stammen, und die E-Mail mit dem angepassten E-Mail-Absender zu senden.

3. Der Hauptteil, der von {{site.data.keyword.appid_short_notm}} gesendet wird, weist das folgende Format auf: `{"jws": "jws-format-string"}`. Nachdem Sie die Nutzdaten entschlüsselt und verifiziert haben, ergibt sich als Inhalt eine JSON-Zeichenfolge.

  ```
  {
    "tenant": "tenant-id",
      "iss" : "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61",
      "iat": 1539173126,
      "jti": "uniq-id",
      "message": {
        "to": "your@mail.com",
          "from": {
            "name": "My Awesome Service",
              "address": "no-reply@company.com"
        },
          "replyTo": {
            "name": "My Awesome Service",
              "address": "yes-reply@company.com"
        },
          "subject": "Welcome to My Awesome Service",
          "body": "<p>Hello<p><br/><p>Thanks for signing up John Doe</p>"
    }
  }
  ```
  {: screen}

  <table>
    <tr>
      <th>Variable</th>
      <th>Beschreibung</th>
    </tr>
    <tr>
      <td><code>tenant</code></td>
      <td>Die Tenant-ID Ihrer {{site.data.keyword.appid_short_notm}}-Instanz.</td>
    </tr>
    <tr>
      <td><code>iat</code></td>
      <td>Die Zeitmarke für den Zeitpunkt, zu dem die Nachricht gesendet wurde.</td>
    </tr>
    <tr>
      <td><code>iss</code></td>
      <td>Das Prinzip oder die {{site.data.keyword.appid_short_notm}}-Instanz, von dem bzw. der das JWS-Token ausgegeben wurde. </td>
    </tr>
    <tr>
      <td><code>jti</code></td>
      <td>Die eindeutige Transaktions-ID.</td>
    </tr>
    <tr>
      <td><code>message: to</code></td>
      <td>Die E-Mail-Adresse des Empfängers der Nachricht.</td>
    </tr>
    <tr>
      <td><code>message: from</code></br><code>name</code></br><code>address</code></td>
      <td></br>Der Name des Absenders der Nachricht.</br>Die E-Mail-Adresse des Absenders.</td>
    </tr>
    <tr>
      <td><code>Optional: message: reply to</code></br><code>name</code></br><code>address</code></td>
      <td></br>Der Name, der der Antwort-E-Mail-Adresse zugeordnet ist.</br>Die E-Mail-Adresse, an die der Benutzer antworten kann.</td>
    </tr>
  </table>

  Sie können verifizieren, ob Ihre Anforderung erfolgreich war, indem Sie den Antwortstatuscode überprüfen. Jeder Code im Bereich 200 - 299 gilt als erfolgreich. Wenn Sie eine andere Antwort erhalten, versuchen Sie, Ihre Anforderung erneut zu stellen.
  {: tip}

4. Alle HTTP-Nutzdaten, die von {{site.data.keyword.appid_short_notm}} gesendet werden, werden automatisch gemäß dem JWS-Standard signiert. Dazu wird ein asymmetrisches Schlüsselpaar verwendet.
Für jede {{site.data.keyword.appid_short_notm}}-Instanz wird ein privater und ein öffentlicher Schlüssel generiert, die nicht für andere Instanzen genutzt werden. Der private Schlüssel wird verwendet, um die HTTP-Nutzdaten zu signieren, und Sie können den öffentlichen Schlüssel verwenden, um zu prüfen, ob die Nutzdaten von {{site.data.keyword.appid_short_notm}} generiert und nicht durch eine dritte Partei geändert wurden (<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#!/Authorization_Server_V4/publicKeys" target="_blank">Public-Keys-Endpunkt</a>).

5. Beispielcode für den Erweiterungspunkt (JavaScript).
  ```
  const sgMail = require('@sendgrid/mail');
  const {promisify} = require('bluebird');
  const request = promisify(require('request'));
  const jwtVerify = promisify(require('jsonwebtoken').verify);
  const jwtDecode = require('jsonwebtoken').decode;
  const jwkToPem = require('jwk-to-pem');

  async function obtainPublicKeys() {
  	// Ihre {{site.data.keyword.appid_short_notm}}-Instanz-Tenant-ID
  	const tenantId = '<TENANT-ID>';

  	// Sendeanforderung an {{site.data.keyword.appid_short_notm}}-Public-Keys-Endpunkt
  	const keysOptions = {
  		method: 'GET',
  		url: `https://<REGION>.appid.cloud.ibm.com/oauth/v4/${tenantId}/publickeys`
  	};
  	const keysResponse = await request(keysOptions);
  	return JSON.parse(keysResponse.body).keys;
  }

  async function verifySignature(keysArray, kid, jws) {
  	const keyJson = keysArray.find(key => key.kid === kid);
  	if (keyJson) {
  		const pem = jwkToPem(keyJson);
  		await jwtVerify(jws, pem);
  		return;
  	}
  	throw new Error ("Unable to verify signature");
  }

  async function verifyAndSendMail(jws) {
  	// Der API-Schlüssel für Sendgrid
  	const sgApiKey = '<SENDGRID-API-KEY>';

  	// Initialisierung von Sendgrind
  	sgMail.setApiKey(sgApiKey);

  	// Entschlüsseln der Nachricht, um Informationen abzurufen
  	const data = jwtDecode(jws, {complete: true});

  	// kid-Extraktion aus Header
  	const kid = data.header.kid;

  	const keysArray = await obtainPublicKeys();

  	// Verifizierung der Signatur der Nutzdaten mit den öffentlichen Schlüsseln
  	await verifySignature(keysArray, kid ,jws);

  	// Senden der E-Mail mit Ihrem Sendgrid-Konto
  	const message = data.payload.message;
  	const msg = {
  		to: message.to,
  		from: message.from.address,
  		subject: message.subject,
  		html: message.body,
  	};
  	console.log(`Sending email to ${message.to}`);
  	let sendgridResponse = await sgMail.send(msg);

  	return {result : 'email_sent',sendgridResponse};
  }
  ```
  {: screen}

6. Prüfen Sie, ob Ihre Konfiguration ordnungsgemäß eingerichtet ist, indem Sie Ihren E-Mail-Dispatcher testen. Verwenden Sie die <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Config/post_email_dispatcher_test" target="_blank">Test-API</a>, um eine Anforderung an Ihren konfigurierten angepassten E-Mail-Absender auszulösen.

Ein vollständiges Beispiel finden Sie unter <a href="https://www.ibm.com/cloud/blog/use-ibm-cloud-app-id-and-your-email-provider-to-brand-mails-sent-to-app-users" target="_blank">Use your own provider for mail sent with {{site.data.keyword.appid_full}}</a>.



## Unterstützte Sprachen
{: #cd-languages}

Die Sprache, in der die schriftliche Benutzerkommunikation erfolgen kann, können Sie über die <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">Management-APIs für Sprachen <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> festlegen. Ohne weiteren Vorbereitungs- oder Anpassungsaufwand ist jedoch nur die englische Sprache verfügbar. Die Zuständigkeit für die Übersetzung der Nachrichten liegt bei Ihnen. Wenn Sie die entsprechende Konfiguration mit der API festgelegt haben, wird die grafische Benutzerschnittstelle aktualisiert, sodass Sie die Textvorlagen ändern können.
{: shortdesc}

<table>
  <col width="20%">
  <col width="25%">
  <col width="35%">
  <tr>
    <th>Code</th>
    <th>Sprache</th>
    <th>Region</th>
  </tr>
  <tr>
    <td><code>af-ZA</code></td>
    <td>Afrikaans</td>
    <td>Südafrika</td>
  </tr>
  <tr>
    <td><code>sq-AL</code></td>
    <td>Albanisch</td>
    <td>Albanien</td>
  </tr>
  <tr>
    <td><code>am-ET</code></td>
    <td>Amharisch</td>
    <td>Äthiopien</td>
  </tr>
  <tr>
    <td><code>ar-DZ</code></td>
    <td>Arabisch</td>
    <td>Algerien</td>
  </tr>
  <tr>
    <td><code>ar-BH</code></td>
    <td>Arabisch</td>
    <td>Bahrain</td>
  </tr>
  <tr>
    <td><code>ar-EG</code></td>
    <td>Arabisch</td>
    <td>Ägypten</td>
  </tr>
  <tr>
    <td><code>ar-IQ</code></td>
    <td>Arabisch</td>
    <td>Irak</td>
  </tr>
  <tr>
    <td><code>ar-JO</code></td>
    <td>Arabisch</td>
    <td>Jordanien</td>
  </tr>
  <tr>
    <td><code>ar-KW</code></td>
    <td>Arabisch</td>
    <td>Kuwait</td>
  </tr>
  <tr>
    <td><code>ar-LB</code></td>
    <td>Arabisch</td>
    <td>Libanon</td>
  </tr>
  <tr>
    <td><code>ar-LY</code></td>
    <td>Arabisch</td>
    <td>Libyen</td>
  </tr>
  <tr>
    <td><code>ar-MR</code></td>
    <td>Arabisch</td>
    <td>Mauretanien</td>
  </tr>
  <tr>
    <td><code>ar-MA</code></td>
    <td>Arabisch</td>
    <td>Marokko</td>
  </tr>
  <tr>
    <td><code>ar-OM</code></td>
    <td>Arabisch</td>
    <td>Oman</td>
  </tr>
  <tr>
    <td><code>ar-QA</code></td>
    <td>Arabisch</td>
    <td>Katar</td>
  </tr>
  <tr>
    <td><code>ar-SA</code></td>
    <td>Arabisch</td>
    <td>Saudi-Arabien</td>
  </tr>
  <tr>
    <td><code>ar-SY</code></td>
    <td>Arabisch</td>
    <td>Syrien</td>
  </tr>
  <tr>
    <td><code>ar-YE</code></td>
    <td>Arabisch</td>
    <td>Tunesien</td>
  </tr>
  <tr>
    <td><code>ar-AE</code></td>
    <td>Arabisch</td>
    <td>Vereinigte Arabische Emirate</td>
  </tr>
  <tr>
    <td><code>ar-YE</code></td>
    <td>Arabisch</td>
    <td>Jemen</td>
  </tr>
  <tr>
    <td><code>hy-AM</code></td>
    <td>Armenisch</td>
    <td>Armenien</td>
  </tr>
  <tr>
    <td><code>as-IN</code></td>
    <td>Assamesisch</td>
    <td>Indien</td>
  </tr>
  <tr>
    <td><code>az-AZ</code></td>
    <td>Aserbaidschanisch</td>
    <td>Aserbaidschan</td>
  </tr>
  <tr>
    <td><code>eu-ES</code></td>
    <td>Baskisch</td>
    <td>Spanien</td>
  </tr>
  <tr>
    <td><code>be-BY</code></td>
    <td>Weißrussisch</td>
    <td>Weißrussland</td>
  </tr>
  <tr>
    <td><code>bn-BD</code></td>
    <td>Bengalisch</td>
    <td>Bangladesch</td>
  </tr>
  <tr>
    <td><code>be-BY</code></td>
    <td>Weißrussisch</td>
    <td>Weißrussland</td>
  </tr>
  <tr>
    <td><code>bn-BD</code></td>
    <td>Bengalisch</td>
    <td>Bangladesch</td>
  </tr>
  <tr>
    <td><code>bn-IN</code></td>
    <td>Bengalisch</td>
    <td>Indien</td>
  </tr>
  <tr>
    <td><code>bs-Latn-BA</code></td>
    <td>Bosnisch</td>
    <td>Bosnien</td>
  </tr>
  <tr>
    <td><code>bg-BG</code></td>
    <td>Bulgarisch</td>
    <td>Bulgarien</td>
  </tr>
  <tr>
    <td><code>my-MM</code></td>
    <td>Burmesisch</td>
    <td>Myanmar</td>
  </tr>
  <tr>
    <td><code>ca-ES</code></td>
    <td>Katalanisch</td>
    <td>Spanien</td>
  </tr>
  <tr>
    <td><code>zh-Hans-CN</code></td>
    <td>Vereinfachtes Chinesisch</td>
    <td>China</td>
  </tr>
  <tr>
    <td><code>zh-Hans-SG</code></td>
    <td>Vereinfachtes Chinesisch</td>
    <td>Singapur</td>
  </tr>
  <tr>
    <td><code>zh-Hant-HK</code></td>
    <td>Chinesisch in traditioneller Schreibweise</td>
    <td>Hongkong (Sonderverwaltungsregion der VR China)</td>
  </tr>
  <tr>
    <td><code>zh-Hant-MO</code></td>
    <td>Chinesisch in traditioneller Schreibweise</td>
    <td>Sonderverwaltungszone Macao der Volksrepublik China</td>
  </tr>
  <tr>
    <td><code>zh-Hant-TW</code></td>
    <td>Chinesisch in traditioneller Schreibweise</td>
    <td>Taiwan</td>
  </tr>
  <tr>
    <td><code>hr-HR</code></td>
    <td>Kroatisch</td>
    <td>Kroatien</td>
  </tr>
  <tr>
    <td><code>cs-CZ</code></td>
    <td>Tschechisch</td>
    <td>Tschechien</td>
  </tr>
  <tr>
    <td><code>da-DK</code></td>
    <td>Dänisch</td>
    <td>Dänemark</td>
  </tr>
  <tr>
    <td><code>nl-BE</code></td>
    <td>Niederländisch</td>
    <td>Belgien</td>
  </tr>
  <tr>
    <td><code>nl-NL</code></td>
    <td>Niederländisch</td>
    <td>Niederlande</td>
  </tr>
  <tr>
    <td><code>en-AU</code></td>
    <td>Englisch</td>
    <td>Australien</td>
  </tr>
  <tr>
    <td><code>en-BE</code></td>
    <td>Englisch</td>
    <td>Belgien</td>
  </tr>
  <tr>
    <td><code>en-CM</code></td>
    <td>Englisch</td>
    <td>Kamerun</td>
  </tr>
  <tr>
    <td><code>eu-CA</code></td>
    <td>Englisch</td>
    <td>Kanada</td>
  </tr>
  <tr>
    <td><code>en-GH</code></td>
    <td>Englisch</td>
    <td>Ghana</td>
  </tr>
  <tr>
    <td><code>eu-HK</code></td>
    <td>Englisch</td>
    <td>Hongkong (Sonderverwaltungsregion der VR China)</td>
  </tr>
  <tr>
    <td><code>en-IN</code></td>
    <td>Englisch</td>
    <td>Indien</td>
  </tr>
  <tr>
    <td><code>en-IE</code></td>
    <td>Englisch</td>
    <td>Irland</td>
  </tr>
  <tr>
    <td><code>en-KE</code></td>
    <td>Englisch</td>
    <td>Kenia</td>
  </tr>
  <tr>
    <td><code>en-MU</code></td>
    <td>Englisch</td>
    <td>Mauritius</td>
  </tr>
  <tr>
    <td><code>en-NZ</code></td>
    <td>Englisch</td>
    <td>Neuseeland</td>
  </tr>
  <tr>
    <td><code>en-NG</code></td>
    <td>Englisch</td>
    <td>Nigeria</td>
  </tr>
  <tr>
    <td><code>en-PH</code></td>
    <td>Englisch</td>
    <td>Philippinen</td>
  </tr>
  <tr>
    <td><code>en-SG</code></td>
    <td>Englisch</td>
    <td>Singapur</td>
  </tr>
  <tr>
    <td><code>en-ZA</code></td>
    <td>Englisch</td>
    <td>Südafrika</td>
  </tr>
  <tr>
    <td><code>en-TZ</code></td>
    <td>Englisch</td>
    <td>Tansania</td>
  </tr>
  <tr>
    <td><code>en-GB</code></td>
    <td>Englisch</td>
    <td>Vereinigtes Königreich</td>
  </tr>
  <tr>
    <td><code>en-US</code></td>
    <td>Englisch</td>
    <td>Vereinigte Staaten</td>
  </tr>
  <tr>
    <td><code>en-ZM</code></td>
    <td>Englisch</td>
    <td>Sambia</td>
  </tr>
  <tr>
    <td><code>en</code></td>
    <td>Englisch</td>
    <td> </td>
  </tr>
  <tr>
    <td><code>et-EE</code></td>
    <td>Estnisch</td>
    <td>Estland</td>
  </tr>
  <tr>
    <td><code>fil-PH</code></td>
    <td>Filipino</td>
    <td>Philippinen</td>
  </tr>
  <tr>
    <td><code>fi-FI</code></td>
    <td>Finnisch</td>
    <td>Finnland</td>
  </tr>
  <tr>
    <td><code>fr-DZ</code></td>
    <td>Französisch</td>
    <td>Algerien</td>
  </tr>
  <tr>
    <td><code>fr-CM</code></td>
    <td>Französisch</td>
    <td>Kamerun</td>
  </tr>
  <tr>
    <td><code>fr-CD</code></td>
    <td>Französisch</td>
    <td>Demokratische Republik Kongo</td>
  </tr>
  <tr>
    <td><code>fr-BE</code></td>
    <td>Französisch</td>
    <td>Belgien</td>
  </tr>
  <tr>
    <td><code>fr-CA</code></td>
    <td>Französisch</td>
    <td>Kanada</td>
  </tr>
  <tr>
    <td><code>fr-FR</code></td>
    <td>Französisch</td>
    <td>Frankreich</td>
  </tr>
  <tr>
    <td><code>fr-CI</code></td>
    <td>Französisch</td>
    <td>Elfenbeinküste</td>
  </tr>
  <tr>
    <td><code>fr-LU</code></td>
    <td>Französisch</td>
    <td>Luxemburg</td>
  </tr>
  <tr>
    <td><code>fr-MR</code></td>
    <td>Französisch</td>
    <td>Mauretanien</td>
  </tr>
  <tr>
    <td><code>fr-MU</code></td>
    <td>Französisch</td>
    <td>Mauritius</td>
  </tr>
  <tr>
    <td><code>fr-MA</code></td>
    <td>Französisch</td>
    <td>Marokko</td>
  </tr>
  <tr>
    <td><code>fr-SN</code></td>
    <td>Französisch</td>
    <td>Senegal</td>
  </tr>
  <tr>
    <td><code>fr-CH</code></td>
    <td>Französisch</td>
    <td>Schweiz</td>
  </tr>
  <tr>
    <td><code>fr-TN</code></td>
    <td>Französisch</td>
    <td>Tunesien</td>
  </tr>
  <tr>
    <td><code>gl-ES</code></td>
    <td>Galizisch</td>
    <td>Spanien</td>
  </tr>
  <tr>
    <td><code>lg-UG</code></td>
    <td>Ganda</td>
    <td>Uganda</td>
  </tr>
  <tr>
    <td><code>ka-GE</code></td>
    <td>Georgisch</td>
    <td>Georgien</td>
  </tr>
  <tr>
    <td><code>de-AT</code></td>
    <td>Deutsch</td>
    <td>Österreich</td>
  </tr>
  <tr>
    <td><code>de-DE</code></td>
    <td>Deutsch</td>
    <td>Deutschland</td>
  </tr>
  <tr>
    <td><code>de-LU</code></td>
    <td>Deutsch</td>
    <td>Luxemburg</td>
  </tr>
  <tr>
    <td><code>de-CH</code></td>
    <td>Deutsch</td>
    <td>Schweiz</td>
  </tr>
  <tr>
    <td><code>el-GR</code></td>
    <td>Griechisch</td>
    <td>Griechenland</td>
  </tr>
  <tr>
    <td><code>gu-IN</code></td>
    <td>Gujaratisch</td>
    <td>Indien</td>
  </tr>
  <tr>
    <td><code>ha-NG</code></td>
    <td>Haussa</td>
    <td>Nigeria</td>
  </tr>
  <tr>
    <td><code>he-IL</code></td>
    <td>Hebräisch</td>
    <td>Israel</td>
  </tr>
  <tr>
    <td><code>hi-IN</code></td>
    <td>Hindi</td>
    <td>Indien</td>
  </tr>
  <tr>
    <td><code>hu-HU</code></td>
    <td>Ungarisch</td>
    <td>Ungarn</td>
  </tr>
  <tr>
    <td><code>is-IS</code></td>
    <td>Isländisch</td>
    <td>Island</td>
  </tr>
  <tr>
    <td><code>ig-NG</code></td>
    <td>Igbo</td>
    <td>Nigeria</td>
  </tr>
  <tr>
    <td><code>id-ID</code></td>
    <td>Indonesisch</td>
    <td>Indonesien</td>
  </tr>
  <tr>
    <td><code>it-IT</code></td>
    <td>Italienisch</td>
    <td>Italien</td>
  </tr>
  <tr>
    <td><code>it-CH</code></td>
    <td>Italienisch</td>
    <td>Schweiz</td>
  </tr>
  <tr>
    <td><code>ja-JP</code></td>
    <td>Japanisch</td>
    <td>Japan</td>
  </tr>
  <tr>
    <td><code>kn-IN</code></td>
    <td>Kannada</td>
    <td>Indien</td>
  </tr>
  <tr>
    <td><code>kk-KZ</code></td>
    <td>Kasachisch</td>
    <td>Kasachstan</td>
  </tr>
  <tr>
    <td><code>km-KH</code></td>
    <td>Khmer</td>
    <td>Kambodscha</td>
  </tr>
  <tr>
    <td><code>rw-RW</code></td>
    <td>Kinyarwanda</td>
    <td>Ruanda</td>
  </tr>
  <tr>
    <td><code>kok-IN</code></td>
    <td>Konkani</td>
    <td>Indien</td>
  </tr>
  <tr>
    <td><code>ko-KR</code></td>
    <td>Koreanisch</td>
    <td>Südkorea</td>
  </tr>
  <tr>
    <td><code>lo-LA</code></td>
    <td>Litauisch</td>
    <td>Litauen</td>
  </tr>
  <tr>
    <td><code>lv-LV</code></td>
    <td>Lettisch</td>
    <td>Lettland</td>
  </tr>
  <tr>
    <td><code>lt-LT</code></td>
    <td>Khmer</td>
    <td>Kambodscha</td>
  </tr>
  <tr>
    <td><code>mk-MK</code></td>
    <td>Mazedonisch</td>
    <td>Mazedonien</td>
  </tr>
  <tr>
    <td><code>ms-Latn-MY</code></td>
    <td>Malaiisch (Lateinisch)</td>
    <td>Malaysia</td>
  </tr>
  <tr>
    <td><code>ml-IN</code></td>
    <td>Malajalam</td>
    <td>Indien</td>
  </tr>
  <tr>
    <td><code>mt-MT</code></td>
    <td>Maltesisch</td>
    <td>Malta</td>
  </tr>
  <tr>
    <td><code>mr-IN</code></td>
    <td>Marathi</td>
    <td>Indien</td>
  </tr>
  <tr>
    <td><code>mn-Cyrl-MN</code></td>
    <td>Mongolisch (Kyrillisch)</td>
    <td>Mongolei</td>
  </tr>
  <tr>
    <td><code>ne-IN</code></td>
    <td>Nepalesisch</td>
    <td>Indien</td>
  </tr>
  <tr>
    <td><code>ne-NP</code></td>
    <td>Nepalesisch</td>
    <td>Nepal</td>
  </tr>
  <tr>
    <td><code>nb-NO</code></td>
    <td>Norwegisch (Bokmål)</td>
    <td>Norwegen</td>
  </tr>
  <tr>
    <td><code>nn-NO</code></td>
    <td>Nynorsk-Norwegisch</td>
    <td>Norwegen</td>
  </tr>
  <tr>
    <td><code>or-IN</code></td>
    <td>Orija</td>
    <td>Indien</td>
  </tr>
  <tr>
    <td><code>om-ET</code></td>
    <td>Oromo</td>
    <td>Äthiopien</td>
  </tr>
  <tr>
    <td><code>pl-PL</code></td>
    <td>Polnisch</td>
    <td>Polen</td>
  </tr>
  <tr>
    <td><code>pt-AO</code></td>
    <td>Portugiesisch</td>
    <td>Angola</td>
  </tr>
  <tr>
    <td><code>pt-BR</code></td>
    <td>Portugiesisch</td>
    <td>Brasilien</td>
  </tr>
  <tr>
    <td><code>pt-MO</code></td>
    <td>Portugiesisch</td>
    <td>Sonderverwaltungszone Macao der Volksrepublik China</td>
  </tr>
  <tr>
    <td><code>pt-MZ</code></td>
    <td>Portugiesisch</td>
    <td>Mosambik</td>
  </tr>
  <tr>
    <td><code>pt-PT</code></td>
    <td>Portugiesisch</td>
    <td>Portugal</td>
  </tr>
  <tr>
    <td><code>pa-IN</code></td>
    <td>Pundjabisch</td>
    <td>Indien</td>
  </tr>
  <tr>
    <td><code>ro-RO</code></td>
    <td>Rumänisch</td>
    <td>Rumänien</td>
  </tr>
  <tr>
    <td><code>ru-RU</code></td>
    <td>Russisch</td>
    <td>Russland</td>
  </tr>
  <tr>
    <td><code>sr-Cyrl-RS</code></td>
    <td>Serbisch (Kyrillisch)</td>
    <td>Serbien</td>
  </tr>
  <tr>
    <td><code>sr-Latn-ME</code></td>
    <td>Serbisch (Lateinisch)</td>
    <td>Montenegro</td>
  </tr>
  <tr>
    <td><code>sr-Latn-RS</code></td>
    <td>Serbisch (Lateinisch)</td>
    <td>Serbien</td>
  </tr>
  <tr>
    <td><code>si-LK</code></td>
    <td>Singhalesisch</td>
    <td>Sri Lanka</td>
  </tr>
  <tr>
    <td><code>sk-SK</code></td>
    <td>Slowakisch</td>
    <td>Slowakei</td>
  </tr>
  <tr>
    <td><code>sl-SI</code></td>
    <td>Slowenisch</td>
    <td>Slowenien</td>
  </tr>
  <tr>
    <td><code>es-AR</code></td>
    <td>Spanisch</td>
    <td>Argentinien</td>
  </tr>
  <tr>
    <td><code>es-BO</code></td>
    <td>Spanisch</td>
    <td>Bolivien</td>
  </tr>
  <tr>
    <td><code>es-CL</code></td>
    <td>Spanisch</td>
    <td>Chile</td>
  </tr>
  <tr>
    <td><code>es-CO</code></td>
    <td>Spanisch</td>
    <td>Kolumbien</td>
  </tr>
  <tr>
    <td><code>es-CR</code></td>
    <td>Spanisch</td>
    <td>Costa Rica</td>
  </tr>
  <tr>
    <td><code>es-DO</code></td>
    <td>Spanisch</td>
    <td>Dominikanische Republik</td>
  </tr>
  <tr>
    <td><code>es-EC</code></td>
    <td>Spanisch</td>
    <td>Ecuador</td>
  </tr>
  <tr>
    <td><code>es-SV</code></td>
    <td>Spanisch</td>
    <td>El Salvador</td>
  </tr>
  <tr>
    <td><code>es-GT</code></td>
    <td>Spanisch</td>
    <td>Guatemala</td>
  </tr>
  <tr>
    <td><code>es-HN</code></td>
    <td>Spanisch</td>
    <td>Honduras</td>
  </tr>
  <tr>
    <td><code>es-MX</code></td>
    <td>Spanisch</td>
    <td>Mexico</td>
  </tr>
  <tr>
    <td><code>es-NI</code></td>
    <td>Spanisch</td>
    <td>Nicaragua</td>
  </tr>
  <tr>
    <td><code>es-PA</code></td>
    <td>Spanisch</td>
    <td>Panama</td>
  </tr>
  <tr>
    <td><code>es-PY</code></td>
    <td>Spanisch</td>
    <td>Paraguay</td>
  </tr>
  <tr>
    <td><code>es-PE</code></td>
    <td>Spanisch</td>
    <td>Peru</td>
  </tr>
  <tr>
    <td><code>es-PR</code></td>
    <td>Spanisch</td>
    <td>Puerto Rico</td>
  </tr>
  <tr>
    <td><code>es-ES</code></td>
    <td>Spanisch</td>
    <td>Spanien</td>
  </tr>
  <tr>
    <td><code>es-US</code></td>
    <td>Spanisch</td>
    <td>Vereinigte Staaten</td>
  </tr>
  <tr>
    <td><code>es-UY</code></td>
    <td>Spanisch</td>
    <td>Uruguay</td>
  </tr>
  <tr>
    <td><code>es-VE</code></td>
    <td>Spanisch</td>
    <td>Venezuela</td>
  </tr>
  <tr>
    <td><code>sw-KE</code></td>
    <td>Suaheli</td>
    <td>Kenia</td>
  </tr>
  <tr>
    <td><code>sw-TZ</code></td>
    <td>Suaheli</td>
    <td>Tansania</td>
  </tr>
  <tr>
    <td><code>sv-SE</code></td>
    <td>Schwedisch</td>
    <td>Schweden</td>
  </tr>
  <tr>
    <td><code>ta-IN</code></td>
    <td>Tamilisch</td>
    <td>Indien</td>
  </tr>
  <tr>
    <td><code>te-IN</code></td>
    <td>Telugu</td>
    <td>Indien</td>
  </tr>
  <tr>
    <td><code>th-TH</code></td>
    <td>Thailändisch</td>
    <td>Thailand</td>
  </tr>
  <tr>
    <td><code>tr-TR</code></td>
    <td>Türkisch</td>
    <td>Türkei</td>
  </tr>
  <tr>
    <td><code>uk-UA</code></td>
    <td>Ukrainisch</td>
    <td>Ukraine</td>
  </tr>
  <tr>
    <td><code>ur-IN</code></td>
    <td>Urdu</td>
    <td>Indien</td>
  </tr>
  <tr>
    <td><code>ur-PK</code></td>
    <td>Urdu</td>
    <td>Pakistan</td>
  </tr>
  <tr>
    <td><code>uz-Cyrl-UZ</code></td>
    <td>Usbekisch (Kyrillisch)</td>
    <td>Usbekistan</td>
  </tr>
  <tr>
    <td><code>uz-Latn-UZ</code></td>
    <td>Usbekisch (Lateinisch)</td>
    <td>Usbekistan</td>
  </tr>
  <tr>
    <td><code>vi-VN</code></td>
    <td>Vietnamesisch</td>
    <td>Vietnam</td>
  </tr>
  <tr>
    <td><code>cy-GB</code></td>
    <td>Walisisch</td>
    <td>Vereinigtes Königreich</td>
  </tr>
  <tr>
    <td><code>yo-NG</code></td>
    <td>Yoruba</td>
    <td>Nigeria</td>
  </tr>
  <tr>
    <td><code>zu-ZA</code></td>
    <td>Zulu</td>
    <td>Südafrika</td>
  </tr>
</table>
