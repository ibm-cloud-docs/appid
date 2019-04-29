---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-10"

keywords: authentication, authorization, identity, app security, secure, tokens, jwt, development

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


# Tokens validieren
{: #token-validation}

Die Tokenvalidierung ist ein wichtiger Bestandteil der modernen App-Entwicklung. Durch die Validierung von Tokens können Sie Ihre App oder APIs vor unbefugten Benutzern schützen. {{site.data.keyword.appid_full}} verwendet Zugriffs- und Identitätstoken, um sicherzustellen, dass ein Benutzer oder eine Anwendung authentifiziert wird, bevor der Zugriff erteilt wird. Wenn Sie eines der von {{site.data.keyword.appid_short_notm}} zur Verfügung gestellten SDKs verwenden, erfolgt das Anfordern und Validieren der Tokens automatisch für Sie.
{: shortdesc}

Weitere Informationen dazu, wie Tokens in {{site.data.keyword.appid_short_notm}} verwendet werden, finden Sie unter [Informationen zu Tokens](/docs/services/appid?topic=appid-tokens#tokens).
{: tip}

Tokens werden verwendet, um zu überprüfen, ob eine Person die ist, die sie zu sein behauptet. Sie bestätigen alle Zugriffsberechtigungen, die der Benutzer für eine bestimmte Dauer haben kann. Wenn sich ein Benutzer bei Ihrer Anwendung anmeldet und ein Token für ihn ausgegeben wird, muss Ihre App den Benutzer validieren, bevor er Zugriff erhält.

</br>

**Was ist, wenn ich in einer Sprache arbeite, für die {{site.data.keyword.appid_short_notm}} kein SDK hat?**

Kein Problem! Sie haben drei Optionen:

* Mit den {{site.data.keyword.appid_short_notm}}-APIs arbeiten
* Eine eigene Validierungslogik implementieren
* Ein beliebiges OIDC-kompatibles Open-Source-SDK verwenden

Erfahrungsgemäß ist Option 1 das einfachste Verfahren.
{: tip}

</br>
</br>

## {{site.data.keyword.appid_short_notm}}-APIs verwenden
{: #remote-validation}

Mithilfe von Introspektion können Sie {{site.data.keyword.appid_short_notm}} verwenden, um Ihre Tokens zu validieren.
{: shortdesc}

1. Senden Sie eine POST-Anforderung an den API-Endpunkt [/introspect](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Authorization%20Server%20-%20Authorization%20Server%20V4/oauth-server.token), um Ihr Token zu validieren. Die Anforderung muss das Token und einen Header für die Basisautorisierung bereitstellen, der die Client-ID und den geheimen Schlüssel enthält.

  Beispielanforderung:

    ```
    POST /oauth/v4/{tenant_id}/introspect HTTP/1.1
    Host: us-south.appid.cloud.ibm.com
    Content-Type: application/x-www-form-urlencoded
    Authorization: Basic jdFlUaGlZUzAwTW0Tjk15TmpFMw==
    Cache-Control: no-cache

    token=XXXXX.YYYYY.ZZZZZ
    ```
    {: screen}

2. Der Server überprüft den Ablaufzeitpunkt und die Signatur des Tokens und gibt ein JSON-Objekt zurück, das angibt, ob das Token aktiv oder inaktiv ist.

  Beispielantwort:

    ```
    {
      "active": true
    }
    ```
    {: screen}


## Tokens manuell validieren
{: #local-validation}

Sie können Ihre Tokens lokal validieren, indem Sie das Token syntaktisch analysieren, die Tokensignatur verifizieren und die im Token gespeicherten Anforderungen (sog. Claims) validieren.
{: shortdesc}


1. Analysieren Sie die Tokens syntaktisch. [JSON Web Token (JWT)](https://tools.ietf.org/html/rfc7519) ist ein Standardverfahren für die sichere Übermittlung von Informationen. Es besteht aus drei Hauptteilen: Header, Nutzdaten und Signatur. Sie sind base64URL-codiert und durch einen Punkt (.) getrennt. Sie können jeden beliebigen base64URL-Decoder verwenden, um das Token syntaktisch zu analysieren. Alternativ können Sie auch jede der [aufgelisteten Bibliotheken](https://jwt.io/#libraries-io) verwenden, um das Token syntaktisch zu analysieren.

  Beispiel für ein verschlüsseltes Token:

    ```
    eyJhbGciOiJSUzI1NiIsInR5cCI6IkpPU0UiLCJraWQiOiJhMmszIn0
    .eyJpc3MiOiJhcHBpZC1vYXV0aCIsImF1ZCI6ImFiYzEyMyIsImV4cCI6MTU2NDU2Nn0
    .IycnAGUmMHzpTWbe-qaRsx0B4Zi-SVav710Fb_8CTCQvLrHX9d42WuCZ5bW
    d-ikgEsf6waQxeBfhfwYxwHN87LZupApagVMZtylVAnXhG1pHu_32wbZsPvg6QjzNO
    j6ys2Lfl3qfb5Qrp9u4IsZltKPEN8HdfeOcKXxpw6UqP-8
    ```
    {: screen}

  Beispiel für einen entschlüsselten Header:

    ```
    {
      "alg": "RS256",
      "typ": "JOSE",
      "kid": "a2k3"
    }
    ```
    {: screen}

  Entschlüsselte Nutzdaten:

    ```
    {
      "iss": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61",
      "aud": "abc123",
      "exp": 1564566
    }
    ```
    {: screen}

2. Rufen Sie den Endpunkt [/publickeys](https://us-south.appid.cloud.ibm.com/swagger-ui/#!/Authorization_Server_V4/publicKeys) auf, um Ihre öffentlichen Schlüssel abzurufen. Die öffentlichen Schlüssel, die zurückgegeben werden, werden als [JSON Web Keys (JWK)](https://tools.ietf.org/html/rfc7517) formatiert.

  Beispielanforderung:

    ```
    GET /oauth/v4/{tenant_id}/publickeys HTTP/1.1
    Host: us-south.appid.cloud.ibm.com
    Cache-Control: no-cache
    ```
    {: screen}

3. Speichern Sie die Schlüssel für eine spätere Verwendung in Ihrem App-Cache. Das Speichern der Schlüssel beschleunigt die Verarbeitung und verhindert netzbedingte Verzögerungen, wenn ein anderer Aufruf erfolgt.

4. Importieren Sie die Parameter für den öffentlichen Schlüssel.

  Beispielantwort:

    ```
    {
      "keys": [
        {
          "kty": "RSA",
          "use": "sig",
          "n": "AsdaE",
          "e": "SDAasw",
          "kid": "ad123dCAz"
        }
      ]
    }
    ```
    {: screen}

  <table>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="Symbol für weitere Informationen"/> Parameter für öffentlichen Schlüssel </th>
    </thead>
    <tbody>
      <tr>
        <td><code>kty</code></td>
        <td>Definiert den verwendeten Algorithmus.</td>
      </tr>
      <tr>
        <td><code>use</code></td>
        <td>Definiert den Zweck des Schlüssels.</td>
      </tr>
      <tr>
        <td><code>kid</code></td>
        <td>Definiert die eindeutige ID des Schlüssels.</td>
      </tr>
      <tr>
        <td>Andere</td>
        <td>Es können noch weitere Parameter vorhanden sein, die für Ihren Algorithmus spezifisch sind und die ebenfalls importiert werden müssen.</td>
      </tr>
    </tbody>
  </table>

5. Verifizieren Sie die Signatur des Tokens. Der Token-Header enthält den Algorithmus, mit dem das Token signiert wurde, sowie die Schlüssel-ID oder den Claim `kid` des übereinstimmenden öffentlichen Schlüssels. Da öffentliche Schlüssel nicht häufig geändert werden, können Sie öffentliche Schlüssel in Ihrer App zwischenspeichern und sie gelegentlich aktualisieren. Wenn der Claim `kid` des zwischengespeicherten Schlüssels fehlt, können Sie die Tokens lokal validieren.

  1. Lassen Sie Ihre Anwendung überprüfen, ob der Inhalt des eingehenden Token-Headers mit den Parametern des öffentlichen Schlüssels übereinstimmt.
  2. Überprüfen Sie insbesondere, ob dieselben Algorithmen verwendet wurden und ob Ihr Cache für öffentliche Schlüssel einen Schlüssel mit der relevanten Schlüssel-ID enthält.
  3. Stellen Sie sicher, dass Ihr Hashwert mit der Signatur des PEM-Formulars des öffentlichen Schlüssels übereinstimmt. Der Hashwert kann durch Kombinieren und Hashing des Headers der Nutzdaten des Tokens abgerufen werden. Da eine manuelle Implementierung dieses Prozesses komplex sein kann, sollte möglicherweise eine der [aufgelisteten Bibliotheken](https://jwt.io/) verwendet werden, um die Signatur zu überprüfen.

6. Validieren Sie die in den Tokens gespeicherten Claims. Um zukünftige Prüfungen zu verifizieren, können Sie [diese Liste](http://openid.net/specs/openid-connect-core-1_0.html#IDTokenValidation) verwenden.
  <table>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="Symbol für weitere Informationen"/> Claims, die validiert werden müssen </th>
    </thead>
    <tbody>
      <tr>
        <td><code>iss</code></td>
        <td>Der Aussteller muss mit dem {{site.data.keyword.appid_short_notm}}-OAuth-Server identisch sein.</td>
      </tr>
      <tr>
        <td><code>exp</code></td>
        <td>Die aktuelle Uhrzeit muss vor der Ablaufzeit liegen.</td>
      </tr>
      <tr>
        <td><code>aud</code></td>
        <td>Die Zielgruppe muss die Kunden-ID Ihrer App enthalten.</td>
      </tr>
      <tr>
        <td><code>tenant</code></td>
        <td>Der Tenant muss die Tenant-ID Ihrer App enthalten.</td>
      </tr>
      <tr>
        <td><code>scope</code></td>
        <td>Der Umfang der Berechtigungen, die dem Benutzer erteilt wurden. Dies ist für das Zugriffstoken spezifisch.</td>
      </tr>
    </tbody>
  </table>
