---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-20"

keywords: authentication, authorization, identity, app security, secure, development, identity provider, tokens, customization, lifetime

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


# 認証の管理
{: #managing-idp}

ID プロバイダー (IdP) は、認証によって、モバイル・アプリと Web アプリのセキュリティーを強化します。 {{site.data.keyword.appid_full}} では、1 つ以上の ID プロバイダーを構成して、ユーザーのカスタム・サインイン操作環境を作成できます。
{: shortdesc}


{{site.data.keyword.appid_short_notm}} は、OpenID Connect や SAML などの複数のプロトコルを使用して ID プロバイダーと対話します。 例えば、OpenID Connect は、Facebook や Google などの多くのソーシャル・プロバイダーで使用されているプロトコルです。 <a href="https://www.ibm.com/cloud/blog/setting-ibm-cloud-app-id-azure-active-directory" target="_blank">Azure Active Directory <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> や <a href="https://www.ibm.com/cloud/blog/setting-ibm-cloud-app-id-active-directory-federation-service" target="_blank">Active Directory Federation Service <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> などのエンタープライズ・プロバイダーは、一般に ID プロトコルとして SAML を使用します。 [クラウド・ディレクトリー](/docs/services/appid?topic=appid-cloud-directory)の場合、このサービスは SCIM を使用して ID 情報を検証します。

ソーシャル ID プロバイダーまたはエンタープライズ ID プロバイダーを使用する場合、{{site.data.keyword.appid_short_notm}} にはユーザー・アカウント情報への読み取り権限があります。 このサービスは、ID プロバイダーから返されるトークンとアサーションを使用して、ユーザーが本人であることを検証します。 このサービスには情報への書き込み権限がないため、ユーザーは選択した ID プロバイダーを使用して、パスワードのリセットなどのアクションを実行する必要があります。 例えば、ユーザーが Facebook を使用してアプリにサインインした後にパスワードを変更する場合は、`www.facebook.com` にアクセスしてそれを行う必要があります。

[クラウド・ディレクトリー](/docs/services/appid?topic=appid-cloud-directory)を使用する場合、{{site.data.keyword.appid_short_notm}} が ID プロバイダーになります。 このサービスは、レジストリーを使用してユーザー ID を検証します。 {{site.data.keyword.appid_short_notm}} はプロバイダーであるため、ユーザーは、パスワードのリセットなどの拡張機能をアプリ内で直接利用できます。

アプリケーション識別の作業を行いますか? [アプリケーション識別](/docs/services/appid?topic=appid-app)を参照してください。
{: tip}

このサービスで使用するために構成できるプロバイダーは、いくつかあります。 次の表を参照して、オプションを確認してください。

<table>
  <tr>
    <th>プロバイダー</th>
    <th>タイプ</th>
    <th>説明</th>
  </tr>
  <tr>
    <td>[Cloud Directory](/docs/services/appid?topic=appid-cloud-directory)</td>
    <td>管理対象レジストリー</td>
    <td>独自のユーザー・レジストリーをクラウドで保守できます。 ユーザーがアプリに登録すると、ユーザーのディレクトリーに追加されます。 このオプションにより、ユーザーはアプリ内で自分のアカウントをより自由に管理できます。</td>
  </tr>
  <tr>
    <td>[SAML](/docs/services/appid?topic=appid-enterprise#enterprise)</td>
    <td>エンタープライズ</td>
    <td>エンド・ユーザー用のシングル・サインオン操作環境を作成できます。</td>
  </tr>
  <tr>
    <td>[Facebook](/docs/services/appid?topic=appid-social#facebook)</td>
    <td>ソーシャル</td>
    <td>エンド・ユーザーは、Facebook の資格情報を使用してアプリにサインインできます。</td>
  </tr>
  <tr>
    <td>[Google+](/docs/services/appid?topic=appid-social#google)</td>
    <td>ソーシャル</td>
    <td>エンド・ユーザーは、Google の資格情報を使用してアプリにサインインできます。</td>
  </tr>
  <tr>
    <td>[カスタム](/docs/services/appid?topic=appid-custom-identity#custom-identity)</td>
    <td> </td>
    <td>提供されているどのオプションもお客様固有のニーズに合わない場合は、{{site.data.keyword.appid_short_notm}} で作業するための独自の識別フローを構成できます。</td>  
  </tr>
</table>

## プロバイダーの管理
{: #managing-providers}

ID プロバイダーは、ユーザー、機能 ID、アプリケーションなどのエンティティーに関する情報を作成および管理します。 このプロバイダーは、パスワードなどの資格情報を使用してエンティティーの同一性を検証します。 その後、IdP は ID 情報を別のサービス・プロバイダーに送信します。 ID プロバイダーがエンティティーを認証するので、{{site.data.keyword.appid_short_notm}} はそれを許可し、アプリへのアクセス権限を付与できるようになります。
{: shortdesc}

ID プロバイダーを管理するには、以下のようにします。

1. サービス・ダッシュボードにナビゲートします。
2. ナビゲーションの**「ID プロバイダー」**セクションで、**「管理」**ページを選択します。
3. **「ID プロバイダー」**タブで、使用するプロバイダーを**「オン」**に設定します。
4. オプション:**「匿名ユーザー (Anonymous users)」**をオフにするか、それともデフォルト (**「オン」**) のままにするかを決定します。 **「オン」**に設定すると、アプリとの対話を開始した時点から、ユーザー属性がユーザーに関連付けられます。 識別されたユーザーになるための手順について詳しくは、[段階的な認証](/docs/services/appid?topic=appid-anonymous#progressive)を参照してください。

{{site.data.keyword.appid_short_notm}} には、Facebook と Google+ の初期セットアップに役立つデフォルトの資格情報が用意されています。 資格情報の使用は、1 インスタンスあたり毎日 100 回に制限されています。 これらは IBM の資格情報なので、これを使用するのは開発のときだけにしてください。 アプリを公開する前に、自分の資格情報になるように構成を更新してください。
{: tip}


## リダイレクト URI の追加
{: #add-redirect-uri}

リダイレクト URI は、アプリのコールバック・エンドポイントです。 サインイン・フローで、{{site.data.keyword.appid_short_notm}} は、許可ワークフローにクライアントが参加することを許可する前に、URI を検証します。これは、フィッシング攻撃と認可コード漏えいを防ぐのに役立ちます。 URI を登録することで、その URI が信頼できる URI であり、ユーザーをリダイレクトしてよいことを {{site.data.keyword.appid_short_notm}} に認識させます。

信頼できるアプリケーションの URI だけを登録するようにしてください。
{: note}


1. **「認証設定 (Authentication Settings)」**をクリックすると、URI とトークンの構成オプションが表示されます。

2. **「Web リダイレクト URI の追加」**フィールドに URI を入力します。 リダイレクトが正常に行われるためには、各 URI は `http://` または `https://` で始まり、照会パラメーターを含めた絶対パスが含まれていなければなりません。 URI の形式設定については、次の表にあるいくつかの例を確認してください。

  <table>
    <tr>
      <th>タイプ</th>
      <th>サンプル URI</th>
    </tr>
    <tr>
      <td>カスタム・ドメイン</td>
      <td><code>http://mydomain.net/myapp2path/appid_callback</code></td>
    </tr>
    <tr>
      <td>Ingress サブドメイン</td>
      <td><code>https://mycluster.us-south.containers.appdomain.cloud/myapp1path/appid_callback</code></td>
    </tr>
    <tr>
      <td>ログアウト</td>
      <td><code>http://mydomain.net/myapp2path/appid_logout</code></td>
    </tr>  
  </table>

3. **「Web リダイレクト URI の追加 (Add web redirect URIs)」**ボックス内の **+** 記号をクリックします。

4. 考えられる URI をすべてリストに追加するまで、ステップ 1 から 3 を繰り返します。



リダイレクト URI をどこで取得できるかわかりませんか? 以下の短いビデオで、取得場所およびリストへの追加方法を確認してください。

<iframe class="embed-responsive-item" id="redirecturi" title="{{site.data.keyword.appid_short_notm}}: How to fix invalid redirect URI" type="text/html" width="640" height="390" src="//www.youtube.com/embed/6hxqbvpc054?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>



## トークン存続期間の構成
{: #idp-token-lifetime}

ユーザーがサインインするたびに、トークンの存続時間が再び始まります。 例えば、リフレッシュ・トークン存続時間を 10 日に設定したとします。 ユーザーが初めてサインインすると、アクセス・トークンとリフレッシュ・トークンが作成されます。 数日後 (例えば 3 日後) にユーザーがアプリを再度使用する場合は、再度サインインする必要はありません。 しかし、ユーザーが初回のサインインから 12 日間待ってからアプリを再度使用する場合は、再度サインインする必要があり、そのときにトークンのセットがユーザーに関連付けられます。 トークンについて詳しくは、[トークンについて](/docs/services/appid?topic=appid-tokens#tokens)を確認してください。

1. ユーザー対話なしでサインインできるようにするには、**「リフレッシュ・トークン」**を**「オン」**に設定します。

2. リフレッシュ・トークンの存続期間を設定します。 有効期限は日単位で設定され、1 から 90 の範囲の値を使用できます。 数値が小さいほど、ユーザーはより頻繁にサインインする必要があります。

3. アクセス・トークンの存続期間を設定します。 有効期限は分単位で設定され、5 から 1440 の範囲の値を使用できます。 値が小さいほど、トークンの盗用に対する保護を強化できます。

4. 匿名トークンの存続期間を設定します。 [匿名トークン](/docs/services/appid?topic=appid-anonymous#progressive)は、ユーザーがアプリとの対話を開始するときにユーザーに割り当てられます。 ユーザーがサインインすると、匿名トークン内の情報が、そのユーザーに関連付けられたトークンに転送されます。 有効期限は日単位で設定され、1 から 90 までの値を使用できます。


トークンの有効期限を設定すると、ソーシャルとエンタープライズの両方を含め、構成したすべてのプロバイダーに適用されます。
{: tip}
