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

# Configuring the log retention policy
{: #configuring_retention_policy}

By default, the retention policy is disabled, and logs are kept indefinitely. Use the command **ibmcloud logging option-update** to change the retention policy.
{:shortdesc}

You can use the command **ibmcloud logging option-show** to view the retention policy that defines the maximum number of days that logs are kept in Log Collection. 

When you set a retention policy, after the retention period has expired, logs are deleted automatically.


## Disabling the log retention policy for an account
{: #disable_retention_policy_acc}

When you disable the retention policy, all logs are kept. 

Complete the following steps to disable a retention policy:

1. Log in to a region, organization, and space in the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa?topic=cloudloganalysis-cli_qa#login).
	
2. Get the account ID.

    For more information, see [How do I get the GUID of an account](/docs/services/CloudLogAnalysis/qa?topic=cloudloganalysis-cli_qa#account_guid).
    
3. Set the retention period to **-1** to disable the retention period. Run the command:

    ```
    ibmcloud logging option-update -r account -i AccountID -e RETENTION_VALUE
	```
    {: codeblock}
	
	The RETENTION_VALUE is a numeric number that defines the number of days.
    
**Example**
    
For example, to disable the retention period for an account with ID *12345677fgh436902a3*, run the following command:

```
ibmcloud logging option-update -r account -i 12345677fgh436902a3 -e -1
```
{: codeblock}


## Disabling the log retention policy for a space
{: #disable_retention_policy_space}

When you disable the retention policy, all logs are kept.  

Complete the following steps to disable a retention policy:

1. Log in to a region, organization, and space in the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa?topic=cloudloganalysis-cli_qa#login).
    
2. Set the retention period to **-1** to disable the retention period. Run the command:

    ```
    ibmcloud logging option-show -e RETENTION_VALUE
	```
    {: codeblock}
	
	The RETENTION_VALUE is a numeric number that defines the number of days.
    
**Example**
    
For example, to disable the retention period for a space with ID *d35da1e3-b345-475f-8502-cfgh436902a3*, run the following command:

```
ibmcloud logging option-update -e -1
```
{: codeblock}


## Checking the log retention policy for an account
{: #check_retention_policy_acc}

To get the retention period that is set for an account, complete the following steps:

1. Log in to a region, organization, and space in the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa?topic=cloudloganalysis-cli_qa#login).

2. Get the account ID.

    For more information, see [How do I get the GUID of an account](/docs/services/CloudLogAnalysis/qa?topic=cloudloganalysis-cli_qa#account_guid).
    
3. Get the retention period. Run the command:

    ```
    ibmcloud logging option-show -r account -i AccountID
    ```
    {: codeblock}

    The output is:

    ```
    ibmcloud logging option-show -r account -i kjskdsjfksjdflkjdsfbbd06461b066
    Showing log options of resource: kjskdsjfksjdflkjdsfbbd06461b066 ...

    Resource ID                              Retention   
    a:kjskdsjfksjdflkjdsfbbd06461b066       30   
	```
    {: screen}
	
## Checking the log retention policy for a space
{: #check_retention_policy_space}

To get the retention period that is set for a space, complete the following steps:

1. Log in to a region, organization, and space in the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa?topic=cloudloganalysis-cli_qa#login).
    
2. Get the retention period. Run the command:

    ```
    ibmcloud logging option-show
    ```
    {: codeblock}

    The output is:

    ```
    ibmcloud logging option-show
    Showing log options of resource: 12345678-1234-2edr-a9de-378620d6fab5 ...

    SpaceId                                Retention   
    12345678-1234-2edr-a9de-378620d6fab5   30   
	```
    {: screen}
    


## Setting an account level log retention policy
{: #set_retention_policy_acc}

Complete the following steps:

1. Log in to a region, organization, and space in the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa?topic=cloudloganalysis-cli_qa#login).

2. Get the account ID.

    For more information, see [How do I get the GUID of an account](/docs/services/CloudLogAnalysis/qa?topic=cloudloganalysis-cli_qa#account_guid).
    
3. Set the retention period. Run the command:

    ```
    ibmcloud logging option-update -r account -i AccountID -e RETENTION_VALUE
    ```
    {: codeblock}
    
    where *RETENTION_VALUE* is an integer that defines the number of days that you want to keep logs. 
    
    
**Example**
    
For example, to keep any type of log in your account for 15 days only, run the following command:

```
ibmcloud logging option-update -r account -i AccountID -e 15
```
{: codeblock}



## Setting the log retention policy for a space
{: #set_retention_policy_space}

To see the retention period for a space, complete the following steps:

1. Log in to a region, organization, and space in the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa?topic=cloudloganalysis-cli_qa#login).
    
2. Set the retention period. Run the command:

    ```
    ibmcloud logging option-update -e RETENTION_VALUE
    ```
    {: codeblock}
    
    where *RETENTION_VALUE* is an integer that defines the number of days that you want to keep logs.
    
    
**Example**
    
For example, to keep logs that are available in a space for a year, run the following command:

```
ibmcloud logging option-update -e 365
```
{: codeblock}




