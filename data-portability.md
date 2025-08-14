---

copyright:
  years: 2025
lastupdated: "2025-08-14"

keywords: app id data, app id data resiliency, app id data portability

subcollection: appid

---

{{site.data.keyword.attribute-definition-list}}

# Understanding data portability for {{site.data.keyword.appid_short_notm}}
{: #data-portability}

Data portability involves a set of tools and procedures that enable you to export the digital artifacts that are needed to implement similar workload and data processing on different service providers or on-premises software. It includes procedures for copying and storing the service customer content, including the related configuration that is used by the service to store and process the data, in your location.
{: shortdesc}

## Responsibilities
{: #data-portability-responsibilities}

{{site.data.keyword.cloud_notm}} services provide interfaces and instructions to guide you through the process of copying and storing service user content, including the related configuration, in your selected location.

You're responsible for the use of the exported data and configuration for data portability to other infrastructures, which includes:

- The planning and execution for setting up alternative infrastructure on different cloud providers or on-premises software that provide similar capabilities to the {{site.data.keyword.IBM_notm}} services.
- The planning and execution for the porting of the required application code on the alternative infrastructure, including the adaptation of your application code, deployment automation, and so on.
- The conversion of the exported data and configuration to the format that's required by the alternative infrastructure and adapted applications.

To find out more about responsibility ownership for using {{site.data.keyword.cloud_notm}} products between {{site.data.keyword.IBM_notm}} and the customer, see [Shared responsibilities for {{site.data.keyword.cloud_notm}} products](/docs/overview?topic=overview-shared-responsibilities).


## Data export procedures
{: #data-portability-procedures}

{{site.data.keyword.appid_short_notm}} provides the mechanisms to export your content that's uploaded, stored, and processed when you use the service.

* To export users that authenticate through Cloud Directory, use the `export/all` API to retrieve all of your Cloud Directory profiles. Then, download the content with the `export/download` API. For help with exporting Cloud Directory users, see [Migrating users](/docs/appid?topic=appid-cd-users#user-migration).

* To export user profiles that are authenticated through social media integration, use the [users/export API](https://us-south.appid.cloud.ibm.com/swagger-ui/#/Management%20API%20-%20Users/mgmt.userProfilesExport){: external} or the following CURL command:

   ```sh
   curl -X GET 'https://<region>.appid.cloud.ibm.com/management/v4/<tenantID>/users/export' --header 'Content-Type: application/json'  --header 'Authorization: Bearer <IAMToken>'
   ```
   {: screen}


In addition, {{site.data.keyword.appid_short_notm}} provides mechanisms to export settings and configurations that are used to process your content. To download your instance configurations, you can use the [App ID Management](https://us-south.appid.cloud.ibm.com/swagger-ui/#/){: external} endpoints to get the configuration content. 


## Exported data formats
{: #data-portability-data-formats}


{{site.data.keyword.appid_short_notm}} supports the following data format and schema of the exported data, configuration, and application: 

* Users that are added through Cloud Directory.

   ```json
   [
      {
         "passwordHash": "xveImwVxuO7jxRQlRveKgBXD4WoAG0aIHVTY0GLSuTQbfTIsTNy753LFE9kdReAnBTIbSOeQ69UKJdnIxBZZkm9oWf8wsmwWeZwU9njZDDdhxzJWfvAv6Y/XjAqvNdWvJfV3Tag/zwQtKaET6Sc2gSbFL8L1X1wRR/msNA+NSfg=",
         "passwordHashAlg": "PBKDF2WithHmacSHA512",
         "profile": {
            "attributes": {
               "points": 100
            }
         },
         "roles": [],
         "scimUser": {
            "active": true,
            "displayName": "Jane Doe",
            "emails": [
               {
                  "primary": true,
                  "value": "user09857654@mail.com"
               }
            ],
            "name": {
               "familyName": "Doe",
               "formatted": "Jane Doe",
               "givenName": "Jane"
            },
            "orignalId": "e403878c-3ab5-4e99-8953-bb57b05387d8"
         }
      },
      {
         "passwordHash": "YKmBYObTprREAKqjl8F94ofE5lF5lr7Zuc/eJ0Sylvx6IOgI97M56n16U0aGWqBVTu2/P8xayrr6utoH/Uok5v/3Ct9jddXlxhkA1odqgQslJdXiCcBHn/49xU9iejCu6p3PL/81vBfcBGxTll2xeHzF+0qF4rxzn91H6TuNH4o=",
         "passwordHashAlg": "PBKDF2WithHmacSHA512",
         "profile": {
            "attributes": {
               "points": 150
            }
         },
         "roles": [
            "adult",
            "child"
         ],
         "scimUser": {
            "active": true,
            "displayName": "John Doe",
            "emails": [
               {
                  "primary": true,
                  "value": "user0987654@mail.com"
               }
            ],
            "name": {
               "familyName": "Doe",
               "formatted": "John Doe",
               "givenName": "John"
            },
            "orignalId": "66ad3522-2251-4531-abff-3e3aad66b650",
            "userName": "myUserName"
         }
      }
   ]
   ```
   {: codeblock}


* Users that are added through social media integration.

   ```json
   {
      "itemsPerPage": 2,
      "requestOptions": {},
      "totalResults": 2,
      "users": [
         {
            "attributes": {
               "points": 150
            },
            "email": "your@mail.com",
            "id": "7ae804f3-0ed3-45f0-bc6b-1c6af868e6d6",
            "identities": [
               {
                  "id": "105646725068605084546",
                  "idpUserInfo": {
                     "email": "your@mail.com",
                     "id": "105646725068605084546",
                     "picture": "profilePic.jpg"
                  },
                  "provider": "google"
               }
            ],
            "name": "App ID Google User Profile",
            "roles": []
         },
         {
            "attributes": {
               "points": 250
            },
            "email": "mail@mail.com",
            "id": "1439d777-185d-4be1-8f4a-c4e8142b87ea",
            "identities": [
               {
                  "first_name": "AppID",
                  "id": "100195207128541",
                  "last_name": "Development",
                  "picture": {
                     "data": {
                        "height": 50,
                        "url": "https://example-profile-picture.com",
                        "width": 50
                     }
                  },
                  "provider": "facebook"
               }
            ],
            "name": "App ID Facebook user profile",
            "roles": [
               "adult",
               "child"
            ]
         }
      ]
   }
   ```
   {: codeblock}

{{site.data.keyword.appid_short_notm}} doesn't support the export of the following data format and schema of the exported data, configuration, and application:

* Anonymous users

   To learn more about anonymous users and why they cannot be exported, see [Anonymous authentication](/docs/appid?topic=appid-anonymous).


## Data ownership
{: #data-portability-ownership}

All exported data is classified as customer content. Apply the full customer ownership and licensing rights, as stated in the [IBM Cloud Service Agreement](https://www.ibm.com/support/customer/csol/terms/?id=Z126-6304_WS){: external}.

For more information about data and the social media settings, see our [privacy policy](/docs/appid?topic=appid-privacy-policy).
