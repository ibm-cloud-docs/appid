---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-03"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:pre: .pre}
{:tip: .tip}
{:screen: .screen}

# Descrizione dei profili utente
{: #user-profile}

Con {{site.data.keyword.appid_full}}, puoi creare delle esperienze personalizzate per le applicazioni accedendo alle informazioni sugli utenti memorizzate da {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

## Concetti chiave
{: #key-concepts}

**Cos'è un profilo utente??**

Un profilo utente è una raccolta di attributi memorizzati da {{site.data.keyword.appid_short_notm}}. Gli attributi sono parti di informazioni relative agli utenti che interagiscono con la tua applicazione. Esistono due tipi di attributi che è possibile ottenere: `predefined` e `custom`.

**Quali sono gli attributi predefiniti?**

Gli attributi predefiniti vengono restituiti dal provider di identità quando il tuo utente accede alla tua applicazione. Gli attributi potrebbero includere il nome utente, l'età o il sesso.

**Quali sono gli attributi personalizzati?**

Gli attributi personalizzati vengono acquisiti dai tuoi utenti mentre interagiscono con la tua applicazione. Potrebbero essere la dimensione del carattere che utilizzano o gli elementi che hanno inserito in un carrello degli acquisti. Gli attributi personalizzati possono essere modificati.

## Accesso agli attributi dell'utente
{: #access}

Esistono diversi modi con cui puoi accedere alle informazioni del profilo utente. Dopo un'autenticazione utente con esito positivo, la tua applicazione riceve i token di accesso e di identità. Il token di identità contiene un sottoinsieme normalizzato di attributi utente che vengono restituiti da un provider di identità. Per ottenere l'elenco completo degli attributi utente, puoi utilizzare l'endpoint `/userinfo` OIDC. Per gestire gli attributi personalizzati, è possibile utilizzare `REST API`. Sia le informazioni utente che gli endpoint degli attributi personalizzati sono protetti dal token di accesso generato da {{site.data.keyword.appid_short_notm}} alla fine del processo di autenticazione.



![{{site.data.keyword.appid_short_notm}} - Architettura profilo utente](/images/user-profile1.png)

Figura. Flusso di informazioni del profilo utente

Per visualizzare gli attributi personalizzati, puoi utilizzare <a href="https://appid-profiles.ng.bluemix.net/swagger-ui/index.html#/Attributes" target="_blank">REST API <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>.

</br>
</br>
