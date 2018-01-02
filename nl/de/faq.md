---

copyright:
  years: 2017
lastupdated: "2017-12-12"

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

Der Plan mit gestaffelten Preisstufen besteht aus zwei Teilen: der Anzahl von Authentifizierungsereignissen und der Anzahl berechtigter Benutzer. Die Gebühren werden momatlich auf der Basis der Zusammenfassung der beiden Teile erhoben. Der Gesamtpreis besteht aus der kumulativen Gebühr für jede Nutzungsstufe und setzt sich aus der Menge multipliziert mit dem Einzelpreis für die jeweilige Preisstufe zusammen.

### Authentifizierungsereignisse

Ein Authentifizierungsereignis findet statt, wenn ein neues {{site.data.keyword.appid_short_notm}}-Token ausgegeben wird. Für identifizierte Benutzer ist jedes neue Token eine Stunde lang gültig. Für anonyme Benutzer sind Tokens einen Monat lang gültig. Nach dem Ablaufen des Tokens müssen Sie ein neues Token erstellen, um auf geschützte Ressourcen zuzugreifen. Wenn Sie App ID für die mobile Authentifizierung verwenden, werde Benutzertokens in `key-store/key-chain` gespeichert und zu jeder zukünftigen Anforderung hinzugefügt. Auf die Tokens kann über das Android- oder iOS-Swift-SDK von {{site.data.keyword.appid_short_notm}} zugegriffen werden. Wenn Sie den Service für die Webauthentifizierung nutzen, <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">speichern Sie das Benutzertoken <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> in den Sitzungscookies.

### Berechtigte Benutzer

Bei einem berechtigten Benutzer handelt es sich um einen eindeutigen Benutzer, der sich direkt oder indirekt bei Ihrem Service anmeldet. Jede Mal, wenn sich ein neuer Benutzer über einen bestimmten Identitätsprovider anmeldet, werden Gebühren für einen berechtigten Benutzer erhoben; dies gilt auch für anonyme Benutzer. Beispiel: Wenn sich ein Benutzer über Facebook und zu einem späteren Zeitpunkt über Google anmeldet, wird er als zwei separate berechtigte Benutzer betrachtet.


Weitere Informationen zu gestaffelten Preisstufen finden Sie in der [{{site.data.keyword.Bluemix_notm}}-Dokumentation zu Preisstrukturen](/docs/pricing/index.html#pricing).
