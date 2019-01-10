---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}

# Traitement général des incidents
{: #troubleshooting}

Si vous rencontrez des problèmes lorsque vous utilisez {{site.data.keyword.appid_full}}, les techniques suivantes peuvent vous aider à les résoudre et à obtenir de l'aide.
{: shortdesc}

## Aide et assistance
{: #gettinghelp}

Vous pouvez obtenir de l'aide en recherchant des informations précises ou en posant des questions via un forum. Vous pouvez aussi ouvrir un ticket de demande de service. Lorsque vous utilisez les forums pour poser une question, prenez soin d'étiqueter cette dernière de façon à ce qu'elle soit vue par les équipes de développement {{site.data.keyword.Bluemix_notm}}.
  * Posez toute question d'ordre technique sur {{site.data.keyword.appid_short_notm}} sur le forum <a href="https://stackoverflow.com/search?q=ibm-appid" target="_blank">Stack Overflow <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> en indiquant balise "ibm-appid".
  * Posez toute question relative au service et aux instructions de mise en route sur le forum <a href="https://developer.ibm.com/answers/topics/appid/" target="_blank">dW Answers <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> Incluez la balise `appid`.

Pour plus d'informations sur l'obtention de support, voir [Comment obtenir l'aide dont j'ai besoin ?](/docs/get-support/howtogetsupport.html#getting-customer-support).

</br>

## Une adresse URL personnalisée est rejetée
{: #ts-custom-url}


{: tsSymptoms}
Lorsque vous entrez une URL de redirection Web qui utilise un schéma URL personnalisé, elle est rejetée par la console {{site.data.keyword.appid_short_notm}}.

{: tsCauses}
Il est possible que votre URL soit rejetée pour les raisons suivantes :

* L'URL ne suit pas un schéma `http` ou `https`
* L'URL se termine par `://`
* Votre URL comporte une erreur typographique

Les limitations sont en place pour des raisons de sécurité.

{: tsResolve}
Pour résoudre le problème, vérifiez que l'URL est correcte. Si votre URL ne répond pas aux exigences, vous pouvez créer un noeud final HTTPS dans votre application pour rediriger le code d'octroi reçu vers votre URL personnalisée. Indiquez le noeud final créé comme votre URL de redirection dans la console {{site.data.keyword.appid_short_notm}}.

</br>
