---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:tip: .tip}

# Lernprogramm zur Einführung
{: #gettingstarted}

Anwendungssicherheit kann unglaublich kompliziert sein. Für die meisten Entwickler stellt das Thema Sicherheit eine der größten Herausforderungen beim Erstellen einer App dar. Wie können Sie sicher sein, dass Sie die Daten Ihrer Benutzer erfolgreich schützen? Durch die Integration von {{site.data.keyword.appid_full}} in Ihren Apps können Sie selbst dann Ressourcen schützen und eine Authentifizierung hinzufügen, wenn Sie nicht viel Erfahrung mit Sicherheitsfunktionen haben.
{: shortdesc}

Dadurch, dass Benutzer sich bei Ihrer App anmelden müssen, können Sie Benutzerdaten wie App-Benutzervorgaben oder Informationen aus öffentlichen Profilen von sozialen Medien speichern und diese Daten anschließend nutzen, um die einzelnen Erfahrung mit der App anzupassen. App ID bietet Ihnen ein Anmeldeframework. Sie können aber auch Ihre eigenen, an Ihr Brand-Marketing angepassten Anmeldeanzeigen verwenden, wenn Sie mit dem Cloudverzeichnis arbeiten.

Als Kontoeigner können Sie jetzt Richtlinien festlegen, die definieren, wie Mitglieder Ihres Teams mit Instanzen von {{site.data.keyword.appid_short_notm}} interagieren können. Sie können entscheiden, wer berechtigt ist, Instanzen des Service zu erstellen, zu aktualisieren und zu löschen. Weitere Informationen finden Sie in [Servicezugriffsverwaltung](/docs/services/appid/iam.html).
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

1. Nach dem Erstellen einer Instanz des Service können Sie eine Beispielapp in der von Ihnen bevorzugten Arbeitssprache auswählen. Sie können iOS Swift, Android, Node.js und Java auswählen. Sie möchten kein SDK verwenden? Sie können {{site.data.keyword.appid_short_notm}} mithilfe der APIs integrieren. 
2. Führen Sie in der GUI die Schritte zur **Erstellung und Ausführung** der Beispielapp aus. Die Konfigurationen der einzelnen Sprachen weisen geringfügige Unterschiede auf, daher müssen Sie die Sprache der App auswählen, die Sie über die Dropdown-Liste heruntergeladen haben. Nachdem die App konfiguriert ist, können Sie sie in einem Browser öffnen und sich mit Ihren Berechtigungsnachweisen anmelden. Stellen Sie sicher, dass die Voraussetzungen für Ihre App-Sprache installiert sind.
  <dl>
    <dt> Android </dt>
      <dd><ul><li> Android API 27 oder höher </li><li> Java 8.x </li><li> Android SDK Tools 25.2.5+ </li><li> Android SDK Platform Tools 26.1.1+ </li><li> Android Build Tools Version 27.0.0+</li></ul></dd>
    <dt> iOS Swift </dt>
      <dd><ul><li> CocoaPods (Version 1.1.0 oder höher) </li><li> iOS 10.0 oder höher </li><li> MacOS 10.11.5 </li><li> Xcode (Version 9.0.1 oder höher) </li></ul></dd>
    <dt> Node.js </dt>
      <dd><ul><li> {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle</li></ul></dd>
    <dt> Java </dt>
      <dd><ul><li> {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle </li><li> Maven </li></ul></dd>
  </dl>

  Die von Ihnen gesuchte Sprache wird nicht angezeigt? Kein Problem! Sie können mithilfe der APIs von {{site.data.keyword.appid_short_notm}} profitieren. Informieren Sie sich auch anhand <a href="https://www.ibm.com/blogs/bluemix/tag/app-id/" target="_blank">unserer Blogs<img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> über zusätzliche Hilfe in anderen Sprachen. {: tip}

3. Klicken Sie auf **Aktivität überprüfen**, um die Authentifizierungsereignisse anzuzeigen, die aufgetreten sind. Nachdem Sie sich angemeldet haben, können Sie ein Ereignis sehen.
4. Passen Sie die Anmeldeschnittstelle an. Sie können ein Bild, z. B. ein Logo, und eine Headerfarbe auswählen. Sie können eine der Farboptionen auswählen oder einen Hexadezimalwert eingeben. Wenn Sie mit der Vorschau zufrieden sind, klicken Sie auf **Änderungen speichern**.
5. Aktualisieren Sie die Anmeldeseite im Browser. Die im vorhergehenden Schritt vorgenommenen Änderungen werden bereits angezeigt.

## Nächste Schritte
{: #next}

Sind Sie bereit, loszulegen und mit Ihren eigenen Apps zu beginnen? Fangen Sie an, indem Sie den [Service zu Ihrer App hinzufügen](/docs/services/appid/install.md). Vom Service werden SDKs für die am häufigsten verwendeten Sprachen zur Verfügung gestellt. Wird für die Sprache, in der Ihre App geschrieben ist, jedoch kein SDK angezeigt, können Sie immer noch die API verwenden. 

</br>
</br>
