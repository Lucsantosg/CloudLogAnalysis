---

copyright:
  years: 2017

lastupdated: "2017-08-25"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Security
{: #security_ov}

You can use different authentication methods to use the {{site.data.keyword.loganalysisshort}} service. Permissions to collect, store, and analyze your application’s log data are controlled by using roles.
{:shortdesc}

   
## Authentication models
{: #auth}

To retrieve data from the {{site.data.keyword.loganalysisshort}} service for a {{site.data.keyword.Bluemix_notm}} space, you require an authentication token or API key. 

The {{site.data.keyword.loganalysisshort}} service supports the following authentication models:

* [{{site.data.keyword.Bluemix_notm}} UAA authentication](/docs/services/CloudLogAnalysis/security/auth_uaa.html#auth_uaa)
* [{{site.data.keyword.Bluemix_notm}} IAM Authentication](/docs/services/CloudLogAnalysis/security/auth_iam.html#auth_iam)

**Note:** A UAA token and an IAM token expire after a period of time. 

The IAM authentication model offers UI, CLI, or API management capabilities. You can only use the CLI to manage UAA tokens.

The following table lists the authentication models that are supported for each type of domain in {{site.data.keyword.Bluemix_notm}}:

<table>
  <caption>Table 1. Auth models supported for each domain</caption>
  <tr>
    <th></th>
	<th align="right">Account</th>
    <th align="right">Organization</th>
    <th align="right">Space</th>	
  </tr>
  <tr>
    <td align="left">UAA</td>
	<td align="center">No</td>
	<td align="center">Yes</td>
	<td align="center">Yes</td>
  </tr>
  <tr>
    <td align="left">IAM</td>
	<td align="center">Yes</td>
	<td align="center">No</td>
	<td align="center">No</td>
  </tr>
</table>

The {{site.data.keyword.loganalysisshort}} service uses the IAM access control feature to govern what actions or operations a user or service can perform against the domain. For example, you can define an IAM policy to allow a user to send and create dashboards against a domain, but not to retrieve the logs from the domain. For more information about IAM, see [Managing Users and Access in IAM](/docs/iam/users_roles.html#userroles)


## Bluemix UAA roles
{: #bmx_roles}

The following table lists the privileges of each {{site.data.keyword.Bluemix_notm}} role to work with the {{site.data.keyword.loganalysisshort}} service:

<table>
  <caption>Table 2. {{site.data.keyword.Bluemix_notm}} roles and privileges to work with the {{site.data.keyword.loganalysisshort}} service.</caption>
  <tr>
    <th>Role</th>
	<th>Domain</th>
	<th>Access privileges</th>
  </tr>
  <tr>
    <td>Manager</td>
	<td>Organization <br>Space</td>
	<td>All RESTful APIs</td>
  </tr>
  <tr>
    <td>Developer</td>
	<td>Space</td>
	<td>All RESTful APIs</td>
  </tr>
  <tr>
    <td>Auditor</td>
	<td>Organization <br>Space</td>
	<td>Only RESTful APIs that perform read only operations, like query logs.</td>
  </tr>
</table>


## Bluemix IAM roles
{: #iam_roles}

The following table lists the privileges of each {{site.data.keyword.Bluemix_notm}} role to work with the {{site.data.keyword.loganalysisshort}} service:

<table>
  <caption>Table 3. IAM roles and privileges to work with the {{site.data.keyword.loganalysisshort}} service.</caption>
  <tr>
    <th>Role</th>
	<th>Privileges</th>
  </tr>
  <tr>
    <td>Administrator</td>
	<td>Delete logs. <br>View information about the logs in a {{site.data.keyword.Bluemix_notm}} space or at account level. <br>Download logs to a local file or pipe logs to another program such an Elastic stack. <br>Displays the retention period for logs that are available in a {{site.data.keyword.Bluemix_notm}} space or account. <br>Updates the retention period for logs that are available in a {{site.data.keyword.Bluemix_notm}} space or account. <br>Lists the active sessions and their IDs. <br>Create a session that you can use to download logs. <br>Delete a session, specified by session ID. <br>Shows the status of a single session. </td>
  </tr>
  <tr>
    <td>Operator</td>
	<td></td>
  </tr>
  <tr>
    <td>Editor</td>
	<td>Delete logs. <br>View information about the logs in a {{site.data.keyword.Bluemix_notm}} space or at account level. <br>Download logs to a local file or pipe logs to another program such an Elastic stack. <br>Displays the retention period for logs that are available in a {{site.data.keyword.Bluemix_notm}} space or account. <br>Updates the retention period for logs that are available in a {{site.data.keyword.Bluemix_notm}} space or account. <br>Lists the active sessions and their IDs. <br>Create a session that you can use to download logs. <br>Delete a session, specified by session ID. <br>Shows the status of a single session. </td>
  </tr>
  <tr>
    <td>Viewer</td>
	<td>View information about the logs in a {{site.data.keyword.Bluemix_notm}} space or at account level. <br>Displays the retention period for logs that are available in a {{site.data.keyword.Bluemix_notm}} space or account. <br>Lists the active sessions and their IDs. <br>Shows the status of a single session. </td>
  </tr>
</table>

The following table lists the relationship between the API, a service action, and an IAM role that is used by the {{site.data.keyword.loganalysisshort}} service.

<table>
  <caption>Table 4. Relationship between the API, a service action, and an IAM role. </caption>
  <tr>
    <th>API</th>
	<th>Action</th>
	<th>IAM role</th>
	<th>Description</th>
  </tr>
  <tr>
    <td>DELETE /v1/logging/logs</td>
    <td>ibmcloud-log-analysis.domain.log_delete</td>
	<td>Administrator, Editor</td>
	<td>Delete logs.</td>
  </tr>
  <tr>
    <td>GET /v1/logging/logs</td>
    <td>ibmcloud-log-analysis.domain.log_read</td>
	<td>Administrator, Editor, Viewer</td>
	<td>View information about the logs in a {{site.data.keyword.Bluemix_notm}} space or at account level.</td>
  </tr>
  <tr>
    <td>GET /v1/logging/logs/download</td>
    <td>ibmcloud-log-analysis.domain.log_download</td>
	<td>Administrator, Editor</td>
	<td>Download logs to a local file or pipe logs to another program such an Elastic stack.</td>
  </tr>
  <tr>
    <td>GET /v1/logging/logs/retention</td>
    <td>ibmcloud-log-analysis.domain.policy_read</td>
    <td>Administrator, Editor, Viewer</td>
    <td>Displays the retention period for logs that are available in a {{site.data.keyword.Bluemix_notm}} space or account.</td>
  </tr>
  <tr>
    <td>PUT /v1/logging/logs/retention</td>
    <td>ibmcloud-log-analysis.domain.policy_write</td>
    <td>Administrator, Editor</td>
    <td>Updates the retention period for logs that are available in a {{site.data.keyword.Bluemix_notm}} space or account.</td>
  </tr>
  <tr>
    <td>GET /v1/logging/sessions</td>
    <td>ibmcloud-log-analysis.domain.session_read</td>
    <td>Administrator, Editor, Viewer</td>
    <td>Lists the active sessions and their IDs.</td>
  </tr>
  <tr>
    <td>POST /v1/logging/sessions</td>
    <td>ibmcloud-log-analysis.domain.session_write</td>
    <td>Administrator, Editor</td>
    <td>Create a session that you can use to download logs.</td>
  </tr>
  <tr>
    <td>DELETE /v1/logging/sessions/{id}</td>
    <td>ibmcloud-log-analysis.domain.session_delete</td>
    <td>Administrator, Editor</td>
    <td>Delete a session, specified by session ID.</td>
  </tr>
  <tr>
    <td>GET /v1/logging/sessions/{id}</td>
    <td>ibmcloud-log-analysis.domain.session_read</td>
    <td>Administrator, Editor, Viewer</td>
    <td>Shows the status of a single session.</td>
  </tr>
</table>

## Getting the security token
{: #get_token}

Use the {{site.data.keyword.Bluemix_notm}} UAA model to get an authentication token that you can use to access data that is stored in the {{site.data.keyword.loganalysisshort}} service for a space in {{site.data.keyword.Bluemix_notm}}. You can obtain the authentication token by using the {{site.data.keyword.Bluemix_notm}} CLI or by using the `Login` REST API. For more information, see [Getting the UAA token by using the {{site.data.keyword.Bluemix_notm}} CLI](/docs/services/CloudLogAnalysis/security/auth_uaa.html#auth_cli) and [Getting the UAA token by using the API](/docs/services/CloudLogAnalysis/security/auth_uaa.html#auth_api).

Use the {{site.data.keyword.Bluemix_notm}} IAM model to get an authentication token that you can use to access data that is stored in the {{site.data.keyword.loganalysisshort}} service. For more information, see [Authenticating by using the Bluemix IAM model](/docs/services/CloudLogAnalysis/security/auth_iam.html#iam_token_cli).
