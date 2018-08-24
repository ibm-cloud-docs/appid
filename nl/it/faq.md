---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}


# Domande frequenti (FAQ)

Questa FAQ fornisce risposte a domande comuni sul servizio {{site.data.keyword.appid_full}}.
{: shortdesc}


## Come {{site.data.keyword.appid_short_notm}} calcola i prezzi?
{: #pricing}

Con {{site.data.keyword.appid_short_notm}}, paghi meno rispetto all'utilizzo di ulteriori risorse.
{: shortdesc}

Il piano di livello graduale è composto da due parti: il numero di eventi di autenticazione e il numero di utenti autorizzati. Ti viene effettuato un addebito ogni mese, in base al riepilogo delle due parti. Il prezzo totale è l'addebito cumulativo per ogni livello di utilizzo, che consiste dalla tua quantità moltiplicata per il prezzo unitario di quel livello.

### Eventi di autenticazione

Un evento di autenticazione si verifica quando viene emesso un nuovo token regolare o anonimo. Per gli utenti identificati, ogni nuovo token di accesso è valido per impostazione predefinita per 1 ora (tramite l'autenticazione utente reale o mediante i token di aggiornamento). I token anonimi sono validi per impostazione predefinita per 1 mese. Dopo che il token scade, devi creare un nuovo token per accedere alle risorse protette. Puoi aggiornare il tempo di scadenza dei token {{site.data.keyword.appid_short_notm}} nella pagina **Sign-in Expiration** nel dashboard {{site.data.keyword.appid_short_notm}}.

Quando utilizzi {{site.data.keyword.appid_short_notm}} nelle applicazioni mobili, i token vengono memorizzati in keystore o keychain e vengono aggiunti ad ogni richiesta futura. È possibile accedere ai token utilizzando l'SDK iOS o Android ID applicazione. Quando utilizzi {{site.data.keyword.appid_short_notm}} nelle applicazioni web, si consiglia di memorizzare i token nei cookie di sessione dell'applicazione.


### Utenti autorizzati

Un utente autorizzato è un utente univoco che accede al tuo servizio direttamente o indirettamente. Ti viene effettuato un addebito per un utente autorizzato ogni volta che un nuovo utente accede da ogni provider di identità, inclusi gli utenti anonimi. Ad esempio, se un utente accede con Facebook e successivamente utilizzando Google, vengono considerati due utenti autorizzati separati.

Per ulteriori informazioni sui prezzi del livello graduale, consulta la [Documentazione dei prezzi di {{site.data.keyword.Bluemix_notm}}](/docs/billing-usage/how_charged.html#services).

</br>


## Come funziona la crittografia in {{site.data.keyword.appid_short_notm}}?
{: #encryption}

Consulta la seguente tabella per le risposte alle domande più frequenti sulla crittografia.

<table>
  <thead>
    <th colspan=2><img src="images/idea.png" alt="Icona ulteriori informazioni"/>  </th>
  </thead>
  <tbody>
    <tr>
      <td>Perché utilizzate la crittografia?</td>
      <td>Il servizio codifica i dati del cliente a riposo.</td>
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
      <td>Le chiavi sono generate e poi memorizzate localmente dopo che sono state codificate utilizzando una chiave master specifica per ogni regione. Le chiavi master sono memorizzate in {{site.data.keyword.keymanagementserviceshort}}.</td>
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
