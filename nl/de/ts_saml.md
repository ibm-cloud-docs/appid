---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-21"

keywords: authentication, authorization, identity, app security, secure, development, idp, troubleshooting, redirected, validation

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
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}

# Fehlerbehebung: SAML
{: #troubleshooting-idp}

Wenn bei der Konfiguration von SAML für die Nutzung mit {{site.data.keyword.appid_full}} Probleme auftreten, ziehen Sie die folgenden Verfahren zur Fehlerbehebung und zum Abrufen von Hilfe in Betracht.
{: shortdesc}


## Allgemeine Konfigurationsprobleme
{: #ts-common-saml}

Da vom SAML-Framework mehrere Profile, Abläufe und Konfigurationen unterstützt werden, ist es besonders wichtig, dass die Konfiguration des Identitätsproviders ordnungsgemäß ist. In den folgenden Abschnitten finden Sie Hilfe zum Beheben einiger allgemeiner Probleme, die bei der Arbeit mit SAML auftreten können.
{: shortdesc}


Detaillierte Erklärungen bestimmter Fehlercodes und -nachrichten des Identitätsproviders, die auf dieser Seite nicht aufgeführt werden, finden Sie unter [SAML-Spezifikation](http://docs.oasis-open.org/security/saml/Post2.0/sstc-saml-tech-overview-2.0.html). Wenn Sie die gesuchten Informationen nicht finden, können Sie sich an die Administration des Identitätsprovider wenden, um weitere Informationen zu erhalten.
{: note}



### Fehlender Parameter `RelayState`
{: #ts-saml-relaystate}

**Problem**

Der Parameter `RelayState` fehlt in der Authentifizierungsantwort.


**Ursache**

Von {{site.data.keyword.appid_short_notm}} wird ein nicht transparenter Parameter gesendet, der als `RelayState` bezeichnet wird und Teil der Authentifizierungsanforderung ist. Wenn der Parameter in der Antwort nicht angezeigt wird, ist der Identitätsprovider möglicherweise nicht so konfiguriert, dass er ordnungsgemäß zurückgegeben wird. Für `RelayState` wird das folgende Format verwendet. 

```
https://idp.example.org/SAML2/SSO/Redirect?SAMLRequest=request&RelayState=token
```
{: screen}

**Lösung**

Stellen Sie sicher, dass der SAML-Provider so konfiguriert ist, dass der Parameter `RelayState` ohne eine Änderung an {{site.data.keyword.appid_short_notm}} zurückgegeben wird. 


### Fehlendes oder falsches Feld 'NameID'
{: #ts-saml-nameid}

**Problem**

Wenn Sie eine Authentifizierungsanforderung senden, empfangen Sie einen Fehler im Zusammenhang mit `NameID`.

**Ursache**

Von {{site.data.keyword.appid_short_notm}} als Service-Provider wird definiert, wie die Benutzer vom Service und Identitätsprovider identifiziert werden. Mit {{site.data.keyword.appid_short_notm}} werden die Benutzer in der Authentifizierungsanforderung `NameID` im Feld `NameID` wie im folgenden Beispiel dargestellt identifiziert. 

```
<NameIDFormat>urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress</NameIDFormat>
```
{: screen}

**Lösung**

Stellen Sie zur Lösung des Problems sicher, dass der Wert von `NameID` als E-Mail-Adresse formatiert ist. Stellen Sie sicher, dass alle Benutzer in der Registry des Identitätsproviders über ein gültiges E-Mail-Adressformat verfügen. Stellen Sie anschließend sicher, dass das Feld `NameID` entsprechend definiert ist, sodass immer eine gültige E-Mail zurückgegeben wird - auch wenn Benutzer in der Registry über mehrere E-Mails verfügen. 



### Fehler beim Signieren der Antwort
{: #ts-saml-response-sign-fail}

**Problem**

Wenn Sie eine Authentifizierungsanforderung senden, empfangen Sie die folgende Fehlernachricht: 

```
Could not verify SAML assertion signature. Ensure {{site.data.keyword.appid_short_notm}} is configurated with your SAML provider's signing certificate.
```
{: screen}

**Ursache**

Von {{site.data.keyword.appid_short_notm}} wird erwartet, dass alle SAML-Zusicherungen in der Antwort signiert sind. Wenn die Signatur in der Antwort vom Service nicht gefunden oder verifiziert werden kann, wird ein Fehler zurückgegeben.

**Lösung**

Stellen Sie zur Behebung des Problems Folgendes sicher:

* Sie haben das Signierzertifikat aus der XML-Datei mit den Metadaten des Identitätsproviders extrahiert. Stellen Sie sicher, dass Sie den Schlüssel mit `<KeyDescriptor use="signing">` verwenden.
* Sie haben den Antwortsignieralgorithmus XXX festgelegt.  





### Fehler beim Entschlüsseln der Antwort
{: #ts-saml-decrypt-fail}

**Problem**

Als Antwort auf Ihre Authentifizierungsanforderung empfangen Sie eine der folgenden Fehlernachrichten. 

Fehlernachricht 1:

```
Unexpectedly received an encrypted assertion. Please enable response encryption in your {{site.data.keyword.appid_short_notm}} SAML configuration.
```
{: screen}

Fehlernachricht 2: 

```
Could not decrypt SAML assertion. Ensure your SAML provider is configured with the {{site.data.keyword.appid_short_notm}} encryption
```
{: screen}


**Ursache**

Wenn für den Identitätsprovider eine Verschlüsselung konfiguriert wurde, muss für {{site.data.keyword.appid_short_notm}} das Signieren der SAML-Authentifizierungsanforderungen (AuthnRequest) konfiguriert werden. Danach muss der Identitätsprovider so konfiguriert werden, dass von ihm die entsprechende Konfiguration erwartet wird. Diese Fehler können aus einem der folgenden Gründe auftreten: 

- {{site.data.keyword.appid_short_notm}} ist nicht so konfiguriert, dass eine Verschlüsslung der SAML-Antwort des Identitätsproviders erwartet wird. 
- Die Zusicherungen können von {{site.data.keyword.appid_short_notm}} nicht ordnungsgemäß entschlüsselt werden. 


**Lösung**

Wenn Sie Fehlernachricht 1 empfangen, überprüfen Sie, ob SAML so konfiguriert ist, dass eine verschlüsselte Antwort erwartet wird. Standardmäßig wird von {{site.data.keyword.appid_short_notm}} nicht erwartet, dass die Antwort verschlüsselt wird. Legen Sie zum Konfigurieren der Verschlüsselung für den Parameter `encryptResponse` den Wert **true** in der [API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp) fest.

Wenn Sie Fehlernachricht 2 empfangen, stellen Sie sicher, dass Ihr Zertifikat korrekt ist. Sie können das Signaturzertifikat aus der XML-Datei der {{site.data.keyword.appid_short_notm}}-Metadaten extrahieren. Stellen Sie sicher, dass Sie den Schlüssel mit `<KeyDescriptor use="signing">` verwenden. Stellen Sie sicher, dass der Identitätsprovider für die Verwendung von `` als Signatursignieralgorithmus konfiguriert ist. 


### Beantworterfehlercode
{: #ts-saml-responder}

**Problem**

Wenn Sie eine Authentifizierungsanforderung senden, empfangen Sie die folgende allgemeine Fehlernachricht: 

```
urn:oasis:names:tc:SAML:2.0:status:Responder
```
{: screen}

**Ursache**

Von {{site.data.keyword.appid_short_notm}} wird zwar die Anfangsauthentifizierungsanforderung gesendet, vom Identitätsprovider muss jedoch die Benutzerauthentifizierung ausgeführt und die Antwort zurückgegeben werden. Auslöser für die diese Fehlernachricht können mehrere Gründe sein. 

Möglicherweise wird die Nachricht angezeigt, wenn der Identitätsprovider: 

* den Benutzernamen nicht finden oder verifizieren kann.
* das Format von `NameID` nicht unterstützt, das in der Authentifizierungsanforderung (`AuthnRequest`) definiert ist.
* den Authentifizierungskontext nicht unterstützt.
* das Signieren der Authentifizierungsanforderung erwartet oder einen bestimmten Algorithmus in der Signatur verwendet.

**Lösung**

Überprüfen Sie zur Behebung des Problems die Konfiguration und den Benutzernamen. Stellen Sie sicher, dass der korrekte Authentifizierungskontext und die richtigen Variablen definiert sind. Überprüfen Sie, ob die Anforderung auf eine bestimmte Art signiert werden muss.




### Nicht unterstützte Authentifizierungsanforderung
{: #ts-saml-unsupported-request}

**Problem**

Sie empfangen eine Nachricht bezüglich einer nicht unterstützten Authentifizierungsanforderung.

**Ursache**

Wenn von {{site.data.keyword.appid_short_notm}} eine Authentifizierungsanforderung generiert wird, kann der Authentifizierungskontext verwendet werden, um die Qualität der Authentifizierung und der SAML-Zusicherungen zu überprüfen.

**Lösung**

Zur Behebung des Problems können Sie Ihren Authentifizierungskontext aktualisieren. Von {{site.data.keyword.appid_short_notm}} werden standardmäßig die Authentifizierungsklasse `urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport` und der Abgleich `exact` verwendet. Sie können den Kontextparameter mithilfe der APIs so aktualisieren, dass er für den Anwendungsfall geeignet ist. 




### Fehler beim Signieren der SAML-Anforderung
{: #ts-saml-request-sign-fail}

**Problem**

Sie empfangen eine Fehlernachricht, aus der hervorgeht, dass eine Authentifizierungsanforderung nicht überprüft werden kann.

**Ursache**

{{site.data.keyword.appid_short_notm}} kann zwar so konfiguriert werden, dass die SAML-Authentifizierung (`AuthNRequest`) signiert wird, der Identitätsprovider muss jedoch auch für die entsprechende Konfiguration konfiguriert sein. 

**Lösung**

Gehen Sie wie folgt vor, um das Problem zu lösen:

* Stellen Sie sicher, dass {{site.data.keyword.cloud_notm}} für die Signierung der Authentifizierungsanforderung konfiguriert ist; legen Sie hierzu für den Parameter `signRequest` mithilfe der [API zum Festlegen der SAML-IDP](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Identity%20Providers/mgmt.set_saml_idp) den Wert `true` fest. Sie können überprüfen, ob Ihre Authentifizierungsanforderung signiert ist, indem Sie die Anforderungs-URL anzeigen. Die Signatur ist als Abfrageparameter eingeschlossen. Beispiel: `https://idp.example.org/SAML2/SSO/Redirect?SAMLRequest=request&SigAlg=value&Signature=value&RelayState=token`

* Stellen Sie sicher, dass der Identitätsprovider mit dem korrekten Zertifikat konfiguriert ist. Überprüfen Sie zum Beschaffen des Signierzertifikats die XML-Datei mit den {{site.data.keyword.cloud_notm}}-Metadaten, die Sie über das {{site.data.keyword.cloud_notm}}-Dashboard heruntergeladen haben. Stellen Sie sicher, dass Sie den Schlüssel mit `<KeyDescriptor use="signing">` verwenden. 

* Stellen Sie sicher, dass der Identitätsprovider für die Verwendung von `` als Signieralgorithmus konfiguriert ist.



## Debugging der Verbindung
{: #ts-saml-debug-connection}

Ist die Konfiguration korrekt, aber es tritt trotzdem noch ein Fehler auf? Überprüfen Sie die folgenden hilfreichen Tipps für das Debugging der SAML-Verbindung.
{: shortdesc}


### Wie erfasse ich Anforderung und Antwort meiner SAML-Authentifizierung?
{: #ts-saml-capture}

Es gibt verschiedene Optionen für Browser-Plug-ins, zum Beispiel für [Firefox](https://addons.mozilla.org/en-US/firefox/addon/saml-tracer/) und [Chrome](https://chrome.google.com/webstore/detail/saml-tracer/mpdajninpobndbfcldcmbpnnbhibjmch?hl=en), die zum Erfassen der SAML-Anforderungen und -Antworten verwendet werden können. Möchten Sie kein Plug-in verwenden? Das ist kein Problem. Von Atlassian werden Anweisungen zu einem [manuelleren Extraktionsansatz](https://confluence.atlassian.com/jirakb/how-to-view-a-saml-responses-in-your-browser-for-troubleshooting-872129244.html) bereitgestellt. 


### Ich verstehe die Nachrichten nicht. Wie kann ich sie entschlüsseln?
{: #ts-saml-decode-messages}

Wenn Sie noch Probleme haben, obwohl Sie das SAML-Debugging-Tool verwenden, überprüfen Sie die [SAML-Entwicklertools](https://www.samltool.com/online_tools.php) auf weitere Hilfe zum Entschlüsseln der Nachrichten. Nicht vergessen! Abhängig von der Position beim Abfangen der SAML-Nachrichten kann die Anforderung [URL-codiert](https://www.samltool.com/online_tools.php), [Base64-codiert und komprimiert](https://www.samltool.com/decode.php) oder [verschlüsselt](https://www.samltool.com/decrypt.php) sein.

Verwenden Sie keine Online-Tools zum Entschlüsseln von SAML-Nachrichten wie den SAML-Antworten. Für die Tools ist zum Entschlüsseln der Informationen Zugriff auf den privaten Verschlüsselungsschlüssel erforderlich. Der Schlüssel muss jedoch privat bleiben und der Zugriff auf ihn gesteuert werden. Das in diesem Abschnitt erwähnte Entschlüsselungstool sollte nur zu Fehlerbehebungszwecken verwendet werden.
{: important}

