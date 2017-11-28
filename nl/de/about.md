---

copyright:
  years: 2017
lastupdated: "2017-11-09"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


# Produktinformationen
{: #about}

Mit {{site.data.keyword.appid_full}} können Sie den Zugriff auf Ihre Anwendungen benutzerfreundlich verwalten.
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
    <td> Sie möchten Ihre mobilen Anwendungen und Webanwendungen sicherer machen. </td>
    <td> Mit {{site.data.keyword.appid_short_notm}} können Sie ohne großen Aufwand einen Authentifizierungsschritt in Ihre Anwendungen integrieren. Sie können den Service nutzen, um mit Identitätsprovidern zu kommunizieren und so den Zugriff auf Ihre Anwendungen zu verwalten.</td>
  </tr>
  <tr>
    <td> Sie möchten den Zugriff auf Ihre Apps und Back-End-Ressourcen begrenzen. </td>
    <td> Der Service bietet die Möglichkeit, Ressourcen sowohl für authentifizierte Benutzer als auch für anonyme Benutzer zu schützen.</td>
  </tr>
  <tr>
    <td> Sie möchten personalisierte App-Umgebungen für Ihre Benutzer erstellen. </td>
    <td> {{site.data.keyword.appid_short_notm}} ermöglicht das Speichern von Benutzerdaten, wie z. B. App-Benutzervorgaben oder Informationen aus den öffentlichen Social Media-Profilen der Benutzer. Mithilfe dieser Daten können Sie dafür sorgen, dass den Benutzern individuell angepasste Umgebungen zur Verfügung stehen.</td>
  </tr>
</table>

**Hinweis**: Die implementierten Protokolle sind mit OpenID Connect (OIDC) vollständig kompatibel.


## Architektur
{: #architecture}

Mit {{site.data.keyword.appid_short_notm}} können Sie eine zusätzliche Sicherheitsstufe in Ihren Anwendungen implementieren, indem Sie es erforderlich machen, dass die Benutzer eine Anmeldung durchführen. Darüber hinaus können Sie das Server-SDK verwenden, um Ihre Back-End-Ressourcen zu schützen.

Im folgenden Diagramm ist eine Übersicht der Funktionsweise des {{site.data.keyword.appid_short_notm}}-Service dargestellt.


![{{site.data.keyword.appid_short_notm}}-Architekturdiagramm](/images/appid_architecture2.png)

Abbildung 1: {{site.data.keyword.appid_short_notm}} - Architekturdiagramm



<dl>
  <dt> Anwendung </dt>
    <dd> Das Client-SDK stellt eine Anfrageklasse für die Kommunikation mit den Cloudressourcen bereit. Das Client-SDK startet den Authentifizierungsprozess automatisch, wenn es eine Berechtigungsanforderung (Challenge) feststellt. </dd>
  <dt> {{site.data.keyword.Bluemix_notm}} </dt>
    <dd>  Das Server-SDK extrahiert das Zugriffstoken aus der Anforderung und validiert es mit {{site.data.keyword.appid_short_notm}}. Nach der erfolgreichen Authentifizierung gibt {{site.data.keyword.appid_short_notm}} Zugriffs- und Identitätstoken an die Anwendung zurück. </dd>
  <dt> Identitätsprovider </dt>
    <dd> Der Service veranlasst eine Weiterleitung an den Identitätsprovider und verifiziert die Authentifizierung für den Zugriff auf Ihre Anwendung. {{site.data.keyword.appid_short_notm}} verifiziert die Berechtigungsnachweise, ohne über Zugriff auf die tatsächliche Kennphrase zu Verfügen.</dd>
</dl>


## Anforderungsablauf
{: #request}

Das folgende Diagramm zeigt, wie eine Anforderung aus dem Client-SDK an Ihre Back-End-Anwendung und an Identitätsprovider geleitet wird.

![{{site.data.keyword.appid_short_notm}}-Anforderungsablauf](/images/appidrequestflow.png)

Abbildung 2. Anforderungsablauf von {{site.data.keyword.appid_short_notm}}


* Das {{site.data.keyword.appid_short_notm}}-Client-SDK sendet eine Anforderung an Ihre Back-End-Ressourcen, die mit dem {{site.data.keyword.appid_short_notm}}-Server-SDK geschützt werden.
* Das {{site.data.keyword.appid_short_notm}}-Server-SDK erkennt eine nicht autorisierte Anforderung und gibt einen HTTP 401- und Berechtigungsbereich zurück.
* Das Client-SDK erkennt HTTP 401 automatisch und startet den Authentifizierungsprozess.
* Wenn das Client-SDK Kontakt mit dem Service aufnimmt, gibt das Server-SDK das Anmelde-Widget zurück, falls mehr als ein Identitätsprovider konfiguriert ist. {{site.data.keyword.appid_short_notm}} ruft den Identitätsprovider auf und präsentiert das Anmeldeformular für diesen Provider oder gibt einen Bewilligungscode zurück, mit dem die Authentifizierung ohne konfigurierte Identitätsprovider möglich ist.
* {{site.data.keyword.appid_short_notm}} fordert die Client-App auf, sich durch die Bereitstellung einer Authentifizierungsanforderung (Challenge) zu authentifizieren.
* Ist ein Identitätsprovider konfiguriert, wenn sich der Benutzer anmeldet, wird die Authentifizierung durch den jeweiligen OAuth-Ablauf verarbeitet.
* Wenn die Authentifizierung mit demselben Bewilligungscode beendet wird, wird der Code an den Tokenendpunkt gesendet. Der Endpunkt gibt zwei Tokens zurück: ein Zugriffstoken und eine Identitätstoken. Von diesem Punkt an verfügen alle Anforderungen, die mit dem Client-SDK gesendet werden, über einen neu abgerufenen Berechtigungsheader.
* Das Client-SDK wiederholt automatisch das Senden der ursprünglichen Anforderung, die den Berechtigungsablauf ausgelöst hat.
* Das Server-SDK extrahiert den Berechtigungsheader aus der Anforderung, validiert den Header mit dem Service und erteilt den Zugriff auf eine Back-End-Ressource.


## Komponenten
{: #components}

Der Service besteht aus den folgenden Komponenten.

<dl>
  <dt> Dashboard </dt>
    <dd> Im Service-Dashboard können Sie Onboarding-Beispiele herunterladen, Aktivitätenprotokolle anzeigen sowie die Authentifizierung und die Identitätsprovider konfigurieren.</dd>
  <dt> Client-SDK </dt>
    <dd> Sie können das Client-SDK für Ihre mobilen Apps und Web-Apps verwenden, um die Benutzerauthentifizierung zu implementieren.</br></br>
    Voraussetzungen für Android:
    <ul><ul><li> API 25 oder höher </li>
    <li> Java 8.x </li>
    <li> Android SDK-Tools 25.2.5 oder höher </li>
    <li> Android SDK-Plattformtools 25.0.3 oder höher </li>
    <li> Android Build-Tools Version 25.0.2 oder höher </li></ul></ul></br>
    Voraussetzungen für iOS:
    </br>
    <ul><ul><li> iOS9 oder höher </li>
    <li> MacOS 10.11.5 </li>
    <li>Xcode 8.2 </li></ul></ul></dd>
  <dt> Server-SDK </dt>
    <dd> Sie können die Back-End-Ressourcen schützen, die in {{site.data.keyword.Bluemix_notm}} bereitgestellt werden. </br>
    Unterstützte Laufzeiten:
    <ul><ul><li> Node.js </li>
    <li> Liberty for Java </li>
    <li> Swift </li></ul></ul></dd>
</dl>
