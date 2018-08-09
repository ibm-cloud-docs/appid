---

copyright:
  years: 2017, 2018
lastupdated: "2018-4-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:tip: .tip}

# Markenkennzeichnung bei der Registrierung
{: #branding}

Sie können eigene angepasste Anzeigen anzeigen und die Authentifizierungs- und Berechtigungsfunktionen von {{site.data.keyword.appid_full}} nutzen. Mit Cloud Directory als Identitätsprovider können die Benutzer mit Ihren Apps interagieren und benötigen deutlich weniger Unterstützung durch Sie. Sie können sich ohne Unterstützung anmelden.
{: shortdesc}

Wenn Sie Ihre eigenen Anzeigen verwenden, wird der [Ablauf für Kennwortberechtigungsnachweise von Ressourceneignern](https://oauthlib.readthedocs.io/en/stable/oauth2/grants/password.html) verwendet, um Zugriffs- und Identitätstoken bereitzustellen. 


## Angepasste Anzeigen mit dem Android-SDK aufrufen
{: #branded-ui-android}

Wenn Cloud Directory aktiviert ist, können Sie mit dem Android-SDK angepasste Anzeigen aufrufen.  <a href="https://www.ibm.com/blogs/bluemix/2018/01/use-branded-ui-user-sign-app-id/" target="blank">Lesen Sie diesen Blog! <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>
{: shortdesc}

</br>
**Anmelden**

1. **Cloud Directory** als Identitätsprovider **aktivieren**.
2. Den folgenden Befehl in den Code einfügen.
  ```java
  AppID.getInstance().obtainTokensWithROP(getApplicationContext(), username, password,
         new TokenResponseListener() {
         @Override
          public void onAuthorizationFailure (AuthorizationException exception) {
             //Ausnahmebedingung aufgetreten.
  			 }

          @Override
          public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken, RefreshToken refreshToken) {
            //Benutzer authentifiziert.
          }
         });
  ```
  {: pre}

</br>
</br>

## Angepasste Anzeigen mit dem iOS Swift-SDK aufrufen
{: #branded-ui-ios-swift}

Wenn Cloud Directory aktiviert ist, können Sie mit dem iOS Swift-SDK angepasste Anzeigen aufrufen.
{: shortdesc}

</br>
**Anmelden**

1. Auf der Registerkarte für den Identitätsprovider in der GUI den Wert **Aktiv** für Cloud Directory festlegen.
2. Mit dem Kennwort des Ressourceneigners anmelden. Zugriffs- und Identitätstoken werden abgerufen, wenn ein Benutzer versucht, sich mit seinem Benutzernamen und Kennwort anzumelden. 
  ```swift
  class delegate : TokenResponseDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken?, identityToken: IdentityToken?, refreshToken: RefreshToken?, response:Response?) {
      //Benutzer authentifiziert.
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
      //Ausnahmebedingung aufgetreten.
  			 }
  }

  AppID.sharedInstance.obtainTokensWithROP(username: username, password: password, delegate: delegate())
  ```
  {: pre}


</br>
</br>

## Angepasste Anzeigen mit dem Node.js-SDK aufrufen
{: #branded-ui-nodejs}

Wenn Cloud Directory aktiviert ist, können Sie mit dem Node.js-SDK angepasste Anzeigen aufrufen. 
{: shortdesc}

**Anmelden**
1. In den Identitätsprovidereinstellungen den Wert **Aktiv** für Cloud Directory festlegen und einen Callback-Endpunkt angeben.
2. Eine POST-Route zu Ihrer App hinzufügen, die mit den Parametern für den Benutzernamen und das Kennwort aufgerufen werden kann, und mit dem Kennwort des Ressourceneigners anmelden.
    ```javascript
    app.post("/form/submit", bodyParser.urlencoded({extended: false}), passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
    	successRedirect: LANDING_PAGE_URL,
  	failureRedirect: ROP_LOGIN_PAGE_URL,
  	failureFlash : true // Flash-Nachrichten zulassen.
  }));
    ```
    {: pre}
    `WebAppStrategy` ermöglicht es Benutzern, sich bei Ihren Web-Apps mit einem Benutzernamen und einem Kennwort anzumelden. Nach einer erfolgreichen Registrierung wird das Zugriffstoken eines Benutzers in der HTTP-Sitzung gespeichert und ist während der Sitzung verfügbar. Sobald die HTTP-Sitzung gelöscht wird oder abgelaufen ist, ist das Token nicht mehr gültig. {: tip}

