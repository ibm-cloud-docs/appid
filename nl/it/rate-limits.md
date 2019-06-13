---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-06"

keywords: Authentication, authorization, identity, app security, secure, rates, cloud directory, rate limit, attempts

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


# Limiti di App ID
{: #limits}

La limitazione della frequenza viene utilizzata per controllare la quantità di traffico in entrata e in uscita tramite la tua istanza di App ID. Limitando le richieste o le risorse, puoi proteggere le tue applicazioni.
{: shortdesc}

## Piano Lite di App ID 
{: #lite-limits}

Controlla la seguente tabella per vedere i limiti in atto per le istanze del piano Lite di App ID. 

<table>
    <tr>
        <th>Risorsa </th>
        <th>Massimo</th>
    </tr>
    <tr>
        <td>Utenti</td>
        <td>1000</td>
    </tr>
    <tr>
        <td>Autenticazioni</td>
        <td>1000 al mese</td>
    </tr>
</table>

## Generale 
{: #general-limits}

La seguente tabella elenca i limiti massimi per utente per le risorse IBM Cloud App ID e il periodo di blocco quando vengono superati i limiti. Questi limiti si applicano a tutti gli utenti che possono creare le risorse IBM Cloud App ID.
{: shortdesc}

<table>
    <tr>
        <th>API</th>
        <th>Limite</th>
        <th>Quando superato</th>
    </tr>
    <tr>
        <td>Tentativi di accesso per un utente</td>
        <td>5 al minuto</td>
        <td>L'utente non può accedere per 1 minuto.</td>
    </tr>
    <tr>
        <td>Aggiornamento degli attributi del profilo utente</td>
        <td>5 al minuto</td>
        <td>L'utente non può aggiornare il profilo per 1 minuto.</td>
    </tr>
        <td>Eliminazione degli attributi del profilo utente</td>
        <td>5 al minuto</td>
        <td>L'utente non può aggiornare il profilo per 1 minuto.</td>
    </tr>
</table>



## Cloud Directory
{: #limits-cd}

Controlla la seguente tabella per vedere i limiti associati a Cloud Directory.
{: shortdesc}

<table>
    <tr>
        <th>API</th>
        <th>Configurabile </th>
        <th>Limite</th>
        <th>Quando superato</th>
    </tr>
    <tr>
        <td>Tentativi di accesso account</td>
        <td>Sì</td>
        <td>Illimitati</td>
        <td>Tutti i tentativi di accesso all'istanza vengono bloccati per un minuto.</td>
    </tr>
    <tr>
        <td>Tentativi di registrazione account</td>
        <td>Sì</td>
        <td>Illimitati</td>
        <td>Tutti i tentativi di registrazione all'istanza vengono bloccati per un minuto.</td>
    </tr>
    <tr>
        <td>Richiesta di invio email</td>
        <td>No</td>
        <td>10 email in 10 minuti per utente</td>
        <td>Le richieste email per l'utente vengono bloccate per 30 minuti.</td>
    </tr>
</table>

Per ulteriori informazioni, vedi l'<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateRateLimitConfig" target="_blank">API di gestione del limite di frequenza</a>
