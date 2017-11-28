---

copyright:
  years: 2017
lastupdated: "2017-11-02"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Protección de los recursos de Liberty for Java
{: #protecting-liberty}

Puede utilizar {{site.data.keyword.appid_short_notm}} para proteger los puntos finales de apps de IBM Liberty for Java. Liberty for Java tiene la capacidad integrada para gestionar solicitudes de Open ID Connect (OIDC).

## Antes de empezar
{: #begin}

* Es necesario disponer de una [aplicación de IBM Liberty for Java](https://console.bluemix.net/catalog/starters/liberty-for-java) desenlazada. Para familiarizarse con el desarrollo de apps de Liberty for Java, consulte [la documentación](/docs/runtimes/liberty/index.html).
* Asegúrese de que tenga instalado [Apache Maven](https://maven.apache.org/download.cgi).
* Obtenga información sobre cómo funciona OIDC con Liberty for Java.

## Protección de recursos en Liberty for Java
{: #protecting-liberty}

1. Descargue el ejemplo de Liberty for Java de la IU. El ejemplo contiene un archivo zip con los archivos Liberty estándar.

2. Abra el terminal en el directorio en el que haya extraído el ejemplo.

3. Inicie la sesión en {{site.data.keyword.Bluemix_notm}} mediante la línea de mandatos Cloud Foundry. Cuando se le solicite, introduzca sus credenciales.

  ```
  cf login
  ```
  {: codeblock}

4. Despliegue la aplicación. Al ejecutar el mandato siguiente se crea una instancia de Liberty for Java con un nombre relacionado con el tenantid.

  ```
  cf push
  ```
  {: codeblock}

5. Enlace su instancia de servicio a la nueva instancia de Liberty for Java y redespliegue la aplicación.

6. Abra la aplicación en un navegador e inicie la sesión con sus credenciales para revisar las actividades de autenticación.


## Actualización del ejemplo de Liberty for Java
{: #updating-liberty}

Para actualizar la app de ejemplo, utilice las instrucciones siguientes:

1. Cree los servlets, los jsp y los html.
2. Defina los recursos protegidos y añádalos a los filtros de autorización `web.xml` y `server.xml`.
3. Cree un archivo war y despliéguelo en Liberty for Java.

Para obtener más información sobre la actualización de apps, consulte [Añadir {{site.data.keyword.appid_short_notm}} a una aplicación existente](/docs/services/appid/existing.html#existing-liberty).
