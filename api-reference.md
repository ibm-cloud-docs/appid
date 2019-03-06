---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-06"

keywords: authentication, authorization, identity, app security, secure, service access, back-end, region

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

# Managing {{site.data.keyword.appid_short_notm}} with the API
{: #manging-api}

You can use the management API for DevOps automation, customization, and management of your instances of {{site.data.keyword.appid_full}}.
{: shortdesc}

The management API is secured with {{site.data.keyword.cloudaccesstraillong}} generated tokens. With IAM, account owners can specify who on their team has which level of access for each service instance. For more information about how IAM and {{site.data.keyword.appid_short_notm}} work together, see [Service Access Management](/docs/services/appid?topic=appid-service-access-management).

With the API, you can:
* Automate the configuration of {{site.data.keyword.appid_short_notm}} in your app of your DevOps process.
* Set and customize capabilities through your app back-end, such as your login widget configuration, sign-up process, and user management.


Calls to the management api endpoint take the following structure:

```
https://<region-endpoint>.appid.cloud.ibm.com/management
```
{: codeblock}


<table>
  <tr>
    <th>Region</th>
    <th>Endpoint</th>
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
    <td>Tokyo</td>
    <td><code>jp-tok</code></td>
  </tr>
</table>



## Prerequisites
{: #api-prereq}

<ul><ul><li>A service instance that was created after 15 March 2018. If you have an instance of the service that was created before that date, create a new instance and configure it to match your current instance. Be sure to update your apps to use the new instance.</li>
<li>The [{{site.data.keyword.cloud_notm}} CLI](/docs/cli/reference/ibmcloud/cloud-cli-install_use?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli) installed.</li></ul></ul>

## Example usage
{: #api-example}

In the following example, you can see how to use the API to change the {{site.data.keyword.appid_short_notm}} tenant logo with Python.

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


## Next steps
{: #api-try}

To try it out yourself, see <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/" target="_blank">the {{site.data.keyword.appid_short_notm}} Management Rest API <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>
