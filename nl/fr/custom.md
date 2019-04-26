---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

keywords: authentication, authorization, identity, app security, secure, custom, proprietary, private key, public key, jwt

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

# Personnalisation
{: #custom-identity}

Vous pouvez utiliser votre propre fournisseur d'identité personnalisé lorsque vous vous authentifiez. Votre fournisseur d'identité peut se conformer à tout mécanisme d'authentification non spécifiquement pris en charge par {{site.data.keyword.appid_full}}, y compris aux mécanismes propriétaires.
{: shortdesc}

Lorsqu'{{site.data.keyword.appid_short_notm}} ne propose pas de prise en charge directe pour un fournisseur d'identité particulier, vous pouvez utiliser le flux d'identité personnalisé pour relier le protocole d'authentification au flux d'authentification existant d'{{site.data.keyword.appid_short_notm}}. Par exemple, vous pouvez utiliser GitHub ou LinkedIn pour autoriser vos utilisateurs à se connecter. Vous pouvez utiliser le logiciel SDK existant du fournisseur d'identité pour faciliter les informations d'authentification de l'utilisateur avant de les conditionner et de les échanger avec {{site.data.keyword.appid_short_notm}}. Dans de nombreux scénarios d'entreprise, un fournisseur d'identité existant peut utiliser son propre protocole d'authentification personnalisé, mais vous pouvez toujours exploiter les fonctionnalités d'{{site.data.keyword.appid_short_notm}}. Pour ce type de scénario, le flux d'identité personnalisé fournit un moyen découplé d'authentifier vos utilisateurs de manière sécurisée sans exposer leurs données d'identification.

## Configuration de l'identité personnalisée
{: #custom-configure}

Vous pouvez utiliser les étapes suivantes pour configurer votre fournisseur d'identité personnalisé pour utiliser {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

### Avant de commencer
{: #custom-identity-before}

Pour établir la confiance entre {{site.data.keyword.appid_short_notm}} et votre fournisseur d'identité personnalisé, vous devez disposer d'une paire de clés PEM RSA d'une longueur minimale de 2048 caractères. Assurez-vous de sauvegarder les clés que vous utilisez en production de manière sécurisée.

Comment les clés sont-elles utilisées ?

- Votre clé privée est utilisée dans votre application ou votre fournisseur d'identité pour signer les jetons JWT.
- Votre clé publique est utilisée par {{site.data.keyword.appid_short_notm}} pour valider le jeton JWT contenant des informations utilisateur.

Pour générer une paire de clés PEM RSA à l'aide d'Open SSL, exécutez la commande suivante :

```
$ openssl genpkey -algorithm RSA -out private_key.pem -pkeyopt rsa_keygen_bits:2048
$ openssl rsa -pubout -in private_key.pem -out public_key.pem
```
{: codeblock}

</br>

### Configuration à l'aide de l'interface graphique
{: #custom-identity-configure-gui}

1. Connectez-vous à votre compte {{site.data.keyword.cloud_notm}} et accédez à votre instance {{site.data.keyword.appid_short_notm}}.

2. Dans l'onglet **Gérer**, définissez **Custom Identity Provider** sur **Activé**.

3. Enregistrez votre clé publique dans {{site.data.keyword.appid_short_notm}}.
  1. Accédez à l'onglet **Custom Identity Provider**.
  2. Collez votre clé publique dans la zone **Clé publique** et cliquez sur **Sauvegarder**.



### Configuration à l'aide de l'API
{: #custom-identity-configure-api}

Enregistrez votre clé en envoyant une requête PUT au [noeud final d'API de gestion](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_custom_idp).

```
Put {Management URI}/config/idps/custom
Content-Type: application/json
{
    isActive: true,
    config: {
        publicKey: <Your newline separated (\n) PEM public key>
    }
}
```
{: codeblock}

## Test de votre configuration
{: #custom-identity-testing}

Après avoir configuré votre instance {{site.data.keyword.appid_short_notm}} avec une clé publique valide, vous pouvez utiliser l'application de test fournie par le service pour vérifier que votre configuration est correcte. Dans l'exemple d'application, vous pouvez voir les contenus des jetons d'accès et d'identité d'{{site.data.keyword.appid_short_notm}} qui sont renvoyés lors d'un flux de connexion standard.

1. Dans l'onglet **Custom Identity Provider**, cliquez sur **Test** pour ouvrir l'application de test.

2. Créez un exemple de jeton JWT en utilisant [JWT.io](https://jwt.io/) après le [protocole](/docs/services/appid?topic=appid-custom-auth#generating-jwts) d'identité personnalisée.

3. Collez votre jeton JWT dans la case intitulée **Jeton Web JSON** et cliquez sur **Test** pour exécuter un exemple d'authentification.

En cas de succès, vous pouvez voir les jetons d'identité et d'accès d'{{site.data.keyword.appid_short_notm}} décodés qui seront disponibles pour votre application dans un flux de connexion standard.

## Etapes suivantes
{: #custom-identity-next}

Maintenant que votre fournisseur d'identité personnalisé est configuré, [ajoutez-le à votre application](/docs/services/appid?topic=appid-custom-auth#custom-auth) !
