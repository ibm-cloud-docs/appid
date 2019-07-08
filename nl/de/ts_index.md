---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-21"

keywords: authentication, authorization, identity, app security, secure, troubleshooting, help, support, requests, uri

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
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}

# Fehlerbehebung: Allgemein
{: #troubleshooting}

Wenn bei der Verwendung von {{site.data.keyword.appid_full}} Probleme auftreten, ziehen Sie die folgenden Verfahren zur Fehlerbehebung und zum Abrufen von Hilfe in Betracht.
{: shortdesc}

## Hilfe und Unterstützung anfordern
{: #ts-gettinghelp}

Sie können Hilfe erhalten, wenn Sie in einem Forum nach Informationen suchen oder Fragen stellen. Sie können auch ein Support-Ticket öffnen. Wenn Sie eine Frage über die Foren stellen, kennzeichnen Sie Ihre Frage, so dass sie von den {{site.data.keyword.cloud_notm}}-Entwicklerteams gesehen wird.
  * Bei technischen Fragen zu {{site.data.keyword.appid_short_notm}} posten Sie Ihre Frage unter <a href="https://stackoverflow.com/" target="_blank">Stack Overflow <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> und versehen Sie sie mit dem Tag "ibm-appid".
  * Bei Fragen zum Service und zu den ersten Schritten verwenden Sie das Forum <a href="https://developer.ibm.com/" target="_blank">dW Answers <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>. Schließen Sie das Tag `appid` ein.

Weitere Informationen zum Anfordern von Unterstützung finden Sie in [Informationen zur Vorgehensweise beim Anfordern von Unterstützung](/docs/get-support?topic=get-support-getting-customer-support#getting-customer-support).


## Ein Benutzer wird nach dem Anmelden nicht an die App weitergeleitet
{: #ts-signin-fail}

{: tsSymptoms}
Ein Benutzer meldet sich bei Ihrer Anwendung über die Anmeldeseite eines Identitätsproviders an. Entweder passiert nichts oder die Anmeldung schlägt fehl.

{: tsCauses}
Die Anmeldung kann aus folgenden Gründen fehlschlagen:

* Die Weiterleitungs-URL wurde nicht ordnungsgemäß zur [Whitelist](/docs/services/appid?topic=appid-faq#faq-redirect) hinzugefügt.
* Der Benutzer ist nicht berechtigt.
* Der Benutzer versuchte, sich mit falschen Berechtigungsnachweisen anzumelden.

{: tsResolve}
Damit eine Weiterleitung stattfindet, führen Sie folgende Schritte aus:

* Überprüfen Sie, dass Ihre Weiterleitungs-URL richtig ist. Sie muss exakt sein, damit die Weiterleitung funktioniert.
* Stellen Sie sicher, dass der Benutzer sich mit den korrekten Berechtigungsnachweisen anmeldet.
* Überprüfen Sie, dass die Benutzer in den Benutzereinstellungen des Identitätsproviders konfiguriert sind.



## Angepasster URI wird zurückgewiesen
{: #ts-custom-uri}

{: tsSymptoms}
Wenn Sie eine Web-Weiterleitungs-URL eingeben, die ein angepasstes URL-Schema verwendet, wird sie von der {{site.data.keyword.appid_short_notm}}-Konsole zurückgewiesen.

{: tsCauses}
Die URL kann aus den folgenden Gründen zurückgewiesen werden:

* Die URL entspricht nicht dem `http`- oder `https`-Schema
* Die URL endet mit `://`
* Es ist ein typografischer Fehler in Ihrer URL enthalten

Die Einschränkungen gelten aus Sicherheitsgründen.

{: tsResolve}
Um das Problem zu beheben, prüfen Sie, ob die URL korrekt ist. Wenn Ihre URL den Anforderungen nicht entspricht, können Sie einen HTTPS-Endpunkt in Ihrer App erstellen, um den empfangenen Erteilungscode an Ihre angepasste URL umzuleiten. Geben Sie den erstellten Endpunkt als Weiterleitungs-URL in der {{site.data.keyword.appid_short_notm}}-Konsole an. Weitere Informationen zu Weiterleitungs-URIs finden Sie in [Weiterleitungs-URIs hinzufügen](/docs/services/appid?topic=appid-managing-idp#add-redirect-uri).

## Ein Benutzer wird nach dem Anmelden nicht an den Identitätsprovider weitergeleitet
{: #ts-redirect}

{: tsSymptoms}
Ein Benutzer versucht, sich bei Ihrer Anwendung anzumelden, aber die Anmeldeseite wird nicht angezeigt, wenn die Systemanfrage erfolgt.

{: tsCauses}
Der Identitätsprovider kann aus folgenden Gründen fehlschlagen:

* Die von Ihnen konfigurierte Weiterleitungs-URL ist falsch.
* Der Identitätsprovider erkennt die Authentifizierungsanforderung nicht.
* Der Identitätsprovider erwartet eine HTTP-POST-Bindung.
* Der Identitätsprovider erwartet eine signierte authnRequest.

{: tsResolve}
Sie können eine der folgenden Lösungen ausprobieren:

* Aktualisieren Sie Ihre Anmelde-URL. Diese URL wird als Teil der authnRequest gesendet und muss exakt sein.
* Stellen Sie sicher, dass Ihre {{site.data.keyword.appid_short_notm}}-Metadaten in den Einstellungen des Identitätsproviders korrekt definiert sind.
* Konfigurieren Sie Ihren Identitätsprovider so, dass er die authnRequest in der HTTP-Weiterleitung (HTTP-Redirect) akzeptiert.
* {{site.data.keyword.appid_short_notm}} unterstützt die Signierung von authnRequests nicht.

Falls keine dieser Lösungen Abhilfe bringt, liegt möglicherweise ein Verbindungsproblem vor.
{: tip}


## Ein Attribut zeigt den falschen Wert an
{: #ts-saml-attribute}

{: tsSymptoms}
Ein Attributwert ist in einem Benutzerprofil vorhanden, er ist jedoch nicht dem richtigen Attribut zugeordnet.

{: tsCauses}
Das Benutzerprofilattribut ist nicht ordnungsgemäß zugeordnet.

{: tsResolve}
Ordnen Sie das Attribut in den Einstellungen Ihres Identitätsproviders zu. {{site.data.keyword.appid_short_notm}} erwartet die folgenden Attribute:
* `Name`
* `E-Mail`
* `Ländereinstellung`
* `Bild`



## Fehler: Zu viele Anforderungen
{: #ts-requests}

{: tsSymptoms}
Sie versuchen, die Homepage Ihrer App anzuzeigen, empfangen jedoch den folgenden Fehler:

```
{"error_code":"too many requests","error_description":"too many requests"}
```
{: screen}

{: tsCauses}
Möglicherweise erhalten Sie einen Fehler aufgrund zu vieler Anforderungen, wenn Sie automatisierte Tests mit nur einem virtuellen Benutzer durchführen. Jeder Benutzer kann innerhalb eines Zeitraums von einer Minute maximal fünf Anmeldeversuche durchführen. Die Anzahl der Anmeldeversuche wird begrenzt, um Brute-Force-DDOS und andere Typen ähnlicher Attacken zu verhindern.

{: tsResolve}
Um das Problem zu beheben, können Sie beim Durchführen von Tests mehrere virtuelle Benutzer verwenden.
</br>
