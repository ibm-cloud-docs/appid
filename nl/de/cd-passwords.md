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

# Kennwortrichtlinien definieren
{: #cd-strength}

Sie können die Anforderungen, die die mit Cloud Directory verwendeten Kennwörter erfüllen müssen, festlegen. Durch das Definieren spezieller Voraussetzungen, die Ihre Benutzer erfüllen müssen, können Sie die Sicherheit Ihrer Anwendungen verbessern.
{: shortdesc}

## Richtlinie: Kennwortsicherheit
{: #cd-password-strength}

Sichere Kennwörter sind schwerer oder sogar gar nicht durch Ausprobieren oder Algorithmen zu erraten. Zum Festlegen von Voraussetzungen für die Sicherheit eines Benutzerkennworts können Sie die folgenden Schritte ausführen.
{: shortdesc}

1. Wechseln Sie zur Registerkarte **Kennwortrichtlinien** im {{site.data.keyword.appid_short_notm}}-Dashboard.

2. Klicken Sie im Feld **Kennwortsicherheit definieren** auf **Bearbeiten**. Daraufhin wird eine Anzeige geöffnet.

3. Geben Sie im Feld **Kennwortsicherheit** eine gültige regex-Zeichenfolge an.

  Beispiele:
    - Muss aus mindestens acht Zeichen bestehen. (`^.{8,}$`)
    - Muss eine Ziffer, einen Kleinbuchstaben und einen Großbuchstaben enthalten. (`^(?:(?=.*\d)(?=.*[a-z])(?=.*[A-Z]).*)$`)
    - Darf nur im Englischen übliche Buchstaben und Ziffern enthalten. (`^[A-Za-z0-9]*$`)
    - Muss mindestens ein Sonderzeichen enthalten. (`^(\w)\w*?(?!\1)\w+$`)

4. Klicken Sie auf **Speichern**.

Die Kennwortsicherheit kann auf der Seite mit den Einstellungen für Cloud Directory in der {{site.data.keyword.appid_short_notm}}-Konsole oder unter Verwendung der <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.set_cloud_directory_password_regex" target="_blank">Management-APIs <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> festgelegt werden.
{: note}


## Erweiterte Kennwortrichtlinien
{: #cd-advanced-password}


Sie können die Sicherheit Ihrer Anwendung verbessern, indem Sie Kennworteinschränkungen definieren.
{: shortdesc}


Sie können eine erweiterte Kennwortrichtlinie erstellen, die aus einer beliebigen Kombination der folgenden fünf Features besteht:

 - Nach wiederholter Eingabe falscher Berechtigungsnachweise sperren
 - Kennwortwiederverwendung vermeiden
 - Ablauf der Kennwortgültigkeit
 - Mindestzeitraum zwischen Kennwortänderungen
 - Sicherstellen, dass das Kennwort nicht den Benutzernamen enthält


 Wenn Sie diese Funktion aktivieren, wird eine gesonderte Abrechnung für erweiterte Sicherheitsfunktionen aktiviert. Weitere Informationen finden Sie unter [Wie berechnet {{site.data.keyword.appid_short_notm}} die Kosten?](/docs/services/appid?topic=appid-faq#faq-pricing).
 {: important}


### Richtlinie: Kennwortwiederverwendung vermeiden
{: #cd-avoid-reuse}

Wenn Ihre Benutzer ihr Kennwort ändern, können Sie sie daran hindern, ein Kennwort auszuwählen, das bereits kurz zuvor verwendet wurde.
{: shortdesc}

Durch die Verwendung der GUI oder der API können Sie die Anzahl der Kennwörter auswählen, die ein Benutzer aufweisen muss, bevor das zuvor verwendete Kennwort erneut verwendet werden darf. Die Einstellungsoptionen umfassen jeden ganzzahligen Wert im Bereich von 1 - 10.

Falls diese Option aktiviert ist, kann ein Benutzer ein kürzlich verwendetes Kennwort nicht erneut verwenden. Wenn ein Benutzer versucht, für ein Kennwort das zuvor verwendete Kennwort erneut festzulegen, wird ein Fehler in der Standard-GUI des Anmelde-Widgets angezeigt und der Benutzer wird aufgefordert, ein anderes Kennwort einzugeben. 

Früher verwendete Kennwörter werden genauso sicher gespeichert wie das aktuelle Kennwort des Benutzers.
{: note}


### Richtlinie: Nach wiederholter Eingabe falscher Berechtigungsnachweise sperren
{: #cd-lockout}

Sie können die Konten Ihrer Benutzer schützen, indem Sie die Möglichkeit zum Anmelden vorübergehend blockieren, wenn ein verdächtiges Verhalten festgestellt wird (z. B. ein mehrmaliger Anmeldeversuch mit einem falschen Kennwort). Diese Maßnahme soll böswillige Versuche verhindern, durch Erraten des Kennworts Zugriff auf das Konto eines Benutzers zu erlangen.
{: shortdesc}

Durch die Verwendung der GUI oder der API können Sie die maximale Anzahl nicht erfolgreicher Anmeldeversuche festlegen, die ein Benutzer ausführen kann, bevor sein Konto temporär gesperrt wird. Sie können ferner definieren, wie lange diese Kontosperre dauern soll. Sie haben die folgenden Optionen:

* Anzahl der Versuche: Eine beliebige ganze Zahl zwischen 1 und 10.
* Sperrzeitraum: Ein beliebiger ganzzahliger Wert in Minuten im Bereich zwischen 1 Minute und 1440 Minuten (24 Stunden).

Wenn ein Konto gesperrt ist, können Benutzer sich weder anmelden noch andere Self-Service-Operationen wie Kennwortänderungen usw. vornehmen, bis der angegebene Sperrzeitraum abgelaufen ist. Wenn die Sperrfrist abgelaufen ist, wird der Benutzer automatisch entsperrt.

Sie haben de Möglichkeit, einen Benutzer zu entsperren, bevor der Sperrzeitraum abgelaufen ist. Um zu ermitteln, ob ein Benutzer gesperrt ist, müssen Sie prüfen, ob das Feld `active` auf `false` gesetzt ist. Sie können außerdem überprüfen, ob der Benutzerstatus auf der Registerkarte **Benutzer** des Service-Dashboards auf `disabled` gesetzt ist. Um einen Benutzer zu entsperren, müssen Sie [die API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Cloud_Directory_Users/updateCloudDirectoryUser) verwenden, um das Feld `active` auf `true` zu setzen.


### Richtlinie: Mindestzeitraum zwischen Kennwortänderungen
{: #cd-minimum-time}

Sie können verhindern, dass Ihre Benutzer ihr Kennwort in schneller Abfolge ändern, indem Sie eine Mindestdauer festlegen, die ein Benutzer zwischen den Kennwortänderungen warten muss.
{: shortdesc}

Dieses Feature ist besonders nützlich, wenn es in Verbindung mit der Richtlinie 'Kennwortwiederverwendung vermeiden' verwendet wird. Ohne diese Einschränkung kann ein Benutzer sein Kennwort mehrfach in kurzer Abfolge ändern, um die Einschränkung bei der Wiederverwendung von kürzlich verwendeten Kennwörtern zu umgehen. Sie können einen beliebigen Wert im Bereich von 1 und 720 Stunden (30 Tage) auswählen. Der Wert im Feld wird in Stunden angegeben.


### Richtlinie: Ablauf der Kennwortgültigkeit
{: #cd-expiration}

Aus Sicherheitsgründen sollten Sie erzwingen, dass die Benutzer ihr Kennwort nach einem bestimmten Zeitraum ändern.
{: shortdesc}

Wenn Sie die GUI oder die API verwenden, können Sie einen Zeitraum festlegen, für den die Kennwörter Ihres Benutzers gültig bleiben. Wenn das Kennwort eines Benutzers abgelaufen ist, muss er es bei der nächsten Anmeldung neu festlegen. Sie können eine beliebige Anzahl von vollen Tagen zwischen 1 und 90 auswählen.

Sie können sich rasch in die Verwendung des Anmeldewidgets einarbeiten, indem Sie die bereitgestellte Standard-GUI verwenden. Der Benutzer wird angewiesen, ein neues Kennwort anzugeben, erst danach kann die Anmeldung erfolgen.

Wenn Sie eine angepasste Anmeldeerfahrung verwenden, wird ein Fehler ausgelöst, wenn ein Benutzer versucht, sich mit einem abgelaufenen Kennwort anzumelden. Es liegt in Ihrer Verantwortung, Ihre Anwendung so zu konfigurieren, dass sie das erforderliche Benutzererlebnis bereitstellt. Sie können die API zum Ändern des Kennworts aufrufen, damit das neue Kennwort festgelegt werden kann.

Die Antwort des Tokenendpunkts hat etwa folgenden Inhalt:

```javascript
{
  "error" : "invalid_grant",
  "error_description" : "Password expired",
  "user_id" : "356e065e-49da-45f6-afa3-091a7b464f51"
}
```
{: screen}

Wenn diese Option zunächst auf "Ein" gesetzt ist, haben alle vorhandenen Benutzerkennwörter kein Ablaufdatum. Der Ablaufzeitraum beginnt für die Benutzer, wenn ihr Kennwort geändert wird. Fordern Sie die Benutzer dazu auf, ihr Kennwort zu ändern, wenn Sie dieses Feature auf "Ein" gesetzt haben.
{: note}


### Richtlinie: Stellen Sie sicher, dass das Kennwort nicht den Benutzernamen enthält. 
{: #cd-no-username}

Zur Verwendung sichererer Kennwörter möchten Sie möglicherweise verhindern, dass Benutzer ihren Benutzernamen oder einen Teil ihrer E-Mail-Adresse im Kennwort verwenden.
{: shortdesc}

Bei dieser Einschränkung muss die Groß-/Kleinschreibung nicht beachtet werden. Die Benutzer können die Groß-/Kleinschreibung einiger oder aller Zeichen nicht ändern, um persönliche Daten zu verwenden. Um diese Option zu konfigurieren, setzen Sie die Option auf **Ein**.
{: note}

