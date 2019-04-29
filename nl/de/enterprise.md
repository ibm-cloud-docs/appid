---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

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

Security Assertion Markup Language (SAML) ist ein offener Standard für den Austausch von Authentifizierungs- und Autorisierungsdaten zwischen einem Identitätsprovider, der die Benutzeridentität bestätigt, und einem Service-Provider, der die Benutzeridentitätsinformationen verarbeitet.
{: shortdesc}

{{site.data.keyword.appid_short_notm}} funktioniert als Service-Provider und initiiert eine SSO-Anmeldung (Single Sign-on) bei einem anderen Anbieter wie beispielsweise Active Directory Federation Services (Active Directory-Verbunddienste). Das <a href="http://saml.xml.org/saml-specifications" target="blank">SAML-Protokoll <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> unterstützt unterschiedliche Profile und Bindeoptionen. {{site.data.keyword.appid_short_notm}} unterstützt das SSO-Profil des Web-Browsers mit HTTP-POST-Bindung. 

Eine Anleitung zur Verwendung eines bestimmten SAML-Identitätsproviders finden Sie in den Blogbeiträgen zum Einrichten von {{site.data.keyword.appid_short_notm}} mit [Ping One ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-ping-one/), [Azure Active Directory ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-azure-active-directory/) oder [Active Directory Federation Service ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-active-directory-federation-service/).
{: tip}



