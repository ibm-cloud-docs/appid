---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-09"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Cloud Directory konfigurieren
{: #cd}

Benutzer können sich über eine E-Mail-Adresse bzw. einen Benutzernamen und ein Kennwort bei Ihren mobilen Apps und Web-Apps registrieren und anmelden. Ein Cloudverzeichnis (Cloud Directory) ist eine Benutzerregistry, die in der Cloud verwaltet wird. Wenn sich ein Benutzer für Ihre App anmeldet, wird er zu Ihrem Benutzerverzeichnis hinzugefügt. Dieses Feature ermöglicht es Benutzern, ihr eigenes Konto innerhalb Ihrer App zu verwalten.
{: shortdesc}

</br>

## Verzeichniseinstellungen verwalten
{: #cd-settings}

Sie können die Benachrichtigungen und den Grad der Benutzersteuerung für Ihre App konfigurieren. Die Einrichtung des Cloudverzeichnisses nimmt nicht viel Zeit in Anspruch, wie in der folgenden Abbildung veranschaulicht wird. Diese Einstellungen können zu jedem beliebigen Zeitpunkt über das Service-Dashboard aktualisiert werden.
{: shortdesc}


![Cloudverzeichnis konfigurieren](/images/cloud-directory.png)
Abbildung. Konfigurationsabfolge für Cloud Directory


1. Stellen Sie sicher, dass Cloud Directory als Identitätsprovider aktiviert ist und legen Sie für **Benutzern die Registrierung und das Zurücksetzen ihres Kennworts ermöglichen** den Wert **Ein** fest. Wenn für die Option der Wert **Aus** festgelegt ist, können Sie dennoch Benutzer über die Konsole hinzufügen, jedoch nur zu Entwicklungszwecken.
2. Entscheiden Sie, ob Ihre Benutzer sich über einen angegeben Benutzernamen oder eine E-Mail-Adresse anmelden. Dieses Feld wird für den Verarbeitungsablauf für Registrierung, für Anmeldung und für ein vergessenes Kennwort verwendet. Wenn Sie es Benutzern ermöglichen, sich über Benutzername und Kennwort anzumelden, muss der Benutzername aus mindesten 8 Zeichen bestehen. Leerzeichen, Kommas und Schrägstriche dürfen nicht enthalten sein. **Hinweis:** Sie können nur zwischen den Optionen wechseln, wenn Ihr Cloudverzeichnis keine Benutzer enthält. 
3. Konfigurieren Sie die Absenderdetails. Geben Sie die E-Mail-Adresse, die als Absender Ihrer Nachrichten angezeigt werden soll, den Absender und die Adresse, an die Benutzer ihre Antworten senden können, an.
  Stellen Sie beim Konfigurieren der Aktions-URL sicher, dass der festgelegte Zeitraum für das Klicken auf den Link ausreicht. Ein Benutzer muss seine E-Mail-Adresse verifizieren, damit ihm bestimmte Optionen zur Verfügung stehen, wie z. B. die Möglichkeit, das Zurücksetzen des Kennworts anzufordern.
  {: tip}
4. Bestimmen Sie die E-Mail-Typen, die ein Benutzer erhält, sowie die Absenderinformationen.
5. Passen Sie mithilfe der bereitgestellten Vorlagen Ihre Nachrichten mit Marken oder personalisiertem Text an. Weitere Informationen finden Sie in [Nachrichten verwalten](/docs/services/appid/cloud-directory.html#cd-messages).
6. Die Benutzer, die bei Ihrer App angemeldet sind, sind auf der Registerkarte **Benutzer** der GUI aufgeführt.

Ein einzelner Benutzer kann sich bis zu fünfmal pro Minute anmelden. Beim sechsten Versuch wird ein Fehler angezeigt.
{: tip}

</br>

## Nachrichten verwalten
{: #cd-messages}

Eine Vorlage ist ein Beispiel einer E-Mail-Nachricht, die Sie an Ihre Benutzer senden können. Sie können die Vorlage anpassen, indem Sie den Inhalt und das Layout der Nachricht aktualisieren.
{: shortdesc}

1. Legen Sie auf der Registerkarte **Identitätsprovider > Cloud Directory > Einstellungen** für die Nachrichten, die gesendet werden sollen, die Einstellung **Ein** fest. 

2. Optional: Legen Sie mit den <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/updateLocalization" target="_blank">APIs für Sprachenverwaltung <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> eine andere Sprache fest, die in Ihren Nachrichtenvorlagen verwendet werden soll. Eine Liste der unterstützten Sprachencodes finden Sie in [Unterstützte Sprachen](#languages). 

3. Wählen Sie einen **Nachrichtentyp** aus.

4. Passen Sie die Nachricht an, indem Sie den Inhalt und das Design der Nachricht ändern. Sie können Parameter verwenden, um die Nachrichten zu personalisieren. Denken Sie daran, die Änderungen zu speichern!

### Nachrichtentypen

Sie können mehrere Typen von Nachrichten an Ihre Benutzer senden. Sie können die in der Benutzerschnittstelle programmierte Beispielnachricht senden oder den Inhalt anpassen, um die App-Schnittstelle persönlicher zu gestalten.

<dl>
  <dt>Begrüßung</dt>
    <dd><p>Sie können Benutzer per E-Mail bei Ihrer Anwendung begrüßen, nachdem diese eine Registrierung durchgeführt haben. Gestalten Sie die Nachrichten so attraktiv wie möglich, um die Benutzer zu begrüßen und zu binden.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="Symbol für weitere Informationen"/> Liste der Nachrichtenparameter</th>
      </thead>
      <tbody>
        <tr>
          <td><code>%{display.logo}</code></td>
          <td> Zeigt das Bild an, das Sie für das Anmeldewidget konfiguriert haben. </td>
        </tr>
        <tr>
          <td><code>%{user.displayName}</code></td>
          <td> Zeigt den Anzeigenamen an, den ein Benutzer für die Interaktion mit der App ausgewählt hat. </td>
        </tr>
        <tr>
          <td><code>%{user.email}</code></td>
          <td> Zeigt die registrierte E-Mail-Adresse des Benutzers an. </td>
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
      </tbody>
    </table>
    <p>**Hinweis**: Wenn ein Benutzer die vom Parameter abgefragte Information nicht angibt, wird im entsprechenden Feld kein Wert angezeigt.</p></dd>
  <dt>Kennwort vergessen</dt>
    <dd><p>Wenn ein Benutzer das Kennwort vergisst oder es aus einem anderen Grund aktualisieren möchte, kann er ein Zurücksetzen des Kennworts anfordern. Sie können die E-Mail-Antwort auf diese Anforderung anpassen. Wenn ein Benutzer eine Änderung anfordert, wird das Kennwort erst geändert, wenn er auf den Link in dieser E-Mail klickt.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="Symbol für weitere Informationen"/> Parameter für Kennwortänderung</th>
      </thead>
      <tbody>
        <tr>
          <td><code>%{linkExpiration.hours}</code></td>
          <td> Zeigt die Anzahl der Stunden an, die der Link gültig ist. </td>
        </tr>
        <tr>
          <td><code>%{linkExpiration.minutes}</code></td>
          <td> Zeigt die Anzahl der Minuten an, die der Link gültig ist. </td>
        </tr>
        <tr>
          <td><code>%{resetPassword.code}</code></td>
          <td> Zeigt einen einmaligen Kenncode als Teil der URL an. Das bedeutet, dass jeder Person ein anderer Code zugeordnet ist. Beispiel: <code>https://appid-wfm.bluemix.net/verify/6574839563478</code>. </td>
        </tr>
        <tr>
          <td><code>%{resetPassword.link}</code></td>
          <td> Zeigt den Link an, auf den ein Benutzer klicken muss, um sein Kennwort zu ändern. </td>
        </tr>
       </tbody>
    </table>
    </dd>
  <dt>Verifizierung</dt>
    <dd><p>Sie können festlegen, dass ein Benutzer sein Konto per E-Mail verifizieren muss. Indem Sie eine Verifizierung anfordern, begrenzen Sie die Anzahl der gefälschten Konten, die sich bei Ihrer App registrieren können. Sie können den Zugriff auf Ihre App einschränken, bis ein Benutzer seine E-Mail-Adresse verifiziert hat, oder Sie können auf diese Weise die Erstellung von Profilen für bestimmte Benutzer verwalten.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="Symbol für weitere Informationen"/> Parameter für Verifizierungsnachricht</th>
      </thead>
      <tbody>
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
      </tbody>
    </table>
    </dd>
  <dt>Kennwortänderung</dt>
    <dd><p>Sie können einen Benutzer über die Kennwortaktualisierung benachrichtigen. Dies ist nützlich, wenn die Anforderung zur Kennwortänderung nicht vom Benutzer ausging. So können die Benutzer die erforderlichen Schritte unternehmen, um ihr Konto erneut zu schützen.
    </p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="Symbol für weitere Informationen"/> Parameter für Kennwortänderung</th>
      </thead>
      <tbody>
        <tr>
          <td><code>%{passwordChangeInfo.time}</code></td>
          <td> Zeigt den Zeitpunkt an, an dem ein neues Kennwort gültig wurde. </td>
        </tr>
        <tr>
          <td> %{passwordChangeInfo.ipAddress} </td>
          <td> Zeigt die IP-Adresse an, von der aus die Kennwortänderung angefordert wurde. </td>
        </tr>
      </tbody>
    </table>
    </dd>
</dl>
</br>
**Hinweis**: {{site.data.keyword.appid_short_notm}} verwendet <a href="https://www.sendgrid.com" target="_blank">SendGrid <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> als Mailzustellungsservice. Alle E-Mails werden über ein einzelnes SendGrid-Konto gesendet.


</br>

## Kennwortsicherheit verwalten
{: #strength}

Sie können die Anforderungen, die die mit Cloud Directory verwendeten Kennwörter erfüllen müssen, festlegen.
{: shortdesc}

Sichere Kennwörter sind schwerer oder sogar gar nicht durch Ausprobieren oder Algorithmen zu erraten. Die Kennwortsicherheit wird als Zeichenfolge mit einem regulären Ausdruck definiert. 

Allgemeine Beispiele für die Kennwortsicherheit: 

- Muss aus mindestens 8 Zeichen bestehen. Regulärer Beispielausdruck: `^.{8,}$`
- Muss mindestens eine Zahl, einen Kleinbuchstaben und einen Großbuchstaben enthalten. Regulärer Beispielausdruck: `^(?:(?=.*\\d)(?=.*[a-z])(?=.*[A-Z]).*)$`
- Darf nur lateinische Buchstaben und arabische Ziffern enthalten. Regulärer Beispielausdruck: `^[A-Za-z0-9]*$`
- Muss mindestens ein Sonderzeichen enthalten. Regulärer Beispielausdruck: `^(\w)\w*?(?!\1)\w+$`

Sie müssen die Anforderungen mit den <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/set_cloud_directory_password_regex" target="_blank">Verwaltungs-APIs <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> festlegen. 

</br>



</br>

## Unterstützte Sprachen
{: #languages}

Die Sprache, in der die schriftliche Benutzerkommunikation erfolgen kann, können Sie über die <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/updateLocalization" target="_blank">APIs für Sprachenverwaltung <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> festlegen. Ohne weiteren Vorbereitungs- oder Anpassungsaufwand ist jedoch nur die englische Sprache verfügbar. Die Zuständigkeit für die Übersetzung der Nachrichten liegt bei Ihnen. Wenn Sie die entsprechende Konfiguration mit der API festgelegt haben, wird die grafische Benutzerschnittstelle aktualisiert, sodass Sie die Textvorlagen ändern können.
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
    <td>Macau</td>
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
    <td>Laotisch
<!-- sic! -->
</td>
    <td>Laos
<!-- sic! -->
</td>
  </tr>
  <tr>
    <td><code>lv-LV</code></td>
    <td>Lettisch</td>
    <td>Lettland</td>
  </tr>
  <tr>
    <td><code>lt-LT</code></td>
    <td>Litauisch</td>
    <td>Litauen</td>
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
    <td>Macau</td>
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
