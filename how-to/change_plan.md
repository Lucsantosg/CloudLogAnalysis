---

copyright:
  years: 2017, 2019

lastupdated: "2019-05-01"

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
{:deprecated: .deprecated}


# Changing the plan
{: #change_plan}

You can change your {{site.data.keyword.loganalysisshort}} service plan through the {{site.data.keyword.cloud_notm}} UI or by running the `ibmcloud service update` command. You can upgrade or reduce your plan at any time.
{:shortdesc}

{{site.data.keyword.loganalysisfull_notm}} is deprecated. As of 30 April 2019, you cannot provision new {{site.data.keyword.loganalysisshort_notm}} instances. Existing premium plan instances are supported until 30 September 2019. To continue managing system and application logs in {{site.data.keyword.cloud_notm}}, [set up {{site.data.keyword.la_full_notm}}](/docs/services/Log-Analysis-with-LogDNA?topic=LogDNA-getting-started#getting-started).
{: deprecated}

## Changing the service plan through the UI
{: #change_plan_ui}

To change your service plan in the {{site.data.keyword.cloud_notm}} UI, complete the following steps:

1. Log in to the {{site.data.keyword.cloud_notm}}: [https://cloud.ibm.com/login ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/login){:new_window}. 

2. Select the region, organization, and space where the {{site.data.keyword.loganalysisshort}} service is available.  

3. Click the {{site.data.keyword.loganalysisshort}} service instance from the {{site.data.keyword.cloud_notm}} *Dashboard*. 
    
4. Select the **Plan** tab in the {{site.data.keyword.loganalysisshort}} dashboard.

    Information about your current plan is displayed.
	
5. Select a new plan to either upgrade or reduce your plan. 

6. Click **Save**.




## Changing the service plan through the CLI
{: #change_plan_cli}

To change your service plan in Bluemix through the CLI, complete the following steps:

1. Log in to a region, organization, and space in the {{site.data.keyword.cloud_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.cloud_notm}}](/docs/services/CloudLogAnalysis/qa?topic=cloudloganalysis-cli_qa#login).
	
2. Run the `ibmcloud service list` command to check your current plan, and to get the {{site.data.keyword.loganalysisshort}} service name from the list of services that is available in the space. 

    The value of the field **name** is the one that you must use to change the plan. 

    For example,
	
	```
	$ ibmcloud service list
    Invoking 'cf services'...

    Getting services in org MyOrg / space dev as xxx@ibm.com...
    OK

    name                           service                  plan             bound apps            last operation
    Log Analysis-m2                ibmLogAnalysis           premium                                update succeeded
    ```
	{: screen}
    
3. Upgrade or reduce your plan. Run the `ibmcloud service update` command.
    
	```
	ibmcloud service update service_name [-p new_plan]
	```
	{: codeblock}
	
	where 
	
	* *service_name* is the name of your service. You can run the `ibmcloud service list` command to get the value.
	* *new_plan* is the name of the plan.
	
	The following table lists the different plans and their supported values:
	
	<table>
	  <caption>Table 1. List of plans.</caption>
	  <tr>
	    <th>Plan</th>
	    <th>Name</th>
	  </tr>
	  <tr>
	    <td>Lite</td>
	    <td>standard</td>
	  </tr>
	  <tr>
	    <td>Log Collection</td>
	    <td>premium</td>
	  </tr>
	  <tr>
	    <td>Log Collection with 2 GB/Day Search</td>
	    <td>premiumsearch2</td>
	  </tr>
	  <tr>
	    <td>Log Collection with 5 GB/Day Search</td>
	    <td>premiumsearch5</td>
	  </tr>
	  <tr>
	    <td>Log Collection with 10 GB/Day Search</td>
	    <td>premiumsearch10</td>
	  </tr>
	</table>
	
	For example, to reduce your plan to the *Lite* plan, run the following command:
	
	```
	ibmcloud service update "Log Analysis-m2" -p standard
    Updating service instance Log Analysis-m2 as xxx@ibm.com...
    OK
	```
	{: screen}

4. Verify the new plan is changed. Run the `ibmcloud service list` command.

  ```
	ibmcloud service list
	```
	{: codeblock}