## Informationen zu Zusicherungen
{: #saml-assertions}

Eine SAML-Zusicherung weist Ähnlichkeiten mit einem [Benutzerattribut](/docs/services/appid?topic=appid-user-profile#user-profile) auf. Es handelt sich dabei um eine Erklärung oder Einzelinformation über einen Benutzer, die von einem Identitätsprovider an {{site.data.keyword.appid_short_notm}} zurückgegeben wird, wenn sich ein Benutzer erfolgreich bei Ihrer App anmeldet. Abhängig von der App-Konfiguration und vom verwendeten Identitätsprovider umfassen diese Informationen einen Benutzernamen, eine E-Mail-Adresse oder ein weiteres Feld, das Sie angeben müssen.
{: shortdesc}

Wenn die Zusicherungen an {{site.data.keyword.appid_short_notm}} zurückgegeben werden, dann bindet der Service die Benutzeridentität ein. Wenn die SAML-Zusicherung einem der folgenden OIDC-Claims entspricht, dann wird sie automatisch zum Identitätstoken hinzufügt. Dabei ist zu beachten, dass nach einer Änderung von Werten auf der Providerseite die neuen Werte erst nach einer erneuten Anmeldung des Benutzers verfügbar sind.

 * `Name`
 * `E-Mail`
 * `Ländereinstellung`
 * `Bild`

Die Zusicherungen, die keinem der Standardnamen zugeordnet werden können, werden standardmäßig ignoriert. Wenn Ihr SAML-Provider weitere Zusicherungen zurückgibt, dann können diese Informationen ggf. abgerufen werden, wenn sich der Benutzer anmeldet. Durch die Erstellung eines Arrays mit den Zusicherungen, die Sie verwenden möchten, können Sie die [Informationen in Ihre Tokens einfügen](/docs/services/appid?topic=appid-customizing-tokens#customizing-tokens). Dabei ist allerdings darauf zu achten, dass keine unnötigen Informationen zu Ihren Tokens hinzugefügt werden. Tokens werden normalerweise in HTTP-Headern gesendet, die von begrenzter Größe sind.
{: tip}

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




## Dem Identitätsprovider Metadaten zur Verfügung stellen
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
      <td>Die Art und Weise, auf die der Identitätsprovider erfährt, welches ID-Format zum Senden im Betreff einer Zusicherung erforderlich ist. Die Art und Weise, auf die {{site.data.keyword.appid_short_notm}} Benutzer identifiziert.</td>
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

## Das Bereitstellen von Metadaten für {{site.data.keyword.appid_short_notm}}
{: #saml-provide-appid}

Sie können Daten vom Identitätsprovider abrufen und {{site.data.keyword.appid_short_notm}} zur Verfügung stellen.
{: shortdesc}

### Metadaten über die GUI bereitstellen
{: #saml-provide-gui}

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


### Metadaten über die API bereitstellen
{: #saml-provide-api}

1. Rufen Sie Ihre SAML-Metadaten ab, indem Sie eine GET-Anforderung an den API-Endpunkt [/getSamlMetadata](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.get_saml_idp) stellen.

  Beispielcode:
  ```
  <?xml version="1.0"?>
  <getSamlMetadata>
    <?xml version="1.0"?> <EntityDescriptor> <SPSSODescriptor> <NameIDFormat> </NameIDFormat> <AssertionConsumerService /> </SPSSODescriptor>
   </EntityDescriptor>
    </getSamlMetadata>
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
    },
    "validation_data": {
      "certificates": [
        {
          "certificate_index": 0,
          "expiration_timestamp": 1674473996,
          "warning": "Your certificate will expire in 18 days."
        }
      ]
    }
  }
  ```
  {: screen}

2. Konfigurieren Sie Ihre POST-Anforderung an den API-Endpunkt [/set_saml_idp](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp).

  1. Ersetzen Sie in dem folgenden Metadatenbeispiel die Variablen durch Ihre eigenen Daten.

    ```
    Put {Management URI}/config/idps/saml
    Content-Type: application/json
    {
      "isActive": true,
      "config": {
        "entityID": "https://example.com/saml2/metadata/706634",
        "signInUrl": "https://example.com/saml2/sso-redirect/706634",
        "certificates": [
          "primary-certificate-example-pem-format"
        ],
        "displayName": "my saml example"
      }
    }
    ```
    {: codeblock}

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

  2. Optional: Fügen Sie dem primären Zertifikat im Zertifikatarray ein sekundäres Zertifikat hinzu. Das sekundäre Zertifikat wird verwendet, wenn die Signaturvalidierung mit dem primären Zertifikat fehlschlägt. Falls der Signierschlüssel gleich bleibt, blockiert {{site.data.keyword.appid_short_notm}} die Authentifizierung für abgelaufene Zertifikate nicht.

    Beispiel:
    ```
    {
      "isActive": true,
      "config": {
        ...
        "certificates": [
          "primary-certificate-example-pem-format",
          "secondary-certificate-example-pem-format"
        ],
        ...
      }
    }
    ```
    {: screen}
  {: #configuring-saml-new}
  3. Optional: Fügen Sie einen Authentifizierungskontext hinzu, indem Sie ein Klassenarray und eine Vergleichszeichenfolge zu Ihrem Code hinzufügen. Sie müssen die Parameter `class` und `comparison` mit Ihren Werten aktualisieren. Ein Authentifizierungskontext wird verwendet, um die Qualität der Authentifizierung und SAML-Zusicherungen zu überprüfen.

    Beispiel:
    ```
    {
      "isActive": true,
      "config": {
        ...
        "authnContext": {
          "class": [
            "urn:oasis:names:tc:SAML:2.0:ac:classes:YourChosenClassValue",
            "urn:oasis:names:tc:SAML:2.0:ac:classes:YourOtherChosenClassValue"
          ],
          "comparison": "sampleComparisonValue"
        }
      }
    }
    ```
    {: screen}

3. Stellen Sie die Anforderung. Wenn Sie die optionalen Werte hinzufügen möchten, sollte Ihre Anforderung ähnlich wie im folgenden Beispiel aussehen.

  ```
  Put {Management URI}/config/idps/saml
  Content-Type: application/json
  {
    "isActive": true,
    "config": {
      ...
      "authnContext": {
        "class": [
          "urn:oasis:names:tc:SAML:2.0:ac:classes:YourChosenClassValue",
          "urn:oasis:names:tc:SAML:2.0:ac:classes:YourOtherChosenClassValue"
        ],
        "comparison": "sampleComparisonValue"
      "entityID": "https://example.com/saml2/metadata/706634",
      "signInUrl": "https://example.com/saml2/sso-redirect/706634",
      "certificates": [
        "primary-certificate-example-pem-format"
        "secondary-certificate-example-pem-format"
      ],
      "displayName": "my saml example"
    }
  }
  ```
  {: codeblock}


## Testen Sie Ihre Konfiguration
{: #saml-testing}

Sie können die Konfiguration zwischen Ihrem SAML-Identitätsprovider und {{site.data.keyword.appid_short_notm}} testen.

1. Stellen Sie sicher, dass Sie Ihre Konfiguration gespeichert haben.
2. Navigieren Sie zur Registerkarte **SAML 2.0** des {{site.data.keyword.appid_short_notm}}-Dashboards und klicken Sie auf **Testen**. Eine neue Registerkarte wird angezeigt.
3. Melden Sie sich als ein Benutzer an, den Ihr Identitätsprovider bereits authentifiziert hat.
4. Nachdem Sie das Formular ausgefüllt haben, werden Sie auf eine andere Seite weitergeleitet.
  * Erfolgreiche Authentifizierung: Die Verbindung zwischen {{site.data.keyword.appid_short_notm}} und dem Identitätsprovider funktioniert korrekt. Die Seite zeigt gültige [Zugriffs- und Identitätstoken](/docs/services/appid?topic=appid-tokens#tokens) an.
  * Fehlgeschlagene Authentifizierung: Die Verbindung ist unterbrochen. Die Seite zeigt die Fehler und die SAML-XML-Antwortdatei an.


Sind Probleme aufgetreten? Weitere Informationen hierzu finden Sie unter [Fehlerbehebung bei Identitätsproviderkonfigurationen](/docs/services/appid?topic=appid-troubleshooting-idp#troubleshooting-idp).
{: tip}
