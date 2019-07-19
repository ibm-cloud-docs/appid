---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-09"

keywords: Authentication, authorization, identity, app security, secure, development, troubleshooting, redirected, validation

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
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}

# Dépannage : SAML
{: #troubleshooting-idp}

Si vous rencontrez des problèmes lorsque vous configurez SAML pour travailler avec {{site.data.keyword.appid_full}}, veuillez vous référer aux techniques suivantes pour dépanner et demander de l'aide.
{: shortdesc}


## Problèmes de configuration courants
{: #ts-common-saml}

L'infrastructure SAML prend en charge plusieurs profils, flux et configurations, et par conséquent il est essentiel que la configuration de votre fournisseur d'identité soit correctement effectuée. Consultez les rubriques suivantes pour vous aider à résoudre certains des problèmes courants que vous pourriez rencontrer lorsque vous utilisez SAML.
{: shortdesc}


Pour les codes d'erreur spécifiques et les messages de votre fournisseur d'identité que vous ne voyez pas sur cette page, il peut être utile de rechercher des explications détaillées dans les [spécifications SAML](http://docs.oasis-open.org/security/saml/Post2.0/sstc-saml-tech-overview-2.0.html). Si vous ne trouvez pas ce que vous cherchez, vous pouvez contacter l'administrateur de votre fournisseur d'identité pour plus d'informations.
{: note}



### Paramètre `RelayState` manquant
{: #ts-saml-relaystate}

**Que se passe-t-il ?**

Le paramètre `RelayState` est manquant dans votre réponse d'authentification.


**Pourquoi ?**

{{site.data.keyword.appid_short_notm}} envoie un paramètre opaque appelé `RelayState` dans le cadre de la demande d'authentification. Si vous ne voyez pas ce paramètre dans votre réponse, il se peut que votre fournisseur d'identité ne soit pas configuré pour le renvoyer correctement. Le paramètre `RelayState` a le format suivant.

```
https://idp.example.org/SAML2/SSO/Redirect?SAMLRequest=request&RelayState=token
```
{: screen}

**Comment résoudre le problème ?**

Vérifiez que votre fournisseur SAML est configuré pour renvoyer le paramètre `RelayState` à {{site.data.keyword.appid_short_notm}} sans le modifier en aucune façon.


### Paramètre NameId manquant ou incorrect
{: #ts-saml-nameid}

**Que se passe-t-il ?**

Lorsque vous envoyez une demande d'authentification, vous recevez une erreur concernant le paramètre `NameID`.

**Pourquoi ?**

{{site.data.keyword.appid_short_notm}}, en tant que fournisseur de services, définit la manière dont les utilisateurs sont identifiés par le service et par le fournisseur d'identité. Avec {{site.data.keyword.appid_short_notm}}, les utilisateurs sont identifiés dans la demande d'authentification `NameID` dans la zone `NameID`, comme indiqué dans l'exemple suivant.

```
<NameIDFormat>urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress</NameIDFormat>
```
{: screen}

**Comment résoudre le problème ?**

Pour résoudre le problème, assurez-vous que le paramètre `NameID` de votre fournisseur d'identité est formaté en tant qu'adresse e-mail. Vérifiez que tous les utilisateurs de votre registre de fournisseurs d'identité ont un format d'adresse e-mail valide. Ensuite, vérifiez que la zone `NameID` est correctement définie pour qu'un e-mail valide soit toujours renvoyé, même si les utilisateurs de votre registre ont plusieurs adresses e-mail.



### Echec de signature de la réponse
{: #ts-saml-response-sign-fail}

**Que se passe-t-il ?**

Lorsque vous envoyez une demande d'authentification, vous recevez le message d'erreur suivant :

```
Could not verify SAML assertion signature. Ensure {{site.data.keyword.appid_short_notm}} is configurated with your SAML provider's signing certificate.
```
{: screen}

**Pourquoi ?**

{{site.data.keyword.appid_short_notm}} s'attend à ce que toutes les assertions SAML présentes dans votre réponse soient signées. Si le service ne peut pas trouver ou vérifier la signature dans la réponse, cette erreur est renvoyée.

**Comment résoudre le problème ?**

Pour résoudre le problème, assurez-vous que :

* Vous avez extrait le certificat de signature du fichier XML de métadonnées de votre fournisseur d'identité. Assurez-vous d'utiliser la clé avec `<KeyDescriptor use="signing">`.
* Vous avez défini l'algorithme de signature de réponse comme étant XXX. 





### Echec du déchiffrement de la réponse
{: #ts-saml-decrypt-fail}

**Que se passe-t-il ?**

Vous recevez l'un des messages d'erreur suivants en réponse à votre demande d'authentification.

Message d'erreur 1 :

```
Unexpectedly received an encrypted assertion. Please enable response encryption in your {{site.data.keyword.appid_short_notm}} SAML configuration.
```
{: screen}

Message d'erreur 2 : 

```
Could not decrypt SAML assertion. Ensure your SAML provider is configured with the {{site.data.keyword.appid_short_notm}} encryption. 
```
{: screen}


**Pourquoi ?**

Si votre fournisseur d'identité est configuré pour le chiffrement, {{site.data.keyword.appid_short_notm}} doit être configuré pour signer les demandes d'authentification SAML (AuthnRequest). Ensuite, votre fournisseur d'identité doit être configuré pour attendre la configuration correspondante. Vous pourriez recevoir ces erreurs pour l'une des raisons suivantes :

- {{site.data.keyword.appid_short_notm}} n'est pas configuré pour s'attendre à ce que la réponse SAML du fournisseur d'identité soit chiffrée.
- {{site.data.keyword.appid_short_notm}} ne peut pas déchiffrer correctement vos assertions.


**Comment résoudre le problème ?**

Si vous recevez le message d'erreur 1, vérifiez que votre configuration SAML est configurée pour recevoir une réponse chiffrée. Par défaut, {{site.data.keyword.appid_short_notm}} ne s'attend pas à ce que la réponse soit chiffrée. Pour configurer le chiffrement, définissez le paramètre `encryptResponse` sur **true** à l'aide de [l'API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp).

Si vous recevez le message d'erreur 2, assurez-vous que votre certificat est correct. Vous pouvez obtenir le certificat de signature à partir du fichier XML de métadonnées de {{site.data.keyword.appid_short_notm}}. Assurez-vous d'utiliser la clé avec `<KeyDescriptor use="signing">`. Vérifiez que votre fournisseur d'identité est configuré pour utiliser `` comme algorithme de signature. 


### Code d'erreur du répondeur
{: #ts-saml-responder}

**Que se passe-t-il ?**

Lorsque vous envoyez une demande d'authentification, vous recevez le message d'erreur générique suivant :

```
urn:oasis:names:tc:SAML:2.0:status:Responder
```
{: screen}

**Pourquoi ?**

Bien que {{site.data.keyword.appid_short_notm}} envoie la demande d'authentification initiale, le fournisseur d'identité doit effectuer l'authentification de l'utilisateur et renvoyer la réponse. Il y a plusieurs raisons qui peuvent amener votre fournisseur d'identité à envoyer ce message d'erreur.

Le message peut s'afficher si votre fournisseur d'identité : 

* Ne parvient pas à trouver ou vérifier le nom d'utilisateur
* Ne prend pas en charge le format `NameID` défini dans la demande d'authentification (`AuthnRequest`).
* Ne prend pas en charge le contexte d'authentification.
* Nécessite que la demande d'authentification soit signée ou utilise un algorithme spécifique dans la signature.

**Comment résoudre le problème ?**

Pour résoudre le problème, vérifiez votre configuration et votre nom d'utilisateur. Vérifiez que le contexte d'authentification et les variables définies sont corrects. Vérifiez si votre demande doit être signée d'une manière spécifique.




### Demande d'authentification non prise en charge
{: #ts-saml-unsupported-request}

**Que se passe-t-il ?**

Vous recevez un message concernant une demande d'authentification non prise en charge.

**Pourquoi ?**

Lorsque {{site.data.keyword.appid_short_notm}} génère une demande d'authentification, il peut utiliser le contexte d'authentification pour demander la qualité de l'authentification et des assertions SAML.

**Comment résoudre le problème ?**

Pour résoudre le problème, vous pouvez mettre à jour votre contexte d'authentification. Par défaut, {{site.data.keyword.appid_short_notm}} utilise la classe d'authentification `urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport` et la comparaison `exact`. Vous pouvez mettre à jour le paramètre de contexte pour l'adapter à votre cas d'utilisation à l'aide des API.




### Echec de signature de la demande SAML
{: #ts-saml-request-sign-fail}

**Que se passe-t-il ?**

Vous recevez une erreur qui indique qu'une demande d'authentification ne peut pas être vérifiée.

**Pourquoi ?**

{{site.data.keyword.appid_short_notm}} peut être configuré pour signer la demande d'authentification SAML (`AuthNRequest`), mais votre fournisseur d'identité doit être configuré pour recevoir la configuration correspondante.

**Comment résoudre le problème ?**

Pour résoudre le problème :

* Vérifiez qu'{{site.data.keyword.cloud_notm}} est configuré pour signer la demande d'authentification en réglant le paramètre `signRequest` sur `true` à l'aide de l'[API set SAML IdP](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp). Vous pouvez vérifier si votre demande d'authentification est signée en consultant l'URL de la demande. La signature est incluse comme paramètre de requête. Par exemple : `https://idp.example.org/SAML2/SSO/Redirect?SAMLRequest=request&SigAlg=value&Signature=value&RelayState=token`

* Vérifiez que votre fournisseur d'identité est configuré avec le bon certificat. Pour obtenir le certificat de signature, vérifiez le fichier XML de métadonnées {{site.data.keyword.cloud_notm}} que vous avez téléchargé du tableau de bord {{site.data.keyword.cloud_notm}}. Assurez-vous d'utiliser la clé avec `<KeyDescriptor use="signing">`.

* Vérifiez que votre fournisseur d'identité est configuré pour utiliser `` comme algorithme de signature.



## Débogage de votre connexion
{: #ts-saml-debug-connection}

La configuration est correcte mais continue de boguer ? Consultez les conseils suivants pour déboguer votre connexion SAML.
{: shortdesc}


### Comment puis-je capturer ma demande d'authentification SAML et ma réponse ?
{: #ts-saml-capture}

Il existe plusieurs options pour les plug-ins de navigateur tels que [Firefox](https://addons.mozilla.org/en-US/firefox/addon/saml-tracer/) et [Chrome](https://chrome.google.com/webstore/detail/saml-tracer/mpdajninpobndbfcldcmbpnnbhibjmch?hl=en) qui peuvent être utilisées pour capturer vos demandes et réponses SAML. Vous ne voulez pas utiliser un plug-in ? Pas de problème. Atlassian fournit des instructions pour une [approche d'extraction plus manuelle](https://confluence.atlassian.com/jirakb/how-to-view-a-saml-responses-in-your-browser-for-troubleshooting-872129244.html).


### Je ne comprends pas les messages. Comment puis-je les décoder ?
{: #ts-saml-decode-messages}

Si vous continuez à avoir des problèmes après avoir utilisé votre outil de débogage SAML, essayez d'utiliser les [outils de développement SAML](https://www.samltool.com/online_tools.php) pour obtenir une aide supplémentaire pour décoder vos messages. N'oubliez pas ! Selon l'endroit où vous interceptez vos messages SAML, votre requête peut être [codée en URL](https://www.samltool.com/online_tools.php), [codée en base 64 et dégonflée](https://www.samltool.com/decode.php) ou [chiffrée](https://www.samltool.com/decrypt.php).

N'utilisez pas d'outils en ligne pour déchiffrer les messages SAML comme votre réponse SAML. Les outils ont besoin d'accéder à la clé privée de chiffrement pour pouvoir déchiffrer les informations. La clé doit rester privée et l'accès doit être contrôlé. L'outil de déchiffrement mentionné dans cette section ne doit être utilisé qu'à des fins de débogage.
{: important}

