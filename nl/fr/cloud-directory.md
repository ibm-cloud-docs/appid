---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Configuration du répertoire cloud
{: #cd}

Les utilisateurs peuvent s'inscrire et se connecter à vos applications mobiles et Web à l'aide d'un e-mail et d'un mot de passe. Un répertoire cloud est un registre d'utilisateurs géré dans le cloud. Lorsqu'un utilisateur s'inscrit à votre application avec un e-mail et un mot de passe, il est ajouté à votre répertoire d'utilisateurs. Avec cette fonction, l'utilisateur final a la liberté de gérer son propre compte au sein de votre application.
{: shortdesc}

</br>

## Gestion des paramètres de répertoire
{: #cd-settings}

Vous pouvez configurer les notifications et le niveau de contrôle de votre application par les utilisateurs. La configuration de votre répertoire cloud peut s'effectuer rapidement, comme illustré dans l'image suivante. Ces paramètres peuvent être mis à jour à tout moment à partir du tableau de bord du service.
{: shortdesc}

![Configuration du répertoire cloud](/images/cloud-directory.png)

1. Assurez-vous que le répertoire cloud est activé en tant que fournisseur d'identité et définissez **Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe** sur **On**. Si cette option est définie sur **Off**, vous pouvez toujours ajouter des utilisateurs via la console à des fins de développement.
2. Configurez les détails de l'expéditeur. Spécifiez l'adresse e-mail à partir de laquelle vos messages seront envoyés, quel nom d'expéditeur apparaîtra et à qui les utilisateurs pourront répondre.
  Lorsque vous configurez votre URL d'action, veillez à accorder à l'utilisateur un temps suffisant pour cliquer sur le lien. Pour bénéficier de certaines options, telles que la possibilité de demander une réinitialisation de son mot de passe, l'utilisateur doit confirmer la validité (l'existence) de son adresse e-mail.
  {: tip}
3. Déterminez les types d'e-mails reçus par l'utilisateur et les informations sur l'expéditeur.
4. Avec les modèles fournis, personnalisez vos messages avec votre marque ou des contenus personnalisés. Pour plus d'informations, voir [Gestion des messages](/docs/services/appid/cloud-directory.html#cd-messages).
5. Vérifiez dans l'onglet **Utilisateurs** de l'interface graphique qui s'est inscrit à votre application.

</br>

## Gestion des messages
{: #cd-messages}

Un modèle est un exemple d'e-mail que vous pouvez envoyer à vos utilisateurs. Vous pouvez personnaliser le modèle en modifiant le contenu et la présentation du message. Chaque type de message peut être **activé** ou **désactivé** dans l'onglet Paramètres de répertoire.
{: shortdesc}

1. Sélectionnez un **Type de message**.
2. Personnalisez votre message en changeant sa conception et son contenu. Vous pouvez utiliser des paramètres à cet effet. N'oubliez pas de sauvegarder vos changements !

### Types de messages

Vous pouvez envoyer plusieurs types de message à vos utilisateurs. Vous pouvez envoyer l'exemple de message programmé dans l'interface utilisateur ou personnaliser le contenu du message pour une expérience d'application plus personnelle.

<dl>
  <dt>Bienvenue</dt>
    <dd><p>Une fois qu'un utilisateur est enregistré, vous pouvez lui adresse un e-mail de bienvenue dans votre application. Réservez le meilleur accueil à vos utilisateurs. Pour les fidéliser, choisissez un message aussi engageant que possible.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> Paramètres pour tous les messages </th>
      </thead>
      <tbody>
        <tr>
          <td> %{display.logo} </td>
          <td> Affiche l'image que vous avez configurée pour votre widget de connexion. </td>
        </tr>
        <tr>
          <td> %{user.displayName} </td>
          <td> Affiche le pseudonyme (appelé nom d'écran dans l'interface) que l'utilisateur choisit d'utiliser lorsqu'il interagit avec l'application. </td>
        </tr>
        <tr>
          <td> %{user.email} </td>
          <td> Affiche l'adresse e-mail avec laquelle l'utilisateur s'est inscrit. </td>
        </tr>
        <tr>
          <td> %{user.firstName} </td>
          <td> Affiche le prénom spécifié par l'utilisateur. </td>
        </tr>
        <tr>
          <td> %{user.formattedName} </td>
          <td> Affiche le nom complet de l'utilisateur. </td>
        </tr>
        <tr>
          <td> %{user.lastName} </td>
          <td> Affiche le nom de famille spécifié par l'utilisateur. </td>
        </tr>
      </tbody>
    </table>
    <p>**Remarque **: un blanc apparaîtra à la place d'un paramètre si l'utilisateur n'a pas fourni l'information correspondante.</p></dd>
  <dt>Mot de passe oublié</dt>
    <dd><p>Un utilisateur peut demander à faire réinitialiser son mot de passe s'il l'a oublié ou s'il doit en changer pour une raison quelconque. Vous pouvez personnaliser l'e-mail de réponse à cette demande. Le mot de passe restera inchangé tant que l'utilisateur n'aura pas cliqué sur le lien figurant dans cet e-mail de réponse.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> Paramètres de changement de mot de passe </th>
      </thead>
      <tbody>
        <tr>
          <td> %{linkExpiration.hours} </td>
          <td> Affiche le nombre d'heures de validité du lien. </td>
        </tr>
        <tr>
          <td> %{linkExpiration.minutes} </td>
          <td> Affiche le nombre de minutes de validité du lien. </td>
        </tr>
        <tr>
          <td> %{resetPassword.code} </td>
          <td> Affiche un code d'accès à usage unique incorporé dans l'URL. Chaque personne recevra donc un code différent. Exemple : <code>https://appid-wfm.bluemix.net/verify/6574839563478 </code> </td>
        </tr>
        <tr>
          <td> %{resetPassword.link} </td>
          <td> Affiche le lien sur lequel l'utilisateur doit cliquer pour réinitialiser son mot de passe. </td>
        </tr>
       </tbody>
    </table>
    </dd>
  <dt>Vérification</dt>
    <dd><p>Vous pouvez demander que l'utilisateur confirme l'existence de son compte mail en lui envoyant un e-mail à cet effet. Vous limiterez ainsi le nombre de faux comptes (notamment les robots) qui peuvent s'inscrire à votre application. Vous pouvez restreindre l'accès à votre application tant que l'utilisateur n'a pas prouvé la validité de son adresse e-mail.
Utilisable aussi comme moyen de gérer pour quels utilisateurs vous créez des profils.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> Paramètres du message de vérification </th>
      </thead>
      <tbody>
        <tr>
          <td> %{linkExpiration.hours} </td>
          <td> Affiche le nombre d'heures de validité du lien. </td>
        </tr>
        <tr>
          <td> %{linkExpiration.minutes} </td>
          <td> Affiche le nombre de minutes de validité du lien. </td>
        </tr>
        <tr>
          <td> %{verify.code} </td>
          <td> Affiche une URL de vérification à usage unique. </td>
        </tr>
        <tr>
          <td> %{verify.link} </td>
          <td> Affiche l'URL d'action que vous avez spécifiée dans les paramètres. </td>
        </tr>
      </tbody>
    </table>
    </dd>
  <dt>Changement du mot de passe</dt>
    <dd><p>Vous pouvez faire savoir à l'utilisateur que son mot de passe a changé. Cette option est particulièrement utile s'il n'en a pas fait la demande. Il peut alors prendre les mesures appropriées pour sécuriser à nouveau son compte.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> Paramètres de changement de mot de passe </th>
      </thead>
      <tbody>
        <tr>
          <td> %{passwordChangeInfo.time} </td>
          <td> Affiche l'heure à laquelle un nouveau mot de passe est entré en vigueur. </td>
        </tr>
        <tr>
          <td> %{passwordChangeInfo.ipAddress} </td>
          <td> Affiche l'adresse IP d'où provient la demande de changement de mot de passe. </td>
        </tr>
      </tbody>
    </table>
    </dd>
</dl>
</br>
**REMARQUE** : {{site.data.keyword.appid_short_notm}} utilise <a href="https://www.sendgrid.com" target="_blank">SendGrid <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> comme service de distribution de courrier. Tous les courriers électroniques sont envoyés à l'aide d'un seul compte SendGrid.

</br>
## Etapes suivantes
Maintenant que vous avez configuré le répertoire cloud, vous êtes prêt à ajouter le code du widget de connexion à votre code d'application. Cliquez sur une icône de langage SDK dans l'image suivante pour voir ce que vous devez faire.
{: shortdesc}

<img usemap="#options-map" border="0" class="image" id="options" src="images/options.png" width="750" alt="Cliquez sur une icône de langage SDK pour débuter avec le répertoire cloud dans vos applications." style="width:750px;" />
<map name="options-map" id="options-map">
<area href="login-widget.html#branded-ui-android" alt="Gestion de l'expérience de connexion avec le SDK Android" shape="rect" coords="187, 6, 305, 120" />
<area href="login-widget.html#branded-ui-ios-swift" alt="Gestion de l'expérience de connexion avec le SDK Swift iOS." shape="rect" coords="333, 6, 448, 125" />
<area href="login-widget.html#branded-ui-nodejs" alt="Gestion de l'expérience de connexion avec le SDK Node.js." shape="rect" coords="472, 7, 590, 121" />
</map>
