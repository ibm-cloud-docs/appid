---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-11"

keywords: Authentication, authorization, identity, app security, secure, development, access management, liberty, backend, java, token

subcollection: appid

---

{:external: target="_blank" .external}
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


# バックエンド: Liberty for Java
{: #backend-liberty}

{{site.data.keyword.appid_short_notm}} を利用すると、容易に API エンドポイントを保護し、Liberty for Java バックエンド・アプリケーションのセキュリティーを確保することができます。このガイドを使用すると、シンプルな認証フローを 20 分足らずで迅速に起ち上げることができます。
{: shortdesc}


![バックエンドの Liberty for Java アプリ](images/backend_liberty.png)

1. 保護リソースに対して要求を行うには、クライアントにアクセス・トークンが必要です。手順 1 で、クライアントは {{site.data.keyword.appid_short_notm}} にトークンを要求します。アクセス・トークンの取得方法について詳しくは、[トークンの取得](/docs/services/appid?topic=appid-obtain-tokens)を参照してください。
2. {{site.data.keyword.appid_short_notm}} がトークンを返します。
3. クライアントが、アクセス・トークンを使用して、保護リソースへのアクセス要求を行います。
4. リソースが、構造、有効期限、署名、オーディエンス、その他のフィールドを含むトークンを検証します。トークンが無効な場合、リソース・サーバーはアクセスを拒否します。トークンの検証が成功すると、データが返されます。


## ビデオのチュートリアル
{: #backend-liberty-video}

以下のビデオを視聴すると、{{site.data.keyword.appid_short_notm}} を使用してシンプルな Liberty for Java アプリケーションを保護する方法を確認できます。ビデオで扱われている情報はすべて、このページに記載しています。

<iframe class="embed-responsive-item" id="appid-liberty-backend-app" title="{{site.data.keyword.appid_short_notm}} について" type="text/html" width="640" height="390" src="//www.youtube.com/embed/QA6DY2qqLaw?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>

フローを試すことができるアプリがありませんか? 問題ありません。 {{site.data.keyword.appid_short_notm}} には、[シンプルな Liberty for Java サンプル・アプリ](https://github.com/ibm-cloud-security/appid-video-tutorials/tree/master/02d-simple-liberty-backend-app)が用意されています。


## 開始する前に
{: #liberty-before}

Liberty for Java バックエンド・アプリケーションで {{site.data.keyword.appid_short_notm}} の使用を開始する前に、以下の前提条件を満たしている必要があります。

* [{{site.data.keyword.appid_short_notm}} サービス](https://cloud.ibm.com/catalog/services/app-id){: external}のインスタンス
* [IBM Cloud CLI](/docs/cli?topic=cloud-cli-getting-started)
* [Apache Maven 3.5+](https://maven.apache.org/download.cgi){: external}
* [Java 8+](https://www.java.com/download/){: external}
* テスト用の [{{site.data.keyword.appid_short_notm}} Postman コレクション](https://github.com/ibm-cloud-security/appid-postman){: external}

## 手順 1: 資格情報を取得する
{: #liberty-obtain-credentials}

次の 2 つの方法のいずれかを利用して、資格情報を取得できます。


  * {{site.data.keyword.appid_short_notm}} ダッシュボードの**「アプリケーション」**タブに移動します。 アプリケーションがまだない場合は、**「アプリケーションの追加 (Add application)」**をクリックして新しいアプリケーションを作成できます。

  * [`/management/v4/{tenantId}/applications` エンドポイント](https://us-south.appid.cloud.ibm.com/swagger-ui/#!/Applications/registerApplication){: external}に対して POST 要求を行います。

    要求の形式:
    ```
    curl -X POST \  https://us-south.appid.cloud.ibm.com/management/v4/<tenantID>/applications/ \
    -H 'Content-Type: application/json' \
    -H 'Authorization: Bearer IAM_TOKEN' \
    -d '{"name": "ApplicationName"}'
    ```
    {: codeblock}

    応答例:
    ```
    {
      "clientId": "xxxxx-34a4-4c5e-b34d-d12cc811c86d",
      "tenantId": "xxxxx-9b1f-433e-9d46-0a5521f2b1c4",
      "secret": "ZDk5YWZkYmYt*******",
      "name": "app1",
      "oAuthServerUrl": "https://us-south.appid.cloud.ibm.com/oauth/v4/xxxxx-9b1f-433e-9d46-0a5521f2b1c4",
      "profilesUrl": "https://us-south.appid.cloud.ibm.com",
      "discoveryEndpoint": "https://us-south.appid.cloud.ibm.com/oauth/v4/xxxxxx-9b1f-433e-9d46-0a5521f2b1c4/.well-known/openid-configuration"
    }
    ```
    {: screen}


## 手順 2: `server.xml` ファイルを構成する
{: #liberty-configure-server}
 
1. `server.xml` ファイルを開きます。
2. 以下のフィーチャーを `featureManager` セクションに追加します。一部のフィーチャーは、Liberty に組み込まれている可能性があります。サーバーの実行時にエラーを受け取った場合は、Liberty インストール済み環境の bin ディレクトリーから `.installUtility install <name_of_server>` を実行してインストールすることができます。

    ```xml
    <featureManager>
        <feature>appSecurity-2.0</feature>
        <feature>openidConnectClient-1.0</feature>
        <feature>ssl-1.0</feature>
        <feature>servlet-3.1</feature>
    </featureManager>
    ```
    {: codeblock}

3. 以下の内容を `server.xml` ファイルに追加して、SSL を構成します。 

    ```xml
    <keyStore id="defaultKeyStore" password="{password}"/>
    <keyStore id="RootCA" password="{password}" location="${server.config.dir}/resources/security/{myTrustStore}"/>
    <ssl id="{sslID}" keyStoreRef="defaultKeyStore" trustStoreRef="{truststore-ref}"/>
    ```
    {: codeblock}

4. Open ID Connect Client フィーチャーを作成し、以下のプレースホルダーを定義します。 取得した資格情報を使用して、プレースホルダーに入力してください。

    ```xml
    <openidConnectClient 
        id="oidc-client-simple-liberty-backend-app" 		
        inboundPropagation="required"
        jwkEndpointUrl="{region}.appid.cloud.ibm.com/oauth/v4/{tenantID}/publickeys"
        issuerIdentifier="{region).appid.cloud.ibm.com/oauth/v4/{tenantID}"
        signatureAlgorithm="RS256"
        audiences="{client-id}"
        sslRef="oidcClientSSL"
    /> 	
    ```
    {: codeblock}

    <table>
    <caption>表. Liberty for Java アプリケーションの OIDC 要素変数</caption>
        <tr>
            <th colspan="2"> OIDC 要素変数について</th>
        </tr>
        <tr>
            <td><code>id</code></td>
            <td>アプリケーションの名前。</td>
        </tr>
        <tr>
            <td><code>inboundPropagation</code></td>
            <td>トークンで受け取った情報を伝搬させるには、値を「required」に設定する必要があります。</td>
        </tr>
        <tr>
            <td><code> jwkEndpointUrl </code></td>
            <td>トークンを検証するための鍵の取得に使用されるエンドポイント。地域オプションとしては、<code>au-syd</code>、<code>eu-de</code>、<code>eu-gb</code>、<code>jp-tok</code>、<code>us-south</code> があります。テナント ID は、前に作成した資格情報にあります。</td>
        </tr>
        <tr>
            <td><code> issuerIdentifier </code></td>
            <td>発行者 ID は、許可サーバーを定義します。地域オプションとしては、<code>au-syd</code>、<code>eu-de</code>、<code>eu-gb</code>、<code>jp-tok</code>、<code>us-south</code> があります。テナント ID は、前に作成した資格情報にあります。</td>
        </tr>
        <tr>
            <td><code> signatureAlgorithm </code></td>
            <td>"RS256" を指定します。</td>
        </tr>
        <tr>
            <td><code>audiences</code></td>
            <td>デフォルトでは、トークンはアプリケーション資格情報内にある {{site.data.keyword.appid_short_notm}} クライアント ID に対して発行されます。</td>
        </tr>
        <tr>
            <td><code>sslRef</code></td>
            <td>使用する SSL 構成の名前。</td>
        </tr>
    </table>

5. 特別なサブジェクト・タイプを `ALL_AUTHENTICATED_USERS` として定義します。

    ```xml
    <application 
        id="simple-liberty-backend-app" 
        location="location-of-your-war-file" 
        name="simple-liberty-backend-app" 
        type="war">

        <application-bnd>
            <security-role name="myrole">
                <special-subject type="ALL_AUTHENTICATED_USERS"/>
            </security-role>
        </application-bnd>
    </application>
    ```
    {: codeblock}


## 手順 3: `web.xml` ファイルを構成する
{: #liberty-configure-web}

`web.xml` ファイルで、保護するアプリケーションの領域を定義します。

1. セキュリティー役割を定義します。これは、`server.xml` ファイルで定義した役割と同じでなければなりません。

    ```
    <security-role>
		<role-name>myrole</role-name>
	</security-role>
    ```
    {: codeblock}

2. セキュリティー制約を定義します。

    ```
	<security-constraint>
		<display-name>Security Constraints</display-name>
		<web-resource-collection>
			<web-resource-name>ProtectedArea</web-resource-name>
			<url-pattern>/api/*</url-pattern>
		</web-resource-collection>
		<auth-constraint>
			<role-name>myrole</role-name>
		</auth-constraint>
		<user-data-constraint>
			<transport-guarantee>NONE</transport-guarantee>
		</user-data-constraint>
	</security-constraint>
    ```
    {: codeblock}


## 手順 4: 構成をテストする
{: #liberty-test}

初期インストールが完了したので、アプリをビルドし、構成をテストして、期待どおりにすべて機能していることを確認します。

1. アプリケーション・ディレクトリーに移動します。

2. アプリケーションをビルドします。

    ```
    server run
    ```
    {: codeblock}

3. 保護エンドポイントに対して要求を行います。エラーが戻されます。

4. [アクセス・トークンを取得します](/docs/services/appid?topic=appid-obtain-tokens)。

5. 前の手順で取得したアクセス・トークンを使用して、エンドポイントへの要求を行います。今回は保護エンドポイントにアクセスできるはずです。予期した内容が応答に含まれていることを確認してください。


## 次のステップ
{: #liberty-next}

認証エクスペリエンスを作り上げる準備ができましたか? [このブログ](https://www.ibm.com/cloud/blog/perfecting-the-login-experience-with-liberty-oauth2-and-appid){: external}を参照するか、[アプリ間通信](/docs/services/appid?topic=appid-app)の詳細を確認してください。


