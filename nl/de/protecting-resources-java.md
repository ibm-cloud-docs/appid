---

copyright:
  years: 2017
lastupdated: "2017-11-02"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Liberty for Java-Ressourcen schützen
{: #protecting-liberty}

Mit {{site.data.keyword.appid_short_notm}} können Sie Endpunkte in Ihren IBM Liberty for Java-Apps schützen. Liberty for Java bietet die integrierte Funktionalität für die Verarbeitung von Open ID Connect-Anforderungen (OIDC-Anforderungen).

## Vorbereitungen
{: #begin}

* Sie benötigen eine vorhandene, nicht gebundene [IBM Liberty for Java-Anwendung](https://console.bluemix.net/catalog/starters/liberty-for-java). Anhand der [Dokumentation](/docs/runtimes/liberty/index.html) können Sie sich mit der Entwicklung von Liberty for Java-Apps vertraut machen.
* [Apache Maven](https://maven.apache.org/download.cgi) muss installiert sein.
* Machen Sie sich mit der Funktionsweise von OIDC mit Liberty for Java vertraut.

## Ressourcen in Liberty for Java schützen
{: #protecting-liberty}

1. Laden Sie das Liberty for Java-Beispiel von der Benutzerschnittstelle herunter. Das Beispiel enthält eine ZIP-Datei mit den Liberty-Standarddateien.

2. Öffnen Sie das Terminal in dem Verzeichnis, in dem Sie das Beispiel entpackt haben.

3. Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} über die Cloud Foundry-Befehlszeile an. Geben Sie Ihre Berechtigungsnachweise ein, wenn Sie dazu aufgefordert werden.

  ```
  cf login
  ```
  {: codeblock}

4. Stellen Sie die Anwendung bereit. Mit dem folgenden Befehl wird eine Liberty for Java-Instanz mit einem Namen erstellt, der der Tenant-ID zugeordnet ist.

  ```
  cf push
  ```
  {: codeblock}

5. Binden Sie die Serviceinstanz an die neue Liberty for Java-Instanz und stellen Sie die Anwendung erneut bereit.

6. Öffnen Sie die Anwendung in einem Browser und melden Sie sich mit Ihren Berechtigungsnachweisen an, um die Authentifizierungsaktivitäten zu überprüfen.


## Liberty for Java-Beispiel aktualisieren
{: #updating-liberty}

Gehen Sie anhand der folgenden Anweisungen vor, wenn Sie eine Aktualisierung in der Beispiel-App vornehmen möchten:

1. Erstellen Sie die Servlets, JSPs und HTML.
2. Definieren Sie die geschützten Ressourcen und fügen Sie sie zu den Berechtigungsfiltern in `web.xml` und `server.xml` hinzu.
3. Erstellen Sie eine WAR-Datei und stellen Sie sie in Liberty for Java bereit.

Weitere Informationen zur Aktualisierung von Apps finden Sie in [{{site.data.keyword.appid_short_notm}} zu einer vorhandenen Anwendung hinzufügen](/docs/services/appid/existing.html#existing-liberty).
