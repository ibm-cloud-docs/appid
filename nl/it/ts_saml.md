---

copyright:
  years: 2017, 2018
lastupdated: "2018-06-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tip: .tip}

# Configurazioni del provider di identità
{: #troubleshooting-idp}

Se hai dei problemi quando utilizzi {{site.data.keyword.appid_full}}, considera queste tecniche per la risoluzione dei problemi e per ottenere assistenza.
{: shortdesc}


## Non c'è alcun reindirizzamento all'applicazione dopo l'accesso
{: #signin-fail}

{: tsSymptoms}
Un utente accede alla tua applicazione tramite la pagina di accesso di un provider di identità e non accade nulla o l'accesso non riesce.

{: tsCauses}
L'accesso potrebbe non riuscire per i seguenti motivi:

* Il tuo URL di reindirizzamento non è stato correttamente aggiunto alla [whitelist](identity-providers.html#redirect).
* L'utente non è autorizzato.
* L'utente ha provato ad accedere con le credenziali errate.

{: tsResolve}
Perché si verifichi un reindirizzamento:

* Verifica che il tuo URL di reindirizzamento sia corretto. Deve essere esatto affinché il reindirizzamento funzioni.
* Assicurati che l'utente acceda con le credenziali corrette.
* Verifica che siano configurate nelle impostazioni utente del tuo provider di identità.


## Problemi comuni quando si utilizza SAML
{: #common-saml}

Esamina la seguente tabella per le spiegazioni e le risoluzioni relative ai problemi più comuni riscontrati quando si lavora con SAML.

<table summary="Ogni riga della tabella deve essere letta da sinistra a destra, con lo stato del cluster nella prima colonna e una descrizione nella seconda colonna.">
  <thead>
    <th>Messaggio</th>
    <th>Descrizione</th>
  </thead>
  <tbody>
    <tr>
      <td><code>Impossibile analizzare l'asserzione xml.</code></td>
      <td>La risposta di SAML aveva un formato non corretto.</td>
    </tr>
    <tr>
      <td><code>Attributo non valido senza nome. Contatta l'amministratore del tuo provider di identità.</code></td>
      <td>È presente un <code>&lt;saml:Attribute&gt;</code> senza un valore definito. Contatta l'amministratore del tuo provider di identità.</td>
    </tr>
    <tr>
      <td><code>Il corpo della risposta SAML deve contenere RelayState.</code></td>
      <td>Il parametro RelayState non era incluso nel corpo della risposta SAML. {{site.data.keyword.appid_short_notm}} fornisce il parametro al provider di identità come parte della richiesta e il parametro esatto deve essere restituito nella risposta. Se il parametro viene modificato, puoi contattare l'amministratore del tuo provider di identità. </td>
    </tr>
    <tr>
      <td><code>La configurazione SAML deve avere certificati, entityID e signInUrl dell'IdP.</code></td>
      <td>Il provider di identità SAML non è configurato correttamente. Convalida la tua configurazione. Per informazioni, vedi <a href="enterprise.html#configuring-saml" target="_blank">Configurazione della tua applicazione per lavorare con un provider di identità SAML esterno.</a></td>
    </tr>
    <tr>
      <td><code>Errore nella convalida dell'asserzione. Controllo firma dell'asserzione SAML non riuscito. Il certificato potrebbe non essere valido.</code></td>
      <td>Nell'asserzione devono essere inclusi una firma e un digest validi. La firma deve essere creata utilizzando la chiave privata associata al certificato fornito nella configurazione SAML; può essere usato sia quello secondario che primario. <strong>Nota</strong>: {{site.data.keyword.appid_short_notm}} non supporta l'asserzione crittografata. Se il tuo provider di identità la esegue nell'asserzione SAML, disabilita la crittografia.</td>
    </tr>
  </tbody>
</table>


## Non c'è alcun reindirizzamento al provider di identità
{: #saml-redirect}

{: tsSymptoms}
Un utente tenta di accedere alla tua applicazione, ma la pagina di accesso non viene visualizzata quando richiesto.

{: tsCauses}
Il provider di identità potrebbe non funzionare per diversi motivi:

* Il tuo URL di reindirizzamento configurato non è corretto.
* Il provider di identità non riconosce la richiesta di autenticazione.
* Il provider di identità prevede l'associazione HTTP-POST.
* Il provider di identità prevede una authnRequest firmata.

{: tsResolve}
Puoi provare alcune di queste soluzioni:

* Aggiorna il tuo URL di accesso. Questo URL viene inviato come parte di authnRequest e deve essere esatto.
* Assicurati che i metadati {{site.data.keyword.appid_short_notm}} siano impostati correttamente nelle impostazioni del tuo provider di identità.
* Configura il tuo provider di identità per accettare la authnRequest in HTTP-Redirect.
* {{site.data.keyword.appid_short_notm}} non supporta la firma di authnRequest.

Se nessuna delle soluzioni funziona, è possibile che tu abbia un problema di connessione.
{: tip}

## Un attributo mostra il valore errato
{: #saml-attribute}

{: tsSymptoms}
Un valore di attributo esiste in un profilo utente, ma non è collegato all'attributo corretto.

{: tsCauses}
L'attributo del profilo utente non è associato correttamente.

{: tsResolve}
Associa l'attributo nelle impostazioni del tuo provider di identità. {{site.data.keyword.appid_short_notm}} prevede i seguenti attributi:
* `name`
* `email`
* `locale`
* `picture`


