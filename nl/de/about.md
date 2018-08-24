---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Produktinformationen
{: #about}

Anwendungssicherheit kann unglaublich kompliziert sein. Für die meisten Entwickler stellt das Thema Sicherheit eine der größten Herausforderungen beim Erstellen einer App dar. Wie können Sie sicher sein, dass Sie die Daten Ihrer Benutzer erfolgreich schützen? Durch die Integration von {{site.data.keyword.appid_full}} in Ihren Apps können Sie selbst dann Ressourcen schützen und eine Authentifizierung hinzufügen, wenn Sie nicht viel Erfahrung mit Sicherheitsfunktionen haben.
{:shortdesc}


## Gründe für die Verwendung des Service
{: #reasons}

{{site.data.keyword.appid_short_notm}} erleichtert es Entwicklern, ohne großen Aufwand eine Authentifizierung zu Web-Apps und mobilen Apps mit nur wenigen Zeilen Code hinzuzufügen und ihre für die Cloud konzipierten Anwendungen und -Services mit {{site.data.keyword.Bluemix_notm}} zu schützen. Dadurch, dass Benutzer sich bei Ihrer App anmelden müssen, können Sie Benutzerdaten wie App-Benutzervorgaben oder Informationen aus öffentlichen Profilen von sozialen Medien speichern und diese Daten anschließend dazu nutzen, die einzelnen Benutzererfahrungen mit der App anzupassen. {{site.data.keyword.appid_short_notm}} beinhaltet ein Anmeldeframework. Sie können aber auch Ihre eigenen, an Ihr Brand-Marketing angepassten Anmeldeanzeigen verwenden, wenn Sie mit dem Cloudverzeichnis arbeiten.
{: shortdesc}

Zahlreiche Gründe sprechen für die Verwendung von {{site.data.keyword.appid_short_notm}}. Prüfen Sie, ob eines oder mehrere der folgenden Szenarios auf Sie zutrifft.

<table>
  <tr>
    <th>Szenario</th>
    <th>Lösung</th>
  </tr>
  <tr>
    <td>Sie müssen eine Funktion für die [Berechtigung und Authentifizierung](/docs/services/appid/authorization.html) zu Ihren mobilen Apps und Web-Apps hinzufügen, verfügen jedoch nicht über Hintergrundkenntnisse im Bereich der Sicherheit.</td>
    <td>Mit {{site.data.keyword.appid_short_notm}} können Sie ohne großen Aufwand einen Authentifizierungsschritt in Ihren Apps hinzufügen. Sie können eine Anmeldung über eine E-Mail-Adresse oder einen Benutzernamen, eine Anmeldung über soziale Medien oder eine Unternehmensanmeldung mithilfe von APIs, SDKs, vorgefertigten Benutzerschnittstellen oder Ihren eigenen an Ihr Brand-Marketing angepassten Benutzerschnittstellen hinzufügen. </td>
  </tr>
  <tr>
    <td>Sie möchten den Zugriff auf Ihre Apps und Back-End-Ressourcen begrenzen.</td>
    <td>Sie können Ihre Apps, Back-End-Ressourcen und APIs ohne großen Aufwand mit der auf Standards basierenden Authentifizierung schützen, die von {{site.data.keyword.appid_short_notm}} bereitgestellt wird. </td>
  </tr>
  <tr>
    <td>Sie möchten personalisierte App-Umgebungen für Ihre Benutzer erstellen.</td>
    <td>Mit {{site.data.keyword.appid_short_notm}} können Sie [Benutzerdaten speichern](/docs/services/appid/user-profile.html), wie z. B. App-Benutzervorgaben oder Informationen aus den öffentlichen Social Media-Profilen der Benutzer, und diese Daten anschließend zur Anpassung der verschiedenen Benutzererfahrungen in Ihrer App verwenden. </td>
  </tr>
  <tr>
    <td>Sie möchten Benutzer in einem skalierbaren Rahmen verwalten. </td>
    <td> {{site.data.keyword.appid_short_notm}} ermöglicht es Ihnen, über [Cloud Directory](/docs/services/appid/cloud-directory.html) ein Cloudverzeichnis zu erstellen und auf diese Weise Anmelde- und Registrierungsfunktionen für Benutzer zu Ihren Apps hinzuzufügen. Cloud Directory stellt das Framework zur Verwaltung einer Benutzerregistry bereit, die dem jeweiligen Benutzerstamm entsprechend skaliert werden kann. Mit der vordefinierten Self-Service-Funktionalität, z. B. für die E-Mail-Verifizierung und das Zurücksetzen von Kennwörtern, können Sie sich darauf verlassen, dass Ihre App eine sichere Benutzerauthentifizierung bietet.</td>
  </tr>
</table>


## Integrationen
{: #integrations}

Sie können {{site.data.keyword.appid_short_notm}} mit anderen {{site.data.keyword.Bluemix_notm}}-Angeboten nutzen.
{:shortdesc}


<dl>
  <dt>{{site.data.keyword.containerlong_notm}}</dt>
    <dd>Durch die Konfiguration von Ingress in einem Standardcluster können Sie Ihre Apps auf Clusterebene schützen. Einen Einstieg in dieses Thema vermitteln der Abschnitt zur <a href="/docs/containers/cs_annotations.html#appid-auth">Ingress-Annotation für {{site.data.keyword.appid_short_notm}}-Authentifizierung</a> sowie der Blogbeitrag zur <a href="https://www.ibm.com/blogs/bluemix/2018/05/announcing-app-id-integration-ibm-cloud-kubernetes-service/">Ankündigung der Integration von App ID in den IBM Cloud Kubernetes-Service <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>. </dd>
  <dt>{{site.data.keyword.openwhisk}} und API Connect</dt>
    <dd>Wenn Sie Ihre APIs mit [{{site.data.keyword.openwhisk_short}}](/docs/openwhisk/index.html) und [API Connect](/docs/apis/management/manage_apis.html) erstellen, können Sie Ihre Anwendungen auf dem Gateway anstatt in Ihrem App-Code sichern. Um die Integration in Aktion zu erleben, sehen Sie sich <a href="https://www.youtube.com/watch?v=Fa9YD2NGZiE" target="_blank">Einfache und schnelle Social Media-OAUTH-Registrierung mit APIC und {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> an.</dd>
  <dt>Cloud Foundry</dt>
    <dd>Probieren Sie eine der bereitgestellten Cloud Foundry-Beispielapps aus, um zu sehen, wie Sie {{site.data.keyword.appid_short_notm}} in Ihre Apps integrieren können. </dd>
  <dt>Leitfaden für die Programmierung mit iOS</dt>
    <dd>Entwickeln Sie Apps für Apple? Ziehen Sie den <a href="https://console.bluemix.net/docs/swift/index.html#overview" target="_blank">Leitfaden zur Programmierung mit iOS<img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> zurate, um mehr über das Zusammenspiel Ihrer vorhandenen iOS-Apps mit {{site.data.keyword.Bluemix_notm}} zu erfahren, Neues auszuprobieren und diese Apps zu erweitern. </dd>
  <dt>{{site.data.keyword.cloudaccesstrailshort}}</dt>
    <dd>Sie können Verwaltungsaktivitäten in {{site.data.keyword.appid_short_notm}} wie Änderungen an der Dashboard-Konfiguration mit dem [Service '{{site.data.keyword.cloudaccesstrailshort}}'](/docs/services/cloud-activity-tracker/index.html) überwachen. </dd>
  <dt>Leitfaden für Programmierung mit Node.js</dt>
    <dd>Entwickeln Sie Apps für Node.js? Ziehen Sie den <a href="https://console.bluemix.net/docs/node/index.html#getting-started-tutorial" target="_blank">Leitfaden zur Programmierung mit Node.js<img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> zurate, um mehr über das Zusammenspiel Ihrer vorhandenen Node.js-Apps mit {{site.data.keyword.Bluemix_notm}} zu erfahren, Neues auszuprobieren und diese Apps zu erweitern. </dd>
</dl>


## Architektur
{: #architecture}

Mit {{site.data.keyword.appid_short_notm}} können Sie eine zusätzliche Sicherheitsstufe in Ihren Apps implementieren, indem Sie es erforderlich machen, dass die Benutzer eine Anmeldung durchführen. Darüber hinaus können Sie auch das Server-SDK oder APIs verwenden, um Ihre Back-End-Ressourcen zu schützen.
{: shortdesc}

![{{site.data.keyword.appid_short_notm}}-Architekturdiagramm](/images/appid_architecture1.png)

<dl>
  <dt>Anwendung</dt>
    <dd><strong>Server-SDK</strong>: Sie können die Back-End-Ressourcen, die in {{site.data.keyword.Bluemix_notm}} bereitgestellt werden, und die Web-Apps mit dem Server-SDK schützen. Das Server-SDK extrahiert das Zugriffstoken aus einer Anforderung und validiert es mit {{site.data.keyword.appid_short_notm}}. </br>
    <strong>Client-SDK</strong>: Sie können mobile Apps mit dem Android- oder iOS-Client-SDK schützen. Das Client-SDK kommuniziert mit den Cloud-Ressourcen, um den Authentifizierungsprozess zu starten, sobald es eine Berechtigungsanforderung (Challenge) feststellt.</dd>
  <dt>{{site.data.keyword.Bluemix_notm}}</dt>
    <dd><strong>{{site.data.keyword.appid_short_notm}}</strong>: Nach der erfolgreichen Authentifizierung gibt {{site.data.keyword.appid_short_notm}} Zugriffs- und Identitätstoken an die App zurück.</br>
    <strong>Cloudverzeichnis</strong>: Benutzer können sich mit ihrer E-Mail-Adresse und einem Kennwort bei Ihrem Service registrieren. Sie können die Benutzer dann in einer Listenansicht über die Benutzerschnittstelle verwalten. Mit dem Cloudverzeichnis fungiert {{site.data.keyword.appid_short_notm}} wie Ihr Identitätsprovider.</dd>
  <dt>Extern (anderer Anbieter)</dt>
    <dd><strong>Social Media- und Unternehmensidentitätsprovider</strong>: {{site.data.keyword.appid_short_notm}} unterstützt Facebook, Google+ und SAML 2.0 Federation als Identitätsprovideroptionen. Der Service veranlasst eine Weiterleitung an den Identitätsprovider und überprüft die zurückgegebenen Authentifizierungstoken. Wenn die Token gültig sind, gewährt der Service Zugriff auf Ihre App, ohne dass Zugriff auf die tatsächliche Kennphrase besteht.</dd>
</dl>


## Anforderungsablauf
{: #request}

Auch wenn Ihr Anforderungsablauf je nach Anwendungskonfiguration variiert, gibt es drei Hauptabläufe, die Ihnen bei Ihrer Arbeit mit App ID begegnen können. Sie können einen Ablauf für mobile Apps oder einen Ablauf für Web-Apps erstellen oder Ihre Ressourcen mit einem anderen Verarbeitungsablauf schützen. Probieren Sie einige der Beispielabläufe aus, um herauszufinden, ob sie sich als Ausgangspunkt für die Konfiguration Ihrer App eignen.
{: shortdesc}

### Anforderungsablauf für Web-Apps
{: #web-flow}

![{{site.data.keyword.appid_short_notm}}-Anforderungsablauf](/images/web_flow1.png)

1. Über einen Browser führt ein Benutzer eine Aktion aus, die eine Anforderung an das App ID-SDK auslöst. 
2. Verfügt der Benutzer nicht über die erforderliche Berechtigung, wird eine Weiterleitung an App ID gestartet. 
3. App ID ruft das Anmeldewidget auf und sendet es an den Browser. 
4. Der Benutzer wählt einen Identitätsprovider für die Authentifizierung aus und führt den Anmeldeprozess durch. 
5. Der Identitätsprovider leitet mit einem Identitätstoken zurück zum App ID-SDK. 
6. Das App ID-SDK ruft Zugriffstoken vom App ID-Service ab. 
7. Die Token werden vom App ID-SDK gespeichert und es erfolgt eine Weiterleitung. 
8. Dem Benutzer wird der Zugriff auf die Anwendung erteilt. 

### Anforderungsablauf für mobile Apps. 
{: #mobile-flow}

![{{site.data.keyword.appid_short_notm}}-Anforderungsablauf](/images/mobile_flow.png)

1. Ein Benutzer führt eine Aktion aus, die über die Clientanwendung eine Anforderung an das App ID-SDK auslöst. 
2. Verfügt der Benutzer nicht über gültige Zugriffstoken, wird der Berechtigungsprozess vom App ID-SDK gestartet. 
3. Dem Benutzer wird das Anmeldewidget angezeigt. 
4. Der Benutzer führt die Authentifizierung über einen der konfigurierten Identitätsprovider durch. 
5. Sobald der Benutzer über ein Identitätstoken verfügt, ruft das SDK ein Zugriffstoken vom App ID-Service ab. 
6. Mit den beiden Token führt das SDK die Anforderung erneut durch. 
7. Sind die Token gültig, wird dem Benutzer der Zugriff auf die Anwendung erteilt. 

### Anforderungsablauf für geschützte Ressourcen
{: #pr-flow}

![{{site.data.keyword.appid_short_notm}}-Anforderungsablauf](/images/pr_flow.png)

1. Eine Clientanwendung muss über eine Gruppe öffentlicher Schlüssel verfügen, damit eine Anforderung an die Ressource erfolgen kann. 
2. Mit den öffentlichen Schlüsseln wird eine Anforderung von einer Clientanwendung ausgegeben. 
3. Ist kein gültiges Zugriffstoken vorhanden, wird ein Fehler an die Anwendung gemeldet. 
4. Nach dem Abruf eines gültigen Tokens kann erneut eine Anforderung von der Clientanwendung ausgegeben werden, diesmal jedoch unter Einbeziehung des Tokens. 
5. Können die Berechtigungen, die über das Zugriffstoken eingeräumt werden, von der Anwendung als gültig bestätigt werden, erteilt die Anwendung den Zugriff auf die geschützte Ressource. 
