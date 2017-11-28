---

copyright:
  years: 2017
lastupdated: "2017-11-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Identitätsprovider konfigurieren
{: #setting-up-idp}

Identitätsprovider bieten eine zusätzliche Authentifizierungsstufe für Ihre mobilen Apps und Web-Apps. Mit {{site.data.keyword.appid_full}} können Sie einen oder mehrere Identitätsprovider konfigurieren und so Single Sign-on-Funktionalität für Ihre App einrichten.
{: shortdesc}

Die folgenden Identitätsprovider können verwendet werden:

<dl>
  <dt> Facebook </dt>
    <dd> Benutzer melden sich bei Ihrer App an, indem sie dasselbe Kennwort und dieselbe E-Mail-Adresse wie für die Anmeldung bei ihrem Facebook-Konto verwenden. </dd>
  <dt> Google </dt>
    <dd> Benutzer melden sich bei Ihrer App an, indem sie dasselbe Kennwort und dieselbe E-Mail-Adresse wie für die Anmeldung bei ihren Google-Konten verwenden. </dd>
</dl>


</br>
</br>

## Standardkonfiguration
{: #default}

{{site.data.keyword.appid_short_notm}} stellt eine Standardkonfiguration bereit, die Sie bei der ersten Einrichtung der Identitätsprovider unterstützt.
{: shortdesc}

Die Standardberechtigungsnachweise sind für Facebook und Google eingerichtet. Der Grenzwert beträgt 100 Verwendungen der Berechtigungsnachweise pro Instanz und Tag. Da es sich um IBM Berechtigungsnachweise handelt, dürfen sie in den Anwendungen nur im Entwicklungsmodus verwendet werden. Bevor Sie die App veröffentlichen, [aktualisieren Sie die Konfiguration so, dass Ihre eigenen Berechtigungsnachweise verwendet werden](/docs/services/appid/identity-providers.html).


</br>

## Konfiguration für Facebook
{: #facebook}

Sie können den {{site.data.keyword.appid_short}}-Service so konfigurieren, dass Facebook als Identitätsprovider verwendet wird.
{: shortdesc}

### App-ID und geheimen Schlüssel von Facebook abrufen

Zur Verwendung von Facebook als Identitätsprovider müssen Sie die Website-Plattform Ihrer Facebook-Anwendung hinzufügen und sie konfigurieren.

1. Melden Sie sich bei Ihrem Konto auf der Site <a href="https://developers.facebook.com/docs/apps/register" target="_blank">Facebook for Developers<img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> an.
2. Notieren Sie sich die Facebook-App-ID und den geheimen Schlüssel. Diese Werte werden benötigt, um Ihr Webprojekt für die Authentifizierung in Ihrem Service-Dashboard zu konfigurieren.
3. Fügen Sie die Webplattform hinzu und geben Sie die Site-URL ein.
4. Wählen Sie aus der Produktliste den Option **Facebook-Anmeldung** aus.
5. Geben Sie im Feld für gültige OAuth-Weiterleitungs-URLs die Endpunkt-URL für den Autorisierungsserver-Callback ein. Nachdem Sie Ihre Serviceinstanz konfiguriert haben, können Sie diesen Wert hinzufügen.
6. Klicken Sie auf **Änderungen speichern**.


### {{site.data.keyword.appid_short_notm}} für die Facebook-Authentifizierung konfigurieren

Nachdem Sie Ihre Facebook-App-ID und den geheimen Schlüssel erhalten haben und Ihre Facebook for Developers-App zur Bedienung von Web-Clients konfiguriert wurde, können Sie die Facebook-Authentifizierung in Ihrem Service-Dashboard bearbeiten.

1. Wählen Sie im Service-Dashboard in der Registerkarte **Verwalten** die Option **Facebook** aus und klicken Sie auf **Bearbeiten**.
2. Geben Sie die Facebook-App-ID und den geheimen Schlüssel ein, den Sie von der Facebook for Developers-Website erhalten haben.
3. Kopieren Sie den URI in das Feld zum **Weiterleitungs-URI für Facebook for Developers**. Fügen Sie den URI in das Feld **Gültige OAuth-Weiterleitungs-URIs** im Abschnitt **Facebook-Anmeldung** des Facebook Developers-Portals ein.
4. Klicken Sie auf **Speichern**.
5. Optional: Geben Sie für Web-Apps die Weiterleitungs-URL in das Feld für die Weiterleitungs-URLs der Webanwendung ein. Dieser Wert wird vom Entwickler festgelegt und wird verwendet, um auf die Weiterleitungs-URL zuzugreifen, wenn der Berechtigungsprozess beendet ist.


</br>

## Konfiguration für Google
{: #google}

Sie können den {{site.data.keyword.appid_short}}-Service so konfigurieren, dass Google als Identitätsprovider verwendet wird.
{: shortdesc}

### Client-ID und geheimen Schlüssel von Google abrufen

Erstellen Sie ein Projekt in der <a href="https://developers.google.com/" target="_blank">Google Developers-Konsole <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>, konfigurieren Sie das Projekt für Unterstützung von Web-Clients und rufen Sie eine Client-ID und einen  geheimen Clientschlüssel ab.

1. Erstellen Sie ein Projekt.
2. Fügen Sie die API von Google+ zum Google-Projekt hinzu.
3. Fügen Sie Berechtigungsnachweise zur API von Google+ hinzu.
    1. Wählen Sie die API von Google+ API als API-Typ aus.
    2. Wählen Sie **Web-Browser** als Position für das Aufrufen der API aus.
    3. Wählen Sie **Benutzerdaten** aus.
    4. Füllen Sie die erforderlichen Felder für die Erstellung einer Client-ID aus. Zu diesem Zeitpunkt wird auch ein geheimer Schlüssel erstellt.
4. Notieren Sie sich die Google-Client-ID und den geheimen Schlüssel. Wählen Sie auf der Registerkarte mit den Berechtigungsnachweisen die ID aus, die Sie erstellt haben, um den geheimen Schlüssel und die Client-ID abzurufen.

### {{site.data.keyword.appid_short}} für die Google-Authentifizierung konfigurieren

Nachdem Sie das Google-Projekt konfiguriert und die Client-ID sowie den geheimen Clientschlüssel abgerufen haben, können Sie das Service-Dashboard für die Google-Authentifizierung bearbeiten.

1. Wählen Sie im Service-Dashboard in der Registerkarte **Verwalten** die Option **Google** aus und klicken Sie auf **Bearbeiten**.
2. Geben Sie die Client-ID und den geheimen Clientschlüssel ein, die Sie von der Google Developers-Konsole abgerufen haben.
3. Autorisieren Sie die {{site.data.keyword.appid_short}}-URL.
    1. Kopieren Sie die **Weiterleitungs-URL für die Google Developer-Konsole** aus den Google-Identitätsproviderdetails.
    2. Wählen Sie auf der Registerkarte mit den Berechtigungsnachweisen des Google-Projekts die Client-ID aus, die Sie für diese Integration erstellt haben.
    3. Fügen Sie die URL aus {{site.data.keyword.appid_short}} in das Feld **Autorisierte Weiterleitungs-URIs** ein und klicken Sie auf **Speichern**.
4. Klicken Sie auf **Speichern**, um die Google-Konfiguration in {{site.data.keyword.appid_short}} zu aktualisieren.
5. Optional: Geben Sie für Web-Apps eine Weiterleitungs-URL auf der Registerkarte **Verwalten** ein. Nach dem Abschluss des Berechtigungsprozesses wird ein Benutzer an diese URL weitergeleitet.
