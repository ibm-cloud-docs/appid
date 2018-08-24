---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:tip: .tip}

# エンタープライズ ID プロバイダーの構成
{: #enterprise}

既存のユーザー・リポジトリーがあり、内部システムでユーザーを認証するための認定された方式が既に存在する場合、エンタープライズ ID プロバイダーを使用するように {{site.data.keyword.appid_full}} サービスを構成できます。
{: shortdesc}

## SAML についての説明
{: #saml}

SAML は、ユーザーの身分を表明する ID プロバイダーとユーザー ID 情報を取り込むサービス・プロバイダーの間で、認証データと許可データを交換するためのオープン・スタンダードです。
{: shortdesc}

機能する仕組み

{{site.data.keyword.appid_short_notm}} は、サービス・プロバイダーとして機能し、Active Directory Federation Services などのサード・パーティー・プロバイダーに対するシングル・サインオン (SSO) ログインを開始します。 <a href="http://saml.xml.org/saml-specifications" target="_blank">SAML <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> プロトコルは、さまざまなプロファイルやバインド・オプションをサポートします。 {{site.data.keyword.appid_short_notm}} は、HTTP Post バインディングを使用して Web ブラウザー SSO プロファイルをサポートします。

### SAML アサーションおよび識別トークンの請求

SAML アサーションは、1 つ以上のステートメントを入れた情報のパッケージです。 アサーションには許可決定が含まれ、ユーザーに関する ID 情報も含まれることがあります。

ユーザーが ID プロバイダーを使用してサインインすると、そのプロバイダーはアサーションを {{site.data.keyword.appid_short_notm}} に送信します。 {{site.data.keyword.appid_short_notm}} は、SAML アサーションで返されたユーザー ID 情報を OIDC トークン請求としてアプリに伝搬します。 SAML 属性は、識別トークンに追加される以下のいずれかの OIDC 請求に対応するものでなければなりません。

以下の請求を追加できます。
* `name`
* `email`
* `locale`
* `picture`

どの標準名とも対応しない残りの SAML 属性要素は無視されます。 これらの値の 1 つ以上がプロバイダー側で変更された場合、新しい値は、ユーザーが再びログインした後でないと使用できるようになりません。

## 外部 SAML ID プロバイダーと連動するようにアプリを構成する
{: #configuring-saml}

Security Assertion Markup Language (SAML) ID プロバイダーを使用するように {{site.data.keyword.appid_short_notm}} サービスを構成できます。
{: shortdesc}

特定の SAML ID プロバイダーの使用方法の手順については、{{site.data.keyword.appid_short_notm}} のセットアップ手順に関する、[Ping One ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-ping-one/)、[Azure Active Directory ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-azure-active-directory/)、または [Active Directory Federation Service ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/blogs/bluemix/2018/03/setting-ibm-cloud-app-id-active-directory-federation-service/) のブログ投稿を参照してください。
{: tip}

### ID プロバイダーへのメタデータの提供

アプリを構成するには、SAML 互換の ID プロバイダーに情報を提供する必要があります。 その情報はメタデータ XML ファイルを介して交換されます。そこには、信頼関係の確立に使用される構成データも含まれています。

1. {{site.data.keyword.appid_short_notm}} ダッシュボードの**「管理」**タブで、**「SAML 2.0」**を**「オン (On)」**に設定します。 その後、**「編集」**をクリックして SAML 設定を構成します。
2. **「SAML メタデータ・ファイルのダウンロード (Download SAML Metadata file)」**をクリックします。 ID プロバイダーは、以下の情報がファイルにあることを想定しています。
  <table>
    <tr>
      <th> 変数 </th>
      <th> 説明 </th>
    </tr>
    <tr>
      <td><code>EntityID</code></td>
      <td>{{site.data.keyword.appid_short_notm}} が SAML 要求を発行したことを ID プロバイダーに通知するための ID。</td>
    </tr>
    <tr>
      <td><code>Location URL</code></td>
      <td>ユーザーの認証が正常に終了した後に ID プロバイダーが SAML アサーションを送る場所。</td>
    </tr>
    <tr>
      <td><code>Binding</code></td>
      <td>ID プロバイダーが SAML 応答を送信する方法についての指示。</td>
    </tr>
    <tr>
      <td><code>NameID Format</code></td>
      <td>ID プロバイダーがアサーションのサブジェクトの中で送信する必要のある ID 形式を ID プロバイダーが判別する方法。 {{site.data.keyword.appid_short_notm}} がユーザーを識別する方法。</td>
    </tr>
    <tr>
      <td><code>WantAssertionsSigned</code></td>
      <td>アサーションに署名する必要があるかどうかを ID プロバイダーが検査する方法。 このサービスはアサーションが署名されていることを想定していますが、暗号化されたアサーションはサポートしていません。</td>
    </tr>
  </table>

3. ID プロバイダーにデータを提供します。 ID プロバイダーがメタデータ・ファイルのアップロードをサポートしている場合は、そうすることができます。 サポートしていない場合は、プロパティーを手動で構成してください。 すべての ID プロバイダーが同じプロパティーを使用するとは限らないので、それらすべてを使用しない場合でも問題ありません。

プロパティーの名前は ID プロバイダーの間で異なることがあります。
{: tip}

### {{site.data.keyword.appid_short_notm}} へのメタデータの提供

ID プロバイダーからデータを取得して、それを {{site.data.keyword.appid_short_notm}} に提供する必要があります。

1. {{site.data.keyword.appid_short_notm}} ダッシュボードの**「SAML 2.0」**タブに移動します。 ID プロバイダーから取得した以下のメタデータを**「SAML IdP からのメタデータの提供 (Provide Metadata from SAML IdP)」**セクションに入力します。
  <table>
    <tr>
      <th> 変数 </th>
      <th> 説明 </th>
    </tr>
    <tr>
      <td><code>Sign-in URL</code></td>
      <td>認証のためにユーザーがリダイレクトされる URL。 SAML ID プロバイダーによってホストされます。</td>
    </tr>
    <tr>
      <td><code>Entity ID</code></td>
      <td>SAML ID プロバイダーのグローバルな固有名。</td>
    </tr>
    <tr>
      <td><code>Signing certificate</code></td>
      <td>SAML ID プロバイダーによって発行された証明書。 SAML アサーションの署名と検証のために使用されます。 プロバイダーごとに異なりますが、署名証明書を ID プロバイダーからダウンロードできる可能性があります。 証明書は <code>.pem</code> 形式でなければなりません。</td>
    </tr>
  </table>

2. オプション: 1 次証明書で署名検証に失敗した場合に使用される**「2 次証明書 (Secondary certificate)」**を入力します。 同じ署名鍵をそのまま使用する場合、証明書の認証が期限切れを理由に {{site.data.keyword.appid_short_notm}} でブロックされることはありません。

3. **「プロバイダー名 (Provider Name)」**を更新して、**「保存」**をクリックします。 デフォルト名は SAML です。


### 構成のテスト

SAML ID プロバイダーと {{site.data.keyword.appid_short_notm}} の間で構成をテストできます。

1. 構成を保存したことを確認します。
2. {{site.data.keyword.appid_short_notm}} ダッシュボードの**「SAML 2.0」**タブに移動して、**「テスト」**をクリックします。 新しいタブが開きます。
3. ID プロバイダーによって既に認証されているユーザーを使用してログインします。
4. フォームの入力を完了すると、別のページにリダイレクトされます。
  * 認証に成功した場合: {{site.data.keyword.appid_short_notm}} と ID プロバイダーの間の接続は正常に機能しています。 ページには、有効な[アクセス・トークンと識別トークン](/docs/services/appid/authorization.html#key-concepts)が表示されます。
  * 認証に失敗した場合: 接続は切断されています。 ページには、エラーと SAML 応答 XML ファイルが表示されます。
