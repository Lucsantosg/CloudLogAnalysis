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


# Calculating the search quota and daily usage
{: #quota}

To get the quota and current daily usage of a logs domain of the {{site.data.keyword.loganalysisshort}} service, you can run a cURL command. 
{:shortdesc}

## Calculating the search quota and daily usage by using the CLI
{: #quota_cli}

Complete the following steps:

1. Log in to the {{site.data.keyword.Bluemix_notm}}.

    For example, to log in to US South, run the command:

    ```
    ibmcloud login -a api.ng.bluemix.net
    ```
    {: codeblock}

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).

2. Run the `ibmcloud logging quota-usage-show` cli command. 

    ```
    ibmcloud logging quota-usage-show [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID]
    ```
    {: codeblock}

    where 

    * Valid RESOURCE_TYPE values are the following: space, account
    * RESOURCE_ID is the GUID of the account or space for which you want to get the quota usage.


For example, to show the quota usage of an account, run the following command:

```
 ibmcloud logging quota-usage-show -r account -i 475693845023932019c6567c9c8de6dece
Showing quota usage for resource: 475693845023932019c6567c9c8de6dece ...
OK

Daily Allotmant   Current Usage   
524288000         0   
```
{: screen}

To show the quota usage of a space, run the following command:

```
ibmcloud logging quota-usage-show -r space -i js7ydf98-8682-430d-bav4-36b712341744
Showing quota usage for resource: js7ydf98-8682-430d-bav4-36b712341744 ...
OK

Daily Allotmant   Current Usage   
524288000         6774014   
```
{: screen}


## Obtaining the search quota history by using the CLI
{: #quota_history_cli}


Complete the following steps:

1. Log in to the {{site.data.keyword.Bluemix_notm}}.

    For example, to log in to US South, run the command:

    ```
    ibmcloud login -a api.ng.bluemix.net
    ```
    {: codeblock}

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).

2. Run the `ibmcloud logging quota-usage-show` cli command with the paramater `-s`. 

    ```
    ibmcloud logging quota-usage-show [-r,--resource-type RESOURCE_TYPE] [-i,--resource-id RESOURCE_ID] [-s,--history]
    ```
    {: codeblock}

    where 

    * Valid RESOURCE_TYPE values are the following: space, account
    * RESOURCE_ID is the GUID of the account or space for which you want to get the quota usage.

For example,

```
ibmcloud logging quota-usage-show -r space -i js7ydf98-8682-430d-bav4-36b712341744 -s
Showing quota usage for resource: js7ydf98-8682-430d-bav4-36b712341744 ...
OK

Date         Allotmant   Usage   
2018.02.28   524288000   80405926   
2018.03.06   524288000   18955540   
2018.03.05   524288000   47262944   
2018.03.08   524288000   18311338   
2018.03.01   524288000   82416831   
2018.03.03   524288000   75045462   
2018.03.07   524288000   17386278   
2018.03.02   524288000   104316444   
2018.03.04   524288000   73125223   
```
{: screen}



## Calculating the search quota and daily usage of an account by using the API
{: #account}

Complete the following steps:

1. Log in to the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).

2. Get the ID of the account. Run the following command:

    ```
	ibmcloud iam accounts
	```
    {: codeblock}	

	A list of accounts with their GUIDs is displayed.
	
	Export the account ID to a shell variable. For example:
	
	```
	export AccountID="1234567891234567812341234123412"
	```
	{: screen}

3. Get the UAA token. 

    For more information, see [Getting the UAA token](/docs/services/CloudLogAnalysis/security/auth_uaa.html#auth_uaa).

    Export the UAA token to a shell variable. Do not include `Bearer`. For example:
	
	```
	export TOKEN="xxxxxxxxxxxxxxxxxxxxx"
	```
	{: screen}

4. Get the quota of the domain and current usage. Run the following command:

    ```
    curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: a-${AccountID}" -XGET ENDPOINT/quota/usage
	```
	{: codeblock}
	
	where *ENDPOINT* is different per region. For a list of endpoints per region, see [Logging endpoints](/docs/services/CloudLogAnalysis/manage_logs.html#endpoints).
	
	For example, run the cURL command to get the quota for the account in the US South region:
	
	```
    curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: a-${AccountID}" -XGET https://logging.ng.bluemix.net/quota/usage
	```
	{: codeblock}
	
	The result includes the information about the daily quota and usage.
	
	```
    curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: a-${AccountID}" -XGET https://logging.ng.bluemix.net/quota/usage
    HTTP/1.1 200 OK
    Server: nginx/1.10.3 (Ubuntu)
    Date: Wed, 29 Nov 2017 13:18:20 GMT
    Content-Type: application/json; charset=utf-8
    Content-Length: 52
    Connection: keep-alive

   {
      "usage": {
        "dailyallotment": 524288000,
        "current": 2115811531
       }
    }
    ```
    {: screen}

	
## Calculating the search quota and daily usage of a space by using the API
{: #space1}

Complete the following steps:

1. Log in to the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).

2. Get the ID of the space.

    For more information, see [How do I get the GUID of a space](/docs/services/CloudLogAnalysis/qa/cli_qa.html#space_guid).
	
	Export the space ID to a shell variable. For example:
	
	```
	export SpaceID="xxxxxxxxxxxxxxxxxxxxx"
	```
	{: screen}

3. Get the UAA token. 

    For more information, see [Getting the UAA token](/docs/services/CloudLogAnalysis/security/auth_uaa.html#auth_uaa).

    Export the UAA token to a shell variable. Do not include `Bearer`. For example:
	
	```
	export TOKEN="xxxxxxxxxxxxxxxxxxxxx"
	```
	{: screen}

4. Get the quota of the domain and current usage. Run the following command:

    ```
    curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: a-${SpaceID}" -XGET ENDPOINT/quota/usage
	```
	{: codeblock}
	
	where *ENDPOINT* is different per region. For a list of endpoints per region, see [Logging endpoints](/docs/services/CloudLogAnalysis/manage_logs.html#endpoints).

    For example, run the following cURL command to get the quota and usage of a space domain in the US South region:
	
    ```
    curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: a-${SpaceID}" -XGET https://logging.ng.bluemix.net/quota/usage
	```
	{: codeblock}
	
	The result includes the information about the daily quota and usage.
	
	```
    curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: a-${SpaceID}" -XGET https://logging.ng.bluemix.net/quota/usage
    HTTP/1.1 200 OK
    Server: nginx/1.10.3 (Ubuntu)
    Date: Wed, 29 Nov 2017 13:18:20 GMT
    Content-Type: application/json; charset=utf-8
    Content-Length: 52
    Connection: keep-alive

   {
      "usage": {
        "dailyallotment": 524288000,
        "current": 2115811531
       }
    }
    ```
    {: screen}



