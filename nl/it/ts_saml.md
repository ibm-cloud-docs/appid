---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-14"

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

Se hai dei problemi durante la configurazione dei provider di identità da utilizzare con {{site.data.keyword.appid_full}}, considera queste tecniche per la risoluzione dei problemi e per ottenere assistenza.
{: shortdesc}


## Un utente non viene reindirizzato all'applicazione dopo l'accesso.
{: #signin-fail}

{: tsSymptoms}
Un utente accede alla tua applicazione tramite la pagina di accesso di un provider di identità e non accade nulla o l'accesso non riesce.

{: tsCauses}
L'accesso potrebbe non riuscire per i seguenti motivi:

* Il tuo URL di reindirizzamento non è stato correttamente aggiunto alla [whitelist](faq.html#redirect).
* L'utente non è autorizzato.
* L'utente ha provato ad accedere con le credenziali errate.

{: tsResolve}
Perché si verifichi un reindirizzamento:

* Verifica che il tuo URL di reindirizzamento sia corretto. Deve essere esatto affinché il reindirizzamento funzioni.
* Assicurati che l'utente acceda con le credenziali corrette.
* Verifica che siano configurate nelle impostazioni utente del tuo provider di identità.

</br>

## Problemi SAML comuni
{: #common-saml}

Esamina la seguente tabella per le spiegazioni e le risoluzioni relative ai problemi più comuni riscontrati quando lavori con SAML.

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
      <td><code>Il corpo della risposta SAML deve contenere il parametro RelayState.</code></td>
      <td>Il parametro non era incluso nel corpo della risposta SAML. {{site.data.keyword.appid_short_notm}} fornisce il parametro al provider di identità come parte della richiesta e il parametro esatto deve essere restituito nella risposta. Se il parametro viene modificato, puoi contattare l'amministratore del tuo provider di identità. </td>
    </tr>
    <tr>
      <td><code>La configurazione SAML deve avere certificati, entityID e signInUrl dell'IdP.</code></td>
      <td>Il provider di identità SAML non è <a href="enterprise.html" target="_blank">configurato correttamente</a>. Convalida la tua configurazione.</td>
    </tr>
    <tr>
      <td><code>Errore nella convalida dell'asserzione. Controllo firma dell'asserzione SAML non riuscito. Il certificato potrebbe non essere valido.</code></td>
      <td>Nell'asserzione devono essere inclusi una firma e un digest validi. La firma deve essere creata utilizzando la chiave privata associata al certificato fornito nella configurazione SAML, può essere usato sia quello secondario che primario. <strong>Nota</strong>: {{site.data.keyword.appid_short_notm}} non supporta l'asserzione crittografata. Se il tuo provider di identità codifica la tua asserzione SAML, disabilita la crittografia.</td>
    </tr>
  </tbody>
</table>

</br>

## Un utente non viene reindirizzato al provider di identità.
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
Un valore di attributo esiste in un profilo utente, ma non è associato all'attributo corretto.

{: tsCauses}
L'attributo del profilo utente non è associato correttamente.

{: tsResolve}
Associa l'attributo nelle impostazioni del tuo provider di identità. {{site.data.keyword.appid_short_notm}} prevede i seguenti attributi:
* `name`
* `email`
* `locale`
* `picture`

</br>

## Errori di convalida della risposta SAML
{: #saml-response}

{{site.data.keyword.appid_short_notm}} impone i seguenti requisiti di validità per le asserzioni. Tutti gli attributi sono nodi SAMLResponse XML obbligatori a meno che non sia specificato diversamente.
{: shortdesc}


<table summary="Ogni riga della tabella deve essere letta da sinistra a destra, con l'elemento della risposta nella prima colonna e una descrizione nella seconda colonna.">
  <thead>
    <th>Elemento della risposta</th>
    <th>Descrizione</th>
  </thead>
  <tbody>
    <tr>
      <td><code>samlp:Response</code></td>
      <td>L'elemento della risposta deve essere incluso nell'XML di risposta.</td>
    </tr>
    <tr>
      <td><code>SAML version</code></td>
      <td>{{site.data.keyword.appid_short_notm}} accetta solo <code>SAML version 2.0</code>.</td>
    </tr>
    <tr>
      <td><code>InResponseTo</code></td>
      <td>{{site.data.keyword.appid_short_notm}} verifica che l'elemento della risposta <code>InResponseTo</code> restituito nell'asserzione corrisponda all'ID della richiesta salvato dalla richiesta SAML.</td>
    </tr>
    <tr>
      <td><code>saml:issuer</code></td>
      <td>L'emittente specificato in un'asserzione deve corrispondere a quello specificato nella configurazione del provider di identità {{site.data.keyword.appid_short_notm}}.</td>
    </tr>
    <tr>
      <td><code>ds:Signature</code></td>
      <td>Nell'asserzione devono essere inclusi una firma e un digest validi. La firma deve essere creata utilizzando la chiave privata associata al certificato fornito nella configurazione SAML. Il digest viene convalidato utilizzando i valori per <code>CanonicalizationMethod</code> e <code>Transforms</code> specificati. <strong>Nota</strong>: {{site.data.keyword.appid_short_notm}} non convalida la scadenza del certificato. Per avere assistenza nella gestione dei tuoi certificati, prova il [Gestore certificato](/docs/services/certificate-manager/index.html).</td>
    </tr>
    <tr>
      <td><code>saml:subject</code></td>
      <td>L'oggetto o il <code>name_id</code> dell'asserzione deve essere l'email della federazione dell'utente.</td>
    </tr>
    <tr>
      <td><code>saml:AttributeStatement</code></td>
      <td>Afferma che alcuni attributi sono associati a un utente autenticato specifico.</td>
    </tr>
    <tr>
      <td><code>saml:Conditions</code></td>
      <td><strong>Facoltativo</strong>: quando viene inclusa un'istruzione di condizioni in un'asserzione, deve contenere anche una data/ora valida. {{site.data.keyword.appid_short_notm}} rispetta il periodo di validità specificato nell'asserzione. Per verificare, il servizio ricerca i vincoli <code>NotBefore</code> e <code>NotOnOrAfter</code> che devono essere definiti e validi.</td>
    </tr>
  </tbody>
</table>

{{site.data.keyword.appid_short_notm}} non supporta l'asserzione crittografata. Se il tuo provider di identità è configurato per crittografare la tua asserzione, disabilitalo. L'asserzione deve essere in un formato non crittografato.
{: tip}
