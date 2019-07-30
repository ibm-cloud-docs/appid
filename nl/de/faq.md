---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-17"

keywords: authentication, authorization, identity, app security, secure

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
{:faq: data-hd-content-type='faq'}


# Häufige gestellte Fragen
{: #faq}

Hier finden Sie Antworten auf häufig gestellte Fragen (FAQs = Frequently Asked Questions) zum {{site.data.keyword.appid_full}}-Service.
{: shortdesc}


## Wie wird die Preisstruktur in {{site.data.keyword.appid_short_notm}} berechnet?
{: #faq-pricing}
{: faq}

In {{site.data.keyword.appid_short_notm}} sinken die Kosten, je mehr Ressourcen Sie nutzen.
{: shortdesc}

Der Plan mit gestaffelten Preisstufen besteht aus drei Teilen: der Anzahl von Authentifizierungsereignissen, regulärer und erweiterter Sicherheit sowie der Anzahl berechtigter Benutzer. Die Gebühren werden monatlich auf der Basis der Zusammenfassung der beiden Teile erhoben. Der Gesamtpreis besteht aus der kumulativen Gebühr für jede Nutzungsstufe und setzt sich aus der Menge multipliziert mit dem Einzelpreis für die jeweilige Preisstufe zusammen.

Ihre ersten 1000 Authentifizierungsereignisse und die ersten 1000 autorisierten Benutzer sind jeden Monat kostenlos. Ausgenommen hiervon sind lediglich erweiterte Sicherheitsereignisse. Für erweiterte Sicherheitsereignisse fallen zusätzliche Kosten an.

### Authentifizierungsereignisse
{: #faq-authentication}

Ein Authentifizierungsereignis findet statt, wenn ein neues reguläres oder anonymes Zugriffstoken ausgegeben wird. Token können als Antwort auf eine Anmeldeanforderung ausgegeben werden, die von einem Benutzer oder im Namen des Benutzers durch eine App eingeleitet wird. Standardmäßig sind Zugriffstokens für eine Stunde gültig und anonyme Tokens sind für 30 Tage gültig. Nach dem Ablaufen des Tokens müssen Sie ein neues Token erstellen, um auf geschützte Ressourcen zuzugreifen. Sie können die Ablaufzeit der {{site.data.keyword.appid_short_notm}}-Tokens auf der Seite **Identitätsprovider > Verwalten > Authentifizierungseinstellungen** des Service-Dashboards aktualisieren.

#### Erweiterte Sicherheitsfeatures

Erweiterte Sicherheitsfeatures bieten Ihnen die Möglichkeit, die Sicherheit Ihrer Anwendung zu erhöhen.
{: shortdesc}

<table>
  <tr>
    <th>Feature</th>
    <th>Vorteil</th>
  </tr>
  <tr>
    <td>Mehrfaktorauthentifizierung</td>
    <td>[MFA for Cloud Directory](/docs/services/appid?topic=appid-cd-mfa#cd-mfa) bestätigt die Identität eines Benutzers, indem ein Benutzer aufgefordert wird, neben seiner E-Mail-Adresse und dem Kennwort auch einen einmaligen Kenncode einzugeben, der an seine E-Mail-Adresse gesendet wird.</td>
  </tr>
  <tr>
    <td>Kennwortrichtlinienmanagement</td>
    <td>Als Kontoinhaber können Sie die Kennwortsicherheit für Cloud Directory verbessern, indem Sie eine Gruppe von Regeln konfigurieren, denen die Benutzerkennwörter entsprechen müssen. Beispiele: Die Anzahl der versuchten Anmeldeversuche vor einer Sperrung, bestimmte Ablaufzeiten, ein Mindestzeitraum zwischen Kennwortänderungen oder eine Begrenzung der Häufigkeit, mit der ein Kennwort wiederholt werden kann. Eine vollständige Liste der Optionen und Informationen zur Konfiguration finden Sie unter [Erweitertes Kennwortmanagement](/docs/services/appid?topic=appid-cd-strength#cd-advanced-password).</td>
  </tr>
</table>

Die erweiterten Sicherheitsfeatures sind standardmäßig inaktiviert. Wenn Sie die Mehrfaktorauthentifizierung (MFA) oder das Kennwortrichtlinienmanagement aktivieren, fallen zusätzliche Kosten an. Wenn Sie alle erweiterten Features inaktivieren, wird Ihr Konto auf die kostengünstigere Richtlinie zurückgesetzt. Beispiel: Angenommen, Sie haben 10.000 Zugriffstokens erhalten. Anschließend haben Sie das Kennwortrichtlinienmanagement aktiviert und 10.000 weitere erhalten. In diesem Fall fallen Kosten für 20.000 Authentifizierungsereignisse und für 10.000 zusätzliche Sicherheitsereignisse an.

Diese Features sind nur für die Instanzen verfügbar, die im Plan mit gestaffelten Preisstufen enthalten sind und die nach dem 15. März 2018 erstellt wurden.
{: note}

### Berechtigte Benutzer
{: #faq-authorized}

Bei einem berechtigten Benutzer handelt es sich um einen eindeutigen Benutzer, der sich direkt oder indirekt bei Ihrem Service anmeldet (dies schließt anonyme Benutzer ein). Jede Mal, wenn sich ein neuer Benutzer bei Ihrer Anwendung anmeldet, werden Gebühren für einen berechtigten Benutzer erhoben; dies gilt auch für anonyme Benutzer. Beispiel: Wenn sich ein Benutzer über Facebook und zu einem späteren Zeitpunkt über Google anmeldet, wird er als zwei separate berechtigte Benutzer betrachtet.

Um die aktuellsten Preisinformationen zu erfahren, können Sie einen Kostenvoranschlag erstellen. Klicken Sie hierzu im Abschnitt für {{site.data.keyword.appid_short_notm}} des [{{site.data.keyword.cloud_notm}}-Katalogs](https://cloud.ibm.com/catalog/services/app-id) auf **Zur Schätzung hinzufügen**.
{: tip}



## Warum muss ich meinen Weiterleitungs-URI auf die Whitelist setzen?
{: #faq-redirect}
{: faq}

Ein Weiterleitungs-URI ist der Callback-Endpunkt Ihrer App. Um Phishing-Attacken zu vermeiden, überprüft {{site.data.keyword.appid_short_notm}} den URI mithilfe der Whitelist der Weiterleitungs-URIs. Wenn Phishing auftritt, kann ein Nichtberechtigter unter Umständen Zugriff auf Ihre Benutzertokens erhalten. Weitere Informationen zu Weiterleitungs-URIs finden Sie in [Weiterleitungs-URIs hinzufügen](/docs/services/appid?topic=appid-managing-idp#add-redirect-uri).

Schließen Sie keine Abfrageparameter in Ihre URL ein. Diese werden im Validierungsprozess ignoriert. Beispiel-URL: `http://host:[port]/path`
{: tip}



## Wie funktioniert die Verschlüsselung in {{site.data.keyword.appid_short_notm}}?
{: #faq-encryption}
{: faq}

In der folgenden Tabelle finden Sie Antworten auf häufige Fragen zur Verschlüsselung.

<table>
  <thead>
    <th colspan=2><img src="images/idea.png" alt="Symbol für weitere Informationen"/>  </th>
  </thead>
  <tbody>
    <tr>
      <td>Wozu dient die Verschlüsselung?</td>
      <td>Eine Möglichkeit, die Benutzerinformationen zu schützen, ist das Verschlüsseln von ruhenden Kundendaten. Der Service verschlüsselt ruhende Kundendaten mit Pre-Tenant-Schlüsseln.</td>
    </tr>
    <tr>
      <td>Haben Sie einen eigenen Algorithmus erstellt? Welcher Algorithmus wird im Code verwendet?</td>
      <td>Wir haben keinen eigenen Algorithmus erstellt. Der Service verwendet <code>AES</code> und <code>SHA-256</code> mit Salting.</td>
    </tr>
    <tr>
      <td>Werden öffentliche oder Open-Source-Verschlüsselungsmodule oder -provider verwendet? Werden die Verschlüsselungsfunktionen offengelegt? </td>
      <td>Vom Service werden die Java-Bibliotheken <code>javax.crypto</code> verwendet. Die Verschlüsselungsfunktion wird jedoch niemals offengelegt.</td>
    </tr>
    <tr>
      <td>Wie werden Schlüssel gespeichert?</td>
      <td>Schlüssel werden generiert, mit einem Hauptschlüssel verschlüsselt, der für jede Region spezifisch ist, und dann lokal gespeichert. Die Hauptschlüssel werden in {{site.data.keyword.keymanagementserviceshort}} gespeichert. Auf der Speicher- und Middlewareebene erfolgt die Verschlüsselung auf der Serviceebene, d. h., es gibt einen Schlüssel für alle Kunden. Auf der Ebene der App hat jeder Kunde einen eigenen Schlüssel für die Verschlüsselung.</td>
    </tr>
    <tr>
      <td>Welche Schlüssellänge wird verwendet?</td>
      <td>Der Service verwendet 16 Byte.</td>
    </tr>
    <tr>
      <td>Werden ferne APIs aufgerufen, die Verschlüsselungsfunktionalität offenlegen?</td>
      <td>Nein.</td>
    </tr>
  </tbody>
</table>



## Was ist der Unterschied zwischen {{site.data.keyword.appid_short_notm}} und Keycloak?
{:# faq-keycloak}

Sowohl {{site.data.keyword.appid_short_notm}} als auch Keycloak können verwendet werden, um eine Authentifizierung für Anwendungen und sichere Services bereitzustellen. Der Hauptunterschied zwischen den beiden Angeboten ist die Art und Weise, in der sie gepackt sind.
{: shortdesc}

Keycloak ist als Software gepackt, was bedeutet, dass der Entwickler nach dem Herunterladen für die Verwaltung der Funktionen verantwortlich ist. Er ist verantwortlich für das Hosting, die Hochverfügbarkeit, die Compliance, Sicherungen, DDoS-Schutz, Lastausgleich, Web-Firewalls, Datenbanken, usw.

{{site.data.keyword.appid_short_notm}} ist ein vollständig verwaltetes Angebot, das 'As-a-Service' bereitgestellt wird. Dies bedeutet, dass IBM den Betrieb des Service übernimmt und die Konformität, die Verfügbarkeit in mehreren Zonen, die Servicelevel-Agreements (SLAs) und vieles mehr verwaltet. {{site.data.keyword.appid_short_notm}} bietet außerdem die Nutzung der {{site.data.keyword.cloud_notm}}-Plattform ohne Vorbereitungs- oder Anpassungsaufwand, die native Laufzeiten und Services umfasst, zum Beispiel {{site.data.keyword.containershort_notm}}, {{site.data.keyword.openwhisk_short}} und {{site.data.keyword.cloudaccesstrailshort}}.
