---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:tip: .tip}

# Lernprogramm zur Einführung
{: #gettingstarted}

Anwendungssicherheit kann unglaublich kompliziert sein. Für die meisten Entwickler ist es der schwierigste Teil bei der Erstellung einer App. Wie können Sie sicher sein, dass Sie die Benutzerdaten schützen? Durch die Integration der IBM® Cloud App-ID in Ihre Apps, können Sie selbst dann Ressourcen schützen und Authentifizierung hinzufügen, wenn Sie nicht viel Erfahrung mit Sicherheitsfunktionen haben.
{: shortdesc}

Dadurch, dass Benutzer sich bei Ihrer App anmelden müssen, können Sie Benutzerdaten wie App-Benutzervorgaben oder Informationen aus öffentlichen Profilen von sozialen Medien speichern und diese Daten anschließend nutzen, um die einzelnen Erfahrung mit der App anzupassen. Die App-ID bietet Ihnen ein Protokoll im Framework. Sie können aber auch Ihre eigenen geschützten Anmeldeanzeigen verwenden, wenn Sie mit dem Cloudverzeichnis arbeiten. 


Als Kontoeigner können Sie jetzt Richtlinien festlegen, die definieren, wie Mitglieder Ihres Teams mit Instanzen von {{site.data.keyword.appid_short_notm}} interagieren können. Sie können entscheiden, wer berechtigt ist, Instanzen des Service zu erstellen,  zu aktualisieren und zu löschen. Weitere Informationen finden Sie in [Servicezugriffsverwaltung](/docs/services/appid/iam.html).
{:tip}

## Serviceinstanz erstellen
{: #create}

Eine Instanz von {{site.data.keyword.appid_short_notm}} erstellen und an Ihre App binden, um zu starten.
{: shortdesc}

1. Wählen Sie im {{site.data.keyword.Bluemix}}-Katalog den Eintrag {{site.data.keyword.appid_short_notm}} aus. Der Bildschirm für die Servicekonfiguration wird angezeigt.
2. Geben Sie Ihrer Serviceinstanz einen Namen oder verwenden Sie den voreingestellten Namen.
3. Wählen Sie Ihren Preistarif aus und klicken Sie auf **Erstellen**.
4. Binden Sie Ihre Instanz von {{site.data.keyword.appid_short_notm}}.
    1. Klicken Sie auf **Verbindungen**, um eine Liste mit Apps anzuzeigen, die Sie an Ihre Serviceinstanz binden können.
    2. Klicken Sie auf **Verbindung erstellen**. Eine Seite mit allen Apps, die über eine Bindungsoption verfügen, wird angezeigt. 
    3. Klicken Sie auf der App, die Sie verbinden möchten, auf **Verbinden**. 
    4. Klicken Sie auf **Erneutes Staging**, um die Änderung anzuwenden. 

Das ist alles! Sie können nun mit der Konfiguration Ihrer Anwendungseinstellungen beginnen.


## Beispiel-App konfigurieren
{: #sample-app}

Sie können eine der vorkonfigurierten Beispielapps verwenden, um sich mit der Verwendung des Service vertraut zu machen.
{: shortdesc}

Diese Out-of-the-box-Beispielapps sind mit zwei Identitätsprovidern und einer Funktion zu Überprüfung der Authentifizierung konfiguriert. Darüber hinaus können Sie das Anmeldewidget-Feature zum Anpassen einer Anmeldeseite verwenden und beobachten, wie schnell die von Ihnen vorgenommenen Aktualisierungen in der App angezeigt werden.

Gehen Sie wie folgt vor, um eine Beispielapp über die GUI zu konfigurieren:

1. Nach dem Erstellen einer Instanz des Service können Sie eine Beispielapp in der von Ihnen bevorzugten Arbeitssprache auswählen. Sie können iOS Swift, Android, Node.js und Java auswählen. Sie möchten kein SDK verwenden? Befassen Sie sich mit diesem Beispiel, um mit der <a href="https://github.com/mnsn/appid-python-flask-example" target="_blank">Verwendung von {{site.data.keyword.appid_short_notm}} mit anderen Sprachen, z. B. Python <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> zu beginnen.
2. Führen Sie in der GUI die Schritte zur **Erstellung und Ausführung** der Beispielapp aus. Die Konfigurationen der einzelnen Sprachen weisen geringfügige Unterschiede auf, daher müssen Sie die Sprache der App auswählen, die Sie über die Dropdown-Liste heruntergeladen haben. Nachdem die App konfiguriert ist, können Sie sie in einem Browser öffnen und sich mit Ihren Berechtigungsnachweisen anmelden. Stellen Sie sicher, dass die Voraussetzungen für Ihre App-Sprache installiert sind. 
  <dl>
    <dt> Android </dt>
      <dd><ul><li> Android API 25 oder höher </li><li> Java 8.x </li><li> Android SDK Tools 25.2.5+ </li><li> Android SDK Platform Tools 25.0.3+ </li><li> Android Build Tools Version 25.0.2 </li></ul></dd>
    <dt> iOS Swift </dt>
      <dd><ul><li> CocoaPods (Version 1.1.0 oder höher) </li><li> iOS 9 oder höher </li><li> MacOS 10.11.5 </li><li> Xcode (Version 9.0.1 oder höher) </li></ul></dd>
    <dt> Node.js </dt>
      <dd><ul><li> Cloud Foundry-CLI </li></ul></dd>
    <dt> Java </dt>
      <dd><ul><li> Cloud Foundry-CLI </li><li> Maven </li></ul></dd>
  </dl>
3. Klicken Sie auf **Aktivität überprüfen**, um die Authentifizierungsereignisse anzuzeigen, die aufgetreten sind. Nachdem Sie sich angemeldet haben, können Sie ein Ereignis sehen. 
4. Passen Sie die Anmeldeschnittstelle an. Sie können ein Bild, z. B. ein Logo, und eine Headerfarbe auswählen. Sie können eine der Farboptionen auswählen oder einen Hexadezimalwert eingeben. Wenn Sie mit der Vorschau zufrieden sind, klicken Sie auf **Änderungen speichern**.
5. Aktualisieren Sie die Anmeldeseite im Browser. Die im vorhergehenden Schritt vorgenommenen Änderungen werden bereits angezeigt.
