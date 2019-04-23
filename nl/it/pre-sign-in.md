---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

keywords: authentication, authorization, identity, app security, secure, development, user information, attributes, profiles, 

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

# Aggiunta degli attributi prima dell'accesso utente
{: #preregister}

Con {{site.data.keyword.appid_full}}, puoi iniziare a creare un profilo per gli utenti che sai avranno bisogno di accedere alla tua applicazione, prima del loro accesso iniziale.
{: shortdesc}

Per ulteriori informazioni sui tipi di attributi, consulta [Descrizione dei profili utente](/docs/services/appid?topic=appid-user-profile). Per ulteriori informazioni sugli attributi personalizzati e le rispettive considerazioni sulla sicurezza, consulta [Attributi personalizzati](/docs/services/appid?topic=appid-custom-attributes).
{: tip}

## Descrizione della preregistrazione
{: #preregister-understand}

### Perché dovrei utilizzare la preregistrazione?
{: #preregister-why}

Prendi in considerazione un'applicazione in cui utilizzi {{site.data.keyword.appid_short_notm}} per attuare la federazione degli utenti esistenti dal tuo provider di identità SAML. Potresti volere che alcuni utenti abbiamo l'accesso `admin` immediatamente dopo l'accesso all'applicazione per la prima volta. Per far ciò, puoi utilizzare l'endpoint di preregistrazione per impostare un attributo `admin` personalizzato per tali utenti e concedergli l'accesso alla console di gestione senza alcuna ulteriore azione da parte tua. Assicurati di prendere in considerazione i [problemi sulla sicurezza](/docs/services/appid?topic=appid-custom-attributes#custom-attributes) che possono presentarsi modificano le impostazioni predefinite.

### Come vengono identificati gli utenti?
{: #preregister-identify-user}

Puoi identificare i tuoi utenti utilizzando uno dei seguenti:

* L'ID univoco dell'utente, denominato **GUID**, nel provider di identità. Sebbene questo identificativo esista sempre ed è garantito che è univoco, non sempre è prontamente disponibile o facile da comprendere. Ad esempio, Cloud Directory utilizza un GUID da 16 byte casuale.
* Se disponibile, l'**email** dell'utente.

### Quali informazioni forniscono i provider di identità?
{: #preregister-idp-provide}

Controlla la seguente tabella per vedere quale tipo di informazioni sull'identità puoi utilizzare.

<table>
  <thead>
    <tr>
      <th>Provider di identità</th>
      <th>GUID</th>
      <th>Email</th>
      <th>Sub</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Cloud Directory</td>
      <td><img src="images/confirm.png" width="32" alt="Funzione disponibile" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="Funzione disponibile" style="width:32px;" /></td>
      <td> </td>
    </tr>
    <tr>
      <td>Facebook</td>
      <td><img src="images/confirm.png" width="32" alt="Funzione disponibile" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="Funzione disponibile" style="width:32px;" /></td>
      <td> </td>
    </tr>
    <tr>
      <td>Google</td>
      <td><img src="images/confirm.png" width="32" alt="Funzione disponibile" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="Funzione disponibile" style="width:32px;" /></td>
      <td> </td>
    </tr>
    <tr>
      <td>SAML</td>
      <td></td>
      <td><img src="images/confirm.png" width="32" alt="Funzione disponibile" style="width:32px;" /></td>
      <td> </td>
    </tr>
    <tr>
      <td>Personalizzato</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Funzione disponibile" style="width:32px;" /></td>
    </tr>
  </tbody>
</table>

### Come viene gestito Cloud Directory?
{: #preregister-cd}


Per garantire l'integrità degli attributi utente preregistrati, Cloud Directory impone degli ulteriori requisiti ai propri utenti. La preregistrazione può verificarsi solo quando una convalida email viene abilitata e verificata. Se esegui la preregistrazione di un utente Cloud Directory con degli attributi specifichi, tali attributi sono destinati a una persona specifica. Se non viene prima verificata l'email, è possibile che un altro utente richieda l'indirizzo email e tutti gli attributi assegnati ad esso.

1. Imposta Cloud Directory in modalità email e password. Puoi farlo tramite l'IU nelle impostazioni generali sulla scheda **Cloud Directory**. Puoi anche impostarlo tramite le [API di gestione](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.createCloudDirectoryUser).

2. Verifica l'indirizzo email degli utenti per confermarne l'identità in uno dei seguenti modi:

  * Per verificare un'identità degli utenti tramite l'email, imposta **Email verification** su **On** nella scheda **Cloud Directory** del dashboard del servizio. Se aggiungi un utente ed accede alla tua applicazione senza prima verificare la propria email, l'accesso viene completato correttamente, ma i suoi attributi predefiniti vengono eliminati.
  * Per verificare gli utenti manualmente devi essere un amministratore ed utilizzare le [API di gestione](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.createCloudDirectoryUser) di Cloud Directory. Quando crei o aggiorni un utente, devi impostare in modo esplicito il campo `status` su `CONFIRMED` all'interno del tuo payload dei dati utente.

**C'è qualcosa di speciale che devo fare quando utilizzo un provider di identità personalizzato?**

Quando aggiungi delle informazioni sull'utente alla tua applicazione in anticipo, puoi utilizzare un qualsiasi identificativo univoco fornito dal flusso di autenticazione. L'identificativo deve corrispondere _esattamente_ al `sub` del JWT (JSON web token) inviato durante la richiesta di autorizzazione. Se l'identificativo non corrisponde, il profilo che vuoi aggiungere non viene collegato correttamente.



## Aggiunta delle informazioni sull'utente alla tua applicazione
{: #preregister-add-info}

Ora che hai ottenuto delle informazioni sul processo e preso in considerazione le tue implicazioni sulla sicurezza, prova ad aggiungere un utente.

**Prima di cominciare:**

Per aggiungere degli attributi personalizzati per uno specifico utente con l'[/endpoint dell'API di gestione degli utenti](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Users/mgmt.users_search_user_profile), devi conoscere le seguenti informazioni:

* Quale provider di identità sta per essere utilizzato dall'utente per accedere.
* L'identificativo univoco dell'utente fornito dal provider di identità.

Quando un utente accede alla tua applicazione per la prima volta, {{site.data.keyword.appid_short_notm}} ricerca l'utente. Se lo trova, l'utente eredita l'identità che hai assegnato. Se l'utente non viene trovato, viene creato un nuovo utente in base alle informazioni fornite dal provider di identità.

**Per aggiungere un utente:**

1. Accedi a IBM Cloud.
  ```
  ibmcloud login
  ```
  {: pre}

2. Trova il tuo token IAM immettendo il seguente comando.
  ```
  ibmcloud iam oauth-tokens
  ```
  {: pre}

3. Effettua una richiesta POST all'endpoint `/users` che contiene una descrizione dell'utente e degli attributi che vuoi impostare come un oggetto JSON.

  Intestazione:
  ```
  POST {management-url}/management/v4/{tenantId}/users
       Host: <management-server-url>
       Authorization: 'Bearer <IAM_TOKEN>'
       Content-Type: application/json
  ```
  {: pre}

  Corpo:
  ```
   {
       "idp": "<Identity Provider>",
       "idp-identity": "<User's unique identifier>",
       "profile": {
           "attributes": {
             "mealPreference":"vegeterian"
           }
       }
   }
  ```
  {: pre}

  <table>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="Icona idea"/> Descrizione dei componenti</th>
    </thead>
    <tbody>
      <tr>
        <td><code><em>idp</em></code></td>
        <td>Il provider di identità con cui si autenticherà l'utente. Le opzioni includono: `saml`, `cloud_directory`, `facebook`, `google`, `appid_custom`, `ibmid`.</td>
      </tr>
      <tr>
        <td><code><em>idp-identity</em></code></td>
        <td>L'identificativo univoco fornito dal provider di identità.</td>
      </tr>
      <tr>
        <td><code><em>profile</em></code></td>
        <td>Il profilo dell'utente che contiene l'associazione JSON dell'attributo personalizzato.</td>
      </tr>
    </tbody>
  </table>

  Richiesta di esempio:
  ```
  $ curl --request POST \
       --url 'https://{Management_URI}/users \
       --header 'Authorization: Bearer {IAM_TOKEN}' \
       --header 'Content-Type: application/json' \
       --data '{"idp": "saml", "idp-identity": "user@ibm.com", "profile": { "attributes": { "role": "admin",
       "frequent_flyer_points": 1000 }}}'
  ```
  {: screen}

3. Verifica che la registrazione abbia avuto esito positivo in uno dei seguenti modi:
  * Controlla l'ID utente nella risposta.
    ```
    {
        "id": "<{{site.data.keyword.appid_short_notm}} User Id>"
    }
    ```
    {: screen}
  * Controlla il profilo utente che è stato creato.

Tieni presente che gli attributi predefiniti di un utente sono vuoti fino alla prima autenticazione, ma l'utente è, a tutti gli effetti, un utente completamente autenticato. Puoi utilizzare il suo ID univoco come faresti con qualcuno che ha già eseguito l'accesso. Ad esempio, puoi modificare, ricercare o eliminare il profilo.

Ora che hai associato un utente ad attributi specifici, prova ad [accedere o aggiornare gli attributi](/docs/services/appid?topic=appid-custom-attributes)!


</br>
