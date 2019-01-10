---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}


# Autenticazione multifattore
{: #mfa}

L'autenticazione multifattore (MFA) è un metodo per confermare l'identità di un utente richiedendogli di utilizzare qualcosa di cui dispongono in aggiunta a qualcosa che conoscono per verificare che sono chi dicono di essere. Ad esempio, con {{site.data.keyword.appid_full}} puoi avere un input utente di un codice monouso inviato all'email dell'utente dopo che ha immesso l'email e la password.
{: shortdesc}

MFA è disponibile solo per gli utenti Cloud Directory.  Se stai utilizzando l'accesso aziendale con SAML 2.0 o l'accesso social, puoi abilitare MFA nel provider di identità che stai utilizzando.
{: note}

Quando MFA è abilitato, il widget di accesso lo richiede ogni volta che un nuovo utente tenta di accedere. Dopo che l'utente ha inserito correttamente le proprie credenziali, viene inviato un passcode monouso all'indirizzo email che ha registrato quando ha creato il suo account. Ogni codice è di sei caratteri con una scadenza di cinque minuti. Se un utente non riceve il codice, può richiedere che ne venga inviato un altro, ma il tempo di scadenza non viene reimpostato. Dopo la scadenza di un codice, un utente viene forzato a ripetere l'intero processo di accesso.

Se non è ancora stata confermata un'email utente tramite le API di gestione o la verifica dell'email alla registrazione, viene confermata quando una verifica del codice MFA ha esito positivo. Se devi modificare l'indirizzo email di un utente, un amministratore può utilizzare le [API di gestione](https://appid-management.ng.bluemix.net/swagger-ui/#!/Cloud_Directory_Users/updateCloudDirectoryUser).

MFA è disponibile per le istanze di {{site.data.keyword.appid_short_notm}} presenti sul [piano dei prezzi di livello graduale](faq.html#pricing).
{: note}

## Descrizione del flusso
{: #understanding}



1. All'utente dell'applicazione viene mostrata l'IU di accesso predefinita di {{site.data.keyword.appid_short_notm}}.

2. L'utente immette le proprie credenziali utente Cloud Directory, come ad esempio l'email o il nome utente e la password.

3. Le credenziali vengono convalidate e viene restituito il modulo MFA. Il modulo richiede all'utente di incollare il codice inviato per email.

4. L'utente riceve un passcode monouso al proprio indirizzo email e lo immette nell'IU MFA predefinita.

5. Il codice MFA viene convalidato e reindirizzato all'applicazione client con il codice di autorizzazione per continuare il flusso OAuth 2.


</br>

## Configurazione di MFA
{: #configuration}

{{site.data.keyword.appid_short_notm}} MFA è supportata come parte del flusso del codice di autorizzazione OAuth 2.0 per gli utenti Cloud Directory tramite il widget di accesso.
{: shortdesc}

Per configurare MFA tramite la GUI, consulta [Cloud Directory](cloud-directory.html).
{: note}

### Configurazione con l'API

Puoi configurare MFA utilizzando le API di gestione.
{: shortdesc}

**Prima di cominciare**

Assicurati di aver i seguenti prerequisiti: 

* L'ID tenant della tua istanza {{site.data.keyword.appid_short_notm}}. Può essere trovato nella sezione **Service Credentials** del dashboard.
* Il tuo token Identity and Access Management (IAM). Per un aiuto sull'ottenimento del token IAM, consulta la [Documentazione IAM](/docs/iam/apikey_iamtoken.html).


1. Abilita MFA, effettuando una richiesta PUT all'endpoint `/config/mfa` con la tua configurazione MFA per impostare `isActive` su `true`.

  Intestazione:
  ```
  PUT {management-url}/management/v4/{tenantId}/config/mfa
       Host: <management-server-url>
       Authorization: Bearer <IAM_TOKEN>
       Content-Type: application/json
  ```
  {: pre}

  Corpo:
  ```
   {
       "isActive": true
   }
  ```
  {: pre}

  Richiesta di esempio:
  ```
  $ curl -X PUT
    --header 'Content-Type: application/json'
    --header 'Accept: application/json'
    --header 'Authorization: Bearer <IAM_TOKEN>'
    -d '{
          "isActive": true
      }'
    }'
    '{management-url}/management/v4/{tenantId}/config/mfa'
  ```
  {: screen}

2. Abilita il tuo canale MFA effettuando una richiesta PUT all'endpoint `/mfa/channels/{channelType}` con la tua configurazione MFA. Quando `isActive` è impostato su `true`, il tuo canale MFA è abilitato.

  Intestazione:
  ```
  PUT /management/v4/{tenantId}/mfa/channels/{channelType}
       Host: <management-server-url>
       Authorization: Bearer <IAM_TOKEN>
       Content-Type: application/json
  ```
  {: pre}

  <table>
    <thead>
      <th colspan=3>Tipi di canale supportati</th>
    </thead>
    <tbody>
      <tr>
        <td>`email`</td>
      </tr>
    </tbody>
  </table>

  Corpo:
  ```
   {
       "isActive": true
   }
  ```
  {: pre}

  Richiesta di esempio:
  ```
  $ curl -X PUT
    --header 'Content-Type: application/json'
    --header 'Accept: application/json'
    --header 'Authorization: Bearer <IAM_TOKEN>'
    -d '{
          "isActive": true
      }'
    }'
    '{management-url}/management/v4/{tenantId}/mfa/channels/{channelType}'
  ```
  {: screen}

</br>
