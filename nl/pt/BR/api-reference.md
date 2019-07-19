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

# Gerenciando o {{site.data.keyword.appid_short_notm}} com a API
{: #manging-api}

É possível usar a API de gerenciamento para automação, customização e gerenciamento do DevOps de suas instâncias do {{site.data.keyword.appid_full}}.
{: shortdesc}

A API de gerenciamento é protegida com tokens gerados pelo Identity and Access Management (IAM). Com o IAM, os
proprietários da conta podem especificar qual o nível de acesso que alguém da equipe tem para cada instância de
serviço. Para mais informações sobre como o IAM e o {{site.data.keyword.appid_short_notm}} trabalham juntos, consulte
[Gerenciamento de acesso de serviço](/docs/services/appid?topic=appid-service-access-management).


Deseja ver a API em ação? Verifique o tutorial de vídeo a seguir.

<iframe class="embed-responsive-item" id="about-appid-api" title="Sobre a API do {{site.data.keyword.appid_short_notm}}" type="text/html" width="640" height="390" src="//www.youtube.com/embed/b2ABxvAdGg0?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>


Com a API, é possível:
* Automatize a configuração do {{site.data.keyword.appid_short_notm}} no aplicativo do seu processo DevOps.
* Configure e customize os recursos por meio do backend do aplicativo, como a configuração do widget de login, o processo de
inscrição e o gerenciamento de usuários.


As chamadas para o terminal de API de gerenciamento assumem a estrutura a seguir:

```
https://<region-endpoint>.appid.cloud.ibm.com/management
```
{: codeblock}


<table>
  <tr>
    <th>Região</th>
    <th>Ponto de Extremidade</th>
  </tr>
  <tr>
    <td>Dallas</td>
    <td><code> us-south </code></td>
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
    <td>Tóquio</td>
    <td><code>jp-tok</code></td>
  </tr>
</table>



## Pré-requisitos
{: #api-prereq}

<ul><ul><li>Uma instância de serviço que foi criada após 15 de março de 2018. Se você tiver uma instância do serviço que foi criada
antes dessa data, crie uma nova instância e configure-a para corresponder à sua instância atual. Certifique-se de atualizar seus apps para usarem a nova instância.</li>
<li>A [CLI do {{site.data.keyword.cloud_notm}}](/docs/cli?topic=cloud-cli-getting-started) instalada.</li></ul></ul>

## Exemplo de uso
{: #api-example}

No exemplo a seguir, é possível ver como usar a API para mudar o logotipo do locatário do {{site.data.keyword.appid_short_notm}} com Python.

```
import requests
import json

tenantId = '<{{site.data.keyword.appid_short_notm}} instance>'
Img = '<Logo file location>'
apiKey = '<IAM API key>'

# obter um token do IAM
headers = { 'Content-Type ':' application/x-www-form-urlencoded ',' Accept ':' application
/json ' }
dados = 'grant_type = urn:ibm:params: oauth:grant-type:apikey&apikey = ' + apiKey;

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


## Próximas Etapas
{: #api-try}

Para experimentar você mesmo, consulte [API de REST de gerenciamento do {{site.data.keyword.appid_short_notm}}](https://us-south.appid.cloud.ibm.com/swagger-ui/#/){: external}
