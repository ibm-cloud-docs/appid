---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-10"

keywords: authentication, authorization, identity, app security, secure, tokens, jwt, development

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


# Convalida dei token
{: #token-validation}

La convalida dei token è una parte importante dello sviluppo dell'applicazione moderno. Convalidando i token, puoi proteggere la tua applicazione o le tue API da utenti non autorizzati. {{site.data.keyword.appid_full}} utilizza i token di accesso e identità per assicurarti che un utente o un'applicazione sia autenticato prima che gli venga concesso l'accesso. Se stai utilizzando uno degli SDK forniti da {{site.data.keyword.appid_short_notm}}, l'ottenimento e la convalida dei tuoi token vengono fatti al tuo posto.
{: shortdesc}

Per ulteriori informazioni su come vengono utilizzati i token in {{site.data.keyword.appid_short_notm}}, consulta [Descrizione dei token](/docs/services/appid?topic=appid-tokens#tokens).
{: tip}

I token sono utilizzati per verificare che una persona è chi dice di essere. Confermano tutte le autorizzazioni di accesso che un utente potrebbe contenere, per una durata specificata. Quando un utente accede alla tua applicazione e viene emesso un token, la tua applicazione deve convalidare l'utente prima che gli venga fornito l'accesso.

</br>

**Cosa succede se sto lavorando con un linguaggio per cui {{site.data.keyword.appid_short_notm}} non ha un SDK?**

Non preoccuparti. Hai tre opzioni:

* Utilizza le API {{site.data.keyword.appid_short_notm}}
* Implementa la tua logica di convalida
* Utilizza un qualsiasi SDK open source conforme con OIDC

In base ai feedback, l'opzione 1 è normalmente quella più semplice.
{: tip}

</br>
</br>

## Utilizzo delle API {{site.data.keyword.appid_short_notm}}
{: #remote-validation}

Utilizzando l'introspezione, puoi utilizzare {{site.data.keyword.appid_short_notm}} per convalidare i tuoi token.
{: shortdesc}

1. Invia una richiesta POST all'endpoint API [/introspect](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Authorization%20Server%20-%20Authorization%20Server%20V4/oauth-server.token) per convalidare il tuo token. La richiesta deve fornire il token e un'intestazione di autorizzazione di base che contiene il segreto e l'ID client.

  Richiesta di esempio:

    ```
    POST /oauth/v4/{tenant_id}/introspect HTTP/1.1
    Host: us-south.appid.cloud.ibm.com
    Content-Type: application/x-www-form-urlencoded
    Authorization: Basic jdFlUaGlZUzAwTW0Tjk15TmpFMw==
    Cache-Control: no-cache

    token=XXXXX.YYYYY.ZZZZZ
    ```
    {: screen}

2. Il server controlla la scadenza e la firma del token e restituisce un oggetto JSON che indica se il token è attivo o meno.

  Risposta di esempio:

    ```
    {
      "active": true
    }
    ```
    {: screen}


## Convalida manuale dei token
{: #local-validation}

Puoi convalidare i tuoi token localmente analizzando il token, verificandone la firma e convalidando le attestazioni archiviate nel token.
{: shortdesc}


1. Analizza i token. Il [JSON Web Token (JWT)](https://tools.ietf.org/html/rfc7519) è un modo standard di trasmettere in modo sicuro le informazioni. È composto da tre parti principali: intestazione, payload e firma. Sono codificati base64URL e separati da un punto(.). Puoi utilizzare qualsiasi decodificatore base64URL disponibile per analizzare il token. In alternativa, puoi utilizzare una qualsiasi delle [librarie elencate](https://jwt.io/#libraries-io) per analizzare il token.

  Token codificato di esempio:

    ```
    eyJhbGciOiJSUzI1NiIsInR5cCI6IkpPU0UiLCJraWQiOiJhMmszIn0
    .eyJpc3MiOiJhcHBpZC1vYXV0aCIsImF1ZCI6ImFiYzEyMyIsImV4cCI6MTU2NDU2Nn0
    .IycnAGUmMHzpTWbe-qaRsx0B4Zi-SVav710Fb_8CTCQvLrHX9d42WuCZ5bW
    d-ikgEsf6waQxeBfhfwYxwHN87LZupApagVMZtylVAnXhG1pHu_32wbZsPvg6QjzNO
    j6ys2Lfl3qfb5Qrp9u4IsZltKPEN8HdfeOcKXxpw6UqP-8
    ```
    {: screen}

  Intestazione decodificata di esempio

    ```
    {
      "alg": "RS256",
      "typ": "JOSE",
      "kid": "a2k3"
    }
    ```
    {: screen}

  Payload decodificato:

    ```
    {
      "iss": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61",
      "aud": "abc123",
      "exp": 1564566
    }
    ```
    {: screen}

2. Effettua una chiamata all'endpoint [/publickeys](https://us-south.appid.cloud.ibm.com/swagger-ui/#!/Authorization_Server_V4/publicKeys) per richiamare le tue chiavi pubbliche. Le chiavi pubbliche che vengono restituite sono formattate come [JSON Web Keys (JWK)](https://tools.ietf.org/html/rfc7517).

  Richiesta di esempio:

    ```
    GET /oauth/v4/{tenant_id}/publickeys HTTP/1.1
    Host: us-south.appid.cloud.ibm.com
    Cache-Control: no-cache
    ```
    {: screen}

3. Memorizza le chiavi nella tua cache dell'applicazione per un utilizzo futuro. La memorizzazione delle chiavi velocizza il processo e previene il ritardo di rete se viene effettuata un'altra chiamata.

4. Importa i parametri della chiave pubblica.

  Risposta di esempio:

    ```
    {
      "keys": [
        {
          "kty": "RSA",
          "use": "sig",
          "n": "AsdaE",
          "e": "SDAasw",
          "kid": "ad123dCAz"
        }
      ]
    }
    ```
    {: screen}

  <table>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="Icona ulteriori informazioni"/> Parametri della chiave pubblica </th>
    </thead>
    <tbody>
      <tr>
        <td><code>kty</code></td>
        <td>Definisce l'algoritmo che viene utilizzato.</td>
      </tr>
      <tr>
        <td><code>use</code></td>
        <td>Definisce l'ambito della chiave.</td>
      </tr>
      <tr>
        <td><code>kid</code></td>
        <td>Definisce l'ID univoco della chiave.</td>
      </tr>
      <tr>
        <td>Altro</td>
        <td>Potrebbero esserci anche degli altri parametri rimanenti che sono specifici per il tuo algoritmo che devono essere importati.</td>
      </tr>
    </tbody>
  </table>

5. Verifica la firma del token. L'intestazione del token contiene l'algoritmo che è stato utilizzato per firmare il token e l'ID della chiave o l'attestazione `kid` della chiave pubblica corrispondente. Poiché le chiavi pubbliche non vengono modificate frequentemente, puoi memorizzare nella cache le chiavi pubbliche nella tua applicazione e occasionalmente aggiornarle. Se alla tua chiave memorizzata nella cache manca l'attestazione `kid`, puoi convalidare i token localmente.

  1. Chiedi alla tua applicazione di verificare che i contenuti dell'intestazione del token in entrata corrispondano ai parametri della chiave pubblica.
  2. Controlla nello specifico che siano stati utilizzati gli stessi algoritmi e che la tua cache della chiave pubblica contenga una chiave con l'ID della chiave pertinente.
  3. Assicurati che il tuo valore hash sia lo stesso di quello della firma del modulo PEM della chiave pubblica. Il tuo valore hash può essere ottenuto combinando ed eseguendo l'hash dell'intestazione del payload del token. Poiché questo processo può essere complesso da implementare manualmente, potrebbe essere utile utilizzare una delle [librerie elencate](https://jwt.io/) per convalidare la firma.

6. Convalida le attestazioni archiviate nei token. Per verificare dei controlli futuri, puoi utilizzare [questo elenco](http://openid.net/specs/openid-connect-core-1_0.html#IDTokenValidation).
  <table>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="Icona ulteriori informazioni"/> Attestazioni che devono essere convalidate </th>
    </thead>
    <tbody>
      <tr>
        <td><code>iss</code></td>
        <td>L'emittente deve essere lo stesso del server OAuth {{site.data.keyword.appid_short_notm}}.</td>
      </tr>
      <tr>
        <td><code>exp</code></td>
        <td>L'ora corrente deve essere inferiore all'ora di scadenza.</td>
      </tr>
      <tr>
        <td><code>aud</code></td>
        <td>I destinatari devono contenere l'ID client della tua applicazione.</td>
      </tr>
      <tr>
        <td><code>tenant</code></td>
        <td>Il tenant deve contenere l'ID tenant della tua applicazione.</td>
      </tr>
      <tr>
        <td><code>ambito</code></td>
        <td>L'ambito delle autorizzazioni che vengono concesse all'utente. Specifico per il token di accesso.</td>
      </tr>
    </tbody>
  </table>
