---

copyright:
  years: 2017, 2018

lastupdated: "2018-01-10"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Getting the UAA token
{: #auth_uaa}

To manage logs by using the {{site.data.keyword.loganalysisshort}} API, you must use an authentication token. Use the {{site.data.keyword.loganalysisshort}} CLI to get the UAA token. The token has an expiration time. 
{:shortdesc}

		
## Getting the UAA token by using the Log Analysis CLI (CF plugin)
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
	

**Note:** When you use the token, remove *Bearer* from the value of the token that you pass in an API call.