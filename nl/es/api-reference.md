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

# Gestión de {{site.data.keyword.appid_short_notm}} con la API
{: #manging-api}

Puede utilizar la API de gestión para la automatización, la personalización y la gestión de DevOps de sus instancias de {{site.data.keyword.appid_full}}.
{: shortdesc}

La API de gestión está protegida con las señales generadas de IAM (Identity and Access Management). Con IAM, los propietarios de las cuentas pueden especificar qué persona de su equipo tiene qué nivel de acceso para cada instancia de servicio. Para obtener más información sobre cómo funcionan juntos IAM y {{site.data.keyword.appid_short_notm}}, consulte [Gestión de acceso de servicio](/docs/services/appid?topic=appid-service-access-management).


¿Desea ver la API en acción? Vea el siguiente Vídeo de guía de aprendizaje.

<iframe class="embed-responsive-item" id="about-appid-api" title="Acerca de {{site.data.keyword.appid_short_notm}} API" type="text/html" width="640" height="390" src="//www.youtube.com/embed/b2ABxvAdGg0?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>


Con la API, puede:
* Automatizar la configuración de {{site.data.keyword.appid_short_notm}} en su app del proceso de DevOps.
* Establecer y personalizar las funciones a través de la app de fondo, como la configuración del widget de inicio de sesión, el proceso de registro y la gestión de usuarios.


Las llamadas al punto final de la API de gestión toman la siguiente estructura:

```
https://<region-endpoint>.appid.cloud.ibm.com/management
```
{: codeblock}


<table>
  <tr>
    <th>Región</th>
    <th>Punto final</th>
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
    <td>Sídney</td>
    <td><code>au-syd</code></td>
  </tr>
  <tr>
    <td>Londres</td>
    <td><code>eu-gb</code></td>
  </tr>
  <tr>
    <td>Tokio</td>
    <td><code>jp-tok</code></td>
  </tr>
</table>



## Requisitos previos
{: #api-prereq}

<ul><ul><li>Una instancia de servicio que se haya creado después del 15 de marzo de 2018. Si tiene una instancia del servicio que se ha creado antes de esa fecha, cree una instancia nueva y configúrela para que coincida con la instancia actual. Asegúrese de actualizar sus apps para utilizar la instancia nueva.</li>
<li>La [CLI de {{site.data.keyword.cloud_notm}}](/docs/cli?topic=cloud-cli-getting-started) instalada.</li></ul></ul>

## Uso de ejemplo
{: #api-example}

En el ejemplo siguiente, puede ver cómo utilizar la API para cambiar el logotipo del arrendatario de {{site.data.keyword.appid_short_notm}} con Python.

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


## Pasos siguientes
{: #api-try}

Para probarlo usted mismo, consulte la [API REST de gestión de {{site.data.keyword.appid_short_notm}}](https://us-south.appid.cloud.ibm.com/swagger-ui/#/){: external}
