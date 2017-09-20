---

copyright:
  years: 2017
lastupdated: "2017-06-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Identitätsprovider konfigurieren
{: #setting-up-idp}

Sie können Facebook, Google, eine IBMid oder eine Kombination der drei Möglichkeiten konfigurieren, um eine Single Sign-on-Erfahrung einzurichten. Mithilfe eines Identitätsproviders können Benutzer für die Anmeldung Berechtigungsnachweise verwenden, die ihnen bereits bekannt sind.
{:shortdesc}


## Facebook-Authentifizierung konfigurieren
{: #facebook}

Konfigurieren Sie den {{site.data.keyword.appid_short}}-Service so, dass Facebook als Identitätsprovider verwendet wird.


### App-ID und geheimen Schlüssel von Facebook abrufen
{: #getting-facebook-appid}

Zur Verwendung von Facebook als Identitätsprovider in Ihren mobilen und Web-Apps müssen Sie die Website-Plattform Ihrer Facebook-Anwendung hinzufügen und sie konfigurieren.

1. Melden Sie sich bei Ihrem Konto auf der Site <a href="https://developers.facebook.com/docs/apps/register" target="_blank">Facebook for Developers<img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> an.
2. Notieren Sie sich die Facebook-App-ID und den geheimen Schlüssel. Diese Werte werden benötigt, um Ihr Webprojekt für die Authentifizierung in Ihrem Service-Dashboard zu konfigurieren. 
3. Fügen Sie die Webplattform hinzu und geben Sie die Site-URL ein.
4. Wählen Sie aus der Produktliste den Option **Facebook-Anmeldung** aus.
5. Geben Sie im Feld für gültige OAuth-Weiterleitungs-URLs die Endpunkt-URL für den Autorisierungsserver-Callback ein. Nachdem Sie Ihre Serviceinstanz konfiguriert haben, können Sie diesen Wert hinzufügen. 
6. Klicken Sie auf **Änderungen speichern**.

### {{site.data.keyword.appid_short_notm}} für die Facebook-Authentifizierung konfigurieren
{: #configuring-facebook-appid}

Nachdem Sie Ihre Facebook-App-ID und den geheimen Schlüssel erhalten haben und Ihre Facebook for Developers-App zur Bedienung von Web-Clients konfiguriert wurde, können Sie die Facebook-Authentifizierung in Ihrem Service-Dashboard bearbeiten.

1. Wählen Sie im Service-Dashboard in der Registerkarte **Verwalten** die Option **Facebook** aus und klicken Sie auf **Bearbeiten**.
2. Geben Sie die Facebook-App-ID und den geheimen Schlüssel ein, den Sie von der Facebook for Developers-Website erhalten haben.
3. Kopieren Sie den URI in das Feld zum **Weiterleitungs-URI für Facebook for Developers**. Fügen Sie den URI in das Feld **Gültige OAuth-Weiterleitungs-URIs** im Abschnitt **Facebook-Anmeldung** des Facebook Developers-Portals ein. 
4. Klicken Sie auf **Speichern**.
5. Optional: Geben Sie für Web-Apps die Weiterleitungs-URL in das Feld für die Weiterleitungs-URLs der Webanwendung ein. Dieser Wert wird vom Entwickler festgelegt und wird verwendet, um auf die Weiterleitungs-URL zuzugreifen, wenn der Berechtigungsprozess beendet ist.


## Google-Authentifizierung konfigurieren
{: #google}

Konfigurieren Sie den {{site.data.keyword.appid_short_notm}}-Service so, dass Google als Identitätsprovider verwendet wird.


### Client-ID und geheimen Schlüssel von Google abrufen
{: #google-client-id}

Um Google als Identitätsprovider zu verwenden, fordern Sie eine Google-Client-ID und einen geheimen Schlüssel an und erstellen Sie in Google Developer Console ein Projekt.

1. Öffnen Sie Ihre Google-Anwendung in der <a href="https://console.developers.google.com/apis/library" target="_blank">Google Developer Console <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>.
2. Fügen Sie die Google+-API hinzu.
3. Erstellen Sie Berechtigungsnachweise unter Verwendung von 'OAuth'. Wählen Sie im Feld **Anwendungstyp** die Option **Webanwendung** aus. Geben Sie in das Feld **Autorisierte Weiterleitungs-URIs** die Weiterleitungs-URI der {{site.data.keyword.appid_short_notm}} ein. Sie können den autorisierten Weiterleitungs-URI der {{site.data.keyword.appid_short_notm}} für die Google-Konfigurationsanzeige im Service-Dashboard anfordern. 
4. Notieren Sie die Google-Client-ID und den geheimen Schlüssel, und speichern Sie die Änderungen. 



### {{site.data.keyword.appid_short_notm}} für die Google-Authentifizierung konfigurieren
{: #google-client-appid}

Nachdem Sie Ihre Google-Client-ID und den geheimen Schlüssel erhalten haben und Google Developers Console zur Bedienung von Web-Clients konfiguriert wurde, können Sie die Google-Authentifizierung in Ihrem Service-Dashboard bearbeiten.

1. Wählen Sie im Service-Dashboard in der Registerkarte **Verwalten** die Option **Google** aus und klicken Sie auf **Bearbeiten**.
3. Geben Sie die Google-Client-ID und den geheimen Schlüssel ein, den Sie von Google Developers Console erhalten haben.
4. Kopieren Sie die URI in das Feld zum **Weiterleitungs-URI für Google for Developers**. Fügen Sie den URI in das Feld für **Autorisierte Weiterleitungs-URIs** unter **Einschränkungen** im Abschnitt **Client-ID für Webanwendungen** des Google Developers-Portals. 
5. Klicken Sie auf **Speichern**.
6. Optional: Geben Sie für Web-Apps den Weiterleitungs-URI in das Feld **Weiterleitungs-URIs der Webanwendung** ein. Dieser Wert wird vom Entwickler festgelegt und wird verwendet, um auf die Weiterleitungs-URI zuzugreifen, wenn der Berechtigungsprozess beendet ist.


## IBMid-Authentifizierung konfigurieren

Wenn Sie eine IBMid als Identitätsprovider verwenden möchten, verwenden Sie <a href="https://ibm.ent.box.com/notes/78040808400?v=IBMid-Federation-Guide" target="_blank">IBMid Enterprise Federation Adoption Guide<img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>. Falls Sie bereits über eine BlueID-App verfügen, rufen Sie eine Client-ID und einen geheimen Schlüssel für die BlueID ab. 


### Client-ID und geheimen Schlüssel von IBMid abrufen

Gehen Sie wie folgt vor, um eine Client-ID und einen geheimen Schlüssel abzurufen. 

1. Melden Sie sich beim <a href="https://w3.innovate.ibm.com/tools/sso/home.html" target="_blank">Bereitsteller für den SSO-Self-Service<img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> an Ihrem BlueID-Konto an. 
2. Registrieren Sie eine BlueID-App. Stellen Sie sicher, dass für den Identitätsprovider **Vorproduktion** oder **Produktion** ausgewählt ist. 
3. Geben Sie unter **Clientdetails** die Weiterleitungs-URL von App ID ein. Sie können den autorisierten Weiterleitungs-URI für die IBMid-Konfigurationsanzeige im Service-Dashboard anfordern. 
4. Stellen Sie sicher, dass **Autorisierungscode** ausgewählt ist. 
5. Notieren Sie die Client-ID und den geheimen Schlüssel für die BlueID sowie den Typ des Kontoidentitätsproviders. Klicken Sie auf **Fortfahren & Beenden**. 

### App ID für IBMid-Authentifizierung konfigurieren

Sobald Sie über eine Client-ID und einen geheimen Schlüssel für die BlueID verfügen und Ihre BlueID-App mit dem richtigen Weiterleitungs-URI konfiguriert ist, können Sie den Abschnitt zur BlueID-Authentifizierung des Service-Dashboards bearbeiten. 

1. Wählen Sie im Service-Dashboard in der Registerkarte **Verwalten** die Auswahlmöglichkeit **IBMid** aus und klicken Sie auf **Bearbeiten**. 
2. Geben Sie die Client-ID und den geheimen Schlüssel für die BlueID ein. 
3. Kopieren Sie den URI, der im Feld **Weiterleitungs-URI für die IBMid für Entwickler** angegeben ist, und fügen Sie ihn in das Feld **Weiterleitungs-URIs** ein. 
4. Wählen Sie **Vorproduktion** oder **Produktion** für den Identitätsprovider aus und klicken Sie auf die Schaltfläche **Speichern**. 
5. Optional: Geben Sie für Web-Apps den Weiterleitungs-URI in das Feld **Weiterleitungs-URIs der Webanwendung** ein. Dieser Wert wird vom Entwickler festgelegt und wird verwendet, um nach der Autorisierung auf den Weiterleitungs-URI zuzugreifen. 
