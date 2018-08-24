---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Gestion d'{{site.data.keyword.appid_short_notm}} avec l'API
{: manging-api}

Vous pouvez utiliser l'API de gestion pour l'automatisation DevOps, la personnalisation et la gestion de vos instances d'{{site.data.keyword.appid_full}}.
{: shortdesc}

L'API de gestion est sécurisée avec des jetons générés par {{site.data.keyword.cloudaccesstraillong}}. Avec IAM, les propriétaires de compte peuvent spécifier le niveau d'accès de chaque membre de leur équipe pour chaque instance de service. Pour plus d'informations sur la façon dont IAM et {{site.data.keyword.appid_short_notm}} fonctionnent ensemble, voir [Gestion des accès de service](/docs/services/appid/iam.html).

Avec l'API, vous pouvez :
* Automatiser la configuration d'{{site.data.keyword.appid_short_notm}} dans votre application dans votre processus DevOps. 
* Définir et personnaliser des fonctions via votre systèmes de back end d'application, comme la configuration de votre widget de connexion, le processus d'inscription et la gestion des utilisateurs. 


Les appels du noeud final d'API possèdent la structure suivante :

```
appid-management.<region>.bluemix.net
```
{: codeblock}

Pour déterminer la région, consultez le tableau ci-après.

<table>
  <tr>
    <th>Région {{site.data.keyword.Bluemix}}</th>
    <th>Noeud final</th>
  </tr>
  <tr>
    <td>Royaume-Uni</td>
    <td><code>appid-management.eu-gb.bluemix.net</code></td>
  </tr>
  <tr>
    <td>Sud des Etats-Unis</td>
    <td><code>appid-management.ng.bluemix.net</code></td>
  </tr>
  <tr>
    <td>Sydney</td>
    <td><code>appid-management.au-syd.bluemix.net</code></td>
  </tr>
  <tr>
    <td>Allemagne</td>
    <td><code>appid-management.eu-de.bluemix.net</code></td>
  </tr>
</table>



## Conditions requises
{: #api-prereq}

<ul><ul><li>Une instance de service créée après le 15 mars 2018. Si vous disposez d'une instance de service qui a été créée avant cette date, créez une nouvelle instance et configurez-la comme votre instance en cours. Veillez à mettre à jour vos applications pour qu'elles utilisent la nouvelle instance.</li>
<li>L'[interface de ligne de commande d'{{site.data.keyword.Bluemix_notm}}](/docs/cli/index.html) est installée. </li></ul></ul>

## Exemple d'utilisation 
{: #api-example}

L'exemple suivant montre comment utiliser l'API pour changer le logo du titulaire {{site.data.keyword.appid_short_notm}} avec Python.

```
import requests
import json

tenantId = '<App ID instance>'
Img = '<Logo file location>'
apiKey = '<IAM AI key>'

# get IAM token
headers = {'Content-Type': 'application/x-www-form-urlencoded', 'Accept':'application
/json'}
data = 'grant_type=urn:ibm:params:oauth:grant-type:apikey&apikey=' + apiKey;

r = requests.post("https://iam.ng.bluemix.net/oidc/token", data=data, headers=
headers);
token = 'Bearer ' + json.loads(r.text)['access_token'];

#  set login widget logo
headers = {'Authorization': token , 'Accept':'application/json'}
files = {'file': open(img,'rb')}

r = requests.post("https://appid-management.<region>.bluemix.net/management/v4/" + te
nantId + "/config/ui/media?mediaType=logo", files=files, headers=headers);

#  get login widget logo
headers = {'Authorization': token , 'Accept':'application/json'}

r = requests.get("https://appid-management.<region>.bluemix.net/management/v4/" + ten
antId + "/config/ui/media", headers=headers);

if (r.status_code >= 200) :
    print(r.text)
    print("success! the logo was changed")
```
{: screen}


## Etapes suivantes
{: #api-try}

Pour faire un essai par vous-même, voir <a href="https://appid-management.ng.bluemix.net/swagger-ui/
" target="_blank">{{site.data.keyword.appid_short_notm}} Management Rest API <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>
