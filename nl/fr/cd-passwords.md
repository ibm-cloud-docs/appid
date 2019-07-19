---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-09"

keywords: Authentication, authorization, identity, app security, secure, directory, registry, passwords, languages, lockout

subcollection: appid

---

{:external: target="_blank" .external}
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

# Définition de règles sur les mots de passe
{: #cd-strength}

Vous pouvez définir les exigences relatives aux mots de passe pouvant être utilisés avec Cloud Directory. En définissant des exigences spécifiques auxquelles vos utilisateurs doivent se conformer, vous pouvez garantir la sécurité des applications.
{: shortdesc}

## Règle : force du mot de passe
{: #cd-password-strength}

Si le mot de passe est fiable, il est difficile, voire impossible, de le deviner manuellement ou à l'aide d'un programme. Pour définir des exigences concernant la force d'un mot de passe utilisateur, procédez comme suit :
{: shortdesc}

1. Accédez à l'onglet **Règles sur les mots de passe** du tableau de bord {{site.data.keyword.appid_short_notm}}.

2. Dans la case **Définir la force du mot de passe**, cliquez sur **Editer**. Un écran s'ouvre.

3. Entrez une expression régulière valide dans la zone **Force du mot de passe**.

  Exemples :
    - Doit comporter au moins 8 caractères. (`^.{8,}$`)
    - Doit comporter un chiffre, une lettre minuscule et une lettre majuscule. (`^(?:(?=.*\d)(?=.*[a-z])(?=.*[A-Z]).*)$`)
    - Ne doit comporter que des chiffres et des lettres anglaises. (`^[A-Za-z0-9]*$`)
    - Doit comporter au moins un caractère unique. (`^(\w)\w*?(?!\1)\w+$`)

4. Cliquez sur **Sauvegarder**.

La force du mot de passe peut être définie sur la page des paramètres de Cloud Directory dans la console {{site.data.keyword.appid_short_notm}} ou à l'aide des <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.set_cloud_directory_password_regex" target="_blank">API de gestion <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.
{: note}


## Règles avancées sur les mots de passe
{: #cd-advanced-password}


Vous pouvez améliorer la sécurité de votre application en appliquant des contraintes de mot de passe.
{: shortdesc}


Vous pouvez créer une politique de mot de passe avancée qui se compose de n'importe quelle combinaison des cinq caractéristiques suivantes :

 - Verrouillage après plusieurs données d'identification incorrectes
 - Interdiction de réutilisation des mots de passe
 - Expiration du mot de passe
 - Délai minimal entre les changements de mot de passe
 - Vérification du mot de passe pour s'assurer qu'il ne contient pas le nom de l'utilisateur


 Lorsque vous activez cette fonction, les fonctionnalités de sécurité avancée génèrent une facturation supplémentaire. Pour plus d'informations, voir [comment {{site.data.keyword.appid_short_notm}} calcule la tarification](/docs/services/appid?topic=appid-faq#faq-pricing).
 {: important}


### Règle : Interdiction de réutilisation des mots de passe
{: #cd-avoid-reuse}

Lorsque vos utilisateurs modifient leur mot de passe, vous pouvez les empêcher de choisir un mot de passe récemment utilisé.
{: shortdesc}

Vous pouvez choisir le nombre de mots de passe à partir duquel un utilisateur est en mesure de réutiliser un mot de passe déjà utilisé à l'aide de l'interface graphique ou de l'interface de programmation (API). Les options de ce paramètre comprennent une valeur entière comprise entre 1 et 10.

Lorsque cette option est activée, un utilisateur ne peut pas réutiliser un mot de passe qu'il a utilisé récemment. S'il tente de définir un mot de passe utilisé récemment, une erreur s'affiche dans l'interface graphique du widget de connexion par défaut et l'utilisateur est invité à entrer une autre option.

Les mots de passe précédents sont stockés de manière sécurisée de la même manière que le mot de passe actuel de l'utilisateur.
{: note}


### Règle : Verrouillage après plusieurs données d'identification incorrectes
{: #cd-lockout}

Si vous le souhaitez, vous pouvez protéger les comptes de vos utilisateurs en les empêchant temporairement de se connecter lorsqu'un comportement suspect est détecté, par exemple en cas de tentatives de connexion répétées avec un mot de passe incorrect. Cette mesure peut aider à empêcher un tiers malveillant d'accéder au compte d'un utilisateur en devinant son mot de passe.
{: shortdesc}

Vous pouvez définir le nombre maximal de tentatives de connexion infructueuses effectuées par un utilisateur avant que son compte ne soit temporairement verrouillé, à l'aide de l'interface graphique ou de l'interface de programmation. Vous pouvez également définir la durée de verrouillage du compte. Vous disposez des choix suivants :

* Nombre de tentatives : toute valeur entière comprise entre 1 et 10.
* Période de verrouillage : toute valeur entière, spécifiée en minutes, comprise entre 1 et 1440 minutes (24 heures).

Si un compte est verrouillé, les utilisateurs ne peuvent pas se connecter ni effectuer d'autres opérations en libre-service, telle que la modification de leur mot de passe, tant que la période de verrouillage spécifiée n'est pas terminée. Lorsque la période de verrouillage est terminée, l'utilisateur est automatiquement déverrouillé.

Vous pouvez déverrouiller un utilisateur avant la fin de la période de verrouillage. Pour savoir s'il est déverrouillé, vérifiez si la zone `active` est définie sur `false`. Vous pouvez également vérifier que son statut dans l'onglet **Utilisateurs** du tableau de bord du service est `désactivé`. Pour déverrouiller un utilisateur, vous devez utiliser [l'API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Cloud_Directory_Users/updateCloudDirectoryUser) pour définir la zone `active` sur `true`.


### Règle : Délai minimal entre les changements de mot de passe
{: #cd-minimum-time}

Vous pouvez empêcher vos utilisateurs de changer rapidement de mot de passe en définissant une durée minimale pendant laquelle ils devront attendre entre deux changements.
{: shortdesc}

Cette fonctionnalité est particulièrement utile lorsqu'elle est utilisée avec la règle d'interdiction de réutilisation des mots de passe. Sans cette limitation, un utilisateur pourrait simplement changer son mot de passe plusieurs fois de suite pour contourner la limitation de réutilisation des mots de passe récents. Vous pouvez sélectionner n'importe quelle valeur dans la plage comprise entre 1 et 720 heures (30 jours). La zone est spécifiée en heures.


### Règle : Expiration du mot de passe
{: #cd-expiration}

Pour des raisons de sécurité, vous serez peut-être amené à appliquer une politique de rotation des mots de passe afin d'obliger vos utilisateurs à changer leur mot de passe au bout d'une durée indiquée.
{: shortdesc}

Vous pouvez définir une période pendant laquelle les mots de passe de vos utilisateurs restent valides à l'aide de l'interface graphique ou de l'interface de programmation. Lorsque le mot de passe d'un utilisateur a expiré, ce dernier est obligé de le réinitialiser lors de la prochaine connexion. Vous pouvez sélectionner n'importe quel nombre de jours complets dans une plage allant de 1 à 90.

Vous pouvez commencer rapidement avec le widget de connexion en utilisant l'interface graphique par défaut fournie. L'utilisateur est invité à fournir un nouveau mot de passe avant la fin de la connexion.

Si vous utilisez une expérience de connexion personnalisée, une erreur est déclenchée lorsqu'un utilisateur tente de se connecter avec un mot de passe expiré. Il est de votre responsabilité de configurer votre application pour fournir l'expérience utilisateur nécessaire. Vous pouvez appeler l'API de modification du mot de passe pour définir le nouveau mot de passe.

Exemple de réponse du noeud final de jeton :

```javascript
{
  "error" : "invalid_grant",
  "error_description" : "Password expired",
  "user_id" : "356e065e-49da-45f6-afa3-091a7b464f51"
}
```
{: screen}

Lorsque cette option est activée pour la première fois, les mots de passe utilisateur existants n'ont pas de date d'expiration. La période d'expiration commence lorsque l'utilisateur modifie son de passe. Vous pouvez encourager les utilisateurs à mettre à jour leur mot de passe après avoir activé cette fonctionnalité.
{: note}


### Règle : vérification du mot de passe pour s'assurer qu'il ne contient pas le nom de l'utilisateur
{: #cd-no-username}

Pour des mots de passe plus forts, vous pouvez interdire aux utilisateurs d'inclure leur nom d'utilisateur ou la première partie de leur adresse électronique.
{: shortdesc}

Cette contrainte n'est pas sensible à la casse. Les utilisateurs ne sont pas en mesure de modifier la casse de tout ou partie des caractères afin d'utiliser les informations personnelles. Pour configurer cette option, basculez le commutateur sur **activé**.
{: note}

