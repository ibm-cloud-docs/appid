---

copyright:
  years: 2017, 2018
lastupdated: "2018-05-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:pre: .pre}
{:tip: .tip}
{:screen: .screen}


# Storing and accessing user information
{: #user-info}

With {{site.data.keyword.appid_full}}, you can build personalized app experiences by taking advantage of information that is publicly available about your users.
{: shortdesc}

When sign-in occurs with an [identity provider](/docs/services/appid/identity-providers.html), information about the user is returned as part of an identity token. Identity tokens represent authentication and contain information about the user such as their name, gender, or location. The service takes that raw identity provider data and normalizes it to return a profile. Other data is stored in the raw form, but can be accessed through the `userinfo` endpoint.

Typically, the returned information takes the following form:

```
// Normalized Profile
{
    "name": "John Doe",
    "email": "john.doe@gmail.com",
    "picture": "https://lh3.googleusercontent.com/-XdUIqdbhg/AAAAAAAAI/AAAAAAA/42rbcbv5M/photo.jpg",
    "gender": "male",
    "locale": "en",
}
```
{: screen}

<table>
  <thead>
    <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding the components</th>
  </thead>
  <tbody>
    <tr>
      <td><code><em>name</em></code></td>
      <td>The user's full name, in a displayable form.</td>
    </tr>
    <tr>
      <td><code><em>email</em></code></td>
      <td>The user's email address.</td>
    </tr>
    <tr>
      <td><code><em>picture</em></code></td>
      <td>A link to the user's profile picture.</td>
    </tr>
    <tr>
      <td><code><em>gender</em></code></td>
      <td>The user's gender as specified by the identity provider.</td>
    </tr>
    <tr>
      <td><code><em>locale</em></code></td>
      <td>The user's location.</td>
    </tr>
  </tbody>
</table>


## Accessing additional information
{: #accessing}

You can view custom or identity provider specific information about your users by using the protected `/userinfo` endpoint.
{: shortdesc}

To view the additional information:

1. Be sure that you have a valid access token with an `openid` scope. You can verify that your token is valid by using the `/introspect` endpoint.

2. Make a request to the `/userinfo` endpoint.
  ```
  GET [POST] https://{oauth-server-endpoint}/userinfo
  Authorization: 'Bearer {ACCESS_TOKEN}'
  ```
  {: pre}

  Example output:
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

3. Verify that the `sub` claim exactly matches the `sub` claim in the identity token. If these do not match, do not use the returned information. To learn more about token substitution, see the <a href="http://openid.net/specs/openid-connect-core-1_0.html#TokenSubstitution" target="blank">OIDC specification <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.

If changes are made by an external identity provider, you can get the updated information when your users log in again. Your new tokens retrieve the most up-to-date data.
{: tip}
