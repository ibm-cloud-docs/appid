---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

keywords: authentication, authorization, identity, app security, secure, user profiles, personalized apps, attributes, 

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

# Descripción de los perfiles de usuario
{: #user-profile}

Con {{site.data.keyword.appid_full}}, puede crear experiencias de app personalizadas accediendo a la información acerca de los usuarios que almacena {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

## Conceptos clave
{: #profile-concepts}

**¿Qué es un perfil de usuario?**

Un perfil de usuario es una recopilación de atributos almacenados por {{site.data.keyword.appid_short_notm}}. Los atributos son partes de información acerca de los usuarios que interactúan con la app. Puede obtener dos tipos de atributos: `predefinidos` y `personalizados`.



**¿Qué son los atributos predefinidos?**

El proveedor de identidad devuelve los atributos predefinidos cuando el usuario inicia la sesión en la app. Los atributos pueden incluir su nombre de usuario, edad o género.



**¿Qué son atributos personalizados?**

Los atributos personalizados sobre los usuarios se conocen a medida que estos interactúan con la app. También puede establecer los atributos personalizados antes que el usuario inicie sesión en la app por primera vez. Pueden ser el tamaño de letra que utilizan o los elementos que colocan en un carro de la compra. Los atributos personalizados se pueden editar. Asegúrese de comprobar las [implicaciones de seguridad](/docs/services/appid?topic=appid-custom-attributes) que se pueden producir permitiendo a los usuarios editar los atributos antes de modificar el valor predeterminado.


## Acceso a los atributos de usuario
{: #profile-access}

Existen distintas maneras de acceder a los atributos [predefinidos](/docs/services/appid?topic=appid-predefined-attributes) y [personalizados](/docs/services/appid?topic=appid-custom-attributes). Después de una autenticación de usuario satisfactoria, la app recibe señales de acceso y de identidad. La señal de identidad contiene un subconjunto normalizado de atributos de usuario devueltos por un proveedor de identidad. Para obtener la lista completa de atributos de usuario, puede utilizar el punto final [`/userinfo` de OIDC](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Authorization_Server_V4/userInfo). Para gestionar atributos personalizados, puede utilizar la `API REST`. Tanto el punto final de información de usuario como el de atributo personalizado están protegidos por la señal de acceso que genera {{site.data.keyword.appid_short_notm}} al final del proceso de autenticación.

Para obtener más información sobre las señales de identidad y acceso, consulte [Comprensión de las señales](/docs/services/appid?topic=appid-tokens#tokens) o [Validación de las señales](/docs/services/appid?topic=appid-token-validation).

![arquitectura del perfil de usuario de {{site.data.keyword.appid_short_notm}}](images/user-profile1.png)

Figura. Flujo de información de perfil de usuario

Para ver los atributos personalizados, puede utilizar la <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Attributes" target="_blank">API REST <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.

