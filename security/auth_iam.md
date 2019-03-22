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


# Getting the IAM token
{: #auth_iam1}

To manage the logs that are available in the account domain by using the {{site.data.keyword.loganalysisshort}} API, you must use an authentication token. Use the {{site.data.keyword.cloud_notm}} CLI to get the IAM token. The token has an expiration time. 
{:shortdesc}


## Getting the IAM token
{: #iam_token_cli}

To get the authorization token by using the {{site.data.keyword.cloud_notm}} CLI, complete the following steps from a terminal:

1. Install the {{site.data.keyword.cloud_notm}} CLI.

   For more information, see [Download and install the {{site.data.keyword.Bluemix}} CLI](/docs/cli?topic=cloud-cli-ibmcloud-cli#overview).
   
   If the CLI is installed, continue with the next step.
    
2. Log in to a region in the {{site.data.keyword.cloud_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.cloud_notm}}](/docs/services/CloudLogAnalysis/qa?topic=cloudloganalysis-cli_qa#login).
	
3. Run the `ibmcloud iam oauth-tokens` command to get the IAM token.

    ```
	ibmcloud iam oauth-tokens
	```
	{: codeblock}
	
	The output returns the IAM token that you must use to authenticate your user ID in that space and organization. You can export the IAM token to a shell variable such as `$iam_token`.



**Note:** When you use the token, remove *Bearer* from the value of the token that you pass in an API call.

