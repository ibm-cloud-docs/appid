---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-04"

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


# Configuration de Cloud Directory
{: #cloud-directory}

Avec {{site.data.keyword.appid_full}}, les utilisateurs peuvent s'inscrire et se connecter à vos applications mobiles et Web à l'aide d'une adresse électronique ou d'un nom d'utilisateur et d'un mot de passe. Un répertoire cloud est un registre d'utilisateurs géré dans le cloud. Lorsqu'un utilisateur s'inscrit à votre application, il est ajouté à votre répertoire d'utilisateurs. Avec cette fonction, l'utilisateur final a la liberté de gérer son propre compte au sein de votre application.
{: shortdesc}


## Gestion des paramètres de répertoire
{: #cd-settings}

Vous pouvez configurer les notifications et le niveau de contrôle de votre application par les utilisateurs. La configuration de Cloud Directory peut s'effectuer rapidement, comme illustré dans l'image ci-dessous. Ces paramètres peuvent être mis à jour à tout moment à partir du tableau de bord du service et sont reportés dans votre application sans nécessiter de modification du code.
{: shortdesc}


![Configuration du répertoire cloud](images/cloud-directory.png)
Figure. Procédure de configuration de Cloud Directory


1. Accédez à l'onglet **Gérer les authentifications** du tableau de bord {{site.data.keyword.appid_short_notm}}, vérifiez que Cloud Directory est défini sur **Actif**.

2. Dans l'onglet **Cloud Directory > Paramètres**, définissez **Permettre aux utilisateurs de s'inscrire et de se connecter** sur **Adresse électronique et mot de passe** ou sur **Nom d'utilisateur et mot de passe**. Les utilisateurs peuvent se connecter avec une adresse électronique qu'ils détiennent déjà ou créer un nom d'utilisateur à utiliser lorsqu'ils interagissent avec votre application.

  Vous pouvez basculer entre les options avant l'ajout des utilisateurs à votre répertoire. Une fois le premier utilisateur ajouté, les utilisateurs suivants doivent utiliser la même configuration.
  {: note}

2. Choisissez si vous souhaitez que vos utilisateurs créent un nom d'utilisateur ou utilisent leur adresse électronique lorsqu'ils se connectent. Les deux options nécessitent un mot de passe. Une fois les utilisateurs ajoutés à votre répertoire, vous ne pouvez plus changer d'option.

3. Cliquez sur **Editer** sur la ligne des critères de mot de passe pour spécifier toutes les exigences que vous souhaitez mettre en place. Les critères de mot de passe sont fournis sous forme d'expression régulière. Pour obtenir de l'aide sur la détermination de la force ou pour consulter des exemples courants, voir [Gestion de la force du mot de passe](/docs/services/appid?topic=appid-cd-strength#cd-strength). Cliquez sur **Sauvegarder** pour mettre vos exigences en application.

4. Définissez **Permettre aux utilisateurs de s'inscrire à votre application** sur **Oui**. Vous pouvez toujours ajouter des utilisateurs via la console si l'option est définie sur **Non**. Il est toutefois plus courant d'ajouter des utilisateurs via la console uniquement à des fins de développement.

5. Définissez **Permettre aux utilisateurs de gérer leur compte à partir de votre application** sur **Oui** si vous souhaitez que vos utilisateurs puissent réinitialiser leur mot de passe, le changer ou réinitialiser leurs détails. Si vous voulez limiter la possibilité de libre-service pour vos utilisateurs, définissez la valeur sur **Non**.

6. Configurez vos paramètres de courrier électronique. Cliquez sur **Editer** sur la ligne **Détails sur l'expéditeur** pour mettre à jour vos paramètres de courrier électronique. Les paramètres de courrier électronique s'appliquent à toutes les communications envoyées via {{site.data.keyword.appid_short_notm}}.

    1. Indiquez l'adresse électronique d'envoi du message électronique. Si vous choisissez de modifier la valeur par défaut, le courrier électronique peut être envoyé dans le dossier Courrier indésirable de l'utilisateur.

    2. Ajoutez un nom pour l'émetteur.

    3. Entrez une adresse électronique qui peut être utilisée pour envoyer une réponse.

    4. Cliquez sur **Sauvegarder**.
