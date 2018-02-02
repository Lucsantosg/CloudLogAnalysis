---

copyright:
  years: 2017, 2018

lastupdated: "2018-01-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Getting started tutorial
{: #getting-started-with-cla}

Use this tutorial to learn how to start working with the {{site.data.keyword.loganalysislong}} service in the {{site.data.keyword.Bluemix}}. 
{:shortdesc}

## Objectives
{: #objectives}

* Provision the {{site.data.keyword.loganalysislong}} service in a space.
* Set up the command line to manage logs.
* Set permissions for a user to view logs in a space.
* Launch Kibana, the open source tool that you can use to view logs.


## Before you begin
{: #prereqs}

Your must have a user ID that is a member or an owner of an {{site.data.keyword.Bluemix_notm}} account. To get an {{site.data.keyword.Bluemix_notm}} user ID, go to: [Registration ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/registration/){:new_window}

This tutorial provides instructions to provision and work with the {{site.data.keyword.loganalysisshort}} service in the US South region.


## Step 1: Provision the {{site.data.keyword.loganalysisshort}} service
{: #step1}

**Note:** You provision an instance of the {{site.data.keyword.loganalysisshort}} service in a Cloud Foundry (CF) space. You only need one instance of the service per space. You cannot provision the {{site.data.keyword.loganalysisshort}} service at the account level. 

Complete the following steps to provision an instance of the {{site.data.keyword.loganalysisshort}} service in the {{site.data.keyword.Bluemix_notm}}:

1. Log in to the {{site.data.keyword.Bluemix_notm}}: [http://bluemix.net ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://bluemix.net){:new_window}.  

2. Select the region, organization, and space where you want to provision the {{site.data.keyword.loganalysisshort}} service.  

3. Click **Catalog**. The list of the services that are available on {{site.data.keyword.Bluemix_notm}} opens.

4. Select the **DevOps** category to filter the list of services that is displayed.

5. Click the **Log Analysis** tile.

6. Select a service plan. By default, the **Lite** plan is set.

    For more information about the service plans, see [Service plans](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans).
	
7. Click **Create** to provision the {{site.data.keyword.loganalysisshort}} service in the {{site.data.keyword.Bluemix_notm}} space where you are logged in.




## Step 2: [Optional] Change the service plan for the {{site.data.keyword.loganalysisshort}} service
{: #step2}

If you need more search quota, long term storage of logs, or both, you can change your {{site.data.keyword.loganalysisshort}} service instance plan through the {{site.data.keyword.Bluemix_notm}} UI or by running the `bx cf update-service` command to enable these features. 

You can upgrade or reduce the service plan at any time.

For more information, see [{{site.data.keyword.loganalysisshort}} service plans](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans).

**NOTE:** Changing the plan to a paid plan has a cost.

To change the service plan in the {{site.data.keyword.Bluemix_notm}} UI, complete the following steps:

1. Log in to the {{site.data.keyword.Bluemix_notm}}: [http://bluemix.net ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://bluemix.net){:new_window}.  

2. Select the region, organization, and space where the {{site.data.keyword.loganalysisshort}} service is available.  

3. Click the {{site.data.keyword.loganalysisshort}} service instance from the {{site.data.keyword.Bluemix_notm}} *Dashboard*. 
    
4. Select the **Plan** tab in the {{site.data.keyword.loganalysisshort}} dashboard.

    Information about your current plan is displayed.
	
5. Select a new plan to either upgrade or reduce your plan. 

6. Click **Save**.



## Step 3: Setup your local environment to work with the {{site.data.keyword.loganalysisshort}} service
{: #step3}


The {{site.data.keyword.loganalysisshort}} service includes a command line interface (CLI) that you can use to manage logs that are stored in Log Collection (long term storage component). 

You can use the {{site.data.keyword.loganalysisshort}} {{site.data.keyword.Bluemix_notm}} plugin to view the status of the log, to download logs, and to configure the log retention policy. 

The CLI offers different types of help: general help to learn about the CLI and supported commands, command help to learn how to use a command, or subcommand help to learn how to use a subcommands for a command.

To install the {{site.data.keyword.loganalysisshort}} CLI from the {{site.data.keyword.Bluemix_notm}} repo, complete the following steps:

1. Install the {{site.data.keyword.Bluemix_notm}} CLI.

   For more information, see [Installing the {{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/reference/bluemix_cli/download_cli.html#download_install).

2. Install the {{site.data.keyword.loganalysisshort}} plugin. Run the following command:

    ```
    bx plugin install logging-cli -r Bluemix
    ```
    {: codeblock}
 
3. Verify the {{site.data.keyword.loganalysisshort}} plugin is installed.
  
    For example, run the following command to see the list of plugins that are installed:
    
    ```
    bx plugin list
    ```
    {: codeblock}
    
    The output looks as follows:
   
    ```
    bx plugin list
    Listing installed plug-ins...

    Plugin Name          Version   
    logging-cli          0.1.1   
    ```
    {: screen}




## Step 4: Set permissions for a user to view logs
{: #step4}

To control the {{site.data.keyword.loganalysisshort}} actions that a user is allowed to perform, you can assign roles and policies to a user. 

There are two types of security permissions in the {{site.data.keyword.Bluemix_notm}} that control the actions users can do when they work with the {{site.data.keyword.loganalysisshort}} service:

* Cloud Foundry (CF) roles: You grant a user a CF role to define the permissions that the user has to view logs in a space.
* IAM roles: You grant a user an IAM policy to define the permissions that the user has to view logs in the account domain, and the permissions that the user has to manage logs that are stored in Log Collection. 


Complete the following steps to grant a user permissions to view logs in a space:

1. Log in to the {{site.data.keyword.Bluemix_notm}} console.

    Open a web browser and launch the {{site.data.keyword.Bluemix_notm}} dashboard: [http://bluemix.net ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://bluemix.net){:new_window}
	
	After you log in with your user ID and password, the {{site.data.keyword.Bluemix_notm}} UI opens.

2. From the menu bar, click **Manage > Account > Users**. 

    The *Users* window displays a list of users with their email addresses for the currently selected account.
	
3. If the user is a member of the account, select the user name from the list, or click **Manage user** from the *Actions* menu.

    If the user is not a member of the account, see [Inviting users](/docs/iam/iamuserinv.html#iamuserinv).

4. Select **Cloud Foundry access**, then select the organization.

    The list of spaces available in that organization are listed.

5. Choose the space where you provisioned the {{site.data.keyword.loganalysisshort}} service. Then, from the menu action, select **Edit space role**.

6. Select *Auditor*. 

    You can select 1 or more space roles. All of the following roles allow a user to view logs: *Manager*, *Developer*, and *Auditor*
	
7. Click **Save role**.


For more information, see [Granting permissions](/docs/services/CloudLogAnalysis/security/grant_permissions.html#grant_permissions_ui_account).



## Step 5: Launch Kibana
{: #step5}

To view and analyze log data, you must access Kibana in the cloud Public region where the log data is available. 


To launch Kibana in the US South region, open a web browser, and enter the following URL:

```
https://logging.ng.bluemix.net/ 
```
{: codeblock}


For more information on how to launch Kibana in other regions, see [Navigating to Kibana from a web browser](/docs/services/CloudLogAnalysis/kibana/launch.html#launch_Kibana_from_browser).

**Note:** When you launch Kibana, if you get a message that indicates *bearer token not valid*, check your permissions in the space. This message is an indication that your user ID does not have permissions to see logs.
    

## Next steps 
{: #next_steps}

Generate logs. Try any of the following tutorials:

* [Analyze logs in Kibana for an app that is deployed in a Kubernetes cluster](/docs/services/CloudLogAnalysis/tutorials/container_logs.html#container_logs){:new_window} 

    This tutorial demonstrates the steps that are required to get the following end to end scenario working: Provision a cluster, configure the cluster to send logs to the {{site.data.keyword.loganalysisshort}} service in the {{site.data.keyword.Bluemix_notm}}, deploy an app in the cluster, and use Kibana to view and filter container logs for that cluster.     
    
* [Analyze logs in Kibana for a Cloud Foundry app](/docs/tutorials/application-log-analysis.html#generate-access-and-analyze-application-logs){:new_window}                                                                                                            

    This tutorial demonstrates the steps that are required to get the following end to end scenario working: Deploy aa Python Cloud Foundry application, generate different types of logs, and use Kibana to view, search, and analyze CF logs.
   






