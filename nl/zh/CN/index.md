---

copyright:
  years: 2017, 2018

lastupdated: "2018-01-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 入门教程
{: #getting-started-with-cla}

使用本教程了解如何开始使用 {{site.data.keyword.Bluemix}} 中的 {{site.data.keyword.loganalysislong}} 服务。
{:shortdesc}

## 目标
{: #objectives}

* 在页面中供应 {{site.data.keyword.loganalysislong}} 服务。
* 设置命令行以管理日志。
* 设置许可权以供用户查看空间中的日志。
* 启动 Kibana（可用于查看日志的开放式源代码工具）。


## 开始之前
{: #prereqs}

必须具有作为 {{site.data.keyword.Bluemix_notm}} 帐户的成员或所有者的用户标识。要获取 {{site.data.keyword.Bluemix_notm}} 用户标识，请转至[注册 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.bluemix.net/registration/){:new_window}

本教程提供在美国南部区域供应和使用 {{site.data.keyword.loganalysisshort}} 服务的指示信息。


## 步骤 1：供应 {{site.data.keyword.loganalysisshort}} 服务
{: #step1}

**注：**将在 Cloud Foundry (CF) 空间中供应 {{site.data.keyword.loganalysisshort}} 服务的实例。每个空间仅需一个服务实例。无法在帐户级别供应 {{site.data.keyword.loganalysisshort}} 服务。 

要在 {{site.data.keyword.Bluemix_notm}} 中供应 {{site.data.keyword.loganalysisshort}} 服务的实例，请完成以下步骤：

1. 登录到 {{site.data.keyword.Bluemix_notm}}：[http://bluemix.net ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://bluemix.net){:new_window}。  

2. 选择要供应 {{site.data.keyword.loganalysisshort}} 服务的区域、组织和空间。  

3. 单击**目录**。这将打开 {{site.data.keyword.Bluemix_notm}} 上可用的服务的列表。

4. 选择 **DevOps** 类别以过滤显示的服务列表。

5. 单击 **Log Analysis** 磁贴。

6. 选择服务套餐。缺省情况下，已设置 **Lite** 套餐。


    有关服务套餐的更多信息，请参阅[服务套餐](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans)。
	
7. 单击**创建**以在您登录到的 {{site.data.keyword.Bluemix_notm}} 空间中供应 {{site.data.keyword.loganalysisshort}} 服务。




## 步骤 2：[可选] 更改 {{site.data.keyword.loganalysisshort}} 服务的服务套餐
{: #step2}

如果需要更多搜索配额和/或长期存储日志，可以通过 {{site.data.keyword.Bluemix_notm}} UI 或通过运行 `bx cf update-service` 命令来更改 {{site.data.keyword.loganalysisshort}} 服务实例套餐，以启用这些功能。 

您可以随时升级或降级服务套餐。

有关更多信息，请参阅 [{{site.data.keyword.loganalysisshort}} 服务套餐](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans)。

**注：**将套餐更改为付费套餐需要付费。

要在 {{site.data.keyword.Bluemix_notm}} UI 中更改服务套餐，请完成以下步骤：

1. 登录到 {{site.data.keyword.Bluemix_notm}}：[http://bluemix.net ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://bluemix.net){:new_window}。  

2. 选择 {{site.data.keyword.loganalysisshort}} 服务可用的区域、组织和空间。  

3. 在 {{site.data.keyword.Bluemix_notm}} *仪表板*中单击 {{site.data.keyword.loganalysisshort}} 服务实例。 
    
4. 在 {{site.data.keyword.loganalysisshort}} 仪表板中选择**套餐**选项卡。

    这将显示有关当前套餐的信息。
	
5. 选择新套餐以升级或降级现有套餐。 

6. 单击**保存**。



## 步骤 3：设置本地环境以使用 {{site.data.keyword.loganalysisshort}} 服务
{: #step3}


{{site.data.keyword.loganalysisshort}} 服务包含可用于管理存储在“日志收集”（长期存储组件）中的日志的命令行界面 (CLI)。 

可以使用 {{site.data.keyword.loganalysisshort}} {{site.data.keyword.Bluemix_notm}} 插件来查看日志的状态、下载日志以及配置日志保留时间策略。 

该 CLI 提供了以下不同类型的帮助：了解 CLI 和受支持命令的一般帮助、了解如何使用命令的命令帮助，以及了解如何使用某个命令的子命令的子命令帮助。


要从 {{site.data.keyword.Bluemix_notm}} 存储库安装 {{site.data.keyword.loganalysisshort}} CLI，请完成以下步骤：

1. 安装 {{site.data.keyword.Bluemix_notm}} CLI。

   有关更多信息，请参阅[安装 {{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/reference/bluemix_cli/download_cli.html#download_install)。

2. 安装 {{site.data.keyword.loganalysisshort}} 插件。运行以下命令：

    ```
    bx plugin install logging-cli -r Bluemix
    ```
    {: codeblock}
 
3. 验证是否已安装 {{site.data.keyword.loganalysisshort}} 插件。
  
    例如，运行以下命令以查看安装的插件列表：
    
    ```
    bx plugin list
    ```
    {: codeblock}
    
    输出如下所示：
   
    ```
    bx plugin list
    Listing installed plug-ins...

    Plugin Name          Version   
    logging-cli          0.1.1   
    ```
    {: screen}




## 步骤 4：设置许可权以供用户查看日志
{: #step4}

要控制允许用户执行的 {{site.data.keyword.loganalysisshort}} 操作，您可以向用户分配角色和策略。 

在 {{site.data.keyword.Bluemix_notm}} 中有两种类型的安全许可权，控制在用户使用 {{site.data.keyword.loganalysisshort}} 服务时可以执行的操作：

* Cloud Foundry (CF) 角色：向用户授予 CF 角色，以定义用户查看空间中的日志的许可权。
* IAM 角色：向用户授予 IAM 策略，以定义用户查看帐户域中的日志的许可权，以及用户管理“日志收集”中所存储日志的许可权。 


完成以下步骤以授予用户查看空间中的日志的许可权：

1. 登录到 {{site.data.keyword.Bluemix_notm}} 控制台。

    打开 Web 浏览器并启动 {{site.data.keyword.Bluemix_notm}} 仪表板：[http://bluemix.net ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://bluemix.net){:new_window}
	
	使用用户标识和密码登录后，{{site.data.keyword.Bluemix_notm}} UI 将打开。

2. 从菜单栏，单击**管理 > 帐户 > 用户**。 

    *用户*窗口显示用户列表，其中包含目前所选帐户的电子邮件地址。
	
3. 如果用户是帐户的成员，请从列表中选择用户名，或者从*操作*菜单中单击**管理用户**。

    如果用户不是帐户的成员，请参阅[邀请用户](/docs/iam/iamuserinv.html#iamuserinv)。

4. 选择 **Cloud Foundry 访问权**，然后选择组织。

    将列出该组织中可用的空间列表。

5. 选择已供应 {{site.data.keyword.loganalysisshort}} 服务的空间。然后，从菜单操作中，选择**编辑空间角色**。

6. 选择*审计员*。 

    您可以选择 1 个或多个空间角色。以下所有角色均允许用户查看日志：*管理员*、*开发者*和*审计员*
	
7. 单击**保存角色**。


有关更多信息，请参阅[授予许可权](/docs/services/CloudLogAnalysis/security/grant_permissions.html#grant_permissions_ui_account)。



## 步骤 5：启动 Kibana
{: #step5}

要查看和分析日志数据，您必须在日志数据可用的云公共区域中访问 Kibana。 


要在美国南部区域中启动 Kibana，请打开 Web 浏览器并输入以下 URL：

```
https://logging.ng.bluemix.net/
```
{: codeblock}


有关如何在其他区域中启动 Kibana 的更多信息，请参阅[通过 Web 浏览器导航至 Kibana](/docs/services/CloudLogAnalysis/kibana/launch.html#launch_Kibana_from_browser)。

**注：**启动 Kibana 时，如果收到指示 *bearer token not valid* 的消息，请检查空间中的许可权。此消息指示您的用户标识不具有查看日志的许可权。
    

## 后续步骤 
{: #next_steps}

生成日志。尝试使用以下任意教程：

* [在 Kibana 中分析 Kubernetes 集群中部署的应用程序的日志](/docs/services/CloudLogAnalysis/tutorials/container_logs.html#container_logs){:new_window} 

    本教程演示了要使以下端到端场景可运作所需的步骤：供应集群、配置集群以将日志发送到 {{site.data.keyword.Bluemix_notm}} 中的 {{site.data.keyword.loganalysisshort}} 服务、部署集群中的应用程序以及使用 Kibana 查看和过滤该集群的容器日志。     
    
* [在 Kibana 中分析 Cloud Foundry 应用程序的日志](/docs/tutorials/application-log-analysis.html#generate-access-and-analyze-application-logs){:new_window}                                                                                                            

    本教程演示了要使以下端到端场景可运作所需的步骤：部署 Python Cloud Foundry 应用程序、生成不同类型的日志以及使用 Kibana 查看、搜索和分析 CF 日志。
   








