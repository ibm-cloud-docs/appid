---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-17"

keywords: authentication, authorization, identity, app security, secure

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
{:faq: data-hd-content-type='faq'}


# FAQ
{: #faq}

この FAQ には、{{site.data.keyword.appid_full}} サービスに関する一般的な質問に対する答えがあります。
{: shortdesc}


## {{site.data.keyword.appid_short_notm}} の料金はどのように計算しますか?
{: #faq-pricing}
{: faq}

{{site.data.keyword.appid_short_notm}} では、使用するリソースが増えるにつれて、支払いは少なくなります。
{: shortdesc}

累進階層方式のプランは、認証イベントの数と、標準セキュリティーおよび拡張セキュリティーの両方と、許可ユーザーの数の 3 つの部分で構成されています。 この 2 つの部分の合計に基づいて、毎月課金されます。 合計額は、数量にその階層の単価を乗算して計算する、各レベルの使用量の累積料金です。

拡張セキュリティー・イベントを除いて、最初の 1000 個の認証イベントと最初の 1000 人の許可ユーザーは毎月無料です。 すべての拡張セキュリティー・イベントで追加料金が発生します。

### 認証イベント
{: #faq-authentication}

認証イベントは、正規または匿名の新しいアクセス・トークンが発行されたときに発生します。 トークンは、ユーザーが開始した、あるいはユーザーに代わってアプリが開始した、サインイン要求への応答として発行できます。 デフォルトでは、アクセス・トークンは 1 時間有効であり、匿名トークンは 30 日間有効です。 トークンの期限が切れた後に保護リソースにアクセスするには、新しいトークンを作成する必要があります。 サービス・ダッシュボードの**「ID プロバイダー」>「管理」>「認証設定 (Authentication Settings)」**ページで、{{site.data.keyword.appid_short_notm}} トークンの有効期限を更新できます。

#### 拡張セキュリティー・フィーチャー

拡張セキュリティー・フィーチャーを利用すると、アプリケーションのセキュリティーを強化することができます。
{: shortdesc}

<table>
  <tr>
    <th>フィーチャー</th>
    <th>利点</th>
  </tr>
  <tr>
    <td>多要素認証</td>
    <td>[クラウド・ディレクトリー用の多要素認証 (MFA)](/docs/services/appid?topic=appid-cd-mfa#cd-mfa) では、E メール・アドレスとパスワードの入力に加えて、E メール・アドレス宛てに送信されたワンタイム・パスコードの入力をユーザーに要求することで、ユーザーの同一性を確認します。</td>
  </tr>
  <tr>
    <td>パスワード・ポリシー管理</td>
    <td>アカウント所有者は、ユーザー・パスワードが準拠する必要がある一連のルールを構成することにより、いっそうセキュアなパスワードをクラウド・ディレクトリーで施行できます。 例として、ロックアウトまでのサインイン試行回数、有効期限、パスワード更新間隔の最短時間、パスワードを再利用できるようになるまでの入力回数があります。 使用可能なオプションの詳細なリストや、セットアップに関する情報については、[拡張パスワード管理](/docs/services/appid?topic=appid-cd-strength#cd-advanced-password)を参照してください。</td>
  </tr>
</table>

デフォルトでは、拡張セキュリティー・フィーチャーは無効になっています。 MFA またはパスワード・ポリシー管理をオンにすると、追加料金が発生します。 すべての拡張フィーチャーを無効にすると、アカウントは低コストのポリシーに戻ります。 例えば、10,000 個のアクセス・トークンを取得したとします。 その後、パスワード・ポリシー管理をオンにし、さらに 10,000 個を取得しました。 この場合、20,000 個の認証イベントと 10,000 個の拡張セキュリティー・イベントに対して支払うことになります。

これらのフィーチャーは、2018 年 3 月 15 日より後に作成された、累進階層方式の価格プランのインスタンスでのみ使用できます。
{: note}

### 許可ユーザー
{: #faq-authorized}

許可ユーザーとは、直接的または間接的にサービスにサインインする固有のユーザー (匿名ユーザーを含む) のことです。 1 人の新しいユーザー (匿名ユーザーを含む) がアプリケーションにサインインするたびに、1 人分の許可ユーザー料金が課金されます。 例えば、あるユーザーが Facebook でサインインし、その後 Google を使用してサインインした場合には、それらは 2 人の別個の許可ユーザーと見なされます。

最新の料金情報については、[{{site.data.keyword.cloud_notm}} カタログ](https://cloud.ibm.com/catalog/services/app-id)の {{site.data.keyword.appid_short_notm}} のセクションにある**「見積もりに追加」**をクリックすることにより、コスト見積もりを作成できます。
{: tip}



## リダイレクト URI をホワイトリストに登録する必要があるのはなぜですか?
{: #faq-redirect}
{: faq}

リダイレクト URI は、アプリのコールバック・エンドポイントです。 フィッシング攻撃を防ぐために、{{site.data.keyword.appid_short_notm}} はリダイレクト URI のホワイトリストに照らして URI を検証します。 フィッシングが発生すると、攻撃者がユーザーのトークンへのアクセス権限を取得してしまう恐れがあります。 リダイレクト URI について詳しくは、[リダイレクト URI の追加](/docs/services/appid?topic=appid-managing-idp#add-redirect-uri)を参照してください。

URL には照会パラメーターは含めないでください。 それらは検証プロセスで無視されます。 URL 例: `http://host:[port]/path`
{: tip}



## 暗号化は {{site.data.keyword.appid_short_notm}} でどのように機能しますか?
{: #faq-encryption}
{: faq}

暗号化に関するよくある質問の答えは、以下の表を参照してください。

<table>
  <thead>
    <th colspan=2><img src="images/idea.png" alt="詳細情報アイコン"/>  </th>
  </thead>
  <tbody>
    <tr>
      <td>暗号化を使用のはなぜですか?</td>
      <td>ユーザー情報を保護する 1 つの方法は、保存されている顧客データを暗号化することです。当該サービスでは、テナントごとの鍵を使用して、保存されている顧客データを暗号化します。</td>
    </tr>
    <tr>
      <td>独自のアルゴリズムを作成したのですか？ どのアルゴリズムをコードで使用しますか?</td>
      <td>当社は独自のものを作成してはいません。このサービスでは、<code>AES</code> および <code>SHA-256</code> をソルト処理と共に使用します。</td>
    </tr>
    <tr>
      <td>公開済みまたはオープン・ソースの暗号化モジュールまたはプロバイダーを使用していますか? 暗号化機能を公開したことがありますか? </td>
      <td>このサービスでは <code>javax.crypto</code> Java ライブラリーを使用しますが、暗号化機能を公開することはありません。</td>
    </tr>
    <tr>
      <td>鍵を格納するには、どのようにすればよいですか?</td>
      <td>鍵が生成されると、地域ごとに固有のマスター鍵を使用して暗号化された後に、ローカルに格納されます。 マスター鍵は {{site.data.keyword.keymanagementserviceshort}} に格納されます。 ストレージ・レベルおよびミドルウェア・レベルでは、サービス・レベルの暗号化となり、すべての顧客に対して 1 つの鍵が存在します。 アプリ・レベルでは、顧客ごとに独自の暗号鍵が存在します。</td>
    </tr>
    <tr>
      <td>使用する鍵の強度は何ですか?</td>
      <td>サービスは 16 バイトを使用します。</td>
    </tr>
    <tr>
      <td>暗号化機能を公開するリモート API を呼び出していますか?</td>
      <td>いいえ、していません。</td>
    </tr>
  </tbody>
</table>



## {{site.data.keyword.appid_short_notm}} と Keycloak の違いは何ですか?
{:# faq-keycloak}

{{site.data.keyword.appid_short_notm}} も Keycloak も、アプリケーションに認証を追加してサービスを保護するために使用できます。 この 2 つのオファリングの主な違いは、そのパッケージングにあります。
{: shortdesc}

Keycloak はソフトウェアとしてパッケージされています。つまり、ダウンロードした後は、開発者が製品の機能を保守する必要があります。 ホスティング、高可用性、コンプライアンス、バックアップ、DDoS 対策、ロード・バランシング、Web ファイアウォール、データベースなどには開発者が対応します。

{{site.data.keyword.appid_short_notm}} は、「as-a-Service」として提供されるフル・マネージドのオファリングです。 つまり、IBM がサービスの運用を管理し、準拠性、複数のゾーンでの可用性、SLA などに対応することを意味します。 また、{{site.data.keyword.appid_short_notm}} では、{{site.data.keyword.containershort_notm}}、{{site.data.keyword.openwhisk_short}}、{{site.data.keyword.cloudaccesstrailshort}} などのネイティブのランタイムやサービスが含まれている {{site.data.keyword.cloud_notm}} Platform との統合エクスペリエンスをすぐに使用できます。
