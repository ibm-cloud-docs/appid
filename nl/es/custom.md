---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

keywords: authentication, authorization, identity, app security, secure, custom, proprietary, private key, public key, jwt

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

# Personalizado
{: #custom-identity}

Puede utilizar su propio proveedor de identidad personalizado cuando realice la autenticación. El proveedor de identidad puede ajustarse a cualquier mecanismo de autenticación que no esté soportado específicamente por {{site.data.keyword.appid_full}}, incluido el propietario.
{: shortdesc}

Si {{site.data.keyword.appid_short_notm}} no proporciona soporte directo para un proveedor de identidad en concreto, puede utilizar el flujo de identidad personalizado para establecer un puente en el protocolo de autenticación hacia el flujo de autenticación existente de {{site.data.keyword.appid_short_notm}}. Por ejemplo, desea utilizar GitHub o LinkedIn para permitir a los usuarios iniciar sesión. Puede utilizar el SDK existente del proveedor de identidad para facilitar la información de autenticación de usuario antes de empaquetarla e intercambiarla con {{site.data.keyword.appid_short_notm}}. En muchos casos de ejemplo de empresa, un proveedor de identidad existente puede utilizar su propio protocolo de autenticación personalizado, pero debe seguir optimizando las funciones de {{site.data.keyword.appid_short_notm}}. Para este tipo de casos de ejemplo, el flujo de identidad personalizado proporciona un medio desacoplado de autenticar de forma segura los usuarios sin exponer las credenciales.

## Configuración de la identidad personalizada
{: #custom-configure}

Puede utilizar los pasos siguientes para configurar el proveedor de identidad personalizado para que funcione con {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

### Antes de empezar
{: #custom-identity-before}

Para establecer la confianza entre {{site.data.keyword.appid_short_notm}} y el proveedor de identidad personalizado, debe tener un par de claves RSA PEM con una longitud mínima de 2048. Asegúrese de que realiza una copia de seguridad de las claves que utiliza en producción.

¿Cómo se utilizan las claves?

- La clave privada se utiliza en la app o el proveedor de identidad para firmar JWT.
- {{site.data.keyword.appid_short_notm}} utiliza la clave pública para validar el JWT que contiene información de usuario.

Para generar un par de claves RSA PEM utilizando Open SSL, ejecute el mandato siguiente:

```
$ openssl genpkey -algorithm RSA -out private_key.pem -pkeyopt rsa_keygen_bits:2048
$ openssl rsa -pubout -in private_key.pem -out public_key.pem
```
{: codeblock}

</br>

### Configuración con la GUI
{: #custom-identity-configure-gui}

1. Inicie sesión en la cuenta de {{site.data.keyword.cloud_notm}} y vaya a la instancia de {{site.data.keyword.appid_short_notm}}.

2. En el separador **Gestionar**, establezca **Proveedor de identidad personalizado** en **Activo**.

3. Registre la clave pública con {{site.data.keyword.appid_short_notm}}.
  1. Vaya al separador **Proveedor de identidad personalizado**
  2. Pegue la clave pública en el recuadro **Clave pública** y pulse **Guardar**.



### Configuración con la API
{: #custom-identity-configure-api}

Registre la clave realizando una solicitud PUT en el [punto final de API de gestión](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_custom_idp).

```
Put {Management URI}/config/idps/custom
Content-Type: application/json
{
    isActive: true,
    config: {
        publicKey: <Your newline separated (\n) PEM public key>
    }
}
```
{: codeblock}

## Probar la configuración
{: #custom-identity-testing}

Después de configurar la instancia de {{site.data.keyword.appid_short_notm}} con una clave pública válida, puede utilizar la aplicación de prueba que proporciona el servicio para verificar que la configuración se ha establecido correctamente. En la app de ejemplo, puede ver las cargas útiles de las señales de identidad y acceso de {{site.data.keyword.appid_short_notm}} que se devuelven durante un flujo de inicio de sesión estándar.

1. En el separador **Proveedor de identidad personalizado**, pulse **Probar** para abrir la aplicación de prueba.

2. Cree un JWT de ejemplo utilizando [JWT.io](https://jwt.io/) siguiendo el [protocolo](/docs/services/appid?topic=appid-custom-auth#generating-jwts) de identidad personalizado.

3. Pegue el JWT en el recuadro que está etiquetado como **señal web de JSON** y pulse **Probar** para ejecutar una autenticación de muestra.

Si se realiza correctamente, verá las señales de identidad y acceso de {{site.data.keyword.appid_short_notm}} descodificadas, disponibles para la aplicación en un flujo de inicio de sesión estándar.

## Pasos siguientes
{: #custom-identity-next}

Ahora que se ha configurado el proveedor de identidad personalizado, [añádalo a la aplicación](/docs/services/appid?topic=appid-custom-auth#custom-auth).
