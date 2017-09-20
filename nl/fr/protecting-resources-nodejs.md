---

copyright:
  years: 2017
lastupdated: "2017-05-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Protection des ressources Node.js
{: #protecting-resources-nodejs}

Vous pouvez utiliser le SDK serveur d'{{site.data.keyword.appid_short}} pour protéger les ressources dans votre appli Node.js.
{:shortdesc}

## Avant de commencer
{: #before-you-begin}

* Familiarisez-vous avec le développement d'applications Node.js sur {{site.data.keyword.Bluemix_notm}}.
* Le SDK serveur d'{{site.data.keyword.appid_short_notm}} exige que votre serveur Node.js soit implémenté avec l'`<a href="http://expressjs.com/" target="_blank">infrastructure Express<img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>`.

**Remarque** : d'autres infrastructures, notamment LoopBack,
utilisent des infrastructures `Express`. Vous pouvez utiliser le SDK
serveur d'{{site.data.keyword.appid_short_notm}} avec toutes ces infrastructures.


## Installation du SDK serveur
{: #protecting-resources-serversdk}

1. Depuis la ligne de commande, ouvrez le répertoire dans lequel se trouve votre
application Node.js.
2. Exécutez les commandes ci-dessous. 

  ```
  npm install -save express
  npm install -save passport
  npm install -save bluemix-appid
  ```
  {:pre}

## Protection des ressources dans Node.js
{: #protecting-resources-nodesdk}

Le SDK serveur d'{{site.data.keyword.appid_short_notm}} fournit une stratégie de passeport ApiStrategy qui est utilisée dans les applications de back end déployées sur {{site.data.keyword.Bluemix_notm}}. Pour protéger votre application contre des accès non autorisés, vous devez instrumenter votre serveur Node.js avec la stratégie ApiStrategy. Le module `appid-serversdk-nodejs npm module` fournit la stratégie de passeport ApiStrategy et la méthode de vérification servant à valider le jeton d'accès et le jeton d'identité émis par {{site.data.keyword.appid_short_notm}}.

Le SDK serveur d'{{site.data.keyword.appid_short_notm}} utilise <a href="http://passportjs.org/" target="_blank">l'infrastructure Passport<img src="../../icons/launch-glyph.svg" alt="icône de lien externe"></a> pour contrôler l'autorisation.

Le fragment de code suivant illustre comment utiliser la stratégie `APIStrategy` dans une application Express simple pour protéger les méthodes GET de noeud final `/protected`.

  ```JavaScript

  var express = require('express');
  var passport = require('passport');
  var APIStrategy = require('bluemix-appid').APIStrategy;

  passport.use(new APIStrategy());
  var app = express();
  app.use(passport.initialize());

  app.get('/protected', passport.authenticate('APIStrategy.STRATEGY_NAME', {session: false }),
      function(request, response){
          console.log("Securty context", request.securityContext)
          response.send(200, "Success!");
      }
  );

  app.listen(process.env.PORT);
  ```
  {:pre}

Vous pouvez utiliser `WebAppStrategy` pour protéger des ressources
d'application Web.


  ```JavaScript

  var express = require('express');
  var passport = require('passport');
  var WebAppStrategy = require('bluemix-appid').WebAppStrategy;
  ```
  {:pre}

Pour plus d'informations, voir
le
<a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">référentiel
GitHub Node.js pour
{{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.
