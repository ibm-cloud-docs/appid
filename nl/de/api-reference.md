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

# {{site.data.keyword.appid_short_notm}} mit der API verwalten
{: manging-api}

Sie können die Verwaltungs-API für die DevOps-Automation sowie für die Anpassung und Verwaltung Ihrer Instanzen von {{site.data.keyword.appid_full}} verwenden.
{: shortdesc}

Die Verwaltungs-API wird mit Token geschützt, die von {{site.data.keyword.cloudaccesstraillong}} generiert werden. Mit IAM können Kontoeigner angeben, wer in ihrem Team über welche Zugriffsebene für die einzelnen Serviceinstanzen verfügen soll. Weitere Informationen zum Zusammenspiel von IAM und {{site.data.keyword.appid_short_notm}} finden Sie in [Servicezugriffsverwaltung](/docs/services/appid/iam.html). 

Mit der API können Sie:
* Die Konfiguration von {{site.data.keyword.appid_short_notm}} in der App Ihres DevOps-Prozesses automatisieren.
* Funktionen wie die Anmeldewidgetkonfiguration, den Registrierungsprozess und das Benutzermanagement über das App-Back-End festlegen und anpassen. 


Aufrufe an den API-Verwaltungsendpunkt haben die folgende Struktur:

```
appid-management.<region>.bluemix.net
```
{: codeblock}

Sie finden die Region in der folgenden Tabelle.

<table>
  <tr>
    <th>{{site.data.keyword.Bluemix}}-Region</th>
    <th>Endpunkt</th>
  </tr>
  <tr>
    <td>Vereinigtes Königreich</td>
    <td><code>appid-management.eu-gb.bluemix.net</code></td>
  </tr>
  <tr>
    <td>Vereinigte Staaten (Süden)</td>
    <td><code>appid-management.ng.bluemix.net</code></td>
  </tr>
  <tr>
    <td>Sydney</td>
    <td><code>appid-management.au-syd.bluemix.net</code></td>
  </tr>
  <tr>
    <td>Deutschland</td>
    <td><code>appid-management.eu-de.bluemix.net</code></td>
  </tr>
</table>



## Voraussetzungen
{: #api-prereq}

<ul><ul><li>Eine Serviceinstanz, die nach dem 15. März 2018 erstellt wurde. Wenn Sie über eine Instanz des Service verfügen, die vor diesem Datum erstellt wurde, erstellen Sie eine neue Instanz und konfigurieren Sie sie so, dass sie mit Ihrer aktuellen Instanz übereinstimmt. Stellen Sie sicher, dass Sie Ihre Apps für die Verwendung der neuen Instanz aktualisieren.</li>
<li>Die [{{site.data.keyword.Bluemix_notm}}-CLI](/docs/cli/index.html) ist installiert.</li></ul></ul>

## Beispielverwendung
{: #api-example}

Im folgenden Beispiel sehen Sie, wie die API für die Änderung des {{site.data.keyword.appid_short_notm}}-Tenant-Logos mit Python verwendet wird.

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


## Nächste Schritte
{: #api-try}

Versuchen Sie es nun selbst. Mehr Informationen zur Verwaltung der REST-API finden Sie unter <a href="https://appid-management.ng.bluemix.net/swagger-ui/
" target="_blank"> {{site.data.keyword.appid_short_notm}}Management Rest API <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>
