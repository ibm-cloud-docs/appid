---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-01"

keywords: authentication, authorization, identity, app security, secure, development, two factor, mfa 

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


# Use case: App to app



Scenario : 

Consider you are building an application that needs to access certain APIs protected by access tokens, but acting on behalf of the application itself rather than on behalf of any individual user. This is a perfect use case for the OAuth2 Client Credentials flow. The application can obtain access tokens from the OAuth authorization server directly, without the involvement of any end user.

Another example might be a cron job which is performing maintenance tasks over an API or IOT devices trying to communicate over a wireless network and needs to authenticate with the network. In all these cases, what is important is that requests are exchanged on behalf of the application, rather than an end user and it is the application that is authenticated and authorized. In such scenarios, you'd want to leverage App ID Application Identity to secure your work flows/backend API calls.

Overview of the requirements : 
Secure Application endpoints or APIs which are non interactive, in other words there is no user interaction to authenticate.

Application Identity Flow/ Solution :
Using the AppID Application Identity you can obtain an access token and secure your non interactive applications or workflows.

In the application Identity flow, you would first register the application that needs to authenticate to access a protected resource. Once the application registers with App ID, it obtains a client ID and secret. This pair of credentials can be exchanged with App ID to obtain an access token.

It is extremely critical that the credentials used to authenticate the  client be kept highly confidential. Since the application must always hold the client secret, this work flow is only meant to be used in trusted applications such as web application where there is no risk of the secret being misused or leaked. 

- Overview of the runtime flow : 
 The application requests the App ID authorization server /token endpoint for access tokens with its client id and secret. The application can then use the tokens to access the protected resources. More detailed information about setting up and using App ID Application Identity can be found in the documentation. [docs link]

Typical Use cases : 
This section describes some of the typical use cases for App ID Application Identity.

Two Backend Services:  
This is usually the most common use case for Application Identity. You have some REST APIs protected by App ID access tokens and you have another backend application that needs access the protected API on behalf of itself rather than a user requesting access to the protected API.

For example, consider a simple airline reservation system, which handles all the passenger reservation logic and calls another service to process payments, let's call it the payments service. Given the nature of the payments service, it is protected by the App ID access tokens.

The user when making a reservation uses a UI dashboard to make a reservation request, the dashboard then makes a request to the reservation service which then calls the payments service to process the payment before making a reservation. Since the payments service is protected by App ID access tokens, the reservation service needs to obtain access tokens from the App ID authorization server. 



To obtain the access tokens, the reservation service needs to be registered with AppID Application Identity, i.e, the reservationService has to obtain a set of credentials (client id and the secret). It uses these credentials to obtain an access token from the AppID Authorization server and uses this token to call the payments service. It is important to note that the access token the payments service obtains from AppID represents authorization for the payments service itself and not on behalf of the end user.

CLI 
The above use case be further extended to CLIs, cron jobs or any other use case where there is no user interaction needed for authentication and as long as the application running them can securely store its client id and secret.
  
Internet of Things (IOT) 
Internet of Things (IoT) deployments have been increasing steadily over the past few years. These devices   constantly monitor/collect and push data to a central server or applications usually running on the cloud.
The applications collecting the data from these IoT devices are protected by access tokens to prevent misuse. The IoT devices would then need to acquire access tokens from an authorization server and use them 
to push the data over to the application. IoT devices function with little to no user intervention once deployed. This makes the entire IoT ecosystem a very good use case for the AppID Application Identity which implements the OAuth2 client credentials flow.

OAuth2 was primarily designed for use with HTTP-based web applications and it has been extended for use with Simple Authentication and Security Layer (SASL)[https://tools.ietf.org/html/rfc7628] which is used in IoT deployments.

In this scenario, all of your IoT devices would be registered with your AppID instance, this provides each of your IoT devices with a pair credentials which it uses to obtain access tokens from the authorization server. These access tokens are then used to  call the APIs for sending the collected data.

  
