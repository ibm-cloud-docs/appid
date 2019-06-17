---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-06"

keywords: Authentication, authorization, identity, app security, secure, rates, cloud directory, rate limit, attempts

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


# Límites de App ID
{: #limits}

La limitación de velocidad se utiliza para controlar la cantidad de tráfico que viene y se pasa a través de la instancia de App ID. Limitando las solicitudes o los recursos, puede proteger las aplicaciones.
{: shortdesc}

## Plan Lite de App ID 
{: #lite-limits}

Revise la tabla siguiente para ver los límites que hay en vigor para las instancias Lite de App ID. 

<table>
    <tr>
        <th>Recurso</th>
        <th>Máximo</th>
    </tr>
    <tr>
        <td>Usuarios</td>
        <td>1000</td>
    </tr>
    <tr>
        <td>Autenticaciones</td>
        <td>1000 al mes</td>
    </tr>
</table>

## General
{: #general-limits}

En la tabla siguiente se listan los límites máximos por usuario para los recursos de IBM Cloud App ID y el periodo de bloqueo cuando se sobrepasan los límites. Estos límites se aplican a cualquier usuario que pueda crear recursos de IBM Cloud App ID.
{: shortdesc}

<table>
    <tr>
        <th>API</th>
        <th>Límite</th>
        <th>Cuando se supera</th>
    </tr>
    <tr>
        <td>Intentos de inicio de sesión por parte de un usuario</td>
        <td>5 por minuto</td>
        <td>El usuario no podrá iniciar sesión durante 1 minuto.</td>
    </tr>
    <tr>
        <td>Actualización de los atributos del perfil de usuario</td>
        <td>5 por minuto</td>
        <td>El usuario no podrá actualizar el perfil durante 1 minuto.</td>
    </tr>
        <td>Suprimir atributos del perfil de usuario</td>
        <td>5 por minuto</td>
        <td>El usuario no podrá actualizar el perfil durante 1 minuto.</td>
    </tr>
</table>



## Directorio en la nube
{: #limits-cd}

Revise la tabla siguiente para ver los límites asociados al Directorio en la nube.
{: shortdesc}

<table>
    <tr>
        <th>API</th>
        <th>Configurable</th>
        <th>Límite</th>
        <th>Cuando se supera</th>
    </tr>
    <tr>
        <td>Intentos de inicio de sesión por cuenta</td>
        <td>Sí</td>
        <td>Ilimitado</td>
        <td>Se bloquean todos los intentos de inicio de sesión en la instancia durante un minuto.</td>
    </tr>
    <tr>
        <td>Intentos de registro por cuenta</td>
        <td>Sí</td>
        <td>Ilimitado</td>
        <td>Se bloquean todos los intentos de registrarse en la instancia durante un minuto.</td>
    </tr>
    <tr>
        <td>Solicitud de envío de correo</td>
        <td>No</td>
        <td>10 correos electrónicos en 10 minutos por usuario</td>
        <td>Se bloquean las solicitudes de correo electrónico para el usuario durante 30 minutos.</td>
    </tr>
</table>

Para obtener más información, consulte la sección <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateRateLimitConfig" target="_blank">API de gestión de limitación de velocidad.</a>
