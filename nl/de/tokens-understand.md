---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-11"

keywords: authentication, authorization, identity, app security, secure, access, tokens

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



# Informationen zu Tokens
{: #tokens}

Wenn ein Benutzer erfolgreich authentifiziert wurde, empfängt die Anwendung Tokens von {{site.data.keyword.appid_short_notm}}. Der Service verwendet drei Haupttypen von Tokens, um den Authentifizierungsprozess durchzuführen.
{: shortdesc}


## Zugriffstokens
{: #access}

Zugriffstokens stellen die Autorisierung dar und ermöglichen die Kommunikation mit [Back-End-Ressourcen](/docs/services/appid?topic=appid-backend), die durch Autorisierungsfilter geschützt sind, die von {{site.data.keyword.appid_short}} festgelegt werden. Das Token entspricht den JOSE-Spezifikationen (JOSE = JavaScript Object Signing and Encryption). Das Token wird als <a href="https://jwt.io/introduction/" target="blank">JSON Web Token<img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> formatiert und mit einem JSON Web Key signiert, der den RS256-Algorithmus verwendet.

Beispieltoken:
  ```
  Header: {
    "alg": "RS256",
    "typ": "JWT",
    "kid": "appId-39a37f57-a227-4bfe-a044-93b6e6050a61-2018-08-02T11:57:43.401",
    "ver": 4
  }
  Payload:
  {
    "iss": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61",
    "exp": 1551903163,
    "aud": [
      "968c2306-9aef-4109-bc06-4f5ed6axi24a"
    ],
    "sub": "2b96cc04-eca5-4122-a8de-6e07d14c13a5",
    "email_verified": true,
    "amr": [
      "cloud_directory"
    ],
    "iat": 1551899553,
    "tenant": "39a37f57-a227-4bfe-a044-93b6e6050a61",
    "scope": "openid appid_default appid_readprofile appid_readuserattr appid_writeuserattr appid_authenticated"
  }
  ```
  {: screen}

## Was sind Identitätstokens?
{: #identity}

Identitätstokens stellen die Authentifizierung dar und enthalten Informationen zum Benutzer. Sie können Informationen zum Benutzer wie Name, E-Mail-Adresse, Geschlecht und Ort enthalten. Ein Token kann auch eine URL zu einem Bild des Benutzers zurückgeben. Das Token wird als <a href="https://jwt.io/introduction/" target="blank">JSON Web Token<img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> formatiert und mit einem JSON Web Key signiert, der den RS256-Algorithmus verwendet.

Beispieltoken:
  ```
  Header: {
    "alg": "RS256",
    "typ": "JWT",
    "kid": "appId-39a37f57-a227-4bfe-a044-93b6e6050a61-2018-08-02T11:57:43.401",
    "ver": 4
  }
  Payload:
  {
    "iss": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6050a61",
    "aud": [
      "968c2306-9aef-4109-bc06-4f5ed6axi24a"
    ],
    "exp": 1551903163,
    "tenant": "39a37f57-a227-4bfe-a044-93b6e6050a61",
    "iat": 1551899553,
    "email": "appid155@mailinator.com",
    "name": "appid155@mailinator.com",
    "sub": "2b96cc04-eca5-4122-a8de-6e07d14c13a5",
    "email_verified": true,
    "identities": [
      {
        "provider": "cloud_directory",
        "id": "118c0278-3526-4954-876b-cf70eb88efa2"
      }
    ],
    "amr": [
      "cloud_directory"
    ]
  }
  ```
  {: screen}


Identitätstokens enthalten nur einen Teil der Benutzerinformationen. Wenn Sie alle Informationen anzeigen möchten, die vom Identitätsprovider zur Verfügung gestellt werden, können Sie den [Endpunkt /userinfo](/docs/services/appid?topic=appid-predefined-attributes#predefined-access-api) verwenden.

## Was sind Aktualisierungstokens?
{: #refresh}

{{site.data.keyword.appid_short}} ermöglicht es, neue Zugriffs- und Identitätstokens ohne erneute Authentifizierung anzufordern - entsprechend der Definition in <a href="http://openid.net/specs/openid-connect-core-1_0.html#RefreshTokens" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>. Ein Aktualisierungstoken kann verwendet werden, um das Zugriffstoken zu erneuern, sodass ein Benutzer keine Maßnahmen zur Anmeldung ergreifen muss (z. B. Angabe von Anmeldeinformationen). Ähnlich wie Zugriffstokens enthalten auch Aktualisierungstokens Daten, die es {{site.data.keyword.appid_short_notm}} ermöglichen festzustellen, ob Sie berechtigt sind. Diese Tokens haben jedoch den Typ 'Opaque'.

Aktualisierungstokens sind so konfiguriert, dass sie eine längere Lebensdauer aufweisen als ein reguläres Zugriffstoken. Wenn also die Gültigkeit eines Zugriffstokens abläuft, ist das Aktualisierungstoken weiterhin gültig und kann zum Verlängern des Zugriffstokens verwendet werden. Aktualisierungstokens von {{site.data.keyword.appid_short_notm}} können für 1 bis 90 Tage konfiguriert werden. Um die Vorteile von Aktualisierungstokens vollständig zu nutzen, behalten Sie die Tokens für ihre gesamte Lebensdauer bei oder bis sie erneuert werden. Ein Benutzer kann mit einem Aktualisierungstoken alleine nicht direkt auf Ressourcen zugreifen, d. h. eine längere Verwendung ist sicherer als dies bei Zugriffstokens der Fall wäre. Es empfiehlt sich, Aktualisierungstokens sicher von dem Client speichern zu lassen, von dem sie empfangen wurden, und sie nur an den Autorisierungsserver zu senden, der sie ausgegeben hat.

Ein zusätzlicher Vorteil ist, dass {{site.data.keyword.appid_short_notm}} auch sein Aktualisierungstoken - und sein Ablaufdatum - verlängert, wenn das Zugriffstoken erneuert wird, sodass der Benutzer angemeldet bleiben kann, solange sie in irgendeiner Weise aktiv sind, bevor das aktuelle Aktualisierungstoken abläuft. Wenn Sie andererseits Aktualisierungstokens verwenden wollen, den Benutzer aber zwingen möchten, sich in regelmäßigen Abständen anzumelden, könnte Ihre App nur die Aktualisierungstokens verwenden, die zurückgegeben werden, wenn sich der Benutzer mit seinen Berechtigungsnachweisen anmeldet. Es wird jedoch empfohlen, immer das neueste Aktualisierungstoken zu verwenden, das von {{site.data.keyword.appid_short_notm}} empfangen wurde. Lesen Sie hierzu die Informationen in den <a href="https://tools.ietf.org/html/rfc6749#page-47" target="_blank">OAuth 2.0-Spezifikationen <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>.


Obwohl diese Tokens den Anmeldeprozess rationeller gestalten können, sollte Ihre App nicht von ihnen abhängig sein, da sie jederzeit widerrufen werden können (z. B. wenn Sie den Eindruck haben, dass Ihre Aktualisierungstokens nicht mehr sicher sind). Wenn Sie ein Aktualisierungstoken widerrufen müssen, gibt es hierfür zwei Methoden. Wenn Sie über das Aktualisierungstoken verfügen, können Sie es auf der Basis von <a href="https://tools.ietf.org/html/rfc7009#section-2" target="_blank">RFC7009 <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> widerrufen. Wenn Sie über die Benutzer-ID verfügen, können Sie alternativ das Aktualisierungstoken mit der <a href="https://us-south.appid.cloud.ibm.com/swagger-ui/#/" target="_blank">Management-API <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> widerrufen. Weitere Informationen zum Zugriff auf die Management-API finden Sie unter [Servicezugriff verwalten](/docs/services/appid?topic=appid-service-access-management#service-access-management).

Beispiele für das Arbeiten mit Aktualisierungstokens und ihre Verwendung zur Implementierung einer Remember-me-Funktionalität finden Sie unter [Lernprogramm zur Einführung](/docs/services/appid?topic=appid-getting-started#getting-started).


## Woher stammen die Tokens?
{: #where}

Tokens werden vom {{site.data.keyword.appid_short_notm}}-OAuth-Server ausgegeben und als [JSON Web Token (JWT)](https://jwt.io/introduction/) formatiert. Die Tokens wurden mit einem [JSON Web Key (JWK)](https://tools.ietf.org/html/rfc7517) mit dem RS256-Algorithmus signiert.

## Was geschieht mit den Informationen, die das Token enthält?
{: #contains}

Das Zugriffstoken enthält eine Reihe von JWT-Standardanforderungen (sog. Claims) und eine Reihe von {{site.data.keyword.appid_short_notm}}-spezifischen Claims (z. B. eine Tenant-ID). Das Identitätstoken enthält benutzerspezifische Informationen. Die Informationen in den Tokens werden als Claims als Teil eines [Benutzerprofils](/docs/services/appid?topic=appid-user-profile#user-profile) gespeichert.

## Wie werden Tokens empfangen?
{: #received}

Die Tokens werden von Ihrer App nach einer erfolgreichen Authentifizierung empfangen. Sie können die Tokens verwenden, um Informationen zur Benutzerautorisierung und -authentifizierung abzurufen. Das Zugriffstoken kann verwendet werden, um Zugriff auf geschützte Ressourcen zu erhalten, indem eine Anforderung an die Ressource gesendet wird. In der Anforderung wird das Zugriffstoken im [Bearer-Authentifizierungsschema](https://tools.ietf.org/html/rfc6750#page-5) beschrieben. Um die Tokens zu extrahieren, muss Ihre App den Header syntaktisch analysieren.

Beispielanforderung:

  ```
  GET /resource HTTP/1.1
  Host: server.example.com
  Authorization: Bearer  mF_9.B5f-4.1JqM mF_9.B5f-4.1JqM
  ```
  {: screen}

## Wie werden Tokens festgelegt?
{: #set}

Tokenkonfigurationen können über das {{site.data.keyword.appid_short_notm}}-Dashboard aktiviert und inaktiviert werden. Weitere Informationen zu den Konfigurationsoptionen finden Sie in [Tokens verwalten](/docs/services/appid?topic=appid-managing-idp#managing-idp).
