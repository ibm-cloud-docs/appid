---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-21"

keywords: authentication, authorization, identity, app security, secure, troubleshooting, help, support, requests, uri

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
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}

# Risoluzione dei problemi: generale 
{: #troubleshooting}

Se hai dei problemi quando utilizzi {{site.data.keyword.appid_full}}, considera queste tecniche per la risoluzione dei problemi e per ottenere assistenza.
{: shortdesc}

## Come ottenere aiuto e supporto
{: #ts-gettinghelp}

Puoi ottenere aiuto ricercando le informazioni o facendo delle domande in un forum. Inoltre puoi aprire un ticket di supporto. Quando utilizzi i forum per fare una domanda, contrassegnala con una tag in modo che sia visualizzabile dai team di sviluppo {{site.data.keyword.cloud_notm}}.
  * Se hai domande tecniche su {{site.data.keyword.appid_short_notm}}, inserisci la tua domanda in <a href="https://stackoverflow.com/" target="_blank">Stack Overflow <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> e contrassegnala con la tag "ibm-appid".
  * Per domande sul servizio e sulle istruzioni per l'utilizzo iniziale, utilizza il forum <a href="https://developer.ibm.com/" target="_blank">dW Answers <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>. Includi la tag `appid`.

Per ulteriori informazioni su come ottenere supporto, consulta [Come posso ottenere il supporto di cui ho bisogno?](/docs/get-support?topic=get-support-getting-customer-support#getting-customer-support).


## Un utente non viene reindirizzato all'applicazione dopo l'accesso.
{: #ts-signin-fail}

{: tsSymptoms}
Un utente accede alla tua applicazione tramite la pagina di accesso di un provider di identità e non accade nulla o l'accesso non riesce.

{: tsCauses}
L'accesso potrebbe non riuscire per i seguenti motivi:

* Il tuo URL di reindirizzamento non è stato correttamente aggiunto alla [whitelist](/docs/services/appid?topic=appid-faq#faq-redirect).
* L'utente non è autorizzato.
* L'utente ha provato ad accedere con le credenziali errate.

{: tsResolve}
Perché si verifichi un reindirizzamento:

* Verifica che il tuo URL di reindirizzamento sia corretto. Deve essere esatto affinché il reindirizzamento funzioni.
* Assicurati che l'utente acceda con le credenziali corrette.
* Verifica che siano configurate nelle impostazioni utente del tuo provider di identità.



## Un URI personalizzato viene rifiutato
{: #ts-custom-uri}

{: tsSymptoms}
Quando immetti un URL di reindirizzamento web che utilizza uno schema URL personalizzato, tale URL viene rifiutato dalla console {{site.data.keyword.appid_short_notm}}.

{: tsCauses}
Il tuo URL potrebbe venire rifiutato per i seguenti motivi:

* L'URL non segue uno schema `http` o `https`
* L'URL termina con `://`
* È presente un errore tipografico nel tuo URL.

Vengono adottate delle limitazioni per motivi di sicurezza.

{: tsResolve}
Per risolvere il problema, verifica che l'URL sia corretto. Se il tuo URL non soddisfa i requisiti, puoi creare un endpoint HTTPS nella tua applicazione per reindirizzare il codice di concessione al tuo URL personalizzato. Specifica l'endpoint creato come tuo URL di reindirizzamento nella console {{site.data.keyword.appid_short_notm}}. Per ulteriori informazioni sugli URI di reindirizzamento, vedi [Aggiunta di URI di reindirizzamento](/docs/services/appid?topic=appid-managing-idp#add-redirect-uri)

## Un utente non viene reindirizzato al provider di identità.
{: #ts-redirect}

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
{: #ts-saml-attribute}

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



## Errore: too many requests
{: #ts-requests}

{: tsSymptoms}
Provi a visualizzare la home page della tua applicazione ma ricevi il seguente errore:

```
{"error_code":"too many requests","error_description":"too many requests"}
```
{: screen}

{: tsCauses}
Potresti ricevere un errore "too many requests" se stai eseguendo una verifica automatizzata con solo un singolo utente virtuale. Ogni utente è limitato a cinque tentativi di accesso in un arco di tempo di un minuto. I tentativi di accesso sono limitati per evitare attacchi DDOS di forza bruta e altri tipi di attacchi simili.

{: tsResolve}
Per risolvere il problema, potresti voler utilizzare più utenti virtuali quando esegui la verifica.
</br>
