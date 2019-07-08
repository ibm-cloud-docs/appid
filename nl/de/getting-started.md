---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-06"

keywords: Authentication, authorization, identity, app security, secure, development,

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

# Lernprogramm zur Einführung
{: #getting-started}

Anwendungssicherheit kann unglaublich kompliziert sein. Für die meisten Entwickler stellt das Thema Sicherheit eine der größten Herausforderungen beim Erstellen einer App dar. Wie können Sie sicher sein, dass Sie die Daten Ihrer Benutzer erfolgreich schützen? Durch die Integration von {{site.data.keyword.appid_full}} in Ihren Apps können Sie selbst dann Ressourcen schützen und eine Authentifizierung hinzufügen, wenn Sie nicht viel Erfahrung mit Sicherheitsfunktionen haben.
{: shortdesc}

Dadurch, dass Benutzer sich bei Ihrer App anmelden müssen, können Sie Benutzerdaten wie App-Benutzervorgaben oder Informationen aus öffentlichen Profilen von sozialen Medien speichern und diese Daten anschließend nutzen, um die einzelnen Erfahrung mit der App anzupassen. {{site.data.keyword.appid_short_notm}} bietet Ihnen ein Framework. Sie können aber auch eigene, an Ihr Brand-Marketing angepasste Anmeldeanzeigen verwenden, wenn Sie mit Cloud Directory arbeiten.

Wir freuen uns über Ihr Feedback und beantworten gern Ihre Fragen!
* Bei technischen Fragen zu {{site.data.keyword.appid_short_notm}} posten Sie Ihre Frage unter <a href="https://stackoverflow.com" target="_blank">Stack Overflow <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> und versehen Sie sie mit dem Tag `ibm-appid`.
* Bei Fragen zum Service und zu den ersten Schritten verwenden Sie das Forum <a href="https://developer.ibm.com" target="_blank">dW Answers <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>. Schließen Sie das Tag `appid` ein.

## Serviceinstanz erstellen
{: #create}

Eine Instanz von {{site.data.keyword.appid_short_notm}} erstellen und an Ihre App binden, um zu starten.
{: shortdesc}

1. Wählen Sie im {{site.data.keyword.cloud_notm}}-Katalog den Eintrag {{site.data.keyword.appid_short_notm}} aus. Der Bildschirm für die Servicekonfiguration wird angezeigt.
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

Diese Out-of-the-box-Beispielapps sind mit zwei Identitätsprovidern und einer Funktion zu Überprüfung der Authentifizierung konfiguriert. Beispiele für Apps werden in `iOS Swift`, `Android`, `Node.js` und `Java` angeboten. Wenn Sie keine Sprache sehen, mit der Sie vertraut sind, ist das kein Problem! Sie können {{site.data.keyword.appid_short_notm}} in Ihre eigene Beispielanwendung integrieren, indem Sie die zur Verfügung gestellten APIs verwenden.

Gehen Sie wie folgt vor, um eine Beispielapp zu erstellen:

1. Klicken Sie auf **Beispiel herunterladen**.
2. Klicken Sie auf die Sprache Ihrer Wahl, um das Beispiel herunterzuladen.
  Die von Ihnen gesuchte Sprache wird nicht angezeigt? Kein Problem! Sie können mithilfe der APIs von {{site.data.keyword.appid_short_notm}} profitieren.
  {: tip}
3. Stellen Sie sicher, dass die Voraussetzungen installiert bzw. erfüllt sind.
4. Führen Sie die Schritte unter **Erstellung und Ausführung** aus, um das Beispiel mit {{site.data.keyword.appid_short_notm}} einzurichten.
5. Klicken Sie auf **Aktivität überprüfen**, um die Authentifizierungsereignisse anzuzeigen, die aufgetreten sind. Jede Anmeldung führt zu einem Ereignis, das auf dieser Seite sichtbar ist.
6. Passen Sie das Anmeldewidget an.
  1. Fügen Sie ein Bild wie z. B. ein Markenlogo hinzu, indem Sie auf **Auswählen** klicken und Ihr lokales System nach einem hochzuladenden Bild durchsuchen.
  2. Wählen Sie ein Farbschema aus, indem Sie entweder eine der Farboptionen auswählen oder einen Hexadezimalwert angeben.
  3. Wechseln Sie zwischen 'Web' und 'Mobil', um zu sehen, wie das Farbschema auf den verschiedenen Gerätetypen dargestellt wird.
  4. Wenn Sie die gewünschten Optionen gewählt haben, klicken Sie auf **Änderungen speichern**.
7. Aktualisieren Sie die Anmeldeseite im Browser. Die im vorhergehenden Schritt vorgenommenen Änderungen werden bereits angezeigt.


## Nächste Schritte
{: #next}

Sind Sie bereit, loszulegen und mit Ihren eigenen Apps zu beginnen? Fangen Sie an, indem Sie den [Service zu Ihrer App hinzufügen](/docs/services/appid?topic=appid-web-apps#web-apps). Vom Service werden SDKs für die am häufigsten verwendeten Sprachen zur Verfügung gestellt. Wird für die Sprache, in der Ihre App geschrieben ist, jedoch kein SDK angezeigt, können Sie {{site.data.keyword.appid_short_notm}} immer noch nutzen, indem Sie die APIs verwenden.
