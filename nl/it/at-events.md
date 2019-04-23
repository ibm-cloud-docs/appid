---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-05"

keywords: authentication, authorization, identity, app security, secure, application identity, app to app, access token, activity

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


# Eventi {{site.data.keyword.cloudaccesstrailshort}}
{: #at-events}

Puoi visualizzare, gestire e analizzare le attività avviate dall'utente eseguite nella tua istanza del servizio {{site.data.keyword.appid_full}} utilizzando il servizio {{site.data.keyword.cloudaccesstrailshort}}.
{: shortdesc}



Per ulteriori informazioni su come funziona il servizio, vedi la [documentazione di {{site.data.keyword.cloudaccesstrailshort}}](/docs/services/cloud-activity-tracker/reference?topic=cloud-activity-tracker-getting-started-with-cla#getting-started-with-cla).


## Visualizzazione degli eventi di gestione
{: #at-monitor-admin}

Puoi visualizzare, gestire e analizzare l'attività di configurazione che viene eseguita nella tua istanza {{site.data.keyword.appid_short_notm}} utilizzando il servizio {{site.data.keyword.cloudaccesstrailshort}}.
{: shortdesc}

Per monitorare l'attività amministrativa:

1. Accedi al tuo account {{site.data.keyword.cloud_notm}}.
2. Dal catalogo, esegui il provisioning di un'istanza del servizio {{site.data.keyword.cloudaccesstrailshort}} nello stesso account della tua istanza {{site.data.keyword.appid_short_notm}}.
3. Nel dashboard {{site.data.keyword.cloudaccesstrailshort}}, fai clic sulla scheda **Gestisci**.
4. Dall'elenco a discesa, effettua le seguenti configurazioni per ricercare gli eventi generati da {{site.data.keyword.appid_short_notm}}.
    * Per **View logs**, seleziona **Account logs**.
    * Per **Search**, seleziona **target.Management**.
    * Per **Filter**, immetti **appid**.
5. Fai clic su **Filter**.

</br>

## Elenco degli eventi di gestione
{: #at-events-admin}

Consulta la seguente tabella per un elenco di eventi inviati a {{site.data.keyword.cloudaccesstrailshort}}.

<table>
  <tr>
    <th>Azione</th>
    <th>Descrizione</th>
    <th>Ubicazione IU</th>
  </tr>
  <tr>
    <td><code>read.recentActivity</code></td>
    <td>Visualizza l'attività recente.</td>
    <td>Può essere trovata nella casella <strong>Activity Log</strong> nella scheda <strong>Overview</strong>.</td>
  </tr>
  <tr>
    <td><code>read.idpConfig</code></td>
    <td>Visualizza la configurazione del provider di identità.</td>
    <td>Può essere trovata nella scheda <strong>Identity Providers > Manage</strong>.</td>
  </tr>
  <tr>
    <td><code>update.idpConfig</code></td>
    <td>Aggiorna la configurazione del provider di identità.</td>
    <td>Può essere aggiornata nella scheda <strong>Identity Providers > Manage</strong>.</td>
  </tr>
  <tr>
    <td><code>read.tokensConfig</code></td>
    <td>Visualizza la configurazione della scadenza del token.</td>
    <td>Può essere trovata nella scheda <strong>Identity Providers > Token Expiration</strong>.</td>
  </tr>
  <tr>
    <td><code>read.isProfilesActive</code></td>
    <td>Visualizza la configurazione di archiviazione del profilo utente.</td>
    <td>Può essere trovata in <strong>Activity Log</strong> nella scheda <strong>Overview</strong>.</td>
  </tr>
  <tr>
    <td><code>update.isProfilesActive</code></td>
    <td>Aggiorna la tua configurazione di archiviazione del profilo utente.</td>
    <td>Può essere trovata nella scheda <strong>Profiles</strong>.</td>
  </tr>
  <tr>
    <td><code>read.themeColor</code></td>
    <td>Visualizza il colore del tema dell'intestazione del widget di accesso.</td>
    <td>Può essere trovato nella scheda <strong>Login Customization</strong>.</td>
  </tr>
  <tr>
    <td><code>update.themeColor</code></td>
    <td>Aggiorna il colore del tema dell'intestazione del widget di accesso.</td>
    <td>Può essere aggiornato nella scheda <strong>Login Customization</strong>.</td>
  </tr>
  <tr>
    <td><code>read.media</code></td>
    <td>Visualizza l'immagine che viene mostrata nel widget di accesso.</td>
    <td>Può essere trovato nella scheda <strong>Login Customization</strong>.</td>
  </tr>
  <tr>
    <td><code>update.media</code></td>
    <td>Aggiorna l'immagine che viene mostrata nel widget di accesso.</td>
    <td>Può essere aggiornata nella scheda <strong>Login Customization</strong>.</td>
  </tr>
  <tr>
    <td><code>read.uiConfiguration</code></td>
    <td>Visualizza la configurazione dell'IU del widget di accesso che include il colore dell'intestazione e l'immagine.</td>
    <td>Può essere trovato nella scheda <strong>Login Customization</strong>.</td>
  </tr>
  <tr>
    <td><code>read.uiLanguages</code></td>
    <td>Visualizza un elenco di lingue supportate.</td>
    <td>Deve essere visualizzato dall'API.</td>
  </tr>
  <tr>
    <td><code>update.uiLanguages</code></td>
    <td>Aggiorna le tue lingue supportate.</td>
    <td>Devono essere aggiornate tramite l'API.</td>
  </tr>
  <tr>
    <td><code>read.samlMetadata</code></td>
    <td>Visualizza i metadati SAML {{site.data.keyword.appid_short_notm}}.</td>
    <td>Possono essere trovati nella scheda <strong>Identity Providers > SAML 2.0 Federation</strong>.</td>
  </tr>
  <tr>
    <td><code>read.cloudDirectoryUser</code></td>
    <td>Visualizza un utente Cloud Directory.</td>
    <td>Può essere trovato nella scheda <strong>Users</strong>.</td>
  </tr>
  <tr>
    <td><code>update.cloudDirectoryUser</code></td>
    <td>Aggiorna un utente Cloud Directory.</td>
    <td>Può essere aggiornato nella scheda <strong>Users</strong>.</td>
  </tr>
  <tr>
    <td><code>delete.cloudDirectoryUser</code></td>
    <td>Elimina un utente Cloud Directory.</td>
    <td>Può essere eliminato nella scheda <strong>Users</strong>.</td>
  </tr>
  <tr>
    <td><code>read.cloudDirectoryUsers</code></td>
    <td>Visualizza un elenco dei tuoi utenti Cloud Directory.</td>
    <td>Può essere trovato nella scheda <strong>Users</strong>.</td>
  </tr>
  <tr>
    <td><code>update.cloudDirectoryUsers</code></td>
    <td>Aggiorna il tuo elenco di utenti Cloud Directory.</td>
    <td>Può essere aggiornato nella scheda <strong>Users</strong>.</td>
  </tr>
  <tr>
    <td><code>delete.cloudDirectoryUsers</code></td>
    <td>Elimina un elenco di utenti Cloud Directory.</td>
    <td>Può essere eliminato nella scheda <strong>Users</strong>.</td>
  </tr>
  <tr>
    <td><code>read.emailTemplate</code></td>
    <td>Visualizza un modello email.</td>
    <td>Può essere trovato nella scheda <strong>Identity Providers > Cloud Directory > Templates</strong>.</td>
  </tr>
  <tr>
    <td><code>update.emailTemplate</code></td>
    <td>Aggiorna un modello email.</td>
    <td>Può essere trovato nella scheda <strong>Identity Providers > Cloud Directory > Templates</strong>.</td>
  </tr>
  <tr>
    <td><code>delete.emailTemplate</code></td>
    <td>Elimina un modello email per reimpostare il valore predefinito.</td>
    <td>Può essere trovato nella scheda <strong>Identity Providers > Cloud Directory > Templates</strong>.</td>
  </tr>
  <tr>
    <td><code>read.senderDetails</code></td>
    <td>Visualizza i dettagli del mittente.</td>
    <td>Può essere trovata nella scheda <strong>Identity Providers > Cloud Directory > Settings</strong>.</td>
  </tr>
  <tr>
    <td><code>update.senderDetails</code></td>
    <td>Aggiorna i dettagli del mittente</td>
    <td>Può essere trovata nella scheda <strong>Identity Providers > Cloud Directory > Settings</strong>.</td>
  </tr>
  <tr>
    <td><code>update.resendNotification</code></td>
    <td>Reinvia le notifiche utente.</td>
    <td>Può essere trovata nella scheda <strong>Identity Providers > Cloud Directory > Settings</strong>.</td>
  </tr>
  <tr>
    <td><code>update.selfForgotPassword</code></td>
    <td>Aggiorna il processo della password dimenticata.</td>
    <td>Può essere trovata nella scheda <strong>Identity Providers > Cloud Directory > Settings</strong>.</td>
  </tr>
  <tr>
    <td><code>update.forgotPasswordResult</code></td>
    <td>Visualizza il risultato della conferma della password dimenticata.</td>
    <td>Deve essere eseguita tramite l'API.</td>
  </tr>
  <tr>
    <td><code>update.selfSignUp</code></td>
    <td>Aggiorna il processo di registrazione.</td>
    <td>Può essere trovata nella scheda <strong>Identity Providers > Cloud Directory > Settings</strong>.</td>
  </tr>
  <tr>
    <td><code>update.signUpResult</code></td>
    <td>Visualizza la conferma del risultato di registrazione.</td>
    <td>Deve essere eseguita tramite l'API.</td>
  </tr>
  <tr>
    <td><code>read.action_url</code></td>
    <td>Visualizza l'URL personalizzato che viene richiamato quando viene eseguita un'azione.</td>
    <td>Può essere trovato nella scheda <strong>Identity Providers > Cloud Directory > Custom Landing Pages</strong>.</td>
  </tr>
  <tr>
    <td><code>update.action_url</code></td>
    <td>Aggiorna l'URL personalizzato che viene richiamato quando viene eseguita un'azione.</td>
    <td>Può essere trovata nella scheda <strong>Identity Providers > Cloud Directory > Settings</strong>.</td>
  </tr>
  <tr>
    <td><code>update.changePassword</code></td>
    <td>Modifica la password utente di Cloud Directory.</td>
    <td>Può essere trovata nella scheda <strong>Identity Providers > Cloud Directory > Settings</strong>.</td>
  </tr>
  <tr>
    <td><code>read.loginWidgetConfig</code></td>
    <td>Visualizza la configurazione del widget di accesso.</td>
    <td>Può essere trovato nella scheda <strong>Login Customization</strong>.</td>
  </tr>
  <tr>
    <td><code>update.loginWidgetConfig</code></td>
    <td>Aggiorna la configurazione del widget di accesso.</td>
    <td>Può essere aggiornata nella scheda <strong>Login Customization</strong>.</td>
  </tr>
</table>



