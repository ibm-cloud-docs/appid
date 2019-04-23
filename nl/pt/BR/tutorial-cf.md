---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-20"

keywords: authentication, authorization, identity, app security, secure, development, cloud foundry, access management, iam, java, node.js

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


# Tutorial: Configurando o Cloud Foundry para usar o {{site.data.keyword.appid_short_notm}}
{: #cloud-foundry}

Com o {{site.data.keyword.cloud_notm}}, é possível proteger seus apps com dois tipos diferentes de gerenciamento de acesso, Identidade e Gerenciamento de Acesso (IAM) e o Cloud Foundry. Por padrão, todas as novas instâncias do {{site.data.keyword.appid_short_notm}} usam grupos de recursos do IAM para gerenciar o acesso. Se você estiver usando o Cloud Foundry para gerenciar seu aplicativo, será possível vincular os modelos de gerenciamento criando um alias de serviço e ligando o serviço ao app.
{: shortdesc}


## Entendendo o Cloud Foundry
{: #cf-understand}

Um alias cria uma conexão entre o seu serviço gerenciado pelo IAM, como o {{site.data.keyword.appid_short_notm}} e o aplicativo Cloud Foundry. Ao ligar um aplicativo, as credenciais de serviço são criadas e passadas automaticamente para o app. Embora a ligação seja uma etapa necessária na configuração, ela tem os benefícios a seguir:

* Automação: com as credenciais de serviço armazenadas na variável de ambiente VCAP_SERVICES, você não precisa mais copiá-las manualmente para o app. Tudo é feito nos bastidores em seu nome com os SDKs do {{site.data.keyword.appid_short_notm}}.
* Segurança: a configuração se torna a prova de erro porque o processo é automático.
* Segurança: nenhum acesso que seja relacionado é codificado permanentemente em seu aplicativo, pois as credenciais de serviço existem somente nas variáveis de ambiente.

Seu app Cloud Foundry está hospedado em outra plataforma? Sem problemas. É possível definir credenciais do aplicativo em seu app para ligá-lo ao serviço. É possível localizar suas credenciais do aplicativo por meio do painel do {{site.data.keyword.appid_short_notm}} ou fazendo uma solicitação para o terminal [/applications](https://us-south.appid.cloud.ibm.com/swagger-ui/#!/Applications/registerApplication).
{: tip}

Efetue o registro de saída de como os modelos se ajustem no diagrama a seguir:

![Ligando um app do Cloud Foundry](images/cf-alias.png)

## Antes de iniciar
{: #cf-before}

Antes de iniciar, certifique-se de que você tenha os pré-requisitos a seguir:

* Uma conta do {{site.data.keyword.cloud_notm}}
* Uma instância do {{site.data.keyword.appid_short_notm}}
* A [CLI do {{site.data.keyword.cloud_notm}}](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli) instalada localmente

## Implementando um app Node.js
{: #cf-node}


1. Navegue para a sua instância do {{site.data.keyword.appid_short_notm}}.

2. Clique em **Fazer download de amostra** na guia **Visão geral** do painel de serviço.

3. Clique em **Node.js**. Faça download e extraia o aplicativo de amostra.

4. Verifique se você tem todos os pré-requisitos do Node.js.

5. Abra o terminal e mude para a pasta de amostra.

6. Efetue login na CLI do  {{site.data.keyword.cloud_notm}} . A CLI solicitará que você selecione uma conta e região se você não especificar uma.

  ```
  ibmcloud login -a cloud.ibm.com -r <region>
  ```
  {: pre}

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

7. Direcione a organização e o espaço do Cloud Foundry nos quais deseja trabalhar e siga os prompts para destinar uma organização e um espaço.

  ```
  ibmcloud target --cf
  ```
  {: pre}

8. Crie um alias da instância de serviço do {{site.data.keyword.appid_short_notm}}.

  ```
  ibmcloud resource service-alias-create {ALIAS_NAME} --instance-name {SERVICE_INSTANCE_NAME}
  ```
  {: pre}

9. Edite os valores do host e do nome no `manifest.yml` do projeto com as informações obtidas no comando anterior. Inclua o alias que você cria para os seus serviços.

10. Ligue os serviços que estão listados no arquivo `manifest.yml` implementando o aplicativo de amostra.

  ```
  ibmcloud app push
  ```
  {: pre}

## Implementando um aplicativo Java
{: #java}

1. Navegue para a sua instância do {{site.data.keyword.appid_short_notm}}.

2. Clique em **Fazer download de amostra** na guia **Visão geral** do painel de serviço.

3. Clique em **Java**. Faça download e extraia o aplicativo de amostra.

4. Verifique se você tem todos os pré-requisitos do Java.

5. Abra o terminal e mude para a pasta de amostra.

6. Gere seu arquivo `war` e faça upload dele.

  ```
  mvn clean install
  ```
  {: pre}

7. Mude para a pasta do Liberty.

8. Efetue login na CLI do  {{site.data.keyword.cloud_notm}} . A CLI solicitará que você selecione uma conta e região se você não especificar uma.

  ```
  ibmcloud login -a cloud.ibm.com -r <region>
  ```
  {: pre}

8. Direcione a organização e o espaço do Cloud Foundry nos quais deseja trabalhar e siga os prompts para destinar uma organização e um espaço.

  ```
  ibmcloud target --cf
  ```
  {: pre}

10. Crie um alias da instância de serviço do {{site.data.keyword.appid_short_notm}}.

  ```
  ibmcloud resource service-alias-create {ALIAS_NAME} --instance-name {SERVICE_INSTANCE_NAME}
  ```
  {: pre}

11. Edite os valores do host e do nome no `manifest.yml` do projeto com as informações obtidas no comando anterior. Inclua o alias que você cria para os seus serviços.

  Exemplo:
  ```
    aplicativos:
  -nome: ApplicationName
    host: HostName
    buildpack: liberty-for-java
    instâncias: 1
    memória: 512M
    disk_quota: 1024M
    tempo limite: 180
    serviços:
    -alias-AppID
  ```
  {: screen}

13. Ligue os serviços que estão listados no arquivo `manifest.yml` implementando o aplicativo de amostra.

  ```
  ibmcloud app push
  ```
  {: pre}

