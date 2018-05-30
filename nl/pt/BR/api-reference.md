---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Gerenciando o {{site.data.keyword.appid_short_notm}} com a API
{: manging-api}

É possível usar a API de gerenciamento para automação, customização e gerenciamento do DevOps de suas instâncias do {{site.data.keyword.appid_full}}.
{: shortdesc}

O gerenciamento de API é assegurado pelos tokens gerados pelo IBM Cloud Identity e Access Management. Isso significa que os proprietários de conta podem especificar quem na equipe terá qual nível de acesso para cada instância de serviço. Para mais informações sobre como o IAM e {{site.data.keyword.appid_short_notm}} trabalham juntos, consulte [Serviço de gerenciamento de acesso](/docs/services/appid/iam.html).

Com a API, é possível:
* automatizar a configuração do {{site.data.keyword.appid_short_notm}} em seu app de seu processo do DevOps.
* configurar e customizar os recursos por meio do backend do seu app, como a configuração do widget de login, o processo de inscrição e o gerenciamento de usuários.


As chamadas para o terminal de API de gerenciamento assumem a estrutura a seguir:

```
appid-management.<region>.bluemix.net
```
{: codeblock}

É possível localizar a região procurando na tabela a seguir.

<table>
  <tr>
    <th>{{site.data.keyword.Bluemix}} Região</th>
    <th>Ponto de Extremidade</th>
  </tr>
  <tr>
    <td>United Kingdom</td>
    <td><code>appid-management.eu-gb.bluemix.net</code></td>
  </tr>
  <tr>
    <td>Sul dos Estados Unidos</td>
    <td><code>appid-management.ng.bluemix.net</code></td>
  </tr>
  <tr>
    <td>Sydney</td>
    <td><code>appid-management.au-syd.bluemix.net</code></td>
  </tr>
  <tr>
    <td>Alemanha</td>
    <td><code>appid-management.eu-de.bluemix.net</code></td>
  </tr>
</table>



## Pré-requisitos
{: #api-prereq}

<ul><ul><li>Uma instância de serviço que foi criada após 15 de março de 2018. Se você tiver uma instância do serviço criada antes dessa data, crie uma nova instância e configure-a para corresponder à sua instância atual. Certifique-se de atualizar seus apps para usarem a nova instância.</li>
<li>A [CLI do {{site.data.keyword.Bluemix_notm}}](/docs/cli/reference/bluemix_cli/get_started.html) instalada.</li></ul></ul>

## Exemplo de uso
{: #api-example}

No exemplo a seguir, é possível ver como usar a API para mudar o logotipo do locatário do {{site.data.keyword.appid_short_notm}} com Python.

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


## Próximas Etapas
{: #api-try}

Para experimentar você mesmo, veja <a href="https://appid-management.ng.bluemix.net/swagger-ui/
" target="_blank">a API de REST de gerenciamento do {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>
