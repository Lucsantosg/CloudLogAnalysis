---

copyright:
  years: 2017
lastupdated: "2017-07-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Configuring the log retention policy
{: #configuring_retention_policy}

Use the command **cf logging option** to view and configure the retention policy that defines the maximum number of days that logs are kept in Log Collection. By default, logs are kept for 30 days. After the retention period has expired, logs are deleted automatically. By default, the retention policy is disabled.
{:shortdesc}

You can have different retention policies defined in the account. You can have a global account policy and individual space policies. The retention policy that you set at the account level sets the maximum number of days that you can keep logs. If you set a space retention policy for a period of time that is longer than the account level period, the policy that is applied is the last policy that you configure for that space. 


## Disabling the log retention policy for a space
{: #disable_retention_policy_space}

Complete the following steps to disable a retention policy:

1. Log in to the {{site.data.keyword.Bluemix_notm}} region, organization, and space where you want to set a log retention policy. 

    For example, to log in to the US South region, run the following command:
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Set the retention period to **-1** to disable the retention period. Run the command:

    ```
    cf logging option -r -1
    ```
    {: codeblock}
    
**Example**
    
For example, to disable the retention period for a space with ID *d35da1e3-b345-475f-8502-cfgh436902a3*, run the following command:

```
cf logging option -r -1
```
{: codeblock}

The output is:

```
+--------------------------------------+-----------+
|               SPACEID                | RETENTION |
+--------------------------------------+-----------+
| d35da1e3-b345-475f-8502-cfgh436902a3 |        -1 |
+--------------------------------------+-----------+
```
{: screen} 



## Checking the log retention policy for a space
{: #check_retention_policy_space}

To get the retention period that is set for a {{site.data.keyword.Bluemix_notm}} space, complete the following steps:

1. Log in to the {{site.data.keyword.Bluemix_notm}} region, organization, and space where you want to set a log retention policy. 

    For example, to log in to the US South region, run the following command:
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Get the the retention period. Run the command:

    ```
    cf logging option
    ```
    {: codeblock}

    The output is:

    ```
    +--------------------------------------+-----------+
    |               SPACEID                | RETENTION |
    +--------------------------------------+-----------+
    | d35da1e3-b345-475f-8502-cfgh436902a3 |        30 |
    +--------------------------------------+-----------+
    ```
    {: screen}
    

## Checking the log retention policy for all spaces in an account
{: #check_retention_policy_account}

To get the retention period that is set for each {{site.data.keyword.Bluemix_notm}} space in an account, complete the following steps:

1. Log in to the {{site.data.keyword.Bluemix_notm}} region, organization, and space where you want to set a log retention policy. 

    For example, to log in to the US South region, run the following command:
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Get the the retention period for each space in the account. Run the command:

    ```
    cf logging option -a
    ```
    {: codeblock}

    The output is:

    ```
    +--------------------------------------+-----------+
    |               SPACEID                | RETENTION |
    +--------------------------------------+-----------+
    | d35da1e3-b345-475f-8502-cfgh436902a3 |        30 |
    +--------------------------------------+-----------+
    | fdew45e3-b345-4365-8502-cfghrfthy5a3 |        30 |
    +--------------------------------------+-----------+
    ```
    {: screen}
    

## Setting an account level log retention policy
{: #set_retention_policy_space}

To see the retention period for a {{site.data.keyword.Bluemix_notm}} account, complete the following steps:

1. Log in to the {{site.data.keyword.Bluemix_notm}} region, organization, and space where you want to set a log retention policy. 

    For example, to log in to the US South region, run the following command:
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Set the retention period. Run the command:

    ```
    cf logging option -r *Number_of_days* - a
    ```
    {: codeblock}
    
    where *Number_of_days* is an integer that defines the number of days that you want to keep logs. 
    
    
**Example**
    
For example, to keep any type of log in your account for 15 days only, run the following command:

```
cf logging option -r 15 -a
```
{: codeblock}

The output lists an entry for each space in the account, including information about the retention period:

```
+--------------------------------------+-----------+
|               SPACEID                | RETENTION |
+--------------------------------------+-----------+
| d35da1e3-b345-475f-8502-cfgh436902a3 |        15 |
+--------------------------------------+-----------+
| fdew45e3-b345-4365-8502-cfghrfthy5a3 |        30 |
+--------------------------------------+-----------+
```
{: screen}

## Setting the log retention policy for a space
{: #set_retention_policy_account}

To see the retention period for a {{site.data.keyword.Bluemix_notm}} space, complete the following steps:

1. Log in to the {{site.data.keyword.Bluemix_notm}} region, organization, and space where you want to set a log retention policy. 

    For example, to log in to the US South region, run the following command:
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Set the retention period. Run the command:

    ```
    cf logging option -r *Number_of_days*
    ```
    {: codeblock}
    
    where *Number_of_days* is an integer that defines the number of days that you want to keep logs.
    
    
**Example**
    
For example, to keep logs that are available in a space for a year, run the following command:

```
cf logging option -r 365
```
{: codeblock}

The output is:

```
+--------------------------------------+-----------+
|               SPACEID                | RETENTION |
+--------------------------------------+-----------+
| d35da1e3-b345-475f-8502-cfgh436902a3 |       365 |
+--------------------------------------+-----------+
```
{: screen}


