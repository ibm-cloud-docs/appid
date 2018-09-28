---

copyright:
  years: 2017, 2018
lastupdated: "2018-09-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}

# General troubleshooting
{: #troubleshooting}

If you have problems while you're working with {{site.data.keyword.appid_full}}, consider these techniques for troubleshooting and getting help.
{: shortdesc}

## Getting help and support
{: #gettinghelp}

You can get help by searching for information or by asking questions through a forum. You can also open a support ticket. When you are using the forums to ask a question, tag your question so that it is seen by the {{site.data.keyword.Bluemix_notm}} development teams.
  * If you have technical questions about {{site.data.keyword.appid_short_notm}}, post your question on <a href="https://stackoverflow.com/search?q=ibm-appid" target="_blank">Stack Overflow <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> and tag your question with "ibm-appid".
  * For questions about the service and getting started instructions, use the <a href="https://developer.ibm.com/answers/topics/appid/" target="_blank">dW Answers <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> forum. Include the `appid` tag.

For more information about getting support, see [How do I get the support that I need?](/docs/get-support/howtogetsupport.html#getting-customer-support).

</br>

## A custom URL is rejected
{: #ts-custom-url}


{: tsSymptoms}
When you enter a web redirect URL that uses a custom URL Scheme it is rejected by the {{site.data.keyword.appid_short_notm}} console.

{: tsCauses}
Your URL might be rejected for the following reasons:

* The URL does not follow an `http` or `https` scheme
* The URL ends with `://`
* There is a typo in your URL

The limitations are in place for security purposes.

{: tsResolve}
To resolve the issue, verify the URL is correct. If your URL does not meet the requirements, you can create an HTTPS endpoint in your app to redirect the received grant code to your custom URL. Specify the created endpoint as your redirect URL in the {{site.data.keyword.appid_short_notm}} console.

</br>
