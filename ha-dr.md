## Understanding high availability and disaster recovery for App ID
{: #ha-dr}

{{site.data.keyword.appid_short_notm}} is a highly available, regional service that runs in the following regions:

* Dallas (`us-south`)
* Frankfurt (`eu-de`)
* London (`eu-gb`)
* Sydney (`au-syd`)
* Tokyo (`jp-tok`)
* Washington (`us-east`)

In each supported region, the service exists in multiple availability zones with no single point of failure. All of the data that is associated with your instance of the service, including your secrets, is stored and encrypted at rest. 

However, because {{site.data.keyword.appid_short_notm}} is a regional service, there is no automatic cross-regional failover or cross-regional disaster recovery. If all of the availability zones in a region fail, {{site.data.keyword.appid_short_notm}} becomes unavailable in that location. To establish cross-region high availability and implement a recovery plan, you need to create and maintain backup instances in multiple regions. To synchronize a service instance in one region with an instance in another region, you can use [the APIs](https://us-south.appid.cloud.ibm.com/swagger-ui/#/){: external}.

To learn more about the high availability and disaster recovery standards in {{site.data.keyword.cloud_notm}}, see [How do I ensure zero downtime?](/docs/overview?topic=overview-zero-downtime) or [Service Level Agreements](/docs/overview?topic=overview-slas).
