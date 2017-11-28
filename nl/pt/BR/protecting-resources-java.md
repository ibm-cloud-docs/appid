---

copyright:
  years: 2017
lastupdated: "2017-11-02"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Protegendo recursos do Liberty for Java
{: #protecting-liberty}

É possível usar o {{site.data.keyword.appid_short_notm}} para proteger terminais em
seus apps IBM Liberty for Java. O Liberty for Java tem a capacidade integrada de manipular solicitações
do Open ID Connect (OIDC).

## Antes de Começar
{: #begin}

* Você precisa de um [aplicativo
IBM Liberty for Java](https://console.bluemix.net/catalog/starters/liberty-for-java) existente e desvinculado. Para se familiarizar com o desenvolvimento de
apps Liberty for Java, veja [os docs](/docs/runtimes/liberty/index.html).
* Certifique-se de ter o [Apache Maven](https://maven.apache.org/download.cgi) instalado.
* Aprenda sobre como o OIDC funciona com o Liberty for Java.

## Protegendo recursos no Liberty for Java
{: #protecting-liberty}

1. Faça download da amostra do Liberty for Java na UI. A amostra contém um arquivo zip com
os arquivos Liberty padrão.

2. Abra o terminal no diretório no qual você extraiu a amostra.

3. Efetue login no {{site.data.keyword.Bluemix_notm}} usando a linha de comandos do
Cloud Foundry. Quando solicitado, insira suas credenciais.

  ```
  cf login
  ```
  {: codeblock}

4. Implemente o aplicativo. Executar o comando a seguir cria uma instância do Liberty for Java com um nome relacionado ao tenantid.

  ```
  cf push
  ```
  {: codeblock}

5. Vincule sua instância de serviço à nova instância Liberty for Java e reimplemente o aplicativo.

6. Abra seu aplicativo em um navegador e efetue login usando suas credenciais para revisar as
atividades de autenticação.


## Atualizando a amostra do Liberty for Java
{: #updating-liberty}

Para fazer uma atualização no app de amostra, use as instruções a seguir:

1. Crie os servlets, JSPs e html.
2. Defina os recursos protegidos e inclua-os nos filtros de autorização `web.xml`
e `server.xml`.
3. Crie um arquivo war e implemente-o no Liberty for Java.

Para obter mais informações sobre como atualizar apps, veja [incluindo o {{site.data.keyword.appid_short_notm}} em um aplicativo existente](/docs/services/appid/existing.html#existing-liberty).
