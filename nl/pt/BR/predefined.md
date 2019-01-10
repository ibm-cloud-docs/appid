---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:pre: .pre}
{:tip: .tip}
{:screen: .screen}

# Atributos de usuário predefinidos
{: #predefined}

Com o {{site.data.keyword.appid_full}}, é possível visualizar informações específicas do provedor de identidade
sobre seus usuários.
{: shortdesc}


## Acessando com o SDK do iOS
{: #ios}

Se novos tokens não forem passados explicitamente para o SDK, o {{site.data.keyword.appid_short_notm}} usará os tokens recebidos pela última vez para recuperar e validar a resposta. Por exemplo, é possível executar o código a seguir após uma autenticação bem-sucedida e o SDK recupera informações adicionais sobre o usuário.

```
AppID.sharedInstance.userProfileManager.getUserInfo { (error: Error?, userInfo: [String: Any]?) in 	guard let userInfo = userInfo, err == nil {
		return // um erro ocorreu 		}
	// informações do usuário recuperadas com sucesso }

```
{: pre}

Como alternativa, é possível passar explicitamente os tokens de acesso e de identidade. O token de identidade é opcional, mas quando passado, ele é usado para validar a resposta de informações do usuário.

```
AppID.sharedInstance.userProfileManager.getUserInfo (accessToken: String, identityToken: String?) { in 	guard let userInfo = userInfo, err == nil {
		return // um erro ocorreu 		}
	// informações do usuário recuperadas com sucesso }
```
{: pre}

</br>

## Acessando com o Android SDK
{: #android}

Se novos tokens não forem passados explicitamente para o SDK, o {{site.data.keyword.appid_short_notm}} usará os tokens recebidos pela última vez para recuperar e validar a resposta. Por exemplo, é possível executar o código a seguir após uma autenticação bem-sucedida e o SDK recupera informações adicionais sobre o usuário.

```
AppID appId = AppID.getInstance ();

appId.getUserProfileManager( ).getUserInfo (new UserProfileResponseListener () {
	@Override 	public void onSuccess(JSONObject userInfo) {
		// informações do usuário recuperadas com sucesso }

	@Override 	public void onFailure(UserInfoException e) {
		// exception occurred }
});
```
{: pre}

Como alternativa, é possível passar explicitamente os tokens de acesso e de identidade. O token de identidade é opcional, mas quando passado, ele é usado para validar a resposta de informações do usuário.

```
AppID appId = AppID.getInstance ();

appId.getUserProfileManager( ).getUserInfo (accessToken, identityToken, new UserProfileResponseListener () {
	@Override 	public void onSuccess(JSONObject userInfo) {
		// retrieved attribute "name" successfully
	}

	@Override 	public void onFailure(UserInfoException e) {
		// exception occurred }
});
```
{: pre}

</br>

## Acessando com o SDK do servidor Node.js
{: #node}


Usando um SDK do lado do servidor, é possível recuperar informações adicionais sobre os seus usuários. É possível chamar o método a seguir usando os tokens de acesso e de identidade armazenados ou é possível passar explicitamente os tokens. O token de identidade é opcional, mas quando passado, ele é usado para validar a resposta de informações do usuário.


```javascript
let userProfileManager = UserProfileManager (options: options)

let accessToken = req.session[WebAppStrategy.AUTH_CONTEXT].accessToken;
let identityToken = req.session[WebAppStrategy.AUTH_CONTEXT].identityToken;


// Retrieve user info and validate against the given identity token
userProfileManager.getUserInfo(accessToken, identityToken).then(function (profile) {
	// retrieved user info successfully
});

// Retrieve user info without validation
userProfileManager.getUserInfo(accessToken).then(function (profile) {
	// retrieved user info successfully
});
```
{: pre}

</br>

## Acessando com o SDK do servidor Swift
{: #swift}

Usando um SDK do lado do servidor, é possível recuperar informações adicionais sobre os seus usuários. É possível chamar o método a seguir usando os tokens de acesso e de identidade armazenados ou é possível passar explicitamente os tokens. O token de identidade é opcional, mas quando passado, ele é usado para validar a resposta de informações do usuário.


```swift
let userProfileManager = UserProfileManager (options: options)

let accessToken = "<access token>"
let identityToken = "<identity token>"

// If identity token is provided (recommended approach), response is validated against the identity token
userProfileManager.getUserInfo(accessToken: accessToken, identityToken: identityToken) { (err, userInfo) in
	guard let userInfo = userInfo, err == nil {
		return // um erro ocorreu 		}
	// informações do usuário recuperadas com sucesso }

// Retrieve the UserInfo without any validation
userProfileManager.getUserInfo(accessToken: accessToken) { (err, userInfo) in
	guard let userInfo = userInfo, err == nil {
		return // um erro ocorreu 		}
	// informações do usuário recuperadas com sucesso }
```
{: pre}

</br>

## Acessando com a API
{: #api}

É possível visualizar as informações adicionais por meio do terminal `/userinfo`.

1. Certifique-se de que você tenha um token de acesso válido com um escopo `openid`. É possível verificar se
o token é válido usando o terminal `/introspect`.

2. Faça uma solicitação para o terminal [`/userinfo`](https://appid-oauth.ng.bluemix.net/swagger-ui/#!/Authorization_Server_V3/userInfo).
  ```
  GET [POST] https://{oauth-server-endpoint}/userinfo
  Authorization: 'Bearer {ACCESS_TOKEN}'
  ```
  {: pre}

  Saída de exemplo:
  ```
  "sub": "cad9f1d4-e23b-3683-b81b-d1c4c4fd7d4c",
  "name": "John Doe",
  "email": "john.doe@gmail.com",
  "picture": "https://lh3.googleusercontent.com/-XdUIqdbhg/AAAAAAAAI/AAAAAAA/42rbcbv5M/photo.jpg",
  "gender": "male",
  "locale": "en",
  "identities": [
      {
          "provider": "google",
          "id": "104560903311317789798",
          "profile": {
              "id": "104560903311317789798",
              "email": "john.doe@gmail.com",
              "verified_email": true,
              "name": "John Doe",
              "given_name": "John",
              "family_name": "Doe",
              "link": "https://plus.google.com/104560903311317789798",
              "picture": "https://lh3.googleusercontent.com/-XdUIqdbhg/AAAAAAAAI/AAAAAAA/42rbcbv5M/photo.jpg",
              "gender": "male",
              "locale": "en",
              "idpType": "google"
          }
      }
  ]
  ```
  {: screen}

3. Verifique se a solicitação `sub` corresponde exatamente à solicitação `sub` no token de identidade. Se elas não corresponderem, não use as informações retornadas. Para saber mais sobre a substituição de token, consulte a
<a href="http://openid.net/specs/openid-connect-core-1_0.html#TokenSubstitution" target="__blank">Especificação OIDC
<img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"> </a>.

Se as mudanças forem feitas por um provedor de identidade externo, você poderá obter as informações atualizadas quando os
usuários efetuarem login novamente. Os novos tokens recuperam os dados mais atualizados.
{: tip}
