---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-21"

keywords: authentication, authorization, identity, app security, secure, development, ingress, policy, networking, containers, kubernetes

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


# Tutoriel : Configuration d'Ingress pour utilisation d'{{site.data.keyword.appid_short_notm}}
{: #kube-auth}

Vous pouvez appliquer de façon cohérente la sécurité gérée par des règles à l'aide de la fonctionnalité de mise en réseau d'Ingress dans {{site.data.keyword.containerlong}}. Avec cette approche, vous pouvez activer simultanément l'autorisation et l'authentification pour toutes les applications de votre cluster sans même modifier le code de votre application. Ce guide pas à pas vous apprend à configurer votre contrôleur Ingress de manière à utiliser {{site.data.keyword.appid_short_notm}}.
{: shortdesc}

Examinez le flux d'authentification dans le diagramme suivant :

![{{site.data.keyword.appid_short_notm}} Architecture d'intégration Kubernetes](images/kube-integration.png)

1. Un utilisateur ouvre votre application et envoie une demande à l'API ou l'application Web.
2. Pour le flux d'API, le contrôleur Ingress tente de valider les jetons fournis. Si le flux Web est utilisé, il lance un processus d'authentification OIDC en trois étapes.
3. {{site.data.keyword.appid_short_notm}} démarre le processus d'authentification en affichant le widget de connexion.
4. L'utilisateur fournit un nom d'utilisateur ou une adresse de courrier électronique et un mot de passe.
5. Le contrôleur Ingress obtient des jetons d'accès et d'identité d'{{site.data.keyword.appid_short_notm}} pour autorisation.
6. Chaque demande validée et envoyée par le contrôleur Ingress à vos applications a un en-tête d'autorisation qui contient les jetons.

Actuellement, l'intégration du contrôleur Ingress à {{site.data.keyword.appid_short_notm}} ne prend pas en charge les jetons d'actualisation. Lorsque vos jetons d'accès et d'identité expirent, l'utilisateur doit s'authentifier à nouveau.
{: note}


## Avant de commencer
{: #kube-prereqs}

Avant de commencer, vérifiez que les prérequis suivants sont respectés.
{: shortdesc}

Pour des raisons de sécurité, l'authentification {{site.data.keyword.appid_short_notm}} prend en charge uniquement les systèmes de back end avec TLS/SSL activé.
{: note}

* Une application ou un modèle d'application.
* Un cluster Kubernetes standard avec au moins deux noeuds worker par zone. Si vous utilisez Ingress dans des clusters à zones multiples, passez en revue les prérequis supplémentaires indiqués dans la [documentation du service Kubernetes](/docs/containers?topic=containers-ingress#config_prereqs).
* Une instance d'{{site.data.keyword.appid_short_notm}} dans la région où votre cluster est déployé. Vérifiez que le nom du service ne contient aucun espace.

* Les [rôles IAM {{site.data.keyword.cloud_notm}}](/docs/containers?topic=containers-access_reference#access_reference) suivants :
  * Cluster : rôle de plateforme Administrateur
  * Espaces de nom Kubernetes : rôle de service Responsable

* Les interfaces de ligne de commande suivantes :

  * [{{site.data.keyword.cloud_notm}}](/docs/cli/reference/ibmcloud/cloud-cli-install_use?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli)
  * [Kubernetes](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
  * [Docker](https://www.docker.com/products/docker-engine#/download)

* Les [plug-ins d'interface de ligne de commande {{site.data.keyword.cloud_notm}}](/docs/cli/reference/ibmcloud?topic=cloud-cli-plug-ins#plug-ins) suivants :

  * Kubernetes Service
  * Container Registry

Pour obtenir de l'aide sur les interfaces de ligne de commande et les plug-ins téléchargés et l'environnement de service Kubernetes configuré, voir le tutoriel de [création de clusters Kubernetes](/docs/containers?topic=containers-cs_cluster_tutorial#cs_cluster_tutorial_lesson1).
{: tip}

Allons-y !

## Etape 1 : Liaison d'{{site.data.keyword.appid_short_notm}} à votre cluster
{: #kube-create-appid}

Vous pouvez lier votre instance {{site.data.keyword.appid_short_notm}} à votre cluster de façon à autoriser l'utilisation de toutes les instances de votre application déployées dans votre cluster. Lorsque vous liez votre instance de service à votre cluster, vos métadonnées et données d'identification {{site.data.keyword.appid_short_notm}} sont disponibles en tant que valeurs confidentielles Kubernetes dès le démarrage de votre application.
{: shortdesc}


1. Connectez-vous à l'interface de ligne de commande {{site.data.keyword.cloud_notm}}. Suivez les invites de l'interface de ligne de commande pour effectuer la connexion.

  ```
  ibmcloud login -a cloud.ibm.com -r <region>
  ```
  {: codeblock}

  <table>
    <tr>
      <th>Région</th>
      <th>Noeud final</th>
    </tr>
    <tr>
      <td>Dallas</td>
      <td><code>us-south</code></td>
    </tr>
    <tr>
      <td>Francfort</td>
      <td><code>eu-de</code></td>
    </tr>
    <tr>
      <td>Sydney</td>
      <td><code>au-syd</code></td>
    </tr>
    <tr>
      <td>Londres </td>
      <td><code>eu-gb</code></td>
    </tr>
    <tr>
      <td>Tokyo</td>
      <td><code>jp-tok</code></td>
    </tr>
  </table>

2. Définissez le contexte pour votre cluster.

  1. Obtenez la commande permettant de définir la variable d'environnement et téléchargez les fichiers de configuration Kubernetes.

    ```
    ibmcloud ks cluster-config <ID_ou_nom_cluster>
    ```
    {: codeblock}

  2. Copiez la sortie qui commence par `export` et collez-la dans votre terminal pour définir la variable d'environnement `KUBECONFIG`.

3. Vérifiez si vous disposez déjà d'un contrôleur Ingress dans votre espace de nom par défaut. IBM Cloud Kubernetes Service prend en charge un contrôleur Ingress par espace de nom. Si vous en avez déjà un, vous pouvez mettre à jour la configuration Ingress existante ou utiliser un autre espace de nom.

  ```
  kubectl get ingress
  ```
  {: pre}

4. Liez votre instance d'{{site.data.keyword.appid_short_notm}}. Cette liaison crée une clé de service pour l'instance de service. Vous pouvez spécifier une clé de service existante avec l'indicateur `-key`.

  ```
  ibmcloud ks cluster-service-bind --cluster <cluster_name_or_ID> --namespace <namespace> --service <App-ID_instance_name> [--key <service_instance_key>]
  ```
  {: pre}

  Si vous ne spécifiez pas d'espace de nom, la valeur confidentielle est créée dans l'espace de nom `par défaut`.
  {: tip}

  Exemple de sortie :

  ```
  ibmcloud ks cluster-service-bind --cluster mycluster --namespace default --service appid1
  Binding service instance to namespace...
  OK
  Namespace:    default
  Secret name:  binding-appid1
  ```
  {: screen}

Bon travail !

## Etape 2 : Envoi de votre application à Container Registry
{: #kube-registry}

Pour que votre application s'exécute dans Kubernetes, vous devez l'héberger dans un registre.
{: shortdesc}


1. Connectez-vous au plug-in d'interface de ligne de commande de Container Registry.

  ```
  ibmcloud cr login
  ```
  {: pre}

2. Créez un espace de nom Container Registry.

  ```
  ibmcloud cr namespace-add <my_namespace>
  ```
  {: pre}

3. Générez, étiquetez et envoyez l'application en tant qu'image à votre espace de nom dans Container Registry. N'oubliez pas le point (.) à la fin de la commande.

  ```
  ibmcloud cr build -t registry.<region>.bluemix.net/<namespace>/<app-name>:<tag> .
  ```
  {: pre}

Bien ! Vous êtes presque prêt à déployer.

## Etape 3 : Configuration d'Ingress
{: kube-ingress}

Lors de la création du cluster, un équilibreur de charge d'application (ALB) Ingress privé et un public ont été automatiquement créés. Pour déployer votre application et profiter de votre contrôleur Ingress, créez un script de déploiement.
{: shortdesc}

1. Procurez-vous la valeur confidentielle créée dans l'espace de nom de votre cluster lorsque vous avez lié {{site.data.keyword.appid_short_notm}} à votre cluster. Remarque : ce n'est **pas** votre espace de nom Container Registry.

  ```
  kubectl get secrets --namespace=<namespace>
  ```
  {: pre}

  Exemple de sortie :

  ```
  NAME                       TYPE                                  DATA      AGE
  binding-appid1             Opaque                                1         1m
  bluemix-default-secret     kubernetes.io/dockercfg               1         1h
  default-token-kf97z        kubernetes.io/service-account-token   3         1h
  ```
  {: screen}

2. Utilisez l'exemple de fichier `yaml` suivant pour créer votre configuration Ingress. Pour de l'aide concernant le reste de votre déploiement, voir [Déploiement d'applications avec l'interface de ligne de commande](/docs/containers?topic=containers-app#app_cli).

  ```
  apiVersion: extensions/v1beta1
  kind: Ingress
  metadata:
    name: myingress
    annotations:
      ingress.bluemix.net/appid-auth: "bindSecret=<bind_secret> namespace=<namespace> requestType=<request_type> serviceName=<myservice> [idToken=false]"
  spec:
    tls:
    - hosts:
      - mydomain
      secretName: mytlssecret
    rules:
    - host: mydomain
      http:
        paths:
        - path: /
          backend:
            serviceName: myservice
            servicePort: 8080
  ```
  {: screen}

  <table>
    <tr>
      <th>Variable</th>
      <th>Description</th>
    </tr>
    <tr>
      <td><code>bindSecret</code></td>
      <td>Valeur confidentielle Kubernetes créée lors de la liaison de votre instance de service {{site.data.keyword.appid_short_notm}} à votre cluster.</td>
    </tr>
    <tr>
      <td><code>namespace</code></td>
      <td>Espace de nom dans lequel la valeur <code>bindSecret</code> a été créée. Si vous ne spécifiez pas d'espace de nom, la valeur est créée dans l'espace de nom <code>par défaut</code>.</td>
    </tr>
    <tr>
      <td><code>requestType</code></td>
      <td><p>Type de demande à envoyer à {{site.data.keyword.appid_short_notm}}. Les options incluent <code>web</code> et <code>api</code>. Si vous définissez le type de demande sur <code>web</code>, une demande Web qui contient un jeton d'accès {{site.data.keyword.appid_short_notm}} est validée. En cas d'échec de la validation du jeton, la demande Web est rejetée. Si la demande ne contient pas de jeton d'accès, elle est redirigée vers la page de connexion {{site.data.keyword.appid_short_notm}}. Pour que l'authentification Web {{site.data.keyword.appid_short_notm}} fonctionne, les cookies doivent être activés dans le navigateur de l'utilisateur.</p><p>Si vous définissez le type de demande sur <code>api</code>, une demande API qui contient un jeton d'accès {{site.data.keyword.appid_short_notm}} est validée. Si la demande ne contient pas de jeton d'accès, le message d'erreur <code>401: Unauthorized</code> est renvoyé à l'utilisateur.</p></td>
    </tr>
    <tr>
      <td><code>serviceName</code></td>
      <td><p>Obligatoire : nom du service Kubernetes que vous avez créé pour votre application. Si aucun nom de service n'est inclus, l'annotation est activée pour tous les services.</p> <p>L'utilisation de plusieurs types de demande dans le même cluster, configurez une instance {{site.data.keyword.appid_short_notm}} de manière à utiliser <code>web</code> et une autre pour utiliser <code>api</code>.</p></td>
    </tr>
    <tr>
      <td><code>idToken</code></td>
      <td>Facultatif : le client Liberty OIDC ne peut pas analyser simultanément le jeton d'accès et le jeton d'identité. Lorsque vous utilisez Liberty, définissez cette valeur sur <code>false</code> pour que le jeton d'identité ne soit pas envoyé au serveur Liberty.</td>
    </tr>
    <tr>
      <td><code>secretName</code></td>
      <td>Valeur confidentielle TLS associée à votre certificat TLS. Si votre certificat est hébergé dans IBM Cloud Certificate Manager, vous pouvez exécuter <code>ibmcloud ks alb-cert-deploy --secret-name <secret_name> --cluster <cluster_name_or_ID> --cert-crn <certificate_crn></code> pour le déployer dans votre cluster. Si vous n'avez pas de certificat, effectuez l'étape 3 de la section [Exposition d'applications avec Ingress](/docs/containers?topic=containers-ingress#ingress_expose_public).</td>
    </tr>
  </table>

3. Exécutez le fichier de configuration.

  ```
  kubectl apply -f <file-name>.yaml
  ```
  {: pre}

Bon travail !


## Etape 4 : Ajout de vos URL de redirection
{: #kube-add-redirect}

Une URL de redirection est l'URL du site sur lequel vous voulez qu'{{site.data.keyword.appid_short_notm}} envoie vos utilisateurs une fois authentifiés.
{: shortdesc}

1. Accédez à l'interface graphique {{site.data.keyword.cloud_notm}} et ouvrez votre tableau de bord {{site.data.keyword.appid_short_notm}}.

2. Dans **Fournisseurs d'identité > Gérer**, définissez sur **On** les fournisseurs que vous voulez utiliser. Si aucun fournisseur n'est activé, les utilisateurs reçoivent un jeton d'accès qui permet un accès anonyme à votre application.

3. Cliquez sur **Paramètres d'authentification**.

4. Cliquez sur le signe **+** dans la case **Ajouter des URL de redirection Web**.

  * Domaine personnalisé :

    Une URL enregistrée auprès d'un domaine personnalisé peut se présenter comme suit : `http://mydomain.net/myapp2path/appid_callback`. Si les applications à exposer se trouvent dans le même cluster mais dans des espaces de nom différents, vous pouvez utiliser un caractère générique pour désigner toutes les applications du cluster à la fois. Cette possibilité peut se révéler utile en phase de développement, mais vous devez faire attention si vous utilisez des caractères génériques en production. Par exemple : `https://custom_domain.net/*`

  * Sous-domaine Ingress :

    Si votre application est enregistrée auprès d'un sous-domaine IBM Ingress, votre URL de rappel peut se présenter comme suit : `https://mycluster.us-south.containers.appdomain.cloud/myapp1path/appid_callback`

{{site.data.keyword.appid_short_notm}} offre une fonction de déconnexion : si `/logout` est présent dans votre chemin {{site.data.keyword.appid_short_notm}}, les cookies sont supprimés et l'utilisateur est renvoyé sur la page de connexion. Pour utiliser cette fonction, ajoutez `/appid_logout` à votre domaine au format `https://mycluster.us-south.containers.appdomain.cloud/myapp1path/appid_logout` et incluez cet élément dans vos URL de redirection.
{: note}


Excellent travail ! Maintenant, vous pouvez vérifier que le déploiement a abouti en accédant à votre domaine personnalisé ou votre sous-domaine Ingress pour le tester.


## Etapes suivantes
{: #kube-next}

Maintenant que votre application s'exécute dans un cluster Kubernetes et qu'Ingress est configuré, vous pouvez tester :

* L'utilisation d'attributs personnalisés pour [définir des rôles](/docs/services/appid?topic=appid-tutorial-roles)
* La configuration de l'[authentification multi-facteur](/docs/services/appid?topic=appid-cd-mfa)
* La personnalisation du [widget de connexion](/docs/services/appid?topic=appid-login-widget)



