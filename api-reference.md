---

copyright:
  years: 2017, 2018
lastupdated: "2018-03-21"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Managing {{site.data.keyword.appid_short_notm}} with the API
{: manging-api}

You can use the management API for DevOps automation, customization, and management of your instances of {{site.data.keyword.appid_full}}.
{: shortdesc}

The management API is secured with IBM Cloud Identity and Access Management generated tokens. This means that account owners can specify who on their team has which level of access for each service instance. For more information about how IAM and {{site.data.keyword.appid_short_notm}} work together, see [Service access management](/docs/services/appid/iam.html).

With the API, you can:
* automate the configuration of {{site.data.keyword.appid_short_notm}} in your app of your DevOps process.
* set and customize capabilities through your app back-end, such as your login widget configuration, sign-up process, and user management.


Calls to the management api point to the following endpoint:
```
appid-oauth.<region>.bluemix.net
```
{: codeblock}

You can find the region by looking in the following table.

<table>
  <tr>
    <th> {{site.data.keyword.Bluemix}} Region </th>
    <th> Endpoint </th>
  </tr>
  <tr>
    <td> United Kingdom </td>
    <td> appid-oauth.eu-gb.bluemix.net </td>
  </tr>
  <tr>
    <td> US South </td>
    <td> appid-oauth.ng.bluemix.net </td>
  </tr>
  <tr>
    <td> Sydney </td>
    <td> appid-oauth.au-syd.bluemix.net </td>
  </tr>
</table>

## Prerequisites
{: #api-prereq}

<ul><ul><li>A service instance that was created after March 15th, 2018. If you have an instance of the service created prior to that date, create a new instance and configure it to match your current instance. Be sure to update your apps to use the new instance.</li>
<li>The [{{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/reference/bluemix_cli/get_started.html) installed.</li></ul></ul>

## Example usage
{: #api-example}

In the following example, you can see how to use the API to change the {{site.data.keyword.appid_short_notm}} tenant logo with Python.

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


## Next steps
{: #api-try}

To try it out yourself, see <a href="https://appid-management.ng.bluemix.net/swagger-ui/
" target="_blank">the {{site.data.keyword.appid_short_notm}} Management Rest API <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>
