---

copyright:
  years: 2017
lastupdated: "2017-11-20"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Configuring the log retention policy
{: #configuring_retention_policy}

Use the command **bx logging option-show** to view the retention policy that defines the maximum number of days that logs are kept in Log Collection. By default, the retention policy is disabled, and logs are kept indefinitely. After the retention period has expired, logs are deleted automatically. Use the command **bx logging option-update** to change the retention policy.
{:shortdesc}

You can have different retention policies defined in the account. You can have a global account policy and individual space policies. The retention policy that you set at the account level sets the maximum number of days that you can keep logs. If you set a space retention policy for a period of time that is longer than the account level period, the policy that is applied is the last policy that you configure for that space. 


## Disabling the log retention policy for an account
{: #disable_retention_policy_space}

When you disable the retention policy, all logs are kept. 

Complete the following steps to disable a retention policy:

1. Log in to a region, organization, and space in the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
	
2. Get the account ID.

    For more information, see [How do I get the GUID of an account](/docs/services/CloudLogAnalysis/qa/cli_qa.html#account_guid).
    
3. Set the retention period to **-1** to disable the retention period. Run the command:

    ```
    bx logging option-update -r account -i AccountID -e RETENTION_VALUE
	```
    {: codeblock}
	
	The RETENTION_VALUE is a numeric number that defines the number of days.
    
**Example**
    
For example, to disable the retention period for an account with ID *12345677fgh436902a3*, run the following command:

```
bx logging option-update -r account -i 12345677fgh436902a3 -e -1
```
{: codeblock}


## Disabling the log retention policy for a space
{: #disable_retention_policy_space}

When you disable the retention policy, all logs are kept.  

Complete the following steps to disable a retention policy:

1. Log in to a region, organization, and space in the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
    
2. Set the retention period to **-1** to disable the retention period. Run the command:

    ```
    bx logging option-show -e RETENTION_VALUE
	```
    {: codeblock}
	
	The RETENTION_VALUE is a numeric number that defines the number of days.
    
**Example**
    
For example, to disable the retention period for a space with ID *d35da1e3-b345-475f-8502-cfgh436902a3*, run the following command:

```
bx logging option-update -e -1
```
{: codeblock}


## Checking the log retention policy for an account
{: #check_retention_policy_space}

To get the retention period that is set for an account, complete the following steps:

1. Log in to a region, organization, and space in the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).

2. Get the account ID.

    For more information, see [How do I get the GUID of an account](/docs/services/CloudLogAnalysis/qa/cli_qa.html#account_guid).
    
3. Get the the retention period. Run the command:

    ```
    bx logging option-show -r account -i AccountID
    ```
    {: codeblock}

    The output is:

    ```
    bx logging option-show -r account -i kjskdsjfksjdflkjdsfbbd06461b066
    Showing log options of resource: kjskdsjfksjdflkjdsfbbd06461b066 ...

    Resource ID                              Retention   
    a:kjskdsjfksjdflkjdsfbbd06461b066       30   
	```
    {: screen}
	
## Checking the log retention policy for a space
{: #check_retention_policy_space}

To get the retention period that is set for a space, complete the following steps:

1. Log in to a region, organization, and space in the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
    
2. Get the the retention period. Run the command:

    ```
    bx logging option-show
    ```
    {: codeblock}

    The output is:

    ```
    bx logging option-show
    Showing log options of resource: 12345678-1234-2edr-a9de-378620d6fab5 ...

    SpaceId                                Retention   
    12345678-1234-2edr-a9de-378620d6fab5   30   
	```
    {: screen}
    


## Setting an account level log retention policy
{: #set_retention_policy_space}

Complete the following steps:

1. Log in to a region, organization, and space in the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).

2. Get the account ID.

    For more information, see [How do I get the GUID of an account](/docs/services/CloudLogAnalysis/qa/cli_qa.html#account_guid).
    
3. Set the retention period. Run the command:

    ```
    bx logging option-update -r account -i AccountID -e RETENTION_VALUE
    ```
    {: codeblock}
    
    where *RETENTION_VALUE* is an integer that defines the number of days that you want to keep logs. 
    
    
**Example**
    
For example, to keep any type of log in your account for 15 days only, run the following command:

```
bx logging option-update -r account -i AccountID -e 15
```
{: codeblock}



## Setting the log retention policy for a space
{: #set_retention_policy_account}

To see the retention period for a space, complete the following steps:

1. Log in to a region, organization, and space in the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
    
2. Set the retention period. Run the command:

    ```
    bx logging option-update -e RETENTION_VALUE
    ```
    {: codeblock}
    
    where *RETENTION_VALUE* is an integer that defines the number of days that you want to keep logs.
    
    
**Example**
    
For example, to keep logs that are available in a space for a year, run the following command:

```
bx logging option-update -e 365
```
{: codeblock}




