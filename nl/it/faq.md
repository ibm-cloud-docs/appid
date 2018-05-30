---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

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

Un evento di autenticazione si verifica quando viene emesso un nuovo token {{site.data.keyword.appid_short_notm}}. Per gli utenti identificati, ogni nuovo token è valido per 1 ora. I token anonimi sono validi per 1 mese. Dopo che il token scade, devi creare un nuovo token per accedere alle risorse protette. Quando utilizzi{{site.data.keyword.appid_short_notm}} per l'autenticazione mobile, i token utente vengono memorizzati in `key-store/key-chain` e vengono aggiunti a ogni richiesta futura. È possibile accedere ai token utilizzando l'SDK Android o iOS Swift {{site.data.keyword.appid_short_notm}}. Quando utilizzi il servizio per l'autenticazione web, <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">archivia il token dell'utente <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> nei cookie della sessione.

### Utenti autorizzati

Un utente autorizzato è un utente univoco che accede al tuo servizio direttamente o indirettamente. Ti viene effettuato un addebito per un utente autorizzato ogni volta che un nuovo utente accede da ogni provider di identità, inclusi gli utenti anonimi. Ad esempio, se un utente accede con Facebook e successivamente utilizzando Google, vengono considerati due utenti autorizzati separati.

Per ulteriori informazioni sui prezzi del livello graduale, consulta la [Documentazione dei prezzi di {{site.data.keyword.Bluemix_notm}}](/docs/billing-usage/how_charged.html#services).

</br>

## Che tipo di attività è monitorata da {{site.data.keyword.appid_short_notm}}?
{: #activity-monitor}

Puoi tenere traccia dell'attività che è stata generata all'interno dell'applicazione che è associata all'istanza del servizio. Puoi anche monitorare l'attività amministrativa effettuata in {{site.data.keyword.appid_short_notm}} utilizzando il servizio {{site.data.keyword.cloudaccesstrailshort}}.

Per visualizzare l'attività generata dalla tua applicazione:

1. Accedi al tuo account {{site.data.keyword.Bluemix_notm}}.
2. Dal dashboard, seleziona la tua istanza di {{site.data.keyword.appid_short_notm}}.
3. Fai clic sulla scheda **Panoramica**.
4. Visualizza l'attività elencata in **Log attività**.

</br>
Per monitorare l'attività amministrativa:

1. Accedi al tuo account {{site.data.keyword.Bluemix_notm}}. Passa all'organizzazione e allo spazio in cui è stato eseguito il provisioning della tua istanza {{site.data.keyword.appid_short_notm}}.
2. Dal catalogo, esegui il provisioning di un'istanza del servizio {{site.data.keyword.cloudaccesstrailshort}}. Assicurati di essere nello stesso spazio della tua istanza {{site.data.keyword.appid_short_notm}}.
3. Nel dashboard {{site.data.keyword.cloudaccesstrailshort}}, fai clic sulla scheda **Gestisci**.
4. Dall'elenco a discesa, seleziona le seguenti configurazioni per ricercare gli eventi generati da {{site.data.keyword.appid_short_notm}}.
<table>
  <tr>
    <th> Campo </th>
    <th> Configurazione </th>
  </tr>
  <tr>
    <td>Visualizza log</td>
    <td>Log spazio</td>
  </tr>
  <tr>
    <td>Ricerca</td>
    <td>target.name</td>
  </tr>
  <tr>
    <td>Filtro</td>
    <td>appid</td>
  </tr>
</table>
5. Fai clic su **Filtro**.

Consulta la [Documentazione di {{site.data.keyword.cloudaccesstrailshort}}](/docs/services/cloud-activity-tracker/index.html) per ulteriori informazioni su come funziona il servizio.

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
