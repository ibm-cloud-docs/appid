---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-31"

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

Con Cloud Directory, puoi gestire i tuoi utenti in un registro scalabile utilizzando una funzionalità predefinita che migliora la sicurezza e il self service.
{: shortdesc}

Un utente Cloud Directory non è la stessa cosa di un utente {{site.data.keyword.appid_short_notm}}. Gli utenti possono registrarsi per la tua applicazione utilizzando le diverse opzioni del provider di identità da te configurate oppure puoi aggiungerli alla tua directory. Gli utenti menzionati in questo argomento sono quelli associati a Cloud Directory con un provider di identità.
{: note}

## Visualizzazione delle informazioni sull'utente
{: #cd-user-info}

Puoi visualizzare tutte le informazioni note su tutti i tuoi utenti Cloud Directory come un oggetto JSON utilizzando le API o il dashboard.
{: shortdesc}


### Con la GUI

Puoi utilizzare il dashboard {{site.data.keyword.appid_short_notm}} per visualizzare i dettagli sui tuoi utenti dell'applicazione. 

1. Passa alla scheda **Cloud Directory > Users** della tua istanza {{site.data.keyword.appid_short_notm}}.

2. Sfoglia la tabella o ricerca utilizzando un indirizzo email per trovare l'utente per cui vuoi visualizzare le informazioni.

3. Nel menu di overflow nella riga dell'utente, fai clic su **View user details**. Si apre una pagina che contiene le informazioni dell'utente. Consulta la seguente tabella per vedere quali informazioni puoi visualizzare. 

<table>
  <tr>
    <th colspan="2">Dettagli utente </th>
  </tr>
  <tr>
    <td>Identificativo utente</td>
    <td>L'identificativo utente dipende dal tipo di registrazione utente che hai configurato. Se hai configurato un flusso di email e password, l'identificativo è l'email dell'utente. Se utilizzi il flusso di nome utente e password, l'identificativo è il nome utente fornito alla registrazione.</td>
  </tr>
  <tr>
    <td>Email</td>
    <td>L'indirizzo email primario collegato all'utente.</td>
  </tr>
    <tr>
    <td>Nome e cognome</td>
    <td>Il nome e il cognome del tuo utente come sono stati forniti durante il processo di registrazione.</td>
  </tr>
  <tr>
    <td>Ultimo accesso</td>
    <td>La data/ora dell'ultima volta in cui l'utente ha eseguito l'accesso alla tua applicazione. Nota: se hai aggiunto il tuo utente tramite il dashboard, l'accesso è vuoto finché l'utente stesso non accede alla tua applicazione. Quando si verifica l'accesso diventano anche un utente App ID.</td>
  </tr>
  <tr>
    <td>ID</td>
    <td>L'ID assegnato all'utente da {{site.data.keyword.appid_short_notm}}. Nell'IU, non viene mostrato ma puoi copiare il valore e incollarlo in un editor di testo per visualizzarlo.</td>
  </tr>
  <tr>
    <td>Attributi predefiniti</td>
    <td>Gli attributi predefiniti sono le cose note su un utente basato su SCIM.</td>
  </tr>
  <tr>
    <td>Attributi personalizzati</td>
    <td>Gli attributi personalizzati sono ulteriori informazioni che vengono aggiunte al profilo o che vengono apprese sull'utente quando interagisce con la tua applicazione.</td>
  </tr>
  <tr>
    <td>Riepilogo</td>
    <td>Tutti gli attributi vengono compilati per formare un profilo che ti fornisce una panoramica completa sul tuo utente Cloud Directory. Per ulteriori informazioni, vedi [profili utente](/docs/services/appid?topic=appid-profiles).</td>
  </tr>
</table>

</br>

### Con l'API

Puoi utilizzare l'API {{site.data.keyword.appid_short_notm}} per visualizzare i dettagli sui tuoi utenti dell'applicazione. 

1. Ottieni il tuo ID tenant dalla tua istanza del servizio.

2. Cerca i tuoi utenti App ID con una query di identificazione, ad esempio un indirizzo email, per trovare l'ID utente.

  ```
  curl -X GET "https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/cloud_directory/Users?query={identifying-search-query}" -H "accept: application/json" -H "authorization: Bearer {token}"
  ```
  {: codeblock}

  Esempio:

  ```
  curl -X GET https://us-south.appid.cloud.ibm.com/management/v4/e19a2778-3262-4986-8875-8khjafsdkhjsdafkjh/cloud_directory/Users?query=example@email.com -H "accept: application/json" -H "authorization: Bearer eyJraWQiOiIyMDE3MTEyOSIsImFsZ...."
  ```
  {: screen}

3. Utilizzando l'ID ottenuto nel passo precedente, effettua una richiesta GET all'endpoint `cloud_directory/users` per vedere il profilo utente completo.

  ```
  curl -X GET "https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/cloud_directory/Users/{user-ID}" -H "accept: application/json" -H "authorization: Bearer {token}"
  ```
  {: codeblock}

  Risposta di esempio:

  ```
  {
    sub: "c155c0ff-337a-46d3-a22a-a8f2cca08995",
    name: "Test User",
    email: "testuser@test.com",
    identities: [
      {
        provider: "cloud_directory",
        id: "f1772fcc-ff70-4d88-81a0-07dd7a3d988f",
        idpUserInfo: {
          displayName: "Test User",
          active: true,
          mfaContext: {},
          emails: [
            {
              value: "testuser@test.com",
              primary: true
            }
          ],
          meta: {
            lastLogin: "2019-05-20T16:33:20.699Z",
            created: "2019-05-20T16:25:13.019Z",
            location: "/v1/6b8ab644-1d4a-4b3e-bcd9-777ba8430a51/Users/f1772fcc-ff70-4d88-81a0-07dd7a3d988f",
            lastModified: "2019-05-20T16:33:20.707Z",
            resourceType: "User"
          },
          scemas: [
            "urn:ietf:params:scim:schemas:core:2.0:User"
          ],
          name: {
            givenName: "Test",
            familyName: "User",
            formatted: "Test User"
            },
          id: "f1772fcc-ff70-4d88-81a0-07dd7a3d988f",
          status: "CONFIRMED",
          idpType: "cloud_directory"
        }
      }
    ]
  }
  ```
  {: screen}

  Per visualizzare l'insieme di dati completo di un utente supportato da {{site.data.keyword.appid_short_notm}}, consulta [lo schema standard di SCIM](https://tools.ietf.org/html/rfc7643#section-8.2).
  {: tip}


## Aggiunta ed eliminazione di utenti
{: #add-delete-users}

Puoi gestire i tuoi utenti Cloud Directory mediante il dashboard {{site.data.keyword.appid_short_notm}} oppure utilizzando le API.
{: shortdesc}

Quando un utente si registra alla tua applicazione, lo fa tramite un flusso di lavoro self service che attiva automaticamente le email come ad esempio il benvenuto e una richiesta di verifica. Quando tu, come amministratore, aggiungi un utente alla tua applicazione, non viene avviato un flusso di lavoro self service, il che significa che gli utenti non ricevono alcuna email dalla tua applicazione. Se vuoi che i tuoi utenti siano ancora avvertiti quando vengono aggiunti, puoi attivare i flussi di messaggistica tramite l'[API di gestione App ID](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.set_cloud_directory_email_dispatcher).


### Aggiunta di utenti
{: #add-users}

Quando un utente si registra alla tua applicazione, viene aggiunto come un utente. Per scopi di test, puoi aggiungere un utente mediante il dashboard {{site.data.keyword.appid_short_notm}} o utilizzando l'API.

Se disabiliti la registrazione self service o aggiungi un utente per suo conto, l'utente non riceve un'email di benvenuto o di verifica quando viene aggiunto.
{: tip}



**Per aggiungere un nuovo utente con la GUI:**

1. Passa alla scheda **Cloud Directory > Users** del dashboard {{site.data.keyword.appid_short_notm}}.

2. Fai clic su **Add user**. Viene visualizzato un modulo.

3. Immetti dei valori per **First name**, **Last name**, **Email** e **Password**. Assicurati che l'email che tenti di registrare non sia già stata presa da un altro utente. Assicurati di avere digitato la tua password correttamente confermandola immettendola nel campo **Re-enter Password**.

4. Fai clic su **Save**. Viene creato un utente Cloud Directory.

</br>


**Per aggiungere un nuovo utente con l'API:**

Il seguente flusso mostra come aggiungere un utente con un'email e una password. Puoi anche scegliere di utilizzare un flusso di nome utente e password.

1. Ottieni il tuo ID tenant (`tenantID`) dalla tua applicazione o dalle tue credenziali del servizio.

2. Ottieni un token IAM {{site.data.keyword.cloud_notm}}.

  ```
  curl --X GET "https://iam.cloud.ibm.com/oidc/token" -H "accept: application/x-www-form-urlencoded"
  ```
  {: codeblock}

3. Con il token ottenuto nel passo 2, effettua una richiesta POST all'endpoint `cloud-directory/users`. Tieni presente che questo esempio utilizza il flusso email/ password. Puoi anche utilizzare il flusso nome utente/ password.

  ```
  curl --X POST "https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/cloud_directory/Users"
  -H "accept: application/json"
  -H "content-type: application/json"
  -H "authorization: Bearer {token}"
  -d {
    "displayName": "Test User",
    "password": "{App-ID-Cloud-Directory-User-Password}",
    "active": true,
    "emails": [
      {
        "value": "{App-ID-Cloud-Directory-User-Email}",
        "primary": true
      }
    ]
  }
  ```
  {: codeblock}

</br>


### Eliminazione di utenti
{: #delete-users}

Se vuoi rimuovere un utente dalla tua directory, puoi eliminarlo dalla GUI o utilizzando le API.
{: shortdesc}

**Per eliminare un utente tramite la GUI:**

1. Passa alla scheda **Cloud Directory > Users** del dashboard {{site.data.keyword.appid_short_notm}}.

2. Fai clic sulla casella di spunta accanto all'utente che vuoi eliminare. Viene visualizzata una casella.

3. Nella casella, fai clic su **Delete**. Viene visualizzata una schermata.

4. Conferma che comprendi che l'eliminazione di un utente non può essere annullata facendo clic su **Delete**. Se l'azione è stato un errore, puoi aggiungere nuovamente l'utente alla tua directory ma tutte le informazioni su tale utente non saranno più disponibili.

</br>

**Per eliminare un utente utilizzando l'API:**

1. Ottieni il tuo ID tenant.

2. Utilizzando l'email collegata all'utente, cerca nella tua directory per trovare l'ID dell'utente.

  ```
  curl -X GET "https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/users?email={user-email}" -H "accept: application/json"
  ```
  {: codeblock}

3. Elimina l'utente.

  ```
  curl --X DELETE "https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/cloud_directory/Users/{user-GUID}"
  -H "accept: application/x-www-form-urlencoded"
  ```
  {: codeblock}



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
    <td>Assicurati di avere le autorizzazioni da <code>manager</code> prima di ottenere il token. Per un aiuto nell'ottenimento del token IAM, consulta <a href="/docs/iam?topic=iam-iamtoken_from_apikey#iamtoken_from_apikey" target="_blank">la documentazione <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>.</td>
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
