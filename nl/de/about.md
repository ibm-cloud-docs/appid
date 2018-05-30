---

copyright:
  years: 2017, 2018
lastupdated: "2018-04-27"

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
    <td> {{site.data.keyword.appid_short_notm}} ermöglicht das [Speichern von Benutzerdaten](/docs/services/appid/user-profile.html), wie z. B. App-Benutzervorgaben oder Informationen aus den öffentlichen Social Media-Profilen der Benutzer, und das Verwenden dieser Daten zur Anpassung der verschiedenen Schnittstellen Ihrer App. </td>
  </tr>
  <tr>
    <td> Sie möchten es Benutzern ermöglichen, mit ihrer E-Mail-Adresse und einem Kennwort auf Ihre App zuzugreifen. </td>
    <td> {{site.data.keyword.appid_short_notm}} ermöglicht Ihnen, ein [Cloudverzeichnis](/docs/services/appid/cloud-directory.html) zu erstellen, womit Sie Anmelde- und Registrierungsfunktionen für Benutzer zu mobilen Apps und Web-Apps hinzufügen können. Cloud Directory stellt das Framework zur Verwaltung einer Benutzerregistry bereit, die dem jeweiligen Benutzerstamm entsprechend skaliert werden kann. Mit der vordefinierten Self-Service-Funktionalität, z. B. für die E-Mail-Verifizierung und das Zurücksetzen von Kennwörtern, können Sie sich darauf verlassen, dass Ihre App eine sichere Benutzerauthentifizierung bietet. </td>
  </tr>
</table>


## Integrationen
{: #integrations}

Sie können {{site.data.keyword.appid_short_notm}} mit anderen {{site.data.keyword.Bluemix_notm}}-Angeboten nutzen.
{:shortdesc}


<dl>
  <dt>{{site.data.keyword.containerlong_notm}}</dt>
    <dd>Durch die Konfiguration von Ingress in einem Standardcluster können Sie Ihre Apps auf Clusterebene schützen. Entnehmen Sie die Ingress-Annotation der {{site.data.keyword.appid_short_notm}}-Authentifizierung, um zu beginnen. </dd>
  <dt>{{site.data.keyword.openwhisk}} und API Connect</dt>
    <dd>Wenn Sie Ihre APIs mit [{{site.data.keyword.openwhisk_short}}](/docs/openwhisk/index.html) und [API Connect](/docs/apis/management/manage_apis.html) erstellen, können Sie Ihre Anwendungen auf dem Gateway anstatt in Ihrem App-Code sichern. Um die Integration in Aktion zu erleben, sehen Sie sich <a href="https://www.youtube.com/watch?v=Fa9YD2NGZiE" target="_blank">Einfache und schnelle Social Media-OAUTH-Registrierung mit APIC und {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> an.</dd>
  <dt>Cloud Foundry</dt>
    <dd>Probieren Sie eine unserer Cloud Foundry-Beispielapps aus, um zu sehen, wie Sie die App-ID in Ihre Apps integrieren können. </dd>
  <dt>iOS Programming Guide</dt>
    <dd>Entwickeln Sie Apps für Apple? Lesen Sie im <a href="https://console.bluemix.net/docs/swift/index.html#overview" target="_blank">iOS Programming Guide <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>, um mehr über Ihre vorhandenen iOS-Apps mit {{site.data.keyword.Bluemix_notm}} zu erfahren, damit zu experimentieren und sie zu verbessern. </dd>
</dl>


## Architektur
{: #architecture}

Mit {{site.data.keyword.appid_short_notm}} können Sie eine zusätzliche Sicherheitsstufe in Ihren Apps implementieren, indem Sie es erforderlich machen, dass die Benutzer eine Registrierung durchführen. Darüber hinaus können Sie das Server-SDK verwenden, um Ihre Back-End-Ressourcen zu schützen.
{: shortdesc}

![{{site.data.keyword.appid_short_notm}}-Architekturdiagramm](/images/appid_architecture.png)

<dl>
  <dt> Anwendung </dt>
    <dd><strong>Server-SDK</strong>: Sie können die Back-End-Ressourcen, die in {{site.data.keyword.Bluemix_notm}} bereitgestellt werden, und die Web-Apps mit dem Server-SDK schützen. Das Server-SDK extrahiert das Zugriffstoken aus einer Anforderung und validiert es mit {{site.data.keyword.appid_short_notm}}. </br>
    <strong>Client-SDK</strong>: Sie können mobile Apps mit dem Android- oder iOS-Client-SDK schützen. Das Client-SDK kommuniziert mit den Cloud-Ressourcen, um den Authentifizierungsprozess zu starten, sobald es eine Berechtigungsanforderung (Challenge) feststellt.</dd>
  <dt>{{site.data.keyword.Bluemix_notm}}</dt>
    <dd><strong>{{site.data.keyword.appid_short_notm}}</strong>: Nach der erfolgreichen Authentifizierung gibt {{site.data.keyword.appid_short_notm}}  Zugriffs- und Identitätstoken an die App zurück.</br>
    <strong>Cloudverzeichnis</strong>: Benutzer können sich mit ihrer E-Mail-Adresse und einem Kennwort bei Ihrem Service registrieren. Sie können die Benutzer dann in einer Listenansicht über die Benutzerschnittstelle verwalten. Mit dem Cloudverzeichnis fungiert {{site.data.keyword.appid_short_notm}} wie Ihr Identitätsprovider. </dd>
  <dt>Extern (anderer Anbieter)</dt>
    <dd><strong>Social Media- und Unternehmensidentitätsprovider</strong>:{{site.data.keyword.appid_short_notm}} unterstützt zwei Social Media-Identitätsprovider: Facebook und Google+ sowie einen Unternehmensidentitätsprovider: SAML 2.0 Federation. Der Service veranlasst eine Weiterleitung an den Identitätsprovider und überprüft die zurückgegebenen Authentifizierungstokens. Wenn die Tokens gültig sind, gewährt der Service Zugriff auf Ihre App, ohne dass Zugriff auf die tatsächliche Kennphrase besteht. </dd>
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
