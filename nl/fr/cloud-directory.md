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

# Cloud Directory
{: #cd}

Avec {{site.data.keyword.appid_full}}, les utilisateurs peuvent s'inscrire et se connecter à vos applications mobiles et Web à l'aide d'une adresse électronique ou d'un nom d'utilisateur et d'un mot de passe. Un répertoire cloud est un registre d'utilisateurs géré dans le cloud. Lorsqu'un utilisateur s'inscrit à votre application, il est ajouté à votre répertoire d'utilisateurs. Avec cette fonction, l'utilisateur final a la liberté de gérer son propre compte au sein de votre application.
{: shortdesc}

</br>

## Gestion des paramètres de répertoire
{: #cd-settings}

Vous pouvez configurer les notifications et le niveau de contrôle de votre application par les utilisateurs. La configuration du répertoire cloud peut s'effectuer rapidement, comme illustré dans l'image ci-dessous. Ces paramètres peuvent être mis à jour à tout moment à partir du tableau de bord du service.
{: shortdesc}


![Configuration du répertoire cloud](images/cloud-directory.png)
Figure. Procédure de configuration du répertoire cloud

1. Dans l'onglet **Gérer** du tableau de bord {{site.data.keyword.appid_short_notm}}, vérifiez que le répertoire cloud est défini sur **Activé**.

2. Configurez vos paramètres généraux.
  1. Choisissez si vous souhaitez que vos utilisateurs créent un nom d'utilisateur ou utilisent leur adresse électronique lorsqu'ils se connectent. Les deux options nécessitent un mot de passe. Une fois les utilisateurs ajoutés à votre répertoire, vous ne pouvez plus choisir entre les deux options.
  2. Cliquez sur **Editer** sur la ligne des critères de mot de passe pour spécifier toutes les exigences que vous souhaitez mettre en place. Les critères de mot de passe sont fournis sous forme d'expression régulière. Pour obtenir de l'aide sur la détermination de la force ou pour consulter des exemples courants, voir [Gestion de la force du mot de passe](#strength). Cliquez sur **Sauvegarder** pour mettre vos exigences en application.
  3. Définissez **Permettre aux utilisateurs de s'inscrire à votre application** sur **Oui**. Vous pouvez toujours ajouter des utilisateurs via la console si l'option est définie sur **Non** toutefois, vous ne devez le faire qu'à des fins de développement.
  4. Définissez **Permettre aux utilisateurs de gérer leur compte à partir de votre application** sur **Oui** si vous souhaitez que vos utilisateurs puissent réinitialiser leur mot de passe, le changer ou réinitialiser leurs détails. Si vous souhaitez limiter le libre-service à vos utilisateurs, définissez la valeur sur **Non**.
  5. Cliquez sur **Editer** sur la ligne **Détails sur l'expéditeur** pour mettre à jour vos paramètres de courrier électronique. Les paramètres de courrier électronique s'appliquent à toutes les communications envoyées via {{site.data.keyword.appid_short_notm}}. Spécifiez l'adresse électronique qui doit envoyer le courrier électronique, son nom et laissez un courrier électronique distinct pour que les utilisateurs envoient une réponse.
  6. Activez **Règles avancées sur les mots de passe** pour créer des limitations et des exigences temporelles pour vos mots de passe. Cette fonctionnalité nécessite une facturation supplémentaire. Pour plus d'informations sur vos options, voir [Règles avancées sur les mots de passe](#advanced-password).
  6. Cliquez sur **Sauvegarder**.

3. Configurez vos paramètres de courrier électronique de vérification.
  1. Pour que vos utilisateurs vérifient leur adresse électronique, définissez **Vérification de l'adresse électronique** sur **Activé**. Lorsqu'un utilisateur s'inscrit à votre application, il reçoit un courrier électronique lui demandant de confirmer qu'il s'est abonné à l'application.
  2. Si vous avez décidé de demander à vos utilisateurs de vérifier leur courrier électronique, vous devez ensuite les autoriser à entrer dans votre application avant de vérifier leur adresse électronique. Selon vos préférences, définissez **Permettre aux utilisateurs de se connecter à votre application sans vérifier d'abord leur adresse électronique** sur **Oui** ou sur **Non**.
  3. Personnalisez le contenu et concevez l'apparence de votre message. Un modèle de message existe, mais vous pouvez mettre à jour le texte avec votre propre message. Vous pouvez utiliser une autre [langue](/docs/services/appid/cloud-directory.html#languages) que l'anglais mais vous êtes responsable de la traduction du texte. Pour choisir une autre langue, utilisez les API de gestion des langues <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/updateLocalization" target="_blank"> <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.
  4. Attribuez à l'URL de vérification un délai d'expiration, exprimé en minutes. Lorsque cette période est définie ici, cela affecte également la durée de validité de votre lien de réinitialisation du mot de passe.
  5. Entrez votre propre URL de page de vérification si vous souhaitez que les utilisateurs voient une page spécifique lorsqu'ils cliquent sur le lien. Si vous laissez la zone **Custom verification page URL** vide, une page de vérification par défaut est fournie par {{site.data.keyword.appid_short_notm}}.
  6. Cliquez sur **Sauvegarder**.

4. Configurez vos paramètres de courrier électronique de bienvenue.
  1. Pour souhaiter la bienvenue par courrier électronique aux utilisateurs qui s'inscrivent à votre application, définissez **Courrier électronique de bienvenue** sur **Activé**.
  2. Personnalisez le contenu et concevez l'apparence de votre message. Vous pouvez utiliser un exemple de message ou mettre à jour le texte avec votre propre message. Vous pouvez utiliser une autre [langue](#languages) que l'anglais mais vous êtes responsable de la traduction du texte. Pour choisir une autre langue, utilisez les API de gestion des langues <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/updateLocalization" target="_blank"> <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.
  3. Cliquez sur **Sauvegarder**.

5. Configurez vos paramètres de réinitialisation de mot de passe.
  1. Pour autoriser les utilisateurs à demander la réinitialisation de leur mot de passe, définissez **E-mail d'oubli de mot de passe** sur **Activé**. **Remarque** : la validation de l'adresse électronique est une étape préalable à la réinitialisation du mot de passe. Cela signifie que vous devez exiger la vérification du courrier électronique pour autoriser les réinitialisations de mot de passe.
  2. Personnalisez le contenu et concevez l'apparence de votre message. Vous pouvez utiliser un exemple de message ou mettre à jour le texte avec votre propre message. Vous pouvez utiliser une autre [langue](#languages) que l'anglais mais vous êtes responsable de la traduction du texte. Pour choisir une autre langue, utilisez les API de gestion des langues <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/updateLocalization" target="_blank"> <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.
  3. Attribuez à l'URL de réinitialisation de mot de passe un délai d'expiration, exprimé en minutes. Lorsque cette période est définie ici, cela affecte également la durée de validité de votre lien de vérification de courrier électronique.
  4. Entrez votre propre URL de réinitialisation de mot de passe si vous souhaitez que les utilisateurs voient une page spécifique lorsqu'ils cliquent sur le lien. Si vous laissez la zone **URL de la page de redéfinition de mot de passe** vide, une page de réinitialisation de mot de passe par défaut est fournie par {{site.data.keyword.appid_short_notm}}.
  5. Cliquez sur **Sauvegarder**.

6. Configurez vos paramètres de modification de mot de passe.
  1. Pour avertir les utilisateurs des modifications apportées à leur mot de passe, définissez **Courrier électronique de changement de mot de passe** sur **Activé**.
  2. Personnalisez le contenu et concevez l'apparence de votre message. Vous pouvez utiliser un exemple de message ou mettre à jour le texte avec votre propre message. Vous pouvez utiliser une autre [langue](#languages) que l'anglais mais vous êtes responsable de la traduction du texte. Pour choisir une autre langue, utilisez les API de gestion des langues <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/updateLocalization" target="_blank"> <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.
  3. Cliquez sur **Sauvegarder**.

7. Configurez l'authentification multi-facteur.
  1. Pour exiger l'authentification multi-facteur lors de la connexion de l'utilisateur, définissez **Enable Email Multi-Factor Authentication** sur **Activé**.
  2. Personnalisez le contenu et la conception de votre courrier électronique à l'aide du modèle suivant. Vous pouvez utiliser une autre [langue](#languages) que l'anglais mais vous êtes responsable de la traduction du texte. Pour choisir une autre langue, utilisez les API de gestion des langues <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/updateLocalization" target="_blank"> <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.
  3. Cliquez sur **Sauvegarder**.

8. Dans l'onglet **Utilisateurs**, vous pouvez voir quels sont les utilisateurs inscrits à votre application. Remarque : un utilisateur unique peut tenter de se connecter jusqu'à 5 fois en 60 secondes. S'il tente de s'inscrire une sixième fois, une erreur s'affiche.

</br>
</br>

## Types de messages
{: #types}

Vous pouvez envoyer plusieurs types de message à vos utilisateurs. Vous pouvez envoyer l'exemple de message fourni par le service ou personnaliser le contenu du message pour une expérience d'application plus personnelle. {{site.data.keyword.appid_short_notm}} utilise <a href="https://www.sendgrid.com" target="_blank">SendGrid <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> comme service de distribution de courrier. Tous les courriers électroniques sont envoyés à l'aide d'un seul compte SendGrid.
{: shortdesc}

Un blanc apparaît à la place d'un paramètre si l'utilisateur n'a pas fourni l'information correspondante.
{: tip}

<dl>
  <dt>Bienvenue</dt>
    <dd><p>Une fois qu'un utilisateur est enregistré, vous pouvez lui adresse un courrier électronique de bienvenue dans votre application. Réservez le meilleur accueil à vos utilisateurs. Pour les fidéliser, choisissez un message aussi engageant que possible.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="Icône Plus d'informations"/> Tous les paramètres de message </th>
      </thead>
      <tbody>
        <tr>
          <td><code>%{display.logo}</code></td>
          <td> Affiche l'image que vous avez configurée pour votre widget de connexion. </td>
        </tr>
        <tr>
          <td><code>%{user.displayName}</code></td>
          <td> Affiche le pseudonyme (appelé nom d'écran dans l'interface) que l'utilisateur choisit d'utiliser lorsqu'il interagit avec l'application. </td>
        </tr>
        <tr>
          <td><code>%{user.email}</code></td>
          <td> Affiche l'adresse électronique avec laquelle l'utilisateur s'est inscrit. </td>
        </tr>
        <tr>
          <td><code>%{user.username}</code></td>
          <td> Affiche le nom d'utilisateur spécifié pour l'utilisateur lorsque l'authentification est effectuée à l'aide d'un nom d'utilisateur et d'un mot de passe. </td>
        </tr>
        <tr>
          <td><code>%{user.firstName}</code></td>
          <td> Affiche le prénom spécifié par l'utilisateur. </td>
        </tr>
        <tr>
          <td><code>%{user.formattedName}</code></td>
          <td> Affiche le nom complet de l'utilisateur. </td>
        </tr>
        <tr>
          <td><code>%{user.lastName}</code></td>
          <td> Affiche le nom de famille spécifié par l'utilisateur. </td>
        </tr>
      </tbody>
    </table></dd>
  <dt>Mot de passe oublié</dt>
    <dd><p>Un utilisateur peut demander à réinitialiser son mot de passe s'il l'a oublié ou s'il doit en changer pour une raison quelconque. Vous pouvez personnaliser le courrier électronique de réponse à cette demande. Le mot de passe restera inchangé tant que l'utilisateur n'aura pas cliqué sur le lien figurant dans ce courrier électronique de réponse.</p>
    <table>
      <tr>
        <th colspan=2><img src="images/idea.png" alt="Icône Plus d'informations"/> Paramètres d'oubli de mot de passe </th>
      </tr>
      <tr>
        <td><code>%{linkExpiration.hours}</code></td>
        <td> Affiche le nombre d'heures pendant lequel le lien est valide.</td>
      </tr>
      <tr>
        <td><code>%{linkExpiration.minutes}</code></td>
        <td>Affiche le nombre de minutes pendant lequel le lien est valide.</td>
      </tr>
      <tr>
        <td><code>%{resetPassword.code}</code></td>
        <td> Affiche un code d'accès à usage unique incorporé dans l'URL. Chaque personne recevra donc un code différent. Exemple : <code>https://appid.cloud.ibm.com/wfm</td>
      </tr>
      <tr>
        <td><code>%{resetPassword.link}</code></td>
        <td> Affiche le lien sur lequel l'utilisateur doit cliquer pour réinitialiser son mot de passe. </td>
      </tr>
     </tbody>
  </table></dd>
  <dt>Vérification</dt>
    <dd><p>Vous pouvez demander que l'utilisateur confirme l'existence de son compte mail en lui envoyant un courrier électronique à cet effet. Vous limiterez ainsi le nombre de faux comptes (notamment les robots) qui peuvent s'inscrire à votre application. Vous pouvez restreindre l'accès à votre application tant que l'utilisateur n'a pas prouvé la validité de son adresse électronique.
Utilisable aussi comme moyen de gérer pour quels utilisateurs vous créez des profils. Notez que les utilisateurs ajoutés manuellement via le tableau de bord {{site.data.keyword.appid_short_notm}} ou l'API de création d'utilisateur ne reçoivent pas automatiquement ce courrier électronique.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="Icône Plus d'informations"/> Paramètres de vérification de message </th>
      </thead>
      <tbody>
        <tr>
          <td><code>%{linkExpiration.hours}</code></td>
          <td> Affiche le nombre d'heures pendant lequel le lien est valide. </td>
        </tr>
        <tr>
          <td><code>%{linkExpiration.minutes}</code></td>
          <td> Affiche le nombre de minutes pendant lequel le lien est valide. </td>
        </tr>
        <tr>
          <td><code>%{verify.code}</code></td>
          <td> Affiche une URL de vérification à usage unique. </td>
        </tr>
        <tr>
          <td><code>%{verify.link}</code></td>
          <td> Affiche l'URL d'action que vous avez spécifiée dans les paramètres. </td>
        </tr>
      </tbody>
    </table></dd>
  <dt>Changement du mot de passe</dt>
    <dd><p>Vous pouvez faire savoir à l'utilisateur que son mot de passe a changé. Cette option est particulièrement utile s'il n'en a pas fait la demande. Il peut alors effectuer les étapes appropriées pour resécuriser son compte.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="Icône Plus d'informations"/> Paramètres de changement de mot de passe</th>
      </thead>
      <tbody>
        <tr>
          <td><code>%{passwordChangeInfo.time}</code></td>
          <td> Affiche l'heure à laquelle un nouveau mot de passe est entré en vigueur. </td>
        </tr>
        <tr>
          <td><code>%{passwordChangeInfo.ipAddress}</code></td>
          <td> Affiche l'adresse IP d'où provient la demande de changement de mot de passe. </td>
        </tr>
      </tbody>
    </table></dd>
    </dd>
    <dt>Code de vérification d'authentification multi-facteur</dt>
      <dd><p>Lorsque l'authentification multi-facteur est activée, les utilisateurs peuvent recevoir des codes challenge comme moyen secondaire d'authentification.</p>
      <table>
        <thead>
          <th colspan=2><img src="images/idea.png" alt="Icône Plus d'informations"/> Tous les paramètres de message </th>
        </thead>
        <tbody>
          <tr>
            <td><code>%{mfa.code}</code></td>
            <td> Affiche un code de vérification d'authentification multi-facteur unique. </td>
          </tr>
        </tbody>
      </table></dd></dl>

</br>
</br>

## Gestion de la force du mot de passe
{: #strength}

Vous pouvez définir les exigences relatives aux mots de passe pouvant être utilisés avec le répertoire cloud.
{: shortdesc}

Si le mot de passe est fiable, il est difficile, voire impossible, de le deviner manuellement ou à l'aide d'un programme. La force du mot de passe est définie en tant qu'expression régulière.

Voici quelques exemples de force communs pour le mot de passe :

- Il doit comporter au moins huit caractères. Exemple d'expression régulière : `^.{8,}$`
- Il doit contenir un chiffre, une lettre minuscule et une lettre majuscule. Exemple d'expression régulière : `^(?:(?=.*\d)(?=.*[a-z])(?=.*[A-Z]).*)$`
- Il ne doit comporter que des chiffres et des lettres en anglais. Exemple d'expression régulière : `^[A-Za-z0-9]*$`
- Il doit comporter au moins un caractère unique. Exemple d'expression régulière : `^(\w)\w*?(?!\1)\w+$`

La force du mot de passe peut être définie sur la page des paramètres du répertoire cloud de la console ID App ou à l'aide <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/set_cloud_directory_password_regex" target="_blank">des API de gestion <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.

</br>


## Règles avancées sur les mots de passe
{: #advanced-password}


Vous pouvez améliorer la sécurité de votre application en appliquant des contraintes de mot de passe supplémentaires.
{: shortdesc}


Les règles avancées sur les mots de passe consistent en 5 fonctionnalités qui peuvent être activées séparément.

 - Verrouillage après plusieurs données d'identification incorrectes
 - Interdiction de réutilisation des mots de passe
 - Expiration du mot de passe
 - Délai minimal entre les changements de mot de passe
 - Vérification que le mot de passe ne comporte pas de nom d'utilisateur


 L'activation de cette fonctionnalité de règles avancées sur les mots de passe génère une facturation supplémentaire. Pour plus d'informations, voir la [Calculatrice de prix](faq.html#pricing).

</br>

### Interdiction de réutilisation des mots de passe
{: #avoid-reuse}

Lorsque vos utilisateurs modifient leur mot de passe, vous pouvez les empêcher de choisir un mot de passe récemment utilisé.
{: shortdesc}

Vous pouvez choisir le nombre de mots de passe à partir duquel un utilisateur peut réutiliser un mot de passe déjà utilisé à l'aide de l'interface graphique ou de l'interface de programmation. Vous pouvez sélectionner n'importe quelle valeur entière comprise entre 1 et 10.

Si cette option est activée, et que l'un de vos utilisateurs tente de définir son mot de passe sur un mot de passe récemment utilisé, un message d'erreur s'affiche dans l'interface utilisateur du widget de connexion par défaut et invite l'utilisateur à entrer un autre mot de passe.

Les mots de passe précédents sont stockés de manière sécurisée de la même manière que le mot de passe actuel de l'utilisateur.

</br>

### Verrouillage après plusieurs données d'identification incorrectes
{: #lockout}

Si vous le souhaitez, vous pouvez protéger les comptes de vos utilisateurs en les empêchant temporairement de se connecter lorsqu'un comportement suspect est détecté, tel que plusieurs tentatives de connexion consécutives avec un mot de passe incorrect. Cette mesure peut aider à empêcher un tiers malveillant d'accéder au compte d'un utilisateur en devinant son mot de passe.
{: shortdesc}

Vous pouvez choisir de définir le nombre maximal de tentatives de connexion infructueuses qu'un utilisateur peut effectuer avant que son compte ne soit temporairement verrouillé à l'aide de l'interface graphique ou de l'interface de programmation. Vous pouvez également définir la durée de verrouillage du compte. Vous disposez des choix suivants :

* Nombre de tentatives : n'importe quelle valeur entière comprise entre 1 et 10.
* Période de verrouillage : n'importe quelle valeur entière comprise entre 1 minute et 24 heures, indiquée en minutes.

Si un compte est verrouillé, les utilisateurs ne peuvent pas se connecter ni effectuer d'autres opérations de libre-service, telle que la modification de leur mot de passe, tant que la période de verrouillage spécifiée n'est pas terminée. Lorsque la période de verrouillage est terminée, l'utilisateur est automatiquement déverrouillé.

Vous pouvez déverrouiller un utilisateur avant la fin de la période de verrouillage. Pour savoir s'il est déverrouillé, regardez si la zone `Actif` est définie sur `false`. Vous pouvez également vérifier que son statut dans l'onglet **Utilisateurs** du tableau de bord du service est `désactivé`. Pour déverrouiller un utilisateur, vous devez utiliser [l'API](https://appid-management.ng.bluemix.net/swagger-ui/#!/Cloud_Directory_Users/updateCloudDirectoryUser) pour définir la zone `Actif` sur `true`.

</br>

### Délai minimal entre les changements de mot de passe
{: #minimum-time}

Vous pouvez empêcher vos utilisateurs de changer rapidement de mot de passe en définissant une période minimale pendant laquelle ils devront attendre entre deux changements.
{: shortdesc}

Cette fonctionnalité est particulièrement utile lorsqu'elle est utilisée conjointement avec les règles régissant la réutilisation des mots de passe. Sans cette limitation, un utilisateur pourrait facilement et rapidement changer son mot de passe à plusieurs reprises pour contourner la règle relative à la réutilisation des mots de passe récemment utilisés. Vous pouvez sélectionner n'importe quelle valeur comprise entre 1 heure et 30 jours, indiquée en heures.

</br>

### Expiration du mot de passe
{: #expiration}

Pour des raisons de sécurité, vous pouvez souhaiter imposer une stratégie de rotation des mots de passe, de telle sorte que vos utilisateurs doivent modifier leur mot de passe après un certain temps.
{: shortdesc}

Vous pouvez définir une période pendant laquelle les mots de passe de vos utilisateurs resteront valides à l'aide de l'interface graphique ou de l'interface de programmation. Lorsque le mot de passe d'un utilisateur a expiré, ce dernier est obligé de le réinitialiser lors de la prochaine connexion. Vous pouvez sélectionner n'importe quel nombre de jours complets compris entre 1 et 90.

Le service fournit une interface graphique par défaut et une expérience immédiate grâce au widget de connexion. L'utilisateur est invité à fournir un nouveau mot de passe avant la fin de la connexion.

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

Lorsque cette option est activée pour la première fois, les mots de passe utilisateur existants n'ont pas de date d'expiration. Pour ces utilisateurs, la période d'expiration commence lorsque leur mot de passe est modifié. Vous pouvez encourager les utilisateurs à mettre à jour leur mot de passe après avoir activé cette fonctionnalité.
{: note}

</br>

### Vérification que le mot de passe ne comporte pas de nom d'utilisateur
{: #no-username}

Pour des mots de passe plus forts, vous pouvez interdire aux utilisateurs d'inclure leur nom d'utilisateur ou la première partie de leur adresse électronique.
{: shortdesc}

Cette contrainte n'est pas sensible à la casse, ce qui signifie que les utilisateurs ne sont pas en mesure de modifier la casse de tout ou partie des caractères afin d'utiliser les informations personnelles. Pour configurer cette option, basculez le commutateur sur **activé**.

</br>

## Utilisation d'un émetteur de courrier électronique personnalisé
{: #custom-email}

Avec {{site.data.keyword.appid_short_notm}}, vous pouvez définir un point d'extension personnalisé pour envoyer vos messages électroniques de répertoire cloud. La définition d'un point d’extension vous permet de contrôler entièrement l’envoi des courriers électroniques et d'utiliser votre propre nom de domaine.
 {: shortdesc}

**Pourquoi utiliser un émetteur de courrier électronique personnalisé ?**

Par défaut, {{site.data.keyword.appid_short_notm}} utilise SendGrid pour délivrer des messages en votre nom. La configuration de votre propre émetteur de courrier électronique personnalisé vous permet d'améliorer davantage l'expérience de marque des utilisateurs de votre application.

Quelques exemples plus spécifiques :
- **Domaine personnalisé**
La configuration d'un répartiteur de courriers électroniques personnalisé vous permet d'avoir un contrôle complet sur l'envoi des messages électroniques. Cela inclut la personnalisation du domaine d'e-mail, ce qui peut réduire davantage les risques de filtrage des emails en tant que spam.
- **Analyses et dépannage**
Obtenez des analyses de votre fournisseur d'e-mail telles que le nombre de personnes ayant ouvert les courriers électroniques ou les messages non distribués. Le fait de pouvoir suivre des messages individuels et consulter des statistiques globales peut vous aider à résoudre des problèmes.

</br>

**Principes de fonctionnement**

Une fois le point d'extension configuré, il est appelé par {{site.data.keyword.appid_short_notm}} chaque fois qu'un courrier électronique doit être envoyé. Le point d'extension contient toutes les informations sur le message, notamment le contenu final du corps du message.

</br>

**Pour créer un émetteur de courrier électronique personnalisé :**

1. Pour configurer l'instance {{site.data.keyword.appid_short_notm}} pour qu'elle utilise le répartiteur personnalisé, utilisez <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/set_cloud_directory_email_dispatcher" target="_blank">l'API de gestion</a>.</br>
Vous devez fournir l'adresse URL. Vous pouvez également fournir des informations d'autorisation. Les types d'autorisation pris en charge sont les suivants : `autorisation de base` ou `valeur d'en-tête de l'autorisation constante`.

  Exemples de configuration valide :
  ```
  {
    "custom": {
      "url": "https://example.com/send_mail"
    }
  }
  ```
  {: screen}

  ```
  {
    "custom": {
      "url": "https://example.com/send_mail",
      "authorization": {
        "type": "basic",
        "username": "username",
        "password": "password"
      }
    }
  }
  ```
  {: screen}

  ```
  {
    "custom": {
      "url": "https://example.com/send_mail",
      "authorization": {
        "type": "value",
        "value": "myApiKey"
      }
    }
  }
  ```
  {: screen}

2. Configurez un point d'extension pouvant écouter la demande d'envoi. Ce noeud final doit pouvoir lire le contenu provenant d'{{site.data.keyword.appid_short_notm}} et envoyer le courrier électronique avec votre émetteur de courrier électronique personnalisé.

3. Le corps envoyé depuis {{site.data.keyword.appid_short_notm}} est au format suivant : `{"jws": "jws-format-string"}`. </br> Après avoir décodé et vérifié le contenu, celui-ci est une chaîne JSON.</br>
  ```
    {
      "tenant": "tenant-id",
      "iss" : "appid-oauth.ng.bluemix.net",
      "iat": 1539173126,
      "jti": "uniq-id",
      "message": {
          "to": "your@mail.com",
          "from": {
              "name": "My Awesome Service",
              "address": "no-reply@company.com"
          },
          "replyTo": {
              "name": "My Awesome Service",
              "address": "yes-reply@company.com"
          },
          "subject": "Welcome to My Awesome Service",
          "body": "<p>Hello<p><br/><p>Thanks for signing up John Doe</p>"
      }
    }
  ```
  {: screen}

  - tenant : ID titulaire de l'instance App ID
  - iat : horodatage indiquant quand le message a été envoyé
  - iss : identifie l'entité émettrice principale de la signature des informations d'identité d'utilisateur (JWS).
  - jti : ID transaction unique
  - message : message à envoyer, comprend les zones suivantes :
    - to : adresse de courrier électronique de réception
    - from : informations sur l'expéditeur, comprend les zones suivantes :
      - name : facultatif, nom de l'expéditeur
      - address : adresse de l'expéditeur
    - reply to : facultatif, comprend les zones suivantes :
      - name : facultatif, nom de l'expéditeur
      - address : facultatif, adresse de l'expéditeur
    - subject : objet du courrier électronique
    - body : corps du courrier électronique, au format html

  Vous pouvez vérifier que votre demande a abouti en vérifiant le code d'état de la réponse. Toute réponse comprise entre 200 et 299 est considérée comme un succès. Si vous recevez une autre réponse, tentez de renvoyer la demande.
  {: tip}

4. Chaque contenu HTTP envoyé depuis {{site.data.keyword.appid_short_notm}} est automatiquement signé conformément à la norme JWS à l'aide d'une paire de clés asymétriques.
Pour chaque instance {{site.data.keyword.appid_short_notm}}, une clé privée et une clé publique sont générées et ne sont pas partagées par d'autres instances. La clé privée est utilisée pour signer le contenu HTTP. La clé publique permet de vérifier que le contenu est généré par {{site.data.keyword.appid_short_notm}} et n'est pas modifié par un tiers, <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#!/Authorization_Server_V3/publicKeys" target="_blank">Noeud final des clés publiques</a>.

5. Exemple de code de point d'extension (JavaScript)
  ```
  const sgMail = require('@sendgrid/mail');
  const {promisify} = require('bluebird');
  const request = promisify(require('request'));
  const jwtVerify = promisify(require('jsonwebtoken').verify);
  const jwtDecode = require('jsonwebtoken').decode;
  const jwkToPem = require('jwk-to-pem');

  async function obtainPublicKeys() {
  	// Your App ID instance tenant ID
  	const tenantId = '<TENANT-ID>';

  	// Send request to App ID's public keys endpoint
  	const keysOptions = {
  		method: 'GET',
  		url: `https://appid-oauth.<REGION>.bluemix.net/oauth/v3/${tenantId}/publickeys`
  	};
  	const keysResponse = await request(keysOptions);
  	return JSON.parse(keysResponse.body).keys;
  }

  async function verifySignature(keysArray, kid, jws) {
  	const keyJson = keysArray.find(key => key.kid === kid);
  	if (keyJson) {
  		const pem = jwkToPem(keyJson);
  		await jwtVerify(jws, pem);
  		return;
  	}
  	throw new Error ("Unable to verify signature");
  }

  async function verifyAndSendMail(jws) {
  	// The API key for Sendgrid
  	const sgApiKey = '<SENDGRID-API-KEY>';

  	// Init Sendgrind
  	sgMail.setApiKey(sgApiKey);

  	// Decode message to get information
  	const data = jwtDecode(jws, {complete: true});

  	// Extract kid from header
  	const kid = data.header.kid;

  	const keysArray = await obtainPublicKeys();

  	// Verify the signature of the payload with the public keys
  	await verifySignature(keysArray, kid ,jws);

  	// Send the email with Your Sendgrid account
  	const message = data.payload.message;
  	const msg = {
  		to: message.to,
  		from: message.from.address,
  		subject: message.subject,
  		html: message.body,
  	};
  	console.log(`Sending email to ${message.to}`);
  	let sendgridResponse = await sgMail.send(msg);

  	return {result : 'email_sent',sendgridResponse};
  }
  ```
  {: codeblock}

6. Vérifiez que votre configuration est correcte en testant votre répartiteur de courriers électroniques. Utilisez l'<a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/post_email_dispatcher_test" target="_blank">API de test</a> pour déclencher une demande auprès de votre émetteur de courrier électronique personnalisé configuré.

Pour un exemple complet, voir <a href="https://www.ibm.com/blogs/bluemix/2018/10/use-ibm-cloud-app-id-and-your-email-provider-to-brand-mails-sent-to-app-users/" target="_blank">Use your own provider for mail sent with {{site.data.keyword.appid_full}}</a>.

</br>
</br>


## Migration des utilisateurs
{: #user-migration}

Il est parfois nécessaire de configurer une nouvelle instance d'{{site.data.keyword.appid_short_notm}}. Si vous utilisez Cloud Directory, vos utilisateurs devront être migrés vers la nouvelle instance. Vous pouvez utiliser les API de gestion pour faciliter la migration.
{: shortdesc}

### Avant de commencer

Vous devez disposer du [rôle IAM](/docs/iam/quickstart.html) `Responsable` pour les deux instances d'{{site.data.keyword.appid_short_notm}}.

</br>

**Exportation**

Pour pouvoir ajouter vos utilisateurs à la nouvelle instance, vous devez les exporter à partir de votre instance actuelle. Pour ce faire, vous pouvez utiliser l'<a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Cloud_Directory_Users/cloudDirectoryExport" target="_blank">API de gestion des exportations <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.

Exemple de commande cURL :

```
curl -X GET --header ‘Accept: application/json’ --header ‘Authorization: Bearer <iam-token>’ ’https://eu-gb.appid.cloud.ibm.com/management/v4/111c9bj3-xxxx-4b5b-zzzz-24ad9440k8j9/cloud_directory/export?encryption_secret=myCoolSecret'
```
{: codeblock}

<table>
  <tr>
    <th>Variable</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>encryption_secret</code></td>
    <td>Chaîne personnalisée utilisée pour chiffrer et déchiffrer le mot de passe haché d'un utilisateur.</td>
  </tr>
  <tr>
    <td><code> tenantID </code></td>
    <td>L'ID titulaire du service se trouve dans vos données d'identification du service. Vos données d'identification du service sont disponibles dans le tableau de bord App ID.</td>
  </tr>
</table>

Seuls vos utilisateurs de Cloud Directory et leurs profils sont renvoyés. Les utilisateurs d'autres fournisseurs d'identité ne le sont pas.
{: note}

</br>

**Importation**

Maintenant que vos utilisateurs sont prêts, vous pouvez importer leurs informations dans la nouvelle instance. Pour ce faire, vous pouvez utiliser l'<a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Cloud_Directory_Users/cloudDirectoryImport" target="_blank">API de gestion des importations <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.

Exemple de commande cURL :

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
]}’ ‘https://eu-gb.appid.cloud.ibm.com/management/v4/111c9bj3-xxxx-4b5b-zzzz-24ad9440k8j9/cloud_directory/import?encryption_secret=myCoolSecret’
```
{: codeblock}

</br>

### Utilisation du script de migration

{{site.data.keyword.appid_short_notm}} fournit un script de migration que vous pouvez utiliser via l'interface CLI pour accélérer le processus de migration.

Avant de commencer, assurez-vous de disposer des informations sur les paramètres suivantes :

<table>
  <tr>
    <th> Paramètre        </th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>sourceTenantId</code></td>
    <td>ID titulaire de l'instance d'{{site.data.keyword.appid_short_notm}} à partir de laquelle vous prévoyez d'exporter des utilisateurs.</td>
  </tr>
  <tr>
    <td><code>destinationTenantId</code></td>
    <td>ID titulaire de l'instance d'{{site.data.keyword.appid_short_notm}} vers laquelle vous prévoyez d'importer des utilisateurs.</td>
  </tr>
  <tr>
    <td>Région</td>
    <td>Les options actuelles incluent : Sud des Etats-Unis : <code>ng</code>, Londres : <code>eu-gb</code>,  Sydney : <code>au-syd</code>, Washington : <code>us-east</code> et Allemagne : <code>eu-de</code>.</td>
  </tr>
  <tr>
    <td>Jeton IAM</td>
    <td>Assurez-vous de disposer des droits <code>responsable</code> avant d'obtenir le jeton. Pour obtenir de l'aide sur le jeton IAM, consultez la <a href="https://console.bluemix.net/docs/iam/apikey_iamtoken.html#iamtoken_from_apikey" target="_blank">documentation <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.</td>
  </tr>
</table>

Pour exécuter le script :

1. Clonez le <a href="https://github.com/ibm-cloud-security/appid-sample-code-snippets/tree/master/export-import-cloud-directory-users" target="_blank">référentiel <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.
2. Ouvrez le terminal et accédez au dossier dans lequel vous avez cloné le référentiel.
3. Exécutez la commande suivante.

  ```
  npm install
  ```
  {: codeblock}

4. Exécutez la commande suivante avec vos paramètres.

  ```
  users_export_import 'sourceTenantId' 'destinationTenantId' 'region' 'iamToken'
  ```
  {: codeblock}

  Exemple de commande :

  ```
  users_export_import e00a0366-53c5-4fcf-8fef-ab3e66b2ced8 73321c2b-d35a-497a-9845-15c580fdf58c ng eyJraWQiOiIyMDE3MTAyNS0xNjoyNzoxMCIsImFsZyI6IlJTMjU2In0.eyJpYW1faWQiOiJJQk1pZC0zMTAwMDBUNkZTIiwiaWQiOiJJQk1pZC0zMTAwMDBUNkZTIiwicmVhbG1pZCI6IklCTWlkIiwiaWRlbnRpZmllciI6IjMxMDAwMFQ2RlMiLCJnaXZlbl9uYW1lIjoiUm90ZW0iLCJmYW1pbHlfbmFtZSI6IkJyb3NoIiwibmFtZSI6IlJvdGVtIEJyb3NoIiwiZW1haWwiOiJyb3RlbWJyQGlsLmlibS5jb20iLCJzdWIiOiJyb3RlbWJyQGlsLmlibS5jb20iLCJhY2NvdW50Ijp7ImJzcyI6ImQ3OWM5YTk5NjJkYzc2Y2JkMDZlYTVhNzhjMjY0YzE5In0sImlhdCI6MTUzNzE3Mjg4NCwiZXhwIjoxNTM3MTc2NDg0LCJpc3MiOiJodHRwczovL2lhbS5zdGFnZTEuYmx1ZW1peC5uZXQvaWRlbnRpdHkiLCJncmFudF90eXBlIjoidXJuOmlibTpwYXJhbXM6b2F1dGg6Z3JhbnQtdHlwZTpwYXNzY29kZSIsInNjb3BlIjoiaWJtIG9wZW5pZCIsImNsaWVudF9pZCI6ImJ4IiwiYWNyIjoxLCJhbXIiOlsicHdkIl19.c4vLPzhvvNZLjaLy7znDa37qV4o-yuGmSKmJoQKrEQNZU8IC0NIjxwSo7W9kb0pDi3Yf_03_9ufTTGNfjtltzNWycSXjkNgoL-b9_nU61oHdgn0stY1KmNicqyBWfgUU--4xa904QN_QjRHBaUBeJf3XWEphPIMoF7mZeOxEZLnCMcQXSz9pImCMiP4SNT38cHLiI90Yx01rM7hpteepWULh5MYh-B2V03Gkgxfqvv951HF1LDg6eT4Q9in11laTQKtKuomripUju_4GIIjORVYw9NaAVKIJ9lKrPX0SKPhStsa59qGsC_7Uersms5EY1W1VbZVqOZPJbtp6tVf-Lw
  ```
  {: codeblock}

</br>
</br>


## Langues prises en charge
{: #languages}

Vous pouvez utiliser <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/updateLocalization" target="_blank">les API de gestion des langues <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> pour définir la langue dans laquelle la communication avec vos utilisateurs sera écrite. Toutefois, seul l'anglais est disponible sans configuration. Il vous appartient de traduire les messages. Une fois la configuration définie avec l'API, l'interface graphique est mise à jour pour que vous puissiez changer le texte de modèle.
{: shortdesc}

<table>
  <col width="20%">
  <col width="25%">
  <col width="35%">
  <tr>
    <th>Code</th>
    <th>Langue</th>
    <th>Région</th>
  </tr>
  <tr>
    <td><code>af-ZA</code></td>
    <td>Afrikaans</td>
    <td>Afrique du Sud</td>
  </tr>
  <tr>
    <td><code>sq-AL</code></td>
    <td>Albanais</td>
    <td>Albanie</td>
  </tr>
  <tr>
    <td><code>am-ET</code></td>
    <td>Amharique</td>
    <td>Ethiopie</td>
  </tr>
  <tr>
    <td><code>ar-DZ</code></td>
    <td>Arabe</td>
    <td>Algérie</td>
  </tr>
  <tr>
    <td><code>ar-BH</code></td>
    <td>Arabe</td>
    <td>Bahreïn</td>
  </tr>
  <tr>
    <td><code>ar-EG</code></td>
    <td>Arabe</td>
    <td>Egypte</td>
  </tr>
  <tr>
    <td><code>ar-IQ</code></td>
    <td>Arabe</td>
    <td>Irak</td>
  </tr>
  <tr>
    <td><code>ar-JO</code></td>
    <td>Arabe</td>
    <td>Jordanie</td>
  </tr>
  <tr>
    <td><code>ar-KW</code></td>
    <td>Arabe</td>
    <td>Koweït</td>
  </tr>
  <tr>
    <td><code>ar-LB</code></td>
    <td>Arabe</td>
    <td>Liban</td>
  </tr>
  <tr>
    <td><code>ar-LY</code></td>
    <td>Arabe</td>
    <td>Libye</td>
  </tr>
  <tr>
    <td><code>ar-MR</code></td>
    <td>Arabe</td>
    <td>Mauritanie</td>
  </tr>
  <tr>
    <td><code>ar-MA</code></td>
    <td>Arabe</td>
    <td>Maroc</td>
  </tr>
  <tr>
    <td><code>ar-OM</code></td>
    <td>Arabe</td>
    <td>Oman</td>
  </tr>
  <tr>
    <td><code>ar-QA</code></td>
    <td>Arabe</td>
    <td>Qatar</td>
  </tr>
  <tr>
    <td><code>ar-SA</code></td>
    <td>Arabe</td>
    <td>Arabie saoudite</td>
  </tr>
  <tr>
    <td><code>ar-SY</code></td>
    <td>Arabe</td>
    <td>Syrie</td>
  </tr>
  <tr>
    <td><code>ar-YE</code></td>
    <td>Arabe</td>
    <td>Tunisie</td>
  </tr>
  <tr>
    <td><code>ar-AE</code></td>
    <td>Arabe</td>
    <td>Emirats arabes unis</td>
  </tr>
  <tr>
    <td><code>ar-YE</code></td>
    <td>Arabe</td>
    <td>Yémen</td>
  </tr>
  <tr>
    <td><code>hy-AM</code></td>
    <td>Arménien</td>
    <td>Arménie</td>
  </tr>
  <tr>
    <td><code>as-IN</code></td>
    <td>Assamais</td>
    <td>Inde</td>
  </tr>
  <tr>
    <td><code>az-AZ</code></td>
    <td>Azéri</td>
    <td>Azerbaïdjan</td>
  </tr>
  <tr>
    <td><code>eu-ES</code></td>
    <td>Basque</td>
    <td>Espagne</td>
  </tr>
  <tr>
    <td><code>be-BY</code></td>
    <td>Biélorusse</td>
    <td>Biélorussie</td>
  </tr>
  <tr>
    <td><code>bn-BD</code></td>
    <td>Bengali</td>
    <td>Bangladesh</td>
  </tr>
  <tr>
    <td><code>be-BY</code></td>
    <td>Biélorusse</td>
    <td>Biélorussie</td>
  </tr>
  <tr>
    <td><code>bn-BD</code></td>
    <td>Bengali</td>
    <td>Bangladesh</td>
  </tr>
  <tr>
    <td><code>bn-IN</code></td>
    <td>Bengali</td>
    <td>Inde</td>
  </tr>
  <tr>
    <td><code>bs-Latn-BA</code></td>
    <td>Bosniaque</td>
    <td>Bosnie</td>
  </tr>
  <tr>
    <td><code>bg-BG</code></td>
    <td>Bulgare</td>
    <td>Bulgarie</td>
  </tr>
  <tr>
    <td><code>my-MM</code></td>
    <td>Birman</td>
    <td>Myanmar</td>
  </tr>
  <tr>
    <td><code>ca-ES</code></td>
    <td>Catalan</td>
    <td>Espagne</td>
  </tr>
  <tr>
    <td><code>zh-Hans-CN</code></td>
    <td>Chinois simplifié</td>
    <td>Chine</td>
  </tr>
  <tr>
    <td><code>zh-Hans-SG</code></td>
    <td>Chinois simplifié</td>
    <td>Singapour</td>
  </tr>
  <tr>
    <td><code>zh-Hant-HK</code></td>
    <td>Chinois traditionnel</td>
    <td>Hong Kong, région administrative spéciale de Chine</td>
  </tr>
  <tr>
    <td><code>zh-Hant-MO</code></td>
    <td>Chinois traditionnel</td>
    <td>Macao</td>
  </tr>
  <tr>
    <td><code>zh-Hant-TW</code></td>
    <td>Chinois traditionnel</td>
    <td>Taïwan</td>
  </tr>
  <tr>
    <td><code>hr-HR</code></td>
    <td>Croate</td>
    <td>Croatie</td>
  </tr>
  <tr>
    <td><code>cs-CZ</code></td>
    <td>Tchèque</td>
    <td>République tchèque</td>
  </tr>
  <tr>
    <td><code>da-DK</code></td>
    <td>Danois</td>
    <td>Danemark</td>
  </tr>
  <tr>
    <td><code>nl-BE</code></td>
    <td>Néerlandais</td>
    <td>Belgique</td>
  </tr>
  <tr>
    <td><code>nl-NL</code></td>
    <td>Néerlandais</td>
    <td>Pays-Bas</td>
  </tr>
  <tr>
    <td><code>en-AU</code></td>
    <td>Anglais</td>
    <td>Australie</td>
  </tr>
  <tr>
    <td><code>eu-BE</code></td>
    <td>Anglais</td>
    <td>Belgique</td>
  </tr>
  <tr>
    <td><code>en-CM</code></td>
    <td>Anglais</td>
    <td>Cameroun</td>
  </tr>
  <tr>
    <td><code>eu-CA</code></td>
    <td>Anglais</td>
    <td>Canada</td>
  </tr>
  <tr>
    <td><code>en-GH</code></td>
    <td>Anglais</td>
    <td>Ghana</td>
  </tr>
  <tr>
    <td><code>eu-HK</code></td>
    <td>Anglais</td>
    <td>Hong Kong, région administrative spéciale de Chine</td>
  </tr>
  <tr>
    <td><code>en-IN</code></td>
    <td>Anglais</td>
    <td>Inde</td>
  </tr>
  <tr>
    <td><code>en-IE</code></td>
    <td>Anglais</td>
    <td>Irlande</td>
  </tr>
  <tr>
    <td><code>en-KE</code></td>
    <td>Anglais</td>
    <td>Kenya</td>
  </tr>
  <tr>
    <td><code>en-MU</code></td>
    <td>Anglais</td>
    <td>Maurice</td>
  </tr>
  <tr>
    <td><code>en-NZ</code></td>
    <td>Anglais</td>
    <td>Nouvelle-Zélande</td>
  </tr>
  <tr>
    <td><code>en-NG</code></td>
    <td>Anglais</td>
    <td>Nigéria</td>
  </tr>
  <tr>
    <td><code>en-PH</code></td>
    <td>Anglais</td>
    <td>Philippines</td>
  </tr>
  <tr>
    <td><code>en-SG</code></td>
    <td>Anglais</td>
    <td>Singapour</td>
  </tr>
  <tr>
    <td><code>en-ZA</code></td>
    <td>Anglais</td>
    <td>Afrique du Sud</td>
  </tr>
  <tr>
    <td><code>en-TZ</code></td>
    <td>Anglais</td>
    <td>Tanzanie</td>
  </tr>
  <tr>
    <td><code>en-GB</code></td>
    <td>Anglais</td>
    <td>Royaume-Uni</td>
  </tr>
  <tr>
    <td><code>en-US</code></td>
    <td>Anglais</td>
    <td>Etats-Unis</td>
  </tr>
  <tr>
    <td><code>en-ZM</code></td>
    <td>Anglais</td>
    <td>Zambie</td>
  </tr>
  <tr>
    <td><code>en</code></td>
    <td>Anglais</td>
    <td> </td>
  </tr>
  <tr>
    <td><code>et-EE</code></td>
    <td>Estonien</td>
    <td>Estonie</td>
  </tr>
  <tr>
    <td><code>fil-PH</code></td>
    <td>Filipino</td>
    <td>Philippines</td>
  </tr>
  <tr>
    <td><code>fi-FI</code></td>
    <td>Finnois</td>
    <td>Finlande</td>
  </tr>
  <tr>
    <td><code>fr-DZ</code></td>
    <td>Français</td>
    <td>Algérie</td>
  </tr>
  <tr>
    <td><code>fr-CM</code></td>
    <td>Français</td>
    <td>Cameroun</td>
  </tr>
  <tr>
    <td><code>fr-CD</code></td>
    <td>Français</td>
    <td>République démocratique du Congo</td>
  </tr>
  <tr>
    <td><code>fr-BE</code></td>
    <td>Français</td>
    <td>Belgique</td>
  </tr>
  <tr>
    <td><code>fr-CA</code></td>
    <td>Français</td>
    <td>Canada</td>
  </tr>
  <tr>
    <td><code>fr-FR</code></td>
    <td>Français</td>
    <td>France</td>
  </tr>
  <tr>
    <td><code>fr-CI</code></td>
    <td>Français</td>
    <td>Côte d'ivoire</td>
  </tr>
  <tr>
    <td><code>fr-LU</code></td>
    <td>Français</td>
    <td>Luxembourg</td>
  </tr>
  <tr>
    <td><code>fr-MR</code></td>
    <td>Français</td>
    <td>Mauritanie</td>
  </tr>
  <tr>
    <td><code>fr-MU</code></td>
    <td>Français</td>
    <td>Maurice</td>
  </tr>
  <tr>
    <td><code>fr-MA</code></td>
    <td>Français</td>
    <td>Maroc</td>
  </tr>
  <tr>
    <td><code>fr-SN</code></td>
    <td>Français</td>
    <td>Sénégal</td>
  </tr>
  <tr>
    <td><code>fr-CH</code></td>
    <td>Français</td>
    <td>Suisse</td>
  </tr>
  <tr>
    <td><code>fr-TN</code></td>
    <td>Français</td>
    <td>Tunisie</td>
  </tr>
  <tr>
    <td><code>gl-ES</code></td>
    <td>Galicien</td>
    <td>Espagne</td>
  </tr>
  <tr>
    <td><code>lg-UG</code></td>
    <td>Ganda</td>
    <td>Ouganda</td>
  </tr>
  <tr>
    <td><code>ka-GE</code></td>
    <td>Géorgien</td>
    <td>Géorgie</td>
  </tr>
  <tr>
    <td><code>de-AT</code></td>
    <td>Allemand</td>
    <td>Autriche</td>
  </tr>
  <tr>
    <td><code>de-DE</code></td>
    <td>Allemand</td>
    <td>Allemagne</td>
  </tr>
  <tr>
    <td><code>de-LU</code></td>
    <td>Allemand</td>
    <td>Luxembourg</td>
  </tr>
  <tr>
    <td><code>de-CH</code></td>
    <td>Allemand</td>
    <td>Suisse</td>
  </tr>
  <tr>
    <td><code>el-GR</code></td>
    <td>Grec</td>
    <td>Grèce</td>
  </tr>
  <tr>
    <td><code>gu-IN</code></td>
    <td>Goudjarâtî</td>
    <td>Inde</td>
  </tr>
  <tr>
    <td><code>ha-NG</code></td>
    <td>Haoussa</td>
    <td>Nigéria</td>
  </tr>
  <tr>
    <td><code>he-IL</code></td>
    <td>Hébreu</td>
    <td>Israël</td>
  </tr>
  <tr>
    <td><code>hi-IN</code></td>
    <td>Hindi</td>
    <td>Inde</td>
  </tr>
  <tr>
    <td><code>hu-HU</code></td>
    <td>Hongrois</td>
    <td>Hongrie</td>
  </tr>
  <tr>
    <td><code>is-IS</code></td>
    <td>Islandais</td>
    <td>Islande</td>
  </tr>
  <tr>
    <td><code>ig-NG</code></td>
    <td>Igbo</td>
    <td>Nigéria</td>
  </tr>
  <tr>
    <td><code>id-ID</code></td>
    <td>Indonésien</td>
    <td>Indonésie</td>
  </tr>
  <tr>
    <td><code>it-IT</code></td>
    <td>Italien</td>
    <td>Italie</td>
  </tr>
  <tr>
    <td><code>it-CH</code></td>
    <td>Italien</td>
    <td>Suisse</td>
  </tr>
  <tr>
    <td><code>ja-JP</code></td>
    <td>Japonais</td>
    <td>Japon</td>
  </tr>
  <tr>
    <td><code>kn-IN</code></td>
    <td>Kannada</td>
    <td>Inde</td>
  </tr>
  <tr>
    <td><code>kk-KZ</code></td>
    <td>Kazakh</td>
    <td>Kazakhstan</td>
  </tr>
  <tr>
    <td><code>km-KH</code></td>
    <td>Khmer</td>
    <td>Cambodge</td>
  </tr>
  <tr>
    <td><code>rw-RW</code></td>
    <td>Kinyarwanda</td>
    <td>Rwanda</td>
  </tr>
  <tr>
    <td><code>kok-IN</code></td>
    <td>Konkani</td>
    <td>Inde</td>
  </tr>
  <tr>
    <td><code>ko-KR</code></td>
    <td>Coréen</td>
    <td>Corée du Sud</td>
  </tr>
  <tr>
    <td><code>lo-LA</code></td>
    <td>Lituanien</td>
    <td>Lituanie</td>
  </tr>
  <tr>
    <td><code>lv-LV</code></td>
    <td>Letton</td>
    <td>Lettonie</td>
  </tr>
  <tr>
    <td><code>lt-LT</code></td>
    <td>Khmer</td>
    <td>Cambodge</td>
  </tr>
  <tr>
    <td><code>mk-MK</code></td>
    <td>Macédonien</td>
    <td>Macédoine</td>
  </tr>
  <tr>
    <td><code>ms-Latn-MY</code></td>
    <td>Malais (latin)</td>
    <td>Malaisie</td>
  </tr>
  <tr>
    <td><code>ml-IN</code></td>
    <td>Malayalam</td>
    <td>Inde</td>
  </tr>
  <tr>
    <td><code>mt-MT</code></td>
    <td>Maltais</td>
    <td>Malte</td>
  </tr>
  <tr>
    <td><code>mr-IN</code></td>
    <td>Marathe</td>
    <td>Inde</td>
  </tr>
  <tr>
    <td><code>mn-Cyrl-MN</code></td>
    <td>Mongol (cyrillique)</td>
    <td>Mongolie</td>
  </tr>
  <tr>
    <td><code>ne-IN</code></td>
    <td>Népalais</td>
    <td>Inde</td>
  </tr>
  <tr>
    <td><code>ne-NP</code></td>
    <td>Népalais</td>
    <td>Népal</td>
  </tr>
  <tr>
    <td><code>nb-NO</code></td>
    <td>Norvégien bokmål</td>
    <td>Norvège</td>
  </tr>
  <tr>
    <td><code>nn-NO</code></td>
    <td>Norvégien nynorsk</td>
    <td>Norvège</td>
  </tr>
  <tr>
    <td><code>or-IN</code></td>
    <td>Oriya (Odia)</td>
    <td>Inde</td>
  </tr>
  <tr>
    <td><code>om-ET</code></td>
    <td>Oromo</td>
    <td>Ethiopie</td>
  </tr>
  <tr>
    <td><code>pl-PL</code></td>
    <td>Polonais</td>
    <td>Pologne</td>
  </tr>
  <tr>
    <td><code>pt-AO</code></td>
    <td>Portugais</td>
    <td>Angola</td>
  </tr>
  <tr>
    <td><code>pt-BR</code></td>
    <td>Portugais</td>
    <td>Brésil</td>
  </tr>
  <tr>
    <td><code>pt-MO</code></td>
    <td>Portugais</td>
    <td>Macao</td>
  </tr>
  <tr>
    <td><code>pt-MZ</code></td>
    <td>Portugais</td>
    <td>Mozambique</td>
  </tr>
  <tr>
    <td><code>pt-PT</code></td>
    <td>Portugais</td>
    <td>Portugal</td>
  </tr>
  <tr>
    <td><code>pa-IN</code></td>
    <td>Pendjabi</td>
    <td>Inde</td>
  </tr>
  <tr>
    <td><code>ro-RO</code></td>
    <td>Roumain</td>
    <td>Roumanie</td>
  </tr>
  <tr>
    <td><code>ru-RU</code></td>
    <td>Russe</td>
    <td>Russe</td>
  </tr>
  <tr>
    <td><code>sr-Cyrl-RS</code></td>
    <td>Serbe (cyrillique)</td>
    <td>Serbie</td>
  </tr>
  <tr>
    <td><code>sr-Latn-ME</code></td>
    <td>Serbe (latin)</td>
    <td>Monténégro</td>
  </tr>
  <tr>
    <td><code>sr-Latn-RS</code></td>
    <td>Serbe (latin)</td>
    <td>Serbie</td>
  </tr>
  <tr>
    <td><code>si-LK</code></td>
    <td>Cinghalais</td>
    <td>Sri Lanka</td>
  </tr>
  <tr>
    <td><code>sk-SK</code></td>
    <td>Slovaque</td>
    <td>Slovaquie</td>
  </tr>
  <tr>
    <td><code>sl-SI</code></td>
    <td>Slovène</td>
    <td>Slovénie</td>
  </tr>
  <tr>
    <td><code>es-AR</code></td>
    <td>Espagnol</td>
    <td>Argentine</td>
  </tr>
  <tr>
    <td><code>es-BO</code></td>
    <td>Espagnol</td>
    <td>Bolivie</td>
  </tr>
  <tr>
    <td><code>es-CL</code></td>
    <td>Espagnol</td>
    <td>Chili</td>
  </tr>
  <tr>
    <td><code>es-CO</code></td>
    <td>Espagnol</td>
    <td>Colombie</td>
  </tr>
  <tr>
    <td><code>es-CR</code></td>
    <td>Espagnol</td>
    <td>Costa Rica</td>
  </tr>
  <tr>
    <td><code>es-DO</code></td>
    <td>Espagnol</td>
    <td>République dominicaine</td>
  </tr>
  <tr>
    <td><code>es-EC</code></td>
    <td>Espagnol</td>
    <td>Equateur</td>
  </tr>
  <tr>
    <td><code>es-SV</code></td>
    <td>Espagnol</td>
    <td>El Salvador</td>
  </tr>
  <tr>
    <td><code>es-GT</code></td>
    <td>Espagnol</td>
    <td>Guatemala</td>
  </tr>
  <tr>
    <td><code>es-HN</code></td>
    <td>Espagnol</td>
    <td>Honduras</td>
  </tr>
  <tr>
    <td><code>es-MX</code></td>
    <td>Espagnol</td>
    <td>Mexique</td>
  </tr>
  <tr>
    <td><code>es-NI</code></td>
    <td>Espagnol</td>
    <td>Nicaragua</td>
  </tr>
  <tr>
    <td><code>es-PA</code></td>
    <td>Espagnol</td>
    <td>Panama</td>
  </tr>
  <tr>
    <td><code>es-PY</code></td>
    <td>Espagnol</td>
    <td>Paraguay</td>
  </tr>
  <tr>
    <td><code>es-PE</code></td>
    <td>Espagnol</td>
    <td>Pérou</td>
  </tr>
  <tr>
    <td><code>es-PR</code></td>
    <td>Espagnol</td>
    <td>Porto Rico</td>
  </tr>
  <tr>
    <td><code>es-ES</code></td>
    <td>Espagnol</td>
    <td>Espagne</td>
  </tr>
  <tr>
    <td><code>es-US</code></td>
    <td>Espagnol</td>
    <td>Etats-Unis</td>
  </tr>
  <tr>
    <td><code>es-UY</code></td>
    <td>Espagnol</td>
    <td>Uruguay</td>
  </tr>
  <tr>
    <td><code>es-VE</code></td>
    <td>Espagnol</td>
    <td>Venezuela</td>
  </tr>
  <tr>
    <td><code>sw-KE</code></td>
    <td>Swahili</td>
    <td>Kenya</td>
  </tr>
  <tr>
    <td><code>sw-TZ</code></td>
    <td>Swahili</td>
    <td>Tanzanie</td>
  </tr>
  <tr>
    <td><code>sv-SE</code></td>
    <td>Suédois</td>
    <td>Suède</td>
  </tr>
  <tr>
    <td><code>ta-IN</code></td>
    <td>Tamoul</td>
    <td>Inde</td>
  </tr>
  <tr>
    <td><code>te-IN</code></td>
    <td>Télougou</td>
    <td>Inde</td>
  </tr>
  <tr>
    <td><code>th-TH</code></td>
    <td>Thaï</td>
    <td>Thaïlande</td>
  </tr>
  <tr>
    <td><code>tr-TR</code></td>
    <td>Turc</td>
    <td>Turquie</td>
  </tr>
  <tr>
    <td><code>uk-UA</code></td>
    <td>Ukrainien</td>
    <td>Ukraine</td>
  </tr>
  <tr>
    <td><code>ur-IN</code></td>
    <td>Ourdou</td>
    <td>Inde</td>
  </tr>
  <tr>
    <td><code>ur-PK</code></td>
    <td>Ourdou</td>
    <td>Pakistan</td>
  </tr>
  <tr>
    <td><code>uz-Cyrl-UZ</code></td>
    <td>Ouzbek (cyrillique)</td>
    <td>Ouzbékistan</td>
  </tr>
  <tr>
    <td><code>uz-Latn-UZ</code></td>
    <td>Ouzbek (latin)</td>
    <td>Ouzbékistan</td>
  </tr>
  <tr>
    <td><code>vi-VN</code></td>
    <td>Vietnamien</td>
    <td>Vietnam</td>
  </tr>
  <tr>
    <td><code>cy-GB</code></td>
    <td>Gallois</td>
    <td>Royaume-Uni</td>
  </tr>
  <tr>
    <td><code>yo-NG</code></td>
    <td>Yoruba</td>
    <td>Nigéria</td>
  </tr>
  <tr>
    <td><code>zu-ZA</code></td>
    <td>Zoulou</td>
    <td>Afrique du Sud</td>
  </tr>
</table>
