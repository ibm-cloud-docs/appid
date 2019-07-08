---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-20"

keywords: authentication, authorization, identity, app security, secure, customizing apps, directory, registry, 

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

# App-Branding
{: #branded}

Sie können eigene angepasste Anzeigen anzeigen, eigene Abläufe verwenden und die Authentifizierungs- und Autorisierungsfunktionen von {{site.data.keyword.appid_full}} nutzen. Mit Cloud Directory als Identitätsprovider können die Benutzer mit Ihren Apps interagieren und benötigen deutlich weniger Unterstützung durch Sie. Die Benutzer können sich anmelden, sich registrieren, das Kennwort ändern und weitere Aktionen durchführen, ohne dass sie Unterstützung anfordern müssen.
{: shortdesc}


## Informationen zur Wiederverwendung von Anzeigen
{: #branded-understand}

Wenn Sie Ihre vorhandenen Benutzerschnittstellen wiederverwenden, können Sie einen konsistenten Anmeldeablauf für Ihre App erstellen. Durch die Verwendung einheitlicher Bilder, Farben und Markenkennzeichnung ergibt sich ein Wiedererkennungseffekt für Ihre Benutzer, selbst wenn sie nicht direkt mit Ihrer App interagieren.

### Bestehen Voraussetzungen zur Verwendung meiner eigenen Anzeigen?
{: #branded-requirements}


Wenn Sie eigene Benutzerschnittstellen anzeigen möchten, müssen Sie als Identitätsprovider [Cloud Directory](/docs/services/appid?topic=appid-cloud-directory) verwenden. Es gibt verschiedene Möglichkeiten, wie Cloud Directory [konfiguriert](/docs/services/appid?topic=appid-cloud-directory) werden kann. Sie können entscheiden, welche Art von Nachrichten Sie verwenden möchten, und Sie können Inhalt und Gestaltung anpassen. Wissen Sie nicht, was Sie sagen sollen? Nur zu! In der grafischen Benutzerschnittstelle werden Beispielnachrichten bereitgestellt, die Sie verwenden können. 


Möchten Sie eine andere [Sprache](/docs/services/appid?topic=appid-cd-messages#cd-languages) als Englisch verwenden? Sie können eine andere Sprache auswählen, indem Sie die <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/Config/updateLocalization" target="_blank">Management-APIs für Sprachen <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> verwenden, um Ihren eigenen übersetzten Inhalt anzuzeigen.
{: tip}


### Kann ich eigene Anzeigen und Standardanzeigen zusammen verwenden?
{: #branded-hybrid}

Ja! Sie können einen Hybridablauf erstellen, in dem einige Ihrer Anzeigen und einige Standardanzeigen verwendet werden. Allerdings kann innerhalb eines Ablaufs immer nur eine dieser beiden Optionen benutzt werden. Sie können beispielsweise eine eigene Anmeldeanzeige und außerdem die Standardanmeldeanzeige benutzen. Wenn Sie sich für die Verwendung der Standardanmeldeanzeige entscheiden, dann müssen Sie diese Auswahl jedoch für den gesamten Anmeldeablauf (einschließlich der Verifizierung bei der Anmeldung) beibehalten.

### Wie unterscheiden sich die Abläufe in technischer Hinsicht?
{: #branded-technically}

Der Service verwendet OAuth 2.0-Abläufe, um den Autorisierungsprozess zuzuordnen. Wenn Sie Social-Media-Identitätsprovider wie z. B. Facebook konfigurieren, wird der <a href="https://oauthlib.readthedocs.io/en/stable/oauth2/grants/authcode.html" target="_blank">OAuth2-Berechtigungserteilungsablauf <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> verwendet, um das Anmeldewidget aufzurufen. Wenn Sie eigene Anzeigen verwenden, wird der <a href="https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html" target="_blank">Ablauf für die Kennwortberechtigungsnachweise der Ressourceneigner <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> verwendet, um Zugriffs- und Identitätstokens bereitzustellen, die Ihnen das Aufrufen Ihrer Anzeigen ermöglichen.



### Beispiele
{: #branded-examples}

Ja! Die folgenden Beispiele zeigen Cloud Directory in Aktion:

* <a href="https://www.ibm.com/cloud/blog/use-branded-ui-user-sign-app-id" target="_blank">Eigene an Ihr Brand-Marketing angepasste Benutzerschnittstelle für die Benutzeranmeldung mit {{site.data.keyword.appid_short_notm}} verwenden <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>
* <a href="https://www.ibm.com/cloud/blog/use-ui-flows-user-sign-sign-app-id" target="_blank">Eigene UI und Abläufe für Registrierung und Anmeldung mit {{site.data.keyword.appid_short_notm}} verwenden <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>
* <a href="https://www.ibm.com/cloud/blog/custom-login-page-app-id-integration" target="_blank">Angepasste Anmeldeseite mit {{site.data.keyword.appid_short_notm}} verwenden <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>


## Branding der App mit dem Android-SDK
{: #branded-ui-android}

Wenn Cloud Directory aktiviert ist, können Sie mit dem Node.js-SDK angepasste Anzeigen aufrufen. Sie können die gewünschte Kombination der Anzeigen auswählen, mit denen die Benutzer interagieren sollen. <a href="https://www.ibm.com/cloud/blog/use-branded-ui-user-sign-app-id" target="blank">Lesen in diesem Blog <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> ein ausführliches Beispiel dazu!
{: shortdesc}



### Anmelden
{: #branded-android-sign-in}

1. Konfigurieren Sie Ihre [Einstellungen](/docs/services/appid?topic=appid-cloud-directory#cd-settings) für Cloud Directory in der GUI.
2. Fügen Sie den folgenden Code zu Ihrer Anwendung hinzu. Der Anmeldeablauf wird ausgelöst, wenn ein Benutzer in der angepassten Anzeige auf 'Anmelden' klickt. Sie erhalten Zugriffs-, Identitäts- und Aktualisierungstoken, indem Sie Name und Kennwort des Endbenutzers angeben.

  ```java
  AppID.getInstance().signinWithResourceOwnerPassword(getApplicationContext(), username, password, new TokenResponseListener() {
      @Override
      public void onAuthorizationFailure (AuthorizationException exception) {
          // Ausnahmebedingung aufgetreten.
  			 }

      @Override
      public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          // Benutzer authentifiziert.
          }
  });
  ```
  {: codeblock}

</br>
</br>

## Branding der App mit dem iOS-Swift-SDK
{: #branded-ui-ios-swift}

Wenn Cloud Directory aktiviert ist, können Sie mit dem [iOS-Swift-SDK](https://github.com/ibm-cloud-security/appid-clientsdk-swift) eigene, an das Brand-Marketing Ihres Unternehmens angepasste Anzeigen aufrufen.
{: shortdesc}

</br>

### Anmelden
{: #branded-ios-sign-in}

1. Konfigurieren Sie Ihre [Einstellungen](/docs/services/appid?topic=appid-cloud-directory#cd-settings) für Cloud Directory in der GUI.
2. Fügen Sie den folgenden Code in Ihre Anwendung ein. Wenn ein Benutzer versucht, sich anzumelden, wird Ihre angepasste Anzeige aufgerufen, und der Autorisierungs- und Authentifizierungsprozess beginnt mit Ihrer angepassten Anmeldeseite.

  ```swift
  class delegate : TokenResponseDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, response:Response?) {
      // Benutzer authentifiziert.
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
      // Ausnahmebedingung aufgetreten.
  		 }
  }

  AppID.sharedInstance.signinWithResourceOwnerPassword(username: username, password: password, delegate: delegate())
  ```
  {: codeblock}


## Branding der App mit dem Node.js-SDK
{: #branding-ui-nodejs}

Wenn Cloud Directory aktiviert ist, können Sie mit dem Node.js-SDK angepasste Anzeigen aufrufen.
{: shortdesc}

### Anmelden
{: #branded-node-sign-in}

Mithilfe von `WebAppStrategy` können Benutzer sich bei Ihren Web-Apps mit ihrem Benutzernamen und einem Kennwort anmelden. Nach der Anmeldung bei der App bleibt das Zugriffstoken der Benutzer in einer HTTP-Sitzung erhalten, bis die Sitzung endet. Nach dem Beenden oder Ablaufen der HTTP-Sitzung wird auch das Zugriffstoken gelöscht.


1. Konfigurieren Sie Ihre [Einstellungen](/docs/services/appid?topic=appid-cloud-directory#cd-settings) für Cloud Directory in der GUI.
2. Fügen Sie den folgenden Code in Ihre Anwendung ein. Wenn ein Benutzer versucht, sich anzumelden, wird Ihre angepasste Anzeige aufgerufen, und der Autorisierungs- und Authentifizierungsprozess beginnt.

  ```javascript
  app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true // Flash-Nachrichten zulassen.
  }));
  ```
  {: codeblock}

  <table>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="Symbol für weitere Informationen"/> Befehlsparameter </th>
    </thead>
    <tbody>
      <tr>
        <td><code>successRedirect</code></td>
        <td>Die URL, an die der Benutzer nach einer erfolgreichen Authentifizierung weitergeleitet werden soll.</td>
      </tr>
      <tr>
        <td><code>failureRedirect</code></td>
        <td>Die URL, an die der Benutzer weitergeleitet werden soll, wenn die Authentifizierung fehlschlägt.</td>
      </tr>
      <tr>
        <td><code>failureFlash</code></td>
        <td>Bei Angabe von <code>true</code> wird eine Fehlernachricht vom Cloud Directory-Service zurückgegeben. Standardwert: <code>false</code>.</td>
      </tr>
    </tbody>
  </table>

**Hinweis**: Wenn Sie die Anforderung in HTML übergeben, können Sie die Middleware <a href="https://www.npmjs.com/package/body-parser" target="blank">body parser <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> verwenden. Zum Anzeigen der zurückgegebenen Fehlernachricht eignet sich <a href="https://www.npmjs.com/package/connect-flash" target="blank">connect-flash <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>. Unter <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs/blob/master/samples/web-app-sample.js" target="blank">Web-App-Beispiel <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> wird die Funktionsweise gezeigt.


## Branding der App mit der API
{: #branded-ui-api}

Sie können eigene angepasste Anzeigen anzeigen und die Authentifizierungs- und Autorisierungsfunktionen von {{site.data.keyword.appid_short_notm}} nutzen. Mit Cloud Directory als Identitätsprovider können die Benutzer mit Ihren Apps interagieren und benötigen deutlich weniger Unterstützung durch Sie. Die Benutzer können sich anmelden, sich registrieren, das Kennwort zurücksetzen und weitere Aktionen durchführen, ohne dass sie Unterstützung anfordern müssen.
{: shortdesc}

Um dies zu ermöglichen, stellt {{site.data.keyword.appid_short_notm}} die REST-APIs zur Verfügung. Sie können die REST-APIs verwenden, um einen Back-End-Server zu erstellen, der Ihren Web-Apps dient oder um mit einer mobilen App mit Ihren angepassten Anzeigen zu interagieren.

Die Management-API wird mithilfe von Tokens gesichert, die von IBM Cloud Identity and Access Management generiert werden. Dies bedeutet, dass Kontoeigner angeben können, wer in ihrem Team über welche Zugriffsebene für die einzelnen Serviceinstanzen verfügen soll. Weitere Informationen dazu, wie IAM und {{site.data.keyword.appid_short_notm}} zusammenarbeiten, finden Sie in [Servicezugriffsverwaltung](/docs/services/appid?topic=appid-service-access-management#service-access-management).

Nach der Konfiguration Ihrer [Einstellungen](/docs/services/appid?topic=appid-cloud-directory#cd-settings) können Sie die folgenden Endpunkte aufrufen, um die einzelnen Anzeigen aufzurufen.

### Registrieren
{: #branded-api-signup}

Mit dem Endpunkt `/sign_up` können Sie es Benutzern ermöglichen, sich bei Ihrer App zu registrieren.
Übergeben Sie die folgenden Daten im Anforderungshauptteil:
  * Ihre Tenant-ID (tenantID).
  * Cloud Directory-Benutzerdaten. Weitere Details finden Sie in [SCIM Full User Representation](https://tools.ietf.org/html/rfc7643#section-8.2).
    * Ein Kennwortattribut `password`.
    * Im E-Mail-Bereich, bei dem für das primäre Attribut (`primary`) der Wert `true` festgelegt ist, müssen Sie über mindestens eine E-Mail-Adresse verfügen.

Abhängig von Ihrer [E-Mail-Konfiguration](/docs/services/appid?topic=appid-cd-messages#cd-messages) erhält ein Benutzer möglicherweise die Anforderung für die Verifizierung und/oder eine Begrüßungs-E-Mail, wenn er sich für Ihre App registriert. Beide Typen von E-Mails werden ausgelöst, wenn ein Benutzer sich für Ihre App registriert. Die Bestätigungs-E-Mail enthält einen Link, auf den der Benutzer klicken kann, um seine Identität zu bestätigen; es erscheint eine Anzeige mit einem Dank für die Bestätigung oder dem Hinweis, dass die Prüfung abgeschlossen ist.  

Gehen Sie wie folgt vor, um eine eigene Seite anzugeben, die nach der Verifizierung angezeigt werden soll:

1. Navigieren Sie zum Cloud Directory-Identitätsprovider im Dashboard {site.data.keyword.appid_short_notm}}.
2. Klicken Sie auf die Registerkarte für die **E-Mail-Prüfung**.
3. Geben Sie im Feld **URL für angepasste Verifizierungsseite** die URL Ihrer Landing-Page ein.

Wenn dieser Wert bereitgestellt ist, ruft {{site.data.keyword.appid_short_notm}} die URL zusammen mit einer `Kontext`abfrage auf. Wenn Sie den Endpunkt `/sign_up/confirmation_result` aufrufen und die empfangenen `Kontext`parameter übergeben, können Sie im Ergebnis sehen, ob Ihr Benutzer das Konto verifiziert hat. Wurde das Konto verifiziert, können Sie jetzt Ihre angepasste Seite anzeigen.


### Kennwort vergessen
{: #branded-api-forgot-password}

Sie können den Endpunkt `/forgot_password` verwenden, um Benutzern zu ermöglichen, Ihr Kennwort wiederherzustellen, falls Sie es vergessen haben sollten.

Übergeben Sie die folgenden Daten im Anforderungshauptteil:
  * Ihre Tenant-ID (tenantID).
  * Die E-Mail des Cloud Directory-Benutzers.

Wenn der Endpunkt aufgerufen wird, wird die E-Mail zum Zurücksetzen des Kennworts an den Benutzer gesendet. Die E-Mail enthält die Schaltfläche **Zurücksetzen**. Nachdem die Benutzer auf diese Schaltfläche geklickt haben, wird von {{site.data.keyword.appid_short_notm}} eine Anzeige aufgerufen, in der sie ihr Kennwort zurücksetzen können.

Sie können eine eigene Seite angeben, die nach dem Zurücksetzen des Kennworts angezeigt werden soll:

1. Konfigurieren Sie Ihre [Einstellungen](/docs/services/appid?topic=appid-cloud-directory#cd-settings) für Cloud Directory in der GUI. Die Option **Benutzern das Kontomanagement innerhalb Ihrer App ermöglichen** muss auf **Ein** eingestellt sein.
2. Vergewissern Sie sich, dass auf der Registerkarte **Kennwort zurücksetzen** des Service-Dashboards die Option **E-Mail für vergessenes Kennwort** auf **Ein** gesetzt ist.
3. Geben Sie die URL Ihrer Landing-Page im Feld für die **URL für die angepasste Seite zum Zurücksetzen des Kennworts** ein.  

Wenn dieser Wert bereitgestellt ist, ruft {{site.data.keyword.appid_short_notm}} die URL zusammen mit einer `Kontext`abfrage auf. Der `Kontext`parameter wird verwendet, um das Ergebnis zu empfangen, wenn `/forgot_password/confirmation_result` aufgerufen wird. Falls das Ergebnis erfolgreich war, können Sie Ihre angepasste Seite anzeigen.

Fügen Sie eine zufällige Zeichenfolge zur angepassten Seite für das Zurücksetzen des Kennworts hinzu und übergeben Sie sie an Ihr Back-End, wenn die Anforderung übergeben wird. Lassen Sie Ihren Handler die Zeichenfolge überprüfen und den Endpunkt `/change_password` nur dann aufrufen, wenn die Zeichenfolge gültig ist. Auf diese Weise, können Sie die Verletzlichkeit Ihres Back-End-Endpunkts zum Zurücksetzen des Kennworts verringern.
{: tip}


### Kennwort ändern
{: #branded-api-change-password}

Sie können den Endpunkt `/change_password` auf zwei Weisen verwenden. Wenn ein Benutzer eine Anforderung zum Zurücksetzen übergibt oder wenn ein Benutzer sich bei Ihrer App anmeldet und sein Kennwort aktualisieren möchte.

Übergeben Sie die folgenden Daten im Anforderungshauptteil, um das zugehörige Kennwort nach einer Anforderung zum Zurücksetzen zu aktualisieren:
  * Ihre Tenant-ID (tenantID).
  * Das neue Kennwort des Benutzers.
  * Die Cloud Directory-Benutzer-UUID.
  * Optional: Die IP-Adresse, von der die Anforderung zum Zurücksetzen des Kennworts ausgeführt wurde. Wenn Sie auswählen, dass die IP-Adresse übergeben wird, dann ist der Platzhalter `%{passwordChangeInfo.ipAddress}` für die E-Mail-Vorlage zum Ändern des Kennworts verfügbar.

Abhängig von Ihrer Konfiguration sendet {{site.data.keyword.appid_short_notm}} beim Ändern des Kennworts eine E-Mail an den Benutzer und lässt diesen wissen, das eine Änderung vorgenommen wurde.


Gehen Sie wie folgt vor, um Benutzern das Ändern ihres Kennworts zu ermöglichen, während sie sich bei Ihrer App anmelden:

Übergeben Sie die folgenden Daten im Anforderungshauptteil:
  * Ihre Tenant-ID (tenantID).
  * Das neue Kennwort des Benutzers.
  * Die Cloud Directory-Benutzer-UUID.

Ihre Seite zum Ändern des Kennworts sollte den Benutzer auffordern, sein aktuelles Kennwort und sein neues Kennwort einzugeben.
{: tip}

Ihr Back-End validiert das aktuelle Kennwort des Benutzers mit der ROP-API und falls dieses gültig ist, wird der Endpunkt mit dem neuen Kennwort aufgerufen. Abhängig von Ihrer Konfiguration sendet {{site.data.keyword.appid_short_notm}} beim Ändern des Kennworts möglicherweise eine E-Mail an den Benutzer und lässt diesen wissen, dass eine Änderung vorgenommen wurde.


### Erneut senden
{: #branded-api-resend}

Sie können den Endpunkt `/resend/{templateName}` verwenden, um eine E-Mail erneut zu senden, wenn ein Benutzer die E-Mail nicht erhalten haben sollte.

Übergeben Sie die folgenden Daten im Anforderungshauptteil:
  * Die Tenant-ID (tenantID).
  * Den Vorlagennamen.
  * Die Cloud Directory-Benutzer-UUID.

### Details ändern
{: #branded-api-change-details}

Wenn ein Benutzer bei Ihrer App angemeldet ist, kann er einige seiner Daten aktualisieren. Sie können `/Users/{userId}` verwenden, um die Daten abzurufen und zu aktualisieren.

Wenn die Benutzerdetails aktualisiert werden, ruft der Endpunkt die aktualisierten Benutzerdaten im Anforderungshauptteil im [SCIM-Format](https://tools.ietf.org/html/rfc7643#section-8.2) ab. Stellen Sie sicher, dass Sie nur die relevanten Details ändern.

Die E-Mail-Adresse kann nicht geändert werden.
{: tip}
