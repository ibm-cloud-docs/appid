---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Lernprogramm zur Einführung
{: #gettingstarted}

{{site.data.keyword.appid_full}} unterstützt Sie beim Hinzufügen einer Authentifizierung zu Ihren mobilen Apps und Web-Apps und schützt Ihre Back-End-Ressourcen.
{: shortdesc}

## Serviceinstanz erstellen
{: #create}

Erstellen Sie als ersten Schritt eine Instanz von {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

1. Wählen Sie im {{site.data.keyword.Bluemix}}-Katalog den Eintrag {{site.data.keyword.appid_short_notm}} aus. Der Bildschirm für die Servicekonfiguration wird angezeigt.
2. Geben Sie Ihrer Serviceinstanz einen Namen oder verwenden Sie den voreingestellten Namen.
3. Wählen Sie zum Binden der Instanz eine App aus dem Menü **Verbindung herstellen zu** aus. Wenn Sie **Nicht binden** auswählen, können Sie die Serviceinstanz auch später binden.
4. Wählen Sie Ihren Preistarif aus und klicken Sie auf **Erstellen**.

## Beispiel-App konfigurieren
{: #sample-app}

Sie können eine der vorkonfigurierten Beispielapps verwenden, um sich mit der Verwendung des Service vertraut zu machen.
{: shortdesc}

Diese Out-of-the-box-Beispielapps sind mit zwei Identitätsprovidern und einer Funktion zu Überprüfung der Authentifizierung konfiguriert. Darüber hinaus können Sie das Anmeldewidget-Feature zum Anpassen einer Anmeldeseite verwenden und beobachten, wie schnell die von Ihnen vorgenommenen Aktualisierungen in der App angezeigt werden.

Gehen Sie wie folgt vor, um eine Beispielapp über die GUI zu konfigurieren:

1. Nach dem Erstellen einer Instanz des Service können Sie eine Beispielapp in der von Ihnen bevorzugten Sprache auswählen. Sie können iOS Swift, Android, Node.js und Java auswählen. Sie möchten kein SDK verwenden? Lesen Sie den Blog zur <a href="https://github.com/mnsn/appid-python-flask-example" target="_blank">Verwendung von {{site.data.keyword.appid_short_notm}} mit anderen Sprachen, z. B. Python <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>.
2. Führen Sie in der GUI die Schritte zur **Erstellung und Ausführung** der Beispielapp aus. Die Konfigurationen der einzelnen Sprachen weisen geringfügige Unterschiede auf, daher müssen Sie die Sprache der App auswählen, die Sie über die Dropdown-Liste heruntergeladen haben. Nachdem die App konfiguriert ist, können Sie sie in einem Browser öffnen und sich mit Ihren Berechtigungsnachweisen anmelden.
  **Hinweis**: Stellen Sie sicher, dass die Voraussetzungen für die gewünschte Sprache installiert sind.
  <dl>
    <dt> Android </dt>
      <dd><ul><li> Android API 25 oder höher</li><li> Java 8.x </li><li> Android SDK Tools 25.2.5+ </li><li> Android SDK Platform Tools 25.0.3+ </li><li> Android Build Tools Version 25.0.2 </li></ul></dd>
    <dt> iOS Swift </dt>
      <dd><ul><li> CocoaPods (Version 1.1.0 oder höher) </li><li> iOS 9 oder höher</li><li> MacOS 10.11.5 </li><li> Xcode 8.1 25.0.3+ </li></ul></dd>
    <dt> Node.js </dt>
      <dd><ul><li> Cloud Foundry-CLI </li></ul></dd>
    <dt> Java </dt>
      <dd><ul><li> Cloud Foundry-CLI </li><li> Maven </li></ul></dd>
  </dl>
3. Klicken Sie auf **Aktivität überprüfen**, um die Authentifizierungsereignisse anzuzeigen, die aufgetreten sind. Nach der Anmeldung sollte mindestens ein Ereignis angezeigt werden.
4. Passen Sie die Anmeldeschnittstelle an. Sie können ein Bild, z. B. ein Logo, und eine Headerfarbe auswählen. Sie können eine der Farboptionen auswählen oder einen Hexadezimalwert eingeben. Wenn Sie mit der Vorschau zufrieden sind, klicken Sie auf **Änderungen speichern**. In der folgenden Abbildung ist ein Beispiel für die Anmeldeschnittstelle dargestellt.
5. Aktualisieren Sie die Anmeldeseite im Browser. Die im vorhergehenden Schritt vorgenommenen Änderungen werden bereits angezeigt.
