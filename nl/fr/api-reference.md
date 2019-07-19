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

# Gestion d'{{site.data.keyword.appid_short_notm}} avec l'API
{: #manging-api}

Vous pouvez utiliser l'API de gestion pour l'automatisation DevOps, la personnalisation et la gestion de vos instances d'{{site.data.keyword.appid_full}}.
{: shortdesc}

L'API de gestion est sécurisée par des jetons générés par IAM (Identity and Access Management). Avec IAM, les propriétaires de compte peuvent spécifier le niveau d'accès de chaque membre de leur équipe pour chaque instance de service. Pour plus d'informations sur la façon dont IAM et {{site.data.keyword.appid_short_notm}} fonctionnent ensemble, voir [Gestion des accès de service](/docs/services/appid?topic=appid-service-access-management).


Vous voulez voir l'API en action ? Regardez le tutoriel ci-dessous !

<iframe class="embed-responsive-item" id="about-appid-api" title="A propos de l'API {{site.data.keyword.appid_short_notm}}" type="text/html" width="640" height="390" src="//www.youtube.com/embed/b2ABxvAdGg0?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>


Avec l'API, vous pouvez :
* Automatiser la configuration d'{{site.data.keyword.appid_short_notm}} dans votre application dans votre processus DevOps.
* Définir et personnaliser des fonctions via votre systèmes de back end d'application, comme la configuration de votre widget de connexion, le processus d'inscription et la gestion des utilisateurs.


Les appels du noeud final d'API présentent la structure suivante :

```
https://<region-endpoint>.appid.cloud.ibm.com/management
```
{: codeblock}


<table>
  <tr>
    <th>Région</th>
    <th>Noeud final</th>
  </tr>
  <tr>
    <td>Dallas</td>
    <td><code>us-south</code></td>
  </tr>
  <tr>
    <td>Francfort</td>
    <td><code>eu-de</code></td>
  </tr>
  <tr>
    <td>Sydney</td>
    <td><code>au-syd</code></td>
  </tr>
  <tr>
    <td>Londres</td>
    <td><code>eu-gb</code></td>
  </tr>
  <tr>
    <td>Tokyo</td>
    <td><code>jp-tok</code></td>
  </tr>
</table>



## Conditions requises
{: #api-prereq}

<ul><ul><li>Une instance de service créée après le 15 mars 2018. Si vous disposez d'une instance de service qui a été créée avant cette date, créez une nouvelle instance et configurez-la comme votre instance en cours. Veillez à mettre à jour vos applications pour qu'elles utilisent la nouvelle instance.</li>
<li>L'[interface de ligne de commande d'{{site.data.keyword.cloud_notm}}](/docs/cli?topic=cloud-cli-getting-started) installée.</li></ul></ul>

## Exemple d'utilisation
{: #api-example}

L'exemple suivant montre comment utiliser l'API pour changer le logo du titulaire {{site.data.keyword.appid_short_notm}} avec Python.

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


## Etapes suivantes
{: #api-try}

Pour faire un essai par vous-même, voir l'[API REST de gestion du service {{site.data.keyword.appid_short_notm}}](https://us-south.appid.cloud.ibm.com/swagger-ui/#/){: external}
