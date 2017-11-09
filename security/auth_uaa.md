---

copyright:
  years: 2017

lastupdated: "2017-11-09"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Authenticating by using the UAA method
{: #auth_uaa}

Use the UAA method to get an authentication token that you can use to manage logs that are stored in a space. You can obtain the authentication token by using the {{site.data.keyword.Bluemix_notm}} CLI or by using the `Login` REST API.
{:shortdesc}

To manage logs by using a UAA authentication token, you need the following information:

* A UAA token to access the {{site.data.keyword.loganalysisshort}} service by using the RESTful APIs.
* The GUID of the space.

		
## Getting the UAA token by using the {{site.data.keyword.Bluemix_notm}} CLI
{: #uaa_cli}


To get the authorization token, complete the following steps:

1. Install the {{site.data.keyword.Bluemix_notm}} CLI.

   For more information, see [Download and install the {{site.data.keyword.Bluemix}} CLI](/docs/cli/reference/bluemix_cli/download_cli.html#download_install).
   
   If the CLI is installed, continue with the next step.
    
2. Log in to a region, organization, and space in the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
	
3. Run the `bx cf oauth-token` command to get the {{site.data.keyword.Bluemix_notm}} UAA token.

    ```
	bx cf oauth-token
	```
	{: codeblock}
	
	The output returns the UAA token that you must use to authenticate your user ID in that space and organization.

4. Get the GUID for the space of the organization for which you have obtained an authentication token.

   For more information, see [How do I get the GUID of a space](/docs/services/CloudLogAnalysis/qa/cli_qa.html#space_guid).  
	
5. Export the following variables: TOKEN and SPACE.

    * *TOKEN* is the oauth token that you got in the previous step excluding Bearer.
	
	* *SPACE* is the GUID of the space that you got in the previous step.
		
	For example,
	
	```
	export TOKEN="eyJhbGciOiJI....cGFzc3dvcmQiLCJjZiIsInVhYSIsIm9wZW5pZCJdfQ.JaoaVudG4jqjeXz6q3JQL_SJJfoIFvY8m-rGlxryWS8"
	export SPACE="667fb895-abcd-defg-aaaa-cf4587341095"
	```
	{: screen}
	
6. Run the following command to get the UAA token to work with the {{site.data.keyword.loganalysisshort}} service:
 
    ```
	curl -k -X GET  --header "X-Auth-Token: ${TOKEN}"  --header "X-Auth-Project-Id: ${SPACE}"  LOGGING_ENDPOINT/token
    ```
    {: codeblock}	
	
	where
	* SPACE is the GUID of the space where the service is running.
	* TOKEN is the {{site.data.keyword.Bluemix_notm}} UAA token that you get in a previous step without the bearer prefix.
	* LOGGING_ENDPOINT is the {{site.data.keyword.loganalysisshort}} endpoint for the {{site.data.keyword.Bluemix_notm}} region where the organization and space are available. The LOGGING_ENDPOINT is different per region. To see the URLs for the different endpoints, see [Endpoints](/docs/services/CloudLogAnalysis/manage_logs.html#endpoints).
	
	
	
## Getting the UAA token by using the API
{: #uaa_api}

To get the authorization token, run the following cURL command:

```
curl -XPOST -d 'user=USERNAME&passwd=PASSWORD&space=SPACE_NAME&organization=ORG_NAME' LOGGING_ENDPOINT
```
{: codeblock}

where

* USERNAME is a {{site.data.keyword.Bluemix_notm}} ID for which you want to get the authentication token to work with the {{site.data.keyword.loganalysisshort}} service.
* PASSWORD is the password of the user ID used to log in to {{site.data.keyword.Bluemix_notm}}.
* SPACE_NAME is the name of the space where logs are collected.
* ORG_NAME is the organization name in {{site.data.keyword.Bluemix_notm}} where the space is hosted.
* LOGGING_ENDPOINT is the logging endpoint for the {{site.data.keyword.Bluemix_notm}} region where the organization and space are available. The LOGGING_ENDPOINT is different per region.To see the URLs for the different endpoints, see [Endpoints](/docs/services/CloudLogAnalysis/manage_logs.html#endpoints).

The output is a JSON document that contains the UAA token. Get the value for the token from the field **access-token**. 

For example, a sample JSON document looks as follows:

```
{
    "access_token": "eyJhbGc...",
    "logging_token": "xxxxxxxxxxxx",
    "org_id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "space_id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
}
```
{: screen}

The value of the *logging_token* corresponds to the UAA token that you need to work with the {{site.data.keyword.loganalysisshort}} service.
 
**Note:** 

* If you are not using cURL, you must set the header **Content-Type: application/x-www-form-urlencoded**.
* If you get the error code *BXNMS0122E: User credentials are invalid*, check that you are using a valid {{site.data.keyword.IBM_notm}} ID.
