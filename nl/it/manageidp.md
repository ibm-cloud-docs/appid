---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}


# Gestione
{: #managing}

I provider di identità (IdP) aggiungono un livello di sicurezza per le tue applicazioni mobili e web, tramite l'autenticazione. Con {{site.data.keyword.appid_full}}, puoi configurare uno o più provider di identità per creare un'esperienza di accesso personalizzata per i tuoi utenti.
{: shortdesc}


**Cos'è un provider di identità?**

Un provider di identità crea e gestisce le informazioni su un'entità come ad esempio un utente, un ID funzionale o un'applicazione. Il provider verifica l'identità dell'entità utilizzando delle credenziali, come ad esempio una password. Successivamente, l'IdP invia le informazioni sull'identità a un altro provider del servizio. Poiché il provider di identità autentica l'entità, {{site.data.keyword.appid_short_notm}} è in grado di autorizzarla e di concedere l'accesso alle tue applicazioni.

</br>

**Quali sono i provider di identità per cui {{site.data.keyword.appid_short_notm}} fornisce un'integrazione?**

Il servizio è preconfigurato per utilizzare diversi provider.

<table>
  <tr>
    <th>Provider</th>
    <th>Tipo</th>
    <th>Descrizione</th>
  </tr>
  <tr>
    <td>[Cloud Directory](/docs/services/appid/cloud-directory.html)</td>
    <td>Registro gestito</td>
    <td>Puoi mantenere il tuo registro utenti nel cloud. Quando un utente si registra alla tua applicazione, viene aggiunto alla tua directory di utenti. Questa opzione fornisce ai tuoi utenti maggiore libertà nel gestire il proprio account all'interno della tua applicazione.</td>
  </tr>
  <tr>
    <td>[SAML](/docs/services/appid/enterprise.html)</td>
    <td>Aziendale</td>
    <td>Puoi creare un'esperienza SSO (Single Sign On) per i tuoi utenti finali.</td>
  </tr>
  <tr>
    <td>[Facebook](/docs/services/appid/identity-providers.html#facebook)</td>
    <td>Social</td>
    <td>Gli utenti finali possono accedere alla tua applicazione utilizzando le loro credenziali Facebook.</td>
  </tr>
  <tr>
    <td>[Google+](/docs/services/appid/identity-providers.html#google)</td>
    <td>Social</td>
    <td>Gli utenti finali possono accedere alla tua applicazione utilizzando le loro credenziali Google+.</td>
  </tr>
  <tr>
    <td>[Personalizzato](/docs/services/appid/custom.html)</td>
    <td> </td>
    <td>Se nessuna delle opzioni fornite soddisfa le tue necessità specifiche, puoi configurare il tuo flusso di identità per lavorare con {{site.data.keyword.appid_short_notm}}.</td>
  </tr>
  
</table>

</br>

**Come {{site.data.keyword.appid_short_notm}} interagisce con un provider di identità?**

{{site.data.keyword.appid_short_notm}} interagisce con i provider di identità utilizzando più protocolli come ad esempio OpenID Connect, SAML e altri. Ad esempio, OpenID Connect è il protocollo utilizzato con molti provider social come Facebook e Google. I provider aziendali come ad esempio <a href="https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-azure-active-directory/" target="_blank">Azure Active Directory <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> o <a href="https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-active-directory-federation-service/" target="_blank">Active Directory Federation Service <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>, normalmente utilizzano SAML come loro protocollo di identità. Per [Cloud Directory](cloud-directory.html), il servizio utilizza SCIM per verificare le informazioni sull'identità.

Come gestisco l'identità dell'applicazione? Consulta [Identità dell'applicazione](app-to-app.html).
{: tip}

</br>
</br>

## Configurazione delle impostazioni
{: #configuring}

Puoi decidere quali provider desideri utilizzare, i tuoi URL di reindirizzamento e le informazioni sul token per la tua applicazione. Le impostazioni che configuri si applicano a tutti i tuoi provider di identità in questa istanza del servizio. Ad esempio: quando imposti la scadenza del token, viene applicata a tutti i provider che hai configurato sia social che aziendali.

</br>

**Per configurare i tuoi provider:**

1. Passa al tuo dashboard del servizio.
2. Nella sezione **Identity Providers** della navigazione, seleziona la pagina **Manage**.
3. Sulla scheda **Identity Providers**, imposta i provider che desideri utilizzare su **On**.
4. Facoltativo: decidi se disattivare gli utenti anonimi (**Anonymous users**) o lasciare il valore predefinito, ossia **On**. Quando impostato su **On**, gli attributi utente personalizzati vengono associati all'utente dal momento in cui iniziano ad interagire con la tua applicazione. Per ulteriori informazioni sul percorso per diventare un utente identificato, consulta [Autenticazione progressiva](progressive.html#progressive).

{{site.data.keyword.appid_short_notm}} fornisce delle credenziali predefinite per aiutarti con la configurazione iniziale di Facebook e Google+. Sei limitato a 100 utilizzi delle credenziali per istanza, al giorno. Poiché sono credenziali IBM, sono pensate per essere utilizzate solo per lo sviluppo. Prima di pubblicare la tua applicazione, aggiorna la configurazione con le tue proprie credenziali.
{: tip}

</br>

**Per configurare le tue impostazioni:**

1. Aggiungi i tuoi URL di reindirizzamento. Un URL di reindirizzamento è l'endpoint di callback della tua applicazione. Per impedire gli attacchi di phishing, {{site.data.keyword.appid_short_notm}} convalida gli URL rispetto alla whitelist.
  1. Nel campo **Add web redirect URL**, immetti l'URL e fai clic sull'icona **+**.
  2. Ripeti il passo 1 finché non sono stati aggiunti tutti i possibili URL di reindirizzamento all'elenco.

  Non includere parametri di query nel tuo URL. Vengono ignorati nel processo di convalida. Ad esempio: `http://host:[port]/path`
  {: tip}

2. Configura i tuoi token. La durata del token riinizia ad ogni accesso utente. Ad esempio, hai impostato la tua durata del token di aggiornamento su 10 giorni. Vengono creati un token di accesso e un token di aggiornamento quando l'utente accede per la prima volta. Se l'utente ritorna alla tua applicazione pochi giorni dopo, 3 giorni per essere precisi, non ha bisogno di riaccedere. Ma, se l'utente ha atteso 12 giorni dopo l'accesso iniziale e poi ritorna alla tua applicazione, dovrà riaccedere e sarà associata all'utente un serie di token.
  1. Per consentire l'accesso senza il bisogno di un'interazione da parte dell'utente, imposta **refresh tokens** su **On**.
  2. Imposta la tua durata del token di aggiornamento. La scadenza viene impostata in giorni e può essere un qualsiasi valore compreso nell'intervallo tra 1 e 90. Più piccolo è il numero, maggiore è la frequenza in cui un utente deve accedere.
  3. Imposta la tua durata del token di accesso. La scadenza viene impostata in minuti e può essere un valore compreso nell'intervallo tra 5 e 1440. Più piccolo è il valore e maggiore è la protezione che hai in caso di furto del token.
  4. Imposta la tua durata del token anonimo. Viene assegnato un [token anonimo](/docs/services/appid/progressive.html#anonymous) agli utenti nel momento in cui iniziano ad interagire con la tua applicazione. Quando un utente accede, le informazioni nel token anonimo vengono poi trasferite al token associato all'utente. La scadenza viene impostata in giorni e può essere un qualsiasi compreso tra 1 e 90.

</br>
</br>
