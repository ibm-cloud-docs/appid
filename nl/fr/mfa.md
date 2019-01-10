---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}


# Authentification multi-facteur
{: #mfa}

L'authentification multi-facteur (MFA) est une méthode qui permet de confirmer l'identité d'un utilisateur en lui demandant d'utiliser un élément qu'il possède en plus d'un élément qu'il connaît pour vérifier qu'il est bien qui il prétend être. Par exemple, avec {{site.data.keyword.appid_full}}, vous pouvez demander à un utilisateur de saisir un code unique qui lui est envoyé par courrier électronique après avoir saisi son adresse électronique et son mot de passe.
{: shortdesc}

L'authentification MFA est uniquement disponible pour les utilisateurs Cloud Directory.  Si vous utilisez une connexion d'entreprise avec SAML 2.0 ou une connexion sociale, vous pouvez activer l'authentification MFA dans le fournisseur d'identité que vous utilisez.
{: note}

Lorsque l'authentification MFA est activée, le widget de connexion exige une authentification MFA chaque fois qu'un nouvel utilisateur tente de se connecter. Lorsque l'utilisateur a correctement saisi ses données d'identification, un code d'accès unique est envoyé à l'adresse électronique enregistrée lors de la création de son compte. Chaque code est composé de six caractères et dispose d'un délai d'expiration de cinq minutes. Si un utilisateur ne reçoit pas son code, il peut demander qu'un autre code lui soit envoyé mais le délai d'expiration n'est pas réinitialisé. Après l'expiration du code, l'utilisateur est obligé de recommencer tout le processus de connexion.

Si l'adresse électronique d'un utilisateur n'a pas déjà été confirmée par les API de gestion ou la vérification du courrier électronique lors de l'inscription, elle est confirmée lorsque la vérification du code d'authentification MFA aboutit. Si vous devez modifier l'adresse électronique d'un utilisateur, un administrateur peut utiliser les API de gestion [](https://appid-management.ng.bluemix.net/swagger-ui/#!/Cloud_Directory_Users/updateCloudDirectoryUser).

L'authentification MFA est disponible pour les instances de {{site.data.keyword.appid_short_notm}} qui figurent sur le [plan de tarification à tranches graduées](faq.html#pricing).
{: note}

## Comprendre le flux
{: #understanding}



1. L'utilisateur de l'application est présenté dans l'interface utilisateur de connexion par défaut de l'{{site.data.keyword.appid_short_notm}}.

2. L'utilisateur entre ses données d'identification de l'utilisateur Cloud Directory, telles que son adresse électronique ou ses nom d'utilisateur et mot de passe.

3. Les données d'identification sont validées et le formulaire MFA est renvoyée. Le formulaire demande à l'utilisateur de coller le code envoyé par courrier électronique.

4. L'utilisateur reçoit un code d'accès unique à son adresse électronique et l'entre dans l'interface utilisateur MFA par défaut.

5. Le code MFA est validé et redirigé vers l'application client avec le code d'autorisation pour continuer le flux OAuth 2.


</br>

## Configurer l'authentification MFA
{: #configuration}

L'authentification MFA {{site.data.keyword.appid_short_notm}} est prise en charge dans le flux de code d'autorisation OAuth 2.0 pour les utilisateurs Cloud Directory via le widget de connexion.
{: shortdesc}

Pour configurer l'authentification MFA via l'interface graphique, consultez [Cloud Directory](cloud-directory.html).
{: note}

### Configurer à l'aide de l'API

Vous pouvez configurer l'authentification MFA à l'aide des API de gestion.
{: shortdesc}

**Avant de commencer**

Assurez-vous de disposer des prérequis suivants :

* Votre ID titulaire d'instance {{site.data.keyword.appid_short_notm}}. Il est disponible dans la section **Données d'identification pour le service** du tableau de bord.
* Votre jeton IAM (Identity and Access Management). Pour obtenir de l'aide sur le jeton IAM, consultez la [documentation IAM](/docs/iam/apikey_iamtoken.html).


1. Activez l'authentification MFA en envoyant une requête PUT au noeud final `/config/mfa` avec votre configuration MFA pour définir `isActive` sur `true`.

  En-tête :
  ```
  PUT {management-url}/management/v4/{tenantId}/config/mfa
       Host: <management-server-url>
       Authorization: Bearer <IAM_TOKEN>
       Content-Type: application/json
  ```
  {: pre}

  Corps de texte :
  ```
   {
       "isActive": true
   }
  ```
  {: pre}

  Exemple de demande :
  ```
  $ curl -X PUT
    --header 'Content-Type: application/json'
    --header 'Accept: application/json'
    --header 'Authorization: Bearer <IAM_TOKEN>'
    -d '{
          "isActive": true
      }'
    }'
    '{management-url}/management/v4/{tenantId}/config/mfa'
  ```
  {: screen}

2. Activez votre canal MFA en envoyant une requête PUT au noeud final `/mfa/channels/{channelType}` avec votre configuration MFA. Lorsque `isActive` est défini sur `true`, votre canal MFA est activé.

  En-tête :
  ```
  PUT /management/v4/{tenantId}/mfa/channels/{channelType}
       Host: <management-server-url>
       Authorization: Bearer <IAM_TOKEN>
       Content-Type: application/json
  ```
  {: pre}

  <table>
    <thead>
      <th colspan=3>Types de canaux pris en charge</th>
    </thead>
    <tbody>
      <tr>
        <td>`email`</td>
      </tr>
    </tbody>
  </table>

  Corps de texte :
  ```
   {
       "isActive": true
   }
  ```
  {: pre}

  Exemple de demande :
  ```
  $ curl -X PUT
    --header 'Content-Type: application/json'
    --header 'Accept: application/json'
    --header 'Authorization: Bearer <IAM_TOKEN>'
    -d '{
          "isActive": true
      }'
    }'
    '{management-url}/management/v4/{tenantId}/mfa/channels/{channelType}'
  ```
  {: screen}

</br>
