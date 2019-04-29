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

# Kennwortrichtlinien definieren
{: #cd-strength}

Sie können die Anforderungen, die die mit Cloud Directory verwendeten Kennwörter erfüllen müssen, festlegen. Durch das Definieren spezieller Voraussetzungen, die Ihre Benutzer erfüllen müssen, können Sie die Sicherheit Ihrer Anwendungen verbessern.
{: shortdesc}

## Richtlinie: Kennwortsicherheit
{: #cd-password-strength}

Sichere Kennwörter sind schwerer oder sogar gar nicht durch Ausprobieren oder Algorithmen zu erraten. Zum Festlegen von Voraussetzungen für die Sicherheit eines Benutzerkennworts können Sie die folgenden Schritte ausführen.
{: shortdesc}

1. Navigieren Sie zur Registerkarte **Kennwortrichtlinien** des App ID-Dashboards.

2. Klicken Sie im Feld **Kennwortsicherheit definieren** auf **Bearbeiten**. Daraufhin wird eine Anzeige aufgerufen.

3. Geben Sie im Feld **Kennwortsicherheit** eine gültige regex-Zeichenfolge an.

  Beispiele:
    - Muss aus mindestens acht Zeichen bestehen. Regulärer Beispielausdruck: `^.{8,}$`
    - Muss eine Ziffer, einen Kleinbuchstaben und einen Großbuchstaben enthalten. Regulärer Beispielausdruck: `^(?:(?=.*\d)(?=.*[a-z])(?=.*[A-Z]).*)$`
    - Darf nur lateinische Buchstaben und arabische Ziffern enthalten. Regulärer Beispielausdruck: `^[A-Za-z0-9]*$`
    - Muss mindestens ein Sonderzeichen enthalten. Regulärer Beispielausdruck: `^(\w)\w*?(?!\1)\w+$`

4. Klicken Sie auf **Speichern**.

Die Kennwortsicherheit kann auf der Seite mit den Einstellungen für Cloud Directory in der {{site.data.keyword.appid_short_notm}}-Konsole oder unter Verwendung der <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.set_cloud_directory_password_regex" target="_blank">Management-APIs <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> festgelegt werden.
{: note}


## Erweiterte Kennwortrichtlinien
{: #cd-advanced-password}


Sie können die Sicherheit Ihrer Anwendung verbessern, indem Sie zusätzliche Kennworteinschränkungen definieren.
{: shortdesc}


Sie können eine erweiterte Kennwortrichtlinie erstellen, die aus einer beliebigen Kombination der folgenden fünf Features besteht:

 - Nach wiederholter Eingabe falscher Berechtigungsnachweise sperren
 - Kennwortwiederverwendung vermeiden
 - Ablauf der Kennwortgültigkeit
 - Mindestzeitraum zwischen Kennwortänderungen
 - Verwendung des Benutzernamens im Kennwort verhindern


 Wenn Sie dieses Feature aktivieren, fallen zusätzliche Kosten für die erweiterten Sicherheitsfunktionen an. Weitere Informationen zu diesem Thema finden Sie im Abschnitt [Wie wird die Preisstruktur in {{site.data.keyword.appid_short_notm}} berechnet?](/docs/services/appid?topic=appid-faq#faq-pricing).
 {: important}


### Richtlinie: Kennwortwiederverwendung vermeiden
{: #cd-avoid-reuse}

Wenn Ihre Benutzer ihr Kennwort ändern, können Sie sie daran hindern, ein Kennwort auszuwählen, das bereits kurz zuvor verwendet wurde.
{: shortdesc}

Mithilfe der GUI oder der API können Sie angeben, nach wie viel Kennwortänderungen ein bereits zuvor genutztes Kennwort nochmals verwendet werden kann. Sie können eine beliebige ganze Zahl zwischen 1 und 10 auswählen.

Wenn diese Option aktiviert ist, kann ein Benutzer kein Kennwort verwenden, das erst kürzlich von ihm verwendet wurde. Versucht ein Benutzer, ein erst kürzlich verwendetes Kennwort erneut festzulegen, dann wird in der standardmäßigen Anmeldewidget-GUI ein Fehler angezeigt und der Benutzer wird aufgefordert, ein anderes Kennwort einzugeben.

Früher verwendete Kennwörter werden genauso sicher gespeichert wie das aktuelle Kennwort des Benutzers.
{: note}


### Richtlinie: Nach wiederholter Eingabe falscher Berechtigungsnachweise sperren
{: #cd-lockout}

Sie können die Konten Ihrer Benutzer schützen, indem Sie die Möglichkeit zum Anmelden vorübergehend blockieren, wenn ein verdächtiges Verhalten festgestellt wird (z. B. ein mehrmaliger Anmeldeversuch mit einem falschen Kennwort). Diese Maßnahme soll böswillige Versuche verhindern, durch Erraten des Kennworts Zugriff auf das Konto eines Benutzers zu erlangen.
{: shortdesc}

Wenn Sie die GUI oder die API verwenden, können Sie die maximale Anzahl nicht erfolgreicher Anmeldeversuche festlegen, bis ein Konto vorübergehend gesperrt wird. Sie können auch die Zeitdauer festlegen, für die das Konto gesperrt ist. Sie haben die folgenden Optionen:

* Anzahl der Versuche: Eine beliebige ganze Zahl zwischen 1 und 10.
* Sperrzeitraum: Ein beliebiger ganzzahliger Wert in Minuten im Bereich zwischen 1 Minute und 1440 Minuten (24 Stunden).

Wenn ein Konto gesperrt ist, können sich Benutzer nicht anmelden oder andere Self-Service-Operationen ausführen (z. B. das Kennwort ändern), bis der angegebene Sperrzeitraum abgelaufen ist. Wenn die Sperrfrist abgelaufen ist, wird der Benutzer automatisch entsperrt.

Sie haben de Möglichkeit, einen Benutzer zu entsperren, bevor der Sperrzeitraum abgelaufen ist. Um zu ermitteln, ob ein Benutzer gesperrt ist, müssen Sie prüfen, ob das Feld `active` auf `false` gesetzt ist. Sie können außerdem überprüfen, ob der Benutzerstatus auf der Registerkarte **Benutzer** des Service-Dashboards auf `disabled` gesetzt ist. Um einen Benutzer zu entsperren, müssen Sie [die API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Cloud_Directory_Users/updateCloudDirectoryUser) verwenden, um das Feld `active` auf `true` zu setzen.


### Richtlinie: Mindestzeitraum zwischen Kennwortänderungen
{: #cd-minimum-time}

Sie können verhindern, dass Ihre Benutzer ihr Kennwort in schneller Abfolge ändern, indem Sie eine Mindestdauer festlegen, die ein Benutzer zwischen den Kennwortänderungen warten muss.
{: shortdesc}

Dieses Feature ist besonders nützlich, wenn es in Verbindung mit der Richtlinie 'Kennwortwiederverwendung vermeiden' verwendet wird. Ohne diese Einschränkung könnte ein Benutzer sein Kennwort mehrfach in schneller Folge ändern, um die Einschränkung bei der Wiederverwendung kürzlich genutzter Kennwörter zu umgehen. Sie können einen beliebigen Wert zwischen 1 Stunde und 30 Tagen (angegeben in Stunden) auswählen.


### Richtlinie: Ablauf der Kennwortgültigkeit
{: #cd-expiration}

Aus Sicherheitsgründen sollten Sie erzwingen, dass die Benutzer ihr Kennwort nach einer bestimmten Zeit ändern.
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


### Richtlinie: Verwendung des Benutzernamens im Kennwort verhindern
{: #cd-no-username}

Um die Kennwortsicherheit zu verbessern, muss verhindert werden, dass die Benutzer ihren Benutzernamen oder den ersten Teil ihrer E-Mail-Adresse im Kennwort verwenden.
{: shortdesc}

Bei dieser Einschränkung muss die Groß-/Kleinschreibung nicht beachtet werden. Allerdings können die Benutzer die Groß-/Kleinschreibung bestimmter Zeichen oder aller Zeichen nicht ändern, um die persönlichen Daten zu verwenden. Um diese Option zu konfigurieren, setzen Sie die Option auf **Ein**.

