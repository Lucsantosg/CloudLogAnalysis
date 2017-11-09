---

copyright:
  years: 2017

lastupdated: "2017-11-09"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Security
{: #security_ov}

To control the {{site.data.keyword.loganalysisshort}} actions that a user is allowed to perform, you can assign one or more roles to a user. To authenticate a user to work with logs, you need a UAA token or an IAM token.
{:shortdesc}

## Authentication models
{: #auth}

To manage logs through the CLI or the API, you need an authentication token.

The {{site.data.keyword.loganalysisshort}} service supports the following authentication models:

* [UAA authentication](/docs/services/CloudLogAnalysis/security/auth_uaa.html#auth_uaa)

    You can only use the CLI to manage UAA tokens.
	
* [IAM Authentication](/docs/services/CloudLogAnalysis/security/auth_iam.html#auth_iam)

    The IAM authentication model offers UI, CLI, or API management capabilities. 

**Note:** A UAA token and an IAM token expire after a period of time. 

## Roles
{: #roles}

There are two types of roles in the {{site.data.keyword.Bluemix_notm}} that control the actions users can do when they work with the {{site.data.keyword.loganalysisshort}} service:

* Cloud Foundry (CF) roles: You control what {{site.data.keyword.loganalysisshort}} actions a user can do by assigning one or more CF roles. With these roles, you control the user's permissions to view and manage logs in a space or in an organization.
* IAM roles: You control what {{site.data.keyword.loganalysisshort}} actions a user can do by assigning one or more IAM roles. With these roles, you control the user's permissions to view and manage account logs. 


The following table lists the type of roles and the domain in the {{site.data.keyword.Bluemix_notm}} that they control:

<table>
  <caption>Table 1. Type of roles that control actions per domain</caption>
  <tr>
    <th></th>
	<th align="right">Account</th>
    <th align="right">Organization</th>
    <th align="right">Space</th>	
  </tr>
  <tr>
    <td align="left">CF roles</td>
	<td align="center">No</td>
	<td align="center">Yes</td>
	<td align="center">Yes</td>
  </tr>
  <tr>
    <td align="left">IAM roles</td>
	<td align="center">Yes</td>
	<td align="center">No</td>
	<td align="center">No</td>
  </tr>
</table>


## CF roles
{: #bmx_roles}

The following table lists the privileges of each the CF roles to work with the {{site.data.keyword.loganalysisshort}} service:

<table>
  <caption>Table 2. Cloud Foundry roles and privileges to work with the {{site.data.keyword.loganalysisshort}} service.</caption>
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


## IAM roles
{: #iam_roles}

The following table lists the privileges of each of teh IAM roles to work with the {{site.data.keyword.loganalysisshort}} service:

<table>
  <caption>Table 3. IAM roles and privileges to work with the {{site.data.keyword.loganalysisshort}} service.</caption>
  <tr>
    <th>Role</th>
	<th>Privileges</th>
  </tr>
  <tr>
    <td>Administrator</td>
	<td>Delete logs. <br>View information about the logs in a space or at account level. <br>Download logs to a local file or pipe logs to another program such an Elastic stack. <br>Displays the retention period for logs that are available in a space or account. <br>Updates the retention period for logs that are available in a space or account. <br>Lists the active sessions and their IDs. <br>Create a session that you can use to download logs. <br>Delete a session, specified by session ID. <br>Shows the status of a single session. </td>
  </tr>
  <tr>
    <td>Operator</td>
	<td></td>
  </tr>
  <tr>
    <td>Editor</td>
	<td>Delete logs. <br>View information about the logs in a space or at account level. <br>Download logs to a local file or pipe logs to another program such an Elastic stack. <br>Displays the retention period for logs that are available in a space or account. <br>Updates the retention period for logs that are available in a space or account. <br>Lists the active sessions and their IDs. <br>Create a session that you can use to download logs. <br>Delete a session, specified by session ID. <br>Shows the status of a single session. </td>
  </tr>
  <tr>
    <td>Viewer</td>
	<td>View information about the logs in a space or at account level. <br>Displays the retention period for logs that are available in a space or account. <br>Lists the active sessions and their IDs. <br>Shows the status of a single session. </td>
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

## Getting a security token
{: #get_token}

Use the {{site.data.keyword.Bluemix_notm}} CLI or the `Login` REST API, to get the authentication token that you need to work with logs that are available in a {{site.data.keyword.Bluemix_notm}} space or in a {{site.data.keyword.Bluemix_notm}} organization. For more information, see [Getting the UAA token by using the {{site.data.keyword.Bluemix_notm}} CLI](/docs/services/CloudLogAnalysis/security/auth_uaa.html#auth_cli) and [Getting the UAA token by using the API](/docs/services/CloudLogAnalysis/security/auth_uaa.html#auth_api).

Use the {{site.data.keyword.Bluemix_notm}} CLI to get the IAM authentication token that you need to work with account logs in {{site.data.keyword.Bluemix_notm}}. For more information, see [Getting the IAM token by using the Bluemix CLI](/docs/services/CloudLogAnalysis/security/auth_iam.html#iam_token_cli).


## Granting permissions to work with logs
{: #grant_permissions}

In the {{site.data.keyword.Bluemix_notm}}, you can assign one or more roles to users. These roles define what tasks are enabled for that user to work with the {{site.data.keyword.loganalysisshort}} service. 

* [You can grant a user permissions to view account logs by using the {{site.data.keyword.Bluemix_notm}} UI](/docs/services/CloudLogAnalysis/security/grant_permissions.html#grant_permissions_ui_account).
* [You can grant a user permissions to work with space logs by using the {{site.data.keyword.Bluemix_notm}} UI](/docs/services/CloudLogAnalysis/security/grant_permissions.html#grant_permissions_ui_space).
* [You can grant a user permissions to view account logs by using the command line](/docs/services/CloudLogAnalysis/security/grant_permissions.html#grant_permissions_commandline).

