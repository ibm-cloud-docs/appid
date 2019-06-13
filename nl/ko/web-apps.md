---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-21"

keywords: authentication, authorization, identity, app security, secure, web apps, client, server

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


# 웹 앱
{: #web-apps}

{{site.data.keyword.appid_full}}를 사용하여 신속하게 웹 애플리케이션에 대한 인증 계층을 생성할 수 있습니다.
{: shortdesc}

## 플로우에 대한 정보
{: #web-understanding}

**어떤 경우에 이 플로우가 유용합니까?**

웹 애플리케이션을 개발하는 경우 {{site.data.keyword.appid_short_notm}} 웹 플로우를 사용하여 안전하게 사용자를 인증할 수 있습니다. 그런 다음 사용자는 웹 앱에 있는 서버 측에서 보호된 컨텐츠에 액세스할 수 있습니다.

**이 플로우의 기술적 기반은 무엇입니까?**

웹 앱을 사용하기 위해 사용자가 보호된 컨텐츠에 액세스해야 하는 경우도 있습니다. {{site.data.keyword.appid_short_notm}}는 안전하게 사용자를 인증하기 위해 OIDC 권한 코드 플로우를 사용합니다. 이 플로우를 사용하는 경우 사용자가 인증되면 앱에서 권한 코드를 수신하게 됩니다. 그런 다음 이 코드가 액세스, ID 및 새로 고치기 토큰으로 교환됩니다. 코드 교환 단계에서 토큰은 항상 앱과 OIDC 서버 간의 보안 백채널을 통해 전송됩니다. 이 기능을 통해 공격자가 토큰을 가로챌 수 없도록 추가적인 보안 계층을 제공합니다. 이러한 토큰은 사용자 인증을 위해 웹 서버 호스팅 애플리케이션으로 직접 전송할 수 있습니다.

**이 플로우는 어떻게 작동합니까?**

![{{site.data.keyword.appid_short_notm}} 요청 플로우](images/web-flow.png)

1. 사용자는 {{site.data.keyword.appid_short_notm}} SDK 또는 API를 통해 `/authorization` 엔드포인트에 대한 요청을 전송함으로써 권한 플로우를 시작합니다.

2. 사용자에게 권한이 없는 경우 {{site.data.keyword.appid_short_notm}}로 경로 재지정되면서 인증 플로우가 시작됩니다.

3. 사용자의 `/authorization` 요청 매개변수 또는 ID 제공자 구성에 따라 사용자의 브라우저에서 로그인 위젯이 실행됩니다.

4. 사용자가 인증할 ID 제공자를 선택하고 사인인 프로세스를 완료합니다.

5. ID 제공자는 인증 코드가 포함된 클라이언트 앱으로 경로 재지정됩니다.

6. {{site.data.keyword.appid_short_notm}} SDK는 권한 코드를 {{site.data.keyword.appid_short_notm}} 서비스의 액세스, ID 및 선택적 새로 고치기 토큰으로 교환합니다.

7. {{site.data.keyword.appid_short_notm}} SDK에서 토큰을 저장한 후 클라이언트 애플리케이션으로의 경로 재지정이 발생합니다.

8. 사용자에게 앱에 대한 액세스 권한이 부여됩니다.


## Node.js SDK 구성
{: #web-configuring-nodejs}

Node.js 웹 애플리케이션에서 작동하도록 {{site.data.keyword.appid_short_notm}}를 구성할 수 있습니다.
{: shortdesc}

**시작하기 전에**

다음과 같은 전제조건이 준비되어 있어야 합니다.

* {{site.data.keyword.appid_short_notm}} 서비스의 인스턴스
* 서비스 인증 정보 세트
* NPM 버전 4 이상
* 노드 버전 6 이상
* {{site.data.keyword.appid_short_notm}} 서비스 대시보드의 경로 재지정 URI 세트


{{site.data.keyword.appid_short_notm}}를 사용한 Node 애플리케이션 보호에 대해 학습하려면 다음 동영상을 확인하십시오. 그런 다음 [간단한 Node 샘플 앱](https://github.com/ibm-cloud-security/appid-video-tutorials/tree/master/02a-simple-node-web-app)을 사용하여 직접 시도해 보십시오. 

<iframe class="embed-responsive-item" id="appid-nodejs" title="{{site.data.keyword.appid_short_notm}} 정보" type="text/html" width="640" height="390" src="//www.youtube.com/embed/6roa1ZOvwtw?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>


### Node.js SDK 설치
{: #web-nodejs-install}

1. 명령행을 사용하여 Node.js 앱이 포함된 디렉토리로 변경하십시오.

2. {{site.data.keyword.appid_short_notm}} 서비스를 설치하십시오.

  ```bash
  npm install --save ibmcloud-appid
  ```
  {: codeblock}

### Node.js SDK 초기화
{: #web-nodejs-initialize}

1. 다음 `require` 정의를 `server.js` 파일에 추가하십시오.

  ```javascript
    const express = require('express');
    const session = require('express-session')
    const passport = require('passport');
    const WebAppStrategy = require("ibmcloud-appid").WebAppStrategy;
    const CALLBACK_URL = "/ibm/cloud/appid/callback";
  ```
  {: codeblock}

2. express-session 미들웨어를 사용하도록 express 앱을 설정하십시오.

  ```javascript
    const app = express();
    app.use(session({
        secret: "123456",
        resave: true,
        saveUninitialized: true
        }));
    app.use(passport.initialize());
    app.use(passport.session());
  ```
  {: codeblock}

  프로덕션 환경에 적합한 세션 스토리지로 미들웨어를 구성해야 합니다. 자세한 정보는 <a href="https://github.com/expressjs/session" target="_blank"> express.js 문서<img src="../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 참조하십시오.
  {: note}

3. 다음 방법 중 하나를 통해 인증 정보를 받으십시오.

  * {{site.data.keyword.appid_short_notm}} 대시보드의 **애플리케이션** 탭으로 이동하십시오. 애플리케이션이 나열되지 않을 경우 **애플리케이션 추가**를 클릭하여 새 애플리케이션을 작성하십시오.

  * [`/management/v4/{tenantId}/applications` 엔드포인트](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Applications/mgmt.registerApplication)에 대한 POST 요청을 작성하십시오.

    요청 형식:
    ```
    curl -X POST \  https://us-south.appid.cloud.ibm.com/management/v4/39a37f57-a227-4bfe-a044-93b6e6060b61/applications/ \
    -H 'Content-Type: application/json' \
    -H 'Authorization: Bearer IAM_TOKEN' \
    -d '{"name": "ApplicationName"}'
    ```
    {: codeblock}

    응답 예제:
    ```
    {
    "clientId": "111c22c3-38ea-4de8-b5d4-338744d83b0f",
    "tenantId": "39a37f57-a227-4bfe-a044-93b6e6060b61",
    "secret": "ZmE5ZDQ5ODctMmA1ZS00OGRiLWExZDMtZTA1MjkyZTc4MDB4",
    "name": "ApplicationName",
    "oAuthServerUrl": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6060b61"
    }
    ```
    {: screen}

4. 선택사항: 경로 재지정 URI를 형식화하는 방법을 결정하십시오. 경로 재지정은 서로 다른 두 가지 방법으로 형식화할 수 있습니다.

  * 새 `WebAppStrategy({redirectUri: "...."})`에서 수동으로
  * `redirectUri`로 이름 지정된 환경 변수로

  둘 다 제공되지 않을 경우 {{site.data.keyword.appid_short_notm}} SDK는 {{site.data.keyword.cloud_notm}}에서 실행 중인 앱의 `application_uri`를 검색하여 기본 접미부인 `/ibm/cloud/appid/callback`을 추가합니다.

5. 이전 단계에서 얻은 정보를 사용하여 SDK를 초기화하십시오.

  ```javascript
  passport.use(new WebAppStrategy({
    	  tenantId: "{tenant-id}",
   	    clientId: "{client-id}",
      	secret: "{secret}",
      	oauthServerUrl: "{oauth-server-url}",
      	redirectUri: "{app-url}" + CALLBACK_URL
      }));
  ```
  {: codeblock}

6. 직렬화 및 직렬화 해제로 passport를 구성하십시오. 이 구성 단계는 HTTP 요청 전체에 걸쳐 인증된 세션 지속성에 필요합니다. 자세한 정보는 <a href="http://www.passportjs.org/docs/" target="_blank">passport 문서 <img src="../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 참조하십시오.

  ```javascript
  passport.serializeUser(function(user, cb) {
    cb(null, user);
    });

  passport.deserializeUser(function(obj, cb) {
    cb(null, obj);
    });
  ```
  {: codeblock}

5. 다음 코드를 `server.js` 파일에 추가하여 서비스 경로 재지정을 실행하십시오.

   ```javascript
   app.get(CALLBACK_URL, passport.authenticate(WebAppStrategy.STRATEGY_NAME));
   ```
   {: codeblock}

6. 보호된 엔드포인트를 등록하십시오.

   ```javascript
   app.get(‘/protected’, passport.authenticate(WebAppStrategy.STRATEGY_NAME), function(req, res) {res.json(req.user); });
   ```
   {: codeblock}

자세한 정보는 <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">{{site.data.keyword.appid_short_notm}} Node.js GitHub repository <img src="../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 참조하십시오.



## Liberty for Java SDK 구성
{: #web-configuring-liberty}

Liberty for Java 웹 애플리케이션에서 작동하도록 {{site.data.keyword.appid_short_notm}}를 구성할 수 있습니다.
{:shortdesc}

**시작하기 전에**

다음과 같은 전제조건이 준비되어 있어야 합니다.
* {{site.data.keyword.appid_short_notm}} 서비스의 인스턴스
* 서비스 인증 정보 세트
* Apache Maven 3.5 이상
* Java 1.8
* A Liberty for Java 웹 애플리케이션


{{site.data.keyword.appid_short_notm}}를 사용한 Liberty for Java 애플리케이션 보호에 대해 학습하려면 다음 동영상을 확인하십시오. 그런 다음 [간단한 Liberty for Java 샘플 앱](https://github.com/ibm-cloud-security/appid-video-tutorials/tree/master/02c-simple-liberty-web-app)을 사용하여 직접 시도해 보십시오. 

<iframe class="embed-responsive-item" id="appid-liberty-web" title="{{site.data.keyword.appid_short_notm}} 정보" type="text/html" width="640" height="390" src="//www.youtube.com/embed/o_Er69YUsMQ?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>



### Liberty for Java SDK 설치
{: #web-liberty-install}

1. `server.xml`에 OpenID Connect 기능을 추가하십시오.

  ```xml
  <featureManager>
      <feature>ssl-1.0</feature>
      <feature>appSecurity-2.0</feature>
      <feature>openidConnectClient-1.0</feature>
  </featureManager>
  ```
  {: codeblock}

2. 두 가지 방법 중 하나를 통해 인증 정보를 받으십시오.

  * {{site.data.keyword.appid_short_notm}} 대시보드의 **애플리케이션** 탭으로 이동하십시오. 애플리케이션이 없는 경우 **애플리케이션 추가**를 클릭하여 새 애플리케이션을 작성하십시오.

  * [`/management/v4/{tenantId}/applications` 엔드포인트](https://us-south.appid.cloud.ibm.com/swagger-ui/#!/Applications/registerApplication)에 대한 POST 요청을 작성하십시오.

    요청 형식:
    ```
    curl -X POST \  https://us-south.appid.cloud.ibm.com/management/v4/39a37f57-a227-4bfe-a044-93b6e6060b61/applications/ \
    -H 'Content-Type: application/json' \
    -H 'Authorization: Bearer IAM_TOKEN' \
    -d '{"name": "ApplicationName"}'
    ```
    {: codeblock}

    응답 예제:
    ```
    {
    "clientId": "111c22c3-38ea-4de8-b5d4-338744d83b0f",
    "tenantId": "39a37f57-a227-4bfe-a044-93b6e6060b61",
    "secret": "ZmE5ZDQ5ODctMmA1ZS00OGRiLWExZDMtZTA1MjkyZTc4MDB4",
    "name": "ApplicationName",
    "oAuthServerUrl": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6060b61"
    }
    ```
    {: screen}

3. Open ID Connect 클라이언트 기능을 작성한 후 다음과 같은 플레이스홀더를 정의하십시오. 서비스 인증 정보를 사용하여 플레이스홀더를 채우십시오.

  ```xml
  <openidConnectClient
    clientId='{{site.data.keyword.appid_short_notm}} client_ID'
    clientSecret='{{site.data.keyword.appid_short_notm}} Secret'
    authorizationEndpointUrl='oauthServerUrl/authorization'
    tokenEndpointUrl='oauthServerUrl/token'
    jwkEndpointUrl='oauthServerUrl/publickeys'
    issuerIdentifier='Changed according to the region'
    tokenEndpointAuthMethod="basic"
    signatureAlgorithm="RS256"
    authFilterid="myAuthFilter"
    trustAliasName="ibm.com"
  />
  ```
  {: codeblock}

  <table>
  <caption>표. Liberty for Java 앱에 대한 OIDC 요소 변수</caption>
    <tr>
      <th> 컴포넌트 </th>
      <th> 설명 </th>
    </tr>
    <tr>
    <td><code>clientID</code> </br> <code>secret</code> </br> <code>oauth-server-url</code> </br></td>
    <td>2단계를 완료하여 서비스 인증 정보를 받으십시오.</td>
    </tr>
    <tr>
      <td><code> authorizationEndpointURL </code></td>
      <td> <code>oauthServerURL</code>의 끝 부분에 <code>/authorization</code>을 추가하십시오.</td>
    </tr>
    <tr>
      <td><code> tokenEndpointUrl </code></td>
      <td><code>oauthServerURL</code>의 끝 부분에 <code>/token</code>을 추가하십시오.</td>
    </tr>
    <tr>
      <td><code> jwkEndpointUrl </code></td>
      <td><code>oauthServerURL</code>의 끝 부분에 <code>/publickeys</code>를 추가하십시오.</td>
    </tr>
    <tr>
      <td><code> issuerIdentifier </code></td>
      <td>발행자 ID의 형식은 <code>&lt;region>&gt;.cloud.ibm.com</code>입니다. 지역 옵션에는 <code>au-syd</code>, <code>eu-de</code>, <code>eu-gb</code>, <code>jp-tok</code> 및 <code>us-south</code>가 있습니다.</td>
    </tr>
    <tr>
      <td><code> tokenEndpointAuthMethod </code></td>
      <td>"basic"으로 지정됩니다.</td>
    </tr>
    <tr>
      <td><code> signatureAlgorithm </code></td>
      <td>"RS256"으로 지정됩니다.</td>
    </tr>
    <tr>
      <td><code> authFilterid </code></td>
      <td>보호할 리소스의 목록입니다.</td>
    </tr>
    <tr>
      <td><code> trustAliasName </code></td>
      <td>신뢰 저장소 내에서 인증서의 이름입니다.</td>
    </tr>
  </table>

### Liberty for Java SDK 초기화
{: #web-liberty-initialize}

1. `server.xml` 파일에서 보호된 리소스를 지정하는 권한 필터를 정의하십시오. 필터가 <a href="https://www.ibm.com/support/knowledgecenter/en/SSD28V_9.0.0/com.ibm.websphere.wlp.core.doc/ae/rwlp_auth_filter.html" target="_blank">정의 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>되지 않은 경우 이 서비스에서 모든 리소스를 보호합니다.

  ```xml
  <authFilter id="myAuthFilter">
             <requestUrl id="myRequestUrl" urlPattern="/protected" matchType="contains"/>
    </authFilter>
  ```
  {: codeblock}

2. 특수 주제 유형을 `ALL_AUTHENTICATED_USERS`로 정의하십시오.

  ```xml
  <application type="war" id="ProtectedServlet" context-root="/appidSample"
  location="${server.config.dir}/apps/libertySample-1.0.0.war">
    <application-bnd>
        <security-role name="myrole">
        <special-subject type="ALL_AUTHENTICATED_USERS"/>
        </security-role>
            </application-bnd>
        </application>
  ```
  {: codeblock}

3. <a href="https://github.com/ibm-cloud-security/appid-sample-code-snippets/tree/master/liberty-for-java" target="_blank">GitHub <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>에서 `libertySample-1.0.0.war` 파일을 다운로드하여 서버의 앱 폴더에 배치하십시오. 예를 들어 서버의 이름이 `defaultServer`인 경우 war 파일은 `target/liberty/wlp/usr/servers/defaultServer/apps/`로 이동할 수 있습니다.

4. `server.xml` 파일에 다음 코드를 추가하여 SSL을 구성하십시오. 신뢰 저장소도 작성해야 합니다.

  ```xml
    <keyStore id="defaultKeyStore" password="myPassword"/>
  <keyStore id="appidtruststore" password="Liberty" location="${server.config.dir}/mytruststore.jks"/>
  <ssl id="defaultSSLConfig" keyStoreRef="defaultKeyStore" trustStoreRef="appidtruststore"/>
  ```
  {: codeblock}

기본적으로 SSL 구성을 사용하려면 OpenID Connect에 대한 신뢰 저장소를 구성해야 합니다. <a href="https://www.ibm.com/support/knowledgecenter/en/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/twlp_config_oidc_rp.html" target="_blank">Liberty에서 OpenID Connect 클라이언트 구성 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>에 대한 자세한 정보를 참조하십시오.
{: tip}



## Spring Boot for Java SDK 구성
{: #web-configuring-spring-boot}

Spring Boot 애플리케이션에서 작동하도록 {{site.data.keyword.appid_short_notm}}를 구성할 수 있습니다.
{:shortdesc}

**시작하기 전에**

다음과 같은 전제조건이 준비되어 있어야 합니다.

* {{site.data.keyword.appid_short_notm}} 서비스의 인스턴스
* 서비스 인증 정보 세트
* Java + Maven 프로젝트
* Apache Maven 3.5 이상
* Java 1.8
* Spring Boot 2.0 및 Security OAuth 2.0 이상


### Spring Boot 프레임워크 초기화
{: #web-spring-boot-initialize}

1. Maven `pom.xml` 파일에서 `<project> </project>` 태그 사이에 다음 코드를 추가하십시오.

  ```xml
  <parent>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-parent</artifactId>
      <version>2.0.2.RELEASE</version>
      <relativePath/>
  </parent>
  ```
  {: codeblock}

2. Maven `pom.xml` 파일에 다음 종속 항목을 추가하십시오.

  ```xml
  <dependencies>
      <dependency>
          <groupId>org.springframework.boot</groupId>
          <artifactId>spring-boot-starter-web</artifactId>
      </dependency>
      <dependency>
          <groupId>org.springframework.boot</groupId>
          <artifactId>spring-boot-starter-security</artifactId>
      </dependency>
      <dependency>
          <groupId>org.springframework.security.oauth.boot</groupId>
          <artifactId>spring-security-oauth2-autoconfigure</artifactId>
          <version>2.0.0.RELEASE</version>
      </dependency>
  </dependencies>
  ```
  {: codeblock}

3. 동일한 파일에 Maven 플러그인을 포함하십시오.

  ```xml
  <plugin>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-maven-plugin</artifactId>
  </plugin>
  ```
  {: codeblock}

### OAuth2 초기화
{: #web-oauth-initialize}

1. Java 파일에 다음 어노테이션을 추가하십시오.

  ```java
  @SpringBootApplication
  @EnableOAuth2Sso
  ```
  {: codeblock}

2. `WebSecurityConfigurerAdapter`로 클래스를 확장하십시오.
3. 보안 구성을 모두 대체한 후 보호된 엔드포인트를 등록하십시오.

  ```java
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.authorizeRequests()
                .antMatchers("/protectedResource").authenticated()
                .and().logout().logoutSuccessUrl("/").permitAll();
    }
  ```
  {: codeblock}


### 인증 정보 추가
{: #web-spring-boot-credentials}

1. 다음 방법 중 하나를 통해 인증 정보를 받으십시오.

  * {{site.data.keyword.appid_short_notm}} 대시보드의 **애플리케이션** 탭으로 이동하십시오. 애플리케이션이 없는 경우 **애플리케이션 추가**를 클릭하여 새 애플리케이션을 작성하십시오.

  * [`/management/v4/{tenantId}/applications` 엔드포인트](https://us-south.appid.cloud.ibm.com/swagger-ui/#!/Applications/registerApplication)에 대한 POST 요청을 작성하십시오.

    요청 형식:
    ```
    curl -X POST \  https://us-south.appid.cloud.ibm.com/management/v4/39a37f57-a227-4bfe-a044-93b6e6060b61/applications/ \
    -H 'Content-Type: application/json' \
    -H 'Authorization: Bearer IAM_TOKEN' \
    -d '{"name": "ApplicationName"}'
    ```
    {: codeblock}

    응답 예제:
    ```
    {
    "clientId": "111c22c3-38ea-4de8-b5d4-338744d83b0f",
    "tenantId": "39a37f57-a227-4bfe-a044-93b6e6060b61",
    "secret": "ZmE5ZDQ5ODctMmA1ZS00OGRiLWExZDMtZTA1MjkyZTc4MDB4",
    "name": "ApplicationName",
    "oAuthServerUrl": "https://us-south.appid.cloud.ibm.com/oauth/v4/39a37f57-a227-4bfe-a044-93b6e6060b61"
    }
    ```
    {: screen}

2. `/springbootsample/src/main/resources/` 디렉토리에 `application.yml` 구성 파일을 추가하십시오. 서비스 인증 정보의 정보를 사용하여 구성을 완료할 수 있습니다.

  ```
  security:
  oauth2:
    client:
      clientId: {client ID}
      clientSecret: {client Secret}
      accessTokenUri: {oauthServerUrl}/token
      userAuthorizationUri: {oauthServerUrl}/authorization
    resource:
      userInfoUri: {oauthServerUrl}/userinfo
  ```
  {: codeblock}

단계별 예제는 <a href="https://www.ibm.com/cloud/blog/creating-spring-boot-applications-app-id" target="_blank">이 블로그</a>를 참조하십시오!


## 다른 언어로 {{site.data.keyword.appid_short_notm}} 사용
{: #web-other-languages}

OIDC 준수 클라이언트 SDK를 사용하는 경우 다른 언어로 {{site.data.keyword.appid_short_notm}}를 사용할 수 있습니다. 자세한 정보는 <a href="https://openid.net/developers/certified/">인증된 라이브러리</a> 목록을 참조하십시오.

## 다음 단계
{: #web-next}

애플리케이션에 {{site.data.keyword.appid_short_notm}}가 설치되면 사용자 인증을 시작할 준비가 거의 된 것입니다! 이제 다음 활동 중 하나를 수행하십시오.

* [ID 제공자](/docs/services/appid?topic=appid-social) 구성
* [로그인 위젯](/docs/services/appid?topic=appid-login-widget) 사용자 정의 및 구성
* <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">Node.js SDK<img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>에 대한 정보 확인
