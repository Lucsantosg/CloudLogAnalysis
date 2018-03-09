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


# 授予许可权
{: #grant_permissions}

在 {{site.data.keyword.Bluemix}} 中，您可以将一个或多个角色分配给用户。这些角色可定义要启用什么任务以便该用户能够使用 {{site.data.keyword.loganalysisshort}} 服务。
{:shortdesc}



## 通过 {{site.data.keyword.Bluemix_notm}} UI 向用户分配 IAM 政策
{: #grant_permissions_ui_account}

要授予用户查看和管理帐户日志的许可权，您必须针对该用户添加一项策略，该策略描述此用户可以在帐户中使用 {{site.data.keyword.loganalysisshort}} 服务执行的操作。只有帐户所有者可以向用户分配个别策略。

在 {{site.data.keyword.Bluemix_notm}} 中，完成以下步骤，以授予用户使用 {{site.data.keyword.loganalysisshort}} 服务的许可权：

1. 登录到 {{site.data.keyword.Bluemix_notm}} 控制台。

    打开 Web 浏览器并启动 {{site.data.keyword.Bluemix_notm}} 仪表板：[http://bluemix.net ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](http://bluemix.net){:new_window}
	
	使用用户标识和密码登录后，{{site.data.keyword.Bluemix_notm}} UI 将打开。

2. 从菜单栏，单击**管理 > 帐户 > 用户**。 

    *用户*窗口显示用户列表，其中包含目前所选帐户的电子邮件地址。
	
3. 如果用户是帐户的成员，请从列表中选择用户名，或者从*操作*菜单中单击**管理用户**。

    如果用户不是帐户的成员，请参阅[邀请用户](/docs/iam/iamuserinv.html#iamuserinv)。

4. 在**访问策略**部分中，单击**分配服务策略**，然后选择**分配对资源的访问权**。

    这将打开*向用户分配资源访问权** 窗口。

5. 输入策略的信息。下表列出定义策略所需的字段列表： 

    <table>
	  <caption>用于配置 IAM 策略的字段列表。</caption>
	  <tr>
	    <th>字段</th>
		<th>值</th>
	  </tr>
	  <tr>
	    <td>服务</td>
		<td>*IBM Cloud Log Analysis*</td>
	  </tr>	  
	  <tr>
	    <td>区域</td>
		<td>您可以指定要授予用户使用日志的访问权的区域。分别选择一个或多个区域，或者选择**所有当前区域**以授予所有区域的访问权。</td>
	  </tr>
	  <tr>
	    <td>服务实例</td>
		<td>选择*所有服务实例*。</td>
	  </tr>
	  <tr>
	    <td>角色</td>
		<td>选择一个或多个 IAM 角色。<br>有效角色为：*管理员*、*操作员*、*编辑者*和*查看者*。<br>有关每种角色所允许的操作的更多信息，请参阅 [IAM 角色](/docs/services/CloudLogAnalysis/security_ov.html#iam_roles)。</td>
	  </tr>
     </table>
	
6. 单击**分配策略**。
	
您所配置的策略适用于所选区域。 

## 使用命令行向用户分配 IAM 策略
{: #grant_permissions_commandline}

要授予用户许可权以查看和管理帐户日志，你必须授予用户一个 IAM 角色。有关 IAM 角色以及角色启用什么任务才能使用 {{site.data.keyword.loganalysisshort}} 服务的更多信息，请参阅 [IAM 角色](/docs/services/CloudLogAnalysis/security_ov.html#iam_roles)。

此操作只能由帐户所有者执行。

完成以下步骤，使用命令行，授予用户查看帐户日志的访问权：

1. 获取帐户标识。 

    运行以下命令以获取帐户标识：

    ```
	bx iam accounts
	```
    {: codeblock}	

	这将显示带有 GUID 的帐户列表。
	
	导出您计划向用户授予 shell 变量（如“$acct_id”）许可权的帐户的帐户标识，例如：
	
	```
	export acct_id="1234567891234567812341234123412"
	```
	{: screen}
    
    2. 获取您要授予许可权的用户的 {{site.data.keyword.Bluemix_notm}} 标识。
    1. 显示与帐户关联的用户。运行以下命令：
	
	    ```
		bx iam account-users
		```
		{: codeblock}
    
    2. 获取用户的 GUID。**注：**此步骤必须由计划授予许可权的用户完成。
	    例如，请求用户运行以下命令，以获取此用户标识：
		获取 IAM 令牌。有关更多信息，请参阅[使用 {{site.data.keyword.Bluemix_notm}} CLI 获取 IAM 令牌](/docs/services/CloudLogAnalysis/security/auth_iam.html#iam_token_cli)。
        从 IAM 令牌中获取 IAM 令牌中前两个点之间的数据。将数据导出到 shell 变量“如 $user_data”。
		
		```
	    export user_data="xxxxxxxxxxxxxxxxxxxxxxxxxxx"
	    ```
	        {: screen}
	
    例如，运行以下命令，以获取用户标识。此命令在此样本中使用 jq，将信息解码到 JSON 格式的文本中：
		
		```
		echo $user_data | base64 -d | jq
		```
		{: codeblock}
    
    运行此命令的输出如下：
		
		```
		$ echo $user_data | base64 -d | jq
        {
        "iam_id": "IBMid-xxxxxxxxxx",
        "id": "IBMid-xxxxxxxxxx",
        "realmid": "IBMid",
        ......
		}
        ```
	    {: screen}
		
		向帐户所有者发送用户标识。
		
	3. 将用户标识导出到 shell 变量，如 `$user_ibm_id`。
	
		```
		export user_ibm_id="IBMid-xxxxxxxxxx"
		```
		{: codeblock}

3. 如果用户还不是成员，请邀请用户加入帐户。有关更多信息，请参阅[邀请用户](/docs/iam/iamuserinv.html#iamuserinv)。

    例如，运行以下命令以邀请用户 xxx@yyy.com 加入帐户 zzz@ggg.com：
	
	```
	bx iam account-user-invite xxx@yyy.com zzz@ggg.com OrgAuditor dev SpaceDeveloper
	```
	{: codeblock}
		
4. 创建策略文件名称。 

    例如，使用以下模板授予美国南部区域的查看许可权：
	
	```
	{
		"roles" : [
			{
				"id": "crn:v1:bluemix:public:iam::::role:Editor" 
			}
		],
		"resources": [
			{
				"serviceName": "ibmcloud-log-analysis",
				"region": "us-south"
			}
		]
	}
	```
	{: codeblock}
	
	对策略文件进行命名：`policy.json`
	
5. 获取用户标识的 IAM 令牌。

    有关更多信息，请参阅[使用 {{site.data.keyword.Bluemix_notm}} CLI 获取 IAM 令牌](/docs/services/CloudLogAnalysis/security/auth_iam.html#iam_token_cli)。

    将 IAM 令牌导出到 shell 变量（如 `$iam_token`），例如：
	
	```
	export iam_token="xxxxxxxxxxxxxxxxxxxxx"
	```
	{: screen}
	
6. 授予用户使用 {{site.data.keyword.loganalysisshort}} 服务的许可权。 

   运行以下 cURL 命令以授予美国南部区域的许可权：
	
    ```
	curl -X POST --header "Authorization: $iam_token" --header "Content-Type: application/json" https://iampap.ng.bluemix.net/acms/v1/scopes/a%2F$acct_id/users/$user_ibm_id/policies -d @policy.json
	```
	{: codeblock}
    
    运行以下 cURL 命令以授予英国区域的许可权：
	
    ```
	curl -X POST --header "Authorization: $iam_token" --header "Content-Type: application/json" https://iampap.eu-gb.bluemix.net/acms/v1/scopes/a%2F$acct_id/users/$user_ibm_id/policies -d @policy.json
	```
	{: codeblock}
    
    在您向用户授予许可权后，用户可以登录到 {{site.data.keyword.Bluemix_notm}} 并查看帐户级别日志。

## 使用 {{site.data.keyword.Bluemix_notm}} UI 授予用户查看空间日志的许可权
{: #grant_permissions_ui_space}

要授予用户查看空间中日志的许可权，您必须为用户分配 Cloud Foundry 角色，该角色描述此用户可在该空间中使用 {{site.data.keyword.loganalysisshort}} 服务执行的操作。
完成以下步骤以授予用户使用 {{site.data.keyword.loganalysisshort}} 服务的许可权：

1. 登录到 {{site.data.keyword.Bluemix_notm}} 控制台。

    打开 Web 浏览器并启动 {{site.data.keyword.Bluemix_notm}} 仪表板：[http://bluemix.net ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](http://bluemix.net){:new_window}
	
	使用用户标识和密码登录后，{{site.data.keyword.Bluemix_notm}} UI 将打开。

2. 从菜单栏中，单击**管理 > 帐户 > 用户**。

    *用户*窗口显示用户列表，其中包含目前所选帐户的电子邮件地址。
	
3. 如果用户是帐户的成员，请从列表中选择用户名，或者从*操作*菜单中单击**管理用户**。

    如果用户不是帐户的成员，请参阅[邀请用户](/docs/iam/iamuserinv.html#iamuserinv)。

4. 选择 **Cloud Foundry 访问权**，然后选择组织。

    将列出该组织中可用的空间列表。

5. 选择一个空间。然后，从菜单操作中，选择**编辑空间角色**。

6. 选择 1 个或多个空间角色。有效角色为：*管理员*、*开发者*和*审计员*
	
7. 单击**保存角色**。




