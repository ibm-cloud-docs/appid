
  <tr>
    <td><code>appid-mgmt-send-email-cd</code></td>
    <td>Send an email to a user based on a template.</td>
    <td>Writer, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-get-sender-details-cd</code></td>
    <td>View the sender details for the email.</td>
    <td>Reader, Writer, Manager</td>
  </tr>
  <tr>
    <td><code>appid-mgmt-set-sender-details-cd</code></td>
    <td>Update the sender details.</td>
    <td>Writer, Manager</td>
  </tr>
</table>




## Example: Giving another user access to an instance of {{site.data.keyword.appid_short_notm}}
{: #example}

In this scenario, an administrator created an instance of {{site.data.keyword.appid_short_notm}} and needs to grant viewer access to an employee.

To update their employee's access permissions, the admin completes the following steps:

1. Log in to the {{site.data.keyword.Bluemix_notm}} console.
2. Give the employee view access by following the steps that are laid out in the [IAM documentation](/docs/iam/iamusermanage.html#iamusermanage).
3. Navigate to the **Service credentials** tab of the {{site.data.keyword.appid_short_notm}} dashboard. Click **View credentials** and copy the **tentantID**.
4. Using the {{site.data.keyword.Bluemix_notm}} CLI in your terminal, sign in.
    ```
    bx login -a api.<region>.bluemix.net
    ```
    {: codeblock}
5. Get an IAM token and make a note of it.
    ```
    bx iam oauth-tokens
    ```
    {: codeblock}
6. Verify that the employee cannot make changes.
    ```
    curl -X PUT --header 'Content-Type: application/json' \
    --header 'Accept: application/json' \
    --header 'Authorization: <IAM token value>' \
    -d '{
     "isActive": false,
     "config": {
       "idpId": "appID",
       "secret": "appsecret"
     }
    }' \
    'https://appid-management.stage1.ng.bluemix.net/management/v4/<tenantId>/config/idps/facebook'
    ```
    {: codeblock}

    The result is a 403 unauthorized message.

To view the {{site.data.keyword.appid_short_notm}} configurations from the CLI, the employee completes the following steps:

1. Using the {{site.data.keyword.Bluemix_notm}} CLI in your terminal, sign in.
    ```
    bx login -a api.<region>.bluemix.net
    ```
    {: codeblock}
2. Get an IAM token and make a note of it.
    ```
    bx iam oauth-tokens
    ```
    {: codeblock}
3. Get the identity provider configuration for Facebook by using cURL.
    ```
    curl -X GET --header 'Accept: application/json' --header 'Authorization: <IAM token value>' \  'https://appid-management.ng.bluemix.net/management/v4/<tenantId>/config/idps/facebook'
    ```
    {: codeblock}
    The result is a 200 message that contains the identity provider information.


To try it out yourself, see <a href="https://appid-management.stage1.ng.bluemix.net/swagger-ui/
" target="_blank">the {{site.data.keyword.appid_short_notm}} Management Rest API <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>
</staging>
