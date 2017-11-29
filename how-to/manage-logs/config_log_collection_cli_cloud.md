---

copyright:
  years: 2017
lastupdated: "2017-11-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Configuring the Log Analysis CLI ({{site.data.keyword.Bluemix_notm}} plugin)
{: #config_log_collection_cli}

The {{site.data.keyword.loganalysisshort}} service includes a command line interface (CLI) that you can use to manage your logs in the cloud. You can use the {{site.data.keyword.Bluemix_notm}} plugin to view the status of the log, to download logs, and to configure the log retention policy. The CLI offers different types of help: general help to learn about the CLI and supported commands, command help to learn how to use a command, or subcommand help to learn how to use a subcommands for a command.
{:shortdesc}



## Installing the Log Analysis plugin
{: #install_cli}

To install the {{site.data.keyword.loganalysisshort}} CLI, complete the following steps:

1. Install the {{site.data.keyword.Bluemix_notm}} CLI.

   For more information, see [Installing the {{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/reference/bluemix_cli/download_cli.html#download_install).

2. Install the {{site.data.keyword.loganalysisshort}} plugin.

    * For Linux, see [Installing the {{site.data.keyword.loganalysisshort}} plugin on Linux](/docs/services/CloudLogAnalysis/how-to/manage-logs/config_log_collection_cli_cloud.html#install_cli_linux).
    * For Windows, see [Installing the {{site.data.keyword.loganalysisshort}} plugin on Windows](/docs/services/CloudLogAnalysis/how-to/manage-logs/config_log_collection_cli_cloud.html#install_cli_windows).
    * For Mac OS X, see [Installing the {{site.data.keyword.loganalysisshort}} plugin on Mac OS X ](/docs/services/CloudLogAnalysis/how-to/manage-logs/config_log_collection_cli_cloud.html#install_cli_mac).
 
3. Verify the installation of the CLI plugin.
  
    For example, check the version of the plugin. Run the following command:
    
    ```
    bx plugin list
    ```
    {: codeblock}
    
    The output looks as follows:
   
    ```
    bx plugin list
    Listing installed plug-ins...

    Plugin Name          Version   
    logging-cli          0.1.1   
    ```
    {: screen}
 


## Installing the Log Analysis plugin on Linux
{: #install_cli_linux}

Complete the following steps to install the Log Collection plugin on Linux:

1. Install the plugin.

    Download the latest release of the {{site.data.keyword.loganalysisshort}} service CLI plugin (IBM-Logging) from [the {{site.data.keyword.Bluemix_notm}} CLI page](https://clis.ng.bluemix.net/ui/repository.html#bluemix-plugins). 
	
	* Select the platform value: **linux64**. 
	
	* Click **Save file**. 
    
2. Install the plugin. Run the following command:
        
    ```
    bx plugin install -f logging-cli-linux-amd64-0.1.1
    ```
    {: codeblock}




## Installing the Log Analysis plugin on Windows
{: #install_cli_windows}

Complete the following steps to install the Log Collection plugin on Windows:

1. Download the latest release of the {{site.data.keyword.loganalysisshort}} service CLI plugin (IBM-Logging) from [the {{site.data.keyword.Bluemix_notm}} CLI page](https://clis.ng.bluemix.net/ui/repository.html#cf-plugins). 
	
	1. Select the platform value: **win64**. 
	2. Click **Save file**.  
    
2. Install the plugin. Run the following command:
        
    ```
    bx plugin install -f logging-cli-windows-amd64-0.1.1.exe
    ```
    {: codeblock}

	

## Installing the Log Analysis plugin on Mac OS X
{: #install_cli_mac}

Complete the following steps to install the Log Collection plugin on Mac OS X:

1. Download the latest release of the {{site.data.keyword.loganalysisshort}} service CLI plugin (IBM-Logging) from [the {{site.data.keyword.Bluemix_notm}} CLI page](https://clis.ng.bluemix.net/ui/repository.html#cf-plugins). 
	
	1. Select the platform value: **osx**. 
	2. Click **Save file**.  
    
2. Install the plugin. Run the following command:
        
    ```
    bx plugin install -f logging-cli-darwin-amd64-0.1.1
    ```
    {: codeblock}

	
	
## Uninstalling the Log Analysis CLI
{: #uninstall_cli}

To uninstall the logging CLI, delete the plugin.
{:shortdesc}

Complete the following steps to uninstall the {{site.data.keyword.loganalysisshort}} service CLI:

1. Verify the version of the logging CLI plugin that is installed.
  
    For example, check the version of the plugin. Run the following command:
    
    ```
    bx plugin list
    ```
    {: codeblock}
    
    The output looks as follows:
   
    ```
    bx plugin list
    Listing installed plug-ins...

    Plugin Name          Version   
    logging-cli          0.1.1   
    ```
    {: screen}
    
2. If the plugin is installed, run the `bx plugin uninstall` to uninstall the logging CLI plugin.

    Run the following command:
        
    ```
    bx plugin uninstall logging-cli
    ```
    {: codeblock}
  

## Getting general help
{: #general_cli_help}

To get general information about the CLI and what commands are supported, complete the followimg steps:

1. Log in to a region, organization, and space in the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
    
2. List information about the supported commands and the CLI. Run the following command:

    ```
    bx logging help 
    ```
    {: codeblock}
    
    

## Getting help on a command
{: #command_cli_help}

To get help on how to use a command, complete the followimg steps:

1. Log in to a region, organization, and space in the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
    
2. Get the list of supported comnmands and identify the one that you need. Run the command:

    ```
    bx logging help 
    ```
    {: codeblock}

3. Get help on the command. Run the following command:

    ```
    bx logging help *Command*
    ```
    {: codeblock}
    
    where *Command* is the name of a CLI command, for example, *status*.



## Getting help on a subcommand
{: #subcommand_cli_help}

A command can have subcommands. To get help on subcommands, complete the followimg steps:

1. Log in to a region, organization, and space in the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
    
2. Get the list of supported comnmands and identify the one that you need. Run the command:

    ```
    bx logging help 
    ```
    {: codeblock}

3. Get help on the command and identify the supported subcommands. Run the following command:

    ```
    bx logging help *Command*
    ```
    {: codeblock}
    
    where *Command* is the name of a CLI command, for example, *session*.

4. Get help on the command and identify the supported subcommands. Run the following command:

    ```
    bx logging *Command* help *Subcommand*
    ```
    {: codeblock}
    
    where 
    
    * *Command* is the name of a CLI command, for example, *status*.
    * *Subcommand* is the name of a supported subcommand, for example, for the command *session*, a valid subcommand is *list*.


## Show the details of the plugin
{: #show}
  
Use the 'bx plugin show logging-cli' command to show the plugin details. 

```
bx plugin show logging-cli
```
{: codeblock}
    
The output looks as follows:
   
```
bx plugin show logging-cli
                                  
Plugin                         logging-cli   
Version                        0.1.1   
Minimal CLI version required   0.5.0   
Commands                                                      
                               logging log-delete       Delete log      
                               logging log-download     Download a log      
                               logging log-show         Show the count, size, and type of logs per day      
                               logging session-create   Create a session      
                               logging session-delete   Delete session      
                               logging sessions         List sessions info      
                               logging session-show     Show a session info      
                               logging option-show      Show the log retention      
                               logging option-update    Show the log options    
```
{: screen}

