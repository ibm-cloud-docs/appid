---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-13"

keywords: authentication, authorization, identity, app security, secure, custom, proprietary, private key, public key, jwt

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

# Angepasst
{: #custom-identity}

Wenn Sie sich authentifizieren, können Sie Ihren eigenen angepassten Identitätsprovider verwenden. Ihr Identitätsprovider kann jedem Authentifizierungsmechanismus entsprechen, der nicht speziell von {{site.data.keyword.appid_full}} unterstützt wird (einschließlich proprietärer Provider).
{: shortdesc}

Wenn {{site.data.keyword.appid_short_notm}} keine direkte Unterstützung für einen bestimmten Identitätsprovider bereitstellt, können Sie den angepassten Identitätsablauf verwenden, um das Authentifizierungsprotokoll mit dem vorhandenen Authentifizierungsablauf von {{site.data.keyword.appid_short_notm}} zu verbinden. Beispiel: Sie möchten GitHub oder LinkedIn verwenden, um Ihren Benutzern die Anmeldung zu ermöglichen. Sie können das vorhandene SDK des Identitätsproviders verwenden, um die Benutzerauthentifizierungsinformationen zu vereinfachen, bevor sie mit {{site.data.keyword.appid_short_notm}} gepackt und ausgetauscht werden. In vielen Unternehmensszenarios ist es möglich, dass ein traditioneller Identitätsprovider sein eigenes angepasstes Authentifizierungsprotokoll verwendet, und trotzdem soll die Funktionalität von {{site.data.keyword.appid_short_notm}} genutzt werden. Für ein solches Szenario stellt der angepasste Identitätsablauf eine entkoppelte Möglichkeit bereit, Ihre Benutzer sicher zu authentifizieren, ohne ihre Berechtigungsnachweise offenzulegen.

## Angepasste Identität konfigurieren
{: #custom-configure}

Sie können die folgenden Schritte ausführen, um Ihren angepassten Identitätsprovider für die Verwendung mit {{site.data.keyword.appid_short_notm}} zu konfigurieren.
{: shortdesc}

### Vorbereitungen
{: #custom-identity-before}

Um eine Vertrauensbeziehung zwischen {{site.data.keyword.appid_short_notm}} und Ihrem angepassten Identitätsprovider herzustellen, müssen Sie ein RSA-PEM-Schlüsselpaar mit einer Mindestlänge von 2048 haben. Stellen Sie sicher, dass Sie Backups aller Schlüssel, die Sie in der Produktion verwenden, erstellen und sicher aufbewahren.

Wie werden die Schlüssel verwendet?

- Ihr privater Schlüssel wird in Ihrer App oder im Identitätsprovider zum Signieren von JWTs verwendet.
- Ihr öffentlicher Schlüssel wird von {{site.data.keyword.appid_short_notm}} verwendet, um das JWT zu validieren, das die Benutzerinformationen enthält.

Führen Sie den folgenden Befehl aus, um ein RSA-PEM-Schlüsselpaar unter Verwendung von Open SSL zu generieren:

```
$ openssl genpkey -algorithm RSA -out private_key.pem -pkeyopt rsa_keygen_bits:2048
$ openssl rsa -pubout -in private_key.pem -out public_key.pem
```
{: codeblock}

</br>

### Mit der GUI konfigurieren
{: #custom-identity-configure-gui}

1. Melden Sie sich bei Ihrem {{site.data.keyword.cloud_notm}}-Konto an und navigieren Sie zu Ihrer Instanz von {{site.data.keyword.appid_short_notm}}.

2. Setzen Sie auf der Registerkarte **Verwalten** die Option **Angepasster Identitätsprovider** auf **Ein**.

3. Registrieren Sie Ihren öffentlichen Schlüssel bei {{site.data.keyword.appid_short_notm}}.
  1. Navigieren Sie zur Registerkarte **Angepasster Identitätsprovider**.
  2. Fügen Sie Ihren öffentlichen Schlüssel in das Feld **Öffentlicher Schlüssel** ein und klicken Sie auf **Speichern**.



### Mit der API konfigurieren
{: #custom-identity-configure-api}

Registrieren Sie Ihren Schlüssel, indem Sie eine PUT-Anforderung an den [Management-API-Endpunkt](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_custom_idp) stellen.

```
Put {Management URI}/config/idps/custom
Content-Type: application/json
{
    isActive: true,
    config: {
        publicKey: <Your newline separated (\n) PEM public key>
    }
}
```
{: codeblock}

## Konfiguration testen
{: #custom-identity-testing}

Wenn Sie Ihre {{site.data.keyword.appid_short_notm}}-Instanz mit einem gültigen öffentlichen Schlüssel konfiguriert haben, können Sie die vom Service zur Verfügung gestellte Testanwendung verwenden, um zu prüfen, ob die Konfiguration ordnungsgemäß eingerichtet ist. In der Beispielapp können Sie die Nutzdaten von {{site.data.keyword.appid_short_notm}}-Zugriffs- und -Identitätstoken anzeigen, die während eines Standardanmeldeablaufs zurückgegeben werden.

1. Klicken Sie auf der Registerkarte **Angepasster Identitätsprovider** auf **Test**, um die Testanwendung zu öffnen.

2. Erstellen Sie ein [Beispiel für das JWT](https://jwt.io/) nach dem angepassten [Identitätsprotokoll](/docs/services/appid?topic=appid-custom-auth#generating-jwts).

3. Fügen Sie Ihr JWT in das Feld mit der Bezeichnung **JSON Web Token** ein und klicken Sie auf **Test**, um eine Beispielauthentifizierung auszuführen.

Nach erfolgreicher Ausführung können Sie jetzt die entschlüsselten {{site.data.keyword.appid_short_notm}}-Identitätstokens und -Zugriffstokens anzeigen, die für Ihre Anwendung in einem Standardanmeldeablauf verfügbar wären.

## Nächste Schritte
{: #custom-identity-next}

Ihr angepasster Identitätsprovider ist nun konfiguriert. [Fügen Sie ihn Ihrer Anwendung hinzu.](/docs/services/appid?topic=appid-custom-auth#custom-auth)
