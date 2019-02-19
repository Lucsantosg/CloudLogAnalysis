---

copyright:
  years: 2017, 2018

lastupdated: "2018-07-25"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Frequent questions and answers using the IBM Cloud CLI
{: #cli_qa}

Here are the answers to common questions about using the {{site.data.keyword.Bluemix}} CLI with the {{site.data.keyword.loganalysisshort}} service. 
{:shortdesc}

* [How do I log into the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login)
* [How do I install the {{site.data.keyword.Bluemix_notm}} CLI](/docs/services/CloudLogAnalysis/qa/cli_qa.html#install_bmx_cli)
* [How do I get the GUID of an account](/docs/services/CloudLogAnalysis/qa/cli_qa.html#account_guid)
* [How do I get the GUID of an organization](/docs/services/CloudLogAnalysis/qa/cli_qa.html#org_guid)
* [How do I get the GUID of a space](/docs/services/CloudLogAnalysis/qa/cli_qa.html#space_guid)

## How do I login into the IBM Cloud?
{: #login}

Run the following command to log into a region in the {{site.data.keyword.Bluemix_notm}} where the {{site.data.keyword.loganalysisshort}} service is available:

```
ibmcloud login -a Endpoint
```
{: codeblock}
	
Where *Endpoint* is the URL to log into the {{site.data.keyword.Bluemix_notm}}. This URL is different per region.
	
<table>
    <caption>List of endpoints to access the {{site.data.keyword.Bluemix_notm}}</caption>
	<tr>
	  <th>Region</th>
	  <th>URL</th>
	</tr>
	<tr>
	  <td>Germany</td>
	  <td>api.eu-de.bluemix.net</td>
	</tr>
	<tr>
	  <td>Sydney</td>
	  <td>api.au-syd.bluemix.net</td>
	</tr>
	<tr>
	  <td>US South</td>
	  <td>api.ng.bluemix.net</td>
	</tr>
	<tr>
	  <td>United Kingdom</td>
	  <td>api.eu-gb.bluemix.net</td>
	</tr>
</table>

For example, to log into the US South region, run the following command:
	
```
ibmcloud login -a https://api.ng.bluemix.net
```
{: codeblock}

Follow the instructions. 

You can also set an organization and a space. Run the following command:

```
ibmcloud target -o OrgName -s SpaceName
```
{: codeblock}

where

* OrgName is the name of the organization.
* SpaceName is the name of the space.

	
	
## How do I install the IBM Cloud CLI?
{: #install_bmx_cli}

See [Download and install the {{site.data.keyword.Bluemix}} CLI](/docs/cli/index.html#overview).



## How do I get the GUID of an account
{: #account_guid}
	
Complete the following steps to get the GUID of an account:
	
1. Log in to a region in the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
	
2. Run the `ibmcloud iam accounts` command to get the GUID of an account.

    ```
	ibmcloud iam accounts
	```
	{: codeblock} 
	
	For example, to retrieve all the accounts with their corresponding GUIDs for user xxx@yyy.com, run the command:
	
	```
	ibmcloud iam accounts
	Retrieving all accounts of xxx@yyy.com...
    OK
    Account GUID                       Name                               Type    State    Owner User ID   
    12345123451234512345123451234512   A Account                          TRIAL   ACTIVE   xxx@yyy.com   
    23456234562345622456234561234561   B Account                          TRIAL   ACTIVE   zzz@yyy.com   
	```
	{: screen}

	
## How do I get the GUID of an organization
{: #org_guid}

Complete the following steps to get the GUID of an organization:
	
1. Log in to a region, organization, and space in the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).

2. Run the `ibmcloud iam org` command to get the organization GUID. 

    ```
    ibmcloud iam org NAME --guid
    ```
    {: codeblock}
	
    where NAME is the name of the {{site.data.keyword.Bluemix_notm}} organization.        
		
		
		
## How do I get the GUID of a space
{: #space_guid2}
	
Complete the following steps to get the GUID of a space:
	
1. Log in to a region, organization, and space in the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
	
2. Run the `ibmcloud iam space` command to get the space GUID. 

    ```
    ibmcloud iam space NAME --guid
    ```
    {: codeblock}
	
    where NAME is the name of a {{site.data.keyword.Bluemix_notm}} space. 
	
    For example, to get the GUID for the space *dev*, run the following command:
	
    ```
    ibmcloud iam space dev --guid
    e03afff1-3456-4af6-1234-59treg1b0abc
    ```
    {: screen}




		
		