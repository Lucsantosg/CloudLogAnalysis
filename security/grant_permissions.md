---

copyright:
  years: 2017, 2019

lastupdated: "2019-03-06"

keywords: IBM Cloud, logging

subcollection: cloudloganalysis

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}
{:important: .important}
{:note: .note}

# Granting permissions to manage logs and view account logs
{: #grant_permissions}

In the {{site.data.keyword.Bluemix}}, you can assign a user one or more IAM roles. These roles define what tasks are enabled for that user to work with the {{site.data.keyword.loganalysisshort}} service.  
{:shortdesc}

For example, you can grant a user the **operator** role to allow him to manage logs. If you just want a user to view account logs, then you can grant the user the **viewer** role. For more information, see [IAM roles](/docs/services/CloudLogAnalysis/security_ov.html#iam_roles).

**Note:** 

* To grant a user permissions to manage logs or view account logs, you must have permissions to assign policies to other users in the account, or you must be the account owner. If you are not the account owner, you must have an IAM policy with editor, operator, or administrator role.
* To grant a user permissions to view logs in a space, you must have permissions in the organization and space to assign the user a Cloud Foundry role that describes the actions that this user can do with the {{site.data.keyword.loganalysisshort}} service in that space. 

## Assign an IAM policy to a user through the {{site.data.keyword.Bluemix_notm}} UI
{: #grant_permissions_ui_account}

Complete the following steps to grant a user permissions to work with the {{site.data.keyword.loganalysisshort}} service:

1. Log in to the {{site.data.keyword.Bluemix_notm}} console.

    Open a web browser and launch the {{site.data.keyword.Bluemix_notm}} dashboard: [http://bluemix.net ![External link icon](../../../icons/launch-glyph.svg "External link icon")](http://bluemix.net){:new_window}
	
	After you log in with your user ID and password, the {{site.data.keyword.Bluemix_notm}} UI opens.

2. From the menu bar, click **Manage > Account > Users**. 

    The *Users* window displays a list of users with their email addresses for the currently selected account.
	
3. If the user is a member of the account, select the user name from the list, or click **Manage user** from the *Actions* menu.

    If the user is not a member of the account, see [Inviting users](/docs/iam/iamuserinv.html#iamuserinv).

4. In the **Access policies** section, click **Assign access**, then select **Assign access to resources**.

    The *Assign resource access to user** window opens.

5. Enter information about the policy. The following table lists the fields that are required to define a policy: 

    <table>
	  <caption>List of fields to configure an IAM policy.</caption>
	  <tr>
	    <th>Field</th>
		<th>Value</th>
	  </tr>
	  <tr>
	    <td>Services</td>
		<td>*IBM Cloud Log Analysis*</td>
	  </tr>	  
	  <tr>
	    <td>Regions</td>
		<td>You can specify the regions where the user is going to be granted access to work with logs. Select one or more regions individually, or select **All current regions** to grant access to all regions.</td>
	  </tr>
	  <tr>
	    <td>Service instance</td>
		<td>Select *All service instances*.</td>
	  </tr>
	  <tr>
	    <td>Roles</td>
		<td>Select one or more IAM roles. <br>Valid roles are: *administrator*, *operator*, *editor*, and *viewer*. <br>For more information about the actions that are allowed per role, see [IAM roles](/docs/services/CloudLogAnalysis/security_ov.html#iam_roles).
		</td>
	  </tr>
     </table>
	
6. Click **Assign**.
	
The policy that you configure is applicable to the selected regions. 


## Assign an IAM policy to a user by using the command line
{: #grant_permissions_commandline}

Complete the following steps to grant a user access to view account logs by using the command line:

1. From a terminal, log in to the {{site.data.keyword.Bluemix_notm}} account. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).

2. Check that the user is a member of the account. Run the following command to get the list of users in the account:

    ```
	ibmcloud account users
	```
    {: codeblock}	

	A list of users with their GUIDs is displayed.

3. If the user is not a member of the account, contact the account owner and request an invite of the user to the account. For more information, see [Inviting users](/docs/iam/iamuserinv.html#iamuserinv).

    **Tip:** The command to invite a user to an account is the following: `ibmcloud iam account-user-invite USER_EMAIL`
		
4. Assign a policy to the user. Run the following command:

    ```
    ibmcloud iam user-policy-create USER_NAME --roles ROLE --service-name ibmloganalysis
	```
	{: codeblock}

	where
    * USER_NAME is the {{site.data.keyword.Bluemix_notm}} ID of the user.
	* ROLE is an IAM role. Valid values are: *administrator*, *operator*, *editor*, and *viewer*

5. Verify that the policy is assigned to the user. Run the following command to list all the policies assigned to a user:

    ```
    ibmcloud iam user-policies USER_NAME
	```
	{: codeblock}




## Granting a user permissions to view space logs by using the {{site.data.keyword.Bluemix_notm}} UI
{: #grant_permissions_ui_space}

To grant a user permissions to view logs in a space, you must assign the user a Cloud Foundry role that describes the actions that this user can do with the {{site.data.keyword.loganalysisshort}} service in the space. 

Complete the following steps to grant a user permissions to work with the {{site.data.keyword.loganalysisshort}} service:

1. Log in to the {{site.data.keyword.Bluemix_notm}} console.

    Open a web browser and launch the {{site.data.keyword.Bluemix_notm}} dashboard: [http://bluemix.net ![External link icon](../../../icons/launch-glyph.svg "External link icon")](http://bluemix.net){:new_window}
	
	After you log in with your user ID and password, the {{site.data.keyword.Bluemix_notm}} UI opens.

2. From the menu bar, click **Manage > Account > Users**. 

    The *Users* window displays a list of users with their email addresses for the currently selected account.
	
3. If the user is a member of the account, select the user name from the list, or click **Manage user** from the *Actions* menu.

    If the user is not a member of the account, see [Inviting users](/docs/iam/iamuserinv.html#iamuserinv).

4. Select **Cloud Foundry access**, then select the organization.

    The list of spaces available in that organization are listed.

5. Choose one space. Then, from the menu action, select **Edit space role**.

6. Select 1 or more space roles. Valid roles are: *Manager*, *Developer*, and *Auditor*
	
7. Click **Save role**.




