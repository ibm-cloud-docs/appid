---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

keywords: authentication, authorization, identity, app security, secure, development, identity provider, tokens, customization, lifetime

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


# Authentifizierungen verwalten
{: #managing-idp}

Identitätsprovider bieten durch die Authentifizierung eine zusätzliche Sicherheitsebene für Ihre mobilen Apps und Web-Apps. Mit {{site.data.keyword.appid_full}} können Sie einen oder mehrere Identitätsprovider konfigurieren und so ein angepasstes Anmeldeverfahren für Ihre Benutzer einrichten.
{: shortdesc}


{{site.data.keyword.appid_short_notm}} interagiert mit Identitätsprovidern unter Verwendung verschiedener Protokolle wie z. B. OpenID Connect, SAML usw. Beispielsweise ist OpenID Connect das Protokoll, das für viele Social-Media-Provider wie Facebook, Google usw. verwendet wird. Unternehmensprovider wie beispielsweise <a href="https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-azure-active-directory/" target="_blank">Azure Active Directory <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> oder <a href="https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-active-directory-federation-service/" target="_blank">Active Directory Federation Service <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> verwenden in der Regel SAML als Identitätsprotokoll. Für [Cloud Directory](/docs/services/appid?topic=appid-cloud-directory) verwendet der Service SCIM, um Identitätsinformationen zu verifizieren.

Weitere Informationen zur Anwendungsidentität finden Sie unter [Anwendungsidentität](/docs/services/appid?topic=appid-app).
{: tip}

Es gibt mehrere Provider, für deren Verwendung der Service konfiguriert werden kann. In der folgenden Tabelle sind die verfügbaren Optionen aufgeführt.

<table>
  <tr>
    <th>Provider</th>
    <th>Typ</th>
    <th>Beschreibung</th>
  </tr>
  <tr>
    <td>[Cloud Directory](/docs/services/appid?topic=appid-cloud-directory)</td>
    <td>Verwaltete Registry</td>
    <td>Sie können Ihre eigene Benutzerregistry in der Cloud verwalten. Wenn sich ein Benutzer für Ihre App anmeldet, wird er zu Ihrem Benutzerverzeichnis hinzugefügt. Diese Option gibt Ihren Benutzern mehr Freiheit, ihr eigenes Konto in Ihrer App zu verwalten.</td>
  </tr>
  <tr>
    <td>[SAML](/docs/services/appid?topic=appid-enterprise#enterprise)</td>
    <td>Unternehmensprovider</td>
    <td>Sie können eine Single-Sign-on-Funktionalität für Ihre Endbenutzer einrichten.</td>
  </tr>
  <tr>
    <td>[Facebook](/docs/services/appid?topic=appid-social#facebook)</td>
    <td>Social Media</td>
    <td>Die Endbenutzer können sich unter Verwendung ihrer Facebook-Berechtigungsnachweise bei Ihrer App anmelden.</td>
  </tr>
  <tr>
    <td>[Google+](/docs/services/appid?topic=appid-social#google)</td>
    <td>Social Media</td>
    <td>Die Endbenutzer können sich unter Verwendung ihrer Google-Berechtigungsnachweise bei Ihrer App anmelden.</td>
  </tr>
  <tr>
    <td>[Angepasst](/docs/services/appid?topic=appid-custom-identity#custom-identity)</td>
    <td> </td>
    <td>Wenn keine der bereitgestellten Optionen Ihren spezifischen Anforderungen entspricht, können Sie Ihren eigenen Identitätsablauf für die Arbeit mit {{site.data.keyword.appid_short_notm}} konfigurieren.</td>  
  </tr>
</table>

## Provider verwalten
{: #managing-providers}

Ein Identitätsprovider erstellt und verwaltet Informationen zu einer Entität, wie z. B. einem Benutzer, einer funktionalen ID oder einer Anwendung. Der Provider verifiziert die Identität der Entität anhand von Berechtigungsnachweisen, wie z. B. einem Kennwort. Anschließend sendet der Identitätsprovider die Identitätsinformationen an einen anderen Service-Provider. Da der Identitätsprovider die Entität authentifiziert, ist {{site.data.keyword.appid_short_notm}} in der Lage, sie zu autorisieren und Zugriff auf Ihre Apps zu erteilen.
{: shortdesc}

Gehen Sie wie folgt vor, um Ihre Identitätsprovider zu verwalten:

1. Navigieren Sie zu Ihrem Service-Dashboard.
2. Wählen Sie im Abschnitt **Identitätsprovider** in der Navigation die Seite **Verwalten** aus.
3. Setzen Sie auf der Registerkarte **Identitätsprovider** die Provider, die Sie verwenden möchten, auf **Ein**.
4. Optional: Entscheiden Sie, ob **Anonyme Benutzer** inaktiviert werden soll, oder übernehmen Sie den Standardwert **Ein**. Wenn diese Option auf **Ein** gesetzt ist, werden dem Benutzer Benutzerattribute von dem Zeitpunkt an zugeordnet, zu dem er mit der Interaktion mit Ihrer App beginnt. Weitere Informationen dazu, wie Sie ein identifizierter Benutzer werden, finden Sie unter [Progressive Authentifizierung](/docs/services/appid?topic=appid-anonymous#progressive).

{{site.data.keyword.appid_short_notm}} stellt Standardberechtigungsnachweise zur Verfügung, um Sie bei der Ersteinrichtung von Facebook und Google+ zu unterstützen. Der Grenzwert beträgt 100 Verwendungen der Berechtigungsnachweise pro Instanz und Tag. Da es sich um IBM Berechtigungsnachweise handelt, sollten sie nur zu Entwicklungszwecken verwendet werden. Bevor Sie die App veröffentlichen, aktualisieren Sie die Konfiguration so, dass Ihre eigenen Berechtigungsnachweise verwendet werden.
{: tip}


## Weiterleitungs-URIs hinzufügen
{: #add-redirect-uri}

Ein Weiterleitungs-URI ist der Callback-Endpunkt Ihrer App. Während des Anmeldeablaufs validiert {{site.data.keyword.appid_short_notm}} die URIs, bevor Clients am Autorisierungsworkflow teilnehmen können. Dies trägt dazu bei, Phishing-Attacken und Codelecks zu vermeiden. Durch die Registrierung Ihres URI wird {{site.data.keyword.appid_short_notm}} darüber informiert, dass der URI vertrauenswürdig ist und dass Ihre Benutzer ohne Risiko zu diesem URI weitergeleitet werden können.

Beachten Sie hierbei unbedingt, dass nur URIs von Anwendungen registriert werden sollten, die Sie als vertrauenswürdig einstufen.
{: note}


1. Klicken Sie auf **Authentifizierungseinstellungen**, um Ihre Konfigurationsoptionen für URIs und Tokens anzuzeigen.

2. Geben Sie im Feld **Webweiterleitungs-URI hinzufügen** den gewünschten URI ein. Jeder URI muss mit `http://` oder mit `https://` beginnen und muss den vollständigen Pfad einschließlich aller Abfrageparameter umfassen, damit die Weiterleitung erfolgreich ausgeführt werden kann. Benötigen Sie Hilfe bei der Formatierung? In der folgenden Tabelle sind verschiedene Beispiele aufgeführt.

  <table>
    <tr>
      <th>Typ</th>
      <th>Beispiel-URI</th>
    </tr>
    <tr>
      <td>Angepasste Domäne</td>
      <td><code>http://mydomain.net/myapp2path/appid_callback</code></td>
    </tr>
    <tr>
      <td>Ingress-Unterdomäne</td>
      <td><code>https://mycluster.us-south.containers.appdomain.cloud/myapp1path/appid_callback</code></td>
    </tr>
    <tr>
      <td>Abmeldung</td>
      <td><code>http://mydomain.net/myapp2path/appid_logout</code></td>
    </tr>  
  </table>

3. Klicken Sie auf das Plussymbol (**+**) im Feld **Webweiterleitungs-URI hinzufügen**.

4. Wiederholen Sie die Schritte 1 bis 3, bis alle möglichen URIs zu Ihrer Liste hinzugefügt wurden.



## Lebensdauer des Tokens konfigurieren
{: #idp-token-lifetime}

Die Tokenlebensdauer beginnt bei jeder Benutzeranmeldung neu. Beispiel: Sie legen die Lebensdauer des Aktualisierungstokens auf 10 Tage fest. Ein Zugriffstoken und ein Aktualisierungstoken werden erstellt, wenn sich der Benutzer zum ersten Mal anmeldet. Wenn der Benutzer nach ein paar Tagen wieder Ihre App aufruft, z. B. nach drei Tagen, dann muss er sich nicht erneut anmelden. Wenn der Benutzer aber erst zwölf Tage nach seiner ersten Anmeldung wieder Ihre App aufruft, muss er sich neu anmelden und dem Benutzer werden Tokens zugeordnet. Weitere Informationen zu Tokens finden Sie in [Informationen zu Tokens](/docs/services/appid?topic=appid-tokens#tokens).

1. Um eine Anmeldung ohne Benutzerinteraktion zu ermöglichen, setzen Sie **Aktualisierungstoken** auf **Ein**.

2. Legen Sie die Lebensdauer des Aktualisierungstokens fest. Die Ablaufzeit wird in Tagen festgelegt und kann ein beliebiger Wert im Bereich von 1 bis 90 sein. Je kleiner die Zahl ist, um so häufiger muss sich ein Benutzer anmelden.

3. Legen Sie die Lebensdauer Ihres Zugriffstokens fest. Die Ablaufzeit wird in Minuten festgelegt und kann im Bereich von 5 bis 1440 liegen. Je kleiner der Wert ist, umso höher ist der Schutz, den Sie im Fall eines Tokendiebstahls haben.

4. Legen Sie die Lebensdauer des anonymen Tokens fest. Ein [anonymes Token](/docs/services/appid?topic=appid-anonymous#progressive) wird den Benutzern zugewiesen, sobald sie beginnen, mit Ihrer App zu interagieren. Wenn sich ein Benutzer anmeldet, werden die Informationen in dem anonymen Token an das Token übertragen, das dem Benutzer zugeordnet ist. Die Ablaufzeit wird in Tagen festgelegt und kann ein beliebiger Wert zwischen 1 und 90 sein.


Wenn Sie eine Ablaufzeit für die Gültigkeit des Tokens festlegen, gilt diese Ablaufzeit für alle Provider (einschließlich Social-Media-Provider und Unternehmensprovider), die Sie konfiguriert haben.
{: tip}
