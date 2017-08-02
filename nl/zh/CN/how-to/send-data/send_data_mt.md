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

# 使用多租户 Logstash 转发器发送数据
{: #send_data_mt}

要将数据发送到 {{site.data.keyword.loganalysisshort}} 服务中，可以配置多租户 Logstash 转发器 (mt-logstash-forwarder)。
{:shortdesc}

要将日志数据发送到“日志收集”中，请完成以下步骤：

## 步骤 1：获取日志记录令牌
{: #get_logging_auth_token}

要将数据发送到 {{site.data.keyword.loganalysisshort}} 服务，您需要：

* {{site.data.keyword.IBM_notm}} 标识：登录到 {{site.data.keyword.Bluemix_notm}} 时需要此标识。
* {{site.data.keyword.Bluemix_notm}} 组织中的空间：这是您计划将日志发送到其中并在其中分析日志的空间。
* 用于发送数据的日志记录令牌。 

请完成以下步骤：

1. 登录到 {{site.data.keyword.Bluemix_notm}} 区域、组织和空间。 

    例如，要登录到美国南部区域，请运行以下命令：
	
    ```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. 运行 `cf logging auth` 命令。 

    ```
    cf logging auth
    ```
    {: codeblock}

    该命令返回以下信息：
    
    * 日志记录令牌。
    * 组织标识：这是您所登录到的 {{site.data.keyword.Bluemix_notm}} 组织的 GUID。 
    * 空间标识：您所登录到的组织内空间的 GUID。 
    
    例如：

    ```
    cf logging auth
    +-----------------+--------------------------------------+
    |      NAME       |                VALUE                 |
    +-----------------+--------------------------------------+
    | Access Token    | $(cf oauth-token|cut -d' ' -f2)      |
    | Logging Token   | oT98_bKsdfTz                         |
    | Organization Id | 98450123-6f1c-9999-96a3-0210fjyuwplt |
    | Space Id        | 93f54jh6-b5f5-46c9-9f0e-kfeutpldnbcf |
    +-----------------+--------------------------------------+
    ```
    {: screen}

有关更多信息，请参阅 [cf logging auth](/docs/services/CloudLogAnalysis/reference/logging_cli.html#auth)。


## 步骤 2：配置 mt-logstash-forwarder
{: #configure_mt_logstash_forwarder}

要在您计划从中将日志发送到 {{site.data.keyword.loganalysisshort}} 服务的环境中配置 mt-logstash-forwarder，请完成以下步骤：

1.	以 root 用户身份登录。 

    ```
    sudo -s
    ```
    {: codeblock}
    
2.	安装网络时间协议 (NTP) 包以同步日志的时间。 

    例如，对于 Ubuntu 系统，请检查 `timedatectl status` 是否显示 *Network time on: yes*。如果是，说明 Ubuntu 系统已经配置为使用 NTP，您可跳过此步骤。
    
    ```
    # timedatectl status
    Local time: Mon 2017-06-12 03:01:22 PDT
    Universal time: Mon 2017-06-12 10:01:22 UTC
    RTC time: Mon 2017-06-12 10:01:22
    Time zone: America/Los_Angeles (PDT, -0700)
    Network time on: yes
    NTP synchronized: yes
    RTC in local TZ: no
    ```
    {: screen}
    
    要在 Ubuntu 系统中安装 NTP，请完成以下步骤：

    1.	运行以下命令来更新包。 

        ```
        apt-get update
        ```
        {: codeblock}
        
    2.	运行以下命令来安装 ntp 包。 

        ```
        apt-get install ntp
        ```
        {: codeblock}
        
    3.	运行以下命令来安装 ntpdate 包。 
    
        ```
        apt-get install ntpdate
        ```
        {: codeblock}
        
    4.	运行以下命令来停止服务。 
        
        ```
        service ntp stop
        ```
        {: codeblock}
        
    5.	运行以下命令来同步系统时钟。 
    
        ```
        ntpdate -u 0.ubuntu.pool.ntp.org
        ```
        {: codeblock}
        
        结果证实时间已调整，例如：
        
        ```
        4 May 19:02:17 ntpdate[5732]: adjust time server 50.116.55.65 offset 0.000685 sec
        ```
        {: screen}
        
    6.	运行以下命令来重新启动 ntpd。 
    
        ```
        service ntp start
        ```
        {: codeblock}
    
        结果证实服务正在启动。

    7.	运行以下命令来支持 ntpd 服务在崩溃或重新引导后自动启动。 
    
        ```
        service ntp enable
        ```
        {: codeblock}
        
        显示的结果是可用于管理 ntpd 服务的命令的列表，例如：
        
        ```
        Usage: /etc/init.d/ntpd {start|stop|status|restart|try-restart|force-reload}
        ```
        {: screen}

3. 为系统软件包管理器中的 {{site.data.keyword.loganalysisshort}} 服务添加存储库。运行以下命令：

    ```
    wget -O - https://downloads.opvis.bluemix.net/client/IBM_Logmet_repo_install.sh | bash
    ```
    {: codeblock}

4. 安装 mt-logstash-forwarder 并将其配置为将您环境中的日志发送到“日志收集”中。 

    1. 运行以下命令来安装 mt-logstash-forwarder：
    
        ```
        apt-get install mt-logstash-forwarder 
        ```
        {: codeblock}
        
    2. 为您的环境创建 mt-logstash-forwarder 配置文件。此文件包含用于配置 mt-logstash-forwarder 以将该转发器指向 {{site.data.keyword.loganalysisshort}} 服务的变量。
    
       编辑 `/etc/mt-logstash-forwarder/mt-lsf-config.sh` 文件。例如，可以使用 vi 编辑器：
               
       ```
       vi /etc/mt-logstash-forwarder/mt-lsf-config.sh
       ```
       {: codeblock}
        
       要将转发器指向 {{site.data.keyword.loganalysisshort}} 服务，请将以下变量添加到 **mt-lsf-config.sh** 文件： 
         
       <table>
          <caption>表 1. 将 VM 中的转发器指向 {{site.data.keyword.loganalysisshort}} 服务所需的变量的列表</caption>
          <tr>
            <th>变量名称</th>
            <th>描述</th>
          </tr>
          <tr>
            <td>LSF_INSTANCE_ID</td>
            <td>VM 的标识，例如 *MyTestVM*。</td>
          </tr>
          <tr>
            <td>LSF_TARGET</td>
            <td>目标 URL。将此值设置为 **https://ingest.logging.ng.bluemix.net:9091**。</td>
          </tr>
          <tr>
            <td>LSF_TENANT_ID</td>
            <td>{{site.data.keyword.loganalysisshort}} 服务准备好在其中收集您发送到 {{site.data.keyword.Bluemix_notm}} 的日志的空间标识。<br>请使用在步骤 1 中获得的值。</td>
          </tr>
          <tr>
            <td>LSF_PASSWORD</td>
            <td>日志记录令牌。<br>请使用在步骤 1 中获得的值。</td>
          </tr>
          <tr>
            <td>LSF_GROUP_ID</td>
            <td>将此值设置为您可以定义用于对相关日志分组的定制标记。</td>
          </tr>
       </table>
        
       例如，查看以下样本文件，以找到英国区域中标识为 *7d576e3b-170b-4fc2-a6c6-b7166fd57912* 的空间：
        
       ```
       # more mt-lsf-config.sh 
       LSF_INSTANCE_ID="myhelloapp"
       LSF_TARGET="ingest.logging.ng.bluemix.net:9091"
       LSF_TENANT_ID="7d576e3b-170b-4fc2-a6c6-b7166fd57912"
       LSF_PASSWORD="oT98_bKsdfTz"
       LSF_GROUP_ID="Group1"
       ```
       {: screen}
        
    3. 启动 mt-logstash-forwarder。 
    
       ```
       service mt-logstash-forwarder start
       ```
       {: codeblock}
        
       支持 mt-logstash-forwarder 在崩溃或重新引导后自动启动。 
        
       ```
       service mt-logstash-forwarder enable
       ```
       {: codeblock}
        
       **提示**：要重新启动 mt-logstash-forwarder 服务，请运行以下命令：
    
       ```
       service mt-logstash-forwarder restart
       ```
       {: codeblock}
        
        
缺省情况下，转发器仅监视 syslog。您的日志可供在 Kibana 中进行分析。
        

## 步骤 3：指定更多日志文件
{: #add_logs}

缺省情况下，转发器仅监视 /var/log/syslog 文件。可以将更多配置文件添加到转发器的目录 `/etc/mt-logstash-forwarder/conf.d/syslog.conf/` 以同时监视这些文件。 

要为您环境中运行的应用程序添加配置文件，请完成以下步骤：

1.	复制 `/etc/mt-logstash-forwarder/conf.d/syslog.conf` 文件。 

    **提示**：不要通过编辑 syslog.conf 文件来添加日志文件。
    
    例如，在 Ubuntu 系统中，运行以下命令：
    
    ```
    cp /etc/mt-logstash-forwarder/conf.d/syslog.conf /etc/mt-logstash-forwarder/conf.d/myapp.conf
    ```
    {: codeblock}
        
2.	使用文本编辑器编辑 *myapp.conf* 文件，并将该文件更新为包含要监视的应用程序日志。请包含每个应用程序日志的日志类型。删除未使用的任何示例。

3.	重新启动 mt-logstash-forwarder。 

     重新启动 mt-logstash-forwarder 服务。运行以下命令：
    
    ```
    service mt-logstash-forwarder restart
    ```
    {: codeblock}

**示例**

要包含来自 hello 应用程序的 stdout 或 stderr，请将 stdout 或 stderr 重定向到日志文件。为该应用程序创建转发器配置文件。然后，重新启动 mt-logstash-forwarder。

1.	复制 `/etc/mt-logstash-forwarder/conf.d/syslog.conf` 文件。 

    ```
    cp /etc/mt-logstash-forwarder/conf.d/syslog.conf /etc/mt-logstash-forwarder/conf.d/myapp.conf
    ```
    {: codeblock}
    
2. 编辑 *myapp.conf* 配置文件。

    要启用 JSON 解析，请将配置文件中的 is_json 设置为 true。
    
    ```
    {
    "files": [
         # other file configurations omitted...
            {
            "paths": [ "/var/log/myhelloapp.log" ],
            "fields": { "type": "helloapplog" },
            "is_json": true
            }
         ]
     }
     ```
     {: screen}
