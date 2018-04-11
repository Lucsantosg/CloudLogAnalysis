---

copyright:
  years: 2017, 2018

lastupdated: "2018-04-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Getting the logging token
{: #logging_token}

Get a logging token to send logs into the {{site.data.keyword.loganalysisshort}} service. 
{:shortdesc}


## Getting the logging token to send logs to a space by using the {{site.data.keyword.loganalysisshort}} CLI 
{: #logging_token_la_cloud_cli}

To get the logging token that you can use to send logs to the {{site.data.keyword.loganalysisshort}} service, complete the following steps:

1. Install the {{site.data.keyword.Bluemix_notm}} CLI.

   For more information, see [Download and install the {{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/reference/bluemix_cli/download_cli.html#download_install).
   
   If the CLI is installed, continue with the next step.
    
2. Log in to a region, organization, and space in the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
	
3. Run the following command:

    ```
	bx logging token-get
	```
	{: codeblock}

The output returns the logging token.


## Getting the logging token to send logs to a space by using the {{site.data.keyword.Bluemix_notm}} CLI 
{: #logging_token_cloud_cli}

To get the logging token that you can use to send logs to the {{site.data.keyword.loganalysisshort}} service, complete the following steps:

1. Install the {{site.data.keyword.Bluemix_notm}} CLI.

   For more information, see [Download and install the {{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/reference/bluemix_cli/download_cli.html#download_install).
   
   If the CLI is installed, continue with the next step.
    
2. Log in to a region, organization, and space in the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
	
3. Create a service key in the space where the {{site.data.keyword.loganalysisshort}} service is provisioned. Run the following commands:

    List the services to obtain the name of the {{site.data.keyword.loganalysisshort}} instance in the space:
	
    ```
	bx service list
	```
	{: codeblock}
	
	For example:
	
	```
	bx service list
    Invoking 'cf services'...

    Getting services in org lopezdsr_org / space dev as xxx@yyyy...
    OK

    name              service          plan       bound apps   last operation
    Log Analysis-vg   ibmloganalysis   standard                create succeeded
    ```
	{: screen}
	
	Create a key. Use the value of **name** for the servicename, and enter the name of your key.
	
	```
	bx service key-create servicename KeyName 
	```
	{: codeblock}
	
	For example,
	
	```
	bx service key-create "Log Analysis-vg" mykey2
    Invoking 'cf create-service-key Log Analysis-vg mykey2'...

    Creating service key mykey2 for service instance Log Analysis-vg as xxx@yyyy...
    OK
    ```
	{: screen}
	
4. Get the logging token. Run the following command:
	
	```
	bx service key-show name Keyname
	```
	{: codeblock}
	
	For example, 
	
	```
	bx service key-show "Log Analysis-vg" "mykey2" 
    Invoking 'cf service-key Log Analysis-vg mykey2'...

    Getting key mykey2 for service instance Log Analysis-vg as xxx@yyyy...

    {
     "LOG_INGESTION_MTLJ_URL": "https://ingest-eu-fra.logging.bluemix.net:9091",
     "logging_token": "sdtghyrtfde4",
     "space_id": "12345678-avfg-erft-b1f2-2efrtgcb1744"
    }
    ```
	{: screen}
	
	To get the logging token, you can run the following command:
	
	```
	bx service key-show "Log Analysis-vg" "mykey2" | tail -n +4 | jq -r .logging_token
    sdtghyrtfde4
	```
	{: screen}


	
## Getting the logging token to send logs to a space by using the Log Analysis API
{: #logging_token_api}


To get the logging token that you can use to send logs to the {{site.data.keyword.loganalysisshort}} service, complete the following steps:

1. Install the {{site.data.keyword.Bluemix_notm}} CLI.

   For more information, see [Download and install the {{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/reference/bluemix_cli/download_cli.html#download_install).
   
   If the CLI is installed, continue with the next step.
    
2. Log in to a region, organization, and space in the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
	
3. Get the [UAA token](/docs/services/CloudLogAnalysis/security/auth_uaa.html#uaa_cli).

    For example, run the `bx cf oauth-token` command to get the UAA token.

    ```
	bx cf oauth-token
	```
	{: codeblock}
	
	The output returns the UAA token that you must use to authenticate your user ID in that space and organization.

4. Get the GUID for the space.

   For more information, see [How do I get the GUID of a space](/docs/services/CloudLogAnalysis/qa/cli_qa.html#space_guid).  
	
5. Export the following variables: TOKEN and SPACEID.

    * *TOKEN* is the oauth token that you got in the previous step excluding Bearer.
	
	* *SPACEID* is the GUID of the space that you got in the previous step. 
		
	For example,
	
	```
	export TOKEN="eyJhbGciOiJI....cGFzc3dvcmQiLCJjZiIsInVhYSIsIm9wZW5pZCJdfQ.JaoaVudG4jqjeXz6q3JQL_SJJfoIFvY8m-rGlxryWS8"
	export SPACEID="667fb895-abcd-defg-aaaa-cf4587341095"
	```
	{: screen}
	
6. Get the logging token. Run the following command:
 
    ```
	curl -k -X GET  --header "X-Auth-Token: ${TOKEN}"  --header "X-Auth-Project-Id: s-${SPACEID}"  LOGGING_ENDPOINT/token
    ```
    {: codeblock}	
	
	where
	* SPACEID is the GUID of the space where the service is running.
	* TOKEN is the UAA token that you get in a previous step without the bearer prefix.
	* LOGGING_ENDPOINT is the {{site.data.keyword.loganalysisshort}} endpoint for the {{site.data.keyword.Bluemix_notm}} region where the organization and space are available. The LOGGING_ENDPOINT is different per region. To see the URLs for the different endpoints, see [Endpoints](/docs/services/CloudLogAnalysis/manage_logs.html#endpoints).
	
    The command returns the logging token that you must use to send logs to that space.
	
