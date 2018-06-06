---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# クラウド・ディレクトリーの構成
{: #cd}

クラウド・ディレクトリーを ID プロバイダーとして使用するように、{{site.data.keyword.appid_short_notm}} を構成できます。ユーザーは、E メールとパスワードを使用して、モバイル・アプリや Web アプリに登録し、サインインすることができます。クラウド・ディレクトリーは、クラウド内で管理されるユーザー・レジストリーです。ユーザーが E メールとパスワードを使用してアプリに登録すると、それらのユーザーがユーザー・ディレクトリーに追加されます。この機能により、エンド・ユーザーはアプリ内で自分のアカウントを自由に管理できます。
{: shortdesc}

</br>

## ディレクトリー設定の管理
{: #cd-settings}

アプリでの通知とユーザー制御レベルを構成することができます。 以下の図に示すように、クラウド・ディレクトリーは簡単にセットアップできます。これらの設定は、いつでもサービス・ダッシュボードから更新できます。
{: shortdesc}

![クラウド・ディレクトリーの構成](/images/cloud-directory.png)

1. ID プロバイダーとしてクラウド・ディレクトリーをオンにしたことを確認し、**「登録とパスワード・リセットをユーザーに許可する (Allow users to sign up and reset their password)」**を**「オン (On)」**に設定します。**「オフ (Off)」**に設定されている場合でもコンソールでユーザーを追加できますが、そうするのは開発目的に限られます。
2. 送信者の詳細を構成します。 メッセージの送信元として表示される E メール・アドレス、送信者、ユーザーの返信先を指定します。
**注**: アクション URL を構成するときには、ユーザーにリンクをクリックしてもらうのに十分な時間を設定してください。 ユーザーは、特定のオプション (パスワードのリセットを要求する機能など) を利用する際に、E メールを検証する必要があります。
3. ユーザーが受信する E メールのタイプと、送信者情報を決定します。
4. 用意されているテンプレートを基にカスタマイズし、ユーザーのブランドを表すメッセージや、個人別に設定したメッセージを作成します。詳しくは、[メッセージの管理](/docs/services/appid/cloud-directory.html#cd-messages)を参照してください。
5. GUI の「**ユーザー**」タブで、アプリに登録したユーザーを参照します。

</br>

## メッセージの管理
{: #cd-messages}

テンプレートとは、ユーザーに送信する E メール・メッセージのサンプルです。 テンプレートは、メッセージの内容やレイアウトを更新してカスタマイズできます。 それらのメッセージは、ディレクトリー設定タブで**「オン (On)」**または**「オフ (Off)」**に設定できます。
{: shortdesc}

1. **「メッセージ・タイプ (Message type)」**を選択します。
2. メッセージの内容やデザインを変更して、メッセージをカスタマイズします。 パラメーターを使用して、メッセージをパーソナライズすることができます。 変更後は必ず保存してください。

### メッセージのタイプ

ユーザーに送信できるメッセージにはいくつかのタイプがあります。UI 内にプログラムされているサンプル・メッセージを送信することも、個人に合わせたアプリ操作環境にするためにコンテンツをカスタマイズすることもできます。

<dl>
  <dt>ようこそ</dt>
    <dd><p>ユーザーが登録されたら、アプリケーションのウェルカム・メッセージを E メールで送信できます。 ユーザーを歓迎してアプリを長く使ってもらうために、できるだけ魅力的なメッセージを作成します。</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> すべてのメッセージ・タイプで使用可能なパラメーター </th>
      </thead>
      <tbody>
        <tr>
          <td> %{display.logo} </td>
          <td> ログイン・ウィジェットのために構成したイメージを表示します。 </td>
        </tr>
        <tr>
          <td> %{user.displayName} </td>
          <td> アプリとやり取りするときに使用する、ユーザーが選択した画面名を表示します。 </td>
        </tr>
        <tr>
          <td> %{user.email} </td>
          <td> ユーザーが登録した E メール・アドレスを表示します。 </td>
        </tr>
        <tr>
          <td> %{user.firstName} </td>
          <td> ユーザーが指定した名を表示します。 </td>
        </tr>
        <tr>
          <td> %{user.formattedName} </td>
          <td> ユーザーのフルネームを表示します。 </td>
        </tr>
        <tr>
          <td> %{user.lastName} </td>
          <td> ユーザーが指定した姓を表示します。 </td>
        </tr>
      </tbody>
    </table>
    <p>**注**: パラメーターによってプルされた情報をユーザーが指定していない場合は、ブランクとして表示されます。</p></dd>
  <dt>パスワードを忘れた場合</dt>
    <dd><p>ユーザーは、パスワードを忘れた場合や、何らかの理由でパスワードを更新する必要がある場合に、パスワードのリセットを要求することができます。 その要求に対する E メール応答をカスタマイズすることができます。 ユーザーが変更を要求しても、ユーザーがこのメール内のリンクをクリックするまでパスワードは変更されません。

    </p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> パスワード変更パラメーター </th>
      </thead>
      <tbody>
        <tr>
          <td> %{linkExpiration.hours} </td>
          <td> リンクが有効な時間数を表示します。 </td>
        </tr>
        <tr>
          <td> %{linkExpiration.minutes} </td>
          <td> リンクが有効な分数を表示します。 </td>
        </tr>
        <tr>
          <td> %{resetPassword.code} </td>
          <td> URL の一部としてワンタイム・パスコードを表示します。 ユーザーごとに異なるコードになります。 例: <code>https://appid-wfm.bluemix.net/verify/6574839563478 </code> </td>
        </tr>
        <tr>
          <td> %{resetPassword.link} </td>
          <td> パスワードをリセットするためにユーザーがクリックするリンクを表示します。 </td>
        </tr>
       </tbody>
    </table>
    </dd>
  <dt>検証</dt>
    <dd><p>E メールによってアカウントを検証するようユーザーに要求することができます。 検証を要求することで、アプリに登録されるおそれのある偽アカウントの数を抑制します。 ユーザーが E メールを検証するまでアプリへのアクセスを制限したり、プロファイルの作成対象ユーザーを管理する手段として利用したりできます。</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> 検証メッセージ・パラメーター </th>
      </thead>
      <tbody>
        <tr>
          <td> %{linkExpiration.hours} </td>
          <td> リンクが有効な時間数を表示します。 </td>
        </tr>
        <tr>
          <td> %{linkExpiration.minutes} </td>
          <td> リンクが有効な分数を表示します。 </td>
        </tr>
        <tr>
          <td> %{verify.code} </td>
          <td> ワンタイム検証 URL を表示します。 </td>
        </tr>
        <tr>
          <td> %{verify.link} </td>
          <td> 設定で指定したアクション URL を表示します。 </td>
        </tr>
      </tbody>
    </table>
    </dd>
  <dt>パスワード変更</dt>
    <dd><p>パスワードが更新されたときにユーザーに通知することができます。 これは、ユーザーがパスワードの変更を要求しなかった場合に役立ちます。 ユーザーは適切な手順に沿って、アカウントを再びセキュアにすることができます。

    </p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png"/> パスワード変更パラメーター </th>
      </thead>
      <tbody>
        <tr>
          <td> %{passwordChangeInfo.time} </td>
          <td> 新規パスワードが有効になった時刻を表示します。 </td>
        </tr>
        <tr>
          <td> %{passwordChangeInfo.ipAddress} </td>
          <td> パスワード変更の要求元となった IP アドレスを表示します。 </td>
        </tr>
      </tbody>
    </table>
    </dd>
</dl>
</br>
**注**: {{site.data.keyword.appid_short_notm}} は <a href="https://www.sendgrid.com" target="_blank">SendGrid <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> をメール配信サービスとして使用します。すべての E メールは、単一の SendGrid アカウントを使用して送信されます。

</br>
## 次のステップ
クラウド・ディレクトリーを構成したので、loginwidget のコードをアプリのコードに追加する準備が整いました。以下の画像内の SDK 言語アイコンをクリックして、必要な作業を参照してください。
{: shortdesc}

<img usemap="#options-map" border="0" class="image" id="options" src="images/options.png" width="750" alt="SDK 言語アイコンをクリックして、アプリでクラウド・ディレクトリーを使用する方法の概要を参照します。" style="width:750px;" />
<map name="options-map" id="options-map">
<area href="branded.html#branded-ui-android" alt="Android SDK によるサインイン操作環境の管理" shape="rect" coords="187, 6, 305, 120" />
<area href="branded.html#branded-ui-ios-swift" alt="iOS Swift SDK によるサインイン操作環境の管理" shape="rect" coords="333, 6, 448, 125" />
<area href="branded.html#branded-ui-nodejs" alt="Node.js SDK によるサインイン操作環境の管理" shape="rect" coords="472, 7, 590, 121" />
</map>
