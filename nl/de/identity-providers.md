---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-09"

keywords: Authentication, authorization, identity, app security, secure, custom, proprietary, social, facebook, google, 

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

# Social Media
{: #social}

Mit {{site.data.keyword.appid_full}} können Sie Social-Identity-Provider konfigurieren und so eine Single-Sign-on-Funktionalität für Ihre App einrichten. Wenn sich ein Benutzer mit seinen Social-Media-Profilen anmelden kann, muss er sich nicht mehr mehrere verschiedene Kennwörter für verschiedene Anwendungen merken.
{: shortdesc}


## Standardkonfiguration
{: #social-default}

{{site.data.keyword.appid_short_notm}} stellt eine Standardkonfiguration bereit, die Sie bei der schnellen Ausführung des Service unterstützt.
{: shortdesc}

Die Daten werden verwendet, wenn Sie die zulässigen Verwendungen des Service beauftragen. Durch die Verwendung des Service stimmen Sie der Erfassung und Verwendung von Informationen gemäß der beschriebenen [Datenschutzrichtlinie](/docs/services/appid?topic=appid-privacy-policy) zu.
{: important}


Wenn Sie {{site.data.keyword.appid_short_notm}} konfigurieren, werden Facebook, Google und Cloud Directory automatisch als Identitätsprovider aktiviert. Sie können die Konfiguration jederzeit ändern. Für Facebook und Google stehen Standardberechtigungsnachweise zur Verfügung, um zu testen, ob der Service benutzt werden soll, sollten jedoch die IBM Berechtigungsnachweise benutzt werden. Bevor Sie die App veröffentlichen, aktualisieren Sie die Konfiguration so, dass Ihre eigenen Berechtigungsnachweise verwendet werden.

Mit den Standardberechtigungsnachweisen besteht eine Begrenzung von 100 Authentifizierungen pro Tag.
{: note}


## Konfiguration für Facebook
{: #facebook}

Sie können den {{site.data.keyword.appid_short}}-Service so konfigurieren, dass Facebook als Identitätsprovider verwendet wird.
{: shortdesc}

### App-ID und geheimen Schlüssel von Facebook abrufen
{: #facebook-appid-secret}

Zur Verwendung von Facebook als Identitätsprovider müssen Sie die Website-Plattform Ihrer Facebook-Anwendung hinzufügen und sie konfigurieren.

1. Melden Sie sich bei Ihrem Konto auf der Website <a href="https://developers.facebook.com/docs/apps#register" target="_blank">Facebook for Developers<img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> an.
2. Notieren Sie sich die Facebook-App-ID und den geheimen Schlüssel. Diese Werte werden benötigt, um Ihr Webprojekt für die Authentifizierung in Ihrem Service-Dashboard zu konfigurieren.
3. Fügen Sie die Webplattform hinzu und geben Sie die Site-URL ein.
4. Wählen Sie aus der Produktliste den Option **Facebook-Registrierung** aus.
5. Geben Sie im Feld **Gültige OAuth-Weiterleitungs-URLs** die URL für den Callback-Endpunkt des Autorisierungsservers ein.
6. Klicken Sie auf **Änderungen speichern**.


### {{site.data.keyword.appid_short_notm}} für die Facebook-Authentifizierung konfigurieren
{: #facebook-configure}

Nachdem Sie Ihre Facebook-App-ID und den geheimen Schlüssel erhalten haben und Ihre Facebook for Developers-App zur Bedienung von Web-Clients konfiguriert wurde, können Sie die Facebook-Authentifizierung in Ihrem Service-Dashboard bearbeiten.

1. Wählen Sie im Service-Dashboard in der Registerkarte **Verwalten** die Option **Facebook** aus und klicken Sie auf **Bearbeiten**.
2. Geben Sie die Facebook-App-ID und den geheimen Schlüssel ein, den Sie von der Facebook for Developers-Website erhalten haben.
3. Kopieren Sie den URI in das Feld zum **Weiterleitungs-URI für Facebook for Developers**. Fügen Sie den URI in das Feld **Gültige OAuth-Weiterleitungs-URIs** im Abschnitt **Facebook-Registrierung** des Facebook Developers-Portals ein.
4. Klicken Sie auf **Speichern**.
5. Optional: Geben Sie für Web-Apps die Weiterleitungs-URL in das Feld für die Weiterleitungs-URLs der Webanwendung ein. Dieser Wert wird vom Entwickler festgelegt und wird verwendet, um auf die Weiterleitungs-URL zuzugreifen, wenn der Autorisierungsprozess beendet ist. Die URL muss das Schema `http` oder `https` enthalten. Verwenden Sie das Schema `https`, wenn eine höhere Sicherheitsstufe gewünscht ist.


## Konfiguration für Google
{: #google}

Sie können den {{site.data.keyword.appid_short}}-Service so konfigurieren, dass Google als Identitätsprovider verwendet wird.
{: shortdesc}

### Client-ID und geheimen Schlüssel abrufen
{: #google-clientid-secret}

Erstellen Sie ein Projekt in der <a href="https://developers.google.com/" target="_blank">Google Developers-Konsole <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>, konfigurieren Sie das Projekt für Unterstützung von Web-Clients und rufen Sie eine Client-ID und einen geheimen Clientschlüssel ab.

1. Erstellen Sie ein Projekt.
2. Fügen Sie die API von Google+ zum Google-Projekt hinzu.
3. Fügen Sie Berechtigungsnachweise zur API von Google+ hinzu.
    1. Wählen Sie die API von Google+ API als API-Typ aus.
    2. Wählen Sie **Web-Browser** als Position für das Aufrufen der API aus.
    3. Wählen Sie **Benutzerdaten** aus.
    4. Füllen Sie die erforderlichen Felder aus, um eine Client-ID zu erstellen. Zu diesem Zeitpunkt wird auch ein geheimer Schlüssel erstellt.
4. Notieren Sie sich die Google-Client-ID und den geheimen Schlüssel. Wählen Sie auf der Registerkarte mit den Berechtigungsnachweisen die ID aus, die Sie erstellt haben, um den geheimen Schlüssel und die Client-ID abzurufen.

### {{site.data.keyword.appid_short}} für die Google-Authentifizierung konfigurieren
{: #google-configure}

Nachdem Sie das Google-Projekt konfiguriert und die Client-ID sowie den geheimen Schlüssel abgerufen haben, können Sie das Service-Dashboard für die Google-Authentifizierung bearbeiten.

1. Wählen Sie im Service-Dashboard auf der Seite **Verwalten** die Option **Google** aus und klicken Sie auf **Bearbeiten**.
2. Geben Sie die Client-ID und den geheimen Clientschlüssel ein, die Sie von der Google Developers-Konsole abgerufen haben.
3. Autorisieren Sie die {{site.data.keyword.appid_short}}-URL.
    1. Kopieren Sie die **Weiterleitungs-URL für die Google Developer-Konsole** aus den Google-Identitätsproviderdetails.
    2. Wählen Sie auf der Seite mit den Berechtigungsnachweisen des Google-Projekts die Client-ID aus, die Sie für diese Integration erstellt haben.
    3. Fügen Sie die URL aus {{site.data.keyword.appid_short}} in das Feld **Autorisierte Weiterleitungs-URIs** ein und klicken Sie auf **Speichern**.
4. Klicken Sie auf **Speichern**, um die Google-Konfiguration in {{site.data.keyword.appid_short}} zu aktualisieren.
5. Geben Sie für die Web-Apps eine Weiterleitungs-URL auf der Registerkarte **Verwalten** ein. Nach dem Abschluss des Autorisierungsprozesses wird ein Benutzer an diese URL weitergeleitet. Die URL muss das Schema `http` oder `https` enthalten. Verwenden Sie das Schema `https`, wenn eine höhere Sicherheitsstufe gewünscht ist.






