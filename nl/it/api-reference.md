---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-18"

keywords: Authentication, authorization, identity, app security, secure, application identity, app to app, access token

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

# Gestione di {{site.data.keyword.appid_short_notm}} con l'API
{: #manging-api}

Puoi utilizzare l'API di gestione per l'automazione DevOps, la personalizzazione e la gestione delle tue istanze di {{site.data.keyword.appid_full}}.
{: shortdesc}

L'API di gestione è protetta con i token generati da Identity and Access Management (IAM). Con IAM, i proprietari degli account possono specificare quali sono i livelli di accesso a disposizione dei vari membri del proprio team per ciascuna istanza del servizio. Per ulteriori informazioni su come funzionano insieme IAM e {{site.data.keyword.appid_short_notm}}, vedi [Gestione dell'accesso al servizio](/docs/services/appid?topic=appid-service-access-management).


Vuoi vedere l'API in azione? Controlla la seguente esercitazione video.

<iframe class="embed-responsive-item" id="about-appid-api" title="Informazioni sull'API {{site.data.keyword.appid_short_notm}} " type="text/html" width="640" height="390" src="//www.youtube.com/embed/b2ABxvAdGg0?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>


Con l'API, puoi:
* Automatizzare la configurazione di {{site.data.keyword.appid_short_notm}} nella tua applicazione del processo DevOps.
* Impostare e personalizzare le funzionalità attraverso il backend della tua applicazione, come la configurazione del widget di accesso, il processo di registrazione e la gestione degli utenti.


Le chiamate all'endpoint API di gestione assumono la seguente struttura:

```
https://<region-endpoint>.appid.cloud.ibm.com/management
```
{: codeblock}


<table>
  <tr>
    <th>Regione</th>
    <th>Endpoint</th>
  </tr>
  <tr>
    <td>Dallas</td>
    <td><code>us-south</code></td>
  </tr>
  <tr>
    <td>Francoforte</td>
    <td><code>eu-de</code></td>
  </tr>
  <tr>
    <td>Sydney</td>
    <td><code>au-syd</code></td>
  </tr>
  <tr>
    <td>Londra</td>
    <td><code>eu-gb</code></td>
  </tr>
  <tr>
    <td>Tokyo</td>
    <td><code>jp-tok</code></td>
  </tr>
</table>



## Prerequisiti
{: #api-prereq}

<ul><ul><li>Un'istanza del servizio creata dopo il 15 marzo 2018. Se hai un'istanza del servizio creata prima di questa data, crea una nuova istanza e configurala in modo che corrisponda alla tua istanza corrente. Assicurati di aggiornare le tue applicazioni per utilizzare la nuova istanza.</li>
<li>La [CLI {{site.data.keyword.cloud_notm}}](/docs/cli?topic=cloud-cli-getting-started) installata.</li></ul></ul>

## Utilizzo di esempio
{: #api-example}

Nel seguente esempio, puoi vedere come utilizzare l'API per modificare il logo del tenant {{site.data.keyword.appid_short_notm}} con Python.

```
import requests
import json

tenantId = '<{{site.data.keyword.appid_short_notm}} instance>'
Img = '<Logo file location>'
apiKey = '<IAM API key>'

# get an IAM token
headers = {'Content-Type': 'application/x-www-form-urlencoded', 'Accept':'application
/json'}
data = 'grant_type=urn:ibm:params:oauth:grant-type:apikey&apikey=' + apiKey;

r = requests.post("https://iam.cloud.ibm.com/oidc/token", data=data, headers=
headers);
token = 'Bearer ' + json.loads(r.text)['access_token'];

#  set the Login Widget logo
headers = {'Authorization': token , 'Accept':'application/json'}
files = {'file': open(img,'rb')}

r = requests.post("https://<region>.appid.cloud.com/management/v4/" + tenantId + "/config/ui/media?mediaType=logo", files=files, headers=headers);

#  get login widget logo
headers = {'Authorization': token , 'Accept':'application/json'}

r = requests.get("https://<region>.appid.cloud.com/management/v4/" + tenantId + "/config/ui/media", headers=headers);

if (r.status_code >= 200) :~
    print(r.text)
    print("success! the logo was changed")
```
{: screen}


## Passi successivi
{: #api-try}

Per provare tu stesso, vedi [{{site.data.keyword.appid_short_notm}} Management Rest API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/){: external}
