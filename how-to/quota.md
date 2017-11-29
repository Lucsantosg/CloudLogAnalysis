---

copyright:
  years: 2017

lastupdated: "2017-11-29"

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


## Calculating the search quota and daily usage of an account
{: #account}

Complete the following steps:

1. Log in to the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).

2. Get the ID of the account. Run the following command:

    ```
	bx iam accounts
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
	
	The result includes the information about the daily quota and usage in bytes.
	
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

	
## Calculating the search quota and daily usage of a space
{: #space}

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
    curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: s-${SpaceID}" -XGET ENDPOINT/quota/usage
	```
	{: codeblock}
	
	where *ENDPOINT* is different per region. For a list of endpoints per region, see [Logging endpoints](/docs/services/CloudLogAnalysis/manage_logs.html#endpoints).

    For example, run the following cURL command to get the quota and usage of a space domain in the US South region:
	
    ```
    curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: s-${SpaceID}" -XGET https://logging.ng.bluemix.net/quota/usage
	```
	{: codeblock}
	
	The result includes the information about the daily quota and usage in bytes.
	
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



