---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-09"

keywords: authentication, authorization, identity, app security, secure, development, two factor, mfa 

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


# Authentification multi-facteur
{: #cd-mfa}


Demander plusieurs facteurs lors de la connexion vous permet d'accroître la sécurité de l'authentification d'utilisateur auprès des applications. Avec Cloud Directory for {{site.data.keyword.appid_full}}, le premier facteur est le mot de passe utilisateur Cloud Directory, que les utilisateurs utilisent normalement pour se connecter. Le second facteur d'authentification est un code à utilisation unique envoyé à l'utilisateur {{site.data.keyword.appid_short_notm}} par SMS ou par courrier électronique. {{site.data.keyword.appid_short_notm}} utilise une combinaison des deux facteurs pour vérifier l'identité d'un utilisateur.
{: shortdesc}

L'authentification multi-facteur {{site.data.keyword.appid_short_notm}} est prise en charge dans le flux de code d'autorisation OAuth 2.0 pour les utilisateurs Cloud Directory via le widget de connexion. Si vous utilisez une connexion d'entreprise avec SAML 2.0 ou une connexion sociale, vous pouvez activer l'authentification multi-facteur via ce fournisseur d'identité.
{: note}

Lorsque l'authentification multi-facteur est activée, le widget de connexion {{site.data.keyword.appid_short_notm}} exige une seconde forme de vérification (second facteur d'authentification) chaque fois qu'un utilisateur tente de se connecter. Une fois que l'utilisateur a entré avec succès ses données d'identification, un code à utilisation unique est envoyé à l'adresse de courrier électronique ou au numéro de téléphone enregistré pour le compte de l'utilisateur.

Examinez le diagramme suivant pour voir comment fonctionne le flux d'authentification multi-facteur.

