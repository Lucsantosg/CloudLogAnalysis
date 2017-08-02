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

# Configuration de l'interface de ligne de commande Collecte des journaux
{: #config_log_collection_cli}

Le service {{site.data.keyword.loganalysisshort}} inclut une interface de ligne de commande (CLI) que vous pouvez utiliser pour gérer vos journaux dans le cloud. L'interface CLI
est un plug-in Cloud Foundry (CF). Vous pouvez utiliser des commandes pour afficher l'état du journal, pour télécharger des journaux et pour configurer la règle de conservation des journaux. L'interface CLI offre différents types d'aides : une aide générale concernant l'interface CLI et les commandes prises en charge,
une aide relative aux commandes pour savoir comment utiliser une commande et une aide relative aux sous-commandes pour savoir comment utiliser une sous-commande d'une commande.
{:shortdesc}


## Installation de l'interface de ligne de commande Collecte des journaux
{: #install_cli}

Pour installer l'interface de ligne de commande Log Collection, procédez comme suit :

1. Vérifiez si l'interface de ligne de commande CF est disponible dans votre système.  

    Pour plus d'informations, voir [Prérequis](/docs/services/CloudLogAnalysis/how-to/manage-logs/config_log_collection_cli.html#pre_req).

2. Installez le plug-in CF Log Collection :

    * Pour Linux, voir [Installation de l'interface de ligne de commande Log Collection sous Linux](/docs/services/CloudLogAnalysis/how-to/manage-logs/config_log_collection_cli.html#install_cli_linux).
    * Pour Windows, voir [Installation de l'interface de ligne de commande Log Collection sous Windows](/docs/services/CloudLogAnalysis/how-to/manage-logs/config_log_collection_cli.html#install_cli_windows).
    * Pour Mac OS X, voir [Installation de l'interface de ligne de commande Log Collection sous Mac OS X](/docs/services/CloudLogAnalysis/how-to/manage-logs/config_log_collection_cli.html#install_cli_mac).
 

## Prérequis
{: #pre_req}

L'interface de ligne de commande Log Collection est un plug-in CF. Avant de l'installer, examinez les scénarios suivants :

* Vous installez l'interface de ligne de commande CF pour la première fois :

     Installez le plug-in CF. Pour plus d'informations, voir [Installation de l'interface de ligne de commande cf ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](http://docs.cloudfoundry.org/cf-cli/install-go-cli.html){: new_window}. 

* Le package de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}} est installé :

    L'interface de ligne de commande CF est intégré dans le package de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}. 

* Vous aurez besoin de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}} pour gérer d'autres ressources Cloud :  

    Installez le package de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}. Voir [Installation de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}](/docs/cli/reference/bluemix_cli/index.html#install_bluemix_cli).

Ensuite, vérifiez que le plug-in CF est disponible. Exécutez la commande suivante à partir d'une session dans votre système :
    
```
cf -v
```
{: codeblock}
    
La sortie prend la forme suivante :
    
```
cf version 6.25.0+787326d.2017-02-28
```
{: screen}

**Remarque :** vous ne pouvez pas mélanger des commandes d'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}, c'est-à-dire, des commandes `bx`, et des commandes d'interface de ligne de commande CF, c'est-à-dire des commandes `cf`. 



	
## Installation de l'interface de ligne de commande Log Collection sous Linux
{: #install_cli_linux}

Procédez comme suit pour installer le plug-in CF Log Collection sous Linux :

1. Installez le plug-in d'interface de ligne de commande Log Collection.

    1. Téléchargez la dernière édition du plug-in d'interface de ligne de commande du service {{site.data.keyword.loganalysisshort}} (IBM-Logging) depuis la [page relative à l'interface de ligne de commande Bluemix](https://clis.ng.bluemix.net/ui/repository.html#cf-plugins). 
	
		Sélectionnez la valeur de plateforme : **linux64**.
		Cliquez sur **Save file**. 
    
    2. Décompressez le plug-in.
    
        Par exemple, pour décompresser le plug-in `logging-cli-linux64.gz` dans Ubuntu, exécutez la commande suivante :
        
        ```
        gunzip logging-cli-linux64.gz
        ```
        {: codeblock}

    3. Rendez le fichier exécutable.
    
        Par exemple, pour rendre le fichier `logging-cli-linux64` exécutable, exécutez la commande suivante :
        
        ```
        chmod a+x logging-cli-linux64
        ```
        {: codeblock}

    4. Installation du plug-in CF de journalisation.
    
        Par exemple, pour rendre le fichier `logging-cli-linux64` exécutable, exécutez la commande suivante :
        
        ```
        cf install-plugin -f logging-cli-linux64
        ```
        {: codeblock}

2. Définissez la variable d'environnement **LANG**.

    Définissez *LANG* sur la valeur par défaut : *en_US.UTF-8* si l'environnement local de votre système n'est pas pris en charge par CF. Pour des informations
sur les environnements locaux pris en charge par CF, voir [Getting Started with the cf CLI
![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://docs.cloudfoundry.org/cf-cli/getting-started.html){: new_window}
	
	Par exemple, dans un système Ubuntu, éditez le fichier *~/.bashrc* et entrez les lignes suivantes :
    
    ```
    # add entry for logging CLI
    export LANG = en_US.UTF-8
    ```
    {: codeblock}
    
    Ouvrez une nouvelle fenêtre de terminal et exécutez la commande suivante pour vérifier que les variables LANG et LOGGING_ENDPOINT sont définies :
    
    ```
    $echo LANG
    en_US.UTF-8
    ```
    {: screen}   
    
3. Vérifiez l'installation du plug-in de l'interface de ligne de commande de journalisation.
  
    Par exemple, vérifiez la version du plug-in. Exécutez la commande suivante :
    
    ```
    cf logging --version
    ```
    {: codeblock}
    
    La sortie prend la forme suivante :
   
    ```
    cf logging version 0.3.5
    ```
    {: screen}


## Installation de l'interface de ligne de commande Log Collection sous Windows
{: #install_cli_windows}

Procédez comme suit pour installer le plug-in CF Log Collection sous Windows :

1. Téléchargez la dernière édition du plug-in d'interface de ligne de commande du service {{site.data.keyword.loganalysisshort}} (IBM-Logging) depuis la [page relative à l'interface de ligne de commande Bluemix](https://clis.ng.bluemix.net/ui/repository.html#cf-plugins). 
	
	1. Sélectionnez la valeur de plateforme : **win64**.	 
	2. Cliquez sur **Save file**.  
    
2. Exécutez la commande **cf install-plugin** pour installer le plug-in Log Collection sous Windows. 

    ```
	cf install-plugin PluginName
	```
	{: codeblock}
	
	où *PluginName* est le nom du fichier que vous avez téléchargé.
	
    Par exemple, pour installer le plug-in *logging-cli-win64_v1.0.1.exe*, exécutez la commande suivante depuis une fenêtre de terminal :
	
	```
	cf install-plugin logging-cli-win64_v1.0.1.exe
	```
	{: codeblock}
	
    Lorsque le plug-in est installé, le message suivant s'affiche : `Plugin IBM-Logging 1.0.1 successfully installed.`

3. Vérifiez l'installation du plug-in d'interface de ligne de commande logging.

    Par exemple, vérifiez la version du plug-in. Exécutez la commande suivante :
    
    ```
    cf logging --version
    ```
    {: codeblock}
    
    La sortie prend la forme suivante :
   
    ```
    cf logging version 1.0.1
    ```
    {: screen}
	
    ## Installation de l'interface de ligne de commande Log Collection sous Mac OS X
{: #install_cli_mac}

Procédez comme suit pour installer le plug-in CF Log Collection sous Mac OS X :

1. Téléchargez la dernière édition du plug-in d'interface de ligne de commande du service {{site.data.keyword.loganalysisshort}} (IBM-Logging) depuis [la page relative à l'interface de ligne de commande Bluemix](https://clis.ng.bluemix.net/ui/repository.html#cf-plugins). 	
	1. Sélectionnez la valeur de plateforme : **osx**.
	2. Cliquez sur **Save file**.

2. Exécutez la commande **cf install-plugin** pour installer le plug-in Log Collection sous Mac OS X.

    ```
	cf install-plugin PluginName
	```
	{: codeblock}
	
	où *PluginName* est le nom du fichier que vous avez téléchargé.
	
    Par exemple, pour installer le plug-in *logging-cli-darwin_v1.0.1*, exécutez la commande suivante depuis un terminal :
	
	```
	cf install-plugin logging-cli-darwin_v1.0.1
	```
	{: codeblock}
	
    Lorsque le plug-in est installé, le message suivant s'affiche : `Plugin IBM-Logging 1.0.1 successfully installed.`

3. Vérifiez l'installation du plug-in d'interface de ligne de commande logging.

    Par exemple, vérifiez la version du plug-in. Exécutez la commande suivante :
    
    ```
    cf logging --version
    ```
    {: codeblock}

    La sortie prend la forme suivante :
   
    ```
    cf logging version 1.0.1
    ```
    {: screen}
	
	
## Désinstallation de l'interface de ligne de commande Log Collection
{: #uninstall_cli}

Pour désinstaller l'interface de ligne de commande logging, supprimez le plug-in.
{:shortdesc}

Procédez comme suit pour désinstaller l'interface de ligne de commande du service {{site.data.keyword.loganalysisshort}} :

1. Vérifiez la version du plug-in de l'interface de ligne de commande de journalisation qui est installée.

    Par exemple, vérifiez la version du plug-in. Exécutez la commande suivante :
    
    ```
    cf plugins
    ```
    {: codeblock}

    La sortie prend la forme suivante :
   
    ```
    Listing Installed Plugins...
    OK

    Plugin Name   Version   Command Name   Command Help
    IBM-Logging   1.0.1     logging        IBM Logging plug-in
    ```
    {: screen}

2. Si le plug-in est installé, exécutez la commande `cf uninstall-plugin` pour désinstaller le plug-in de l'interface de ligne de commande de journalisaiton (logging).

    Exécutez la commande suivante :
        
    ```
    cf uninstall-plugin IBM-Logging
    ```
    {: codeblock}
  

## Obtention de l'aide générale
{: #general_cli_help}

Pour obtenir des informations générales sur l'interface de ligne de commande et sur les commandes prises en charge, procédez comme suit :

1. Connectez-vous à un espace, à une organisation et à une région {{site.data.keyword.Bluemix_notm}}. 

    Par exemple, pour vous connecter à la région du sud des États-Unis, exécutez la commande suivante :

```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Affichez des informations sur les commandes prises en charge et sur l'interface de ligne de commande. Exécutez la commande suivante :

    ```
    cf logging help 
    ```
    {: codeblock}
    
    

## Obtenir de l'aide sur une commande
{: #command_cli_help}

Pour obtenir de l'aide au sujet de l'utilisation d'une commande, procédez comme suit :

1. Connectez-vous à un espace, une organisation ou une région {{site.data.keyword.Bluemix_notm}}.  

    Par exemple, pour vous connecter à la région du sud des États-Unis, exécutez la commande suivante :
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Obtenez la liste des commandes prises en charge et identifiez celle dont vous avez besoin. Exécutez la commande suivante :

    ```
    cf logging help 
    ```
    {: codeblock}

3. Obtenez de l'aide sur la commande. Exécutez la commande suivante :

    ```
    cf logging help *Command*
    ```
    {: codeblock}
    
    où *Command* est le nom d'une commande de l'interface de ligne de commande, par exemple *status*.



## Obtention d'aide sur une sous-commande
{: #subcommand_cli_help}

Une commande peut avoir des sous-commandes. Pour obtenir de l'aide sur des sous-commandes, procédez comme suit :

1. Connectez-vous à un espace, une organisation ou une région {{site.data.keyword.Bluemix_notm}}.  

    Par exemple, pour vous connecter à la région du sud des États-Unis, exécutez la commande suivante :
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Obtenez la liste des commandes prises en charge et identifiez celle dont vous avez besoin. Exécutez la commande suivante :

    ```
    cf logging help 
    ```
    {: codeblock}

3. Obtenez de l'aide sur la commande et identifiez les sous-commandes prises en charge. Exécutez la commande suivante :

    ```
    cf logging help *Command*
    ```
    {: codeblock}
    
    où *Command* est le nom d'une commande de l'interface de ligne de commande, par exemple *session*.

4. Obtenez de l'aide sur la commande et identifiez les sous-commandes prises en charge. Exécutez la commande suivante :

    ```
    cf logging *Command* help *Subcommand*
    ```
    {: codeblock}
    
    où 
    
    * *Command* est le nom d'une commande de l'interface de ligne de commande, par exemple *status*.
    * *Subcommand* est le nom d'une sous-commande prise en charge. Par exemple, pour la commande *session*, une sous-commande valide est *list*.




