---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-03"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:pre: .pre}
{:tip: .tip}
{:screen: .screen}

# ユーザー・プロファイルの理解
{: #user-profile}

{{site.data.keyword.appid_full}} では、{{site.data.keyword.appid_short_notm}} によって保管されているユーザーに関する情報にアクセスすることによって、個別設定されたアプリ操作環境を構築できます。
{: shortdesc}

## 主要な概念
{: #key-concepts}

**ユーザー・プロファイルとは**

ユーザー・プロファイルとは、{{site.data.keyword.appid_short_notm}} によって保管されている属性をまとめたものです。属性とは、アプリと対話するユーザーに関する情報の特定の側面を示すそれぞれの部分のことです。取得可能な属性には、`事前定義`と`カスタム`の 2 つのタイプがあります。

**事前定義属性とは?**

事前定義属性は、ユーザーがアプリにサインインするときに ID プロバイダーから返されます。その属性には、ユーザー名、年齢、性別などが含まれる可能性があります。

**カスタム属性とは**

カスタム属性は、ユーザーがアプリと対話する際に学習される、ユーザーについての情報です。これには、使用するフォント・サイズやショッピング・カートに入れた品目などが含まれる可能性があります。カスタム属性は編集できます。

## ユーザー属性へのアクセス
{: #access}

ユーザー・プロファイル情報には、いくつかの異なる方法でアクセスできます。ユーザー認証が成功した後に、アプリはアクセス・トークンと識別トークンを受け取ります。識別トークンには、ID プロバイダーによって返されるユーザー属性の正規化されたサブセットが格納されます。ユーザー属性の完全なリストを取得するときには、OIDC `/userinfo` エンドポイントを使用できます。カスタム属性を管理するときには、`REST API` を使用できます。userinfo エンドポイントとカスタム属性エンドポイントはどちらも、認証プロセスの最後に {{site.data.keyword.appid_short_notm}} によって生成されるアクセス・トークンによって保護されます。



![{{site.data.keyword.appid_short_notm}} ユーザー・プロファイルのアーキテクチャー](/images/user-profile1.png)

図. ユーザー・プロファイル情報のフロー

カスタム属性を表示するには、<a href="https://appid-profiles.ng.bluemix.net/swagger-ui/index.html#/Attributes" target="_blank">REST API <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を使用できます。

</br>
</br>
