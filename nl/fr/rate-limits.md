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


# Limites d'App ID
{: #limits}

La limitation du débit est utilisée pour contrôler la quantité de trafic qui entre et sort de votre instance App ID. En limitant les demandes ou les ressources, vous pouvez protéger vos applications.
{: shortdesc}

## Plan lite d'App ID 
{: #lite-limits}

Examinez le tableau suivant pour voir les limites qui sont en place pour les instances lite d'App ID. 

<table>
    <tr>
        <th>Ressource</th>
        <th>Maximum</th>
    </tr>
    <tr>
        <td>Utilisateurs</td>
        <td>1000</td>
    </tr>
    <tr>
        <td>Authentifications</td>
        <td>1000 par mois</td>
    </tr>
</table>

## Informations générales
{: #general-limits}

Le tableau suivant répertorie les limites maximales par utilisateur pour les ressources IBM Cloud App ID et la période de blocage lorsque les limites sont dépassées. Ces limites s'appliquent à tout utilisateur qui peut créer des ressources IBM Cloud App ID.
{: shortdesc}

<table>
    <tr>
        <th>API</th>
        <th>Limite</th>
        <th>En cas de dépassement</th>
    </tr>
    <tr>
        <td>Tentatives de connexion par un utilisateur</td>
        <td>5 par minute</td>
        <td>L'utilisateur ne peut pas se connecter pendant 1 minute.</td>
    </tr>
    <tr>
        <td>Mise à jour des attributs de profil d'utilisateur</td>
        <td>5 par minute</td>
        <td>L'utilisateur ne peut pas mettre à jour son profil pendant 1 minute.</td>
    </tr>
        <td>Suppression des attributs de profil d'utilisateur</td>
        <td>5 par minute</td>
        <td>L'utilisateur ne peut pas mettre à jour son profil pendant 1 minute.</td>
    </tr>
</table>



## Cloud Directory
{: #limits-cd}

Examinez le tableau suivant pour voir les limites associées à Cloud Directory.
{: shortdesc}

<table>
    <tr>
        <th>API</th>
        <th>Configurable</th>
        <th>Limite</th>
        <th>En cas de dépassement</th>
    </tr>
    <tr>
        <td>Tentatives de connexion par compte</td>
        <td>Oui</td>
        <td>Illimitées</td>
        <td>Toutes les tentatives de connexion de l'instance sont bloquées pendant une minute.</td>
    </tr>
    <tr>
        <td>Tentatives d'inscription par compte</td>
        <td>Oui</td>
        <td>Illimitées</td>
        <td>Toutes les tentatives d'inscription de l'instance sont bloquées pendant une minute.</td>
    </tr>
    <tr>
        <td>Demande d'envoi d'e-mail</td>
        <td>Non</td>
        <td>10 e-mails en 10 minutes par utilisateur</td>
        <td>Les demandes d'e-mail de l'utilisateur sont bloquées pendant 30 minutes.</td>
    </tr>
</table>

Pour plus d'informations, voir l'<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateRateLimitConfig" target="_blank">API de gestion des limites de débit</a>
