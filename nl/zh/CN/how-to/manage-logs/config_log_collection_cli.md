---

copyright:
  years: 2017
lastupdated: "2017-07-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 配置日志收集 CLI
{: #config_log_collection_cli}

{{site.data.keyword.loganalysisshort}} 服务包含可用于在云中管理日志的命令行界面 (CLI)。该 CLI 是一个 Cloud Foundry (CF) 插件。可以使用命令来查看日志的状态，下载日志以及配置日志保留时间策略。该 CLI 提供了不同类型的帮助：用于了解 CLI 和受支持命令的一般帮助，用于了解如何使用命令的命令帮助，或用于了解如何使用某个命令的子命令的子命令帮助。
{:shortdesc}


## 安装日志收集 CLI
{: #install_cli}

要安装“日志收集”CLI，请完成以下步骤：

1. 检查 CF CLI 在系统中是否可用。 

    有关更多信息，请参阅[先决条件](/docs/services/CloudLogAnalysis/how-to/manage-logs/config_log_collection_cli.html#pre_req)。


2. 安装“日志收集”CF 插件：

    * 对于 Linux，请参阅[在 Linux 上安装日志收集 CLI](/docs/services/CloudLogAnalysis/how-to/manage-logs/config_log_collection_cli.html#install_cli_linux)。
    * 对于 Windows，请参阅[在 Windows 上安装日志收集 CLI](/docs/services/CloudLogAnalysis/how-to/manage-logs/config_log_collection_cli.html#install_cli_windows)。
    * 对于 Mac OS X，请参阅[在 Mac OS X 上安装日志收集 CLI](/docs/services/CloudLogAnalysis/how-to/manage-logs/config_log_collection_cli.html#install_cli_mac)。
 

## 先决条件
{: #pre_req}

“日志收集”CLI 是一个 CF 插件。开始安装之前，请考虑以下场景：

* 您是首次安装 CF CLI：

     安装 CF 插件。有关更多信息，请参阅[安装 CF CLI ![外部链接图标](../../../../icons/launch-glyph.svg "外部链接图标")](http://docs.cloudfoundry.org/cf-cli/install-go-cli.html "外部链接图标"){: new_window}。 

* 您已安装 {{site.data.keyword.Bluemix_notm}} CLI 包：

    CF CLI 已捆绑在 {{site.data.keyword.Bluemix_notm}} CLI 包中。

* 您将需要 {{site.data.keyword.Bluemix_notm}} CLI 来管理其他云资源：  

    安装 {{site.data.keyword.Bluemix_notm}} CLI 包；请参阅[安装 {{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/reference/bluemix_cli/index.html#install_bluemix_cli)。

然后，验证该 CF 插件是否可用。通过系统中的会话，运行以下命令：
    
```
cf -v
```
{: codeblock}
    
输出如下所示：
    
```
    cf version 6.25.0+787326d.2017-02-28
    ```
{: screen}

**注：**不能混合使用 {{site.data.keyword.Bluemix_notm}} CLI 命令（即 `bx` 命令）和 CF CLI 命令（即 `cf` 命令）。



	
## 在 Linux 上安装日志收集 CLI
{: #install_cli_linux}

要在 Linux 上安装“日志收集”CF 插件，请完成以下步骤：

1. 安装“日志收集”CLI 插件。

    1. 从 [Bluemix CLI 页面](https://clis.ng.bluemix.net/ui/repository.html#cf-plugins)下载 {{site.data.keyword.loganalysisshort}} 服务 CLI 插件 (IBM-Logging) 的最新发行版。 
	
		选择平台值：**linux64**。单击**保存文件**。 
    
    2. 解压缩该插件。
    
        例如，要在 Ubuntu 中解压缩 `logging-cli-linux64.gz` 插件，请运行以下命令：
        
        ```
        gunzip logging-cli-linux64.gz
        ```
        {: codeblock}

    3. 使该文件成为可执行文件。
    
        例如，要使 `logging-cli-linux64` 文件成为可执行文件，请运行以下命令：
        
        ```
        chmod a+x logging-cli-linux64
        ```
        {: codeblock}

    4. 安装日志记录 CF 插件。
    
        例如，要使 `logging-cli-linux64` 文件成为可执行文件，请运行以下命令：
        
        ```
        cf install-plugin -f logging-cli-linux64
        ```
        {: codeblock}

2. 设置环境变量 **LANG**。

    如果 CF 不支持系统语言环境，请将 *LANG* 设置为缺省值：*en_US.UTF-8*。有关 CF 支持的语言环境的信息，请参阅 [cf CLI 入门 ![外部链接图标](../../../../icons/launch-glyph.svg "外部链接图标")](https://docs.cloudfoundry.org/cf-cli/getting-started.html "外部链接图标"){: new_window}
	
	例如，在 Ubuntu 系统中，编辑 *~/.bashrc* 文件并输入以下行：
    
    ```
    # add entry for logging CLI
    export LANG = en_US.UTF-8
    ```
    {: codeblock}
    
    打开新的终端窗口，并运行以下命令以验证 LANG 和 LOGGING_ENDPOINT 变量是否已设置：
    
    ```
    $echo LANG
    en_US.UTF-8
    ```
    {: screen}   
    
3. 验证日志记录 CLI 插件的安装情况。
  
    例如，检查该插件的版本。运行以下命令：
    
    ```
    cf logging --version
    ```
    {: codeblock}
    
    输出如下所示：
   
    ```
    cf logging version 0.3.5
    ```
    {: screen}


## 在 Windows 上安装日志收集 CLI
{: #install_cli_windows}

要在 Windows 上安装“日志收集”CF 插件，请完成以下步骤：

1. 从 [Bluemix CLI 页面](https://clis.ng.bluemix.net/ui/repository.html#cf-plugins)下载 {{site.data.keyword.loganalysisshort}} 服务 CLI 插件 (IBM-Logging) 的最新发行版。 
	
	1. 选择平台值：**win64**。 
	2. 单击**保存文件**。  
    
2. 运行 **cf install-plugin** 命令以在 Windows 上安装“日志收集”插件。 

    ```
	cf install-plugin PluginName
	```
	{: codeblock}
    
    其中，*PluginName* 是已下载文件的名称。
	
    例如，要安装 *logging-cli-win64_v1.0.1.exe* 插件，请在终端窗口中运行以下命令：
	```
	cf install-plugin logging-cli-win64_v1.0.1.exe
	```
	{: codeblock}
    
    该插件安装后，将收到以下消息：`IBM-Logging 1.0.1 插件已成功安装。`

3. 验证日志记录 CLI 插件的安装情况。

    例如，检查该插件的版本。运行以下命令：

    ```
    cf logging --version
    ```
    {: codeblock}

    输出如下所示：

    ```
    cf logging version 1.0.1
    ```
    {: screen}
	
    ## 在 Mac OS X 上安装“日志收集”CLI
{: #install_cli_mac}

要在 Mac OS X 上安装“日志收集”CF 插件，请完成以下步骤：

1. 从 [Bluemix CLI 页面](https://clis.ng.bluemix.net/ui/repository.html#cf-plugins)下载 {{site.data.keyword.loganalysisshort}} 服务 CLI 插件 (IBM-Logging) 的最新发行版。 	
	1. 选择平台值：**osx**。
	2. 单击**保存文件**。

2. 运行 **cf install-plugin** 命令以在 Mac OS X 上安装“日志收集”插件。

    ```
	cf install-plugin PluginName
	```
	{: codeblock}
    
    其中，*PluginName* 是已下载文件的名称。
	
    例如，要安装 *logging-cli-darwin_v1.0.1* 插件，请在终端中运行以下命令：

	```
	cf install-plugin logging-cli-darwin_v1.0.1
	```
	{: codeblock}
    
    该插件安装后，将收到以下消息：`IBM-Logging 1.0.1 插件已成功安装。`

3. 验证日志记录 CLI 插件的安装情况。

    例如，检查该插件的版本。运行以下命令：

    ```
    cf logging --version
    ```
    {: codeblock}

    输出如下所示：

    ```
    cf logging version 1.0.1
    ```
    {: screen}
	
	
## 卸载“日志收集”CLI
{: #uninstall_cli}

要卸载日志记录 CLI，请删除该插件。
{:shortdesc}

要卸载 {{site.data.keyword.loganalysisshort}} 服务 CLI，请完成以下步骤：

1. 验证安装的日志记录 CLI 插件的版本。

    例如，检查该插件的版本。运行以下命令：

    ```
    cf plugins
    ```
    {: codeblock}

    输出如下所示：

    ```
    Listing Installed Plugins...
    OK

    Plugin Name   Version   Command Name   Command Help
    IBM-Logging   1.0.1     logging        IBM Logging plug-in
    ```
    {: screen}

2. 如果日志记录 CLI 插件已安装，请运行 `cf uninstall-plugin` 来卸载该插件。

    运行以下命令：

    ```
    cf uninstall-plugin IBM-Logging
    ```
    {: codeblock}


## 获取一般帮助
{: #general_cli_help}

要获取有关 CLI 以及受支持命令的常规信息，请完成以下步骤：

1. 登录到 {{site.data.keyword.Bluemix_notm}} 区域、组织和空间。例如，要登录到美国南部区域，请运行以下命令：
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. 列出有关受支持命令和 CLI 的信息。运行以下命令：

    ```
    cf logging help 
    ```
    {: codeblock}
    
    

## 获取有关命令的帮助
{: #command_cli_help}

要获取有关如何使用命令的帮助，请完成以下步骤：

1. 登录到 {{site.data.keyword.Bluemix_notm}} 区域、组织和空间。 

    例如，要登录到美国南部区域，请运行以下命令：
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. 获取受支持命令的列表，并确定您需要的命令。运行以下命令：

    ```
    cf logging help 
    ```
    {: codeblock}

3. 获取有关命令的帮助。运行以下命令：

    ```
    cf logging help *Command*
    ```
    {: codeblock}
    
    其中，*Command* 是 CLI 命令的名称，例如 *status*。



## 获取有关子命令的帮助
{: #subcommand_cli_help}

一个命令可能具有子命令。要获取有关子命令的帮助，请完成以下步骤：

1. 登录到 {{site.data.keyword.Bluemix_notm}} 区域、组织和空间。 

    例如，要登录到美国南部区域，请运行以下命令：
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. 获取受支持命令的列表，并确定您需要的命令。运行以下命令：

    ```
    cf logging help 
    ```
    {: codeblock}

3. 获取有关命令的帮助并确定受支持的子命令。运行以下命令：

    ```
    cf logging help *Command*
    ```
    {: codeblock}
    
    其中，*Command* 是 CLI 命令的名称，例如 *session*。

4. 获取有关命令的帮助并确定受支持的子命令。运行以下命令：

    ```
    cf logging *Command* help *Subcommand*
    ```
    {: codeblock}
    
    其中 
    
    * *Command* 是 CLI 命令的名称，例如 *status*。
    * *Subcommand* 是受支持子命令的名称，例如，对于 *session* 命令，有效的子命令是 *list*。




