---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:faq: data-hd-content-type='faq'}


# Domande frequenti (FAQ)
{: #faq}

Questa FAQ fornisce risposte a domande comuni sul servizio {{site.data.keyword.appid_full}}.
{: shortdesc}


## Come {{site.data.keyword.appid_short_notm}} calcola i prezzi?
{: #pricing}
{: faq}

Con {{site.data.keyword.appid_short_notm}}, paghi meno rispetto all'utilizzo di ulteriori risorse.
{: shortdesc}

Il piano di livello graduale è composto da tre parti: il numero di eventi di autenticazione, la sicurezza avanzata e regolare e il numero di utenti autorizzati. Ti viene effettuato un addebito ogni mese, in base al riepilogo delle due parti. Il prezzo totale è l'addebito cumulativo per ogni livello di utilizzo, che consiste dalla tua quantità moltiplicata per il prezzo unitario di quel livello.

I tuoi primi 1000 eventi di autenticazione e i primi 1000 utenti autorizzati sono gratuiti ogni mese, con l'eccezione di tutti gli eventi di sicurezza avanzata. Gli eventi di sicurezza avanzata comportano degli ulteriori costi.

### Eventi di autenticazione

Un evento di autenticazione si verifica quando viene emesso un nuovo token regolare o anonimo. I token possono essere emessi come una risposta a una richiesta di accesso iniziata da un utente o al posto dell'utente da un'applicazione. Per impostazione predefinita, i token di accesso sono validi per un'ora e i token anonimi per 30 giorni. Dopo che il token scade, devi creare un nuovo token per accedere alle risorse protette. Puoi aggiornare il tempo di scadenza dei tuoi token {{site.data.keyword.appid_short_notm}} nella pagina **Sign-in Expiration** del dashboard del servizio.

#### Funzioni di sicurezza avanzate

Le funzioni di sicurezza avanzate ti forniscono la possibilità di rafforzare la sicurezza della tua applicazione.
{: shortdesc}

<table>
  <tr>
    <th>Funzione</th>
    <th>Vantaggio</th>
  </tr>
  <tr>
    <td>Autenticazione multifattore </td>
    <td>[MFA for Cloud Directory](mfa.html) conferma l'identità di un utente richiedendo a un utente di immettere un passcode monouso inviato alla sua email in aggiunta all'immissione di email e password.</td>
  </tr>
  <tr>
    <td>Gestione della politica della password</td>
    <td>Come proprietario dell'account, puoi applicare password più sicure per Cloud Directory configurando una serie di regole a cui devono conformarsi le password degli utenti. Gli esempi includono, il numero di accessi tentati prima del blocco, le date di scadenza, l'intervallo di tempo minimo tra gli aggiornamenti della password o il numero di volte in cui può essere ripetuta una password. Per un elenco completo delle opzioni e delle informazioni di configurazione, consulta [Gestione della password avanzata](cloud-directory.html#advanced-password).</td>
  </tr>
</table>

Per impostazione predefinita, le funzioni di sicurezza avanzate sono disabilitate. Se attivi l'autenticazione multifattore o la gestione della politica della password ti verrà addebitato un ulteriore costo. Se disabiliti tutte le funzioni avanzate, il tuo account tornerà alla politica di basso costo. Ad esempio, se hai ottenuto 10.000 token di accesso. Hai poi attivato MFA e la gestione della politica della password e ne hai ottenuti altri 10.000. Pagherai 20.000 eventi di autenticazione e 10.000 eventi di sicurezza avanzata.

Queste funzioni sono disponibili solo per le istanze presenti sul piano dei prezzi di livello graduale e che sono state create dopo il 15 marzo 2018.
{: note}

### Utenti autorizzati

Un utente autorizzato è un utente univoco che accede al tuo servizio direttamente o indirettamente, inclusi gli utenti anonimi. Ti viene effettuato un addebito per un utente autorizzato ogni volta che un nuovo utente accede alla tua applicazione, inclusi gli utenti anonimi. Ad esempio, se un utente accede con Facebook e successivamente utilizzando Google, viene considerato come due utenti autorizzati separati.

Per delle informazioni sui prezzi più aggiornate per {{site.data.keyword.appid_short_notm}}, consulta il [calcolatore dei prezzi](https://console.cloud.ibm.com/pricing/configure/service/AdvancedMobileAccess-d6aece47-d840-45b0-8ab9-ad15354deeea).
{: important}

</br>


## Perché devo inserire nella whitelist il mio URL di reindirizzamento?
{: #redirect}
{: faq}

Un URL di reindirizzamento è l'endpoint di callback della tua applicazione. Per impedire gli attacchi di phishing, {{site.data.keyword.appid_short_notm}} convalida l'URL rispetto alla whitelist degli URL di reindirizzamento. Quando si verifica il phishing, esiste la possibilità che un aggressore possa accedere ai token dei tuoi utenti.

Per aggiungere il tuo URL alla whitelist:

1. Passa a **Identity Providers > Manage**.
2. Nel campo **Add web redirect URL**, immetti l'URL e fai clic su **+**.

Non includere parametri di query nel tuo URL. Vengono ignorati nel processo di convalida. URL di esempio: `http://host:[port]/path`
{: tip}

</br>

## Come funziona la crittografia in {{site.data.keyword.appid_short_notm}}?
{: #encryption}
{: faq}

Consulta la seguente tabella per le risposte alle domande più frequenti sulla crittografia.

<table>
  <thead>
    <th colspan=2><img src="images/idea.png" alt="Icona ulteriori informazioni"/>  </th>
  </thead>
  <tbody>
    <tr>
      <td>Perché utilizzate la crittografia?</td>
      <td>Un modo con cui proteggiamo le informazioni dei nostri utenti è di codificare i dati del cliente quando inattivi. Il servizio codifica i dati del cliente quando inattivi con le chiavi per tenant.</td>
    </tr>
    <tr>
      <td>Avete creato i vostri algoritmi? Quali utilizzate nel vostro codice?</td>
      <td>Non abbiamo creato i nostri, il servizio utilizza <code>AES</code> e <code>SHA-256</code> con salting.</td>
    </tr>
    <tr>
      <td>Utilizzate provider o moduli di crittografia open source o pubblici? Avete mai esposto le funzioni di crittografia? </td>
      <td>Il servizio utilizza le librerie Java <code>javax.crypto</code>, ma non espone mai le funzioni di crittografia.</td>
    </tr>
    <tr>
      <td>Come memorizzate le chiavi?</td>
      <td>Le chiavi sono generate, codificate con una chiave master specifica per ogni regione e poi archiviate localmente. Le chiavi master sono memorizzate in {{site.data.keyword.keymanagementserviceshort}}. Ai livelli di archiviazione e middleware, è presente la crittografia al livello del servizio, ossia è presente una chiave per tutti i clienti. Al livello dell'applicazione, ogni cliente ha la propria chiave di crittografia.</td>
    </tr>
    <tr>
      <td>Quale è la complessità della chiave che utilizzate?</td>
      <td>Il servizio utilizza 16 byte.</td>
    </tr>
    <tr>
      <td>Richiamate delle API remote che espongono le funzionalità di crittografia?</td>
      <td>No, non lo facciamo.</td>
    </tr>
  </tbody>
</table>

</br>

## Quale aspetto deve avere un'asserzione SAML per {{site.data.keyword.appid_short_notm}}?
{: #saml-example}
{: faq}

Il servizio prevede che un'asserzione SAML sia simile al seguente esempio.

```
<samlp:Response xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol" ID="s2202bbbbafa9d270d1c15990b738f4ab36139d463" InResponseTo="_e4a78780-35da-012e-8ea7-0050569200d8" Version="2.0" IssueInstant="2011-03-21T11:22:02Z" Destination="https://example.example.com/">
  <saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">idp_entityId</saml:Issuer>
  <samlp:Status xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <samlp:StatusCode  xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol"Value="urn:oasis:names:tc:SAML:2.0:status:Success"/>
  </samlp:Status>
  <saml:Assertion xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="2.0" ID="pfx539c9774-de5c-5f52-0c3f-b1c2e2697a89" IssueInstant="2018-01-29T13:02:58Z" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <saml:Issuer>idp_entityId</saml:Issuer>
    <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      <ds:SignedInfo>
        <ds:CanonicalizationMethod Algorithm="one_of_supported_algo"/>
        <ds:SignatureMethod Algorithm="one_of_supported_algo"/>
        <ds:Reference URI="#pfx539c9774-de5c-5f52-0c3f-b1c2e2697a89">
          <ds:Transforms>
            <ds:Transform Algorithm="one_of_supported_algo"/>
            <ds:Transform Algorithm="one_of_supported_algo"/>
          </ds:Transforms>
          <ds:DigestMethod Algorithm="one_of_supported_algo"/>
          <ds:DigestValue>huywDPPfOEGyyzE7d5hjOG97p7FDdGrjoSfes6RB19g=</ds:DigestValue>
        </ds:Reference>
      </ds:SignedInfo>
 <ds:SignatureValue>BAwNZFgWF2oxD1ux0WPfeHnzL+IWYqGhkM9DD28nI9v8XtPN8tqmIb5y4bomaYknmNpWYn7TgNO2Rn/XOq+N9fTZXO2RybaC49iF+zWibRIcNwFKCCpDL6H6jA5eqJX2YKBR+K6Yt2JPoUIRLmqdgm2lMr4Nwq1KYcSzQ/yoV5W0SN/V5t8EfctFoaXVPdtfHVXkwqHeufo+L4gobFt9NRTzXB0SQEClA1L8hQ+/LhY4l46k1D0c34iWjVLZr+ecQyubf7rekOG/R7DjWCFMTke822dR+eJTPWFsHGSPWCDDHFYqB4QMinTvUnsngjY3AssPqIOjeUxjL3p+GXn8IQ==</ds:SignatureValue>
    </ds:Signature>
    <saml:Subject>
      <saml:NameID Format="urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress">JohnDoe@gmail.com</saml:NameID>
    </saml:Subject>
    <saml:Conditions NotBefore="2018-01-29T12:59:58Z" NotOnOrAfter="2018-01-29T13:05:58Z">
    </saml:Conditions>
</samlp:Response>
```
{: screen}

</br>

## Quali tipi di algoritmi sono supportati per le firme SAML?
{: #saml-signatures}
{: faq}

Puoi utilizzare uno dei seguenti algoritmi per elaborare le firme digitali XML.

<table>
  <tr>
    <th> Tipo di algoritmo </th>
    <th> Opzioni di algoritmo </th>
  </tr>
  <tr>
    <td>Algoritmi di canonicalizzazione e trasformazione con e senza commenti</td>
    <td><ul><li><a href="http://www.w3.org/TR/2001/REC-xml-c14n-20010315" target="_blank">Canonicalizzazione <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></li>
    <li><a href="http://www.w3.org/2001/10/xml-exc-c14n#" target="_blank">Canonicalizzazione esclusiva con e senza commenti <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></li>
    <li><a href=" http://www.w3.org/2000/09/xmldsig#enveloped-signature" target="_blank">Trasformazione di firma in busta <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></li></ul></td>
  </tr>
  <tr>
    <td>Algoritmi di hash</td>
    <td><ul><li><a href="http://www.w3.org/2000/09/xmldsig#sha1" target="_blank">Digest SHA1 <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmlenc#sha256" target="_blank">Digest SHA256 <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmlenc#sha512" target="_blank">Digest SHA512 <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></li></ul></td>
  </tr>
  <tr>
    <td>Algoritmi di firma</td>
    <td><ul><li><a href="http://www.w3.org/2000/09/xmldsig#rsa-sha1" target="_blank">RSA-SHA1 <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmldsig-more#rsa-sha256" target="_blank">RSA-SHA256 <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></li>
    <li><a href="http://www.w3.org/2001/04/xmldsig-more#rsa-sha512" target="_blank">RSA-SHA512 <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></li>
    <li><a href="http://www.w3.org/2000/09/xmldsig#hmac-sha1" target="_blank">HMAC-SHA1 <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></li></ul></td>
  </tr>
</table>

Per ulteriori informazioni sull'utilizzo di un provider di identità SAML, vedi [Configurazione di provider di identità aziendali](enterprise.html).
