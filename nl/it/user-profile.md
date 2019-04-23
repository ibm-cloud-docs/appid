---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

keywords: authentication, authorization, identity, app security, secure, user profiles, personalized apps, attributes, 

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

# Descrizione dei profili utente
{: #user-profile}

Con {{site.data.keyword.appid_full}}, puoi creare delle esperienze personalizzate per le applicazioni accedendo alle informazioni sugli utenti memorizzate da {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

## Concetti chiave
{: #profile-concepts}

**Cos'è un profilo utente??**

Un profilo utente è una raccolta di attributi memorizzati da {{site.data.keyword.appid_short_notm}}. Gli attributi sono parti di informazioni relative agli utenti che interagiscono con la tua applicazione. Puoi ottenere due tipi di attributi: `predefined` e `custom`.



**Quali sono gli attributi predefiniti?**

Gli attributi predefiniti vengono restituiti dal provider di identità quando il tuo utente accede alla tua applicazione. Gli attributi potrebbero includere il nome utente, l'età o il sesso.



**Quali sono gli attributi personalizzati?**

Gli attributi personalizzati vengono acquisiti dai tuoi utenti mentre interagiscono con la tua applicazione. Puoi anche impostare gli attributi personalizzati prima che l'utente acceda alla tua applicazione per la prima volta. Un esempio potrebbe essere la dimensione del carattere preferita o gli elementi che hanno inserito in un carrello degli acquisti. Gli attributi personalizzati possono essere modificati. Assicurati di controllare le [implicazioni sulla sicurezza](/docs/services/appid?topic=appid-custom-attributes) che possono verificarsi consentendo agli utenti di modificare i propri attributi prima di modificare il valore predefinito.


## Accesso agli attributi dell'utente
{: #profile-access}

Esistono diversi modi con cui puoi accedere agli attributi [predefiniti](/docs/services/appid?topic=appid-predefined-attributes) e [personalizzati](/docs/services/appid?topic=appid-custom-attributes). Dopo un'autenticazione utente con esito positivo, la tua applicazione riceve i token di accesso e di identità. Il token di identità contiene un sottoinsieme normalizzato di attributi utente che vengono restituiti da un provider di identità. Per ottenere l'elenco completo degli attributi utente, puoi utilizzare l'endpoint [`/userinfo` OIDC](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Authorization_Server_V4/userInfo). Per gestire gli attributi personalizzati, è possibile utilizzare `REST API`. Sia le informazioni utente che gli endpoint degli attributi personalizzati sono protetti dal token di accesso generato da {{site.data.keyword.appid_short_notm}} alla fine del processo di autenticazione.

Per ulteriori informazioni sui token di identità e accesso, consulta [Descrizione dei token](/docs/services/appid?topic=appid-tokens#tokens) o [Convalida dei token](/docs/services/appid?topic=appid-token-validation).

![{{site.data.keyword.appid_short_notm}} - Architettura profilo utente](images/user-profile1.png)

Figura. Flusso di informazioni del profilo utente

Per visualizzare gli attributi personalizzati, puoi utilizzare <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Attributes" target="_blank">REST API <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>.

