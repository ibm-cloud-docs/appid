---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Produktinformationen
{: #about}

Mit {{site.data.keyword.appid_full}} können Sie eine Authentifizierung zu Ihren Apps hinzufügen und die Back-End-Ressourcen schützen.
{:shortdesc}

## Gründe für die Verwendung des Service
{: #reasons}

Zahlreiche Gründe sprechen für die Verwendung von {{site.data.keyword.appid_short_notm}}. Prüfen Sie, ob eines oder mehrere der folgenden Szenarios auf Sie zutrifft.
{: shortdesc}

<table>
  <tr>
    <th> Szenario </th>
    <th> Grund </th>
  </tr>
  <tr>
    <td> Sie müssen eine Funktion für die [Berechtigung und Authentifizierung](/docs/services/appid/authorization.html) zu Ihren mobilen Apps und Web-Apps hinzufügen, verfügen jedoch nicht über Hintergrundkenntnisse im Bereich der Sicherheit. </td>
    <td> Mit {{site.data.keyword.appid_short_notm}} können Sie ohne großen Aufwand einen Authentifizierungsschritt in Ihre Apps integrieren. Sie können den Service nutzen, um mit [Identitätsprovidern](/docs/services/appid/identity-providers.html) zu kommunizieren und so den Zugriff auf Ihre Apps zu verwalten. </td>
  </tr>
  <tr>
    <td> Sie möchten den Zugriff auf Ihre Apps und Back-End-Ressourcen begrenzen. </td>
    <td> Der Service bietet die Möglichkeit, sowohl für authentifizierte Benutzer als auch für anonyme Benutzer [Ressourcen zu schützen](/docs/services/appid/protecting-resources.html). </td>
  </tr>
  <tr>
    <td> Sie möchten personalisierte App-Umgebungen für Ihre Benutzer erstellen. </td>
    <td> {{site.data.keyword.appid_short_notm}} ermöglicht das [Speichern von Benutzerdaten](/docs/services/appid/user-profile.html), wie z. B. App-Benutzervorgaben oder Informationen aus den öffentlichen Social Media-Profilen der Benutzer, und das Verwenden dieser Daten zur Anpassung der verschiedenen Schnittstellen Ihrer App.</td>
  </tr>
  <tr>
    <td> Sie möchten es Benutzern ermöglichen, mit ihrer E-Mail-Adresse und einem Kennwort auf Ihre App zuzugreifen.</td>
    <td> {{site.data.keyword.appid_short_notm}} bietet die Möglichkeit, ein [Cloudverzeichnis](/docs/services/appid/cloud-directory.html) zu erstellen. Damit können Sie Benutzeranmeldefunktionalität zu mobilen Apps und Web-Apps hinzufügen. Cloud Directory stellt das Framework zur Verwaltung einer Benutzerregistry bereit, die dem jeweiligen Benutzerstamm entsprechend skaliert werden kann. Mit der vordefinierten Self-Service-Funktionalität, z. B. für die E-Mail-Verifizierung und das Zurücksetzen von Kennwörtern, können Sie sich darauf verlassen, dass Ihre App eine sichere Benutzerauthentifizierung bietet.</td>
  </tr>
</table>


## Architektur
{: #architecture}

Mit {{site.data.keyword.appid_short_notm}} können Sie eine zusätzliche Sicherheitsstufe in Ihren Apps implementieren, indem Sie es erforderlich machen, dass die Benutzer eine Anmeldung durchführen. Darüber hinaus können Sie das Server-SDK verwenden, um Ihre Back-End-Ressourcen zu schützen.
{: shortdesc}

![{{site.data.keyword.appid_short_notm}}-Architekturdiagramm](/images/appid_architecture.png)

<dl>
  <dt> Anwendung </dt>
    <dd> Server-SDK: Sie können die Back-End-Ressourcen, die in {{site.data.keyword.Bluemix_notm}} bereitgestellt werden, und die Web-Apps mit dem Server-SDK schützen. Das Server-SDK extrahiert das Zugriffstoken aus einer Anforderung und validiert es mit {{site.data.keyword.appid_short_notm}}. </br>
    Client-SDK: Sie können mobile Apps mit dem Android- oder iOS-Client-SDK schützen. Das Client-SDK kommuniziert mit den Cloud-Ressourcen, um den Authentifizierungsprozess zu starten, sobald es eine Berechtigungsanforderung (Challenge) feststellt.</dd>
  <dt> {{site.data.keyword.Bluemix_notm}} </dt>
    <dd> App ID: Nach der erfolgreichen Authentifizierung gibt {{site.data.keyword.appid_short_notm}} Zugriffs- und Identitätstoken an die Anwendung zurück.</br>
    Cloud Directory: Benutzer können sich mit ihrer E-Mail-Adresse und einem Kennwort bei Ihrem Service anmelden. Sie können die Benutzer dann in einer Listenansicht über die Benutzerschnittstelle verwalten. </dd>
  <dt> Extern (anderer Anbieter) </dt>
    <dd>  {{site.data.keyword.appid_short_notm}} unterstützt zwei Social Media-Identitätsprovider: Facebook und Google+. Der Service veranlasst eine Weiterleitung an den Identitätsprovider und ermöglicht nach dem Verifizieren der Authentifizierung den Zugriff auf Ihre App. {{site.data.keyword.appid_short_notm}} verifiziert die Berechtigungsnachweise, ohne über Zugriff auf die tatsächliche Kennphrase zu Verfügen.</dd>
</dl>


## Anforderungsablauf
{: #request}

Das folgende Diagramm zeigt, wie eine Anforderung aus dem Client-SDK an Ihre Back-End-Ressourcen und an Identitätsprovider geleitet wird.
{: shortdesc}

![{{site.data.keyword.appid_short_notm}}-Anforderungsablauf](/images/appidrequestflow.png)


* Das {{site.data.keyword.appid_short_notm}}-Client-SDK sendet eine Anforderung an Ihre Back-End-Ressourcen, die mit dem {{site.data.keyword.appid_short_notm}}-Server-SDK geschützt werden.
* Das {{site.data.keyword.appid_short_notm}}-Server-SDK erkennt eine nicht autorisierte Anforderung und gibt einen HTTP 401- und Berechtigungsbereich zurück.
* Das Client-SDK erkennt HTTP 401 automatisch und startet den Authentifizierungsprozess.
* Wenn das Client-SDK Kontakt mit dem Service aufnimmt, gibt das Server-SDK das Anmelde-Widget zurück, falls mehr als ein Identitätsprovider konfiguriert ist. {{site.data.keyword.appid_short_notm}} ruft den Identitätsprovider auf und präsentiert das Anmeldeformular für diesen Provider oder gibt einen Bewilligungscode zurück, mit dem die Authentifizierung ohne konfigurierte Identitätsprovider möglich ist.
* {{site.data.keyword.appid_short_notm}} fordert die Client-App auf, sich durch die Bereitstellung einer Authentifizierungsanforderung (Challenge) zu authentifizieren.
* Ist ein Identitätsprovider konfiguriert, wenn sich der Benutzer anmeldet, wird die Authentifizierung durch den jeweiligen OAuth-Ablauf verarbeitet.
* Wenn die Authentifizierung mit demselben Bewilligungscode beendet wird, wird der Code an den Tokenendpunkt gesendet. Der Endpunkt gibt zwei Tokens zurück: ein Zugriffstoken und eine Identitätstoken. Von diesem Punkt an verfügen alle Anforderungen, die mit dem Client-SDK gesendet werden, über einen neu abgerufenen Berechtigungsheader.
* Das Client-SDK wiederholt automatisch das Senden der ursprünglichen Anforderung, die den Berechtigungsablauf ausgelöst hat.
* Das Server-SDK extrahiert den Berechtigungsheader aus der Anforderung, validiert den Header mit dem Service und erteilt den Zugriff auf eine Back-End-Ressource.

**Hinweis**: Die implementierten Protokolle sind mit OpenID Connect (OIDC) vollständig kompatibel.
