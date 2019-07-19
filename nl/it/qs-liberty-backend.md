---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-11"

keywords: Authentication, authorization, identity, app security, secure, development, access management, liberty, backend, java, token

subcollection: appid

---

{:external: target="_blank" .external}
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


# Backend: Liberty for Java
{: #backend-liberty}

Con {{site.data.keyword.appid_short_notm}}, puoi facilmente proteggere i tuoi endpoint API e garantire la sicurezza delle tue applicazioni di backend Liberty for Java. Con questa guida, puoi ottenere rapidamente un semplice flusso di autenticazione operativo in meno di 20 minuti.
{: shortdesc}


![Applicazioni Liberty for Java di backend](images/backend_liberty.png)

1. Per effettuare una richiesta a una risorsa protetta, un client deve disporre di un token di accesso. Nel passo 1, il client effettua una richiesta a {{site.data.keyword.appid_short_notm}} per un token. Per ulteriori informazioni sull'ottenimento di token di accesso, vedi [Ottenimento dei token](/docs/services/appid?topic=appid-obtain-tokens).
2. {{site.data.keyword.appid_short_notm}} restituisce i token.
3. Utilizzando il token di accesso, il client effettua una richiesta per accedere alla risorsa protetta.
4. Il processo convalida il token, compresi struttura, scadenza, firma, destinatari e qualsiasi altro campo presente. Se il token non è valido, il server delle risorse nega l'accesso. Se la convalida del token ha esito positivo, restituisce i dati.


## Esercitazione video
{: #backend-liberty-video}

Guarda il seguente video per vedere come puoi utilizzare {{site.data.keyword.appid_short_notm}} per proteggere una semplice applicazione Liberty for Java. Tutte le informazioni trattate nel video possono essere trovate anche in forma scritta in questa pagina.

<iframe class="embed-responsive-item" id="appid-liberty-backend-app" title="Informazioni su {{site.data.keyword.appid_short_notm}}" type="text/html" width="640" height="390" src="//www.youtube.com/embed/QA6DY2qqLaw?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>

Non hai un'applicazione con cui puoi provare il flusso? Nessun problema! {{site.data.keyword.appid_short_notm}} fornisce una [semplice applicazione di esempio Liberty for Java](https://github.com/ibm-cloud-security/appid-video-tutorials/tree/master/02d-simple-liberty-backend-app).


## Prima di cominciare
{: #liberty-before}

Prima di iniziare con {{site.data.keyword.appid_short_notm}} nella tua applicazione di backend Liberty for Java, devi disporre dei seguenti prerequisiti:

* Un'istanza del [servizio {{site.data.keyword.appid_short_notm}}](https://cloud.ibm.com/catalog/services/app-id){: external}
* [La CLI di IBM Cloud](/docs/cli?topic=cloud-cli-getting-started)
* [Apache Maven 3.5+](https://maven.apache.org/download.cgi){: external}
* [Java 8+](https://www.java.com/download/){: external}
* La [{{site.data.keyword.appid_short_notm}} Postman Collection](https://github.com/ibm-cloud-security/appid-postman){: external} per l'esecuzione di test

## Passo 1: Ottieni le tue credenziali
{: #liberty-obtain-credentials}

Puoi ottenere le tue credenziali in uno dei due modi di seguito indicati.

  * Passando alla scheda **Applications** del dashboard {{site.data.keyword.appid_short_notm}}. Se non ne hai già una, puoi fare clic su **Add application** per crearne una nuova.

  * Eseguendo una richiesta POST all'[endpoint `/management/v4/{tenantId}/applications`](https://us-south.appid.cloud.ibm.com/swagger-ui/#!/Applications/registerApplication){: external}.

    Formato della richiesta:
    ```
    curl -X POST \  https://us-south.appid.cloud.ibm.com/management/v4/<tenantID>/applications/ \
    -H 'Content-Type: application/json' \
    -H 'Authorization: Bearer IAM_TOKEN' \
    -d '{"name": "ApplicationName"}'
    ```
    {: codeblock}

    Risposta di esempio:
    ```
    {
      "clientId": "xxxxx-34a4-4c5e-b34d-d12cc811c86d",
      "tenantId": "xxxxx-9b1f-433e-9d46-0a5521f2b1c4",
      "secret": "ZDk5YWZkYmYt*******",
      "name": "app1",
      "oAuthServerUrl": "https://us-south.appid.cloud.ibm.com/oauth/v4/xxxxx-9b1f-433e-9d46-0a5521f2b1c4",
      "profilesUrl": "https://us-south.appid.cloud.ibm.com",
      "discoveryEndpoint": "https://us-south.appid.cloud.ibm.com/oauth/v4/xxxxxx-9b1f-433e-9d46-0a5521f2b1c4/.well-known/openid-configuration"
    }
    ```
    {: screen}


## Passo 2: Configura il tuo file `server.xml`
{: #liberty-configure-server}
 
1. Apri il tuo file `server.xml`.
2. Aggiungi le seguenti funzioni alla sezione `featureManager`. Alcune funzioni potrebbero essere integrate con Liberty. Se ricevi un errore quando esegui il tuo server, puoi installarle eseguendo `.installUtility install <name_of_server>` dalla directory bin della tua installazione Liberty.

    ```xml
    <featureManager>
        <feature>appSecurity-2.0</feature>
        <feature>openidConnectClient-1.0</feature>
        <feature>ssl-1.0</feature>
        <feature>servlet-3.1</feature>
    </featureManager>
    ```
    {: codeblock}

3. Configura SSL aggiungendo quanto segue al tuo file `server.xml`. 

    ```xml
    <keyStore id="defaultKeyStore" password="{password}"/>
    <keyStore id="RootCA" password="{password}" location="${server.config.dir}/resources/security/{myTrustStore}"/>
    <ssl id="{sslID}" keyStoreRef="defaultKeyStore" trustStoreRef="{truststore-ref}"/>
    ```
    {: codeblock}

4. Crea una funzione Open ID Connect Client e definisci i seguenti segnaposto. Con le credenziali che hai ottenuto, compila i segnaposto.

    ```xml
    <openidConnectClient
        id="oidc-client-simple-liberty-backend-app" 		
        inboundPropagation="required"
        jwkEndpointUrl="{region}.appid.cloud.ibm.com/oauth/v4/{tenantID}/publickeys"
        issuerIdentifier="{region).appid.cloud.ibm.com/oauth/v4/{tenantID}"
        signatureAlgorithm="RS256"
        audiences="{client-id}"
        sslRef="oidcClientSSL"
    /> 	
    ```
    {: codeblock}

    <table>
    <caption>Tabella. Variabili dell'elemento OIDC per le applicazioni Liberty for Java</caption>
        <tr>
            <th colspan="2"> Descrizione delle variabili di elemento OIDC</th>
        </tr>
        <tr>
            <td><code>id </code></td>
            <td>Il nome della tua applicazione.</td>
        </tr>
        <tr>
            <td><code>inboundPropagation</code></td>
            <td>Per propagare le informazioni ricevute nel token, il valore deve essere impostato su "required".</td>
        </tr>
        <tr>
            <td><code>jwkEndpointUrl</code></td>
            <td>L'endpoint che viene utilizzato per ottenere le chiavi per convalidare il token. Le opzioni di regione includono: <code>au-syd</code>, <code>eu-de</code>, <code>eu-gb</code>, <code>jp-tok</code> e <code>us-south</code>. Puoi trovare il tuo ID tenant nelle credenziali che hai creato in precedenza.</td>
        </tr>
        <tr>
            <td><code>issuerIdentifier</code></td>
            <td>L'identificativo dell'emittente definisce il tuo server di autorizzazione. Le opzioni di regione includono: <code>au-syd</code>, <code>eu-de</code>, <code>eu-gb</code>, <code>jp-tok</code> e <code>us-south</code>. Puoi trovare il tuo ID tenant nelle credenziali che hai creato in precedenza.</td>
        </tr>
        <tr>
            <td><code>signatureAlgorithm</code></td>
            <td>Specificata come "RS256".</td>
        </tr>
        <tr>
            <td><code>audiences</code></td>
            <td>Per impostazione predefinita, il token viene emesso per il tuo ID client {{site.data.keyword.appid_short_notm}} che può essere trovato nelle tue credenziali dell'applicazione.</td>
        </tr>
        <tr>
            <td><code>sslRef</code></td>
            <td>Il nome della configurazione SSL che vuoi utilizzare.</td>
        </tr>
    </table>

5. Definisci il tuo tipo di oggetto speciale come `ALL_AUTHENTICATED_USERS`.

    ```xml
    <application
        id="simple-liberty-backend-app"
        location="location-of-your-war-file"
        name="simple-liberty-backend-app"
        type="war">

        <application-bnd>
            <security-role name="myrole">
                <special-subject type="ALL_AUTHENTICATED_USERS"/>
            </security-role>
        </application-bnd>
    </application>
    ```
    {: codeblock}


## Passo 3: Configura il tuo file `web.xml`
{: #liberty-configure-web}

Nel tuo file `web.xml`, definisci le aree della tua applicazione che vuoi proteggere.

1. Definisci un ruolo di sicurezza. Questo dovrebbe essere lo stesso ruolo che hai definito nel file `server.xml`.

    ```
    <security-role>
		<role-name>myrole</role-name>
	</security-role>
    ```
    {: codeblock}

2. Definisci un vincolo di sicurezza.

    ```
	<security-constraint>
		<display-name>Security Constraints</display-name>
		<web-resource-collection>
			<web-resource-name>ProtectedArea</web-resource-name>
			<url-pattern>/api/*</url-pattern>
		</web-resource-collection>
		<auth-constraint>
			<role-name>myrole</role-name>
		</auth-constraint>
		<user-data-constraint>
			<transport-guarantee>NONE</transport-guarantee>
		</user-data-constraint>
	</security-constraint>
    ```
    {: codeblock}


## Passo 4: Verifica la tua configurazione
{: #liberty-test}

Ora che hai completato l'installazione iniziale, crea l'applicazione e verifica la tua configurazione per assicurarti che tutto stia funzionando come previsto.

1. Passa alla directory della tua applicazione.

2. Crea la tua applicazione.

    ```
    server run
    ```
    {: codeblock}

3. Effettua una richiesta all'endpoint protetto. Viene restituito un errore.

4. [Ottieni un token di accesso](/docs/services/appid?topic=appid-obtain-tokens).

5. Con il token di accesso che hai ottenuto nel passo precedente, effettua una richiesta all'endpoint. Ora dovresti essere in grado di accedere all'endpoint protetto. Verifica che la risposta contenga quanto previsto.


## Passi successivi
{: #liberty-next}

Pronto a cominciare a perfezionare la tua esperienza di autenticazione? Prova a esplorare [questo blog](https://www.ibm.com/cloud/blog/perfecting-the-login-experience-with-liberty-oauth2-and-appid){: external} o ad accedere a ulteriori informazioni sulle [comunicazioni da applicazione ad applicazione](/docs/services/appid?topic=appid-app).


