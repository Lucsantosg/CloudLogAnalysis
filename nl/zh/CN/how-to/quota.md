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


# 计算搜索配额和每日使用情况
{: #quota}

要获取 {{site.data.keyword.loganalysisshort}} 服务的日志域配额和当前每日使用情况，您可以运行 cURL 命令。
{:shortdesc}


## 计算帐户的搜索配额和每日使用情况
{: #account}

请完成以下步骤：

1. 登录到 {{site.data.keyword.Bluemix_notm}}。 

    有关更多信息，请参阅[如何登录到 {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login)。

2. 获取帐户的标识。运行以下命令：

    ```
	bx iam accounts
	```
    {: codeblock}	

	这将显示带有 GUID 的帐户列表。
	
	将帐户标识导出到 shell 变量。例如：
```
	export AccountID="1234567891234567812341234123412"
	```
	{: screen}
    
    3. 获取 UAA 令牌。

    有关更多信息，请参阅[获取 UAA 令牌](/docs/services/CloudLogAnalysis/security/auth_uaa.html#auth_uaa)。
    将 UAA 令牌导出到 shell 变量。请勿包含“Bearer”。例如：
```
	export TOKEN="xxxxxxxxxxxxxxxxxxxxx"
	```
	{: screen}
    
    4. 获取域的配额和当前使用情况。运行以下命令：
```
    curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: a-${AccountID}" -XGET ENDPOINT/quota/usage
	```
	{: codeblock}
    
    其中，*ENDPOINT* 对于每个区域来说是不同的。有关每个区域的端点列表，请参阅[日志记录端点](/docs/services/CloudLogAnalysis/manage_logs.html#endpoints)。 	
	例如，运行 cURL 命令以获取美国南部区域中帐户的配额：
	
	```
    curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: a-${AccountID}" -XGET https://logging.ng.bluemix.net/quota/usage
	```
	{: codeblock}
    
    结果包含每日配额和使用情况的相关信息。
	
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
	
    ## 计算空间的搜索配额和每日使用情况
{: #space}

完成以下步骤：

1. 登录到 {{site.data.keyword.Bluemix_notm}}。

    有关更多信息，请参阅[如何登录到 {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login)。

2. 获取空间的标识。

    有关更多信息，请参阅[如何获取空间的 GUID](/docs/services/CloudLogAnalysis/qa/cli_qa.html#space_guid)。
	
将空间标识导出到 shell 变量。例如：
```
	export SpaceID="xxxxxxxxxxxxxxxxxxxxx"
	```
	{: screen}
    
    3. 获取 UAA 令牌。

    有关更多信息，请参阅[获取 UAA 令牌](/docs/services/CloudLogAnalysis/security/auth_uaa.html#auth_uaa)。

    将 UAA 令牌导出到 shell 变量。请勿包含“Bearer”。例如：
```
	export TOKEN="xxxxxxxxxxxxxxxxxxxxx"
	```
	{: screen}
    
    4. 获取域的配额和当前使用情况。运行以下命令：
```
    curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: a-${SpaceID}" -XGET ENDPOINT/quota/usage
	```
	{: codeblock}
    
    其中，*ENDPOINT* 对于每个区域来说是不同的。有关每个区域的端点列表，请参阅[日志记录端点](/docs/services/CloudLogAnalysis/manage_logs.html#endpoints)。

    例如，运行以下 cURL 命令以获取美国南部区域中空间域的配额和使用情况：
	
    ```
    curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: a-${SpaceID}" -XGET https://logging.ng.bluemix.net/quota/usage
	```
	{: codeblock}
    
    结果包含每日配额和使用情况的相关信息。
	
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



