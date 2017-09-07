---

copyright:
  years: 2017

lastupdated: "2017-08-25"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Authenticating by using the Bluemix IAM model
{: #auth_iam}

Use the {{site.data.keyword.Bluemix}} IAM model to get an authentication token that you can use to access logs that are stored in the {{site.data.keyword.loganalysisshort}} service. The token has an expiration time. 
{:shortdesc}


## Getting the IAM token by using the Bluemix CLI 
{: #iam_token_cli}

To get the authorization token by using the {{site.data.keyword.Bluemix_notm}} CLI, complete the following steps:

1. Install the {{site.data.keyword.Bluemix_notm}} CLI.

   For more information, see [Installing the {{site.data.keyword.Bluemix_notm}} CLI](/docs/services/CloudLogAnalysis/qa/cli_qa.html#cli_qa).
   
   If the CLI is installed, continue with the next step.
    
2. Log in to a {{site.data.keyword.Bluemix_notm}} region, organization, and space. Run the command:

    ```
    bx login -a Endpoint
    ```
    {: codeblock}
	
	Where *Endpoint* is the URL to log in to {{site.data.keyword.Bluemix_notm}}. This URL is different per region.
	
	<table>
	    <caption>List of endpoints to access {{site.data.keyword.Bluemix_notm}}</caption>
		<tr>
		  <th>Region</th>
		  <th>URL</th>
		</tr>
		<tr>
		  <td>US South</td>
		  <td>api.ng.bluemix.net</td>
		</tr>
		<tr>
		  <td>United Kingdom</td>
		  <td>api.eu-gb.bluemix.net</td>
		</tr>
	</table>

    Follow the instructions. Enter your {{site.data.keyword.Bluemix_notm}} credentials, select an organization and a space.
	
3. Run the `bx iam oauth-tokens` command to get the IAM token.

    ```
	bx iam oauth-tokens
	```
	{: codeblock}
	
	The output returns the IAM token that you must use to authenticate your user ID in that space and organization. You can export the IAM token to a shell variable such as `$iam_token`.

	You can retrieve the user's IAM ID (`"iam_id": "IBMid-xxxxxxx"`) by running the following command:

	```
	echo $iam_token_middle | base64 -d
	```
	{: codeblock}
	
	The IAM ID is available in the middle part of the IAM token, betweeen 2 dots.

**Note:** When you use the token, remove *Bearer* from the value of the token that you pass in an API call.

