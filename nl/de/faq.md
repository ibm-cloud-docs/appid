---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}


# Häufige Fragen

Hier finden Sie Antworten auf häufig gestellte Fragen zum {{site.data.keyword.appid_full}}-Service.
{: shortdesc}


## Wie wird die Preisstruktur in {{site.data.keyword.appid_short_notm}} berechnet?
{: #pricing}

In {{site.data.keyword.appid_short_notm}} sinken die Kosten, je mehr Ressourcen Sie nutzen.
{: shortdesc}

Der Plan mit gestaffelten Preisstufen besteht aus zwei Teilen: der Anzahl von Authentifizierungsereignissen und der Anzahl berechtigter Benutzer. Die Gebühren werden monatlich auf der Basis der Zusammenfassung der beiden Teile erhoben. Der Gesamtpreis besteht aus der kumulativen Gebühr für jede Nutzungsstufe und setzt sich aus der Menge multipliziert mit dem Einzelpreis für die jeweilige Preisstufe zusammen.

### Authentifizierungsereignisse

Ein Authentifizierungsereignis findet statt, wenn ein neues reguläres oder anonymes Zugriffstoken ausgegeben wird. Für identifizierte Benutzer ist jedes neue Zugriffstoken standardmäßig für eine Stunde gültig, unabhängig davon, ob es über eine tatsächliche Benutzerauthentifizierung oder über Aktualisierungstoken generiert wurde. Anonyme Token sind standardmäßig einen Monat gültig. Nach dem Ablaufen des Tokens müssen Sie ein neues Token erstellen, um auf geschützte Ressourcen zuzugreifen. Sie können die Ablaufzeit der {{site.data.keyword.appid_short_notm}}-Token auf der Seite für die Ablaufzeit bei der Anmeldung**** im {{site.data.keyword.appid_short_notm}}-Dashboard aktualisieren. 

Wenn Sie {{site.data.keyword.appid_short_notm}} in mobilen Anwendungen verwenden, werden Token im Keystore oder in einer Schlüsselkette (Keychain) gespeichert und späteren Anforderungen hinzugefügt. Auf die Token kann über das Android- oder iOS-Swift-SDK für APP ID zugegriffen werden. Wenn Sie {{site.data.keyword.appid_short_notm}} in Webanwendungen verwenden, empfiehlt es sich, die Token in Cookies für die Anwendungssitzung zu speichern. 


### Berechtigte Benutzer

Bei einem berechtigten Benutzer handelt es sich um einen eindeutigen Benutzer, der sich direkt oder indirekt bei Ihrem Service anmeldet. Jede Mal, wenn sich ein neuer Benutzer über einen bestimmten Identitätsprovider anmeldet, werden Gebühren für einen berechtigten Benutzer erhoben; dies gilt auch für anonyme Benutzer. Beispiel: Wenn sich ein Benutzer über Facebook und zu einem späteren Zeitpunkt über Google anmeldet, wird er als zwei separate berechtigte Benutzer betrachtet.

Weitere Informationen zu gestaffelten Preisstufen finden Sie in der [{{site.data.keyword.Bluemix_notm}}-Dokumentation zu Preisstrukturen](/docs/billing-usage/how_charged.html#services).

</br>


## Wie funktioniert die Verschlüsselung in {{site.data.keyword.appid_short_notm}}?
{: #encryption}

In der folgenden Tabelle finden Sie Antworten auf häufige Fragen zur Verschlüsselung. 

<table>
  <thead>
    <th colspan=2><img src="images/idea.png" alt="Symbol für weitere Informationen"/>  </th>
  </thead>
  <tbody>
    <tr>
      <td>Wozu dient die Verschlüsselung?</td>
      <td>Vom Service werden gespeicherte Kundendaten verschlüsselt. </td>
    </tr>
    <tr>
      <td>Haben Sie einen eigenen Algorithmus erstellt? Welcher Algorithmus wird im Code verwendet?</td>
      <td>Wir haben keinen eigenen Algorithmus erstellt. Der Service verwendet <code>AES</code> und <code>SHA-256</code> mit Salting. </td>
    </tr>
    <tr>
      <td>Werden öffentliche oder Open-Source-Verschlüsselungsmodule oder -provider verwendet? Werden die Verschlüsselungsfunktionen offengelegt? </td>
      <td>Vom Service werden die Java-Bibliotheken <code>javax.crypto</code> verwendet. Die Verschlüsselungsfunktionen werden jedoch niemals offengelegt. </td>
    </tr>
    <tr>
      <td>Wie werden Schlüssel gespeichert?</td>
      <td>Schlüssel werden nach dem Generieren lokal gespeichert, nachdem sie mit einem regionsspezifischen Hauptschlüssel verschlüsselt wurden. Die Hauptschlüssel werden in {{site.data.keyword.keymanagementserviceshort}} gespeichert. </td>
    </tr>
    <tr>
      <td>Welche Schlüssellänge wird verwendet? </td>
      <td>Der Service verwendet 16 Byte. </td>
    </tr>
    <tr>
      <td>Werden ferne APIs aufgerufen, die Verschlüsselungsfunktionalität offenlegen? </td>
      <td>Nein. </td>
    </tr>
  </tbody>
</table>

</br>

## Wie muss die SAML-Zusicherung für {{site.data.keyword.appid_short_notm}} gestaltet sein?
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

</br>

## Welche Algorithmen werden für SAML-Signaturen unterstützt?
{: #saml-signatures}

Sie können einen beliebigen der folgenden Algorithmen verwenden, um digitale XML-Signaturen zu verarbeiten.

<table>
  <tr>
    <th> Typ des Algorithmus </th>
    <th> Algorithmusoptionen </th>
  </tr>
  <tr>
    <td>Kanonisierungs- und Transformationsalgorithmen mit Kommentaren und ohne Kommentare</td>
    <td><ul><li><a href="http://www.w3.org/TR/2001/REC-xml-c14n-20010315" target="_blank">Kanonisierung <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></li>
    <li><a href="http://www.w3.org/2001/10/xml-exc-c14n#" target="_blank">Exklusive Kanonisierung mit Kommentaren und ohne Kommentare <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></li>
    <li><a href=" http://www.w3.org/2000/09/xmldsig#enveloped-signature" target="_blank">Enveloped Signature-Transformation <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></li></ul></td>
  </tr>
  <tr>
    <td>Hashalgorithmen</td>
    <td><ul><li><a href="http://www.w3.org/2000/09/xmldsig#sha1" target="_blank">SHA1-Fingerabdrücke <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmlenc#sha256" target="_blank">SHA256-Fingerabdrücke <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmlenc#sha512" target="_blank">SHA512-Fingerabdrücke <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></li></ul></td>
  </tr>
  <tr>
    <td>Signaturalgorithmen</td>
    <td><ul><li><a href="http://www.w3.org/2000/09/xmldsig#rsa-sha1" target="_blank">RSA-SHA1 <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmldsig-more#rsa-sha256" target="_blank">RSA-SHA256 <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmldsig-more#rsa-sha512" target="_blank">RSA-SHA512 <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></li>
    <li><a href="http://www.w3.org/2000/09/xmldsig#hmac-sha1" target="_blank">HMAC-SHA1 <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></li></ul></td>
  </tr>
</table>

Weitere Informationen zur Verwendung eines SAML-Identitätsproviders finden Sie in [Unternehmensidentitätsprovider konfigurieren](enterprise.html).
