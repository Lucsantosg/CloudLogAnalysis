---

copyright:
  years: 2017
lastupdated: "2017-11-20"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Configuring the Log Analysis CLI (CF plugin)
{: #config_log_collection_cli}

The {{site.data.keyword.loganalysisshort}} service includes a command line interface (CLI) that you can use to manage your logs in the cloud. You can use the Cloud Foundry (CF) plugin to view the status of the log, to download logs, and to configure the log retention policy. The CLI offers different types of help: general help to learn about the CLI and supported commands, command help to learn how to use a command, or subcommand help to learn how to use a subcommands for a command.
{:shortdesc}



## Installing the Log Collection CF plugin
{: #install_cli}

To install the {{site.data.keyword.loganalysisshort}} CLI, complete the following steps:

1. Install the {{site.data.keyword.Bluemix_notm}} CLI.

   For more information, see [Installing the {{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/reference/bluemix_cli/download_cli.html#download_install).

2. Install the {{site.data.keyword.loganalysisshort}} CF plugin.

    * For Linux, see [Installing the {{site.data.keyword.loganalysisshort}} CLI on Linux](/docs/services/CloudLogAnalysis/how-to/manage-logs/config_log_collection_cli.html#install_cli_linux).
    * For Windows, see [Installing the {{site.data.keyword.loganalysisshort}} CLI on Windows](/docs/services/CloudLogAnalysis/cli/config_at_cli.html#install_cli_windows).
    * For Mac OS X, see [Installing the {{site.data.keyword.loganalysisshort}} CLI on Mac OS X ](/docs/services/CloudLogAnalysis/cli/config_at_cli.html#install_cli_mac).
 
3. Verify the installation of the CLI plugin.
  
    For example, check the version of the plugin. Run the following command:
    
    ```
    bx cf plugins
    ```
    {: codeblock}
    
    The output looks as follows:
   
    ```
    Invoking 'cf plugins'...

    Listing Installed Plugins...
    OK

    Plugin Name           Version   Command Name   Command Help
    IBM-Logging           1.0.2     logging        IBM Logging plug-in
    ```
    {: screen}
 


## Installing the Log Collection CLI on Linux
{: #install_cli_linux}

Complete the following steps to install the Log Collection CF plugin on Linux:

1. Install the Log Collection CLI plugin.

    1. Download the latest release of the {{site.data.keyword.loganalysisshort}} service CLI plugin (IBM-Logging) from [the {{site.data.keyword.Bluemix_notm}} CLI page](https://clis.ng.bluemix.net/ui/repository.html#cf-plugins). 
	
		Select the platform value: **linux64**. 
		Click **Save file**. 
    
    2. Unzip the plugin.
    
        For example, to unzip the `logging-cli-linux64.gz` plugin in Ubuntu, run the following command:
        
        ```
        gunzip logging-cli-linux64.gz
        ```
        {: codeblock}

    3. Make the file executable.
    
        For example, to make the file `logging-cli-linux64` executable, run the following command:
        
        ```
        chmod a+x logging-cli-linux64
        ```
        {: codeblock}

    4. Install the logging CF plugin.
    
        For example, to make the file `logging-cli-linux64` executable, run the following command:
        
        ```
        bx cf install-plugin -f logging-cli-linux64
        ```
        {: codeblock}

2. Set the environment variable **LANG**.

    Set *LANG* to the default value *en_US.UTF-8* if your system locale is not supported by CF. For information about CF supported locales, see [Getting Started with the cf CLI ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://docs.cloudfoundry.org/cf-cli/getting-started.html){: new_window}
	
	For example in an Ubuntu system, edit the  *~/.bashrc* file and enter the following lines:
    
    ```
    # add entry for logging CLI
    export LANG = en_US.UTF-8
    ```
    {: codeblock}
    
    Open a new terminal window and run the following command to verify that the variables LANG and LOGGING_ENDPOINT are set:
    
    ```
    $echo LANG
    en_US.UTF-8
    ```
    {: screen}   
    
3. Verify the installation of the logging CLI plugin.
  
    For example, check the version of the plugin. Run the following command:
    
    ```
    bx cf logging --version
    ```
    {: codeblock}
    
    The output looks as follows:
   
    ```
    cf logging version 1.0.2
    ```
    {: screen}


## Installing the Log Collection CLI on Windows
{: #install_cli_windows}

Complete the following steps to install the Log Collection CF plugin on Windows:

1. Download the latest release of the {{site.data.keyword.loganalysisshort}} service CLI plugin (IBM-Logging) from [the {{site.data.keyword.Bluemix_notm}} CLI page](https://clis.ng.bluemix.net/ui/repository.html#cf-plugins). 
	
	1. Select the platform value: **win64**. 
	2. Click **Save file**.  
    
2. Run the **cf install-plugin** command to install the Log Collection plugin on Windows. 

    ```
	bx cf install-plugin PluginName
	```
	{: codeblock}
	
	where *PluginName* is the name of the file that you have downloaded.
	
    For example, to install the plugin *logging-cli-win64_v1.0.1.exe*, run the following command from a terminal window:
	
	```
	bx cf install-plugin logging-cli-win64_v1.0.1.exe
	```
	{: codeblock}
	
    When the plugin is installed, you get the following message: `Plugin IBM-Logging 1.0.1 successfully installed.`

3. Verify the installation of the logging CLI plugin.
  
    For example, check the version of the plugin. Run the following command:
    
    ```
    bx cf logging --version
    ```
    {: codeblock}
    
    The output looks as follows:
   
    ```
    bx cf logging version 1.0.1
    ```
    {: screen}
	

## Installing the Log Collection CLI on Mac OS X
{: #install_cli_mac}

Complete the following steps to install the Log Collection CF plugin on Mac OS X:

1. Download the latest release of the {{site.data.keyword.loganalysisshort}} service CLI plugin (IBM-Logging) from [the {{site.data.keyword.Bluemix_notm}} CLI page](https://clis.ng.bluemix.net/ui/repository.html#cf-plugins). 
	
	1. Select the platform value: **osx**. 
	2. Click **Save file**.  
    
2. Run the **cf install-plugin** command to install the Log Collection plugin on Mac OS X. 

    ```
	bx cf install-plugin PluginName
	```
	{: codeblock}
	
	where *PluginName* is the name of the file that you have downloaded.
	
    For example, to install the plugin *logging-cli-darwin_v1.0.1*, run the following command from a terminal:
	
	```
	bx cf install-plugin logging-cli-darwin_v1.0.1
	```
	{: codeblock}
	
    When the plugin is installed, you get the following message: `Plugin IBM-Logging 1.0.1 successfully installed.`

3. Verify the installation of the logging CLI plugin.
  
    For example, check the version of the plugin. Run the following command:
    
    ```
    bx cf logging --version
    ```
    {: codeblock}
    
    The output looks as follows:
   
    ```
    bx cf logging version 1.0.1
    ```
    {: screen}
	
	
## Uninstalling the Log Collection CLI
{: #uninstall_cli}

To uninstall the logging CLI, delete the plugin.
{:shortdesc}

Complete the following steps to uninstall the {{site.data.keyword.loganalysisshort}} service CLI:

1. Verify the version of the logging CLI plugin that is installed.
  
    For example, check the version of the plugin. Run the following command:
    
    ```
    bx cf plugins
    ```
    {: codeblock}
    
    The output looks as follows:
   
    ```
    Listing Installed Plugins...
    OK

    Plugin Name   Version   Command Name   Command Help
    IBM-Logging   1.0.1     logging        IBM Logging plug-in
    ```
    {: screen}
    
2. If the plugin is installed, run the `cf uninstall-plugin` to uninstall the logging CLI plugin.

    Run the following command:
        
    ```
    bx cf uninstall-plugin IBM-Logging
    ```
    {: codeblock}
  

## Getting general help
{: #general_cli_help}

To get general information about the CLI and what commands are supported, complete the followimg steps:

1. Log in to a region, organization, and space in the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
    
2. List information about the supported commands and the CLI. Run the following command:

    ```
    bx cf logging help 
    ```
    {: codeblock}
    
    

## Getting help on a command
{: #command_cli_help}

To get help on how to use a command, complete the followimg steps:

1. Log in to a region, organization, and space in the {{site.data.keyword.Bluemix_notm}}. 

    For more information, see [How do I log in to the {{site.data.keyword.Bluemix_notm}}](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
    
2. Get the list of supported comnmands and identify the one that you need. Run the command:

    ```
    bx cf logging help 
    ```
    {: codeblock}

3. Get help on the command. Run the following command:

    ```
    bx cf logging help *Command*
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
    bx cf logging help 
    ```
    {: codeblock}

3. Get help on the command and identify the supported subcommands. Run the following command:

    ```
    bx cf logging help *Command*
    ```
    {: codeblock}
    
    where *Command* is the name of a CLI command, for example, *session*.

4. Get help on the command and identify the supported subcommands. Run the following command:

    ```
    bx cf logging *Command* help *Subcommand*
    ```
    {: codeblock}
    
    where 
    
    * *Command* is the name of a CLI command, for example, *status*.
    * *Subcommand* is the name of a supported subcommand, for example, for the command *session*, a valid subcommand is *list*.




