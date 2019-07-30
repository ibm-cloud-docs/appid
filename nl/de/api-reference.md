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

# {{site.data.keyword.appid_short_notm}} mit der API verwalten
{: #manging-api}

Sie können die Management-API für die DevOps-Automation sowie für die Anpassung und Verwaltung Ihrer Instanzen von {{site.data.keyword.appid_full}} verwenden.
{: shortdesc}

Die Management-API wird mit Tokens geschützt, die von IAM (Identity and Access Management) generiert werden. Mit IAM können Kontoeigner angeben, wer in ihrem Team über welche Zugriffsebene für die einzelnen Serviceinstanzen verfügen soll. Weitere Informationen zum Zusammenspiel von IAM und {{site.data.keyword.appid_short_notm}} finden Sie in [Servicezugriffsverwaltung](/docs/services/appid?topic=appid-service-access-management).


Möchten Sie die API in Aktion sehen? Sehen Sie sich das folgende Schulungsvideo an.

<iframe class="embed-responsive-item" id="about-appid-api" title="Informationen zur {{site.data.keyword.appid_short_notm}}-API" type="text/html" width="640" height="390" src="//www.youtube.com/embed/b2ABxvAdGg0?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>


Mit der API können Sie:
* Die Konfiguration von {{site.data.keyword.appid_short_notm}} in der App Ihres DevOps-Prozesses automatisieren.
* Funktionen wie die Anmeldewidgetkonfiguration, den Registrierungsprozess und das Benutzermanagement über das App-Back-End festlegen und anpassen.


Aufrufe an den Endpunkt der Management-API haben die folgende Struktur:

```
https://<region-endpoint>.appid.cloud.ibm.com/management
```
{: codeblock}


<table>
  <tr>
    <th>Region</th>
    <th>Endpunkt</th>
  </tr>
  <tr>
    <td>Dallas</td>
    <td><code>us-south</code></td>
  </tr>
  <tr>
    <td>Frankfurt</td>
    <td><code>eu-de</code></td>
  </tr>
  <tr>
    <td>Sydney</td>
    <td><code>au-syd</code></td>
  </tr>
  <tr>
    <td>London</td>
    <td><code>eu-gb</code></td>
  </tr>
  <tr>
    <td>Tokio</td>
    <td><code>jp-tok</code></td>
  </tr>
</table>



## Voraussetzungen
{: #api-prereq}

<ul><ul><li>Eine Serviceinstanz, die nach dem 15. März 2018 erstellt wurde. Wenn Sie über eine Instanz des Service verfügen, die vor diesem Datum erstellt wurde, erstellen Sie eine neue Instanz und konfigurieren Sie sie so, dass sie mit Ihrer aktuellen Instanz übereinstimmt. Stellen Sie sicher, dass Sie Ihre Apps für die Verwendung der neuen Instanz aktualisieren.</li>
<li>Die [{{site.data.keyword.cloud_notm}}-CLI](/docs/cli?topic=cloud-cli-getting-started) ist installiert.</li></ul></ul>

## Beispielverwendung
{: #api-example}

Im folgenden Beispiel sehen Sie, wie die API für die Änderung des {{site.data.keyword.appid_short_notm}}-Tenant-Logos mit Python verwendet wird.

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


## Nächste Schritte
{: #api-try}

Versuchen Sie es nun selbst. Weitere Informationen finden Sie unter [{{site.data.keyword.appid_short_notm}}-Management-Rest-API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/){: external}
