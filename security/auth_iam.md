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


# Authenticating by using the IAM method
{: #auth_iam}

Use the IAM method to get an authentication token that you can use to manage logs that are stored in the {{site.data.keyword.loganalysisshort}} service. The token has an expiration time. 
{:shortdesc}


## Getting the IAM token by using the {{site.data.keyword.Bluemix_notm}} CLI 
{: #iam_token_cli}

To get the authorization token by using the {{site.data.keyword.Bluemix_notm}} CLI, complete the following steps:

1. Install the {{site.data.keyword.Bluemix_notm}} CLI.

   For more information, see [Download and install the {{site.data.keyword.Bluemix}} CLI](/docs/cli/reference/bluemix_cli/download_cli.html#download_install).
   
   If the CLI is installed, continue with the next step.
    
2. Log in to a region, organization, and space in the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
	
3. Run the `bx iam oauth-tokens` command to get the IAM token.

    ```
	bx iam oauth-tokens
	```
	{: codeblock}
	
	The output returns the IAM token that you must use to authenticate your user ID in that space and organization. You can export the IAM token to a shell variable such as `$iam_token`.



**Note:** When you use the token, remove *Bearer* from the value of the token that you pass in an API call.

