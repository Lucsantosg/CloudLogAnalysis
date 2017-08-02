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

# Sending Data by using the Multi-Tenant Logstash Forwarder
{: #send_data_mt}

To send log data into the {{site.data.keyword.loganalysisshort}} service, you can configure a Multi-Tenant Logstash Forwarder (mt-logstash-forwarder). 
{: shortdesc}

To send log data into Log Collection, complete the following steps:

## Step 1: Get the logging token
{: #get_logging_auth_token}

To send data to the {{site.data.keyword.loganalysisshort}} service, you need:

* An {{site.data.keyword.IBM_notm}}ID: This ID is required to log in to {{site.data.keyword.Bluemix_notm}}.
* A space in a {{site.data.keyword.Bluemix_notm}} organization: This space is where you plan to send and analyze logs.
* A logging token to send data. 

Complete the following steps:

1. Log in to a {{site.data.keyword.Bluemix_notm}} region, organization, and space. 

    For example, to log in to the US South region, run the following command:
	
    ```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Run the `cf logging auth` command. 

    ```
    cf logging auth
    ```
    {: codeblock}

    The command returns the following information:
    
    * The logging token.
    * The organization ID: This is the GUID of the {{site.data.keyword.Bluemix_notm}} organization where you are logged in. 
    * The space ID: GUID of the space within the organization where you are logged in. 
    
    For example,

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

For more information, see [cf logging auth](/docs/services/CloudLogAnalysis/reference/logging_cli.html#auth).


## Step 2: Configure the mt-logstash-forwarder
{: #configure_mt_logstash_forwarder}

Complete the following steps to configure mt-logstash-forwarder in the environment from where you plan to send logs into the {{site.data.keyword.loganalysisshort}} service:

1.	Log in as the root user. 

    ```
    sudo -s
    ```
    {: codeblock}
    
2.	Install the Network Time Protocol (NTP) package to synchronize the time of the logs. 

    For example, for an Ubunutu system, chek if `timedatectl status` shows *Network time on: yes*. If it does, your Ubuntu system is already configured to use ntp and you can skip this step.
    
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
    
    Complete the following steps to install ntp in an Ubuntu system:

    1.	Run the following command to update the packages. 

        ```
        apt-get update
        ```
        {: codeblock}
        
    2.	Run the following command to install the ntp package. 

        ```
        apt-get install ntp
        ```
        {: codeblock}
        
    3.	Run the following command to install the ntpdate package. 
    
        ```
        apt-get install ntpdate
        ```
        {: codeblock}
        
    4.	Run the following command to stop the service 
        
        ```
        service ntp stop
        ```
        {: codeblock}
        
    5.	Run the following command to synchronize the system clock. 
    
        ```
        ntpdate -u 0.ubuntu.pool.ntp.org
        ```
        {: codeblock}
        
        The result confirms that the time is adjusted, for example:
        
        ```
        4 May 19:02:17 ntpdate[5732]: adjust time server 50.116.55.65 offset 0.000685 sec
        ```
        {: screen}
        
    6.	Run the following command to start ntpd again. 
    
        ```
        service ntp start
        ```
        {: codeblock}
    
        The result confirms that the service is starting.

    7.	Run the following command to enable the ntpd service to start automatically after a crash or reboot. 
    
        ```
        service ntp enable
        ```
        {: codeblock}
        
        The result that is displayed is a list of commands that can be used to manage the ntpd service, for example:
        
        ```
        Usage: /etc/init.d/ntpd {start|stop|status|restart|try-restart|force-reload}
        ```
        {: screen}

3. Add the repository for the {{site.data.keyword.loganalysisshort}} service in the system's package manager. Run the following command:

    ```
    wget -O - https://downloads.opvis.bluemix.net/client/IBM_Logmet_repo_install.sh | bash
    ```
    {: codeblock}

4. Install and configure mt-logstash-forwarder to send logs from your environment into Log Collection. 

    1. Run the following command to install mt-logstash-forwarder:
    
        ```
        apt-get install mt-logstash-forwarder 
        ```
        {: codeblock}
        
    2. Create the mt-logstash-forwarder config file for your environment. This file includes variables that are used to configure mt logstash forwarder to point the forwarder to the {{site.data.keyword.loganalysisshort}} service.
    
       Edit the file `/etc/mt-logstash-forwarder/mt-lsf-config.sh`. For example, you can use the vi editor:
               
       ```
       vi /etc/mt-logstash-forwarder/mt-lsf-config.sh
       ```
       {: codeblock}
        
       To point the forwarder to the {{site.data.keyword.loganalysisshort}} service, add the following variables to the **mt-lsf-config.sh** file: 
         
       <table>
          <caption>Table 1. List of variables required to point the forwarder in a VM to the {{site.data.keyword.loganalysisshort}} service </caption>
          <tr>
            <th>Variable Name</th>
            <th>Description</th>
          </tr>
          <tr>
            <td>LSF_INSTANCE_ID</td>
            <td>ID for your VM, for example. *MyTestVM*. </td>
          </tr>
          <tr>
            <td>LSF_TARGET</td>
            <td>Target URL. To get the lits of ingestion URLs, see [Ingestion URLs](/docs/services/CloudLogAnalysis/log_analysis_ov.html#log_ingestion_urls). For example, set the value to **https://ingest.logging.ng.bluemix.net:9091** to send logs in the US South region. </td>
          </tr>
          <tr>
            <td>LSF_TENANT_ID</td>
            <td>Space ID where the {{site.data.keyword.loganalysisshort}} service is ready to collect the logs that you send into  {{site.data.keyword.Bluemix_notm}}. <br>Use the value that you get in step 1.</td>
          </tr>
          <tr>
            <td>LSF_PASSWORD</td>
            <td>Logging token. <br>Use the value that you get in step 1.</td>
          </tr>
          <tr>
            <td>LSF_GROUP_ID</td>
            <td>Set this value to a custom tag that you can define to group related logs.</td>
          </tr>
       </table>
        
       For example, look at the following sample file for an space that has ID *7d576e3b-170b-4fc2-a6c6-b7166fd57912* in the United Kingdom region:
        
       ```
       # more mt-lsf-config.sh 
       LSF_INSTANCE_ID="myhelloapp"
       LSF_TARGET="ingest.logging.ng.bluemix.net:9091"
       LSF_TENANT_ID="7d576e3b-170b-4fc2-a6c6-b7166fd57912"
       LSF_PASSWORD="oT98_bKsdfTz"
       LSF_GROUP_ID="Group1"
       ```
       {: screen}
        
    3. Start the mt-logstash-forwarder. 
    
       ```
       service mt-logstash-forwarder start
       ```
       {: codeblock}
        
       Enable the mt-logstash-forwarder to start automatically after a crash or reboot. 
        
       ```
       service mt-logstash-forwarder enable
       ```
       {: codeblock}
        
       **Tip:** To restart the mt-logstash-forwarder service, run the following command:
    
       ```
       service mt-logstash-forwarder restart
       ```
       {: codeblock}
        
        
By default, the forwarder only watches syslog. Your logs are available in Kibana for analysis.
        

## Step 3: Specify more log files
{: #add_logs}

By default, only the /var/log/syslog file is monitored by the forwarder. You can add more configuration files to the following directory `/etc/mt-logstash-forwarder/conf.d/syslog.conf/` for the forwarder to monitor them as well. 

Complete the following steps to add a configuration file for an app that runs in your environment:

1.	Copy the `/etc/mt-logstash-forwarder/conf.d/syslog.conf` file. 

    **Tip:** Do not edit the syslog.conf file to add log files.
    
    For example, in an Ubuntu system, run the following command:
    
    ```
    cp /etc/mt-logstash-forwarder/conf.d/syslog.conf /etc/mt-logstash-forwarder/conf.d/myapp.conf
    ```
    {: codeblock}
        
2.	With a text editor, edit the *myapp.conf* file, and update the file to include the application logs that you want to monitor. Include the log type for each app log. Delete any examples that are not used.

3.	Restart the mt-logstash-forwarder. 

     Restart the mt-logstash-forwarder service. Run the following command:
    
    ```
    service mt-logstash-forwarder restart
    ```
    {: codeblock}

**Example**

To include the stdout or stderr from a hello app, redirect stdout or stderr to a log file. Create a forwarder config file for the app. Then, restart the mt-logstash-forwarder.

1.	Copy the `/etc/mt-logstash-forwarder/conf.d/syslog.conf` file. 

    ```
    cp /etc/mt-logstash-forwarder/conf.d/syslog.conf /etc/mt-logstash-forwarder/conf.d/myapp.conf
    ```
    {: codeblock}
    
2. Edit the config file *myapp.conf*.

    To be able to search by a JSON field in Kibana when you ingest a log, enable JSON parsing. Set `is_json` to true in the config file for specific file paths. For log files that are configured this way, the log lines should be formatted as JSON blocks, separated by carriage returns. The mt-logstash-forwarder will then consume all those JSON fields as individual Kibana-searchable fields. JSON field names include a suffix that is based on type.
    
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
