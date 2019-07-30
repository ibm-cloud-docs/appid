---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-11"

keywords: Authentication, authorization, identity, app security, secure, development, nodejs, frontend, web apps, 

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


# Web: Node.js
{: #web-node}

Mit {{site.data.keyword.appid_short_notm}} können Sie Ihre Node.js-Front-End-Webanwendungen auf einfache Weise schützen. Mit diesem Handbuch können Sie in weniger als 20 Minuten einen einfachen Authentifizierungsablauf erstellen, der sofort betriebsbereit ist.
{: shortdesc}

Das folgende Diagramm zeigt den Ablauf für den Autorisierungscode mit OAuth 2.0

![Berechtigungsablauf für Node.js-Anwendung](images/node_web.png)

1. Ein Benutzer versucht, Zugriff auf Ihre geschützte Webanwendung zu erhalten, ist jedoch nicht autorisiert.
2. Ihre Anwendung leitet den Benutzer an {{site.data.keyword.appid_short_notm}} weiter.
3. {{site.data.keyword.appid_short_notm}} zeigt eine Anmeldeanzeige, die der Benutzer für die Authentifizierung verwenden kann.
4. Benutzer geben dazu ihre Berechtigungsnachweise wie Benutzername und Kennwort ein. Die App-ID überprüft die Berechtigungsnachweise. 
5. {{site.data.keyword.appid_short_notm}} leitet den Benutzer mit einem Erteilungscode an Ihre Anwendung weiter. 
6. Durch die Verwendung des Erteilungscodes stellt Ihre Anwendung eine Anfrage bei {{site.data.keyword.appid_short_notm}}, um zu gewährleisten, dass der Benutzer überprüft wurde. Weitere Informationen zum Abrufen von Zugriffstokens finden Sie unter [Token abrufen](/docs/services/appid?topic=appid-obtain-tokens).
7. {{site.data.keyword.appid_short_notm}} gibt Zugriffs- und Identitätstoken für die überprüften Benutzer zurück. 
8. Der Benutzer erhält nun Zugriff auf Ihre Anwendung.



## Schulungsvideo
{: #web-node-video}

Sehen Sie sich das folgende Video an, um zu erfahren, wie Sie {{site.data.keyword.appid_short_notm}} verwenden können, um eine einfache Node.js-Webanwendung zu schützen. Alle Informationen aus dem Video können Sie auch in schriftlicher Form auf dieser Seite finden. 

<iframe class="embed-responsive-item" id="appid-web-node" title="Informationen zu Node-js-Anwendungen von {{site.data.keyword.appid_short_notm}}" type="text/html" width="640" height="390" src="//www.youtube.com/embed/6roa1ZOvwtw?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>

Sie haben keine App, mit der Sie den Ablauf ausprobieren können? Kein Problem! {{site.data.keyword.appid_short_notm}} stellt eine [einfache Node.js-Beispielapp](https://github.com/ibm-cloud-security/appid-video-tutorials/tree/master/02a-simple-node-web-app){: external} zur Verfügung.

 

## Vorbereitungen
{: #web-node-before}

Bevor Sie {{site.data.keyword.appid_short_notm}} in Ihren Node.js-Webanwendungen verwenden können, müssen Sie über die folgenden Voraussetzungen verfügen.
{: shortdesc}

* Eine Instanz des [{{site.data.keyword.appid_short_notm}}-Service](https://cloud.ibm.com/catalog/services/app-id){: external}
* [IBM Cloud-CLI](/docs/cli?topic=cloud-cli-getting-started)
* [NPM Version 4+](https://www.npmjs.com/get-npm){: external}
* [Node Version 6+](https://nodejs.org/en/download/){: external}


## Schritt 1: Ihre Weiterleitungs-URI registrieren
{: #node-web-redirect-uri}

Ein Weiterleitungs-URI ist der Callback-Endpunkt Ihrer App. Während des Anmeldeablaufs validiert {{site.data.keyword.appid_short_notm}} die URIs, bevor Clients am Autorisierungsworkflow teilnehmen können. Dies trägt dazu bei, Phishing-Attacken und Codelecks zu vermeiden. Durch die Registrierung des URI wird {{site.data.keyword.appid_short_notm}} darüber informiert, dass der URI vertrauenswürdig ist und dass Ihre Benutzer ohne Risiko zu diesem URI weitergeleitet werden können.
{: shortdesc}

1. Klicken Sie auf **Authentifizierungen verwalten > Authentifizierungseinstellungen**.

2. Geben Sie im Feld **Webweiterleitungs-URI hinzufügen** den gewünschten URI ein. Jeder URI muss mit `http://` oder mit `https://` beginnen und muss den vollständigen Pfad einschließlich aller Abfrageparameter umfassen, damit die Weiterleitung erfolgreich ausgeführt werden kann.

3. Klicken Sie auf das Plussymbol (**+**) im Feld **Webweiterleitungs-URI hinzufügen**.

4. Wiederholen Sie die Schritte 1 bis 3, bis alle möglichen URIs zu Ihrer Liste hinzugefügt wurden.



## Schritt 2: Ihre Berechtigungsnachweise abrufen
{: #node-web-credentials}

Sie können Ihre Berechtigungsnachweise mithilfe einer der folgenden Methoden abrufen.
{: shortdesc}

  * Navigieren Sie zur Registerkarte **Anwendungen** des {{site.data.keyword.appid_short_notm}}-Dashboards. Wenn Sie noch nicht über eine Anwendung verfügen, dann können Sie auf **Anwendung hinzufügen** klicken, um eine neue Anwendung zu erstellen.

  * Erstellen Sie eine POST-Anforderung an den Endpunkt [`/management/v4/{tenantId}/applications`](https://us-south.appid.cloud.ibm.com/swagger-ui/#!/Applications/registerApplication).

    Anforderungsformat:
    ```javascript
    curl -X POST \  https://us-south.appid.cloud.ibm.com/management/v4/39a37f57-a227-4bfe-a044-93b6e6060b61/applications/ \
    -H 'Content-Type: application/json' \
    -H 'Authorization: Bearer IAM_TOKEN' \
    -d '{"name": "ApplicationName"}'
    ```
    {: codeblock}

    Beispielantwort:
    ```javascript
    {
      "clientId": "xxxxx-34a4-4c5e-b34d-d12cc811c86d",
      "tenantId": "xxxxx-9b1f-433e-9d46-0a5521f2b1c4",
      "secret": "ZDk5YWZkYmYt*******",
      "name": "app1",
      "oAuthServerUrl": "https://us-south.appid.cloud.ibm.com/oauth/v4/xxxxx-9b1f-433e-9d46-0a5521f2b1c4",
      "profilesUrl": "https://us-south.appid.cloud.ibm.com",
      "discoveryEndpoint": "https://us-south.appid.cloud.ibm.com/oauth/v4/xxxxxx-9b1f-433e-9d46-0a5521f2b1c4/.well-known/openid-configuration"
    }
    ```
    {: screen}



## Schritt 3: Das SDK initialisieren
{: #web-node-install}

Die einfachste Möglichkeit mit {{site.data.keyword.appid_short_notm}} zu arbeiten, besteht in der Nutzung des Node.JS-SDK.
{: shortdesc}


1. Wechseln Sie mithilfe der Befehlszeile in das Verzeichnis, das Ihre Node.js-Anwendung enthält. 

2. Installieren Sie die folgenden Voraussetzungen. 

    ```javascript
    npm install --save express express-session passport
    ```
    {: codeblock}

3. Installieren Sie den {{site.data.keyword.appid_short_notm}}-Service.

    ```javascript
    npm install --save ibmcloud-appid
    ```
    {: codeblock}

4. Fügen Sie die folgenden Anforderungen zu Ihrer Datei `server.js` hinzu. 

    ```javascript
    const express = require('express'); 								// https://www.npmjs.com/package/express
    const session = require('express-session');							// https://www.npmjs.com/package/express-session
    const passport = require('passport');								// https://www.npmjs.com/package/passport
    const WebAppStrategy = require('ibmcloud-appid').WebAppStrategy;	// https://www.npmjs.com/package/ibmcloud-appid
    ```
    {: shortdesc}

5. Konfigurieren Sie Ihre Anwendung für die Verwendung der Middleware des Typs 'express-session', indem Sie die Berechtigungsnachweise verwenden, die Sie in Schritt 1 angefordert haben. Sie haben ausgewählt, dass Ihre Weiterleitungs-URI auf eine der folgenden Weisen formatiert wird. Manuell oder mithilfe einer neuen `WebAppStrategy({redirectUri: "...."})` oder durch Festlegen des Werts als Umgebungsvariable, wie dies im Beispielcode dargestellt wird. 

    ```javascript
    const app = express();
    app.use(session({
        secret: '123456',
        resave: true,
        saveUninitialized: true
    }));
    app.use(passport.initialize());
    app.use(passport.session());
    passport.serializeUser((user, cb) => cb(null, user));
    passport.deserializeUser((user, cb) => cb(null, user));
    passport.use(new WebAppStrategy({
        tenantId: "<tenant_ID>",
        clientId: "<client_ID>",
        secret: "<secret>",
        oauthServerUrl: "<OAuth_Server_URL>",
        redirectUri: "<redirect_URI>"
    }));
    ```
    {: codeblock}

    Sie müssen die Middleware mit dem passenden Sitzungsspeicher für die Produktionsumgebungen konfigurieren. Weitere Informationen finden Sie in der <a href="https://github.com/expressjs/session" target="_blank"> Dokumentation zu express.js<img src="../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>.
    {: note}


## Schritt 4: Anwendung schützen
{: #node-web-protect}

Nachdem Sie nun {{site.data.keyword.appid_short_notm}} installiert haben, können Sie Ihre Anwendung schützen. Sie können auswählen, ob Sie Ihre gesamte Anwendung oder nur bestimmte Ressourcen schützen möchten, indem Sie eine Web-App-Strategie definieren.
{: shortdesc}


1. Konfigurieren Sie den Callback-Endpunkt. Der Callback beendet den Berechtigungsprozess, indem er Zugriffs- und Identitätstoken aus der App-ID abruft und den Benutzer an einen der folgenden Positionen weiterleitet:<ul><li>Die ursprüngliche URL der Anforderung, die die Authentifizierung ausgelöst hat und die in der HTTP-Sitzung als `WebAppStrategy.ORIGINAL_URL` persistent gespeichert ist. </li><li>Angabe einer Weiterleitung im Fall einer erfolgreichen Authentifizierung. </li><li>Das Stammverzeichnis der Anwendung (`/`), so wie es im nächsten Schritt dargestellt wird. </li></ul>

    ```javascript
    app.get(CALLBACK_URL, passport.authenticate(WebAppStrategy.STRATEGY_NAME));
    ```
    {: codeblock}

2. Richten Sie einen Anmeldeendpunkt ein, der einen Browser immer zu einem Anmelde-Widget weiterleitet. Stellen Sie sicher, dass Sie eine Option für erfolgreiche Weiterleitung hinzufügen, damit es nicht zu einer endlosen Authentifizierungsschleife kommt. 

    ```javascript
    app.get('/appid/login', passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
        successRedirect: '/',
        forceLogin: true
    }));
    ```
    {: codeblock}

3. Konfigurieren Sie die Abmeldung. Wenn ein Benutzer sich bei Ihrer Anwendung abmeldet, werden die zugehörigen Authentifizierungsdaten aus der Sitzung entfernt. Um mit Ihrer Anwendung zu interagieren, müssen die Benutzer sich erneut anmelden. 

    ```javascript
    app.get('/appid/logout', function(req, res){
        webappstrategy.logout(req);
        res.redirect('/');
    });
    ```
    {: shortdesc}

## Schritt 5: App personalisieren
{: #node-web-user-info}

Sie könne Informationen abrufen, die von Ihren Identitätsprovidern bereitgestellt werden, um Ihre Apperfahrung individuell zu gestalten.
{: shortdesc}

1. Konfigurieren Sie Ihre Anwendung, um Benutzerdaten abzurufen. `protected` ist eine Platzhaltervariable, die Sie ändern können, um sie dem Endpunkt für Ihre Anwendung anzupassen. 

    ```javascript
    app.get("/protected", passport.authenticate(WebAppStrategy.STRATEGY_NAME), function(req, res){
        res.json(req.user);
    });
    ```
    {: codeblock}

    In der Beispielanwendung können Sie beispielsweise sehen, wie der Benutzername abgerufen wird, um Ihre Anwendung zu personalisieren.
    ```javascript
    app.get('/api/user', (req, res) => {
        // console.log(req.session[WebAppStrategy.AUTH_CONTEXT]);
        res.json({
            user: {
                name: req.user.name
            }
        });
    });
    ```
    {: codeblock}


## Schritt 6: Konfiguration testen
{: #node-web-test}

Um Ihre Berechtigungskonfiguration zu testen, navigieren Sie zu der URL, auf der Ihr Server - wie in Ihrer Anwendung definiert - empfangsbereit ist. Versuchen Sie, sich anzumelden, und versuchen Sie, sich abzumelden. Stellen Sie sicher, dass die Konfiguration wie erwartet funktioniert. 

Wenn Sie für den nächsten Schritte bereit sind, können Sie versuchen, die [Mehrfaktorauthentifizierung für Cloud Directory](/docs/services/appid?topic=appid-cd-mfa) zu aktivieren oder [angepasste Attribute](/docs/services/appid?topic=appid-profiles) hinzuzufügen, um Ihre App weiter individuell anzupassen. 


