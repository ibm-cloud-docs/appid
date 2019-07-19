---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-09"

keywords: Authentication, authorization, identity, app security, secure, access, platform, management, permissions

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


# Gestione dell'accesso al servizio
{: #service-access-management}

Con {{site.data.keyword.appid_full}} e {{site.data.keyword.cloud_notm}} IAM (Identity and Access Management), i proprietari dell'account possono gestire l'accesso degli utenti nel tuo account.
{: shortdesc}

Come proprietario dell'account, puoi impostare delle politiche all'interno del tuo account per creare diversi livelli di accesso per i vari utenti. Ad esempio, alcuni utenti possono avere accesso in **Sola lettura** a un'istanza, ma l'accesso in **Scrittura** a un'altra. Puoi decidere chi è autorizzato a creare, aggiornare ed eliminare le istanze di {{site.data.keyword.appid_short_notm}}.

Per ulteriori informazioni su IAM, vedi [Accesso IAM](/docs/iam?topic=iam-userroles).

## Ruoli utente
{: #iam-roles}

L'ambito di una politica di accesso si basa su un ruolo assegnato agli utenti.
{: shortdesc}

Le politiche consentono di concedere l'accesso a diversi livelli. Alcune delle opzioni includono:
<ul><ul>
  <li>Accesso a tutte le istanze del servizio nel tuo account</li>
  <li>Accesso alle istanze di un singolo servizio nel tuo account</li>
  <li>Accesso a una risorsa specifica all'interno di un'istanza</li>
  <li>Accesso a tutti i servizi abilitati a IAM nel tuo account</li>
</ul></ul>

### Ruoli della piattaforma
{: #iam-platform-roles}

I ruoli di gestione della piattaforma consentono agli utenti di eseguire attività sulle risorse del servizio a livello di piattaforma. Ad esempio, è possibile assegnare ruoli per determinare chi può creare o eliminare ID, creare istanze e associare le istanze alle applicazioni. La seguente tabella descrive le azioni correlate ai ruoli di gestione della piattaforma.

<table>
  <tr>
    <th>Ruolo piattaforma</th>
    <th>Autorizzazioni</th>
    <th>Azioni di esempio</th>
  </tr>
  <tr>
    <td><i>Visualizzatore</i></td>
    <td>Visualizza le istanze {{site.data.keyword.appid_short_notm}}.</td>
    <td>Puoi vedere i dati di un utente Cloud Directory o la configurazione del provider di identità.</td>
  </tr>
  <tr>
    <td><i>Editor</i></td>
    <td>Visualizza e associa le istanze {{site.data.keyword.appid_short_notm}}.</td>
    <td>Puoi associare le applicazioni a un'istanza di {{site.data.keyword.appid_short_notm}}.</td>
  </tr>
  <tr>
    <td><i>Operatore</i></td>
    <td>Crea, elimina, modifica, sospendi, riprendi, visualizza o associa le istanze {{site.data.keyword.appid_short_notm}}.</td>
    <td>Puoi creare o eliminare un'istanza {{site.data.keyword.appid_short_notm}} dal catalogo.</td>
  </tr>
  <tr>
    <td><i>Amministratore</i></td>
    <td>Tutte le azioni di gestione per ogni servizio nell'account.</td>
    <td>Puoi eseguire tutte le azioni dell'operatore e hai la possibilità di assegnare politiche ad altri utenti.</td>
  </tr>
</table>

### Ruoli di accesso al servizio
{: #iam-service-roles}
La seguente tabella descrive le azioni associate ai ruoli di accesso al servizio. I ruoli di accesso al servizio consentono agli utenti di accedere a {{site.data.keyword.appid_short_notm}} nonché la possibilità di richiamare l'API {{site.data.keyword.appid_short_notm}}.


<table>
  <tr>
    <th>Ruolo servizio</th>
    <th>Autorizzazioni</th>
    <th>Azioni di esempio</th>
  </tr>
  <tr>
    <td><i>Lettore</i></td>
    <td>Visualizza i dati dell'istanza {{site.data.keyword.appid_short_notm}}.</td>
    <td>Puoi visualizzare i dettagli dell'istanza del servizio come dati utente o informazioni sul provider di identità.</td>
  </tr>
  <tr>
    <td><i>Scrittore o Gestore</i></td>
    <td>Visualizza e modifica un'istanza {{site.data.keyword.appid_short_notm}}.</td>
    <td>Puoi eseguire tutte le azioni del Lettore e modificare l'istanza del servizio, ad esempio modificare la configurazione del provider di identità. </li></ul></td>
  </tr>
</table>

Per ulteriori informazioni sull'assegnazione dei ruoli utente nell'IU, vedi [Gestione dell'accesso IAM](/docs/iam?topic=iam-iammanidaccser#iammanidaccser).


## Politiche di accesso {{site.data.keyword.appid_short_notm}}
{: #iam-access}

Ad ogni utente che accede al servizio {{site.data.keyword.appid_short_notm}} nel tuo account deve essere assegnato una politica di accesso con un ruolo utente IAM definito. Tale politica determina quali azioni l'utente può eseguire nel contesto del servizio o dell'istanza che selezioni.
{: shortdesc}

Le azioni sono personalizzate e definite dal servizio {{site.data.keyword.cloud_notm}} come operazioni che possono essere eseguite nel servizio. Le azioni vengono quindi associate ai ruoli utente IAM. Alcune delle azioni intraprese possono tracciare il servizio {{site.data.keyword.cloudaccesstrailshort}}. Nella seguente tabella, vengono associate le azioni e le autorizzazioni richieste per {{site.data.keyword.appid_short_notm}}.

<table>
  <tr>
    <th>Azione</th>
    <th>Spiegazione</th>
    <th>Ruolo richiesto</th>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-redirect-uris</code></td>
    <td>Visualizza gli URL di reindirizzamento dopo l'autenticazione.</td>
    <td>Lettore, Scrittore, Gestore</td>
  </tr>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-redirect-uris</code></td>
    <td>Aggiungi o aggiorna gli URL di reindirizzamento dopo l'autenticazione.</td>
    <td>Scrittore, Gestore</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-idps</code></td>
    <td>Aggiorna la configurazione del tuo provider di identità.</td>
    <td>Scrittore, Gestore</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-idps</code></td>
    <td>Visualizza la configurazione del tuo provider di identità.</td>
    <td>Lettore, Scrittore, Gestore</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-recent-activities</code></td>
    <td>Visualizza tutti i recenti eventi di autenticazione come elenco.</td>
    <td>Lettore, Scrittore, Gestore</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-ui-config</code></td>
    <td>Visualizza la configurazione del widget di accesso, come logo e colori.</td>
    <td>Lettore, Scrittore, Gestore</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-ui-config</code></td>
    <td>Aggiorna la configurazione del widget di accesso.</td>
    <td>Scrittore, Gestore</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-user-profile-config</code></td>
    <td>Visualizza la configurazione del profilo utente.</td>
    <td>Lettore, Scrittore, Gestore</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-user-profile-config</code></td>
    <td>Modifica la configurazione del profilo utente.</td>
    <td>Scrittore, Gestore</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-cd-users</code></td>
    <td>Visualizza la configurazione del profilo utente.</td>
    <td>Lettore, Scrittore, Gestore</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-add-cd-user</code></td>
    <td>Aggiungi nuovi utenti a Cloud Directory.</td>
    <td>Scrittore, Gestore</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-cd-user</code></td>
    <td>Aggiorna i dettagli di un utente Cloud Directory.</td>
    <td>Scrittore, Gestore</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-delete-cd-user</code></td>
    <td>Elimina un utente da Cloud Directory.</td>
    <td>Scrittore, Gestore</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-email-template</code></td>
    <td>Visualizza i template di email di Cloud Directory.</td>
    <td>Lettore, Scrittore, Gestore</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-update-email-template</code></td>
    <td>Aggiorna il template di email con il tuo contenuto.</td>
    <td>Scrittore, Gestore</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-delete-email-template</code></td>
    <td>Elimina un template di email di Cloud Directory.</td>
    <td>Scrittore, Gestore</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-saml-metadata</code></td>
    <td>Visualizza i metadati del SP (service provider) SAML della directory cloud.</td>
    <td>Lettore, Scrittore, Gestore</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-post-saml-logo</code></td>
    <td>Imposta o aggiorna l'immagine nel widget di accesso per il provider di identità SAML.</td>
    <td>Scrittore, Gestore</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-send-email-cd</code></td>
    <td>Invia un'email a un utente in base a un template.</td>
    <td>Scrittore, Gestore</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-sender-details-cd</code></td>
    <td>Visualizza i dettagli del mittente per l'email.</td>
    <td>Lettore, Scrittore, Gestore</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-sender-details-cd</code></td>
    <td>Aggiorna i dettagli del mittente.</td>
    <td>Scrittore, Gestore</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-revoke-refresh-token</code></td>
    <td>Revoca il token di aggiornamento di un utente con il relativo ID utente.</td>
    <td>Scrittore, Gestore</td>
  </tr>
</table>

</br>

## Esempio: concedere a un altro utente l'accesso a un'istanza di {{site.data.keyword.appid_short_notm}}
{: #iam-example}

In questo scenario, un amministratore ha creato un'istanza di {{site.data.keyword.appid_short_notm}} e deve concedere l'accesso di visualizzatore a un altro membro del team.
{: shortdesc}

Prima di cominciare:

* Installa la [CLI {{site.data.keyword.cloud_notm}}](/docs/cli?topic=cloud-cli-getting-started).

Per aggiornare le autorizzazioni di accesso, l'amministratore completa la seguente procedura:

1. Accedi alla console {{site.data.keyword.cloud_notm}}.

2. Concedi al dipendente l'accesso di visualizzazione seguendo le istruzioni illustrate nella [documentazione IAM](/docs/iam?topic=iam-iammanidaccser).

3. Passa alla scheda **Credenziali del servizio** del dashboard {{site.data.keyword.appid_short_notm}}. Fai clic su **Visualizza credenziali** e copia il **tentantID**.

4. Accedi con la CLI {{site.data.keyword.cloud_notm}} nel tuo terminale.

    ```
    ibmcloud login -api -a https://api.{region}.cloud.ibm.com
    ```
    {: codeblock}

    <table>
      <tr>
        <th>Regione</th>
        <th>Endpoint</th>
      </tr>
      <tr>
        <td>Dallas</td>
        <td><code>us-south</code></td>
      </tr>
      <tr>
        <td>Francoforte</td>
        <td><code>eu-de</code></td>
      </tr>
      <tr>
        <td>Sydney</td>
        <td><code>au-syd</code></td>
      </tr>
      <tr>
        <td>Londra</td>
        <td><code>eu-gb</code></td>
      </tr>
      <tr>
        <td>Tokyo</td>
        <td><code>jp-tok</code></td>
      </tr>
    </table>

5. Ottieni un token IAM e prendine nota.

    ```
    ibmcloud iam oauth-tokens
    ```
    {: codeblock}

6. Verifica che il membro del team non possa apportare modifiche.

    ```
    curl -X PUT --header 'Content-Type: application/json' \
    --header 'Accept: application/json' \
    --header 'Authorization: <IAM token value>' \
    -d '{
     "isActive": false,
     "config": {
       "idpId": "appID",
       "secret": "appsecret"
     }
    }' \
    'https://{region}.appid.cloud.ibm.com/management/v4/{tenant-ID}/config/idps/facebook'
    ```
    {: codeblock}

    Il risultato è un messaggio 403 non autorizzato.

Per visualizzare la configurazione di {{site.data.keyword.appid_short_notm}} dalla CLI, il membro del team completa la seguente procedura:

1. Esegui l'accesso utilizzando la CLI {{site.data.keyword.cloud_notm}} nel tuo terminale.

    ```
    ibmcloud login -a api.<region>.console.cloud.ibm.com
    ```
    {: codeblock}

2. Ottieni un token IAM e prendine nota.

    ```
    ibmcloud iam oauth-tokens
    ```
    {: codeblock}

3. Visualizza la configurazione del provider di identità per Facebook utilizzando cURL.

    ```
    curl -X GET --header 'Accept: application/json' --header 'Authorization: <IAM token value>' \  'https://us-south.appid.cloud.ibm.com/management/v4/<tenant-ID>/config/idps/facebook'
    ```
    {: codeblock}

    Il risultato è un messaggio 200 che contiene le informazioni sul provider di identità.

