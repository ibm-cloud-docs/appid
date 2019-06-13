---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-31"

keywords: authentication, authorization, identity, app security, secure, access management, roles, attributes, users

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


# Esercitazione: Impostazione dei ruoli utente
{: #tutorial-roles}

Assicurarsi che le persone giuste abbiano l'accesso corretto al momento adatto può essere difficile quando stai codificando la tua applicazione. Per facilitare tale processo, puoi utilizzare {{site.data.keyword.appid_full}} per definire un attributo personale come ad esempio `role`, che ti consente di assegnare diversi tipi di utenti. Puoi quindi utilizzare la tua applicazione per implementare diversi livelli di autorizzazioni per ciascun tipo di utente. Utilizzando questa guida dettagliata, puoi imparare a impostare gli attributi utente, ad aggiornarli e a inserirli quindi in un token utilizzando le API {{site.data.keyword.appid_short_notm}} .
{: shortdesc}

Non hai già esperienza con le API? Provale con questa [raccolta Postman](https://github.com/ibm-cloud-security/appid-postman).
{: tip}

## Scenario
{: #roles-scenario}

Sei uno sviluppatore per un parco a tema fittizio. Hai l'incarico di gestire l'accesso per l'[applicazione web](/docs/services/appid?topic=appid-web-apps) e ritieni che il modo più facile per farlo sia impostando dei ruoli per ciascun tipo di utente. Hai vari tipi diversi di ruoli, come ad esempio personale del parco e visitatori, e tutti hanno bisogno di livelli di autorizzazioni differenti. Vuoi poter ottimizzare il processo e garantire che ai tuoi utenti venga assegnato il ruolo corretto dalla prima volta che eseguono l'accesso alla tua applicazione.  
{: shortdesc}

Nessun problema! Puoi utilizzare la [funzione degli attributi personalizzati](/docs/services/appid?topic=appid-profiles) di {{site.data.keyword.appid_short_notm}} per memorizzare qualsiasi informazione correlata agli utenti. Quindi, poiché stai lavorando con un controllo dell'accesso basato sui ruoli, puoi creare un attributo denominato `role` e assegnare valori differenti per specificare un tipo di ruolo. Ad esempio, il parco a tema potrebbe avere `visitors` o `staff` che potrebbero essere ognuno dei valori differenti per l'attributo `role`. Puoi quindi garantire che il tuo codice applicativo implementi i privilegi e le politiche di accesso da te assegnati.

Anche se questa esercitazione è scritta specificamente pensando alle applicazioni web e a Cloud Foundry, gli attributi possono essere utilizzati in un senso molto più ampio. Gli attributi personalizzati possono essere qualsiasi cosa tu voglia. Puoi memorizzare tutti i tipi di informazione, a condizione che resti sotto i 100.000 attributi e li formatti come un oggetto JSON normale!
{: note}


## Prima di cominciare
{: #roles-before}

Pronto? Cominciamo!

Assicurati di avere i seguenti prerequisiti prima di iniziare:
- Un'istanza del servizio {{site.data.keyword.appid_short_notm}}
- Una serie di credenziali del servizio
- Un indirizzo email a cui puoi accedere e che puoi convalidare


## Passo 1: Configurazione della tua istanza {{site.data.keyword.appid_short_notm}}
{: #roles-configure-app}

Prima di poter iniziare ad aggiungere attributi per i tuoi utenti di Cloud Land, devi configurare la tua istanza di {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

1. Nella scheda **Identity Providers** del dashboard del servizio, abilita **Cloud Directory**. Anche se questa esercitazione utilizza [Cloud Directory](/docs/services/appid?topic=appid-cloud-directory), puoi anche scegliere di utilizzare uno qualsiasi degli altri provider di identità, come ad esempio [SAML](/docs/services/appid?topic=appid-enterprise), [Facebook](/docs/services/appid?topic=appid-social#facebook), [Google](/docs/services/appid?topic=appid-social#google) o un [provider personalizzato](/docs/services/appid?topic=appid-custom-identity).

2. Nella scheda **Cloud Directory > Email Verification**, abilita la verifica e imposta **Allow users to sign-in to your app without first verifying their email address** su **No**. Quando utilizzi gli attributi personalizzati per impostare i ruoli correlati alle autorizzazioni, assicurati che gli utenti debbano convalidare la loro identità prima di assumere gli attributi da te impostati.

3. Nella scheda **Profiles**, imposta **Change custom attributes from the app** su **Disabled**.

  Per impostazione predefinita, gli attributi personalizzati possono essere modificati da chiunque abbia un token di accesso. Per garantire la sicurezza dell'applicazione, devi configurare {{site.data.keyword.appid_short_notm}} in modo che gli attributi personalizzati possano essere modificati solo dall'amministratore o dal proprietario dell'applicazione. Ciò impedisce agli utenti di modificare i propri attributi personalizzati e di concedere a se stessi le autorizzazioni che non dovrebbero avere.
  {: important}

Eccellente! Il tuo dashboard è configurato e sei pronto a iniziare ad impostare i ruoli.


## Passo 2: Impostazione dei ruoli per conto di un altro utente prima dell'accesso
{: #roles-set-before}

Cloud Land ha un nuovo membro del personale! Conosci tutte le sue informazioni ma inizierà solo tra qualche giorno. Puoi [preregistrarlo](/docs/services/appid?topic=appid-preregister) creando un utente e un profilo {{site.data.keyword.appid_short_notm}} che contiene gli attributi quali ad esempio il ruolo `staff`.
{: shortdesc}

Questo processo non termina la registrazione di Cloud Directory. L'utente deve comunque eseguire la registrazione per l'applicazione per ereditare l'attributo nel profilo da te creato.
{: tip}

1. Esegui l'accesso a {{site.data.keyword.cloud_notm}} utilizzando la CLI.

  ```
  ibmcloud login
  ```
  {: codeblock}

2. Ottieni un token di accesso IAM.

  ```
  ibmcloud iam oauth-tokens
  ```
  {: codeblock}

3. Esegui una richiesta POST per creare un profilo utente per il nuovo utente che contiene l'attributo `staff`. Assicurati di poter accedere alla email che utilizzi e di poterla convalidare.

  ```
  curl --request POST \
  https://us-south.appid.cloud.ibm.com/management/v4/{{APPID_TENANT_ID}}/users \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  - d '{
    "idp": "cloud_directory",
    "idp-identity": “user@email.com“,
    "profile": {
      "attributes": {
        “role”: “staff”
      }
    }
  }'
  ```
  {: codeblock}

  Output di risposta di esito positivo:

  ```
  {
      "id": "5ty78b09-1356-4py8-l45p-808l633101zz"
  }
  ```
  {: screen}

6. Convalida che il profilo sia stato creato con il ruolo `staff`.

  ```
  curl --request GET \
  https://us-south.appid.cloud.ibm.com/management/v4/<tenant-ID>/users?email=<user-email> \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  ```
  {: codeblock}

  Corpo di risposta di esito positivo:

  ```
  {
      "users": [
          {
              "idp": "nominated_cloud_directory",
              "id": "5ty78b09-1356-4py8-l45p-808l633101zz"
          }
      ]
  }
  ```
  {: screen}

Ottimo lavoro! Hai preregistrato un utente per la tua applicazione. Ora, quando esegue l'accesso alla tua applicazione con l'identificativo che hai utilizzato per la preregistrazione, viene creato un utente Cloud Directory che eredita il profilo utente {{site.data.keyword.appid_short_notm}}. Impara quindi come aggiornare gli attributi.


## Passo 3: Aggiornamento degli attributi utente
{: #roles-update-attributes}

Cloud Land sta crescendo. Per tenere il passo con questa crescita, la tua azienda sta assumendo nuovo personale. L'utente `staff` dal passo 2 è ora un manager. Puoi aggiornare il suo profilo [assegnando un nuovo ruolo](/docs/services/appid?topic=appid-profiles#profile-set-custom).
{: shortdesc}

1. Aggiorna il profilo.

  ```
  curl --request PUT \
  https://us-south.appid.cloud.ibm.com/management/v4/<tenant-id>/users/<user-id>/profile \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  - d '{
    "profile": {
      "attributes": {
        “role”: “manager”
      }
    }
  }'
  ```
  {: codeblock}

3. Visualizza il profilo per verificare che sia stato aggiornato correttamente.

  ```
  curl --request POST \
  GET https://us-south.appid.cloud.ibm.com/management/v4/{{APPID_TENANT_ID}}/users/{{user_profile_id}}/profile \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  ```
  {: codeblock}

  Output di risposta di esito positivo:

  ```
  {
      "id": "5ce78e09-1356-4ef8-a45d-808b633101db",
      "identities": [],
      "attributes": {
          "role": "manager"
      }
  }
  ```
  {: screen}

Ottimo lavoro!


## Passo 4: Inserimento di attributi nei token
{: #roles-map-claims}

Il parco a tema diventa sempre più popolare e continua a crescere. Il numero di nuovi visitatori e di nuovi dipendenti è tale che vuoi limitare il numero di richieste eseguite. Per prestazioni migliori, puoi associare gli attributi di profilo utente alle tue attestazioni di token di accesso e identità. Associando le attestazioni personalizzate, puoi memorizzare gli attributi personalizzati nei token stessi.
{: shortdesc}

La [configurazione del token](/docs/services/appid?topic=appid-customizing-tokens#customizing-tokens) è globale, il che significa che si applica a tutti gli utenti con un attributo `role`, indipendentemente dal ruolo effettivo ad essi assegnato.
{: tip}


1. Esegui una richiesta all'endpoint di configurazione del token.

  ```
  curl --request PUT \
  https://us-south.appid.cloud.ibm.com/management/v4/{{APPID_TENANT_ID}}/config/tokens \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  - d '{
      "access": {
          "expires_in": 3601
      },
      "refresh": {
          "enabled": false,
          "expires_in": 2592001
      },
      "anonymousAccess": {
          "expires_in": 2592001
      },
      "accessTokenClaims": [
      {
      "source": "attributes",
      "sourceClaim": "role"
      }
      ]
  }'
  ```
  {: codeblock}

  <table>
    <tr>
      <th>Variabile</th>
      <th>Descrizione</th>
    </tr>
    <tr>
      <td><code>tenant-id</code></td>
      <td>Un ID tenant è il modo in cui la tua istanza {{site.data.keyword.appid_short_notm}} è identificata nella richiesta. Puoi trovare il tuo ID nella scheda <em>Service credentials</em> del dashboard. Se non ne hai una serie, puoi attenerti alla procedura nella GUI per creare le credenziali.</td>
    </tr>
    <tr>
      <td><code>source</code></td>
      <td>Sia per <code>accessTokenClaim</code> che per <code>idTokenClaims</code>, imposta l'origine su <code>attribute</code>.</td>
    </tr>
    <tr>
      <td><code>sourceClaim</code></td>
      <td>Sia per <code>accessTokenClaim</code> che per <code>idTokenClaims</code>, imposta l'attestazione di origine su <code>role</code>.</td>
    </tr>
    <tr>
      <td><code>expires_in</code></td>
      <td>Questo valore si applica a ciascun tipo di token e deve essere impostato in ogni richiesta. Se hai precedentemente impostato il valore nella GUI, ed esegui quindi questa richiesta, i valori nella richiesta sovrascrivono i valori impostati precedentemente. Assicurati di impostare la scadenza sul valore corretto per la tua configurazione.</td>
    </tr>
  </table>

  Output di risposta di esito positivo:

  ```
  {
      "access": {
          "expires_in": 3601
      },
      "refresh": {
          "enabled": false,
          "expires_in": 2592001
      },
      "anonymousAccess": {
          "expires_in": 2592001
      },
      "accessTokenClaims": [
      {
      "source": "attributes",
      "sourceClaim": "role"
      }
      ]
  }
  ```
  {: screen}


## Passo 5: Visualizzazione del token di accesso
{: #roles-view-token}

Facoltativamente, puoi verificare che il passo 4 sia stato eseguito correttamente visualizzando un token di accesso.
{: shortdesc}

1. Per scopi di test, crea un utente Cloud Directory utilizzando la GUI {{site.data.keyword.appid_short_notm}}.

  1. Nella scheda **Users**, fai clic su **Add User**. Viene visualizzato un modulo.
  2. Immetti un nome e un cognome, una email e una password.
  3. Fai clic su **Save**.

2. Codifica il tuo ID client e il tuo segreto.

  1. Nella scheda **Service Credentials** della GUI {{site.data.keyword.appid_short_notm}}, copia il tuo ID client e il tuo segreto.
  2. Utilizza un codificatore base64 per codificare le tue informazioni di autorizzazione.
  3. Copia l'output da utilizzare nel seguente comando.

4. Esegui l'accesso utilizzando le API per ottenere le tue informazioni sul token di accesso. Il token restituito è codificato.

  ```
  curl --request PUT \
  https://appid.cloud.ibm.com/oauth/v4/<tenant-ID>/token \
  --header 'Authorization: Basic <encoded-clientID>:<encoded-client-secret>' \
  --header 'Content-Type: application/x-www-form-urlencoded' \
  --header `Accept: application/json`
  - d 'grant_type=password&username=<user-email>%40<user-email-domain>&password=<user-password>
  ```
  {: codeblock}

5. Decodifica il tuo token di accesso.
  1. Copia il token nell'output della risposta dal comando precedente.
  2. In un browser, vai a https://jwt.io/.
  3. Incolla il token nella casella etichettata come **Encoded**.

6. Nella sezione **Decoded**, verifica che puoi visualizzare il ruolo.

  ```
  {
    "iss": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61",
    "exp": 1551903163,
    "aud": [
      "968c2306-9aef-4109-bc06-4f5ed6axi24a"
    ],
    "sub": "2b96cc04-eca5-4122-a8de-6e07d14c13a5",
    "email_verified": true,
    "amr": [
      "cloud_directory"
    ],
    "iat": 1551899553,
    "tenant": "39a37f57-a227-4bfe-a044-93b6e6050a61",
    "scope": "openid appid_default appid_readprofile appid_readuserattr appid_writeuserattr appid_authenticated"
    "role": "manager"
  }
  ```
  {: screen}



## Passi successivi
{: #roles-next}

Ottimo lavoro! Hai completato l'esercitazione. Ora puoi provare a configurare l'[autenticazione multifattore (MFA, multi-factor authentication)](/docs/services/appid?topic=appid-cd-mfa) o a impostare la [GUI personalizzata](/docs/services/appid?topic=appid-branded).
