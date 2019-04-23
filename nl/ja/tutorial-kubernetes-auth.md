---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-21"

keywords: authentication, authorization, identity, app security, secure, development, ingress, policy, networking, containers, kubernetes

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


# チュートリアル: {{site.data.keyword.appid_short_notm}} を使用するように Ingress を構成する
{: #kube-auth}

{{site.data.keyword.containerlong}} 内の Ingress ネットワーキング機能を使用して、ポリシー駆動のセキュリティーを一貫して実施できます。この方法を使用すると、クラスター内のすべてのアプリケーションに関する許可と認証を同時に有効にでき、その際にアプリ・コードの変更を行う必要すらありません。以下のステップバイステップ・ガイドを使用して、{{site.data.keyword.appid_short_notm}} を使用するように Ingress コントローラーを構成する方法を学習できます。
{: shortdesc}

以下の図で、認証の流れを確認してください。

![{{site.data.keyword.appid_short_notm}} Kubernetes 統合アーキテクチャー](images/kube-integration.png)

1. ユーザーがアプリケーションを開いて、Web アプリまたは API に対する要求をトリガーします。
2. API フローの場合、Ingress コントローラーは提供されたトークンの検証を試行します。Web フローを使用する場合、3 つの経路がある OIDC 認証プロセスが開始されます。
3. {{site.data.keyword.appid_short_notm}} が、ログイン・ウィジェットを表示して認証プロセスを開始します。
4. ユーザーがユーザー名または E メールとパスワードを提供します。
5. Ingress コントローラーが {{site.data.keyword.appid_short_notm}} から許可用のアクセス・トークンと識別トークンを入手します。
6. Ingress コントローラーにより検証されて転送される、アプリに対するすべての要求には、これらのトークンが含まれる許可ヘッダーがあります。

Ingress コントローラーと {{site.data.keyword.appid_short_notm}} の統合では、現在リフレッシュ・トークンはサポートされていません。アクセス・トークンや識別トークンの有効期限が切れると、ユーザーは再認証しなければなりません。
{: note}


## 開始する前に
{: #kube-prereqs}

開始する前には、以下の前提条件を満たしていることを確認してください。
{: shortdesc}

セキュリティー上の理由から、{{site.data.keyword.appid_short_notm}} 認証は、TLS/SSL が有効化されているバックエンドのみをサポートします。
{: note}

* アプリまたはサンプル・アプリ。
* ゾーンあたり 2 つ以上のワーカー・ノードがある標準的な Kubernetes クラスター。複数ゾーン・クラスターで Ingress を使用している場合は、[Kubernetes Service の資料](/docs/containers?topic=containers-ingress#config_prereqs)で追加の前提条件を確認してください。
* クラスターのデプロイ場所と同じ地域にある {{site.data.keyword.appid_short_notm}} のインスタンス。サービス名にスペースが含まれていないことを確認してください。

* 以下の [{{site.data.keyword.cloud_notm}} IAM 役割](/docs/containers?topic=containers-access_reference#access_reference):
  * クラスター: 管理者 (Administrator) のプラットフォーム役割
  * Kubernetes 名前空間: マネージャー (Manager) のサービス役割

* 次の CLI:

  * [{{site.data.keyword.cloud_notm}}](/docs/cli/reference/ibmcloud/cloud-cli-install_use?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli)
  * [Kubernetes](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
  * [Docker](https://www.docker.com/products/docker-engine#/download)

* 以下の [{{site.data.keyword.cloud_notm}} CLI プラグイン](/docs/cli/reference/ibmcloud?topic=cloud-cli-plug-ins#plug-ins):

  * Kubernetes サービス
  * Container Registry

CLI やプラグインをダウンロードしたり Kubernetes Service 環境を構成したりするのにヘルプが必要な場合は、チュートリアル: [Kubernetes クラスターの作成](/docs/containers?topic=containers-cs_cluster_tutorial#cs_cluster_tutorial_lesson1)を確認してください。
{: tip}

では、開始しましょう。

## ステップ 1: {{site.data.keyword.appid_short_notm}} のクラスターへのバインド
{: #kube-create-appid}

クラスター内でデプロイされているアプリのインスタンスをすべて使用できるようにするために、{{site.data.keyword.appid_short_notm}} のインスタンスをクラスターにバインドできます。サービス・インスタンスをクラスターにバインドすると、アプリケーションが Kubernetes シークレットとして開始されると即時に {{site.data.keyword.appid_short_notm}} のメタデータと資格情報が使用できるようになります。
{: shortdesc}


1. {{site.data.keyword.cloud_notm}} CLI にログインします。 CLI のプロンプトに従って、ログインを完了します。

  ```
  ibmcloud login -a cloud.ibm.com -r <region>
  ```
  {: codeblock}

  <table>
    <tr>
      <th>地域</th>
      <th>エンドポイント</th>
    </tr>
    <tr>
      <td>ダラス</td>
      <td><code>us-south</code></td>
    </tr>
    <tr>
      <td>フランクフルト</td>
      <td><code>eu-de</code></td>
    </tr>
    <tr>
      <td>シドニー</td>
      <td><code>au-syd</code></td>
    </tr>
    <tr>
      <td>ロンドン</td>
      <td><code>eu-gb</code></td>
    </tr>
    <tr>
      <td>東京</td>
      <td><code> jp-tok </code></td>
    </tr>
  </table>

2. クラスターのコンテキストを設定します。

  1. 環境変数を設定して Kubernetes 構成ファイルをダウンロードするためのコマンドを取得します。

    ```
    ibmcloud ks cluster-config <cluster_name_or_ID>
    ```
    {: codeblock}

  2. `export` で始まる出力をコピーし、端末に貼り付け、`KUBECONFIG` 環境変数を設定します。

3. デフォルトの名前空間内に Ingress コントローラーが既にあるかどうかを確認します。IBM Cloud Kubernetes Service は名前空間あたり 1 つの Ingress をサポートします。既に 1 つある場合は、既存の Ingress 構成を更新するか、別の名前空間を使用することができます。

  ```
  kubectl get ingress
  ```
  {: pre}

4. {{site.data.keyword.appid_short_notm}} のインスタンスをバインドします。 バインドすると、サービス・インスタンスのサービス・キーが作成されます。`-key` フラグを使用して、既存のサービス・キーを指定できます。

  ```
  ibmcloud ks cluster-service-bind --cluster <cluster_name_or_ID> --namespace <namespace> --service <App-ID_instance_name> [--key <service_instance_key>]
  ```
  {: pre}

  名前空間を指定しないと、`default` 名前空間内でシークレットが作成されます。
  {: tip}

  出力例:

  ```
  ibmcloud ks cluster-service-bind --cluster mycluster --namespace default --service appid1
  Binding service instance to namespace...
  OK
  Namespace:    default
  Secret name:  binding-appid1
  ```
  {: screen}

おつかれさまでした。

## ステップ 2: アプリをコンテナー・レジストリーにプッシュする
{: #kube-registry}

アプリケーションが Kubernetes 内で稼働するには、レジストリー内でホストしなければなりません。
{: shortdesc}


1. コンテナー・レジストリー CLI プラグインにサインインします。

  ```
  ibmcloud cr login
  ```
  {: pre}

2. コンテナー・レジストリー名前空間を作成します。

  ```
  ibmcloud cr namespace-add <my_namespace>
  ```
  {: pre}

3. コンテナー・レジストリーの名前空間へのイメージとして、アプリをビルドして、タグを指定し、プッシュします。コマンドの最後に必ずピリオド (.) を付けてください。

  ```
  ibmcloud cr build -t registry.<region>.bluemix.net/<namespace>/<app-name>:<tag> .
  ```
  {: pre}

おつかれさまでした。デプロイの準備がほぼできました。

## ステップ 3: Ingress の構成
{: kube-ingress}

クラスターの作成中に、プライベートとパブリックの Ingress ALB が両方とも自動的に作成されます。アプリケーションをデプロイし、Ingress コントローラーを利用するには、デプロイメント・スクリプトを作成します。
{: shortdesc}

1. {{site.data.keyword.appid_short_notm}} をクラスターにバインドする際にクラスター名前空間に作成されたシークレットを取得します。注: これはコンテナー・レジストリー名前空間では**ありません**。

  ```
  kubectl get secrets --namespace=<namespace>
  ```
  {: pre}

  出力例:

  ```
  NAME                       TYPE                                  DATA      AGE
  binding-appid1             Opaque                                1         1m
  bluemix-default-secret     kubernetes.io/dockercfg               1         1h
  default-token-kf97z        kubernetes.io/service-account-token   3         1h
  ```
  {: screen}

2. 以下の `yaml` ファイルの例を使用して、Ingress 構成を作成します。残りのデプロイメントを定義するのにヘルプが必要な場合は、[CLI でアプリをデプロイする方法](/docs/containers?topic=containers-app#app_cli)を確認します。

  ```
  apiVersion: extensions/v1beta1
  kind: Ingress
  metadata:
    name: myingress
    annotations:
      ingress.bluemix.net/appid-auth: "bindSecret=<bind_secret> namespace=<namespace> requestType=<request_type> serviceName=<myservice> [idToken=false]"
  spec:
    tls:
    - hosts:
      - mydomain
      secretName: mytlssecret
    rules:
    - host: mydomain
      http:
        paths:
        - path: /
          backend:
            serviceName: myservice
            servicePort: 8080
  ```
  {: screen}

  <table>
    <tr>
      <th>変数</th>
      <th>説明</th>
    </tr>
    <tr>
      <td><code>bindSecret</code></td>
      <td>{{site.data.keyword.appid_short_notm}} サービス・インスタンスをクラスターにバインドする際に作成された Kubernetes シークレット。</td>
    </tr>
    <tr>
      <td><code>namespace</code></td>
      <td><code>bindSecret</code> が作成された名前空間。名前空間を指定しなかった場合は、<code>default</code> 名前空間が使用されます。</td>
    </tr>
    <tr>
      <td><code>requestType</code></td>
      <td><p>{{site.data.keyword.appid_short_notm}} に送信する要求のタイプ。オプションには <code>web</code> と <code>api</code> が含まれます。要求タイプを <code>web</code> に設定すると、{{site.data.keyword.appid_short_notm}} アクセス・トークンを含む Web 要求が検証されます。 トークンの検証が失敗すると、Web 要求は拒否されます。 要求にアクセス・トークンが含まれていない場合、要求は {{site.data.keyword.appid_short_notm}} ログイン・ページにリダイレクトされます。 {{site.data.keyword.appid_short_notm}} Web 認証が機能するためには、ユーザーのブラウザーで Cookie を有効にする必要があります。</p><p>要求タイプを <code>api</code> に設定すると、{{site.data.keyword.appid_short_notm}} アクセス・トークンを含む API 要求が検証されます。 要求にアクセス・トークンが含まれていない場合、「<code>401 : Unauthorized</code>」というエラー・メッセージがユーザーに返されます。</p></td>
    </tr>
    <tr>
      <td><code>serviceName</code></td>
      <td><p>必須: アプリ用に作成した Kubernetes サービスの名前。サービス名を指定しない場合、アノテーションはすべてのサービスに対して有効になります。</p> <p>同一のクラスター内で複数の要求のタイプを使用するには、<code>web</code> を使用するように {{site.data.keyword.appid_short_notm}} の 1 つのインスタンスを構成し、<code>api</code> を使用するようにもう 1 つを構成します。</p></td>
    </tr>
    <tr>
      <td><code>idToken</code></td>
      <td>オプション: Liberty OIDC クライアントはアクセス・トークンと識別トークンの両方を同時に解析することはできません。Liberty を処理する際には、この値を <code>false</code> に設定して、識別トークンが Liberty サーバーに送信されないようにしてください。</td>
    </tr>
    <tr>
      <td><code>secretName</code></td>
      <td>TLS 証明書と関連付けられている TLS シークレット。証明書が IBM Cloud Certificate Manager 内でホストされている場合は、<code>ibmcloud ks alb-cert-deploy --secret-name <secret_name> --cluster <cluster_name_or_ID> --cert-crn <certificate_crn></code> を実行して、その証明書をクラスターにデプロイできます。証明書がない場合は、[Ingress によるアプリの公開](/docs/containers?topic=containers-ingress#ingress_expose_public)のステップ 3 を完了してください。</td>
    </tr>
  </table>

3. 構成ファイルを実行します。

  ```
  kubectl apply -f <file-name>.yaml
  ```
  {: pre}

おつかれさまでした。


## ステップ 4: リダイレクト URL を追加する
{: #kube-add-redirect}

リダイレクト URL は、正常に認証された後に {{site.data.keyword.appid_short_notm}} がユーザーを送信するサイトの URL のことです。
{: shortdesc}

1. {{site.data.keyword.cloud_notm}} GUI にナビゲートして、{{site.data.keyword.appid_short_notm}} ダッシュボードを開きます。

2. **「ID プロバイダー」 >「管理」**で、使用するプロバイダーを**「オン」**に設定します。 プロバイダーを有効にしないと、アプリへの匿名アクセス権を提供するアクセス・トークンがユーザーに対して発行されます。

3. **「認証設定 (Authentication Settings)」**をクリックします。

4. **「リダイレクト URL の追加 (Add web redirect URLs)」**ボックス内の**「+」**記号をクリックします。

  * カスタム・ドメイン:

    カスタム・ドメインに登録されている URL は、`http://mydomain.net/myapp2path/appid_callback` のようになります。同一のクラスター内のさまざまな名前空間内にあるアプリを公開しようとしている場合は、ワイルドカードを使用してクラスター内のすべてのアプリを同時に指定できます。この方法は開発時に役立つことがありますが、実動時にワイルドカードを使用する場合には注意する必要があります。例: `https://custom_domain.net/*`

  * Ingress サブドメイン:

    IBM Ingress サブドメインに登録されているアプリの場合、コールバック URL は `https://mycluster.us-south.containers.appdomain.cloud/myapp1path/appid_callback` のようになります。

{{site.data.keyword.appid_short_notm}} はログアウト機能を提供しています。{{site.data.keyword.appid_short_notm}} パス内に `/logout` がある場合、Cookie は削除され、ユーザーはログイン・ページに戻されます。この機能を使用するには、`/appid_logout` をドメインに `https://mycluster.us-south.containers.appdomain.cloud/myapp1path/appid_logout` という形式で付加し、リダイレクト URL 内に組み込んでください。
{: note}


おつかれさまでした。次に、Ingress サブドメインかカスタム・ドメインにナビゲートして試用し、デプロイメントが正常に行われたことを検証できます。


## 次のステップ
{: #kube-next}

この時点で、アプリケーションが Kubernetes クラスター内で稼働しており Ingress が構成されているので、以下の作業を試行できます。

* カスタム属性を使用した[役割の設定](/docs/services/appid?topic=appid-tutorial-roles)
* [多要素認証](/docs/services/appid?topic=appid-cd-mfa)の構成
* [ログイン・ウィジェット](/docs/services/appid?topic=appid-login-widget)のカスタマイズ



