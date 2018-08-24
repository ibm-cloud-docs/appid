---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-03"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:pre: .pre}
{:tip: .tip}
{:screen: .screen}

# Wissenswertes zu Benutzerprofilen
{: #user-profile}

Mit {{site.data.keyword.appid_full}} können Sie für Ihre App individuelle Benutzererfahrungen gestalten, indem Sie auf Informationen zu Ihren Benutzern zugreifen, die von {{site.data.keyword.appid_short_notm}} gespeichert werden.
{: shortdesc}

## Zentrale Konzepte
{: #key-concepts}

**Was ist ein Benutzerprofil?**

Bei einem Benutzerprofil handelt es sich um eine Gruppe von Attributen, die von {{site.data.keyword.appid_short_notm}} gespeichert werden. Bei den Attributen handelt es sich um Angaben über die Benutzer, die mit Ihrer App interagieren. Es können zwei Typen von Attributen abgerufen werden: `vordefinierte` und `angepasste` Attribute. 

**Was sind vordefinierte Attribute?**

Vordefinierte Attribute werden vom Identitätsprovider zurückgegeben, wenn ein Benutzer sich bei Ihrer App anmeldet. Die Attribute umfassen den zugehörigen Benutzernamen sowie Alter und Geschlecht. 

**Was sind angepasste Attribute?**

Angepasste Attribute zu Ihren Benutzern werden im Laufe der Interaktion mit Ihrer App erfasst. Dabei kann es sich um die verwendete Schriftgröße oder Elemente handeln, die vom Benutzer in einen Warenkorb platziert wurden. Angepasste Attribute können bearbeitet werden. 

## Auf Benutzerattribute zugreifen
{: #access}

Sie können auf unterschiedliche Weise auf Benutzerprofilinformationen zugreifen. Nach einer erfolgreichen Benutzerauthentifizierung empfängt Ihre App Zugriffs- und Identitätstoken. Das Identitätstoken enthält eine normalisierte Untergruppe von Benutzerattributen, die von einem Identitätsprovider zurückgegeben wurden. Eine vollständige Liste der Benutzerattribute können Sie über den OIDC-Endpunkt `/userinfo` abrufen. Zur Verwaltung von angepassten Attributen eignet sich die `REST-API`. Die Endpunkte für Benutzerinformationen und für angepasste Attribute werden über das Zugriffstoken geschützt, das von {{site.data.keyword.appid_short_notm}} zum Ende des Authentifizierungsprozesses generiert wird. 



![{{site.data.keyword.appid_short_notm}}-Benutzerprofilarchitektur](/images/user-profile1.png)

Abbildung. Datenfluss der Benutzerprofilinformationen

Verwenden Sie zum Anzeigen von angepassten Attributen die <a href="https://appid-profiles.ng.bluemix.net/swagger-ui/index.html#/Attributes" target="_blank">REST-API <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>.

</br>
</br>