![Flux d'authentification multi-facteur](images/mfa.png)

1. Le widget de connexion d'{{site.data.keyword.appid_short_notm}} s'affiche et l'utilisateur entre ses données d'identification Cloud Directory. Ces données d'identification sont soit son adresse de courrier électronique soit son nom d'utilisateur, et son mot de passe. Les données d'identification de l'utilisateur Cloud Directory constituent le premier facteur d'authentification.

2. Les données d'identification sont validées et l'écran d'authentification multi-facteur pour la vérification du second facteur est renvoyé. Selon la configuration du second facteur, l'utilisateur reçoit un courrier électronique ou un SMS contenant un code à utilisation unique qu'il entre dans l'écran de vérification.

3. Si le code d'authentification multi-facteur est validé, l'utilisateur est redirigé vers l'application et connecté.


## Comprendre l'authentification multi-facteur
{: #cd-mfa-understanding}


L'authentification multi-facteur est une méthode permettant de confirmer l'identité d'un utilisateur en lui demandant de prouver à l'aide de plusieurs facteurs qu'il est bien la personne qu'il dit être. Ces facteurs peuvent être une informations que détient l'utilisateur en plus d'une information qu'il connaît ou qui indique qui il est.
{: shortdesc}

A sa première activation, l'authentification multi-facteur est définie pour utiliser par défaut les courriers électroniques. Vous pouvez modifier ce paramétrage afin d'utiliser des SMS, mais vous ne pouvez pas configurer les deux en même temps. Pour les courriers électroniques comme pour les SMS, quelques paramètres sont automatiquement configurés et vous ne pouvez pas les modifier.


<table>
  <tr>
    <th>Paramètre</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>Caractères du code</td>
    <td>Six caractères numériques</td>
  </tr>
  <tr>
    <td>Validité du code</td>
    <td>Quinze minutes <br> Lorsqu'un utilisateur ne valide pas son code dans les quinze minutes, il peut demander qu'un autre code lui soit envoyé sous réserve que la session d'authentification n'a pas expiré. Le code peut être envoyé plusieurs fois au cours de la session d'authentification. Une fois la session d'authentification expirée, l'utilisateur doit répéter le processus de connexion depuis le début.</td>
  </tr>
</table>

<p>Défini dans SCIM en tant qu'<a href="https://tools.ietf.org/html/rfc7643#section-2.4" target="_blank">attribut à valeurs multiples <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>, l'adresse de courrier électronique ou le numéro de téléphone d'un utilisateur Cloud Directory peut contenir les éléments suivants :
<ul>
  <li>Valeur : la valeur réelle de l'attribut telle que l'adresse de courrier électronique ou le numéro de téléphone.</li>
  <li>Principale : une valeur booléenne qui indique la valeurs préférée pour l'attribut. La valeur d'attribut principale <code>true</code> n'est possible qu'une seule fois. Si elle n'est pas spécifiée, la valeur de <code>principale</code> est <code>false</code>.</li>
</ul>Pour plus d'informations, voir la [documentation Cloud Directory](/docs/services/appid?topic=appid-cloud-directory#cloud-directory).</p>



## Configuration du canal de courrier électronique d'authentification multi-facteur
{: #cd-mfa-configure-email}

Vous pouvez configurer {{site.data.keyword.appid_short_notm}} de manière à envoyer un code d'authentification multi-facteur à vos utilisateurs par courrier électronique.
{: shortdesc} 

A la première activation de l'authentification multi-facteur, deux événements se produisent :

- Le canal de courrier électronique est sélectionné par défaut. Vous pouvez basculer sur le [canal SMS](/docs/services/appid?topic=appid-cd-mfa#cd-mfa-configure-sms).
- {{site.data.keyword.appid_short_notm}} enregistre automatiquement l'adresse de courrier électronique principale associée au profil de votre utilisateur Cloud Directory.

Lorsque l'adresse de courrier électronique d'un utilisateur n'est pas déjà confirmée, via des [API de gestion](https://us-south.appid.cloud.ibm.com/swagger-ui/#/) ou une vérification des adresses de courrier électronique au moment de son inscription, elle est confirmée lors de la vérification du code d'authentification multi-facteur.

Avant de démarrer, assurez-vous que votre instance {{site.data.keyword.appid_short_notm}} figure sur le [plan de tarification à tranches graduées](/docs/services/appid?topic=appid-faq#faq-pricing).
{: note}

### Avec l'interface graphique
{: #cd-mfa-configure-email-gui}

Vous pouvez configure le canal de courrier électronique d'authentification multi-facteur à l'aide de l'interface graphique.

1. Accédez à l'onglet **Cloud Directory > Authentification multi-facteur** du tableau de bord {{site.data.keyword.appid_short_notm}}.

2. Dans la section **Activer l'authentification multi-facteur**, sur l'onglet des **paramètres**, basculez l'authentification multi-facteur sur **Activé**. Confirmez que vous avez compris que l'authentification multi-facteur est facturée en tant qu'[événement de sécurité avancée](/docs/services/appid?topic=appid-faq#faq-pricing). Par défaut, **E-mail** est sélectionné comme **Méthode d'authentification**.

3. Dans l'onglet **Canal des e-mails**, examinez le **Modèle d'e-mail**. Vous pouvez choisir d'envoyer le modèle avec les termes fournis ou rédiger votre propre message. Veillez à utiliser la balise HTML appropriée. Dans l'interface graphique, vous pouvez ajouter des paramètres et insérer des images. Pour modifier la [langue](/docs/services/appid?topic=appid-cd-messages#cd-languages) du message, vous pouvez utiliser des <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Config/mgmt.updateLocalization" target="_blank">API <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> afin de définir la langue. Toutefois, le contenu et la traduction du message sont de votre seule responsabilité. Consultez le tableau suivant pour la liste des tables utilisables dans ce message et dans tous les autres messages que vous pouvez envoyer. Un blanc apparaît à la place d'un paramètre si l'utilisateur n'a pas fourni l'information correspondante.

  <table>
    <thead>
      <tr>
        <th colspan=2><img src="images/idea.png" alt="Icône Plus d'informations"/> Paramètres des messages d'authentification multi-facteur</th>
      </tr>
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
      <tr>
        <td><code>%{mfa.code}</code></td>
        <td> Affiche un code de vérification d'authentification multi-facteur unique. </td>
      </tr>
    </tbody>
  </table>

  Un blanc apparaît à la place d'un paramètre si l'utilisateur n'a pas fourni l'information correspondante.
  {: tip}


### Avec les API
{: #cd-mfa-configure-email-apis}

**Avant de commencer**

Assurez-vous de disposer des prérequis suivants :

* Votre ID titulaire d'instance {{site.data.keyword.appid_short_notm}}. Cet ID est disponible dans la section **Données d'identification pour le service** du tableau de bord.
* Votre jeton IAM (Identity and Access Management). Pour de l'aide concernant l'obtention d'un jeton IAM, consultez la [documentation IAM](/docs/iam?topic=iam-iamtoken_from_apikey#iamtoken_from_apikey).


1. Activez l'authentification multi-facteur en envoyant une requête PUT au noeud final `/config/mfa` avec votre configuration d'authentification multi-facteur pour définir `isActive` sur `true`.

  En-tête :
  ```
  PUT {management-url}/management/v4/{tenantId}/config/mfa
       Host: <management-server-url>
       Authorization: Bearer <IAM_TOKEN>
       Content-Type: application/json
  ```
  {: codeblock}

  Corps :
  ```
   {
       "isActive": true
   }
  ```
  {: codeblock}

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

2. Activez le canal d'authentification multi-facteur en envoyant une requête PUT au noeud final `/mfa/channels/{channel}` avec votre configuration d'authentification multi-facteur. Lorsque `isActive` est défini sur `true`, votre canal d'authentification multi-facteur est activé.

  En-tête :
  ```
  PUT /management/v4/{tenantId}/mfa/channels/{channel}
       Host: <management-server-url>
       Authorization: Bearer <IAM_TOKEN>
       Content-Type: application/json
  ```
  {: codeblock}

  Corps :
  ```
   {
       "isActive": true
   }
  ```
  {: codeblock}

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
    '{management-url}/management/v4/{tenantId}/mfa/channels/email'
  ```
  {: screen}

Si votre instance {{site.data.keyword.appid_short_notm}} Cloud Directory est configurée pour fonctionner avec un répartiteur de courrier électronique personnalisé, l'authentification multi-facteur utilise le même répartiteur pour envoyer le code à utilisation unique. Pour plus d'informations sur le paramétrage d'un répartiteur personnalisé, voir la documentation [Cloud Directory](/docs/services/appid?topic=appid-cd-messages#cd-custom-email).
{: note}




## Configuration de l'authentification multi-facteur pour un fonctionnement avec des SMS
{: #cd-mfa-configure-sms}

Vous pouvez envoyer un message SMS à vos utilisateurs comme second élément de vérification. Lorsque vous activez les SMS, {{site.data.keyword.appid_short_notm}} tente automatiquement d'enregistrer le premier numéro de téléphone principal [valide](https://en.wikipedia.org/wiki/E.164) trouvé dans un profil d'utilisateur Cloud Directory. Si le numéro n'est pas valide ou qu'aucun numéro de téléphone n'est trouvé dans le profil d'utilisateur, un widget d'enregistrement s'affiche pour permettre à l'utilisateur d'ajouter un numéro. Ensuite, le numéro fait partie du profil d'utilisateur et, après validation, devient le numéro par défaut utilisé pour l'authentification multi-facteur.
{: shortdesc}

**Avant de commencer**

{{site.data.keyword.appid_short_notm}} utilise [Nexmo](https://www.nexmo.com/products/sms) pour envoyer par SMS les codes à utilisation unique d'authentification multi-facteur. Avant de commencer, vérifiez que vous disposez d'une instance {{site.data.keyword.appid_short_notm}} qui figure sur le [plan de tarification à tranches graduées](/docs/services/appid?topic=appid-faq#faq-pricing) et des informations Nexmo suivantes.

 - Procurez-vous votre clé d'API et votre secret Nexmo. Ces informations figurent sur la page des paramètres de votre compte dans le tableau de bord Nexmo. Pour plus d'informations sur l'obtention de vos données d'identification, voir la [documentation Nexmo](https://developer.nexmo.com/concepts/guides/authentication#api-key-and-secret).

 - Enregistrez votre ID d'émetteur ou le numéro `émetteur` dans Nexmo. Ce numéro `émetteur` est celui qui s'affiche sur le téléphone de votre utilisateur pour indiquer d'où provient le SMS. Dans certains pays, Nexmo prend en charge les ID d'émetteur alphanumériques. {{site.data.keyword.appid_short_notm}} utilise la valeur que vous avez entrée en tant qu'ID d'émetteur Nexmo. Par conséquent, s'ils sont pris en charge par Nexmo, vous pouvez utiliser les ID avec {{site.data.keyword.appid_short_notm}}. Pour plus d'informations, voir la [documentation Nexmo](https://help.nexmo.com/hc/en-us/articles/217571017-What-is-a-Sender-ID).


### Avec l'interface graphique
{: #cd-mfa-configure-sms-gui}

Pour configurer l'authentification multi-facteur avec l'interface graphique, consultez [Cloud Directory](/docs/services/appid?topic=appid-cloud-directory).
{: note}

1. Accédez à l'onglet **Cloud Directory > Authentification multi-facteur** du tableau de bord {{site.data.keyword.appid_short_notm}}.

2. Dans la section **Activer l'authentification multi-facteur**, sur l'onglet des **paramètres**, basculez l'authentification multi-facteur sur **Activé**. Confirmez que vous avez compris que l'authentification multi-facteur est facturée en tant qu'[événement de sécurité avancée](/docs/services/appid?topic=appid-faq#faq-pricing).

3. Sélectionnez **SMS** comme **méthode d'authentification**.

4. Dans l'onglet **Canal des SMS**, configurez vos informations de compte Nexmo.

    1. Si vous n'avez pas encore ce compte Nexmo, créez-en un.

    2. Dans le tableau de bord Nexmo, cliquez sur **SMS**.

    3. Dans la section **Code it yourself**, copiez votre clé d'API et collez-la dans la zone **key** du tableau de bord {{site.data.keyword.appid_short_notm}}.

    4. Copiez la valeur de la zone **API secret** du tableau de bord Nexmo et collez-la dans la zone **Secret** du tableau de bord {{site.data.keyword.appid_short_notm}}.

    5. Entrez [l'ID](https://help.nexmo.com/hc/en-us/articles/217571017-What-is-a-Sender-ID) à partir duquel vous souhaitez envoyer des messages. Un format valide suit le [format de numérotation international E.164](https://en.wikipedia.org/wiki/E.164) (par exemple, pour un numéro aux Etats-Unis, `+1 999 888 7777 `). Vous devez spécifier à la fois le code pays précédé du signe `+` et le numéro national de l'abonné. Dans certains pays, Nexmo prend en charge les ID d'émetteur alphanumériques. {{site.data.keyword.appid_short_notm}} utilise la valeur que vous avez entrée en tant qu'ID d'émetteur Nexmo. Par conséquent, s'ils sont pris en charge par Nexmo, vous pouvez utiliser les ID avec {{site.data.keyword.appid_short_notm}}. 



### Avec les API
{: #cd-mfa-configure-sms-api}

**Avant de commencer**

Assurez-vous de disposer des prérequis suivants :

* Votre ID titulaire d'instance {{site.data.keyword.appid_short_notm}}. Cet ID est disponible dans la section **Données d'identification pour le service** du tableau de bord.
* Votre jeton IAM (Identity and Access Management). Pour de l'aide concernant l'obtention d'un jeton IAM, consultez la [documentation IAM](/docs/iam?topic=iam-iamtoken_from_apikey).


1. Activez l'authentification multi-facteur en envoyant une requête PUT au noeud final `/config/mfa` avec votre configuration d'authentification multi-facteur pour définir `isActive` sur `true`.

En-tête :

  ```
  PUT {management-url}/management/v4/{tenantId}/config/mfa
       Host: <management-server-url>
       Authorization: Bearer <IAM_TOKEN>
       Content-Type: application/json
  ```
  {: codeblock}

Corps :

  ```
  {
   "isActive": true
   }
  ```
  {: codeblock}


Exemple de demande :

  ```
  $ curl -X PUT
    --header 'Content-Type: application/json'
    --header 'Accept: application/json'
    --header 'Authorization: Bearer <IAM_TOKEN>'
    -d '{
    "isActive": true
      }'
  '{management-url}/management/v4/{tenantId}/config/mfa'
  ```
  {: screen}

2. Activez le canal d'authentification multi-facteur en envoyant une requête PUT au noeud final `/mfa/channels/{channel}` avec votre configuration d'authentification multi-facteur. Lorsque `isActive` est défini sur `true`, votre canal d'authentification multi-facteur est activé.
`config` extrait la clé d'API et le secret Nexmo ainsi que le numéro de `from`.

En-tête :

  ```
  PUT /management/v4/{tenantId}/mfa/channels/{channel}
       Host: <management-server-url>
       Authorization: Bearer <IAM_TOKEN>
       Content-Type: application/json
  ```
  {: codeblock}

Corps :

  ```
  {
      "isActive": true,
      "config": {
        "key": "nexmo key",
        "secret": "nexmo secret",
        "from": sender-phoneNumber
      }
  }
  ```
  {: codeblock}

Exemple de demande :

  ```
  $ curl -X PUT
    --header 'Content-Type: application/json'
    --header 'Accept: application/json'
    --header 'Authorization: Bearer <IAM_TOKEN>'
    -d '{
         "isActive": true,
      "config": {
          "key": "key",
          "secret": "secret",
          "from": 12345678900
        }
     }'
   '{management-url}/management/v4/{tenantId}/mfa/channels/nexmo'
  ```
  {: screen}


3. Une fois le canal correctement configuré, vérifiez que votre configuration et connexion Nexmo sont correctes
à l'aide du bouton de test de l'interface utilisateur ou de l'API de gestion.

En-tête :

  ```
  POST /management/v4/{tenantId}/config/cloud_directory/sms_dispatcher/test
     Host: <management-server-url>
     Authorization: Bearer <IAM_TOKEN>
     Content-Type: application/json
  ```
  {: codeblock}

Corps :

  ```
  {
    "phone_number": "phoneNumber-receives-test-message"
  }
  ```
  {: codeblock}

Exemple de demande :

  ```
  $ curl -X POST
  --header 'Content-Type: application/json'
  --header 'Accept: application/json'
  --header 'Authorization: Bearer <IAM_TOKEN>'
  -d '{
        "phone_number": "+1 999 999 9999"
      }'
  '{management-url}/management/v4/{tenantId}/config/cloud_directory/sms_dispatcher/test'
  ```
  {: screen}

  </br>
