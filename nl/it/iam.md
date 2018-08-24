---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# Gestione dell'accesso al servizio
{: #service-access-management}

Con l'account {{site.data.keyword.appid_full}} e {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM), i proprietari possono gestire l'accesso degli utenti nel tuo account.
{: shortdesc}

Come proprietario dell'account, puoi impostare delle politiche all'interno del tuo account per creare diversi livelli di accesso per i vari utenti. Ad esempio, alcuni utenti possono avere accesso in **Sola lettura** a un'istanza, ma l'accesso in **Scrittura** a un'altra. Puoi decidere chi è autorizzato a creare, aggiornare ed eliminare le istanze di {{site.data.keyword.appid_short_notm}}.

Per ulteriori informazioni su IAM, vedi [Accesso IAM](/docs/iam/users_roles.html).

## Ruoli utente
{: #roles}

L'ambito di una politica di accesso si basa su un ruolo assegnato agli utenti.
{: shortdesc}

Le politiche consentono di concedere l'accesso a diversi livelli. Alcune delle opzioni includono:
<ul><ul>
  <li>Accesso a tutte le istanze del servizio nel tuo account</li>
  <li>Accesso alle istanze di un singolo servizio nel tuo account</li>
  <li>Accesso a una risorsa specifica all'interno di un'istanza</li>
  <li>Accesso a tutti i servizi abilitati a IAM nel tuo account</li>
</ul></ul>

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

</br>
</br>
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
    <td> <i>Scrittore o Gestore</i></td>
    <td>Visualizza e modifica un'istanza {{site.data.keyword.appid_short_notm}}.</td>
    <td>Puoi eseguire tutte le azioni del Lettore e modificare l'istanza del servizio, ad esempio modificare la configurazione del provider di identità. </li></ul></td>
  </tr>
</table>

Per ulteriori informazioni sull'assegnazione dei ruoli utente nell'IU, vedi [Gestione dell'accesso IAM](/docs/iam/mngiam.html#iammanidaccser).


## Politiche di accesso {{site.data.keyword.appid_short_notm}}
{: #access}

Ad ogni utente che accede al servizio {{site.data.keyword.appid_short_notm}} nel tuo account deve essere assegnato una politica di accesso con un ruolo utente IAM definito. Tale politica determina quali azioni l'utente può eseguire nel contesto del servizio o dell'istanza che selezioni.
{: shortdesc}

Le azioni sono personalizzate e definite dal servizio {{site.data.keyword.Bluemix_notm}} come operazioni che possono essere eseguite nel servizio. Le azioni vengono quindi associate ai ruoli utente IAM. Alcune delle azioni intraprese possono tracciare il servizio {{site.data.keyword.cloudaccesstrailshort}}. Nella seguente tabella, vengono associate le azioni e le autorizzazioni richieste per {{site.data.keyword.appid_short_notm}}.

<table>
  <tr>
    <th>Azione </th>
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

## Traccia delle modifiche alle tue istanze di {{site.data.keyword.appid_short_notm}}
{: #tracking}

Puoi visualizzare, gestire e controllare l'attività di configurazione che viene eseguita nella tua istanza {{site.data.keyword.appid_short_notm}} utilizzando il servizio {{site.data.keyword.cloudaccesstrailshort}}.
{: shortdesc}

Per monitorare l'attività amministrativa:

1. Accedi al tuo account {{site.data.keyword.Bluemix_notm}}.
2. Dal catalogo, esegui il provisioning di un'istanza del servizio {{site.data.keyword.cloudaccesstrailshort}} nello stesso account della tua istanza {{site.data.keyword.appid_short_notm}}.
3. Nel dashboard {{site.data.keyword.cloudaccesstrailshort}}, fai clic sulla scheda **Gestisci**.
4. Dall'elenco a discesa, effettua le seguenti configurazioni per ricercare gli eventi generati da {{site.data.keyword.appid_short_notm}}.
    * Per **View logs**, seleziona **Account logs**.
    * Per **Search**, seleziona **target.Management**.
    * Per **Filter**, immetti **appid**.
5. Fai clic su **Filter**.


Consulta la seguente tabella per un elenco di eventi inviati a {{site.data.keyword.cloudaccesstrailshort}}.

<table>
  <tr>
    <th>Azione </th>
    <th>Descrizione</th>
    <th>Ubicazione IU</th>
  </tr>
  <tr>
    <td><code>read.recentActivity</code></td>
    <td>Visualizza l'attività recente.</td>
    <td>Può essere trovata nella casella <strong>Activity Log</strong> nella scheda <strong>Overview</strong>.</td>
  </tr>
  <tr>
    <td><code>read.idpConfig</code></td>
    <td>Visualizza la configurazione del provider di identità.</td>
    <td>Può essere trovata nella scheda <strong>Identity Providers > Manage</strong>.</td>
  </tr>
  <tr>
    <td><code>update.idpConfig</code></td>
    <td>Aggiorna la configurazione del provider di identità.</td>
    <td>Può essere aggiornata nella scheda <strong>Identity Providers > Manage</strong>.</td>
  </tr>
  <tr>
    <td><code>read.tokensConfig</code></td>
    <td>Visualizza la configurazione della scadenza del token.</td>
    <td>Può essere trovata nella scheda <strong>Identity Providers > Token Expiration</strong>.</td>
  </tr>
  <tr>
    <td><code>read.isProfilesActive</code></td>
    <td>Visualizza la configurazione di archiviazione del profilo utente.</td>
    <td>Può essere trovata in <strong>Activity Log</strong> nella scheda <strong>Overview</strong>.</td>
  </tr>
  <tr>
    <td><code>update.isProfilesActive</code></td>
    <td>Aggiorna la tua configurazione di archiviazione del profilo utente.</td>
    <td>Può essere trovata nella scheda <strong>Profiles</strong>.</td>
  </tr>
  <tr>
    <td><code>read.themeColor</code></td>
    <td>Visualizzare il colore del tema dell'intestazione del widget di accesso.</td>
    <td>Può essere trovato nella scheda <strong>Login Customization</strong>.</td>
  </tr>
  <tr>
    <td><code>update.themeColor</code></td>
    <td>Aggiorna il colore del tema dell'intestazione del widget di accesso.</td>
    <td>Può essere aggiornato nella scheda <strong>Login Customization</strong>.</td>
  </tr>
  <tr>
    <td><code>read.media</code></td>
    <td>Visualizzare l'immagine che viene visualizzata nel widget di accesso.</td>
    <td>Può essere trovata nella scheda <strong>Login Customization</strong>.</td>
  </tr>
  <tr>
    <td><code>update.media</code></td>
    <td>Aggiorna l'immagine che viene visualizzata nel widget di accesso.</td>
    <td>Può essere aggiornata nella scheda <strong>Login Customization</strong>.</td>
  </tr>
  <tr>
    <td><code>read.uiConfiguration</code></td>
    <td>Visualizza la configurazione dell'IU del widget di accesso incluso il colore dell'intestazione e l'immagine.</td>
    <td>Può essere trovata nella scheda <strong>Login Customization</strong>.</td>
  </tr>
  <tr>
    <td><code>read.uiLanguages</code></td>
    <td>Visualizza un elenco di lingue supportate.</td>
    <td>Deve essere visualizzato dall'API.</td>
  </tr>
  <tr>
    <td><code>update.uiLanguages</code></td>
    <td>Aggiorna le tue lingue supportate. </td>
    <td>Devono essere aggiornate tramite l'API.</td>
  </tr>
  <tr>
    <td><code>read.samlMetadata</code></td>
    <td>Visualizza i metadati SAML ID applicazione.</td>
    <td>Possono essere trovati nella scheda <strong>Identity Providers > SAML 2.0 Federation</strong>.</td>
  </tr>
  <tr>
    <td><code>read.cloudDirectoryUser</code></td>
    <td>Visualizza un utente Cloud Directory.</td>
    <td>Può essere trovato nella scheda <strong>Users</strong>.</td>
  </tr>
  <tr>
    <td><code>update.cloudDirectoryUser</code></td>
    <td>Aggiorna un utente Cloud Directory.</td>
    <td>Può essere aggiornato nella scheda <strong>Users</strong>.</td>
  </tr>
  <tr>
    <td><code>delete.cloudDirectoryUser</code></td>
    <td>Elimina un utente Cloud Directory.</td>
    <td>Può essere eliminato nella scheda <strong>Users</strong>.</td>
  </tr>
  <tr>
    <td><code>read.cloudDirectoryUsers</code></td>
    <td>Visualizza un elenco dei tuoi utenti Cloud Directory.</td>
    <td>Può essere trovato nella scheda <strong>Users</strong>.</td>
  </tr>
  <tr>
    <td><code>update.cloudDirectoryUsers</code></td>
    <td>Aggiorna il tuo elenco di utenti Cloud Directory.</td>
    <td>Può essere aggiornato nella scheda <strong>Users</strong>.</td>
  </tr>
  <tr>
    <td><code>delete.cloudDirectoryUsers</code></td>
    <td>Elimina un elenco di utenti Cloud Directory.</td>
    <td>Può essere eliminato nella scheda <strong>Users</strong>.</td>
  </tr>
  <tr>
    <td><code>read.emailTemplate</code></td>
    <td>Visualizza un modello email.</td>
    <td>Può essere trovato nella scheda <strong>Identity Providers > Cloud Directory > Templates</strong>.</td>
  </tr>
  <tr>
    <td><code>update.emailTemplate</code></td>
    <td>Aggiorna un modello email.</td>
    <td>Può essere trovato nella scheda <strong>Identity Providers > Cloud Directory > Templates</strong>.</td>
  </tr>
  <tr>
    <td><code>delete.emailTemplate</code></td>
    <td>Elimina un modello email per reimpostare il valore predefinito.</td>
    <td>Può essere trovato nella scheda <strong>Identity Providers > Cloud Directory > Templates</strong>.</td>
  </tr>
  <tr>
    <td><code>read.senderDetails</code></td>
    <td>Visualizza i dettagli del mittente.</td>
    <td>Possono essere trovati nella scheda <strong>Identity Providers > Cloud Directory > Settings</strong>.</td>
  </tr>
  <tr>
    <td><code>update.senderDetails</code></td>
    <td>Aggiorna i dettagli del mittente</td>
    <td>Possono essere trovati nella scheda <strong>Identity Providers > Cloud Directory > Settings</strong>.</td>
  </tr>
  <tr>
    <td><code>update.resendNotification</code></td>
    <td>Reinvia le notifiche utente.</td>
    <td>Possono essere trovate nella scheda <strong>Identity Providers > Cloud Directory > Settings</strong>.</td>
  </tr>
  <tr>
    <td><code>update.selfForgotPassword</code></td>
    <td>Aggiorna il processo della password dimenticata.</td>
    <td>Può essere trovato nella scheda <strong>Identity Providers > Cloud Directory > Settings</strong>.</td>
  </tr>
  <tr>
    <td><code>update.forgotPasswordResult</code></td>
    <td>Visualizza il risultato della conferma della password dimenticata.</td>
    <td>Deve essere eseguito tramite l'API.</td>
  </tr>
  <tr>
    <td><code>update.selfSignUp</code></td>
    <td>Aggiorna il processo di registrazione.</td>
    <td>Può essere trovato nella scheda <strong>Identity Providers > Cloud Directory > Settings</strong>.</td>
  </tr>
  <tr>
    <td><code>update.signUpResult</code></td>
    <td>Visualizza la conferma del risultato di registrazione.</td>
    <td>Deve essere eseguita tramite l'API.</td>
  </tr>
  <tr>
    <td><code>read.action_url</code></td>
    <td>Visualizza l'URL personalizzato che viene richiamato quando viene eseguita un'azione.</td>
    <td>Può essere trovato nella scheda <strong>Identity Providers > Cloud Directory > Custom Landing Pages</strong>.</td>
  </tr>
  <tr>
    <td><code>update.action_url</code></td>
    <td>Aggiorna l'URL personalizzato che viene richiamato quando viene eseguita un'azione.</td>
    <td>Può essere trovato nella scheda <strong>Identity Providers > Cloud Directory > Settings</strong>.</td>
  </tr>
  <tr>
    <td><code>update.changePassword</code></td>
    <td>Modifica la password utente di Cloud Directory.</td>
    <td>Può essere trovata nella scheda <strong>Identity Providers > Cloud Directory > Settings</strong>.</td>
  </tr>
  <tr>
    <td><code>read.loginWidgetConfig</code></td>
    <td>Visualizza la configurazione del widget di accesso.</td>
    <td>Può essere trovata nella scheda <strong>Login Customization</strong>.</td>
  </tr>
  <tr>
    <td><code>update.loginWidgetConfig</code></td>
    <td>Aggiorna la configurazione del widget di accesso.</td>
    <td>Può essere aggiornata nella scheda <strong>Login Customization</strong>.</td>
  </tr>
</table>


Per ulteriori informazioni su come funziona il servizio, consulta la [Documentazione {{site.data.keyword.cloudaccesstrailshort}}](/docs/services/cloud-activity-tracker/index.html).

</br>
</br>

## Esempio: concedere a un altro utente l'accesso a un'istanza di {{site.data.keyword.appid_short_notm}}
{: #example}

In questo scenario, un amministratore ha creato un'istanza di {{site.data.keyword.appid_short_notm}} e deve concedere l'accesso di visualizzatore a un altro membro del team.
{: shortdesc}

Prima di cominciare:
* Installa la [CLI {{site.data.keyword.Bluemix_notm}}](/docs/cli/index.html).

Per aggiornare le autorizzazioni di accesso, l'amministratore completa la seguente procedura:

1. Accedi alla console {{site.data.keyword.Bluemix_notm}}.
2. Concedi al dipendente l'accesso di visualizzazione seguendo le istruzioni illustrate nella [documentazione IAM](/docs/iam/iamusermanage.html#iamusermanage).
3. Passa alla scheda **Credenziali del servizio** del dashboard {{site.data.keyword.appid_short_notm}}. Fai clic su **Visualizza credenziali** e copia il **tentantID**.
4. Accedi con la CLI {{site.data.keyword.Bluemix_notm}} nel tuo terminale.
    ```
    bx login -a api.<region>.bluemix.net
    ```
    {: codeblock}
5. Ottieni un token IAM e prendine nota.
    ```
    bx iam oauth-tokens
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
    'https://appid-management.ng.bluemix.net/management/v4/<tenantId>/config/idps/facebook'
    ```
    {: codeblock}

    Il risultato è un messaggio 403 non autorizzato.

Per visualizzare la configurazione di {{site.data.keyword.appid_short_notm}} dalla CLI, il membro del team completa la seguente procedura:

1. Esegui l'accesso utilizzando la CLI {{site.data.keyword.Bluemix_notm}} nel tuo terminale.
    ```
    bx login -a api.<region>.bluemix.net
    ```
    {: codeblock}
2. Ottieni un token IAM e prendine nota.
    ```
    bx iam oauth-tokens
    ```
    {: codeblock}
3. Visualizza la configurazione del provider di identità per Facebook utilizzando cURL.
    ```
    curl -X GET --header 'Accept: application/json' --header 'Authorization: <IAM token value>' \  'https://appid-management.ng.bluemix.net/management/v4/<tenantId>/config/idps/facebook'
    ```
    {: codeblock}
    Il risultato è un messaggio 200 che contiene le informazioni sul provider di identità.
