---

copyright:
  years: 2017, 2018
lastupdated: "2018-05-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}

# Protocols and specifications
{: #protocol-spec}

THIS CONTENT IS ONLY IN STAGING AND SHOULD NOT BE PROMOTED TO PRODUCTION!
{: tip}



CONTENT NEEDED


<dl>
  <dt>OAuth 2</dt>
    <dd><a href="https://tools.ietf.org/html/rfc6749" target="_blank">OAuth 2 <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> is open standard protocol that is used to provide app authorization.</dd>
  <dt>Open ID Connect (OIDC)</dt>
    <dd><p><a href="http://openid.net/developers/specs/" target="_blank">OIDC <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> is an authentication layer that works on top of OAuth 2.</p>
    <p>When you use OIDC clients to work with App ID, your service credentials contain the information that you need to create the configuration. In the <strong>Service credentials</strong> tab of the App ID dashboard you can find your credentials. By using the provided <code>oauthserverURL</code> you can form your OIDC endpoint.</p>
    <pre class="codeblock">
    <code>{
      "version": 3,
      "clientId": "e8ac1132-5151-4d8a-934e-0141de8e2b34",
      "secret": "NDE5ZWEzZDYtNjg5Yi00NzQ2LWEwMTctMjM5ODA4NjFhYjBl",
      "tenantId": "5b167052-a79a-40c7-9562-809493c660a6",
      "oauthServerUrl": "https://appid-oauth.ng.bluemix.net/oauth/v3/5b167052-a79a-40c7-9562-809493c660a6",
      "profilesUrl": "https://appid-profiles.ng.bluemix.net"
    }</code></pre>
    <table>
      <tr>
        <th>Endpoint</th>
        <th>Format</th>
      </tr>
      <tr>
        <td>Authorization</td>
        <td>{oauthServerUrl}/authorization</td>
      </tr>
      <tr>
        <td>Token</td>
        <td>{oauthServerUrl}/token</td>
      </tr></dd>
</dl>
