---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-11"

keywords: Authentication, authorization, identity, app security, secure, development, nodejs, frontend, web apps, 

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


# 웹: Node.js
{: #web-node}

{{site.data.keyword.appid_short_notm}}를 사용하여 Node.js 프론트 엔드 웹 애플리케이션을 쉽게 보호할 수 있습니다. 이 안내서를 사용하면 20분 이내에 간단한 인증 플로우를 신속하게 시작하고 실행할 수 있습니다.
{: shortdesc}

다음 다이어그램에서 권한 코드 OAuth 2.0 워크플로우를 확인하십시오.

![Node.js 애플리케이션 권한 부여 플로우](images/node_web.png)

1. 사용자가 보호된 웹 애플리케이션에 대한 액세스 권한을 얻으려고 하지만 권한이 없습니다.
2. 애플리케이션에서 사용자를 {{site.data.keyword.appid_short_notm}}로 경로 재지정합니다.
3. {{site.data.keyword.appid_short_notm}}에서 사용자가 인증하는 데 사용할 수 있는 사인인 화면을 보여줍니다.
4. 사용자 이름과 비밀번호와 같은 인증 정보를 입력합니다. App ID에서 인증 정보의 유효성을 검증합니다.
5. {{site.data.keyword.appid_short_notm}}에서 권한 부여 코드를 사용하여 사용자를 다시 애플리케이션으로 경로 재지정합니다.
6. 권한 부여 코드를 사용하여 애플리케이션에서 {{site.data.keyword.appid_short_notm}}에 요청을 보내 사용자의 유효성을 검증하게 합니다. 액세스 토큰을 얻는 데 관한 자세한 정보는 [토큰 확보](/docs/services/appid?topic=appid-obtain-tokens)를 참조하십시오.
7. {{site.data.keyword.appid_short_notm}}에서 유효성 검증된 사용자의 액세스 및 ID 토큰을 리턴합니다.
8. 그러면 사용자에게 애플리케이션에 대한 액세스 권한이 부여됩니다.



## 동영상 튜토리얼
{: #web-node-video}

{{site.data.keyword.appid_short_notm}}를 사용하여 단순 Node.js 웹 애플리케이션을 보호하는 방법을 보려면 다음 동영상을 확인하십시오. 이 동영상에 포함된 모든 정보는 이 페이지에서 서면으로도 확인할 수 있습니다.

<iframe class="embed-responsive-item" id="appid-web-node" title="{{site.data.keyword.appid_short_notm}} Node.js 애플리케이션 정보" type="text/html" width="640" height="390" src="//www.youtube.com/embed/6roa1ZOvwtw?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>

플로우를 사용해 볼 수 있는 앱이 없습니까? 걱정하지 마십시오! {{site.data.keyword.appid_short_notm}}에서는 [단순 Node.js 웹 샘플 앱](https://github.com/ibm-cloud-security/appid-video-tutorials/tree/master/02a-simple-node-web-app){: external}을 제공합니다.

 

## 시작하기 전에
{: #web-node-before}

Node.js 웹 애플리케이션에서 {{site.data.keyword.appid_short_notm}}를 시작하기 전에 다음 필수 소프트웨어가 있어야 합니다.
{: shortdesc}

* [{{site.data.keyword.appid_short_notm}} 서비스](https://cloud.ibm.com/catalog/services/app-id){: external} 인스턴스
* [IBM Cloud CLI](/docs/cli?topic=cloud-cli-getting-started)
* [NPM 버전 4+](https://www.npmjs.com/get-npm){: external}
* [Node 버전 6+](https://nodejs.org/en/download/){: external}


## 1단계: 경로 재지정 URI 등록
{: #node-web-redirect-uri}

경로 재지정 URI는 앱의 콜백 엔드포인트입니다. {{site.data.keyword.appid_short_notm}}는 사인인 플로우 중에 클라이언트에서 피싱 공격 및 권한 부여 코드 누출을 방지하는 데 도움이 되는 권한 워크플로우에 참가할 수 있도록 허용하기 전에 URI를 유효성 검증합니다. URI를 등록하면 {{site.data.keyword.appid_short_notm}}에서 해당 URI를 신뢰할 수 있으며 사용자의 경로를 재지정할 수 있습니다.
{: shortdesc}

1. **인증 관리 > 인증 설정**을 클릭하십시오.

2. **웹 경로 재지정 URI 추가** 필드에 URI를 입력하십시오. 각각의 URI는 `http://` 또는 `https://`로 시작되어야 하며 정상적으로 경로 재지정하기 위한 조회 매개변수를 포함한 전체 경로가 포함되어야 합니다.

3. **웹 경로 재지정 URI 추가** 상자에서 **+** 기호를 클릭하십시오.

4. 목록에 가능한 모든 URI가 추가될 때까지 1 - 3단계를 반복하십시오.



## 2단계: 인증 정보 얻기
{: #node-web-credentials}

다음 두 가지 방법 중 하나로 인증 정보를 얻을 수 있습니다.
{: shortdesc}

  * {{site.data.keyword.appid_short_notm}} 대시보드의 **애플리케이션** 탭으로 이동하십시오. 애플리케이션이 없는 경우 **애플리케이션 추가**를 클릭하여 새 애플리케이션을 작성하십시오.

  * [`/management/v4/{tenantId}/applications` 엔드포인트](https://us-south.appid.cloud.ibm.com/swagger-ui/#!/Applications/registerApplication)에 대한 POST 요청을 작성하십시오.

    요청 형식:
    ```javascript
    curl -X POST \  https://us-south.appid.cloud.ibm.com/management/v4/39a37f57-a227-4bfe-a044-93b6e6060b61/applications/ \
    -H 'Content-Type: application/json' \
    -H 'Authorization: Bearer IAM_TOKEN' \
    -d '{"name": "ApplicationName"}'
    ```
    {: codeblock}

    응답 예제:
    ```javascript
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



## 3단계: SDK 초기화
{: #web-node-install}

{{site.data.keyword.appid_short_notm}}와 작업하는 가장 쉬운 방법은 Node.JS SDK를 사용하는 것입니다.
{: shortdesc}


1. 명령행을 사용하여 Node.js 애플리케이션이 포함된 디렉토리로 변경하십시오.

2. 다음 NPM 요구사항을 설치하십시오.

    ```javascript
    npm install --save express express-session passport
    ```
    {: codeblock}

3. {{site.data.keyword.appid_short_notm}} 서비스를 설치하십시오.

    ```javascript
  npm install --save ibmcloud-appid
    ```
    {: codeblock}

4. `server.js` 파일로 다음 요구사항을 추가하십시오.

    ```javascript
    const express = require('express'); 								// https://www.npmjs.com/package/express
    const session = require('express-session');							// https://www.npmjs.com/package/express-session
    const passport = require('passport');								// https://www.npmjs.com/package/passport
    const WebAppStrategy = require('ibmcloud-appid').WebAppStrategy;	// https://www.npmjs.com/package/ibmcloud-appid
    ```
    {: shortdesc}

5. 1단계에서 얻은 인증 정보를 사용하여 express-session 미들웨어를 사용하도록 애플리케이션을 설정하십시오. 다음 두 가지 방법 중 하나로 경로 재지정 URI를 형식화하도록 선택할 수 있습니다. 수동으로 새 `WebAppStrategy({redirectUri: "...."})`를 사용하거나 예제 코드에 표시된 대로 환경 변수로 값을 설정합니다.

    ```javascript
    const app = express();
    app.use(session({
        secret: '123456',
        resave: true,
        saveUninitialized: true
    }));
    app.use(passport.initialize());
    app.use(passport.session());
    passport.serializeUser((user, cb) => cb(null, user));
    passport.deserializeUser((user, cb) => cb(null, user));
    passport.use(new WebAppStrategy({
        tenantId: "<tenant_ID>",
        clientId: "<client_ID>",
        secret: "<secret>",
        oauthServerUrl: "<OAuth_Server_URL>",
        redirectUri: "<redirect_URI>"
    }));
    ```
    {: codeblock}

    프로덕션 환경에 적합한 세션 스토리지로 미들웨어를 구성해야 합니다. 자세한 정보는 <a href="https://github.com/expressjs/session" target="_blank"> express.js 문서<img src="../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 참조하십시오.
    {: note}


## 4단계: 애플리케이션 보호
{: #node-web-protect}

이제 {{site.data.keyword.appid_short_notm}}가 설치되었으므로 애플리케이션을 보호할 준비가 되었습니다. 웹 앱 전략을 정의하여 전체 애플리케이션 또는 특정 리소스만 보호하도록 선택할 수 있습니다.
{: shortdesc}


1. 콜백 엔드포인트를 구성하십시오. App ID에서 액세스 및 ID 토큰을 검색하고 다음 위치 중 하나로 사용자의 경로를 재지정하여 콜백에서 권한 프로세스를 완료합니다.<ul><li>HTTP 세션에서 `WebAppStrategy.ORIGINAL_URL`로 지속되므로 인증을 트리거한 요청의 원래 URL.</li><li>인증에 성공한 경우 경로 재지정을 지정합니다.</li><li>다음 단계에 표시된 대로 애플리케이션 루트(`/`).</li></ul>

    ```javascript
   app.get(CALLBACK_URL, passport.authenticate(WebAppStrategy.STRATEGY_NAME));
    ```
    {: codeblock}

2. 브라우저의 경로를 항상 로그인 위젯으로 재지정하는 로그인 엔드포인트를 설정하십시오. 무한 인증 루프에 빠지지 않도록 성공 경로 재지정 옵션을 추가하십시오.

    ```javascript
    app.get('/appid/login', passport.authenticate(WebAppStrategy.STRATEGY_NAME, {
        successRedirect: '/',
        forceLogin: true
    }));
    ```
    {: codeblock}

3. 로그아웃을 구성하십시오. 사용자가 애플리케이션에서 로그아웃하면 해당 세션에서 모든 인증 정보를 지웁니다. 애플리케이션과 상호작용하려면 다시 사인인해야 합니다.

    ```javascript
    app.get('/appid/logout', function(req, res){
        webappstrategy.logout(req);
        res.redirect('/');
    });
    ```
    {: shortdesc}

## 5단계: 앱 개인화
{: #node-web-user-info}

앱 환경을 개인화하기 위해 ID 제공자가 제공한 정보를 가져올 수 있습니다.
{: shortdesc}

1. 사용자 정보를 얻도록 애플리케이션을 구성하십시오. `protected`는 애플리케이션의 엔드포인트와 일치하도록 변경할 수 있는 플레이스홀더 변수입니다.

    ```javascript
    app.get("/protected", passport.authenticate(WebAppStrategy.STRATEGY_NAME), function(req, res){
        res.json(req.user);
    });
    ```
    {: codeblock}

    예를 들어 샘플 애플리케이션에서 애플리케이션을 개인화할 사용자 이름을 얻는 방법을 확인할 수 있습니다.
    ```javascript
    app.get('/api/user', (req, res) => {
        // console.log(req.session[WebAppStrategy.AUTH_CONTEXT]);
        res.json({
            user: {
                name: req.user.name
            }
        });
    });
    ```
    {: codeblock}


## 6단계: 구성 테스트
{: #node-web-test}

권한 구성을 테스트하려면 애플리케이션에 정의된 대로 서버가 청취 중인 URL로 이동하십시오. 로그인한 다음 로그아웃해 보십시오. 구성이 예상대로 작동하는지 확인하십시오. 

다음 단계로 이동할 준비가 되면 [Cloud Directory의 다중 요소 인증](/docs/services/appid?topic=appid-cd-mfa)을 사용으로 설정하거나 [사용자 정의 속성](/docs/services/appid?topic=appid-profiles)을 추가하여 앱을 추가로 개인화할 수 있습니다.


