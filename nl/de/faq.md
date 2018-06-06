---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-02"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# Häufige Fragen

Hier finden Sie Antworten auf häufig gestellte Fragen zum {{site.data.keyword.appid_full}}-Service.
{: shortdesc}


## Wie wird die Preisstruktur in {{site.data.keyword.appid_short_notm}} berechnet?
{: #pricing}

In {{site.data.keyword.appid_short_notm}} sinken die Kosten, je mehr Ressourcen Sie nutzen.
{: shortdesc}

Der Plan mit gestaffelten Preisstufen besteht aus zwei Teilen: der Anzahl von Authentifizierungsereignissen und der Anzahl berechtigter Benutzer. Die Gebühren werden monatlich auf der Basis der Zusammenfassung der beiden Teile erhoben. Der Gesamtpreis besteht aus der kumulativen Gebühr für jede Nutzungsstufe und setzt sich aus der Menge multipliziert mit dem Einzelpreis für die jeweilige Preisstufe zusammen.

### Authentifizierungsereignisse

Ein Authentifizierungsereignis findet statt, wenn ein neues {{site.data.keyword.appid_short_notm}}-Token ausgegeben wird. Für identifizierte Benutzer ist jedes neue Token eine Stunde lang gültig. Für anonyme Benutzer sind Tokens einen Monat lang gültig. Nach dem Ablaufen des Tokens müssen Sie ein neues Token erstellen, um auf geschützte Ressourcen zuzugreifen. Wenn Sie App ID für die mobile Authentifizierung verwenden, werde Benutzertokens in `key-store/key-chain` gespeichert und zu jeder zukünftigen Anforderung hinzugefügt. Auf die Tokens kann über das Android- oder iOS-Swift-SDK von {{site.data.keyword.appid_short_notm}} zugegriffen werden. Wenn Sie den Service für die Webauthentifizierung nutzen, <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">speichern Sie das Benutzertoken <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> in den Sitzungscookies.

### Berechtigte Benutzer

Bei einem berechtigten Benutzer handelt es sich um einen eindeutigen Benutzer, der sich direkt oder indirekt bei Ihrem Service anmeldet. Jede Mal, wenn sich ein neuer Benutzer über einen bestimmten Identitätsprovider anmeldet, werden Gebühren für einen berechtigten Benutzer erhoben; dies gilt auch für anonyme Benutzer. Beispiel: Wenn sich ein Benutzer über Facebook und zu einem späteren Zeitpunkt über Google anmeldet, wird er als zwei separate berechtigte Benutzer betrachtet.

Weitere Informationen zu gestaffelten Preisstufen finden Sie in der [{{site.data.keyword.Bluemix_notm}}-Dokumentation zu Preisstrukturen](/docs/billing-usage/how_charged.html#services).

</br>

## Welche Aktivitätstypen werden von App ID überwacht?
{: #activity-monitor}

Sie können Aktivitäten verfolgen, die in der App generiert werden, die an die Serviceinstanz gebunden ist. Darüber hinaus können Sie administrative Aktivitäten, die in App ID stattfinden, mithilfe des Activity Tracker-Service überwachen.

Gehen Sie wie folgt vor, um die von Ihrer App generierten Aktivitäten anzuzeigen:

1. Melden Sie sich bei Ihrem IBM Cloud-Konto an.
2. Wählen Sie im Dashboard Ihre App ID-Instanz aus.
3. Klicken Sie auf die Registerkarte **Übersicht**.
4. Zeigen Sie die im **Aktivitätenprotokoll** aufgeführten Aktivitäten an.

</br>
Überwachen administrativer Aktivitäten:

1. Melden Sie sich bei Ihrem IBM Cloud-Konto an. Navigieren Sie zu der Organisation und dem Bereich, in der bzw. dem Ihre App ID-Instanz bereitgestellt wird.
2. Stellen Sie über den Katalog eine Instanz des Activity Tracker-Service bereit. Stellen Sie sicher, dass Sie sich im selben Bereich befinden wie Ihre App ID-Instanz.
3. Klicken Sie im Activity Tracker-Dashboard auf die Registerkarte **Verwalten**.
4. Wählen Sie in der Dropdown-Liste die folgenden Konfigurationen aus, um nach Ereignissen zu suchen, die von App ID generiert wurden.
<table>
  <tr>
    <th> Feld </th>
    <th> Konfiguration </th>
  </tr>
  <tr>
    <td><i>Protokolle anzeigen</i></td>
    <td><b>Bereichsprotokolle</b></td>
  </tr>
  <tr>
    <td><i>Suchen</i></td>
    <td><b>target.name</b></td>
  </tr>
  <tr>
    <td>Filtern</td>
    <td>appid</td>
  </tr>
</table>
5. Klicken Sie auf **Filtern**.

Weitere Informationen zur Funktionsweise des Service finden Sie in der [Activity Tracker-Dokumentation](/docs/services/cloud-activity-tracker/index.html).
