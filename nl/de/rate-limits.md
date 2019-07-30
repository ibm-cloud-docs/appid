---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-09"

keywords: Authentication, authorization, identity, app security, secure, rates, cloud directory, rate limit, attempts

subcollection: appid

---

{:external: target="_blank" .external}
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


# Einschränkungen von App ID
{: #limits}

Zum Steuern des Datenverkehrsvolumens durch die App ID-Instanz wird eine Ratenbegrenzung (Rate Limiting) verwendet. Durch die Begrenzung der Anforderung bzw. Ressourcen können Sie die Anwendungen schützen.
{: shortdesc}

## App ID-Lite-Plan 
{: #lite-limits}

Überprüfen Sie die folgende Tabelle, um sich mit den Einschränkungen vertraut zu machen, die für Lite-Instanzen von App ID gelten. 

<table>
    <tr>
        <th>Ressource</th>
        <th>Maximum</th>
    </tr>
    <tr>
        <td>Benutzer</td>
        <td>1000</td>
    </tr>
    <tr>
        <td>Authentifizierungen</td>
        <td>1000 pro Monat</td>
    </tr>
</table>

## Allgemein
{: #general-limits}

In der folgenden Tabelle werden die Höchstwerte pro Benutzer für IBM Cloud App ID-Ressourcen und die Blockierungsdauer im Fall einer Überschreitung der Grenzwerte aufgelistet. Diese Grenzwerte gelten für alle Benutzer, die IBM Cloud App ID-Ressourcen erstellen können.
{: shortdesc}

<table>
    <tr>
        <th>API</th>
        <th>Grenzwert</th>
        <th>Bei Überschreitung</th>
    </tr>
    <tr>
        <td>Anmeldeversuche durch einen Benutzer</td>
        <td>5 pro Minute</td>
        <td>Benutzer kann sich für 1 Minute nicht anmelden.</td>
    </tr>
    <tr>
        <td>Benutzerprofilattribute aktualisieren</td>
        <td>5 pro Minute</td>
        <td>Benutzer kann für 1 Minute keine Aktualisierung ausführen.</td>
    </tr>
        <td>Benutzerprofilattribute löschen</td>
        <td>5 pro Minute</td>
        <td>Benutzer kann für 1 Minute keine Aktualisierung ausführen.</td>
    </tr>
</table>



## Cloud Directory
{: #limits-cd}

Überprüfen Sie die folgende Tabelle, um sich mit den Grenzwerten vertraut zu machen, die mit der Verwendung von Cloud Directory verknüpft sind.
{: shortdesc}

<table>
    <tr>
        <th>API</th>
        <th>Konfigurierbar</th>
        <th>Grenzwert</th>
        <th>Bei Überschreitung</th>
    </tr>
    <tr>
        <td>Anmeldeversuche pro Konto</td>
        <td>Ja</td>
        <td>Unbegrenzt</td>
        <td>Alle Anmeldeversuche für die Instanz werden für eine Minute blockiert.</td>
    </tr>
    <tr>
        <td>Registrierungsversuche pro Konto</td>
        <td>Ja</td>
        <td>Unbegrenzt</td>
        <td>Alle Registrierungsversuche für die Instanz werden für eine Minute blockiert.</td>
    </tr>
    <tr>
        <td>E-Mail-Sendeanforderung</td>
        <td>Nein</td>
        <td>10 E-Mails in 10 Minuten pro Benutzer</td>
        <td>E-Mail-Anforderungen für den Benutzer werden für 30 Minuten blockiert.</td>
    </tr>
</table>

Weitere Informationen finden Sie in <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateRateLimitConfig" target="_blank">API für Rate Limiting-Management</a>.
