---

copyright:
  years: 2017
lastupdated: "2017-07-28"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Configuring the Log collection CLI
{: #config_log_collection_cli}

The {{site.data.keyword.loganalysisshort}} service includes a command line interface (CLI) that you can use to manage your logs in the cloud. The CLI is a Cloud Foundry (CF) plugin. You can use commands to view the status of the log, to download logs, and to configure the log retention policy. The CLI offers different types of help: general help to learn about the CLI and supported commands, command help to learn how to use a command, or subcommand help to learn how to use a subcommands for a command.
{:shortdesc}


## Installing the Log Collection CLI
{: #install_cli}

To install the Log Collection CLI, complete the following steps:

1. Check the CF CLI is available in your system. 

    For more information, see [Pre-requisite](/docs/services/CloudLogAnalysis/how-to/manage-logs/config_log_collection_cli.html#pre_req).

2. Install the Log Collection CF plugin:

    * For Linux, see [Installing the Log Collection CLI on Linux](/docs/services/CloudLogAnalysis/how-to/manage-logs/config_log_collection_cli.html#install_cli_linux).
    * For Windows, see [Installing the Log Collection CLI on Windows](/docs/services/CloudLogAnalysis/how-to/manage-logs/config_log_collection_cli.html#install_cli_windows).
    * For Mac OS X, see [Installing the Log Collection CLI on Mac OS X ](/docs/services/CloudLogAnalysis/how-to/manage-logs/config_log_collection_cli.html#install_cli_mac).
 

## Pre-requisite
{: #pre_req}

The Log Collection CLI is a CF plugin. Before you can install it, consider the following scenarios:

* You are installing for the first time the CF CLI:

     Install the CF plugin. For more information, see [Installing the cf CLI ![External link icon](../../../icons/launch-glyph.svg "External link icon")](http://docs.cloudfoundry.org/cf-cli/install-go-cli.html){: new_window}. 

* You have the {{site.data.keyword.Bluemix_notm}} CLI package installed:

    The CF CLI is bundled in the {{site.data.keyword.Bluemix_notm}} CLI package.

* You will need the {{site.data.keyword.Bluemix_notm}} CLI to manage other Cloud resources:  

    Install the {{site.data.keyword.Bluemix_notm}} CLI package, see [Installing the {{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/reference/bluemix_cli/index.html#install_bluemix_cli).

Then, verify the CF plugin is available. Run the following command from a session in your system:
    
```
cf -v
```
{: codeblock}
    
The output looks as follows:
    
```
cf version 6.25.0+787326d.2017-02-28
```
{: screen}

**Note:**  You cannot mix {{site.data.keyword.Bluemix_notm}} CLI commands, that is, `bx` commands, and CF CLI commands, that is, `cf` commands.



	
## Installing the Log Collection CLI on Linux
{: #install_cli_linux}

Complete the following steps to install the Log Collection CF plugin on Linux:

1. Install the Log Collection CLI plugin.

    1. Download the latest release of the {{site.data.keyword.loganalysisshort}} service CLI plugin (IBM-Logging) from [the Bluemix CLI page](https://clis.ng.bluemix.net/ui/repository.html#cf-plugins). 
	
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
        cf install-plugin -f logging-cli-linux64
        ```
        {: codeblock}

2. Set the environment variable **LANG**.

    Set *LANG* to the default value *en_US.UTF-8* if your system locale is not supported by CF. For information about CF supported locales, see [Getting Started with the cf CLI ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://docs.cloudfoundry.org/cf-cli/getting-started.html){: new_window}
	
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
    cf logging --version
    ```
    {: codeblock}
    
    The output looks as follows:
   
    ```
    cf logging version 0.3.5
    ```
    {: screen}


## Installing the Log Collection CLI on Windows
{: #install_cli_windows}

Complete the following steps to install the Log Collection CF plugin on Windows:

1. Download the latest release of the {{site.data.keyword.loganalysisshort}} service CLI plugin (IBM-Logging) from [the Bluemix CLI page](https://clis.ng.bluemix.net/ui/repository.html#cf-plugins). 
	
	1. Select the platform value: **win64**. 
	2. Click **Save file**.  
    
2. Run the **cf install-plugin** command to install the Log Collection plugin on Windows. 

    ```
	cf install-plugin PluginName
	```
	{: codeblock}
	
	where *PluginName* is the name of the file that you have downloaded.
	
    For example, to install the plugin *logging-cli-win64_v1.0.1.exe*, run the following command from a terminal window:
	
	```
	cf install-plugin logging-cli-win64_v1.0.1.exe
	```
	{: codeblock}
	
    When the plugin is installed, you get the following message: `Plugin IBM-Logging 1.0.1 successfully installed.`

3. Verify the installation of the logging CLI plugin.
  
    For example, check the version of the plugin. Run the following command:
    
    ```
    cf logging --version
    ```
    {: codeblock}
    
    The output looks as follows:
   
    ```
    cf logging version 1.0.1
    ```
    {: screen}
	

## Installing the Log Collection CLI on Mac OS X
{: #install_cli_mac}

Complete the following steps to install the Log Collection CF plugin on Mac OS X:

1. Download the latest release of the {{site.data.keyword.loganalysisshort}} service CLI plugin (IBM-Logging) from [the Bluemix CLI page](https://clis.ng.bluemix.net/ui/repository.html#cf-plugins). 
	
	1. Select the platform value: **osx**. 
	2. Click **Save file**.  
    
2. Run the **cf install-plugin** command to install the Log Collection plugin on Mac OS X. 

    ```
	cf install-plugin PluginName
	```
	{: codeblock}
	
	where *PluginName* is the name of the file that you have downloaded.
	
    For example, to install the plugin *logging-cli-darwin_v1.0.1*, run the following command from a terminal:
	
	```
	cf install-plugin logging-cli-darwin_v1.0.1
	```
	{: codeblock}
	
    When the plugin is installed, you get the following message: `Plugin IBM-Logging 1.0.1 successfully installed.`

3. Verify the installation of the logging CLI plugin.
  
    For example, check the version of the plugin. Run the following command:
    
    ```
    cf logging --version
    ```
    {: codeblock}
    
    The output looks as follows:
   
    ```
    cf logging version 1.0.1
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
    cf plugins
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
    cf uninstall-plugin IBM-Logging
    ```
    {: codeblock}
  

## Getting general help
{: #general_cli_help}

To get general information about the CLI and what commands are supported, complete the followimg steps:

1. Log in to a {{site.data.keyword.Bluemix_notm}} region, organization, and space. 

    For example, to log in to the US South region, run the following command:
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. List information about the supported commands and the CLI. Run the following command:

    ```
    cf logging help 
    ```
    {: codeblock}
    
    

## Getting help on a command
{: #command_cli_help}

To get help on how to use a command, complete the followimg steps:

1. Log in to a {{site.data.keyword.Bluemix_notm}} region, organization, and space. 

    For example, to log in to the US South region, run the following command:
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Get the list of supported comnmands and identify the one that you need. Run the command:

    ```
    cf logging help 
    ```
    {: codeblock}

3. Get help on the command. Run the following command:

    ```
    cf logging help *Command*
    ```
    {: codeblock}
    
    where *Command* is the name of a CLI command, for example, *status*.



## Getting help on a subcommand
{: #subcommand_cli_help}

A command can have subcommands. To get help on subcommands, complete the followimg steps:

1. Log in to a {{site.data.keyword.Bluemix_notm}} region, organization, and space. 

    For example, to log in to the US South region, run the following command:
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Get the list of supported comnmands and identify the one that you need. Run the command:

    ```
    cf logging help 
    ```
    {: codeblock}

3. Get help on the command and identify the supported subcommands. Run the following command:

    ```
    cf logging help *Command*
    ```
    {: codeblock}
    
    where *Command* is the name of a CLI command, for example, *session*.

4. Get help on the command and identify the supported subcommands. Run the following command:

    ```
    cf logging *Command* help *Subcommand*
    ```
    {: codeblock}
    
    where 
    
    * *Command* is the name of a CLI command, for example, *status*.
    * *Subcommand* is the name of a supported subcommand, for example, for the command *session*, a valid subcommand is *list*.




