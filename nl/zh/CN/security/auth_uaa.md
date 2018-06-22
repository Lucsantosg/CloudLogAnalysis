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


# 获取 UAA 令牌
{: #auth_uaa}

要使用 {{site.data.keyword.loganalysisshort}} API 来管理日志，您必须使用认证令牌。使用 {{site.data.keyword.loganalysisshort}} CLI 以获取 UAA 令牌。令牌具有到期时间。
{:shortdesc}

		
## 使用 Log Analysis CLI 获取 UAA 令牌（CF 插件）
{: #uaa_cli}


要获取授权令牌，请完成以下步骤：

1. 安装 {{site.data.keyword.Bluemix_notm}} CLI。

   有关更多信息，请参阅[下载并安装 {{site.data.keyword.Bluemix}} CLI](/docs/cli/reference/bluemix_cli/download_cli.html#download_install)。
   
   如果 CLI 已安装，请继续执行下一步。
    
2. 登录到 {{site.data.keyword.Bluemix_notm}} 中的区域、组织和空间。 

    有关更多信息，请参阅[如何登录到 {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login)。
	
3. 运行 `bx cf oauth-token` 命令以获取 {{site.data.keyword.Bluemix_notm}} UAA 令牌。

    ```
	bx cf oauth-token
	```
	{: codeblock}
	
	输出返回您在该空间和组织中认证用户标识时必须使用的 UAA 令牌。
	


	

**注**：使用令牌时，请从您在 API 调用中传递的令牌值中除去 *Bearer*。

