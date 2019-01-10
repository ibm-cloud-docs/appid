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

# Risoluzione dei problemi generali
{: #troubleshooting}

Se hai dei problemi quando utilizzi {{site.data.keyword.appid_full}}, considera queste tecniche per la risoluzione dei problemi e per ottenere assistenza.
{: shortdesc}

## Come ottenere aiuto e supporto
{: #gettinghelp}

Puoi ottenere aiuto ricercando le informazioni o facendo delle domande in un forum. Inoltre puoi aprire un ticket di supporto. Quando utilizzi i forum per fare una domanda, contrassegnala con una tag in modo che sia visualizzabile dai team di sviluppo {{site.data.keyword.Bluemix_notm}}.
  * Se hai domande tecniche su {{site.data.keyword.appid_short_notm}}, inserisci la tua domanda in <a href="https://stackoverflow.com/search?q=ibm-appid" target="_blank">Stack Overflow <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> e contrassegnala con la tag "ibm-appid".
  * Per domande sul servizio e sulle istruzioni per l'utilizzo iniziale, utilizza il forum <a href="https://developer.ibm.com/answers/topics/appid/" target="_blank">dW Answers <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>. Includi la tag `appid`.

Per ulteriori informazioni su come ottenere supporto, vedi [Come posso ottenere il supporto di cui ho bisogno](/docs/get-support/howtogetsupport.html#getting-customer-support).

</br>

## Un URL personalizzato viene rifiutato
{: #ts-custom-url}


{: tsSymptoms}
Quando immetti un URL di reindirizzamento web che utilizza uno schema URL personalizzato, tale URL viene rifiutato dalla console {{site.data.keyword.appid_short_notm}}.

{: tsCauses}
Il tuo URL potrebbe venire rifiutato per i seguenti motivi:

* L'URL non segue uno schema `http` o `https` 
* L'URL termina con `://`
* È presente un errore tipografico nel tuo URL.

Vengono adottate delle limitazioni per motivi di sicurezza.

{: tsResolve}
Per risolvere il problema, verifica che l'URL sia corretto. Se il tuo URL non soddisfa i requisiti, puoi creare un endpoint HTTPS nella tua applicazione per reindirizzare il codice di concessione al tuo URL personalizzato. Specifica l'endpoint creato come tuo URL di reindirizzamento nella console {{site.data.keyword.appid_short_notm}}.

</br>
