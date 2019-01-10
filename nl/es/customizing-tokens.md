---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-25"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}


# Personalización de señales
{: #customizing-tokens}

Puede configurar las señales de {{site.data.keyword.appid_short_notm}} para que cumplan con las necesidades específicas de la aplicación.
{: shortdesc}

**¿Qué tipo de señales existen?**

Diferentes tipos de señales de {{site.data.keyword.appid_short_notm}} para proteger las aplicaciones.

* Señales de acceso: Habilitan la comunicación con los recursos de fondo que están protegidos por filtros de autorización. Si una señal de acceso no está asociada con un usuario específico, la señal tiene capacidades limitadas.
* Señales de identidad: Contienen información personal y se utilizan para autenticar a un usuario. En función de la configuración de la app, las señales de identidad se pueden emitir antes de que se autentique un usuario. Esto le permite empezar a asociar atributos con los usuarios antes de iniciar la sesión en la aplicación.
* Señales de renovación: Se pueden utilizar para ampliar la cantidad de tiempo que puede pasar un usuario sin volver a autenticarse.

¿Desea obtener más información sobre las señales? Consulte más información en [Comprensión de las señales](authorization.html#tokens).
{: tip}

</br>

**¿Cuáles son las opciones de personalización?**

Puede personalizar las señales estableciendo la validez del período de vida o añadiendo reclamaciones personalizadas a las señales. Compruebe la tabla siguiente para ver cómo se configura el período de vida o siga leyendo para obtener más información sobre la correlación de atributos personalizados.

<table>
  <tr>
    <th>Tipo de señal</th>
    <th>Tipo de valor</th>
    <th>Valor predeterminado</th>
    <th>Opciones</th>
  </tr>
  <tr>
    <td>Acceso</td>
    <td>Minutos</td>
    <td>60</td>
    <td>Cualquier valor entre 5 y 1440</td>
  </tr>
  <tr>
    <td>Identidad</td>
    <td>Minutos</td>
    <td>60</td>
    <td>Cualquier valor entre 5 y 1440</td>
  </tr>
  <tr>
    <td>Actualizar</td>
    <td>Días</td>
    <td>30</td>
    <td>Cualquier valor entre 1 y 9</td>
  </tr>
  <tr>
    <td>Anónimo</td>
    <td>Días</td>
    <td>30</td>
    <td>Cualquier valor entre 1 y 9</td>
  </tr>
</table>

</br>

**¿Por qué debería añadir reclamaciones a mis señales?**

Existen varias razones por las que es posible que desee realizar un seguimiento de los atributos adicionales. Cuando trabaja con los desarrolladores de apps, puede correlacionar roles y permisos. O, cuando crea perfiles en los usuarios finales, puede realizar un seguimiento de la información adicional que le ayuda a crear experiencias personalizadas.

</br>

**¿Existen consideraciones sobre seguridad?**

Sí. Puesto que las señales se utilizan para identificar a los usuarios y proteger los recursos, el período de vida de una señal afecta a varias cosas distintas. Mediante la personalización de la configuración de la señal puede garantizar que las necesidades de seguridad y experiencia de usuario se cumplen. Sin embargo, si alguna vez una señal se ve comprometida, un usuario malintencionado tendrá más tiempo para afectar a la aplicación.

¿Desea obtener más información sobre las consideraciones de seguridad que debe realizar? Consulte los [Atributos personalizados](custom-attributes.html).
{: tip}

</br>
</br>

## Comprensión de reclamaciones y atributos personalizados
{: #custom-claims}

Puede correlacionar atributos de perfil de usuario a las reclamaciones de señal de identidad y acceso. Lo que significa que no tendrá que ir al punto final [/userinfo ](https://appid-oauth.ng.bluemix.net/swagger-ui/#!/Authorization_Server_V3/userInfo) o extraer atributos personalizados más adelante, puesto que ya están almacenados en la señal.
{: shortdesc}


**¿Por qué debería añadir atributos a mis reclamaciones?**

En la señal encontrará todo lo que su app necesita saber sobre un usuario o lo que puede hacer, sin tener que hacer llamadas de red adicionales. Siempre que no tenga cantidades masivas de datos, esto hará que el proceso sea más efectivo. Además, puede garantizar la integridad de estos atributos correlacionados cuando se envíen a través de la red porque se almacenan en una señal firmada.

</br>

**¿Qué tipos de reclamaciones puedo definir?**

Las reclamaciones que {{site.data.keyword.appid_short_notm}} proporciona forman parte de varias categorías que se diferencian por su nivel de personalización.

*Reclamaciones registradas*: Hay varias reclamaciones en las señales de identidad y acceso que {{site.data.keyword.appid_short_notm}} define y que las correlaciones personalizadas no pueden alterar. Si la reclamación está restringida, el servicio la ignora. Las reclamaciones son `iss`, `aud`, `sub`, `iat`, `exp`, `amr` y `tenant`.

*Reclamaciones restringidas*: En función de la señal con la que se correlacionan las reclamaciones, algunas tienen posibilidades de personalización limitadas. Para una señal de acceso, `scope` es la única reclamación restringida. No se puede alterar temporalmente mediante correlaciones personalizadas, pero se puede ampliar con sus propios ámbitos. Cuando la reclamación de ámbito se correlaciona con una señal de acceso, el valor debe ser una serie y no puede tener el prefijo `appid_` o se ignorará. En las señales de identidad, las reclamaciones `identities` y `oauth_clients` no se pueden modificar ni alterar temporalmente.

*Reclamaciones normalizadas*: Cada señal de identidad contiene un conjunto de reclamaciones reconocido por {{site.data.keyword.appid_short_notm}} como reclamaciones normalizadas. Cuando están disponibles, se correlacionan directamente del proveedor de identidad a la señal. Estas reclamaciones no se pueden omitir de forma explícita, pero pueden ser alteradas temporalmente por correlaciones de reclamaciones personalizadas. Entre las reclamaciones se incluyen `name`, `email`, `picture`, `local` y `gender`.

</br>

**¿Cómo se definen las reclamaciones?**

Cada correlación está definida por un objeto de origen de datos y una clave que se utiliza para recuperar la reclamación. Cada reclamación personalizada se establece en cada señal por separado y secuencialmente. Puede registrar hasta 100 reclamaciones para cada señal hasta una carga útil máxima de 100 KB.

<table>
    <thead>
      <th colspan=3><img src="images/idea.png" alt="icono Idea"/> Comprensión de los objetos de correlación de reclamaciones</th>
    </thead>
    <tbody>
      <tr>
        <td><code><em>source</em></code></td>
        <td>Necesario</td>
        <td>Define el origen de la reclamación. Puede hacer referencia a la información de usuario del proveedor de identidad o a los atributos personalizados de {{site.data.keyword.appid_short_notm}} del usuario. </br> </br> Entre las opciones se incluyen: `saml`, `cloud_directory`, `facebook`, `google`, `appid_custom`, `ibmid` y `attributes`.</td>
      </tr>
      <tr>
        <td><code><em>sourceClaim</em></code></td>
        <td>Necesario</td>
        <td>Define la reclamación de los datos de origen. </td>
      </tr>
    </tbody>
  </table>

Puede hacer referencia a las reclamaciones añadidas en las correlaciones utilizando la sintaxis de punto. Ejemplo: `nested.attribute`
{:tip}

</br>

## Configuración de las señales de {{site.data.keyword.appid_short_notm}}
{: #configuring-tokens}

Puede configurar las señales de {{site.data.keyword.appid_short_notm}} utilizando la GUI o las API de gestión.
{: shortdesc}

### Configuración del período de vida con la GUI
{: #configuring-tokens-ui}

1. Vaya al panel de control del servicio.
2. En la sección **Proveedores de identidad** de la navegación, seleccione la página **Gestionar**.
3. En el separador **Valores** configure las señales.
  1. Para permitir el inicio de sesión sin la interacción del usuario, establezca las **señales de renovación** en **Activado**.
  2. Establezca el período de vida de la señal de renovación. La caducidad se establece en días y puede ser cualquier valor que se encuentre en un rango de 1 a 90. Cuanto menor sea el número, el usuario deberá registrarse con más frecuencia.
  3. Establezca el período de vida de la señal de acceso. La caducidad se establece en minutos y puede tener un rango entre 5 y 1440. Cuanto menor sea el valor, dispondrá de más protección cuando le roben la señal.
  4. Establezca el período de vida de la señal anónima. Una [señal anónima](/docs/services/appid/progressive.html#anonymous) se asigna a los usuarios en el momento en que empiezan a interactuar con la app. Cuando un usuario inicia sesión, la información de la señal anónima se transfiere a la señal asociada con el usuario. La caducidad se establece en días y puede ser cualquier valor entre 1 y 90.

</br>

### Configuración de señales con las API de gestión
{: #configuring-tokens-api}

**Antes de empezar**

Asegúrese de que tiene los requisitos previos siguientes:

* El ID de arrendatario de la instancia de {{site.data.keyword.appid_short_notm}}. Lo encontrará en la sección **Credenciales de servicio** de la GUI.
* La señal Gestión de identidad y acceso (IAM). Si necesita ayuda para obtener la señal de IAM, consulte los [documentos de IAM](/docs/iam/apikey_iamtoken.html).

**Correlación de reclamaciones**

1. Haga una solicitud PUT al punto final `/config/tokens` con la configuración de la señal.

  Cabecera:
  ```
  PUT {management-url}/management/v4/{tenantId}/tokens
       Host: <management-server-url>
       Authorization: 'Bearer <IAM_TOKEN>'
       Content-Type: application/json
  ```
  {: pre}

  Cuerpo:
  ```
   {
       "access": {
           "expires_in": 3600,
       },
       "refresh": {
           "expires_in": 2592000,
           "enabled": true
       },
       "anonymous": {
           "expires_in": 2592000,
           "enabled": true
       },
       "accessTokenClaims": [
           {
              "source": "saml",
              "sourceClaim": "name_id"
           }
       ],
       "idTokenClaims": [
           {
              "source": "saml",
              "sourceClaim": "attributes.uid"
           }
       ]
   }
  ```
  {: pre}

  <table>
    <thead>
      <th colspan=3><img src="images/idea.png" alt="Icono Idea"/> Comprensión de la configuración de la señal</th>
    </thead>
    <tbody>
      <tr>
        <td><code><em>access</em></code></td>
        <td>Opcional</td>
        <td>El objeto que contiene la hora de caducidad, `expires_in`, en minutos, de las señales de identidad y acceso. </br> </br> La caducidad predeterminada es 60 minutos. </td>
      </tr>
      <tr>
          <td><code><em>refresh</em></code></td>
          <td>Opcional</td>
          <td>El objeto que contiene la hora de caducidad, `expires_in`, en días, de la señal de renovación. </br> </br> La caducidad predeterminada es 30 días. </td>
      </tr>
      <tr>
          <td><code><em>anonymousAccess</em></code></td>
          <td>Opcional</td>
          <td>El objeto que contiene la hora de caducidad, `expires_in`, en días, de las señales de identidad y acceso anónimas. </br> </br> La caducidad predeterminada es 30 días.
      </tr>
      <tr>
          <td><code><em>accessTokenClaims</em></code></td>
          <td>Opcional</td>
          <td>Una matriz que contiene los objetos que se crean cuando las reclamaciones relacionadas con las señales de acceso se correlacionan.</td>
      </tr>
      <tr>
          <td><code><em>idTokenClaims</em></code></td>
          <td>Opcional</td>
          <td>Una matriz que contiene los objetos que se crean cuando las reclamaciones relacionadas con las señales de identidad se correlacionan.</td>
      </tr>
    </tbody>
  </table>

  Solicitud de ejemplo:
  ```
  $ curl -X PUT
    --header 'Content-Type: application/json'
    --header 'Accept: application/json'
    --header 'Authorization: <IAM Token'
    -d '{
          "accessTokenClaims": [
            {
              "source": "saml",
              "sourceClaim": "name_id"
            }
          ],
          "idTokenClaims": [
            {
              "source": "attributes",
              "sourceClaim": "theme"
            }
          ]
      }'
  }' '{management-url}/management/v4/{Tenant ID}/config/tokens'
  ```
  {: screen}
