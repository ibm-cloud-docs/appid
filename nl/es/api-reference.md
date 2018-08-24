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

# Gestión de {{site.data.keyword.appid_short_notm}} con la API
{: manging-api}

Puede utilizar la API de gestión para la automatización, la personalización y la gestión de DevOps de sus instancias de {{site.data.keyword.appid_full}}.
{: shortdesc}

La API de gestión está protegida con las señales generadas de {{site.data.keyword.cloudaccesstraillong}}. Con IAM, los propietarios de las cuentas pueden especificar qué persona de su equipo tiene qué nivel de acceso para cada instancia de servicio. Para obtener más información sobre cómo funcionan juntos IAM y {{site.data.keyword.appid_short_notm}}, consulte [Gestión de acceso de servicio](/docs/services/appid/iam.html).

Con la API, puede:
* Automatizar la configuración de {{site.data.keyword.appid_short_notm}} en su app del proceso de DevOps.
* Establecer y personalizar las funciones a través de la app de fondo, como la configuración del widget de inicio de sesión, el proceso de registro y la gestión de usuarios.


Las llamadas al punto final de la api de gestión toman la siguiente estructura:

```
appid-management.<region>.bluemix.net
```
{: codeblock}

Puede encontrar la región consultando en la tabla siguiente.

<table>
  <tr>
    <th>Región de {{site.data.keyword.Bluemix}}</th>
    <th>Punto final</th>
  </tr>
  <tr>
    <td>Reino Unido</td>
    <td><code>appid-management.eu-gb.bluemix.net</code></td>
  </tr>
  <tr>
    <td>Sur de EE.UU.</td>
    <td><code>appid-management.ng.bluemix.net</code></td>
  </tr>
  <tr>
    <td>Sídney</td>
    <td><code>appid-management.au-syd.bluemix.net</code></td>
  </tr>
  <tr>
    <td>Alemania</td>
    <td><code>appid-management.eu-de.bluemix.net</code></td>
  </tr>
</table>



## Requisitos previos
{: #api-prereq}

<ul><ul><li>Una instancia de servicio que se haya creado después del 15 de marzo de 2018. Si tiene una instancia del servicio que se ha creado antes de esa fecha, cree una instancia nueva y configúrela para que coincida con la instancia actual. Asegúrese de actualizar sus apps para utilizar la instancia nueva.</li>
<li>La [CLI de {{site.data.keyword.Bluemix_notm}}](/docs/cli/index.html) instalada.</li></ul></ul>

## Uso de ejemplo
{: #api-example}

En el ejemplo siguiente, puede ver cómo utilizar la API para cambiar el logotipo del arrendatario de {{site.data.keyword.appid_short_notm}} con Python.

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


## Pasos siguientes
{: #api-try}

Para probarlo usted mismo, consulte <a href="https://appid-management.ng.bluemix.net/swagger-ui/
" target="_blank">la API REST de gestión de {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>
