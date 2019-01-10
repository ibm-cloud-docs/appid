---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:pre: .pre}
{:tip: .tip}
{:screen: .screen}
{:codeblock: .codeblock}

# Aggiunta degli attributi prima dell'accesso utente
{: #sign-in}

Con {{site.data.keyword.appid_full}}, puoi iniziare a creare un profilo per gli utenti che sai avranno bisogno di accedere alla tua applicazione, prima del loro accesso iniziale.
{: shortdesc}

Per ulteriori informazioni sui tipi di attributi, consulta [Descrizione dei profili utente](user-profile.html). Per ulteriori informazioni sugli attributi personalizzati e le rispettive considerazioni sulla sicurezza, consulta [Attributi personalizzati](custom-attributes.html).
{: tip}

**Perché dovrei voler aggiungere delle informazioni su un utente alla mia applicazione prima che acceda per la prima volta?**

Prendi in considerazione un'applicazione in cui utilizzi {{site.data.keyword.appid_short_notm}} per attuare la federazione degli utenti esistenti dal tuo provider di identità SAML. Potresti volere che alcuni utenti abbiamo l'accesso `admin` immediatamente dopo l'accesso all'applicazione per la prima volta. Per far ciò, puoi utilizzare l'endpoint di preregistrazione per impostare un attributo `admin` personalizzato per tali utenti e concedergli l'accesso alla console di gestione senza alcuna ulteriore azione da parte tua. Assicurati di prendere in considerazione i [problemi sulla sicurezza](custom-attributes.html) che possono presentarsi modificano le impostazioni predefinite.

**Come vengono identificati gli utenti?**

Puoi identificare i tuoi utenti utilizzando uno dei seguenti:

* L'ID univoco dell'utente, denominato **GUID**, nel provider di identità. Sebbene questo identificativo esista sempre ed è garantito che è univoco, non sempre è prontamente disponibile o facile da comprendere. Ad esempio, Cloud Directory utilizza un GUID casuale da 16 byte.
* Se disponibile, l'**email** dell'utente.

**Come posso sapere quale provider di identità fornisce quali informazioni?**

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

**Cloud Directory viene gestito in modo diverso?**

Per garantire l'integrità degli attributi utente preregistrati, Cloud Directory impone degli ulteriori requisiti ai propri utenti. La preregistrazione può verificarsi solo quando una convalida email viene abilitata e verificata. Se esegui la preregistrazione di un utente Cloud Directory con degli attributi specifichi, tali attributi sono destinati a una persona specifica. Se non viene prima verificata l'email, è possibile che un altro utente richieda l'indirizzo email e tutti gli attributi assegnati ad esso.

Come posso farlo?

1. Imposta Cloud Directory in modalità email e password. Puoi farlo tramite l'IU nelle impostazioni generali sulla scheda **Cloud Directory**. Puoi anche impostarlo tramite le [API di gestione](https://appid-management.ng.bluemix.net/swagger-ui/#!/Cloud_Directory_Users/createCloudDirectoryUser).

2. Verifica l'indirizzo email degli utenti per confermarne l'identità in uno dei seguenti modi:

  * Per verificare un'identità degli utenti tramite l'email, imposta **Email verification** su **On** nella scheda **Cloud Directory** del dashboard del servizio. Se aggiungi un utente ed accede alla tua applicazione senza prima verificare la propria email, l'accesso viene completato correttamente, ma i suoi attributi predefiniti vengono eliminati.
  * Per verificare gli utenti manualmente devi essere un amministratore ed utilizzare le [API di gestione](https://appid-management.ng.bluemix.net/swagger-ui/#!/Cloud_Directory_Users/createCloudDirectoryUser) di Cloud Directory. Quando crei o aggiorni un utente, devi impostare in modo esplicito il campo `status` su `CONFIRMED` all'interno del tuo payload dei dati utente.

**C'è qualcosa di speciale che devo fare quando utilizzo un provider di identità personalizzato?**

Quando aggiungi delle informazioni sull'utente alla tua applicazione in anticipo, puoi utilizzare un qualsiasi identificativo univoco fornito dal flusso di autenticazione. L'identificativo deve corrispondere _esattamente_ al `sub` del JWT (JSON web token) inviato durante la richiesta di autorizzazione. Se l'identificativo non corrisponde, il profilo che vuoi aggiungere non viene collegato correttamente.



## Aggiunta delle informazioni sull'utente alla tua applicazione
{: #add}

Ora che hai ottenuto delle informazioni sul processo e preso in considerazione le tue implicazioni sulla sicurezza, prova ad aggiungere un utente.

**Prima di cominciare:**

Per aggiungere degli attributi personalizzati per un utente specifico con l'endpoint dell'API di gestione [/users](https://appid-management.ng.bluemix.net/swagger-ui/#!/Users/users_search_user_profile), devi conoscere le seguenti informazioni:

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

Ora che hai associato un utente con degli attributi specifici, tenta di [accedere agli attributi](/docs/services/appid/custom-attributes.html)!


</br>
