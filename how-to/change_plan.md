---

copyright:
  years: 2017, 2018

lastupdated: "2018-01-10"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Changing the plan
{: #change_plan}

You can change your {{site.data.keyword.loganalysisshort}} service plan through the {{site.data.keyword.Bluemix_notm}} UI or by running the `bx cf update-service` command. You can upgrade or reduce your plan at any time.
{:shortdesc}

## Changing the service plan through the UI
{: #change_plan_ui}

To change your service plan in the {{site.data.keyword.Bluemix_notm}} UI, complete the following steps:

1. Log in to the {{site.data.keyword.Bluemix_notm}}: [http://bluemix.net ![External link icon](../../../icons/launch-glyph.svg "External link icon")](http://bluemix.net){:new_window}. 

2. Select the region, organization, and space where the {{site.data.keyword.loganalysisshort}} service is available.  

3. Click the {{site.data.keyword.loganalysisshort}} service instance from the {{site.data.keyword.Bluemix_notm}} *Dashboard*. 
    
4. Select the **Plan** tab in the {{site.data.keyword.loganalysisshort}} dashboard.

    Information about your current plan is displayed.
	
5. Select a new plan to either upgrade or reduce your plan. 

6. Click **Save**.




## Changing the service plan through the CLI
{: #change_plan_cli}

To change your service plan in Bluemix through the CLI, complete the following steps:

1. Log in to a region, organization, and space in the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
	
2. Run the `bx cf services` command to chech your current plan, and to get the {{site.data.keyword.loganalysisshort}} service name from the list of services that is available in the space. 

    The value of the field **name** is the one that you must use to change the plan. 

    For example,
	
	```
	$ bx cf services
    Getting services in org MyOrg / space dev as xxx@yyy.com...
    OK
    
    name              service          plan      bound apps   last operation
    Log Analysis-a4   ibmLogAnalysis   premium                create succeeded
    ```
	{: screen}
    
3. Upgrade or reduce your plan. Run the `bx cf update-service` command.
    
	```
	bx cf update-service service_name [-p new_plan]
	```
	{: codeblock}
	
	where 
	
	* *service_name* is the name of your service. You can run the `bx cf services` command to get the value.
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
	bx cf update-service "Log Analysis-a4" -p standard
    Updating service instance Log Analysis-a4 as xxx@yyy.com...
    OK
	```
	{: screen}

4. Verify the new plan is changed. Run the `cf services` command.

    ```
	bx cf services
    Getting services in org MyOrg / space dev as xxx@yyy.com...
    OK

    name              service          plan       bound apps   last operation
    Log Analysis-a4   ibmLogAnalysis   standard                update succeeded
	```
	{: screen}





