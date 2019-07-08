---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-20"

keywords: authentication, authorization, identity, app security, secure, custom, service provider, identity provider, enterprise, assertions

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

# SAML
{: #enterprise}

Wenn Sie über einen SAML-basierten Identitätsprovider verfügen, können Sie {{site.data.keyword.appid_short_notm}} als Service-Provider konfigurieren, von dem die einmalige Anmeldung (Single Sign-on, SSO) für einen Drittanbieter initiiert wird. Während des Anmeldungsablaufs können die Benutzer ohne großen Aufwand authentifiziert werden und {{site.data.keyword.appid_short_notm}}-Sicherheitstoken abrufen, mit denen Sie auf ihre Apps und geschützten APIs zugreifen können.
{: shortdesc}

 
Mit einem bestimmten SAML-Identitätsprovider arbeiten? Lesen Sie einen der folgenden Blogbeiträge zum Einrichten von {{site.data.keyword.appid_short_notm}} mit [Ping One ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/cloud/blog/setting-ibm-cloud-app-id-ping-one), [Azure Active Directory ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/cloud/blog/setting-ibm-cloud-app-id-azure-active-directory) oder [Active Directory Federation Service ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/cloud/blog/setting-ibm-cloud-app-id-active-directory-federation-service).
{: tip}


## Erläuterungen zu SAML
{: #saml-understanding}

Security Assertion Markup Language (SAML) ist ein offener Standard für den Austausch von Authentifizierungs- und Autorisierungsdaten zwischen einem Identitätsprovider, der die Benutzeridentität bestätigt, und einem Service-Provider, der die Benutzeridentitätsinformationen verarbeitet.
{: shortdesc}

Das <a href="http://saml.xml.org/saml-specifications" target="blank">SAML-Protokoll <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> unterstützt unterschiedliche Profile und Bindeoptionen. {{site.data.keyword.appid_short_notm}} unterstützt das SSO-Profil des Web-Browsers mit HTTP-POST-Bindung.

### Was ist die technische Basis eines Ablaufs?
{: #saml-tech-basis}

SAML 2.0 ist eines der etabliertesten Frameworks für Authentifizierungs- und Autorisierungsstandards. Es handelt sich hierbei um ein XML-basiertes Protokoll zwischen einem Service-Provider ({{site.data.keyword.appid_short_notm}}) und einem Identitätsprovider. Wenn ein Identitätsprovider einen Benutzer authentifiziert, erstellt er SAML-Tokens, die Zusicherungen oder Anweisungen zum Benutzer enthalten. Die Anweisungen können Folgendes enthalten:

- Authentifizierungsinformationen wie die Authentifizierungsmethode des Benutzers - ein Kennwort, eine Mehrfaktorenautentifizierung (MFA), etc. 
- Dem Benutzer zugeordnete Attribute - zu welcher Gruppe er gehört. 
- Berechtigungsentscheidungen, aus denen hervorgeht, ob der Benutzer eine bestimmte Aktion für eine bestimmte Ressource ausführen darf. 

Wenn die Zusicherungen an {{site.data.keyword.appid_short_notm}} zurückgegeben werden, wird die Benutzeridentität vom Service eingebunden und die entsprechenden Tokens werden generiert. Wenn die SAML-Zusicherung einem der folgenden OIDC-Claims entspricht, dann wird sie automatisch zum Identitätstoken hinzufügt.  Dabei ist zu beachten, dass nach einer Änderung von Werten auf der Providerseite die neuen Werte erst nach einer erneuten Anmeldung des Benutzers verfügbar sind.

 * `Name`
 * `E-Mail`
 * `Ländereinstellung`
 * `Bild`

Die Zusicherungen, die keinem der Standardnamen zugeordnet werden können, werden standardmäßig ignoriert. Wenn Ihr SAML-Provider weitere Zusicherungen zurückgibt, dann können diese Informationen ggf. abgerufen werden, wenn sich der Benutzer anmeldet. Durch die Erstellung eines Arrays mit den Zusicherungen, die Sie verwenden möchten, können Sie die [Informationen in Ihre Tokens einfügen](/docs/services/appid?topic=appid-customizing-tokens#customizing-tokens). Dabei ist allerdings darauf zu achten, dass keine unnötigen Informationen zu Ihren Tokens hinzugefügt werden. Tokens werden normalerweise in HTTP-Headern gesendet, die von begrenzter Größe sind.
{: tip}

### Wie sieht der Ablauf aus?
{: #saml-flow}

Auch wenn von {{site.data.keyword.appid_short_notm}} und vom Identitätsprovider das SAML-Framework zum Authentifizieren des Benutzers verwendet wird, wird von {{site.data.keyword.appid_short_notm}} das modernere OAuth 2.0-/OIDC-Framework zum Austauschen der Sicherheitstoken mit der Anwendung verwendet. Überprüfen Sie die folgende Abbildung, um sich mit dem detaillierten Informationsfluss vertraut zu machen. 

![Authentifizierungsablauf für SAML Enterprise](/images/ibmid-flow.png)

1. Ein Benutzer greift auf die Anmeldeseite oder eine begrenzte Ressource für eine Anwendung zu, wodurch eine Anforderung an den {{site.data.keyword.appid_short_notm}}-Endpunkt `/authorization` entweder über ein SDK oder eine API von {{site.data.keyword.appid_short_notm}} initiiert wird. Wenn der Benutzer nicht berechtigt ist, wird der Authentifizierungsablauf mit einer Weiterleitung an {{site.data.keyword.appid_short_notm}} gestartet.
2. Von {{site.data.keyword.appid_short_notm}} wird eine SAML-Authentifizierungsanforderung (AuthNRequest) generiert und der Benutzer automatisch vom Browser an den SAML-Identitätsprovider weitergeleitet.
3. Vom Identitätsprovider wird die SAML-Anforderung ausgewertet, der Benutzer authentifiziert und eine SAML-Antwort mit den jeweiligen Zusicherungen generiert. 
4. Vom Identitätsprovider werden der Benutzer und die Antwort mit der SAML-Antwort an {{site.data.keyword.appid_short_notm}} weitergeleitet. 
5. Wenn die Authentifizierung erfolgreich ist, werden von {{site.data.keyword.appid_short_notm}} Zugriffs- und Identitätstokens erstellt (Autorisierung und Authentifizierung eines Benutzers) und an die App zurückgegeben. Wenn die Authentifizierung fehlschlägt, wird der Fehlercode des Identitätsproviders von {{site.data.keyword.appid_short_notm}} an die App zurückgegeben.
6. Dem Benutzer wird Zugriff auf die App oder die geschützten Ressourcen gewährt.



### Ändert die einmalige Anmeldung (SSO) den Ablauf?
{: #saml-sso-flow}

Das Web-Browser-SSO-Profil, das von {{site.data.keyword.appid_short_notm}} implementiert wird, wird vom Service-Provider initiiert; dies bedeutet, dass von {{site.data.keyword.appid_short_notm}} eine SAML-Anforderung an den Identitätsprovider gesendet werden muss, um die Authentifizierungssitzung einzuleiten. 

Von {{site.data.keyword.appid_short_notm}} werden vom Identitätsprovider initiierte Abläufe derzeit nicht unterstützt; zurzeit dürfen Sie nicht mit dem Service verwendet werden.
{: note}

Wenn vom Identitätsprovider SSO unterstützt wird, kann von der SAML-Authentifizierung eine bereits etablierte SSO-Sitzung zum Authentifizieren des Benutzers verwendet werden. Ist dies nicht der Fall, wird der Benutzer zur Anmeldeseite weitergeleitet. Er wird möglicherweise weitergeleitet, wenn der Identitätsprovider die Voraussetzungen für die Authentifizierung, die in der {{site.data.keyword.cloud_notm}}-Authentifizierungsanforderung definiert sind, nicht mit den Angaben abgleichen kann, die für die SSO verwendet werden. Wenn der Identitätsprovider beispielsweise eine SSO-Benutzersitzung unter Verwendung biometrischer Angaben erstellt, muss der {{site.data.keyword.appid_short_notm}}-Standardauthentifizierungskontext geändert werden. Von {{site.data.keyword.appid_short_notm}} wird standardmäßig erwartet, dass Benutzer unter Verwendung eines Kennworts über HTTPS angemeldet werden: `urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport`.



## SAML für Verwendung mit {{site.data.keyword.appid_short_notm}} konfigurieren
{: #saml-configure}

Sie können SAML für die Verwendung mit {{site.data.keyword.appid_short_notm}} konfigurieren, indem Sie die Metadaten von {{site.data.keyword.appid_short_notm}} dem Identitätsprovider und die Metadaten des Identitätsproviders wiederum {{site.data.keyword.appid_short_notm}} bereitstellen. 



### Dem Identitätsprovider Metadaten zur Verfügung stellen
{: #saml-provide-idp}

Sie müssen einem SAML-kompatiblen Identitätsprovider Informationen zur Verfügung stellen, um Ihre App zu konfigurieren. Die Informationen werden über eine Metadaten-XML-Datei ausgetauscht, die außerdem Konfigurationsdaten enthält, die für die Herstellung einer Vertrauensbeziehung erforderlich sind.
{: shortdesc}

Sie können SAML erst aktivieren, nachdem Sie die Komponente als Identitätsprovider konfiguriert haben.
{: tip}

1. Klicken Sie auf der Registerkarte **Verwalten** des {{site.data.keyword.appid_short_notm}}-Dashboards in der Zeile **SAML** auf **Bearbeiten**, um Ihre Einstellungen zu konfigurieren.
2. Klicken Sie auf die Option, mit der Sie **SAML-Metadatendatei herunterladen** können. Ihr Identitätsprovider erwartet die folgenden Informationen von der Datei.
  <table>
    <tr>
      <th> Variable </th>
      <th> Beschreibung </th>
    </tr>
    <tr>
      <td><code>EntityID</code></td>
      <td>Die Entitäts-ID ermöglicht dem Identitätsprovider die Kenntnis darüber, dass {{site.data.keyword.appid_short_notm}} die SAML-Anforderung ausgegeben hat.</td>
    </tr>
    <tr>
      <td><code>Location URL</code></td>
      <td>Die URL des Standorts, den der Identitätsprovider an die SAML-Zusicherung sendet, nachdem ein Benutzer erfolgreich authentifiziert wurde.</td>
    </tr>
    <tr>
      <td><code>Binding</code></td>
      <td>Die Anweisungen dafür, wie der Identitätsprovider die SAML-Antwort senden soll.</td>
    </tr>
    <tr>
      <td><code>NameID Format</code></td>
      <td>Die Art und Weise, auf die der Identitätsprovider erfährt, welches ID-Format zum Senden im Betreff einer Zusicherung erforderlich ist und wie die Benutzer von {{site.data.keyword.appid_short_notm}} identifiziert werden. Die ID muss das folgende Format aufweisen: <code><saml:NameID Format="urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress"/></code></td>
    </tr>
    <tr>
      <td><code>WantAssertionsSigned</code></td>
      <td>Die Art und Weise, auf die ein Identitätsprovider überprüft, ob er die Zusicherung signieren muss. Der Service erwartet, dass die Zusicherung signiert ist, unterstützt aber keine verschlüsselten Zusicherungen.</td>
    </tr>
  </table>

3. Stellen Sie Ihrem Identitätsprovider die Daten zur Verfügung. Falls Ihr Identitätsprovider das Hochladen der Metadatendatei unterstützt, können Sie dies tun. Falls er das Hochladen nicht unterstützt, konfigurieren Sie die Eigenschaften manuell. Nicht alle Identitätsprovider verwenden dieselben Eigenschaften, sodass nicht alle verwendet werden müssen.

  Die Eigenschaftsnamen können je nach Identitätsprovider variieren.
  {: tip}

4. Legen Sie für **SAML 2.0 Federation** die Einstellung **Aktiviert** fest.



### Das Bereitstellen von Metadaten für {{site.data.keyword.appid_short_notm}}
{: #saml-provide-appid}

Sie können Daten vom Identitätsprovider abrufen und {{site.data.keyword.appid_short_notm}} zur Verfügung stellen.
{: shortdesc}

**Metadaten über die GUI bereitstellen** 

1. Navigieren Sie zur Registerkarte **SAML 2.0** des {{site.data.keyword.appid_short_notm}}-Dashboards. Geben Sie die folgenden Metadaten, die Sie vom Identitätsprovider erhalten haben, im Abschnitt **Metadaten vom SAML-Identitätsprovider (IdP) bereitstellen** ein.
  <table>
    <tr>
      <th> Variable </th>
      <th> Beschreibung </th>
    </tr>
    <tr>
      <td><code>Sign-in URL</code></td>
      <td>Die URL, an die der Benutzer zur Registrierung weitergeleitet wird. Diese URL ist bei Ihrem SAML-Identitätsprovider gehostet.</td>
    </tr>
    <tr>
      <td><code>Entity ID</code></td>
      <td>Die Entitäts-ID ist der globale eindeutige Name für einen SAML-Identitätsprovider.</td>
    </tr>
    <tr>
      <td><code>Signing certificate</code></td>
      <td>Das Signaturzertifikat wird von Ihrem SAML-Identitätsprovider ausgegeben. Es wird für die Registrierung und für die Überprüfung der SAML-Zusicherungen verwendet. Alle Provider sind unterschiedlich, möglicherweise können Sie das Signaturzertifikat von Ihrem Identitätsprovider herunterladen. Das Zertifikat muss das Format <code>.pem</code> aufweisen.</td>
    </tr>
  </table>

2. Optional: Stellen Sie ein **sekundäres Zertifikat** zur Verfügung, das verwendet wird, falls die Signaturvalidierung mit dem primären Zertifikat fehlschlägt. Falls der Signierschlüssel gleich bleibt, blockiert {{site.data.keyword.appid_short_notm}} die Authentifizierung für abgelaufene Zertifikate nicht.
3. Aktualisieren Sie den **Providernamen** und klicken Sie auf **Speichern**. Der Standardname ist SAML.

Möchten Sie einen Authentifizierungskontext festlegen? Sie können dies über die API tun.
{: tip}

</br>

**Metadaten über die API bereitstellen**

1. Zeigen Sie die aktuelle SAML-Konfiguration einschließlich des Authentifizierungskontexts und der Zertifikate an; erstellen Sie hierzu eine GET-Anforderung für den [API-Endpunkt `/saml`](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.get_saml_idp).

  Beispielcode:
  ```
  curl --request GET \
  https://us-south.appid.cloud.ibm.com/management/v4/<tenant-ID>/config/idps/saml \
  --header `Accept: application/json`
  ```
  {: codeblock}

  Beispielausgabe:
  ```
  {
    "isActive": true,
    "config": {
      "entityID": "https://example.com/saml2/metadata/706634",
      "signInUrl": "https://example.com/saml2/sso-redirect/706634",
      "certificates": [
        "certificate-example-pem-format"
      ],
      "displayName": "my saml example",
      "authnContext": {
        "class": [
          "urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport"
        ],
        "comparison": "exact"
      }
    }
  }
  ```
  {: screen}

2. Erstellen Sie eine SAML-Konfiguration durch Ersetzen der Werte im folgenden Beispiel durch die Informationen von Ihrem Provider. Die im Beispiel verwendeten Werte sind erforderlich, Sie können jedoch mehr Informationen als in der Tabelle dargestellt angeben. 

  ```
  "config": {
    "authnContext": {
      "class": [
        "urn:oasis:names:tc:SAML:2.0:ac:classes:YourChosenClassValue",
          "urn:oasis:names:tc:SAML:2.0:ac:classes:YourOtherChosenClassValue"
      ],
      "comparison": "sampleComparisonValue"}
    "entityID": "https://example.com/saml2/metadata/706634",
    "signInUrl": "https://example.com/saml2/sso-redirect/706634",
    "certificates": [
      "primary-certificate-example-pem-format"
        "secondary-certificate-example-pem-format"
    ],
    "displayName": "my saml example",
  }
  ```
  {: codeblock}
  {: #configuring-saml-new}

  <table>
    <tr>
      <th> Variable </th>
      <th> Beschreibung </th>
    </tr>
    <tr>
      <td><code>signInUrl</code></td>
      <td>Die URL, an die der Benutzer zur Registrierung weitergeleitet wird. Diese URL ist bei Ihrem SAML-Identitätsprovider gehostet.</td>
    </tr>
    <tr>
      <td><code>entityID</code></td>
      <td>Die Entitäts-ID ist der globale eindeutige Name für einen SAML-Identitätsprovider.</td>
    </tr>
    <tr>
      <td><code>displayName</code></td>
      <td>Der Name, den Sie Ihrer SAML-Konfiguration zuordnen.</td>
    </tr>
    <tr>
      <td><code>primary-certificate-example-pem-format</code></td>
      <td>Das Zertifikat, das vom SAML-Identitätsprovider ausgegeben wird. Es wird für die Registrierung und für die Überprüfung der SAML-Zusicherungen verwendet. Alle Provider sind unterschiedlich, möglicherweise können Sie das Signaturzertifikat von Ihrem Identitätsprovider herunterladen. Das Zertifikat muss das Format <code>.pem</code> aufweisen.</td>
    </tr>
    <tr>
      <td>Optional: <code>secondary-certificate-example-pem-format</code></td>
      <td>Das Sicherungszertifikat, das vom SAML-Identitätsprovider ausgegeben wird. Es wird verwendet, wenn die Signaturvalidierung mit dem primären Zertifikat fehlschlägt. <strong>Hinweis:</strong> Falls der Signierschlüssel gleich bleibt, blockiert {{site.data.keyword.appid_short_notm}} die Authentifizierung für abgelaufene Zertifikate nicht. </td>
    </tr>
    <tr>
      <td>Optional: <code>authnContext</code></td>
      <td>Der Authentifizierungskontext wird verwendet, um die Qualität der Authentifizierung und SAML-Zusicherungen zu überprüfen. Sie können einen Authentifizierungskontext hinzufügen, indem Sie ein Klassenarray und eine Vergleichszeichenfolge zu Ihrem Code hinzufügen. Sie müssen die Parameter <code>class</code> und <code>comparison</code> mit Ihren Werten aktualisieren. Der Parameter <code>class</code> kann beispielsweise dem Wert für <code>urn:oasis:names:tc:SAML:2.0:ac:classes:YourChosenClassValue</code> ähneln. </td>
    </tr>
  </table>

3. Erstellen Sie eine PUT-Anforderung für den [API-Endpunkt `/saml`](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp), um die Konfiguration anzugeben, die Sie in Schritt 2 in {{site.data.keyword.appid_short_notm}} erstellt haben. Überprüfen Sie das folgende Beispiel, um sich damit vertraut zu machen, wie Ihre Anforderung aussehen kann. 

  ```
  curl --request PUT \
  https://us-south.appid.cloud.ibm.com/management/v4/<tenant-ID>/config/idps/saml \
  --header `Accept: application/json` \
  --data \
  {
    "isActive": true,
    "config": {
      "entityID": "https://example.com/saml2/metadata/706634",
      "signInUrl": "https://example.com/saml2/sso-redirect/706634",
      "certificates": [
        "primary-certificate-example-pem-format"
      ],
      "displayName": "my saml example",
    }
  }
  ```
  {: screen}



## Testen Sie Ihre Konfiguration
{: #saml-testing}

Sie können die Konfiguration zwischen Ihrem SAML-Identitätsprovider und {{site.data.keyword.appid_short_notm}} testen.

1. Stellen Sie sicher, dass Sie Ihre Konfiguration gespeichert haben.
2. Navigieren Sie zur Registerkarte **SAML 2.0** des {{site.data.keyword.appid_short_notm}}-Dashboards und klicken Sie auf **Testen**. Eine neue Registerkarte wird angezeigt.
3. Melden Sie sich als ein Benutzer an, den Ihr Identitätsprovider bereits authentifiziert hat.
4. Nachdem Sie das Formular ausgefüllt haben, werden Sie auf eine andere Seite weitergeleitet.
  * Erfolgreiche Authentifizierung: Die Verbindung zwischen {{site.data.keyword.appid_short_notm}} und dem Identitätsprovider funktioniert korrekt. Die Seite zeigt gültige [Zugriffs- und Identitätstoken](/docs/services/appid?topic=appid-tokens#tokens) an.
  * Fehlgeschlagene Authentifizierung: Die Verbindung ist unterbrochen. Die Seite zeigt die Fehler und die SAML-XML-Antwortdatei an.


Sind Probleme aufgetreten? Weitere Informationen hierzu finden Sie unter [Fehlerbehebung: SAML](/docs/services/appid?topic=appid-troubleshooting-idp#troubleshooting-idp).
{: tip}




## Häufig gestellte Fragen zu SAML
{: #saml-assertions}

SAML-Zusicherungen können auf unterschiedliche Arten zurückgegeben werden. Überprüfen Sie die folgenden Beispiele, um sich damit vertraut zu machen, welches Format von {{site.data.keyword.appid_short_notm}} für die Antwort erwartet wird.
{: shortdesc}


### Wie muss die SAML-Zusicherung für {{site.data.keyword.appid_short_notm}} gestaltet sein?
{: #saml-example}

Der Service erwartet, dass eine SAML-Zusicherung dem folgenden Beispiel entspricht.

```
<samlp:Response xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol" ID="s2202bbbbafa9d270d1c15990b738f4ab36139d463" InResponseTo="_e4a78780-35da-012e-8ea7-0050569200d8" Version="2.0" IssueInstant="2011-03-21T11:22:02Z" Destination="https://example.example.com/">
  <saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">idp_entityId</saml:Issuer>
  <samlp:Status xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <samlp:StatusCode  xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol"Value="urn:oasis:names:tc:SAML:2.0:status:Success"/>
  </samlp:Status>
  <saml:Assertion xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="2.0" ID="pfx539c9774-de5c-5f52-0c3f-b1c2e2697a89" IssueInstant="2018-01-29T13:02:58Z" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <saml:Issuer>idp_entityId</saml:Issuer>
    <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      <ds:SignedInfo>
        <ds:CanonicalizationMethod Algorithm="one_of_supported_algo"/>
        <ds:SignatureMethod Algorithm="one_of_supported_algo"/>
        <ds:Reference URI="#pfx539c9774-de5c-5f52-0c3f-b1c2e2697a89">
          <ds:Transforms>
            <ds:Transform Algorithm="one_of_supported_algo"/>
            <ds:Transform Algorithm="one_of_supported_algo"/>
          </ds:Transforms>
          <ds:DigestMethod Algorithm="one_of_supported_algo"/>
          <ds:DigestValue>huywDPPfOEGyyzE7d5hjOG97p7FDdGrjoSfes6RB19g=</ds:DigestValue>
        </ds:Reference>
      </ds:SignedInfo>
 <ds:SignatureValue>BAwNZFgWF2oxD1ux0WPfeHnzL+IWYqGhkM9DD28nI9v8XtPN8tqmIb5y4bomaYknmNpWYn7TgNO2Rn/XOq+N9fTZXO2RybaC49iF+zWibRIcNwFKCCpDL6H6jA5eqJX2YKBR+K6Yt2JPoUIRLmqdgm2lMr4Nwq1KYcSzQ/yoV5W0SN/V5t8EfctFoaXVPdtfHVXkwqHeufo+L4gobFt9NRTzXB0SQEClA1L8hQ+/LhY4l46k1D0c34iWjVLZr+ecQyubf7rekOG/R7DjWCFMTke822dR+eJTPWFsHGSPWCDDHFYqB4QMinTvUnsngjY3AssPqIOjeUxjL3p+GXn8IQ==</ds:SignatureValue>
    </ds:Signature>
    <saml:Subject>
      <saml:NameID Format="urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress">JohnDoe@gmail.com</saml:NameID>
    </saml:Subject>
    <saml:Conditions NotBefore="2018-01-29T12:59:58Z" NotOnOrAfter="2018-01-29T13:05:58Z">
    </saml:Conditions>
</samlp:Response>
```
{: screen}


### Welche Typen von Algorithmen werden von {{site.data.keyword.appid_short_notm}} unterstützt?
{: #saml-signatures}

{{site.data.keyword.appid_short_notm}} verwendet den Algorithmus <a href="http://www.w3.org/2001/04/xmldsig-more#rsa-sha256" target="_blank">RSA-SHA256 <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>, um digitale XML-Signaturen zu verarbeiten.

