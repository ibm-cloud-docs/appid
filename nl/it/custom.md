---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-13"

keywords: authentication, authorization, identity, app security, secure, custom, proprietary, private key, public key, jwt

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

# Personalizzato
{: #custom-identity}

Puoi utilizzare il tuo provider di identità personalizzato quando esegui l'autenticazione. Il tuo provider di identità può conformarsi a qualsiasi meccanismo di autenticazione che non viene specificatamente supportato da {{site.data.keyword.appid_full}}, inclusa la proprietà.
{: shortdesc}

Quando {{site.data.keyword.appid_short_notm}} non fornisce il supporto diretto per un particolare provider di identità, puoi utilizzare il flusso di identità personalizzato per collegare il protocollo di autenticazione al flusso di autenticazione esistente di {{site.data.keyword.appid_short_notm}}. Ad esempio, vuoi utilizzare GitHub o LinkedIn per consentire agli utenti di accedere. Puoi utilizzare l'SDK esistente del provider di identità per facilitare le informazioni sull'autenticazione utente prima di impacchettarle e scambiarle con {{site.data.keyword.appid_short_notm}}. In molti scenari aziendali, un provider di identità legacy potrebbe utilizzare il proprio protocollo di autenticazione personalizzato, ma tuo vuoi ancora utilizzare le funzionalità di {{site.data.keyword.appid_short_notm}}. Per questo tipo di scenario, il flusso di identità personalizzato fornisce un mezzo disaccoppiato per autenticare in modo sicuro i tuoi utenti senza esporne le credenziali.

## Configurazione dell'identità personalizzata
{: #custom-configure}

Puoi utilizzare la seguente procedura per configurare il tuo provider di identità personalizzato per l'utilizzo con {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

### Prima di cominciare
{: #custom-identity-before}

Per stabilire l'affidabilità tra {{site.data.keyword.appid_short_notm}} e il tuo provider di identità personalizzato, devi avere una coppia di chiavi RSA PEM con una lunghezza minima di 2048. Assicurati di aver eseguito in modo sicuro il backup di tutte le chiavi che utilizzi nella produzione.

Come vengono utilizzate le chiavi?

- La tua chiave privata viene utilizzata nella tua applicazione o nel tuo provider di identità per firmare i JWT.
- La tua chiave pubblica viene utilizzata da {{site.data.keyword.appid_short_notm}} per convalidare il JWT che contiene le informazioni utente.

Per generare una coppia di chiavi RSA PEM utilizzando Open SSL, immetti il seguente comando:

```
$ openssl genpkey -algorithm RSA -out private_key.pem -pkeyopt rsa_keygen_bits:2048
$ openssl rsa -pubout -in private_key.pem -out public_key.pem
```
{: codeblock}

</br>

### Configurazione con la GUI
{: #custom-identity-configure-gui}

1. Accedi al tuo account {{site.data.keyword.cloud_notm}} e passa alla tua istanza di {{site.data.keyword.appid_short_notm}}.

2. Nella scheda **Manage**, imposta **Custom Identity Provider** su **On**.

3. Registra la tua chiave pubblica con {{site.data.keyword.appid_short_notm}}.
  1. Passa alla scheda **Custom Identity Provider**
  2. Incolla la tua chiave pubblica nella casella **Public Key** e fai clic su **Save**.



### Configurazione con l'API
{: #custom-identity-configure-api}

Registra la tua chiave eseguendo una richiesta PUT all'[Endpoint API di gestione](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_custom_idp).

```
Put {Management URI}/config/idps/custom
Content-Type: application/json
{
    isActive: true,
    config: {
        publicKey: <Your newline separated (\n) PEM public key>
    }
}
```
{: codeblock}

## Verifica della configurazione
{: #custom-identity-testing}

Dopo aver configurato la tua istanza {{site.data.keyword.appid_short_notm}} con una chiave pubblica valida, puoi utilizzare l'applicazione di test fornita dal servizio per verificare che la tua configurazione sia configurata correttamente. Nell'applicazione di esempio, puoi visualizzare i payload del token di accesso e identità {{site.data.keyword.appid_short_notm}} restituiti durante un flusso di accesso standard.

1. Dalla scheda **Custom Identity Provider**, fai clic su **Test** per aprire l'applicazione di test.

2. Crea un [JWT di esempio](https://jwt.io/) che segue il [protocollo](/docs/services/appid?topic=appid-custom-auth#generating-jwts) dell'identità personalizzata.

3. Incolla il tuo JWT nella casella etichettata **JSON Web Token** e fai clic su **Test** per eseguire un'autenticazione di esempio.

Se ha esito positivo, puoi ora visualizzare i token di identità e accesso {{site.data.keyword.appid_short_notm}} decodificati che saranno disponibili per la tua applicazione in un flusso di accesso standard.

## Passi successivi
{: #custom-identity-next}

Ora che è stato configurato il tuo provider di identità personalizzato, [aggiungilo alla tua applicazione](/docs/services/appid?topic=appid-custom-auth#custom-auth)!
