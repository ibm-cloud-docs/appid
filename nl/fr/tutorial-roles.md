---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-31"

keywords: authentication, authorization, identity, app security, secure, access management, roles, attributes, users

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


# Tutoriel : Définition de rôles utilisateur
{: #tutorial-roles}

S'assurer que les bonnes personnes disposent des bons droits au bon moment peut s'avérer difficile lorsque vous codifiez votre application. Pour vous aider dans ce processus, vous pouvez utiliser {{site.data.keyword.appid_full}} afin de définir un attribut personnalisé tel que `rôle`, qui vous permet d'affecter différents types d'utilisateur. Ensuite, vous utilisez votre application pour imposer divers niveaux de droits à chaque type d'utilisateur. Ce guide pas à pas vous apprend à définir des attributs utilisateur puis à les injecter dans un jeton à l'aide des API {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

Des nouveautés dans les API ? Testez-les avec cette [ collection Postman](https://github.com/ibm-cloud-security/appid-postman).
{: tip}

## Scénario
{: #roles-scenario}

Vous êtes développeur d'un parc à thèmes de fiction. Vous êtes chargé de gérer l'accès à l'[application Web](/docs/services/appid?topic=appid-web-apps) et vous pensez que le moyen le plus simple est de définir des rôles pour chaque type d'utilisateur. Vous avez différents types de rôle tels que les employés du parc et les visiteurs qui ont tous besoin de différents niveaux de droits. Vous voulez rationaliser le processus et garantir que vos utilisateurs se voient affecter le rôle approprié lors de leur première connexion à votre application.  
{: shortdesc}

Pas de problème ! Vous pouvez utiliser la [fonctionnalité d'attributs personnalisés](/docs/services/appid?topic=appid-profiles) d'{{site.data.keyword.appid_short_notm}} pour stocker tout type d'information relative aux utilisateurs. Etant donné que vous travaillez avec le contrôle d'accès basé sur les rôles, vous pouvez créer un attribut nommé `rôle` et affecter différentes valeurs afin de spécifier un type de rôle. Par exemple, le parc à thèmes peut avoir des `visiteurs` (visitors) ou des `employés` (staff) ayant chacun des valeurs différentes pour l'attribut `rôle`. Ensuite, vous pouvez vos assurer que votre code d'application impose les privilèges et règles d'accès que vous affectez.

Bien que ce tutoriel soit écrit en ayant spécifiquement à l'esprit des applications Web et Cloud Directory, les attributs peuvent avoir une portée bien plus large. Les attributs personnalisés peuvent être tout ce que vous voulez qu'ils soient. Sous réserve que ce soit des attributs de moins de 100k et au format d'objet JSON ordinaire, vous pouvez stocker tout type d'information.
{: note}


## Avant de commencer
{: #roles-before}

Prêt ? Allons-y !

Avant de commencer, assurez-vous de disposer des prérequis suivants :
- Une instance du service {{site.data.keyword.appid_short_notm}}
- Un ensemble de données d'identification du service
- Une adresse de courrier électronique à laquelle vous pouvez accéder et valider


## Etape 1 : Configuration de votre instance {{site.data.keyword.appid_short_notm}}
{: #roles-configure-app}

Avant de commencer à ajouter des attributs pour les utilisateurs de votre parc sur le cloud, vous devez configurer votre instance {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

1. Dans l'onglet **Fournisseurs d'identité** du tableau de bord du service, activez **Cloud Directory**. Bien que ce tutoriel utilise [Cloud Directory](/docs/services/appid?topic=appid-cloud-directory), vous pouvez également utiliser tout autre fournisseurs d'identité tel que [SAML](/docs/services/appid?topic=appid-enterprise), [Facebook](/docs/services/appid?topic=appid-social#facebook), [Google](/docs/services/appid?topic=appid-social#google) ou un [fournisseur personnalisé](/docs/services/appid?topic=appid-custom-identity).

2. Dans l'onglet **Cloud Directory > Vérification de l'adresse électronique**, activez la vérification et définissez **Permettre aux utilisateurs de se connecter à votre application sans vérifier d'abord leur adresse électronique** sur **Non**. Lorsque vous utilisez des attributs personnalisés pour définir des rôles associés à des droits, assurez-vous que les utilisateurs doivent valider leur identité avant qu'ils n'assument les attributs que vous avez définis.

3. Dans l'onglet **Profils**, définissez **Changer les attributs personnalisés via l'application** sur **Désactivé**.

  Par défaut, toute personne qui détient un jeton d'accès peut modifier des attributs personnalisés. Pour garantir la sécurité de l'application, vous devez configurer {{site.data.keyword.appid_short_notm}} de sorte que les attributs personnalisés ne puissent être modifiés que par l'administrateur ou le propriétaire de l'application. Cela évite que les utilisateurs modifient constamment leurs propres attributs personnalisés et s'accordent des droits que vous ne voulez pas qu'ils détiennent.
  {: important}

Excellent ! Votre tableau de bord est configuré et vous êtes prêt à définir des rôles.


## Etape 2 : Définition de rôles pour le compte d'un autre utilisateur avant connexion
{: #roles-set-before}

Le parc sur le cloud a un nouvel employé. Vous connaissez toutes les informations qui le concernent, mais il ne commence pas avant plusieurs jours. Vous pouvez [le pré-enregistrer](/docs/services/appid?topic=appid-preregister) en créant un profil et un utilisateur {{site.data.keyword.appid_short_notm}} qui contient des attributs tels que le rôle `staff`.
{: shortdesc}

Ce processus ne finalise pas l'enregistrement Cloud Directory. L'utilisateur doit encore s'inscrire pour que l'application hérite de l'attribut défini dans le profil que vous avez créé.
{: tip}

1. Connectez-vous à {{site.data.keyword.cloud_notm}} à l'aide de l'interface de ligne de commande.

  ```
  ibmcloud login
  ```
  {: codeblock}

2. Procurez-vous un jeton d'accès IAM.

  ```
  ibmcloud iam oauth-tokens
  ```
  {: codeblock}

3. Envoyez une requête POST afin de créer pour le nouvel utilisateur un profil utilisateur qui contient l'attribut `staff`. Vérifiez que vous pouvez accéder à l'adresse de courrier électronique que vous utilisez et la valider.

  ```
  curl --request POST \
  https://us-south.appid.cloud.ibm.com/management/v4/{{APPID_TENANT_ID}}/users \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  - d '{
    "idp": "cloud_directory",
    "idp-identity": “user@email.com“,
    "profile": {
      "attributes": {
        “role”: “staff”
      }
    }
  }'
  ```
  {: codeblock}

  Sortie sur réussite :

  ```
  {
      "id": "5ty78b09-1356-4py8-l45p-808l633101zz"
  }
  ```
  {: screen}

6. Vérifiez que le profil a été créé avec le rôle `staff`.

  ```
  curl --request GET \
  https://us-south.appid.cloud.ibm.com/management/v4/<tenant-ID>/users?email=<user-email> \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  ```
  {: codeblock}

  Corps de la sortie sur réussite :

  ```
  {
      "users": [
          {
              "idp": "nominated_cloud_directory",
              "id": "5ty78b09-1356-4py8-l45p-808l633101zz"
          }
      ]
  }
  ```
  {: screen}

Bon travail ! Vous avez pré-enregistré un utilisateur pour votre application. Maintenant, lorsqu'il se connecte à votre application avec l'identificateur que vous avez utilisé pour le pré-enregistrement, un utilisateur Cloud Directory qui hérite du profil utilisateur {{site.data.keyword.appid_short_notm}} est créé. Ensuite, apprenez à mettre à jour des attributs.


## Etape 3: Mise à jour des attributs utilisateur
{: #roles-update-attributes}

Votre parc sur le cloud s'agrandit. Pour suivre le rythme de sa croissance, votre société embauche de nouveaux employés. L'utilisateur `staff` de l'étape 2 est désormais un responsable. Vous pouvez mettre à jour son profil en lui [affectant un nouveau rôle](/docs/services/appid?topic=appid-profiles#profile-set-custom).
{: shortdesc}

1. Mettez à jour le profil.

  ```
  curl --request PUT \
  https://us-south.appid.cloud.ibm.com/management/v4/<tenant-id>/users/<user-id>/profile \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  - d '{
    "profile": {
      "attributes": {
        “role”: “manager”
      }
    }
  }'
  ```
  {: codeblock}

3. Affichez le profil pour vérifier qu'il a été correctement mis à jour.

  ```
  curl --request POST \
  GET https://us-south.appid.cloud.ibm.com/management/v4/{{APPID_TENANT_ID}}/users/{{user_profile_id}}/profile \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  ```
  {: codeblock}

  Sortie sur réussite :

  ```
  {
      "id": "5ce78e09-1356-4ef8-a45d-808b633101db",
      "identities": [],
      "attributes": {
          "role": "manager"
      }
  }
  ```
  {: screen}

Bon travail !


## Etape 4 : Injection d'attributs dans des jetons
{: #roles-map-claims}

De plus en plus populaires, le parc continue à s'agrandir. Avec de si nombreux nouveaux visiteurs et employés, vous voulez limiter le nombre de demandes qui sont faites. Pour améliorer les performances, vous pouvez mapper les attributs de profil utilisateur sur vos réclamations de jetons d'accès et d'identité. Le mappage des réclamations personnalisées vous permet de stocker les attributs personnalisés dans les jetons eux-mêmes.
{: shortdesc}

La [Configuration des jetons](/docs/services/appid?topic=appid-customizing-tokens#customizing-tokens) s'effectue globalement, c'est-à-dire qu'elle s'applique à tout utilisateur ayant un attribut `role`, quel que soit le rôle qui lui a été attribué.
{: tip}


1. Envoyez une demande au noeud final de configuration de jeton.

  ```
  curl --request PUT \
  https://us-south.appid.cloud.ibm.com/management/v4/{{APPID_TENANT_ID}}/config/tokens \
  --header 'Authorization: Bearer <iam-access-token>' \
  --header 'Content-Type: application/json' \
  - d '{
      "access": {
          "expires_in": 3601
      },
      "refresh": {
          "enabled": false,
          "expires_in": 2592001
      },
      "anonymousAccess": {
          "expires_in": 2592001
      },
      "accessTokenClaims": [
      {
      "source": "attributes",
      "sourceClaim": "role"
      }
      ]
  }'
  ```
  {: codeblock}

  <table>
    <tr>
      <th>Variable</th>
      <th>Description</th>
    </tr>
    <tr>
      <td><code>tenant-id</code></td>
      <td>Un ID titulaire identifie votre instance {{site.data.keyword.appid_short_notm}} dans la demande. Cet ID figure dans l'onglet <em>Données d'identification pour le service</em> du tableau de bord. Si aucun ID n'est défini, suivez la procédure de création de données d'identification dans l'interface graphique.</td>
    </tr>
    <tr>
      <td><code>source</code></td>
      <td>Pour <code>accessTokenClaim</code> et <code>idTokenClaims</code> définissez la source sur <code>attribute</code>.</td>
    </tr>
    <tr>
      <td><code>sourceClaim</code></td>
      <td>Pour <code>accessTokenClaim</code> et <code>idTokenClaims</code> définissez la réclamation de source sur <code>role</code>.</td>
    </tr>
    <tr>
      <td><code>expires_in</code></td>
      <td>Cette valeur s'applique à chaque type de jeton et doit être définie dans chaque demande. Si vous avez précédemment défini la valeur dans l'interface graphique et exécutez ensuite cette demande, les valeurs de la demande se substituent à celles précédemment définies. Veillez à définir une valeur d'expiration correcte pour votre configuration.</td>
    </tr>
  </table>

  Sortie sur réussite :

  ```
  {
      "access": {
          "expires_in": 3601
      },
      "refresh": {
          "enabled": false,
          "expires_in": 2592001
      },
      "anonymousAccess": {
          "expires_in": 2592001
      },
      "accessTokenClaims": [
      {
      "source": "attributes",
      "sourceClaim": "role"
      }
      ]
  }
  ```
  {: screen}


## Etape 5 : Affichage du jeton d'accès
{: #roles-view-token}

Vous pouvez vérifier si l'étape 4 a réussi en affichant un jeton d'accès.
{: shortdesc}

1. A des fins de test, créez un utilisateur Cloud Directory à l'aide de l'interface graphique {{site.data.keyword.appid_short_notm}}.

  1. Dans l'onglet **Utilisateurs**, cliquez sur **Ajouter un utilisateur**. Un écran s'affiche.
  2. Entrez un prénom et un nom, une adresse électronique et un mot de passe.
  3. Cliquez sur **Sauvegarder**.

2. Codez votre ID client et votre secret.

  1. Dans l'onglet **Données d'identification pour le service** de l'interface graphique {{site.data.keyword.appid_short_notm}}, copiez l'ID client et le secret.
  2. Utilisez un encodeur en Base64 pour encoder vos informations d'autorisation.
  3. Copiez la sortie à utiliser dans la commande suivante.

4. Connectez-vous à l'aide des API afin d'obtenir vos informations de jeton d'accès. Le jeton renvoyé est codé.

  ```
  curl --request PUT \
  https://appid.cloud.ibm.com/oauth/v4/<tenant-ID>/token \
  --header 'Authorization: Basic <encoded-clientID>:<encoded-client-secret>' \
  --header 'Content-Type: application/x-www-form-urlencoded' \
  --header `Accept: application/json`
  - d 'grant_type=password&username=<user-email>%40<user-email-domain>&password=<user-password>
  ```
  {: codeblock}

5. Décodez votre jeton d'accès.
  1. Copiez le jeton de la sortie de réponse de la précédente commande.
  2. Dans un navigateur, accédez à https://jwt.io/.
  3. Collez le jeton dans la zone intitulée **Codé**.

6. Dans la section **Décodé**, vérifiez que vous voyez le rôle.

  ```
  {
    "iss": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61",
    "exp": 1551903163,
    "aud": [
      "968c2306-9aef-4109-bc06-4f5ed6axi24a"
    ],
    "sub": "2b96cc04-eca5-4122-a8de-6e07d14c13a5",
    "email_verified": true,
    "amr": [
      "cloud_directory"
    ],
    "iat": 1551899553,
    "tenant": "39a37f57-a227-4bfe-a044-93b6e6050a61",
    "scope": "openid appid_default appid_readprofile appid_readuserattr appid_writeuserattr appid_authenticated"
    "role": "manager"
  }
  ```
  {: screen}



## Etapes suivantes
{: #roles-next}

Beau travail ! Vous avez terminé le tutoriel. Ensuite, vous pouvez essayer de configurer l'[authentification multi-facteur](/docs/services/appid?topic=appid-cd-mfa) ou [votre propre interface graphique de marque](/docs/services/appid?topic=appid-branded).
