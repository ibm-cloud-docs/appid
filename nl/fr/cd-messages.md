---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-20"

keywords: authentication, authorization, identity, app security, secure, directory, registry, passwords, languages, lockout

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

# Personnalisation des courriers électroniques
{: #cd-types}

Lorsqu'un utilisateur interagit avec votre application, vous pouvez parfois souhaiter envoyer une réponse ou demander une vérification. {{site.data.keyword.appid_short_notm}} fournit des modèles par défaut que vous pouvez utiliser pour les interactions. Vous pouvez également utiliser les modèles pour vous guider et personnaliser vos messages de manière à les adapter à votre marque.
{: shortdesc}

{{site.data.keyword.appid_short_notm}} utilise <a href="https://www.sendgrid.com" target="_blank">SendGrid <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> comme service de distribution de courrier. Tous les courriers électroniques sont envoyés à l'aide d'un seul compte SendGrid.
{: note}

## Modèles de courrier électronique
{: #cd-messages}

Lorsque vous envoyez des messages à vos utilisateurs, vous pouvez utiliser n'importe quelle combinaison des modèles suivants ou modifier les modèles pour personnaliser votre message.
{: shortdesc}

Outre les types de message suivants, vous pouvez également profiter des modèles de [connexion unique](/docs/services/appid?topic=appid-cd-sso#cd-sso) et  d'[authentification multi-facteur](/docs/services/appid?topic=appid-cd-mfa#cd-mfa).
{: tip}

Vous pouvez utiliser des paramètres dans vos messages afin de les personnaliser encore plus. Consultez le tableau suivant pour voir les paramètres utilisables dans tous les types de message.

<table>
  <tr>
    <th colspan=2><img src="images/idea.png" alt="Icône Plus d'informations"/> Tous les paramètres de message </th>
  </tr>
  <tr>
    <td><code>%{display.logo}</code></td>
    <td> Affiche l'image que vous avez configurée pour votre widget de connexion.</td>
  </tr>
  <tr>
    <td><code>%{user.displayName}</code></td>
    <td> Affiche le pseudonyme (appelé nom d'écran dans l'interface) que l'utilisateur choisit d'utiliser lorsqu'il interagit avec l'application.</td>
  </tr>
  <tr>
    <td><code>%{user.email}</code></td>
    <td> Affiche l'adresse électronique avec laquelle l'utilisateur s'est inscrit.</td>
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
</table>


### Courrier électronique de bienvenue
{: #cd-messages-welcome}

Lorsqu'un utilisateur se connecte à votre application, vous pouvez souhaiter lui envoyer un message de bienvenue. 
{: shortdesc}

1. Accédez à l'onglet **Modèles de flux de travaux > Courrier électronique de bienvenue** du tableau de bord du service.

2. Définissez **Courrier électronique de bienvenue** sur **Activé**.

3. Personnalisez le contenu de votre message. Vous pouvez ajouter des paramètres et insérer des images à l'aide de l'interface utilisateur. Pour modifier la [langue](/docs/services/appid?topic=appid-cd-messages#cd-languages) du message, vous pouvez utiliser des <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">API <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> afin de définir la langue. Toutefois, le contenu et la traduction du message sont de votre seule responsabilité. Consultez le tableau suivant pour la liste des tables utilisables dans ce message et dans tous les autres messages que vous pouvez envoyer. Un blanc apparaît à la place d'un paramètre si l'utilisateur n'a pas fourni l'information correspondante.

4. Cliquez sur **Sauvegarder**.


### Courrier électronique de vérification
{: #cd-messages-verification}

Lorsqu'un utilisateur se connecte à votre application à l'aide de son adresse électronique, vous pouvez lui envoyer un message lui demandant de confirmer son identité. Vous limiterez ainsi le nombre de faux comptes (notamment les robots) qui peuvent s'inscrire à votre application. Vous pouvez restreindre l'accès à votre application jusqu'à ce qu'un utilisateur confirme son adresse e-mail, ou l'utiliser pour gérer les utilisateurs pour qui vous créez des profils. Notez que les utilisateurs ajoutés manuellement via le tableau de bord {{site.data.keyword.appid_short_notm}} ou l'API de création d'utilisateur ne reçoivent pas automatiquement ce courrier électronique.
{: shortdesc}


1. Accédez à l'onglet **Modèles de flux de travaux > Vérification de l'adresse électronique** du tableau de bord du service.

2. Définissez **Vérification de l'adresse électronique** sur **Activé**.

3. Définissez **Permettre aux utilisateurs de se connecter à votre application sans vérifier d'abord leur adresse électronique** sur **Oui**. Lorsque cette option est définie sur Oui, les utilisateurs peuvent interagir avec votre application une fois connectés et avant vérification de leur adresse électronique. La valeur par défaut est Non.

4. Personnalisez le contenu de votre message. Vous pouvez ajouter des paramètres et insérer des images à l'aide de l'interface utilisateur. Pour modifier la [langue](/docs/services/appid?topic=appid-cd-messages#cd-languages) du message, vous pouvez utiliser des <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">API <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> afin de définir la langue. Toutefois, le contenu et la traduction du message sont de votre seule responsabilité. Consultez le tableau suivant pour voir les différents paramètres utilisables dans votre message. Un blanc apparaît à la place d'un paramètre si l'utilisateur n'a pas fourni l'information correspondante.

  <table>
    <tr>
      <th colspan=2><img src="images/idea.png" alt="Icône Plus d'informations"/> Paramètres de vérification de message</th>
    </tr>
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
  </table>

  Vous pouvez également utiliser les paramètres de message répertoriés dans la section [Courrier électronique de bienvenue](/docs/services/appid?topic=appid-cd-messages#cd-messages-welcome).
  {: tip}

5. Définissez un délai d'expiration pour l'URL d'action. Le délai d'expiration de l'URL est le temps, en minutes, dont dispose l'utilisateur pour effectuer l'action avant expiration du lien de vérification. Ce paramètre joue également sur la durée de validité du lien de réinitialisation du mot de passe.
 
6. Entrez dans la zone **URL de la page de remerciement** l'URL de la page que vous voulez afficher une fois l'adresse de courrier électronique de l'utilisateur vérifiée. Si vous ne renseignez pas cette zone, une page par défaut {{site.data.keyword.appid_short_notm}} s'affiche.

7. Cliquez sur **Sauvegarder**. 


### Courrier électronique de réinitialisation du mot de passe
{: #cd-messages-reset}

Lorsqu'un utilisateur interagit avec votre application, il peut avoir oublié son mot de passe ou avoir besoin de le mettre à jour. Vous pouvez personnaliser le courrier électronique de réponse à cette demande. Lorsqu'un utilisateur demande à modifier son mot de passe, celui-ci reste inchangé tant que l'utilisateur n'aura pas cliqué sur le lien figurant dans ce courrier électronique.
{: shortdesc}


1. Accédez à l'onglet **Modèles de flux de travaux > Réinitialiser le mot de passe** du tableau de bord du service.

2. Définissez **Courrier électronique d'oubli de mot de passe** sur **Activé**.

3. Personnalisez le contenu de votre message. Vous pouvez ajouter des paramètres et insérer des images à l'aide de l'interface utilisateur. Pour modifier la [langue](/docs/services/appid?topic=appid-cd-messages#cd-languages) du message, vous pouvez utiliser des <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">API <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> afin de définir la langue. Toutefois, le contenu et la traduction du message sont de votre seule responsabilité. Consultez le tableau suivant pour voir les différents paramètres utilisables dans votre message. Un blanc apparaît à la place d'un paramètre si l'utilisateur n'a pas fourni l'information correspondante.

  <table>
    <tr>
      <th colspan=2><img src="images/idea.png" alt="Icône Plus d'informations"/> Paramètres d'oubli de mot de passe</th>
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
      <td> Affiche un code d'accès à usage unique incorporé dans l'URL. Chaque personne recevra donc un code différent. Exemple : `https://us-south.appid.cloud.ibm.com/wfm/verify/6574839563478`</td>
    </tr>
    <tr>
      <td><code>%{resetPassword.link}</code></td>
      <td> Affiche le lien sur lequel l'utilisateur doit cliquer pour réinitialiser son mot de passe.</td>
    </tr>
  </table>

  Vous pouvez également utiliser les paramètres de message répertoriés dans la section [Courrier électronique de bienvenue](/docs/services/appid?topic=appid-cd-messages#cd-messages-welcome).
  {: tip}

4. Définissez un délai d'expiration pour l'URL d'action. Le délai d'expiration de l'URL est le temps, en minutes, dont dispose l'utilisateur pour effectuer l'action avant expiration du lien de vérification. Ce paramètre joue également sur la durée de validité du lien de réinitialisation du mot de passe.
 
5. Entrez dans la zone **URL de la page de redéfinition de mot de passe** l'URL de la page que vous voulez afficher une fois l'adresse de courrier électronique de l'utilisateur vérifiée. Si vous ne renseignez pas cette zone, une page par défaut {{site.data.keyword.appid_short_notm}} s'affiche.

6. Cliquez sur **Sauvegarder**.


### Courrier électronique de changement de mot de passe
{: #cd-messages-password-change}

Vous pouvez faire savoir à l'utilisateur que son mot de passe a changé. Cette option est particulièrement utile s'il n'en a pas fait la demande. Il peut alors effectuer les étapes appropriées pour resécuriser son compte.
{: shortdesc}

1. Accédez à l'onglet **Modèles de flux de travaux > Changer le mot de passe** du tableau de bord du service.

2. Définissez **Courrier électronique de changement de mot de passe** sur **Activé**.

3. Personnalisez le contenu de votre message. Vous pouvez ajouter des paramètres et insérer des images à l'aide de l'interface utilisateur. Pour modifier la [langue](/docs/services/appid?topic=appid-cd-messages#cd-languages) du message, vous pouvez utiliser des <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">API <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> afin de définir la langue. Toutefois, le contenu et la traduction du message sont de votre seule responsabilité. Consultez le tableau suivant pour voir les différents paramètres utilisables dans votre message. Si un utilisateur ne fournit pas l'information recueillie par le paramètre, un blanc apparaît.
  

  <table>
    <tr>
      <th colspan=2><img src="images/idea.png" alt="Icône Plus d'informations"/> Paramètres de changement de mot de passe</th>
    </tr>
    <tr>
      <td><code>%{passwordChangeInfo.time}</code></td>
      <td> Affiche l'heure à laquelle un nouveau mot de passe est entré en vigueur. </td>
    </tr>
    <tr>
      <td><code>%{passwordChangeInfo.ipAddress}</code></td>
      <td> Affiche l'adresse IP d'où provient la demande de changement de mot de passe. </td>
    </tr>
  </table>

  Vous pouvez également utiliser les paramètres de message répertoriés dans la section [Courrier électronique de bienvenue](/docs/services/appid?topic=appid-cd-messages#cd-messages-welcome).
  {: tip}

4. Cliquez sur **Sauvegarder**.




## Utilisation d'un émetteur de courrier électronique personnalisé
{: #cd-custom-email}

Avec {{site.data.keyword.appid_short_notm}}, vous pouvez définir un point d'extension personnalisé pour envoyer vos messages électroniques Cloud Directory. La définition d'un point d’extension vous permet de contrôler entièrement l’envoi des courriers électroniques et d'utiliser votre propre nom de domaine. Par défaut, {{site.data.keyword.appid_short_notm}} utilise <a href="https://www.sendgrid.com" target="_blank">SendGrid <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> comme service de distribution de courrier.
 {: shortdesc}

Vous souhaiterez peut-être utiliser un émetteur de courrier électronique personnalisé pour les raisons suivantes :

- **Domaine personnalisé**
La configuration d'un répartiteur de courriers électroniques personnalisé vous permet d'avoir un contrôle complet sur l'envoi des messages électroniques. Cela inclut la personnalisation du domaine d'e-mail, ce qui peut réduire davantage les risques de filtrage des e-mails en tant que spam. Vous pouvez également améliorer davantage l'expérience de marque des utilisateurs de votre application.

- **Analyses et dépannage**
Obtenez des analyses de votre fournisseur d'e-mail telles que le nombre de personnes ayant ouvert les courriers électroniques ou les messages non distribués. Le fait de pouvoir suivre des messages individuels et consulter des statistiques globales peut vous aider à résoudre des problèmes.

Une fois le point d'extension configuré, il est appelé par {{site.data.keyword.appid_short_notm}} chaque fois qu'un courrier électronique doit être envoyé. Le point d'extension contient toutes les informations sur le message, notamment le contenu final du corps du message.



### Configuration de l'émetteur personnalisé
{: #cd-messages-configure-custom-sender}

Pour configurer votre émetteur de courrier électronique personnalisé, vous devez utiliser l'<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.set_cloud_directory_email_dispatcher" target="_blank">API de gestion</a> de Cloud Directory.


1. Indiquez l'URL. Vous pouvez également fournir des informations d'autorisation. Les types d'autorisation pris en charge sont les suivants : `autorisation de base` ou `valeur d'en-tête de l'autorisation constante`.

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

3. Le corps envoyé par {{site.data.keyword.appid_short_notm}} est au format suivant : `{"jws": "jws-format-string"}`. Après avoir décodé et vérifié le contenu, celui-ci est une chaîne JSON.

  ```
  {
    "tenant": "tenant-id",
      "iss" : "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61", 
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

  <table>
    <tr>
      <th>Variable</th>
      <th>Description</th>
    </tr>
    <tr>
      <td><code>tenant</code></td>
      <td>ID titulaire de votre instance {{site.data.keyword.appid_short_notm}}.</td>
    </tr>
    <tr>
      <td><code> iat </code></td>
      <td>Horodatage d'envoi du message.</td>
    </tr>
    <tr>
      <td><code>iss</code></td>
      <td>Principe ou instance {{site.data.keyword.appid_short_notm}} ayant émis le jeton JWS.</td>
    </tr>
    <tr>
      <td><code>jti</code></td>
      <td>ID transaction unique.</td>
    </tr>
    <tr>
      <td><code>message: to</code></td>
      <td>Adresse électronique du destinataire du message.</td>
    </tr>
    <tr>
      <td><code>message: from</code></br><code>nom</code></br><code>adresse</code></td>
      <td></br>Nom de l'émetteur du message.</br>Adresse électronique de l'émetteur.</td>
    </tr>
    <tr>
      <td><code>Facultatif : message: reply to</code></br><code>nom</code></br><code>adresse</code></td>
      <td></br>Nom associé à l'adresse électronique de réponse.</br>Adresse électronique à laquelle l'utilisateur peut répondre.</td>
    </tr>
  </table>

  Vous pouvez vérifier que votre demande a abouti en vérifiant le code d'état de la réponse. Toute réponse comprise entre 200 et 299 est considérée comme un succès. Si vous recevez une autre réponse, tentez de renvoyer la demande.
  {: tip}

4. Chaque contenu HTTP envoyé depuis {{site.data.keyword.appid_short_notm}} est automatiquement signé conformément à la norme JWS à l'aide d'une paire de clés asymétriques.
Pour chaque instance {{site.data.keyword.appid_short_notm}}, une clé privée et une clé publique sont générées et ne sont pas partagées par d'autres instances. La clé privée est utilisée pour signer le contenu HTTP. La clé publique permet de vérifier que le contenu est généré par {{site.data.keyword.appid_short_notm}} et n'est pas modifié par un tiers, <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#!/Authorization_Server_V4/publicKeys" target="_blank">Noeud final des clés publiques</a>.

5. Exemple de code de point d'extension (JavaScript).
  ```
  const sgMail = require('@sendgrid/mail');
  const {promisify} = require('bluebird');
  const request = promisify(require('request'));
  const jwtVerify = promisify(require('jsonwebtoken').verify);
  const jwtDecode = require('jsonwebtoken').decode;
  const jwkToPem = require('jwk-to-pem');

  async function obtainPublicKeys() {
  	// Your {{site.data.keyword.appid_short_notm}} instance tenant ID
  	const tenantId = '<TENANT-ID>';

  	// Send request to {{site.data.keyword.appid_short_notm}}'s public keys endpoint
  	const keysOptions = {
  		method: 'GET',
  		url: `https://<REGION>.appid.cloud.ibm.com/oauth/v4/${tenantId}/publickeys`
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
  {: screen}

6. Vérifiez que votre configuration est correcte en testant votre répartiteur de courriers électroniques. Utilisez l'<a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Config/post_email_dispatcher_test" target="_blank">API de test</a> pour déclencher une demande auprès de votre émetteur de courrier électronique personnalisé configuré.

Pour un exemple complet, voir <a href="https://www.ibm.com/cloud/blog/use-ibm-cloud-app-id-and-your-email-provider-to-brand-mails-sent-to-app-users" target="_blank">Use your own provider for mail sent with {{site.data.keyword.appid_full}}</a>.



## Langues prises en charge
{: #cd-languages}

Vous pouvez utiliser <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">les API de gestion des langues <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> pour définir la langue dans laquelle la communication avec vos utilisateurs sera écrite. Toutefois, seul l'anglais est disponible sans configuration. Il vous appartient de traduire les messages. Une fois la configuration définie avec l'API, l'interface graphique est mise à jour pour que vous puissiez changer le texte de modèle.
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
    <td>Région administrative spéciale de Macao de la République populaire de Chine</td>
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
    <td>Région administrative spéciale de Macao de la République populaire de Chine</td>
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
