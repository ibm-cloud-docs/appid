---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-09"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# クラウド・ディレクトリーの構成
{: #cd}

ユーザーは、E メールまたはユーザー名とパスワードを使用して、モバイル・アプリや Web アプリに登録し、サインインすることができます。 クラウド・ディレクトリーは、クラウド内で管理されるユーザー・レジストリーです。 ユーザーがアプリに登録すると、ユーザーのディレクトリーに追加されます。 この機能により、ユーザーはアプリ内で自分のアカウントを自由に管理できます。
{: shortdesc}

</br>

## ディレクトリー設定の管理
{: #cd-settings}

アプリでの通知とユーザー制御レベルを構成することができます。 以下の図に示すように、クラウド・ディレクトリーは簡単にセットアップできます。 これらの設定は、いつでもサービス・ダッシュボードから更新できます。
{: shortdesc}


![クラウド・ディレクトリーの構成](/images/cloud-directory.png)
図. Cloud Directory の構成手順


1. ID プロバイダーとして Cloud Directory をオンにしたことを確認し、**「登録とパスワード・リセットをユーザーに許可する (Allow users to sign up and reset their password)」**を**「オン (On)」**に設定します。 **「オフ (Off)」**に設定されている場合でも、開発目的であれば、コンソールでユーザーを追加できます。
2. ユーザーが指定のユーザー名と E メールのどちらで認証を行うかを選択します。このフィールドは、サインアップ、サインイン、およびパスワード忘れの各フローで使用されます。ユーザーがユーザー名とパスワードでサインインできるようにする場合、ユーザー名は 8 文字以上で、スペース、コンマ、スラッシュを含まないものとします。**注:** Cloud Directory にユーザーがいない場合にのみ、オプションを切り替えることができます。
3. 送信者の詳細を構成します。 メッセージの送信元として表示される E メール・アドレス、送信者、ユーザーの返信先を指定します。
  アクション URL を構成するときは、ユーザーがリンクをクリックできるだけの十分な時間を確保してください。 ユーザーは、自分の E メールが特定のオプション (パスワードの再設定を要求する機能など) を備えていることを検証する必要があります。
  {: tip}
4. ユーザーが受信する E メールのタイプと、送信者情報を決定します。
5. 用意されているテンプレートを使用して、ユーザーのブランドを表すメッセージや個人別に設定したメッセージでメッセージをカスタマイズします。 詳しくは、[メッセージの管理](/docs/services/appid/cloud-directory.html#cd-messages)を参照してください。
6. GUI の「**ユーザー**」タブで、アプリに登録したユーザーを参照します。

1 人のユーザーが 1 分間にサインインできる回数は 5 回までです。6 回目の試行が行われると、エラーが表示されます。
{: tip}

</br>

## メッセージの管理
{: #cd-messages}

テンプレートとは、ユーザーに送信する E メール・メッセージのサンプルです。 テンプレートは、メッセージの内容やレイアウトを更新してカスタマイズできます。
{: shortdesc}

1. ダッシュボードの**「ID プロバイダー」>「クラウド・ディレクトリー」>「設定」**タブで、送信するメッセージを**「オン」**に設定します。

2. オプション: <a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/updateLocalization" target="_blank">言語管理 API <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を使用して、メッセージ・テンプレート内で使用する別の言語を設定します。サポートされる言語コードのリストについては、[サポートされる言語](#languages)を参照してください。

3. **「メッセージ・タイプ (Message type)」**を選択します。

4. メッセージの内容やデザインを変更して、メッセージをカスタマイズします。 パラメーターを使用して、メッセージをパーソナライズすることができます。 変更後は必ず保存してください。

### メッセージのタイプ

いくつかのタイプのメッセージをユーザーに送信できます。 UI 内にプログラムされているサンプル・メッセージを送信することも、個人に合わせたアプリ操作環境にするためにコンテンツをカスタマイズすることもできます。

<dl>
  <dt>ようこそ</dt>
    <dd><p>ユーザーが登録されたら、アプリケーションのウェルカム・メッセージを E メールでユーザーに送信できます。 ユーザーを歓迎してアプリを長く使ってもらうために、できるだけ魅力的なメッセージを作成します。</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="詳細情報アイコン"/> すべてのメッセージ・パラメーター </th>
      </thead>
      <tbody>
        <tr>
          <td><code>%{display.logo}</code></td>
          <td> ログイン・ウィジェットのために構成したイメージを表示します。 </td>
        </tr>
        <tr>
          <td><code>%{user.displayName}</code></td>
          <td> アプリとやり取りするときに使用する、ユーザーが選択した画面名を表示します。 </td>
        </tr>
        <tr>
          <td><code>%{user.email}</code></td>
          <td> ユーザーが登録した E メール・アドレスを表示します。 </td>
        </tr>
        <tr>
          <td><code>%{user.username}</code></td>
          <td> 認証方式がユーザー名とパスワードに設定されているとき、ユーザーが指定したユーザー名を表示します。</td>
        </tr>
        <tr>
          <td><code>%{user.firstName}</code></td>
          <td> ユーザーが指定した名を表示します。 </td>
        </tr>
        <tr>
          <td><code>%{user.formattedName}</code></td>
          <td> ユーザーのフルネームを表示します。 </td>
        </tr>
        <tr>
          <td><code>%{user.lastName}</code></td>
          <td> ユーザーが指定した姓を表示します。 </td>
        </tr>
      </tbody>
    </table>
    <p>**注**: パラメーターによってプルされた情報をユーザーが指定していない場合は、ブランクとして表示されます。</p></dd>
  <dt>パスワードを忘れた場合</dt>
    <dd><p>ユーザーは、パスワードを忘れた場合や、何らかの理由でパスワードを更新する必要がある場合に、パスワードの再設定を要求することができます。 その要求に対する E メール応答をカスタマイズすることができます。 ユーザーが変更を要求しても、ユーザーがこのメール内のリンクをクリックするまでパスワードは変更されません。</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="詳細情報アイコン"/> パスワード変更パラメーター </th>
      </thead>
      <tbody>
        <tr>
          <td><code>%{linkExpiration.hours}</code></td>
          <td> リンクが有効な時間数を表示します。 </td>
        </tr>
        <tr>
          <td><code>%{linkExpiration.minutes}</code></td>
          <td> リンクが有効な分数を表示します。 </td>
        </tr>
        <tr>
          <td><code>%{resetPassword.code}</code></td>
          <td> URL の一部としてワンタイム・パスコードを表示します。 ユーザーごとに異なるコードになります。 例: <code>https://appid-wfm.bluemix.net/verify/6574839563478 </code> </td>
        </tr>
        <tr>
          <td><code>%{resetPassword.link}</code></td>
          <td> パスワードをリセットするためにユーザーがクリックするリンクを表示します。 </td>
        </tr>
       </tbody>
    </table>
    </dd>
  <dt>検証</dt>
    <dd><p>E メールによってアカウントを検証するようユーザーに要求することができます。 検証を要求することで、アプリに登録されるおそれのある偽アカウントの数を抑制します。 ユーザーが E メールを検証するまでアプリへのアクセスを制限したり、プロファイルの作成対象ユーザーを管理する手段として利用したりできます。</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="詳細情報アイコン"/> 検証メッセージ・パラメーター </th>
      </thead>
      <tbody>
        <tr>
          <td><code>%{linkExpiration.hours}</code></td>
          <td> リンクが有効な時間数を表示します。 </td>
        </tr>
        <tr>
          <td><code>%{linkExpiration.minutes}</code></td>
          <td> リンクが有効な分数を表示します。 </td>
        </tr>
        <tr>
          <td><code>%{verify.code}</code></td>
          <td> ワンタイム検証 URL を表示します。 </td>
        </tr>
        <tr>
          <td><code>%{verify.link}</code></td>
          <td> 設定で指定したアクション URL を表示します。 </td>
        </tr>
      </tbody>
    </table>
    </dd>
  <dt>パスワード変更</dt>
    <dd><p>パスワードが更新されたときにユーザーに通知することができます。 これは、ユーザーがパスワードの変更を要求しなかった場合に役立ちます。 ユーザーは適切な手順に沿って、アカウントを再びセキュアにすることができます。</p>
    <table>
      <thead>
        <th colspan=2><img src="images/idea.png" alt="詳細情報アイコン"/> パスワード変更パラメーター </th>
      </thead>
      <tbody>
        <tr>
          <td><code>%{passwordChangeInfo.time}</code></td>
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
**注**: {{site.data.keyword.appid_short_notm}} は <a href="https://www.sendgrid.com" target="_blank">SendGrid <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> をメール配信サービスとして使用します。 すべての E メールは、単一の SendGrid アカウントを使用して送信されます。


</br>

## パスワード・ストレングスの管理
{: #strength}

Cloud Directory で使用可能なパスワードの要件を設定できます。
{: shortdesc}

強力なパスワードを使用すると、誰かがそのパスワードを手動または自動化された方法で推測することが困難または不可能になります。パスワード・ストレングスは、正規表現ストリングとして設定されます。

一般的なパスワード・ストレングスの例:

- 少なくとも 8 文字でなければなりません。 正規表現の例: `^.{8,}$`
- 1 つの数字、1 つの小文字、および 1 つの大文字が含まれている必要があります。正規表現の例: `^(?:(?=.*\\d)(?=.*[a-z])(?=.*[A-Z]).*)$`
- 英字と数字だけが含まれている必要があります。正規表現の例: `^[A-Za-z0-9]*$`
- 少なくとも 1 固有文字でなければなりません。 正規表現の例: `^(\w)\w*?(?!\1)\w+$`

要件を設定するには、<a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/set_cloud_directory_password_regex" target="_blank">管理 API <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を使用する必要があります。

</br>



</br>

## サポートされる言語
{: #languages}

<a href="https://appid-management.ng.bluemix.net/swagger-ui/#!/Config/updateLocalization" target="_blank">言語管理 API <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を使用して、ユーザー通信を記述するための言語を設定できます。ただし、すぐに使用できるのは英語だけです。メッセージの翻訳については、お客様の責任となります。 API を使用して構成を設定した後、テンプレート・テキストを変更できるように GUI が更新されます。
{: shortdesc}

<table>
  <col width="20%">
  <col width="25%">
  <col width="35%">
  <tr>
    <th>コード</th>
    <th>言語</th>
    <th>地域</th>
  </tr>
  <tr>
    <td><code>af-ZA</code></td>
    <td>アフリカーンス語</td>
    <td>南アフリカ</td>
  </tr>
  <tr>
    <td><code>sq-AL</code></td>
    <td>アルバニア語</td>
    <td>アルバニア</td>
  </tr>
  <tr>
    <td><code>am-ET</code></td>
    <td>アムハラ語</td>
    <td>エチオピア</td>
  </tr>
  <tr>
    <td><code>ar-DZ</code></td>
    <td>アラビア語</td>
    <td>アルジェリア</td>
  </tr>
  <tr>
    <td><code>ar-BH</code></td>
    <td>アラビア語</td>
    <td>バーレーン</td>
  </tr>
  <tr>
    <td><code>ar-EG</code></td>
    <td>アラビア語</td>
    <td>エジプト</td>
  </tr>
  <tr>
    <td><code>ar-IQ</code></td>
    <td>アラビア語</td>
    <td>イラク</td>
  </tr>
  <tr>
    <td><code>ar-JO</code></td>
    <td>アラビア語</td>
    <td>ヨルダン</td>
  </tr>
  <tr>
    <td><code>ar-KW</code></td>
    <td>アラビア語</td>
    <td>クウェート</td>
  </tr>
  <tr>
    <td><code>ar-LB</code></td>
    <td>アラビア語</td>
    <td>レバノン</td>
  </tr>
  <tr>
    <td><code>ar-LY</code></td>
    <td>アラビア語</td>
    <td>リビア</td>
  </tr>
  <tr>
    <td><code>ar-MR</code></td>
    <td>アラビア語</td>
    <td>モーリタニア</td>
  </tr>
  <tr>
    <td><code>ar-MA</code></td>
    <td>アラビア語</td>
    <td>モロッコ</td>
  </tr>
  <tr>
    <td><code>ar-OM</code></td>
    <td>アラビア語</td>
    <td>オマーン</td>
  </tr>
  <tr>
    <td><code>ar-QA</code></td>
    <td>アラビア語</td>
    <td>カタール</td>
  </tr>
  <tr>
    <td><code>ar-SA</code></td>
    <td>アラビア語</td>
    <td>サウジアラビア</td>
  </tr>
  <tr>
    <td><code>ar-SY</code></td>
    <td>アラビア語</td>
    <td>シリア</td>
  </tr>
  <tr>
    <td><code>ar-YE</code></td>
    <td>アラビア語</td>
    <td>チュニジア</td>
  </tr>
  <tr>
    <td><code>ar-AE</code></td>
    <td>アラビア語</td>
    <td>アラブ首長国連邦</td>
  </tr>
  <tr>
    <td><code>ar-YE</code></td>
    <td>アラビア語</td>
    <td>イエメン</td>
  </tr>
  <tr>
    <td><code>hy-AM</code></td>
    <td>アルメニア語</td>
    <td>アルメニア</td>
  </tr>
  <tr>
    <td><code>as-IN</code></td>
    <td>アッサム語</td>
    <td>インド</td>
  </tr>
  <tr>
    <td><code>az-AZ</code></td>
    <td>アゼルバイジャン語</td>
    <td>アゼルバイジャン</td>
  </tr>
  <tr>
    <td><code>eu-ES</code></td>
    <td>バスク語</td>
    <td>スペイン</td>
  </tr>
  <tr>
    <td><code>be-BY</code></td>
    <td>ベラルーシ語</td>
    <td>ベラルーシ</td>
  </tr>
  <tr>
    <td><code>bn-BD</code></td>
    <td>ベンガル語</td>
    <td>バングラデシュ</td>
  </tr>
  <tr>
    <td><code>be-BY</code></td>
    <td>ベラルーシ語</td>
    <td>ベラルーシ</td>
  </tr>
  <tr>
    <td><code>bn-BD</code></td>
    <td>ベンガル語</td>
    <td>バングラデシュ</td>
  </tr>
  <tr>
    <td><code>bn-IN</code></td>
    <td>ベンガル語</td>
    <td>インド</td>
  </tr>
  <tr>
    <td><code>bs-Latn-BA</code></td>
    <td>ボスニア語</td>
    <td>ボスニア</td>
  </tr>
  <tr>
    <td><code>bg-BG</code></td>
    <td>ブルガリア語</td>
    <td>ブルガリア</td>
  </tr>
  <tr>
    <td><code>my-MM</code></td>
    <td>ビルマ語</td>
    <td>ミャンマー</td>
  </tr>
  <tr>
    <td><code>ca-ES</code></td>
    <td>カタロニア語</td>
    <td>スペイン</td>
  </tr>
  <tr>
    <td><code>zh-Hans-CN</code></td>
    <td>中国語 (簡体字)</td>
    <td>中国</td>
  </tr>
  <tr>
    <td><code>zh-Hans-SG</code></td>
    <td>中国語 (簡体字)</td>
    <td>シンガポール</td>
  </tr>
  <tr>
    <td><code>zh-Hant-HK</code></td>
    <td>中国語 (繁体字)</td>
    <td>中華人民共和国香港特別行政区</td>
  </tr>
  <tr>
    <td><code>zh-Hant-MO</code></td>
    <td>中国語 (繁体字)</td>
    <td>マカオ</td>
  </tr>
  <tr>
    <td><code>zh-Hant-TW</code></td>
    <td>中国語 (繁体字)</td>
    <td>台湾</td>
  </tr>
  <tr>
    <td><code>hr-HR</code></td>
    <td>クロアチア語</td>
    <td>クロアチア</td>
  </tr>
  <tr>
    <td><code>cs-CZ</code></td>
    <td>チェコ語</td>
    <td>チェコ共和国</td>
  </tr>
  <tr>
    <td><code>da-DK</code></td>
    <td>デンマーク語</td>
    <td>デンマーク</td>
  </tr>
  <tr>
    <td><code>nl-BE</code></td>
    <td>オランダ語</td>
    <td>ベルギー</td>
  </tr>
  <tr>
    <td><code>nl-NL</code></td>
    <td>オランダ語</td>
    <td>オランダ</td>
  </tr>
  <tr>
    <td><code>en-AU</code></td>
    <td>英語</td>
    <td>オーストラリア</td>
  </tr>
  <tr>
    <td><code>eu-BE</code></td>
    <td>英語</td>
    <td>ベルギー</td>
  </tr>
  <tr>
    <td><code>en-CM</code></td>
    <td>英語</td>
    <td>カメルーン</td>
  </tr>
  <tr>
    <td><code>eu-CA</code></td>
    <td>英語</td>
    <td>カナダ</td>
  </tr>
  <tr>
    <td><code>en-GH</code></td>
    <td>英語</td>
    <td>ガーナ</td>
  </tr>
  <tr>
    <td><code>eu-HK</code></td>
    <td>英語</td>
    <td>中華人民共和国香港特別行政区</td>
  </tr>
  <tr>
    <td><code>en-IN</code></td>
    <td>英語</td>
    <td>インド</td>
  </tr>
  <tr>
    <td><code>en-IE</code></td>
    <td>英語</td>
    <td>アイルランド</td>
  </tr>
  <tr>
    <td><code>en-KE</code></td>
    <td>英語</td>
    <td>ケニア</td>
  </tr>
  <tr>
    <td><code>en-MU</code></td>
    <td>英語</td>
    <td>モーリシャス</td>
  </tr>
  <tr>
    <td><code>en-NZ</code></td>
    <td>英語</td>
    <td>ニュージーランド</td>
  </tr>
  <tr>
    <td><code>en-NG</code></td>
    <td>英語</td>
    <td>ナイジェリア</td>
  </tr>
  <tr>
    <td><code>en-PH</code></td>
    <td>英語</td>
    <td>フィリピン</td>
  </tr>
  <tr>
    <td><code>en-SG</code></td>
    <td>英語</td>
    <td>シンガポール</td>
  </tr>
  <tr>
    <td><code>en-ZA</code></td>
    <td>英語</td>
    <td>南アフリカ</td>
  </tr>
  <tr>
    <td><code>en-TZ</code></td>
    <td>英語</td>
    <td>タンザニア</td>
  </tr>
  <tr>
    <td><code>en-GB</code></td>
    <td>英語</td>
    <td>英国</td>
  </tr>
  <tr>
    <td><code>ja-JP</code></td>
    <td>英語</td>
    <td>米国</td>
  </tr>
  <tr>
    <td><code>en-ZM</code></td>
    <td>英語</td>
    <td>ザンビア</td>
  </tr>
  <tr>
    <td><code>     en
    </code></td>
    <td>英語</td>
    <td> </td>
  </tr>
  <tr>
    <td><code>et-EE</code></td>
    <td>エストニア語</td>
    <td>エストニア</td>
  </tr>
  <tr>
    <td><code>fil-PH</code></td>
    <td>フィリピン語</td>
    <td>フィリピン</td>
  </tr>
  <tr>
    <td><code>fi-FI</code></td>
    <td>フィンランド語</td>
    <td>フィンランド</td>
  </tr>
  <tr>
    <td><code>fr-DZ</code></td>
    <td>フランス語</td>
    <td>アルジェリア</td>
  </tr>
  <tr>
    <td><code>fr-CM</code></td>
    <td>フランス語</td>
    <td>カメルーン</td>
  </tr>
  <tr>
    <td><code>fr-CD</code></td>
    <td>フランス語</td>
    <td>コンゴ民主共和国</td>
  </tr>
  <tr>
    <td><code>fr-BE</code></td>
    <td>フランス語</td>
    <td>ベルギー</td>
  </tr>
  <tr>
    <td><code>fr-CA</code></td>
    <td>フランス語</td>
    <td>カナダ</td>
  </tr>
  <tr>
    <td><code>fr-FR</code></td>
    <td>フランス語</td>
    <td>フランス</td>
  </tr>
  <tr>
    <td><code>fr-CI</code></td>
    <td>フランス語</td>
    <td>象牙海岸 (コートジボアール)</td>
  </tr>
  <tr>
    <td><code>fr-LU</code></td>
    <td>フランス語</td>
    <td>ルクセンブルグ</td>
  </tr>
  <tr>
    <td><code>fr-MR</code></td>
    <td>フランス語</td>
    <td>モーリタニア</td>
  </tr>
  <tr>
    <td><code>fr-MU</code></td>
    <td>フランス語</td>
    <td>モーリシャス</td>
  </tr>
  <tr>
    <td><code>fr-MA</code></td>
    <td>フランス語</td>
    <td>モロッコ</td>
  </tr>
  <tr>
    <td><code>fr-SN</code></td>
    <td>フランス語</td>
    <td>セネガル</td>
  </tr>
  <tr>
    <td><code>fr-CH</code></td>
    <td>フランス語</td>
    <td>スイス</td>
  </tr>
  <tr>
    <td><code>fr-TN</code></td>
    <td>フランス語</td>
    <td>チュニジア</td>
  </tr>
  <tr>
    <td><code>gl-ES</code></td>
    <td>ガリシア語</td>
    <td>スペイン</td>
  </tr>
  <tr>
    <td><code>lg-UG</code></td>
    <td>ガンダ語</td>
    <td>ウガンダ</td>
  </tr>
  <tr>
    <td><code>ka-GE</code></td>
    <td>ジョージア語</td>
    <td>ジョージア</td>
  </tr>
  <tr>
    <td><code>de-AT</code></td>
    <td>ドイツ語</td>
    <td>オーストリア</td>
  </tr>
  <tr>
    <td><code>de-DE</code></td>
    <td>ドイツ語</td>
    <td>ドイツ</td>
  </tr>
  <tr>
    <td><code>de-LU</code></td>
    <td>ドイツ語</td>
    <td>ルクセンブルグ</td>
  </tr>
  <tr>
    <td><code>de-CH</code></td>
    <td>ドイツ語</td>
    <td>スイス</td>
  </tr>
  <tr>
    <td><code>el-GR</code></td>
    <td>ギリシャ語</td>
    <td>ギリシャ</td>
  </tr>
  <tr>
    <td><code>gu-IN</code></td>
    <td>グジャラート語</td>
    <td>インド</td>
  </tr>
  <tr>
    <td><code>ha-NG</code></td>
    <td>ハウサ語</td>
    <td>ナイジェリア</td>
  </tr>
  <tr>
    <td><code>he-IL</code></td>
    <td>ヘブライ語</td>
    <td>イスラエル</td>
  </tr>
  <tr>
    <td><code>hi-IN</code></td>
    <td>ヒンディ語</td>
    <td>インド</td>
  </tr>
  <tr>
    <td><code>hu-HU</code></td>
    <td>ハンガリー語</td>
    <td>ハンガリー</td>
  </tr>
  <tr>
    <td><code>is-IS</code></td>
    <td>アイスランド語</td>
    <td>アイスランド</td>
  </tr>
  <tr>
    <td><code>ig-NG</code></td>
    <td>イボ語</td>
    <td>ナイジェリア</td>
  </tr>
  <tr>
    <td><code>id-ID</code></td>
    <td>インドネシア語</td>
    <td>インドネシア</td>
  </tr>
  <tr>
    <td><code>it-IT</code></td>
    <td>イタリア語</td>
    <td>イタリア</td>
  </tr>
  <tr>
    <td><code>it-CH</code></td>
    <td>イタリア語</td>
    <td>スイス</td>
  </tr>
  <tr>
    <td><code>ja-JP</code></td>
    <td>日本語</td>
    <td>日本</td>
  </tr>
  <tr>
    <td><code>kn-IN</code></td>
    <td>カンナダ語</td>
    <td>インド</td>
  </tr>
  <tr>
    <td><code>kk-KZ</code></td>
    <td>カザフ語</td>
    <td>カザフスタン</td>
  </tr>
  <tr>
    <td><code>km-KH</code></td>
    <td>クメール語</td>
    <td>カンボジア</td>
  </tr>
  <tr>
    <td><code>rw-RW</code></td>
    <td>キンヤルワンダ語</td>
    <td>ルワンダ</td>
  </tr>
  <tr>
    <td><code>kok-IN</code></td>
    <td>コンカニー語</td>
    <td>インド</td>
  </tr>
  <tr>
    <td><code>ko-KR</code></td>
    <td>韓国語</td>
    <td>韓国</td>
  </tr>
  <tr>
    <td><code>lo-LA</code></td>
    <td>リトアニア語</td>
    <td>リトアニア</td>
  </tr>
  <tr>
    <td><code>lv-LV</code></td>
    <td>ラトビア語</td>
    <td>ラトビア</td>
  </tr>
  <tr>
    <td><code>lt-LT</code></td>
    <td>クメール語</td>
    <td>カンボジア</td>
  </tr>
  <tr>
    <td><code>mk-MK</code></td>
    <td>マケドニア語</td>
    <td>マケドニア</td>
  </tr>
  <tr>
    <td><code>ms-Latn-MY</code></td>
    <td>マレー語ローマ字</td>
    <td>マレーシア</td>
  </tr>
  <tr>
    <td><code>ml-IN</code></td>
    <td>マラヤーラム語</td>
    <td>インド</td>
  </tr>
  <tr>
    <td><code>mt-MT</code></td>
    <td>マルタ語</td>
    <td>マルタ</td>
  </tr>
  <tr>
    <td><code>mr-IN</code></td>
    <td>マラーティー語</td>
    <td>インド</td>
  </tr>
  <tr>
    <td><code>mn-Cyrl-MN</code></td>
    <td>モンゴル語キリル文字</td>
    <td>モンゴル</td>
  </tr>
  <tr>
    <td><code>ne-IN</code></td>
    <td>ネパール語</td>
    <td>インド</td>
  </tr>
  <tr>
    <td><code>ne-NP</code></td>
    <td>ネパール語</td>
    <td>ネパール</td>
  </tr>
  <tr>
    <td><code>nb-NO</code></td>
    <td>ノルウェー語ブークモール</td>
    <td>ノルウェー</td>
  </tr>
  <tr>
    <td><code>nn-NO</code></td>
    <td>ノルウェー語ニーノシュク</td>
    <td>ノルウェー</td>
  </tr>
  <tr>
    <td><code>or-IN</code></td>
    <td>オリヤー語 (オディア語)</td>
    <td>インド</td>
  </tr>
  <tr>
    <td><code>om-ET</code></td>
    <td>オロモ語</td>
    <td>エチオピア</td>
  </tr>
  <tr>
    <td><code>pl-PL</code></td>
    <td>ポーランド語</td>
    <td>ポーランド</td>
  </tr>
  <tr>
    <td><code>pt-AO</code></td>
    <td>ポルトガル語</td>
    <td>アンゴラ</td>
  </tr>
  <tr>
    <td><code>pt-BR</code></td>
    <td>ポルトガル語</td>
    <td>ブラジル</td>
  </tr>
  <tr>
    <td><code>pt-MO</code></td>
    <td>ポルトガル語</td>
    <td>マカオ</td>
  </tr>
  <tr>
    <td><code>pt-MZ</code></td>
    <td>ポルトガル語</td>
    <td>モザンビーク</td>
  </tr>
  <tr>
    <td><code>pt-PT</code></td>
    <td>ポルトガル語</td>
    <td>ポルトガル</td>
  </tr>
  <tr>
    <td><code>pa-IN</code></td>
    <td>パンジャブ語</td>
    <td>インド</td>
  </tr>
  <tr>
    <td><code>ro-RO</code></td>
    <td>ルーマニア語</td>
    <td>ルーマニア</td>
  </tr>
  <tr>
    <td><code>ru-RU</code></td>
    <td>ロシア語</td>
    <td>ロシア</td>
  </tr>
  <tr>
    <td><code>sr-Cyrl-RS</code></td>
    <td>セルビア語キリル文字</td>
    <td>セルビア</td>
  </tr>
  <tr>
    <td><code>sr-Latn-ME</code></td>
    <td>セルビア語ローマ字</td>
    <td>モンテネグロ</td>
  </tr>
  <tr>
    <td><code>sr-Latn-RS</code></td>
    <td>セルビア語ローマ字</td>
    <td>セルビア</td>
  </tr>
  <tr>
    <td><code>si-LK</code></td>
    <td>シンハラ語</td>
    <td>スリランカ</td>
  </tr>
  <tr>
    <td><code>sk-SK</code></td>
    <td>スロバキア語</td>
    <td>スロバキア</td>
  </tr>
  <tr>
    <td><code>sl-SI</code></td>
    <td>スロベニア語</td>
    <td>スロベニア</td>
  </tr>
  <tr>
    <td><code>es-AR</code></td>
    <td>スペイン語</td>
    <td>アルゼンチン</td>
  </tr>
  <tr>
    <td><code>es-BO</code></td>
    <td>スペイン語</td>
    <td>ボリビア</td>
  </tr>
  <tr>
    <td><code>es-CL</code></td>
    <td>スペイン語</td>
    <td>チリ</td>
  </tr>
  <tr>
    <td><code>es-CO</code></td>
    <td>スペイン語</td>
    <td>コロンビア</td>
  </tr>
  <tr>
    <td><code>es-CR</code></td>
    <td>スペイン語</td>
    <td>コスタリカ</td>
  </tr>
  <tr>
    <td><code>es-DO</code></td>
    <td>スペイン語</td>
    <td>ドミニカ共和国</td>
  </tr>
  <tr>
    <td><code>es-EC</code></td>
    <td>スペイン語</td>
    <td>エクアドル</td>
  </tr>
  <tr>
    <td><code>es-SV</code></td>
    <td>スペイン語</td>
    <td>エルサルバドル</td>
  </tr>
  <tr>
    <td><code>es-GT</code></td>
    <td>スペイン語</td>
    <td>グアテマラ</td>
  </tr>
  <tr>
    <td><code>es-HN</code></td>
    <td>スペイン語</td>
    <td>ホンジュラス</td>
  </tr>
  <tr>
    <td><code>es-MX</code></td>
    <td>スペイン語</td>
    <td>メキシコ</td>
  </tr>
  <tr>
    <td><code>es-NI</code></td>
    <td>スペイン語</td>
    <td>ニカラグア</td>
  </tr>
  <tr>
    <td><code>es-PA</code></td>
    <td>スペイン語</td>
    <td>パナマ</td>
  </tr>
  <tr>
    <td><code>es-PY</code></td>
    <td>スペイン語</td>
    <td>パラグアイ</td>
  </tr>
  <tr>
    <td><code>es-PE</code></td>
    <td>スペイン語</td>
    <td>ペルー</td>
  </tr>
  <tr>
    <td><code>es-PR</code></td>
    <td>スペイン語</td>
    <td>プエルトリコ</td>
  </tr>
  <tr>
    <td><code>es-ES</code></td>
    <td>スペイン語</td>
    <td>スペイン</td>
  </tr>
  <tr>
    <td><code>es-US</code></td>
    <td>スペイン語</td>
    <td>米国</td>
  </tr>
  <tr>
    <td><code>es-UY</code></td>
    <td>スペイン語</td>
    <td>ウルグアイ</td>
  </tr>
  <tr>
    <td><code>es-VE</code></td>
    <td>スペイン語</td>
    <td>ベネズエラ</td>
  </tr>
  <tr>
    <td><code>sw-KE</code></td>
    <td>スワヒリ語</td>
    <td>ケニア</td>
  </tr>
  <tr>
    <td><code>sw-TZ</code></td>
    <td>スワヒリ語</td>
    <td>タンザニア</td>
  </tr>
  <tr>
    <td><code>sv-SE</code></td>
    <td>スウェーデン語</td>
    <td>スウェーデン</td>
  </tr>
  <tr>
    <td><code>ta-IN</code></td>
    <td>タミール語</td>
    <td>インド</td>
  </tr>
  <tr>
    <td><code>te-IN</code></td>
    <td>テルグ語</td>
    <td>インド</td>
  </tr>
  <tr>
    <td><code>th-TH</code></td>
    <td>タイ語</td>
    <td>タイ</td>
  </tr>
  <tr>
    <td><code>tr-TR</code></td>
    <td>トルコ語</td>
    <td>トルコ</td>
  </tr>
  <tr>
    <td><code>uk-UA</code></td>
    <td>ウクライナ語</td>
    <td>ウクライナ</td>
  </tr>
  <tr>
    <td><code>ur-IN</code></td>
    <td>ウルドゥー語</td>
    <td>インド</td>
  </tr>
  <tr>
    <td><code>ur-PK</code></td>
    <td>ウルドゥー語</td>
    <td>パキスタン</td>
  </tr>
  <tr>
    <td><code>uz-Cyrl-UZ</code></td>
    <td>ウズベク語キリル文字</td>
    <td>ウズベキスタン</td>
  </tr>
  <tr>
    <td><code>uz-Latn-UZ</code></td>
    <td>ウズベク語ローマ字</td>
    <td>ウズベキスタン</td>
  </tr>
  <tr>
    <td><code>vi-VN</code></td>
    <td>ベトナム語</td>
    <td>ベトナム</td>
  </tr>
  <tr>
    <td><code>cy-GB</code></td>
    <td>ウェールズ語</td>
    <td>英国</td>
  </tr>
  <tr>
    <td><code>yo-NG</code></td>
    <td>ヨルバ語</td>
    <td>ナイジェリア</td>
  </tr>
  <tr>
    <td><code>zu-ZA</code></td>
    <td>ズールー語</td>
    <td>南アフリカ</td>
  </tr>
</table>
