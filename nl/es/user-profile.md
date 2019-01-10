---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:pre: .pre}
{:tip: .tip}
{:screen: .screen}

# Descripción de los perfiles de usuario
{: #user-profile}

Con {{site.data.keyword.appid_full}}, puede crear experiencias de app personalizadas accediendo a la información acerca de los usuarios que almacena {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

## Conceptos clave
{: #key-concepts}

**¿Qué es un perfil de usuario?**

Un perfil de usuario es una recopilación de atributos almacenados por {{site.data.keyword.appid_short_notm}}. Los atributos son partes de información acerca de los usuarios que interactúan con la app. Puede obtener dos tipos de atributos: `predefinidos` y `personalizados`.

</br>

**¿Qué son los atributos predefinidos?**

El proveedor de identidad devuelve los atributos predefinidos cuando el usuario inicia la sesión en la app. Los atributos pueden incluir su nombre de usuario, edad o género.

</br>

**¿Qué son atributos personalizados?**

Los atributos personalizados sobre los usuarios se conocen a medida que estos interactúan con la app. También puede establecer los atributos personalizados antes que el usuario inicie sesión en la app por primera vez. Pueden ser el tamaño de letra que utilizan o los elementos que colocan en un carro de la compra. Los atributos personalizados se pueden editar. Asegúrese de comprobar las [implicaciones de seguridad](custom-attributes.html) que se pueden producir permitiendo a los usuarios editar los atributos antes de modificar el valor predeterminado.

</br>
</br>

## Acceso a los atributos de usuario
{: #access}

Existen distintas maneras de acceder a los atributos [predefinidos](predefined.html) y [personalizados](custom-attributes.html). Después de una autenticación de usuario satisfactoria, la app recibe señales de acceso y de identidad. La señal de identidad contiene un subconjunto normalizado de atributos de usuario devueltos por un proveedor de identidad. Para obtener la lista completa de atributos de usuario, puede utilizar el punto final de OIDC [`/userinfo`. Para gestionar atributos personalizados, puede utilizar la `API REST`. Tanto el punto final de información de usuario como el de atributo personalizado están protegidos por la señal de acceso que genera {{site.data.keyword.appid_short_notm}} al final del proceso de autenticación.

Para obtener más información sobre las señales de identidad y acceso, consulte [Comprensión de las señales](/docs/services/appid/authorization.html#tokens)(https://appid-oauth.ng.bluemix.net/swagger-ui/#!/Authorization_Server_V3/userInfo)] o [Validación de las señales](/docs/services/appid/tokens.html).

![arquitectura del perfil de usuario de {{site.data.keyword.appid_short_notm}}](images/user-profile1.png)

Figura. Flujo de información de perfil de usuario

Para ver los atributos personalizados, puede utilizar la <a href="https://appid-profiles.ng.bluemix.net/swagger-ui/index.html#/Attributes" target="_blank">API REST <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.


</br>
</br>
