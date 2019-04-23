---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

keywords: authentication, authorization, identity, app security, secure, directory, registry, passwords, languages, lockout

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


# Gestione degli utenti
{: #cd-users}

Quando abiliti Cloud Directory, gli utenti possono registrarsi per la tua applicazione utilizzando una email o un nome utente e una password.
{: shortdesc}


Un utente Cloud Directory non è la stessa cosa di un utente {{site.data.keyword.appid_short_notm}}. Gli utenti possono registrarsi per la tua applicazione utilizzando le diverse opzioni del provider di identità da te configurate. Gli utenti menzionati in questo argomento sono quelli che hanno scelto di utilizzare l'opzione Cloud Directory per la registrazione per la tua applicazione.
{: note}


## Aggiunta ed eliminazione di utenti
{: #add-delete-users}

Puoi gestire i tuoi utenti Cloud Directory mediante il dashboard {{site.data.keyword.appid_short_notm}} oppure utilizzando le API.
{: shortdesc}

Per visualizzare i dati completi per un utente specifico, puoi utilizzare le API per restituire le informazioni di un utente di Cloud Directory come un oggetto JSON. Per visualizzare l'insieme di dati completo di un utente supportato da {{site.data.keyword.appid_short_notm}}, consulta [lo schema standard di SCIM](https://tools.ietf.org/html/rfc7643#section-8.2).

### Aggiunta di utenti
{: #add-users}

Puoi utilizzare la seguente procedura per aggiungere un utente mediante il dashboard {{site.data.keyword.appid_short_notm}}.

Per scopi di test, puoi aggiungere un utente mediante il dashboard {{site.data.keyword.appid_short_notm}}.

1. Passa alla scheda **Cloud Directory > Users** del dashboard {{site.data.keyword.appid_short_notm}}.

2. Fai clic su **Add user**. Viene visualizzato un modulo.

3. Immetti dei valori per **First name**, **Last name**, **Email** e **Password**. Assicurati che l'email che tenti di registrare non sia già stata presa da un altro utente. Assicurati di avere digitato la tua password correttamente confermandola immettendola nel campo **Re-enter Password**.

4. Fai clic su **Save**. Viene creato un utente Cloud Directory.


### Eliminazione di utenti
{: #delete-users}

Se vuoi rimuovere un utente dalla tua directory, puoi eliminarlo dalla GUI.

1. Passa alla scheda **Cloud Directory > Users** del dashboard {{site.data.keyword.appid_short_notm}}.

2. Fai clic sulla casella di spunta accanto all'utente che vuoi eliminare. Viene visualizzata una casella.

3. Nella casella, fai clic su **Delete**. Viene visualizzata una schermata.

4. Conferma che comprendi che l'eliminazione di un utente non può essere annullata facendo clic su **Delete**. Se l'azione è stato un errore, puoi aggiungere nuovamente l'utente alla tua directory ma tutte le informazioni su tale utente non saranno più disponibili.


## Migrazione di utenti
{: #user-migration}

Occasionalmente potresti dover configurare una nuova istanza di {{site.data.keyword.appid_short_notm}}. Se stai utilizzando Cloud Directory, questo significa che i tuoi utenti devono essere migrati alla nuova istanza. Puoi utilizzare le API di gestione per aiutarti con la migrazione.
{: shortdesc}


Devi avere assegnato il [ruolo IAM](/docs/iam?topic=iam-getstarted#getstarted) di `Gestore` per entrambe le istanze di {{site.data.keyword.appid_short_notm}}.
{: note}


### Esportazione
{: cd-export}

Prima di poter aggiungere i tuoi utenti alla nuova istanza, devi esportarli dalla tua istanza corrente. Per farlo, puoi utilizzare l'<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryExport" target="_blank">API di gestione dell'esportazione <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>.

Comando cURL di esempio:

```
curl -X GET --header ‘Accept: application/json’ --header ‘Authorization: Bearer <iam-token>’ ’https://us-south.appid.cloud.ibm.com/management/v4/111c9bj3-xxxx-4b5b-zzzz-24ad9440k8j9/cloud_directory/export?encryption_secret=myCoolSecret'
```
{: codeblock}

<table>
  <tr>
    <th>Variabile</th>
    <th>Descrizione</th>
  </tr>
  <tr>
    <td><code>encryption_secret</code></td>
    <td>Una stringa personalizzata utilizzata per codificare e decodificare una password con hash degli utenti.</td>
  </tr>
  <tr>
    <td><code>tenantID</code></td>
    <td>L'ID tenant del servizio può essere trovato nelle tue credenziali del servizio. Puoi trovare le tue credenziali di servizio nel dashboard {{site.data.keyword.appid_short_notm}}.</td>
  </tr>
</table>

Vengono restituiti solo i tuoi utenti Cloud Directory e i loro profili. Gli utenti da altri provider di identità non vengono restituiti.
{: note}


### Importazione
{: #cd-import}

Ora che i tuoi utenti sono pronti, puoi importare le loro informazioni nella nuova istanza. Per farlo, puoi utilizzare l'<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryImport" target="_blank">API di gestione dell'importazione <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>.


Comando cURL di esempio:

```
curl -X POST --header ‘Content-Type: application/json’ --header ‘Accept: application/json’ --header ‘Authorization: Bearer <iam-token>’ -d ‘{“users”: [
    {
      “scimUser”: {
        “originalId”: “3f3f6779-7978-4383-926f-a43aef3b724b”,
        “name”: {
          “givenName”: “<first-name>”,
          “familyName”: “<last-name>”,
          “formatted”: “<first-name> <last-name>”
        },
        “displayName”: “<first-name>”,
        “emails”: [
          {
            “value”: “<user>@gmail.com”,
            “primary”: true
          }
        ],
        “status”: “PENDING”
      },
      “passwordHash”: “<password hash here>“,
      “passwordHashAlg”: “<password hash algorithm>",
      “profile”: {
        “attributes”: {}
      }
    }
]}’ ‘https://us-south.appid.cloud.ibm.com/management/v4/111c9bj3-xxxx-4b5b-zzzz-24ad9440k8j9/cloud_directory/import?encryption_secret=myCoolSecret’
```
{: codeblock}



### Script di migrazione
{: cd-migration-script}

{{site.data.keyword.appid_short_notm}} fornisce uno script di migrazione che puoi utilizzare tramite la CLI per velocizzare il processo di migrazione.

Prima di iniziare, assicurati di avere le seguenti informazioni sui parametri:

<table>
  <tr>
    <th>Parametro</th>
    <th>Descrizione</th>
  </tr>
  <tr>
    <td><code>sourceTenantId</code></td>
    <td>L'ID tenant dell'istanza di {{site.data.keyword.appid_short_notm}} da cui vuoi esportare gli utenti.</td>
  </tr>
  <tr>
    <td><code>destinationTenantId</code></td>
    <td>L'ID tenant dell'istanza di {{site.data.keyword.appid_short_notm}} in cui vuoi importare gli utenti.</td>
  </tr>
  <tr>
    <td>Regione</td>
    <td>Le opzioni di regione includono: <code>au-syd</code>, <code>eu-de</code>, <code>eu-gb</code>, <code>jp-tok</code> e <code>us-south</code>.</td>
  </tr>
  <tr>
    <td>Token IAM</td>
    <td>Assicurati di avere le autorizzazioni da <code>manager</code> prima di ottenere il token. Per un aiuto nell'ottenimento del token IAM, consulta <a href="https://cloud.ibm.com/docs/iam/apikey_iamtoken.html#iamtoken_from_apikey" target="_blank">la documentazione <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>.</td>
  </tr>
</table>

Per eseguire lo script:

1. Clona il <a href="https://github.com/ibm-cloud-security/appid-sample-code-snippets/tree/master/export-import-cloud-directory-users" target="_blank">repository <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>.
2. Apri il terminale e passa alla cartella in cui hai clonato il repository.
3. Immetti il seguente comando.

  ```
  npm install
  ```
  {: codeblock}

4. Con i tuoi parametri, immetti il seguente comando:

  ```
  users_export_import 'sourceTenantId' 'destinationTenantId' 'region' 'iamToken'
  ```
  {: codeblock}

  Comando di esempio:

  ```
  users_export_import e00a0366-53c5-4fcf-8fef-ab3e66b2ced8 73321c2b-d35a-497a-9845-15c580fdf58c ng eyJraWQiOiIyMDE3MTAyNS0xNjoyNzoxMCIsImFsZyI6IlJTMjU2In0.eyJpYW1faWQiOiJJQk1pZC0zMTAwMDBUNkZTIiwiaWQiOiJJQk1pZC0zMTAwMDBUNkZTIiwicmVhbG1pZCI6IklCTWlkIiwiaWRlbnRpZmllciI6IjMxMDAwIFQ2RlMiPCJnaXZlbl9uYW1lIjoiUm90ZW0iLCJmYW1pbHlfbmFtZSI6IkJyb3NoIiwibmFtZSI6IlJvdGVtIEJyb3NoIiwiZW1haWwiOiJyb3RlbWJyQGlsLmlibS5jb20iLCJzdWIiOiJyb3RlbWJyQGlsLmlibS5jb20iLCJhY2NvdW50Ijp7ImJzcyI6ImQ3OWM5YTk5NjJkYzc2Y2JkMDZlYTVhNzhjMjY0YzE5In0sImlhdCI6MTUzNrE3Mjg4NCwiZXhwIjoxNTM3MTc2NDg0LCJpc3MiOiJodHRwczovL2lhbS5zdGFnZTEuYmx1ZW1peC5uZXQvaWRlbnRpdHkiLCJncmFudF90eXBlIjoidXJuOmlibTpwYXJhbXM6b2F1dGg6Z3JhbnQtdHlwZTpwYXNzY29kZSIsInNjb3BlIjoiaWJtIG9wZW5pZCIsImNsaWVudF9pZCI6ImJ4IiwiYWNyIjoxLCJhbXIiOlsicHdkIl19.c4vLPzhvvNZLjaLy7znDa37qV4o-yuGmSKmJoQKrEQNZU8IC0NIjxwSo7W9kb0pDi3Yf_03_9ufTTGNfjtltzNWycSXjkNgoL-b9_nU61oHdgn0stY1KmNicqyBWfgUU--4xa904QN_QjRHBaUBeJf3XWEphPIMoF7mZeOxEZLnCMcQXSz9pImCMiP4SNT38cHLiI90Yx01rM7hpteepWULh5MYh-B2V03Gkgxfqvv951HF1LDg6eT4Q9in11laTQKtKuomripUju_4GIIjORVYw9NaAVKIJ9lKrPX0SKPhStsa59qGsC_7Uersms5EY1W1VbZVqOZPJbtp6tVf-Lw
  ```
  {: codeblock}
