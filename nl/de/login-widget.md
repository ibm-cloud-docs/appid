---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-06"

keywords: authentication, authorization, identity, app security, secure, development, sign in, sign up, password, social, enterprise

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


# Anmeldewidget anzeigen
{: #login-widget}

{{site.data.keyword.appid_full}} stellt ein Anmeldewidget zur Verfügung, mit dem Sie Ihren Benutzern sichere Anmeldeoptionen bieten können.
{: shortdesc}

Wenn Ihre App für die Verwendung eines Identitätsproviders konfiguriert wurde, werden Besucher Ihrer App durch ein Anmeldewidget zur Anmeldeanzeige weitergeleitet. Mit dem Anmeldewidget können Sie vorkonfigurierte Anzeigen für Ihre Anmeldeabläufe anzeigen. Zusätzlich interessant ist hierbei, dass Sie Ihren Anmeldeablauf jederzeit aktualisieren können, ohne Ihren Quellcode in irgendeiner Weise zu ändern!

Wollen Sie eine Benutzererfahrung kreieren, durch die sich Ihre App von anderen abhebt? Sie können [Ihre eigenen Anzeigen einbringen](/docs/services/appid?topic=appid-branded)!
{: tip}

## Informationen zum Anmeldewidget
{: #widget-understanding}

Sie können die Vorteile von {{site.data.keyword.appid_short_notm}} auch ohne eigene UI-Anzeigen nutzen, indem Sie das Anmeldewidget verwenden.
{: shortdesc}

### Was ist der Standardwert?
{: #widget-default}

Wenn mehr als ein Identitätsprovider konfiguriert ist, wird ein Benutzer an das Anmeldewidget weitergeleitet, wenn er versucht, sich bei Ihrer Anwendung anzumelden. Durch die Verwendung des Anmeldewidgets können Benutzer den Provider auswählen, mit dem sie ihre Identität überprüfen möchten. Wenn nur ein einziger Provider aktiviert (**Ein**) ist, werden Besucher zur Authentifizierungsanzeige des betreffenden Identitätsproviders weitergeleitet.

### Wie viele Informationen erhält {{site.data.keyword.appid_short_notm}} von einem Identitätsprovider?
{: #widget-obtain-info}

Wenn Sie Social-Media- oder unternehmenseigene Identitätsprovider verwenden, kann {{site.data.keyword.appid_short_notm}} die Kontoinformationen eines Benutzers lesen. Der Service verwendet ein Token und die Zusicherungen, die vom Identitätsprovider zurückgegeben werden, um zu überprüfen, ob ein Benutzer die Person ist, die er zu sein behauptet. Da der Service nie Schreibzugriff auf die Informationen hat, müssen die Benutzer den ausgewählten Identitätsprovider verwenden, um Aktionen wie das Zurücksetzen des Kennworts ausführen zu können. Wenn sich ein Benutzer beispielsweise mit Facebook bei Ihrer App anmeldet und dann sein Kennwort ändern will, muss er dies über www.facebook.com tun.

Wenn Sie [Cloud Directory](/docs/services/appid?topic=appid-cloud-directory) verwenden, ist {{site.data.keyword.appid_short_notm}} der Identitätsprovider. Der Service verwendet Ihre Registry, um Ihre Benutzeridentität zu überprüfen. Da {{site.data.keyword.appid_short_notm}} der Provider ist, können die Benutzer die Vorteile der erweiterten Funktionalität (wie z. B. das Zurücksetzen des Kennworts) direkt in ihrer App nutzen.


### Welche Anzeigen können für die einzelnen Provider angezeigt werden?
{: #widget-options}

In der folgenden Tabelle sehen Sie, welche Anzeigen Sie für den jeweiligen Identitätsprovidertyp anzeigen können.

<table>
  <thead>
    <tr>
      <th>Anzeige 'Anmeldewidget'</th>
      <th>Social-Media-Identitätsprovider</th>
      <th>Unternehmensidentitätsprovider</th>
      <th>Cloud Directory</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Anmelden</td>
      <td><img src="images/confirm.png" width="32" alt="Funktion verfügbar" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="Funktion verfügbar" style="width:32px;" /></td>
      <td><img src="images/confirm.png" width="32" alt="Funktion verfügbar" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Registrieren</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Funktion verfügbar" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Kennwort vergessen</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Funktion verfügbar" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Kennwort ändern</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Funktion verfügbar" style="width:32px;" /></td>
    </tr>
    <tr>
      <td>Kontodetails</td>
      <td> </td>
      <td> </td>
      <td><img src="images/confirm.png" width="32" alt="Funktion verfügbar" style="width:32px;" /></td>
    </tr>
  </tbody>
</table>

</br>
</br>

## Anmeldewidget anpassen
{: #widget-customize}

{{site.data.keyword.appid_short_notm}} stellt eine Standardanmeldeanzeige zur Verfügung, die Sie aufrufen können, wenn Sie keine eigenen Anzeigen der Benutzerschnittstellen haben. Sie können die Anzeige so anpassen, dass das Logo und die gewünschten Farben angezeigt werden.
{: shortdesc}

Anpassen der Anzeige:

1. Öffnen Sie das {{site.data.keyword.appid_short_notm}}-Service-Dashboard.
2. Wählen Sie den Abschnitt über die **Anpassung der Registrierung** aus. Sie können die Darstellung des Anmeldewidgets ändern, damit es zur Außendarstellung des Unternehmens passt.
3. Laden Sie Ihr Unternehmenslogo hoch. Wählen Sie dazu eine PNG- oder JPG-Datei von Ihrem lokalen System aus. Die empfohlene Bildgröße ist 320 x 320 Pixel. Die maximale Dateigröße ist 100 KB.
4. Wählen Sie eine Headerfarbe für das Widget aus der Farbauswahl aus oder geben Sie den hexadezimalen Code für eine andere Farbe ein.
5. Prüfen Sie das Aussehen im Vorschaubereich und klicken Sie auf **Änderungen speichern**, wenn Sie mit den Anpassungen zufrieden sind. Eine Bestätigungsnachricht wird angezeigt.
6. Aktualisieren Sie die Anmeldeseite im Browser, um Ihre Änderungen zu überprüfen.

Nicht vergessen! Sie können {{site.data.keyword.appid_short_notm}} auch mit anderen Sprachen nutzen. Wenn Sie kein SDK für die Sprache haben, mit der Sie arbeiten, können Sie immer die APIs verwenden. Weitere Informationen finden Sie in <a href="https://www.ibm.com/blogs/bluemix/tag/app-id/" target="blank">unseren Blogs<img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>.
{: tip}


## Anmeldewidget mit dem Android-SDK anzeigen
{: #widget-display-android}

Sie können vorkonfigurierte Anzeigen mit dem [Android-Client-SDK](https://github.com/ibm-cloud-security/appid-clientsdk-android) aufrufen.
{: shortdesc}

Den folgenden Befehl in den Code einfügen.

  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launch(this, new AuthorizationListener() {
        @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          // Ausnahmebedingung aufgetreten.
  			 }

        @Override
        public void onAuthorizationCanceled () {
          //Authentifizierung von Benutzer abgebrochen
        }

        @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, refreshToken: RefreshToken) {
          // Benutzer authentifiziert.
        }
      });
  ```
{: codeblock}

</br>

### Registrieren
{: #widget-android-signup}

1. Konfigurieren Sie Ihre [Einstellungen](/docs/services/appid?topic=appid-cloud-directory#cd-settings) für Cloud Directory in der GUI. Die Optionen **Benutzern die Registrierung bei Ihrer App ermöglichen** und **Benutzern das Kontomanagement innerhalb Ihrer App ermöglichen** müssen auf **Ein** eingestellt sein.
2. Fügen Sie den folgenden Code zu Ihrer App hinzu. Wenn sich ein Benutzer über Ihre angepasste Anzeige für Ihre App registriert, wird der Anmeldeablauf gestartet. Der folgende Aufruf registriert nicht nur den Benutzer, sondern kann abhängig von Ihrer Cloud Directory-Konfiguration auch eine Bestätigungs-E-Mail senden, um die Registrierung abzuschließen.

  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launchSignUp(this, new AuthorizationListener() {
      @Override
      public void onAuthorizationFailure (AuthorizationException exception) {
          // Ausnahmebedingung aufgetreten.
  			 }

      @Override
      public void onAuthorizationCanceled () {
          // Registrierung vom Benutzer abgebrochen
      }

      @Override
      public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          if (accessToken != null && identityToken != null) {
              // Benutzer authentifiziert.
          } else {
              // E-Mail-Verifizierung erforderlich.
          }
      }
  });
  ```
  {: pre}

</br>

### Kennwort vergessen
{: #widget-android-forgot-password}

1. Konfigurieren Sie Ihre [Einstellungen](/docs/services/appid?topic=appid-cloud-directory#cd-settings) für Cloud Directory in der GUI. Die Option **Benutzern das Kontomanagement innerhalb Ihrer App ermöglichen** muss auf **Ein** eingestellt sein.
2. Vergewissern Sie sich, dass auf der Registerkarte **Kennwort zurücksetzen** des Service-Dashboards die Option **E-Mail für vergessenes Kennwort** auf **Ein** gesetzt ist.
3. Fügen Sie den folgenden Code zu Ihrer App hinzu. Wenn ein Benutzer in Ihrer Anwendung auf "Kennwort vergessen" klickt, ruft das SDK die API "forgot_password" auf, um eine E-Mail an den Benutzer zu senden, der es ihnen ermöglicht, ihr Kennwort zurückzusetzen.

  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launchForgotPassword(this, new AuthorizationListener() {
      @Override
   	public void onAuthorizationFailure (AuthorizationException exception) {
          // Ausnahmebedingung aufgetreten.
  			 }

      @Override
      public void onAuthorizationCanceled () {
          // Aktion für vergessenes Kennwort vom Benutzer abgebrochen.  			
      }

      @Override
      public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          // Aktion für vergessenes Kennwort beendet, in diesem Fall sind Zugriffstoken und Identitätstoken null.
      }
  });
  ```
  {: codeblock}

</br>

### Details ändern
{: #widget-android-change-details}

1. Konfigurieren Sie Ihre [Einstellungen](/docs/services/appid?topic=appid-cloud-directory#cd-settings) für Cloud Directory in der GUI. Die Optionen **Benutzern die Registrierung bei Ihrer App ermöglichen** und **Benutzern das Kontomanagement innerhalb Ihrer App ermöglichen** müssen auf **Ein** eingestellt sein.
2. Stellen Sie auf der Registerkarte **Kennwort geändert** des Service-Dashboards die Option **E-Mail bei Kennwortänderung** auf 'Ein'.
3. Rufen Sie das Anmeldewidget auf, um den Verarbeitungsablauf für das Ändern von Details zu starten.

  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launchChangeDetails(this, new AuthorizationListener() {
      @Override
      public void onAuthorizationFailure (AuthorizationException exception) {
          // Ausnahmebedingung aufgetreten.
  			 }

      @Override
      public void onAuthorizationCanceled () {
          // Aktion für Detailänderung vom Benutzer abgebrochen.  			
      }

      @Override
      public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          // Benutzer authentifiziert, neue Tokens erhalten.
  			 }
  });
  ```
  {: codeblock}

</br>

### Kennwort ändern
{: #widget-android-change-password}

1. Konfigurieren Sie Ihre [Einstellungen](/docs/services/appid?topic=appid-cloud-directory#cd-settings) für Cloud Directory in der GUI. Die Optionen **Benutzern die Registrierung bei Ihrer App ermöglichen** und **Benutzern das Kontomanagement innerhalb Ihrer App ermöglichen** müssen auf **Ein** eingestellt sein.
2. Fügen Sie den folgenden Code in Ihre App ein, um den Ablauf für das Ändern des Kennworts zu starten.

  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launchChangePassword(this, new AuthorizationListener() {
      @Override
      public void onAuthorizationFailure (AuthorizationException exception) {
          // Ausnahmebedingung aufgetreten.
  			 }

      @Override
      public void onAuthorizationCanceled () {
          // Aktion für Kennwortänderung vom Benutzer abgebrochen.  			
      }

      @Override
      public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
          // Benutzer authentifiziert, neue Tokens erhalten.
  			 }
  });
  ```
  {: codeblock}



## Anmeldewidget mit dem iOS Swift-SDK anzeigen
{: #widget-display-ios-swift}

Sie können vorkonfigurierte Anzeigen mit dem [iOS Swift-Client-SDK](https://github.com/ibm-cloud-security/appid-clientsdk-swift) aufrufen.
{: shortdesc}

Den folgenden Befehl in den Code einfügen.

  ```swift
  import IBMCloudAppID
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, refreshToken: RefreshToken?) {
          // Benutzer authentifiziert.
      }

      public func onAuthorizationCanceled() {
          // Authentifizierung vom Benutzer abgebrochen
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          // Ausnahmebedingung aufgetreten.
  			 }
  }

  AppID.sharedInstance.loginWidget?.launch(delegate: delegate())
  ```
  {: codeblock}

</br>

### Registrieren
{: #widget-ios-signup}

1. Konfigurieren Sie Ihre [Einstellungen](/docs/services/appid?topic=appid-cloud-directory#cd-settings) für Cloud Directory in der GUI. Die Optionen **Benutzern die Registrierung bei Ihrer App ermöglichen** und **Benutzern das Kontomanagement innerhalb Ihrer App ermöglichen** müssen auf **Ein** eingestellt sein.
2. Fügen Sie den folgenden Code in Ihre Anwendung ein. Wenn ein Benutzer versucht, sich für Ihre Anwendung zu registrieren, wird das Anmeldewidget aufgerufen und zeigt die angepasste Registrierungsseite an.

  ```swift
  class delegate : AuthorizationDelegate {
    public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
       if accessToken == nil && identityToken == nil {
        // E-Mail-Verifizierung erforderlich.
        return
       }
     // Benutzer authentifiziert.
    }

    public func onAuthorizationCanceled() {
        // Registrierung vom Benutzer abgebrochen.
    }

    public func onAuthorizationFailure(error: AuthorizationError) {
        // Ausnahmebedingung aufgetreten.
     			 }
  }

  AppID.sharedInstance.loginWidget?.launchSignUp(delegate: delegate())
  ```
  {: codeblock}

</br>

### Kennwort vergessen
{: #widget-ios-forgot-password}

1. Konfigurieren Sie Ihre [Einstellungen](/docs/services/appid?topic=appid-cloud-directory#cd-settings) für Cloud Directory in der GUI. Die Option **Benutzern das Kontomanagement innerhalb Ihrer App ermöglichen** muss auf **Ein** eingestellt sein.
2. Vergewissern Sie sich, dass auf der Registerkarte **Kennwort zurücksetzen** des Service-Dashboards die Option **E-Mail für vergessenes Kennwort** auf **Ein** gesetzt ist.
3. Fügen Sie den folgenden Code in Ihre Anwendung ein. Wenn einer Ihrer App-Benutzer die Aktualisierung seines Kennworts anfordert, wird das Anmeldewidget aufgerufen und der Prozess wird gestartet.

  ```swift
  class delegate : AuthorizationDelegate {
     public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
        // Aktion für vergessenes Kennwort beendet, in diesem Fall sind Zugriffstoken und Identitätstoken null.
     }

     public func onAuthorizationCanceled() {
         // Aktion für vergessenes Kennwort vom Benutzer abgebrochen.
     }

     public func onAuthorizationFailure(error: AuthorizationError) {
         // Ausnahmebedingung aufgetreten.
  		 }
  }

  AppID.sharedInstance.loginWidget?.launchForgotPassword(delegate: delegate())
  ```
  {: codeblock}

</br>

### Details ändern
{: #widget-ios-change-details}

1. Konfigurieren Sie Ihre [Einstellungen](/docs/services/appid?topic=appid-cloud-directory#cd-settings) für Cloud Directory in der GUI. Die Optionen **Benutzern die Registrierung bei Ihrer App ermöglichen** und **Benutzern das Kontomanagement innerhalb Ihrer App ermöglichen** müssen auf **Ein** eingestellt sein.
2. Stellen Sie auf der Registerkarte **Kennwort geändert** des Service-Dashboards die Option **E-Mail bei Kennwortänderung** auf 'Ein'.
3. Rufen Sie das Anmeldewidget auf, um den Verarbeitungsablauf für das Ändern von Details zu starten.

  ```swift
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
         // Benutzer authentifiziert, neue Tokens erhalten.
      }

      public func onAuthorizationCanceled() {
          // Aktion für Detailänderung vom Benutzer abgebrochen.
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          // Ausnahmebedingung aufgetreten.
  			 }
  }

   AppID.sharedInstance.loginWidget?.launchChangeDetails(delegate: delegate())
  ```
  {: codeblock}

</br>

### Kennwort ändern
{: #widget-ios-change-password}

1. Konfigurieren Sie Ihre [Einstellungen](/docs/services/appid?topic=appid-cloud-directory#cd-settings) für Cloud Directory in der GUI. Die Optionen **Benutzern die Registrierung bei Ihrer App ermöglichen** und **Benutzern das Kontomanagement innerhalb Ihrer App ermöglichen** müssen auf **Ein** eingestellt sein.
2. Fügen Sie den folgenden Code in Ihre App ein, um den Ablauf für das Ändern des Kennworts zu starten.

  ```swift
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
          // Benutzer authentifiziert, neue Tokens erhalten.
      }

      public func onAuthorizationCanceled() {
          // Kennwortänderung vom Benutzer abgebrochen.
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
           // Ausnahmebedingung aufgetreten.
  			 }
   }

   AppID.sharedInstance.loginWidget?.launchChangePassword(delegate: delegate())
  ```
  {: codeblock}


## Anmeldewidget mit dem Node.js-SDK anzeigen
{: #widget-display-nodejs}

Sie können vorkonfigurierte Anzeigen mit dem [Node.js-Server-SDK](https://github.com/ibm-cloud-security/appid-serversdk-nodejs) aufrufen.
{: shortdesc}

Eine POST-Route zu Ihrer App hinzufügen, die mit den Parametern für den Benutzernamen und das Kennwort aufgerufen werden kann, und mit dem Kennwort des Ressourceneigners anmelden.

  ```javascript
  app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true // Flash-Nachrichten zulassen.
  }));
  ```
  {: codeblock}

`WebAppStrategy` ermöglicht es Benutzern, sich bei Ihren Web-Apps mit einem Benutzernamen und einem Kennwort anzumelden. Nach einer erfolgreichen Registrierung wird das Zugriffstoken eines Benutzers in der HTTP-Sitzung gespeichert und ist während der Sitzung verfügbar. Wenn die HTTP-Sitzung gelöscht wird oder abgelaufen ist, ist das Token nicht mehr gültig.
{: tip}

</br>

### Registrieren
{: #widget-nodejs-signup}

1. Konfigurieren Sie Ihre [Einstellungen](/docs/services/appid?topic=appid-cloud-directory#cd-settings) für Cloud Directory in der GUI. Die Optionen **Benutzern die Registrierung bei Ihrer App ermöglichen** und **Benutzern das Kontomanagement innerhalb Ihrer App ermöglichen** müssen auf **Ein** eingestellt sein.
2. Fügen Sie den folgenden Code in Ihre Anwendung ein. Wenn ein Benutzer versucht, sich für Ihre Anwendung zu registrieren, wird das Anmeldewidget aufgerufen und zeigt die angepasste Registrierungsseite an.

  ```javascript
  app.get("/sign_up", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.SIGN_UP
  }));
  ```
  {: codeblock}

</br>

### Kennwort vergessen
{: #widget-nodejs-forgot-password}

1. Konfigurieren Sie Ihre [Einstellungen](/docs/services/appid?topic=appid-cloud-directory#cd-settings) für Cloud Directory in der GUI. Die Option **Benutzern das Kontomanagement innerhalb Ihrer App ermöglichen** muss auf **Ein** eingestellt sein.
2. Vergewissern Sie sich, dass auf der Registerkarte **Kennwort zurücksetzen** des Service-Dashboards die Option **E-Mail für vergessenes Kennwort** auf **Ein** gesetzt ist.
3. Fügen Sie den folgenden Code in Ihre Anwendung ein, um die Eigenschaft *show* an `WebAppStrategy.FORGOT_PASSWORD` zu übergeben. Wenn einer Ihrer Benutzer die Aktualisierung seines Kennworts für Ihre App anfordert, wird das Anmeldewidget aufgerufen und der Prozess wird gestartet.

  ```javascript
  app.get("/forgot_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.FORGOT_PASSWORD
  }));
  ```
  {: codeblock}

</br>

### Details ändern
{: #widget-nodejs-change-details}

1. Konfigurieren Sie Ihre [Einstellungen](/docs/services/appid?topic=appid-cloud-directory#cd-settings) für Cloud Directory in der GUI. Die Optionen **Benutzern die Registrierung bei Ihrer App ermöglichen** und **Benutzern das Kontomanagement innerhalb Ihrer App ermöglichen** müssen auf **Ein** eingestellt sein.
2. Stellen Sie auf der Registerkarte **Kennwort geändert** des Service-Dashboards die Option **E-Mail bei Kennwortänderung** auf 'Ein'.
3. Fügen Sie den folgenden Code in Ihre Anwendung ein, um die Eigenschaft *show* an `WebAppStrategy.FORGOT_PASSWORD` zu übergeben und um damit das Formular zum Ändern der Details aufzurufen.

  ```javascript
  app.get("/change_details", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_DETAILS
  }));
  ```
  {: codeblock}

</br>

### Kennwort ändern
{: #widget-nodejs-change-password}

1. Konfigurieren Sie Ihre [Einstellungen](/docs/services/appid?topic=appid-cloud-directory#cd-settings) für Cloud Directory in der GUI. Die Optionen **Benutzern die Registrierung bei Ihrer App ermöglichen** und **Benutzern das Kontomanagement innerhalb Ihrer App ermöglichen** müssen auf **Ein** eingestellt sein.
2. Stellen Sie auf der Registerkarte **Kennwort geändert** des Service-Dashboards die Option **E-Mail bei Kennwortänderung** auf 'Ein'.
3. Fügen Sie den folgenden Code in Ihre Anwendung ein, um die Eigenschaft *show* an `WebAppStrategy.FORGOT_PASSWORD` zu übergeben und um damit das Formular zum Ändern der Details aufzurufen.

  ```javascript
  app.get("/change_password", passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
  	successRedirect: LANDING_PAGE_URL,
  	show: WebAppStrategy.CHANGE_PASSWORD
  }));
  ```
  {: codeblock}
