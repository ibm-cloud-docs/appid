---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-09"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Configuration du répertoire cloud
{: #cd}

Les utilisateurs peuvent s'inscrire et se connecter à vos applications mobiles et Web à l'aide d'une adresse électronique ou d'un nom d'utilisateur et d'un mot de passe. Un répertoire cloud est un registre d'utilisateurs géré dans le cloud. Lorsqu'un utilisateur s'inscrit à votre application, il est ajouté à votre répertoire d'utilisateurs. Avec cette fonction, l'utilisateur final a la liberté de gérer son propre compte au sein de votre application.
{: shortdesc}

</br>

## Gestion des paramètres de répertoire
{: #cd-settings}

Vous pouvez configurer les notifications et le niveau de contrôle de votre application par les utilisateurs. La configuration de votre répertoire cloud peut s'effectuer rapidement, comme illustré dans l'image ci-dessous. Ces paramètres peuvent être mis à jour à tout moment à partir du tableau de bord du service.
{: shortdesc}


![Configuration du répertoire cloud](/images/cloud-directory.png)
Figure. Procédure de configuration du répertoire cloud 


1. Assurez-vous que le répertoire cloud est activé en tant que fournisseur d'identité et activez **Autoriser les utilisateurs à s'inscrire et à réinitialiser leur mot de passe**. Si cette option est **désactivée**, vous pouvez tout de même ajouter des utilisateurs via la console à des fins de développement.
2. Indiquez si les utilisateurs doivent s'authentifier avec un nom d'utilisateur spécifié ou une adresse électronique. Cette zone est utilisée pour les flux d'inscription, de connexion et d'oubli de mot de passe. Si vous autorisez les utilisateurs à s'inscrire avec un nom d'utilisateur et un mot de passe, le nom d'utilisateur doit comporter au moins 8 caractères et ne peut pas contenir d'espace, de virgule ni de barre oblique. **Remarque :** vous pouvez passer d'une option à une autre uniquement si votre répertoire cloud ne comporte aucun utilisateur. 
3. Configurez les détails de l'expéditeur. Spécifiez l'adresse électronique à partir de laquelle vos messages seront envoyés, quel nom d'expéditeur apparaîtra et à qui les utilisateurs pourront répondre.
  Lorsque vous configurez votre URL d'action, veillez à accorder à l'utilisateur un temps suffisant pour cliquer sur le lien. Pour bénéficier de certaines options, telles que la possibilité de demander une réinitialisation de son mot de passe, l'utilisateur doit confirmer la validité (l'existence) de son adresse électronique.
  {: tip}
4. Déterminez les types de courriers électroniques reçus par l'utilisateur et
les informations
sur l'expéditeur.
5. Avec les modèles fournis, personnalisez vos messages avec votre marque ou des contenus personnalisés. Pour plus d'informations, voir [Gestion des messages](/docs/services/appid/cloud-directory.html#cd-messages).
6. Vérifiez dans l'onglet **Utilisateurs** de l'interface graphique qui s'est inscrit à votre application.

Un utilisateur unique peut s'inscrire jusqu'à 5 fois par minute. S'il tente de s'inscrire une sixième fois, une erreur s'affiche.
{: tip}

</br>

## Gestion des messages
{: #cd-messages}

Un modèle est un exemple de courrier électronique que vous pouvez envoyer à vos utilisateurs. Vous pouvez personnaliser le modèle en modifiant le contenu et la présentation du message.
{: shortdesc}

1. Dans l'onglet **Fournisseurs d'identité > Répertoire cloud > Paramètres** du tableau de bord, **activez** les messages que vous voulez envoyer. 

2. Facultatif : utilisez <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/updateLocalization" target="_blank">les API de gestion des langues <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> pour définir une autre langue à utiliser dans vos modèles de message. Pour la liste des codes de langue pris en charge, voir [Langues prises en charge](#languages). 

3. Sélectionnez un type de message dans **Type de message**.

4. Personnalisez votre message en changeant sa conception et son contenu. Vous pouvez utiliser des paramètres à cet effet. N'oubliez pas de sauvegarder vos changements !

### Types de messages

Vous pouvez envoyer plusieurs types de message à vos utilisateurs. Vous pouvez envoyer l'exemple de message programmé dans l'interface utilisateur ou personnaliser le contenu du message pour une expérience d'application plus personnelle.

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
    </table>
    <p>**Remarque **: un blanc apparaît à la place d'un paramètre si l'utilisateur n'a pas fourni l'information correspondante.</p></dd>
  <dt>Mot de passe oublié</dt>
    <dd><p>Un utilisateur peut demander à réinitialiser son mot de passe s'il l'a oublié ou s'il doit en changer pour une raison quelconque. Vous pouvez personnaliser le courrier électronique de réponse à cette demande. Le mot de passe restera inchangé tant que l'utilisateur n'aura pas cliqué sur le lien figurant dans ce courrier électronique de réponse.</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="Icône Plus d'informations"/> Paramètres de changement de mot de passe </th>
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
          <td><code>%{resetPassword.code}</code></td>
          <td> Affiche un code d'accès à usage unique incorporé dans l'URL. Chaque personne recevra donc un code différent. Exemple : <code>https://appid-wfm.bluemix.net/verify/6574839563478 </code> </td>
        </tr>
        <tr>
          <td><code>%{resetPassword.link}</code></td>
          <td> Affiche le lien sur lequel l'utilisateur doit cliquer pour réinitialiser son mot de passe. </td>
        </tr>
       </tbody>
    </table>
    </dd>
  <dt>Vérification</dt>
    <dd><p>Vous pouvez demander que l'utilisateur confirme l'existence de son compte mail en lui envoyant un courrier électronique à cet effet. Vous limiterez ainsi le nombre de faux comptes (notamment les robots) qui peuvent s'inscrire à votre application. Vous pouvez restreindre l'accès à votre application tant que l'utilisateur n'a pas prouvé la validité de son adresse électronique.
Utilisable aussi comme moyen de gérer pour quels utilisateurs vous créez des profils.</p>
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
    </table>
    </dd>
  <dt>Changement du mot de passe</dt>
    <dd><p>Vous pouvez faire savoir à l'utilisateur que son mot de passe a changé. Cette option est particulièrement utile s'il n'en a pas fait la demande. Il peut alors effectuer les étapes appropriées pour resécuriser son compte. </p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="Icône Plus d'informations"/> Paramètres de changement de mot de passe </th>
      </thead>
      <tbody>
        <tr>
          <td><code>%{passwordChangeInfo.time}</code></td>
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

## Gestion de la force du mot de passe 
{: #strength}

Vous pouvez définir les exigences relatives aux mots de passe pouvant être utilisés avec le répertoire cloud.
{: shortdesc}

Si le mot de passe est fiable, il est difficile, voire impossible, de le deviner manuellement ou à l'aide d'un programme. La force du mot de passe est définie en tant qu'expression régulière. 

Voici quelques exemples de force communs pour le mot de passe : 

- Il doit comporter au moins 8 caractères. Exemple d'expression régulière : `^.{8,}$`
- Il doit comporter 1 chiffre, 1 lettre minuscule et 1 lettre majuscule. Exemple d'expression régulière : `^(?:(?=.*\\d)(?=.*[a-z])(?=.*[A-Z]).*)$`
- Il ne doit comporter que des chiffres et des lettres en anglais. Exemple d'expression régulière : `^[A-Za-z0-9]*$`
- Il doit comporter au moins 1 caractère unique. Exemple d'expression régulière : `^(\w)\w*?(?!\1)\w+$`

Vous devez utiliser <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/set_cloud_directory_password_regex" target="_blank">les API de gestion <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> pour définir les exigences. 

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
    <td>Afrique du Sud </td>
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
    <td>Espagne </td>
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
    <td>Espagne </td>
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
    <td>Hong Kong, région administrative spéciale de Chine </td>
  </tr>
  <tr>
    <td><code>zh-Hant-MO</code></td>
    <td>Chinois traditionnel</td>
    <td>Macao</td>
  </tr>
  <tr>
    <td><code>zh-Hant-TW</code></td>
    <td>Chinois traditionnel</td>
    <td>Taïwan </td>
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
    <td>Hong Kong, région administrative spéciale de Chine </td>
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
    <td>Afrique du Sud </td>
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
    <td>Français </td>
    <td>Algérie</td>
  </tr>
  <tr>
    <td><code>fr-CM</code></td>
    <td>Français </td>
    <td>Cameroun</td>
  </tr>
  <tr>
    <td><code>fr-CD</code></td>
    <td>Français </td>
    <td>République démocratique du Congo</td>
  </tr>
  <tr>
    <td><code>fr-BE</code></td>
    <td>Français </td>
    <td>Belgique</td>
  </tr>
  <tr>
    <td><code>fr-CA</code></td>
    <td>Français </td>
    <td>Canada</td>
  </tr>
  <tr>
    <td><code>fr-FR</code></td>
    <td>Français </td>
    <td>France</td>
  </tr>
  <tr>
    <td><code>fr-CI</code></td>
    <td>Français </td>
    <td>Côte d'ivoire </td>
  </tr>
  <tr>
    <td><code>fr-LU</code></td>
    <td>Français </td>
    <td>Luxembourg</td>
  </tr>
  <tr>
    <td><code>fr-MR</code></td>
    <td>Français </td>
    <td>Mauritanie</td>
  </tr>
  <tr>
    <td><code>fr-MU</code></td>
    <td>Français </td>
    <td>Maurice</td>
  </tr>
  <tr>
    <td><code>fr-MA</code></td>
    <td>Français </td>
    <td>Maroc </td>
  </tr>
  <tr>
    <td><code>fr-SN</code></td>
    <td>Français </td>
    <td>Sénégal</td>
  </tr>
  <tr>
    <td><code>fr-CH</code></td>
    <td>Français </td>
    <td>Suisse</td>
  </tr>
  <tr>
    <td><code>fr-TN</code></td>
    <td>Français </td>
    <td>Tunisie</td>
  </tr>
  <tr>
    <td><code>gl-ES</code></td>
    <td>Galicien</td>
    <td>Espagne </td>
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
    <td>Autriche </td>
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
    <td>Indonésie </td>
  </tr>
  <tr>
    <td><code>it-IT</code></td>
    <td>Italien</td>
    <td>Italie </td>
  </tr>
  <tr>
    <td><code>it-CH</code></td>
    <td>Italien</td>
    <td>Suisse</td>
  </tr>
  <tr>
    <td><code>ja-JP</code></td>
    <td>Japonais </td>
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
    <td>Coréen </td>
    <td>Corée du Sud</td>
  </tr>
  <tr>
    <td><code>lo-LA</code></td>
    <td>Lituanien</td>
    <td>Lituanie</td>
  </tr>
  <tr>
    <td><code>lv-LV</code></td>
    <td>Letton </td>
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
    <td>Malais (latin) </td>
    <td>Malaisie </td>
  </tr>
  <tr>
    <td><code>ml-IN</code></td>
    <td>Malayalam</td>
    <td>Inde</td>
  </tr>
  <tr>
    <td><code>mt-MT</code></td>
    <td>Maltais</td>
    <td>Malte </td>
  </tr>
  <tr>
    <td><code>mr-IN</code></td>
    <td>Marathe</td>
    <td>Inde</td>
  </tr>
  <tr>
    <td><code>mn-Cyrl-MN</code></td>
    <td>Mongol (cyrillique) </td>
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
    <td>Norvège </td>
  </tr>
  <tr>
    <td><code>nn-NO</code></td>
    <td>Norvégien nynorsk</td>
    <td>Norvège </td>
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
    <td>Polonais </td>
    <td>Pologne</td>
  </tr>
  <tr>
    <td><code>pt-AO</code></td>
    <td>Portugais </td>
    <td>Angola</td>
  </tr>
  <tr>
    <td><code>pt-BR</code></td>
    <td>Portugais </td>
    <td>Brésil</td>
  </tr>
  <tr>
    <td><code>pt-MO</code></td>
    <td>Portugais </td>
    <td>Macao</td>
  </tr>
  <tr>
    <td><code>pt-MZ</code></td>
    <td>Portugais </td>
    <td>Mozambique</td>
  </tr>
  <tr>
    <td><code>pt-PT</code></td>
    <td>Portugais </td>
    <td>Portugal</td>
  </tr>
  <tr>
    <td><code>pa-IN</code></td>
    <td>Pendjabi </td>
    <td>Inde</td>
  </tr>
  <tr>
    <td><code>ro-RO</code></td>
    <td>Roumain</td>
    <td>Roumanie</td>
  </tr>
  <tr>
    <td><code>ru-RU</code></td>
    <td>Russe </td>
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
    <td>Slovaque </td>
    <td>Slovaquie</td>
  </tr>
  <tr>
    <td><code>sl-SI</code></td>
    <td>Slovène </td>
    <td>Slovénie </td>
  </tr>
  <tr>
    <td><code>es-AR</code></td>
    <td>Espagnol </td>
    <td>Argentine</td>
  </tr>
  <tr>
    <td><code>es-BO</code></td>
    <td>Espagnol </td>
    <td>Bolivie</td>
  </tr>
  <tr>
    <td><code>es-CL</code></td>
    <td>Espagnol </td>
    <td>Chili </td>
  </tr>
  <tr>
    <td><code>es-CO</code></td>
    <td>Espagnol </td>
    <td>Colombie</td>
  </tr>
  <tr>
    <td><code>es-CR</code></td>
    <td>Espagnol </td>
    <td>Costa Rica</td>
  </tr>
  <tr>
    <td><code>es-DO</code></td>
    <td>Espagnol </td>
    <td>République dominicaine</td>
  </tr>
  <tr>
    <td><code>es-EC</code></td>
    <td>Espagnol </td>
    <td>Equateur</td>
  </tr>
  <tr>
    <td><code>es-SV</code></td>
    <td>Espagnol </td>
    <td>El Salvador</td>
  </tr>
  <tr>
    <td><code>es-GT</code></td>
    <td>Espagnol </td>
    <td>Guatemala</td>
  </tr>
  <tr>
    <td><code>es-HN</code></td>
    <td>Espagnol </td>
    <td>Honduras</td>
  </tr>
  <tr>
    <td><code>es-MX</code></td>
    <td>Espagnol </td>
    <td>Mexique</td>
  </tr>
  <tr>
    <td><code>es-NI</code></td>
    <td>Espagnol </td>
    <td>Nicaragua</td>
  </tr>
  <tr>
    <td><code>es-PA</code></td>
    <td>Espagnol </td>
    <td>Panama</td>
  </tr>
  <tr>
    <td><code>es-PY</code></td>
    <td>Espagnol </td>
    <td>Paraguay</td>
  </tr>
  <tr>
    <td><code>es-PE</code></td>
    <td>Espagnol </td>
    <td>Pérou</td>
  </tr>
  <tr>
    <td><code>es-PR</code></td>
    <td>Espagnol </td>
    <td>Porto Rico</td>
  </tr>
  <tr>
    <td><code>es-ES</code></td>
    <td>Espagnol </td>
    <td>Espagne </td>
  </tr>
  <tr>
    <td><code>es-US</code></td>
    <td>Espagnol </td>
    <td>Etats-Unis</td>
  </tr>
  <tr>
    <td><code>es-UY</code></td>
    <td>Espagnol </td>
    <td>Uruguay</td>
  </tr>
  <tr>
    <td><code>es-VE</code></td>
    <td>Espagnol </td>
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
    <td>Suédois </td>
    <td>Suède </td>
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
    <td>Turc </td>
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
    <td>Inde </td>
  </tr>
  <tr>
    <td><code>ur-PK</code></td>
    <td>Ourdou</td>
    <td>Pakistan</td>
  </tr>
  <tr>
    <td><code>uz-Cyrl-UZ</code></td>
    <td>Ouzbek (cyrillique) </td>
    <td>Ouzbékistan </td>
  </tr>
  <tr>
    <td><code>uz-Latn-UZ</code></td>
    <td>Ouzbek (latin) </td>
    <td>Ouzbékistan </td>
  </tr>
  <tr>
    <td><code>vi-VN</code></td>
    <td>Vietnamien </td>
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
    <td>Zoulou </td>
    <td>Afrique du Sud </td>
  </tr>
</table>
