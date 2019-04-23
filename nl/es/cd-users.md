---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

keywords: authentication, authorization, identity, app security, secure, directory, registry, passwords, languages, lockout

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


# Gestión de usuarios
{: #cd-users}

Cuando habilita el directorio en la nube, los usuarios pueden registrarse en la aplicación utilizando un correo electrónico o un nombre de usuario y una contraseña.
{: shortdesc}


Un usuario del directorio en la nube no es lo mismo que un usuario de {{site.data.keyword.appid_short_notm}}. Los usuarios pueden registrarse en la app utilizando distintas opciones de proveedor de identidades que ha configurado. Los usuarios mencionados en este tema son los que eligen utilizar la opción del directorio en la nube cuando se registran en la app.
{: note}


## Adición y supresión de usuarios
{: #add-delete-users}

Puede gestionar los usuarios del directorio en la nube a través del panel de control de {{site.data.keyword.appid_short_notm}} o utilizando las API.
{: shortdesc}

Para ver los datos completos de un usuario específico, puede utilizar las API para devolver la información de un usuario del directorio en la nube como un objeto JSON. Para ver el conjunto completo de datos de usuario que {{site.data.keyword.appid_short_notm}} admite, consulte [el esquema principal de SCIM](https://tools.ietf.org/html/rfc7643#section-8.2).

### Adición de usuarios
{: #add-users}

Puede utilizar los pasos siguientes para añadir un usuario a través del panel de control de {{site.data.keyword.appid_short_notm}}.

A efectos de prueba, puede añadir usuarios a través del panel de control de {{site.data.keyword.appid_short_notm}}.

1. Vaya al separador **Directorio en la nube > Usuarios** del panel de control de {{site.data.keyword.appid_short_notm}}.

2. Pulse **Añadir usuario**. Aparece un formulario.

3. Escriba un **Nombre**, **Apellido**, **Correo electrónico** y **Contraseña**. Asegúrese de que el correo electrónico que intenta registrar no lo tenga otro usuario. Para estar seguro de que ha escrito correctamente la contraseña, confirme la contraseña introduciéndola en el campo **Vuelva a escribir la contraseña**.

4. Pulse **Guardar**. Se crea un usuario del directorio en la nube.


### Supresión de usuarios
{: #delete-users}

Si desea eliminar un usuario del directorio, puede suprimir el usuario de la GUI.

1. Vaya al separador **Directorio en la nube > Usuarios** del panel de control de {{site.data.keyword.appid_short_notm}}.

2. Pulse sobre el recuadro de selección situado junto al usuario que desea suprimir. Aparece un recuadro.

3. En el recuadro, pulse **Suprimir**. Se mostrará una pantalla.

4. Confirme que comprende que la acción de suprimir un usuario no se puede deshacer pulsando **Suprimir**. Si la acción fue un error, puede volver a añadir el usuario al directorio, pero cualquier información acerca de ese usuario ya no estará disponible.


## Migración de usuarios
{: #user-migration}

Es posible que en alguna ocasión deba configurar una nueva instancia de {{site.data.keyword.appid_short_notm}}. Si utiliza el directorio en la nube, esto significa que los usuarios deben migrarse a la nueva instancia. Puede utilizar las API de gestión para que le ayuden con la migración.
{: shortdesc}


Debe tener asignado el [rol de IAM](/docs/iam?topic=iam-getstarted#getstarted) de `Gestor` para ambas instancias de {{site.data.keyword.appid_short_notm}}.
{: note}


### Exportación
{: cd-export}

Antes de poder añadir los usuarios a la nueva instancia, deberá exportarlos desde la instancia actual. Para ello, puede utilizar la <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryExport" target="_blank">API de gestión de exportación <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.

Mandato cURL de ejemplo:

```
curl -X GET --header ‘Accept: application/json’ --header ‘Authorization: Bearer <iam-token>’ ’https://us-south.appid.cloud.ibm.com/management/v4/111c9bj3-xxxx-4b5b-zzzz-24ad9440k8j9/cloud_directory/export?encryption_secret=myCoolSecret'
```
{: codeblock}

<table>
  <tr>
    <th>Variable</th>
    <th>Descripción</th>
  </tr>
  <tr>
    <td><code>encryption_secret</code></td>
    <td>Una serie personalizada que se utiliza para cifrar y descifrar la contraseña oculta de un usuario.</td>
  </tr>
  <tr>
    <td><code> tenantID </code></td>
    <td>El ID de arrendatario de servicio se puede encontrar en las credenciales de servicio. Encontrará las credenciales de servicio en el panel de control de {{site.data.keyword.appid_short_notm}}.</td>
  </tr>
</table>

Solo se devuelven los usuarios del directorio en la nube y sus perfiles. Los usuarios de otros proveedores de identidad no.
{: note}


### Importación
{: #cd-import}

Ahora que los usuarios están listos para empezar, puede importar su información en la nueva instancia. Para ello, puede utilizar la <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Cloud%20Directory%20Users/mgmt.cloudDirectoryImport" target="_blank">API de gestión de importación <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.


Mandato cURL de ejemplo:

```
curl -X POST --header ‘Content-Type: application/json’ --header ‘Accept: application/json’ --header ‘Authorization: Bearer <iam-token>’ -d ‘{“users”: [
    {
      “scimUser”: {
        “originalId”: “3f3f6779-7978-4383-926f-a43aef3b724b”,
        “name”: {
          “givenName”: “<first-name>”,
          “familyName”: “<last-name>”,
          “formatted”: “<first-name> <last-name>”
        },
        “displayName”: “<first-name>”,
        “emails”: [
          {
            “value”: “<user>@gmail.com”,
            “primary”: true
          }
        ],
        “status”: “PENDING”
      },
      “passwordHash”: “<password hash here>“,
      “passwordHashAlg”: “<password hash algorithm>",
      “profile”: {
        “attributes”: {}
      }
    }
]}’ ‘https://us-south.appid.cloud.ibm.com/management/v4/111c9bj3-xxxx-4b5b-zzzz-24ad9440k8j9/cloud_directory/import?encryption_secret=myCoolSecret’
```
{: codeblock}



### Script de migración
{: cd-migration-script}

{{site.data.keyword.appid_short_notm}} proporciona un script de migración que puede utilizar mediante la CLI que puede ayudarle a agilizar el proceso de migración.

Antes de empezar, asegúrese de tener la siguiente información de parámetro:

<table>
  <tr>
    <th>Parameter</th>
    <th>Descripción</th>
  </tr>
  <tr>
    <td><code>sourceTenantId</code></td>
    <td>El ID de arrendatario de la instancia de {{site.data.keyword.appid_short_notm}} desde la que va a exportar usuarios.</td>
  </tr>
  <tr>
    <td><code>destinationTenantId</code></td>
    <td>El ID de arrendatario de la instancia de {{site.data.keyword.appid_short_notm}} desde la que va a importar usuarios.</td>
  </tr>
  <tr>
    <td>Región</td>
    <td>Las opciones de región incluyen: <code>au-syd</code>, <code>eu-de</code>, <code>eu-gb</code>, <code>jp-tok</code> y <code>us-south</code>.</td>
  </tr>
  <tr>
    <td>Señal de IAM</td>
    <td>Asegúrese de que dispone de permisos de <code>gestor</code> antes de obtener la señal. Para obtener ayuda sobre cómo obtener una señal de IAM, compruebe <a href="https://cloud.ibm.com/docs/iam/apikey_iamtoken.html#iamtoken_from_apikey" target="_blank">los documentos <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.</td>
  </tr>
</table>

Para ejecutar el script:

1. Clone el <a href="https://github.com/ibm-cloud-security/appid-sample-code-snippets/tree/master/export-import-cloud-directory-users" target="_blank">repositorio <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.
2. Abra el terminal y vaya a la carpeta en la que ha clonado el repositorio.
3. Ejecute el mandato siguiente.

  ```
  npm install
  ```
  {: codeblock}

4. Con los parámetros, ejecute el mandato siguiente.

  ```
  users_export_import 'sourceTenantId' 'destinationTenantId' 'region' 'iamToken'
  ```
  {: codeblock}

  Mandato de ejemplo:

  ```
  users_export_import e00a0366-53c5-4fcf-8fef-ab3e66b2ced8 73321c2b-d35a-497a-9845-15c580fdf58c ng eyJraWQiOiIyMDE3MTAyNS0xNjoyNzoxMCIsImFsZyI6IlJTMjU2In0.eyJpYW1faWQiOiJJQk1pZC0zMTAwMDBUNkZTIiwiaWQiOiJJQk1pZC0zMTAwMDBUNkZTIiwicmVhbG1pZCI6IklCTWlkIiwiaWRlbnRpZmllciI6IjMxMDAwIFQ2RlMiPCJnaXZlbl9uYW1lIjoiUm90ZW0iLCJmYW1pbHlfbmFtZSI6IkJyb3NoIiwibmFtZSI6IlJvdGVtIEJyb3NoIiwiZW1haWwiOiJyb3RlbWJyQGlsLmlibS5jb20iLCJzdWIiOiJyb3RlbWJyQGlsLmlibS5jb20iLCJhY2NvdW50Ijp7ImJzcyI6ImQ3OWM5YTk5NjJkYzc2Y2JkMDZlYTVhNzhjMjY0YzE5In0sImlhdCI6MTUzNrE3Mjg4NCwiZXhwIjoxNTM3MTc2NDg0LCJpc3MiOiJodHRwczovL2lhbS5zdGFnZTEuYmx1ZW1peC5uZXQvaWRlbnRpdHkiLCJncmFudF90eXBlIjoidXJuOmlibTpwYXJhbXM6b2F1dGg6Z3JhbnQtdHlwZTpwYXNzY29kZSIsInNjb3BlIjoiaWJtIG9wZW5pZCIsImNsaWVudF9pZCI6ImJ4IiwiYWNyIjoxLCJhbXIiOlsicHdkIl19.c4vLPzhvvNZLjaLy7znDa37qV4o-yuGmSKmJoQKrEQNZU8IC0NIjxwSo7W9kb0pDi3Yf_03_9ufTTGNfjtltzNWycSXjkNgoL-b9_nU61oHdgn0stY1KmNicqyBWfgUU--4xa904QN_QjRHBaUBeJf3XWEphPIMoF7mZeOxEZLnCMcQXSz9pImCMiP4SNT38cHLiI90Yx01rM7hpteepWULh5MYh-B2V03Gkgxfqvv951HF1LDg6eT4Q9in11laTQKtKuomripUju_4GIIjORVYw9NaAVKIJ9lKrPX0SKPhStsa59qGsC_7Uersms5EY1W1VbZVqOZPJbtp6tVf-Lw
  ```
  {: codeblock}
