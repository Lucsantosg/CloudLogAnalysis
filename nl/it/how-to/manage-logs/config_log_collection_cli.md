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

# Configurazione della CLI di raccolta dei log
{: #config_log_collection_cli}

Il servizio {{site.data.keyword.loganalysisshort}} include una CLI (command line interface) che puoi utilizzare per gestire i tuoi log nel cloud. La CLI è un plugin Cloud Foundry (CF). Puoi utilizzare i comandi per visualizzare lo stato del log, per scaricare i log e per configurare la politica di conservazione dei log. La CLI offre diversi tipi di supporto: il supporto generale per le informazioni sulla CLI e i comandi supportati, il supporto sui comandi per le informazioni sull'utilizzo di un comando o il supporto sui comandi secondari per le informazioni su come utilizzare i comandi secondari di un comando.
{:shortdesc}


## Installazione della CLI di raccolta dei log
{: #install_cli}

Per installare la CLI della raccolta dei log, completa la seguente procedura:

1. Controlla che la CLI CF sia disponibile nel tuo sistema. 

    Per ulteriori informazioni, vedi [Prerequisito](/docs/services/CloudLogAnalysis/how-to/manage-logs/config_log_collection_cli.html#pre_req).

2. Installa il plugin CF di raccolta dei log:

    * Per Linux, vedi [Installazione della CLI di raccolta dei log su Linux](/docs/services/CloudLogAnalysis/how-to/manage-logs/config_log_collection_cli.html#install_cli_linux).
    * Per Windows, vedi [Installazione della CLI di raccolta dei log su Windows](/docs/services/CloudLogAnalysis/how-to/manage-logs/config_log_collection_cli.html#install_cli_windows).
    * Per Mac OS X, vedi [Installazione della CLI di raccolta dei log su Mac OS X ](/docs/services/CloudLogAnalysis/how-to/manage-logs/config_log_collection_cli.html#install_cli_mac).
 

## Prerequisito
{: #pre_req}

La CLI di raccolta dei log è un plugin CF. Prima di poterne eseguire l'installazione, considera i seguenti scenari:

* Stai installando per la prima volta la CLI CF:

     Installa il plugin CF. Per ulteriori informazioni, vedi il documento relativo all'[installazione della CLI cf ![Icona di link esterno](../../../../icons/launch-glyph.svg "Icona di link esterno")](http://docs.cloudfoundry.org/cf-cli/install-go-cli.html "Icona di link esterno"){: new_window}. 

* Hai un pacchetto CLI {{site.data.keyword.Bluemix_notm}} installato:

    La CLI CF è integrata nel pacchetto CLI {{site.data.keyword.Bluemix_notm}}.

* Avrai bisogno della CLI {{site.data.keyword.Bluemix_notm}} per gestire le altre risorse cloud:  

    Installa il pacchetto CLI {{site.data.keyword.Bluemix_notm}}; vedi [Installazione della CLI {{site.data.keyword.Bluemix_notm}}](/docs/cli/reference/bluemix_cli/index.html#install_bluemix_cli).

Verifica quindi che il plugin CF sia disponibile. Esegui il seguente comando da una sessione nel tuo sistema:
    
```
cf -v
```
{: codeblock}
    
L'output sarà simile al seguente:
    
```
cf version 6.25.0+787326d.2017-02-28
```
{: screen}

**Nota:**  non puoi combinare comandi CLI {{site.data.keyword.Bluemix_notm}}, ossia comandi `bx`, e comandi CLI CF, ossia comandi `cf`.



	
## Installazione della CLI di raccolta dei log su Linux
{: #install_cli_linux}

Completa la seguente procedura per installare il plugin CF di raccolta dei log su Linux:

1. Installa il plugin della CLI di raccolta dei log.

    1. Scarica la versione più recente del plugin della CLI del servizio {{site.data.keyword.loganalysisshort}} (IBM-Logging) dalla [pagina della CLI Bluemix](https://clis.ng.bluemix.net/ui/repository.html#cf-plugins). 
	
		Seleziona il valore della piattaforma: **linux64**.
		Fai clic su **Salva file**. 
    
    2. Decomprimi il plugin.
    
        Ad esempio, decomprimi il plugin `logging-cli-linux64.gz` in Ubuntu, esegui il seguente comando:
        
        ```
        gunzip logging-cli-linux64.gz
        ```
        {: codeblock}

    3. Rendi il file eseguibile.
    
        Ad esempio, per rendere il file `logging-cli-linux64` eseguibile, esegui il seguente comando:
        
        ```
        chmod a+x logging-cli-linux64
        ```
        {: codeblock}

    4. Installa il plugin CF di registrazione.
    
        Ad esempio, per rendere il file `logging-cli-linux64` eseguibile, esegui il seguente comando:
        
        ```
        cf install-plugin -f logging-cli-linux64
        ```
        {: codeblock}

2. Imposta la variabile di ambiente **LANG**.

    Configura *LANG* con il valore predefinito: *en_US.UTF-8* se il tuo sistema locale non è supportato da CF. Per informazioni sulle locali supportate da CF, vedi [Getting Started with the cf CLI ![Icona link esterno](../../../../icons/launch-glyph.svg "Icona link esterno")](https://docs.cloudfoundry.org/cf-cli/getting-started.html "Icona link esterno"){: new_window}
	
	Ad esempio in un sistema Ubuntu, modifica il file *~/.bashrc* e inserisci le seguenti righe:
    
    ```
    # add entry for logging CLI
    export LANG = en_US.UTF-8
    ```
    {: codeblock}
    
    Apri una nuova finestra di terminale ed esegui il seguente comando per verificare che le variabili LANG e LOGGING_ENDPOINT siano configurate:
    
    ```
    $echo LANG
    en_US.UTF-8
    ```
    {: screen}   
    
3. Verifica l'installazione del plugin della CLI di registrazione.
  
    Ad esempio, verifica la versione del plugin. Esegui il seguente comando:
    
    ```
    cf logging --version
    ```
    {: codeblock}
    
    L'output sarà simile al seguente:
   
    ```
    cf logging version 0.3.5
    ```
    {: screen}


## Installazione della CLI di raccolta dei log su Windows
{: #install_cli_windows}

Completa la seguente procedura per installare il plugin CF di raccolta dei log su Windows:

1. Scarica la versione più recente del plugin della CLI del servizio {{site.data.keyword.loganalysisshort}} (IBM-Logging) dalla [pagina della CLI Bluemix](https://clis.ng.bluemix.net/ui/repository.html#cf-plugins). 
	
	1. Seleziona il valore della piattaforma: **win64**. 
	2. Fai clic su **Salva file**.  
    
2. Esegui il comando **cf install-plugin** per installare il plugin di raccolta dei log su Windows. 

    ```
	cf install-plugin NomePlugin
	```
	{: codeblock}
	
	dove *NomePlugin* è il nome del file che hai scaricato.
	
    Ad esempio, per installare il plugin *logging-cli-win64_v1.0.1.exe*, esegui il seguente comando da una finestra di terminale:
	
	```
	cf install-plugin logging-cli-win64_v1.0.1.exe
	```
	{: codeblock}
	
    Quando il plugin è installato, ottieni il seguente messaggio: `Il plugin IBM-Logging 1.0.1 è stato installato correttamente.`

3. Verifica l'installazione del plugin della CLI di registrazione.

    Ad esempio, verifica la versione del plugin. Esegui il seguente comando:
    
    ```
    cf logging --version
    ```
    {: codeblock}
    
    L'output sarà simile al seguente:
   
    ```
    cf logging version 1.0.1
    ```
    {: screen}
	

## Installazione della CLI di raccolta dei log su Mac OS X
{: #install_cli_mac}

Completa la seguente procedura per installare il plugin CF di raccolta dei log su Mac OS X:

1. Scarica la versione più recente del plugin della CLI del servizio {{site.data.keyword.loganalysisshort}} (IBM-Logging) da [pagina della CLI Bluemix](https://clis.ng.bluemix.net/ui/repository.html#cf-plugins).
	
	1. Seleziona il valore della piattaforma: **osx**.
	2. Fai clic su **Salva file**.

2. Esegui il comando **cf install-plugin** per installare il plugin di raccolta dei log su Mac OS X.

    ```
	cf install-plugin NomePlugin
	```
	{: codeblock}
	
	dove *NomePlugin* è il nome del file che hai scaricato.
	
    Ad esempio, per installare il plugin *logging-cli-darwin_v1.0.1*, esegui il seguente comando da un terminale:
	
	```
	cf install-plugin logging-cli-darwin_v1.0.1
	```
	{: codeblock}
	
    Quando il plugin è installato, ottieni il seguente messaggio: `Il plugin IBM-Logging 1.0.1 è stato installato correttamente.`

3. Verifica l'installazione del plugin della CLI di registrazione.

    Ad esempio, verifica la versione del plugin. Esegui il seguente comando:
    
    ```
    cf logging --version
    ```
    {: codeblock}
    
    L'output sarà simile al seguente:
   
    ```
    cf logging version 1.0.1
    ```
    {: screen}
	
	
## Disinstallazione della CLI di raccolta dei log
{: #uninstall_cli}

Per disinstallare la CLI di registrazione, elimina il plugin.
{:shortdesc}

Completa la seguente procedura per disinstallare la CLI del servizio {{site.data.keyword.loganalysisshort}}:

1. Verifica la versione del plugin della CLI di registrazione installato.

    Ad esempio, verifica la versione del plugin. Esegui il seguente comando:
    
    ```
    cf plugins
    ```
    {: codeblock}
    
    L'output sarà simile al seguente:
   
    ```
    Listing Installed Plugins...
    OK

    Plugin Name   Version   Command Name   Command Help
    IBM-Logging   1.0.1     logging        IBM Logging plug-in
    ```
    {: screen}
    
2. Se il plugin è installato, esegui `cf uninstall-plugin` per disinstallare il plugin della CLI di registrazione.

    Esegui il seguente comando:
        
    ```
    cf uninstall-plugin IBM-Logging
    ```
    {: codeblock}
  

## Ottenimento della guida generale
{: #general_cli_help}

Per ottenere le informazioni generali sulla CLI e su quali comandi sono supportati, completa la seguente procedura:

1. Accedi a una regione, organizzazione e spazio {{site.data.keyword.Bluemix_notm}}. 

    Ad esempio, per accedere alla regione Stati Uniti Sud, esegui questo comando:
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Per elencare le informazioni sui comandi supportati e sulla CLI. Esegui il seguente comando:

    ```
    cf logging help
    ```
    {: codeblock}
    
    

## Come ottenere supporto per un comando
{: #command_cli_help}

Per ottenere supporto sull'utilizzo di un comando, completa la seguente procedura:

1. Accedi a una regione, organizzazione e spazio {{site.data.keyword.Bluemix_notm}}. 

    Ad esempio, per accedere alla regione Stati Uniti Sud, esegui questo comando:
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Per ottenere l'elenco dei comandi supportati e identificare il comando di cui hai bisogno. Esegui il comando:

    ```
    cf logging help
    ```
    {: codeblock}

3. Per ottenere supporto sul comando. Esegui il seguente comando:

    ```
    cf logging help *Command*
    ```
    {: codeblock}
    
    dove *Command* è il nome di un comando della CLI, ad esempio, *status*.



## Come ottenere supporto per un comando secondario
{: #subcommand_cli_help}

Un comando può avere comandi secondari. Per ottenere supporto sui comandi secondari, completa la seguente procedura:

1. Accedi a una regione, organizzazione e spazio {{site.data.keyword.Bluemix_notm}}. 

    Ad esempio, per accedere alla regione Stati Uniti Sud, esegui questo comando:
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Per ottenere l'elenco dei comandi supportati e identificare il comando di cui hai bisogno. Esegui il comando:

    ```
    cf logging help
    ```
    {: codeblock}

3. Per ottenere supporto sul comando e identificare i comandi secondari supportati. Esegui il seguente comando:

    ```
    cf logging help *Command*
    ```
    {: codeblock}
    
    dove *Command* è il nome di un comando della CLI, ad esempio, *session*.

4. Per ottenere supporto sul comando e identificare i comandi secondari supportati. Esegui il seguente comando:

    ```
    cf logging *Command* help *Subcommand*
    ```
    {: codeblock}
    
    dove 
    
    * *Command* è il nome di un comando della CLI, ad esempio, *status*.
    * *Subcommand* è il nome del comando secondario supportato, ad esempio, per il comando *session*, un comando secondario valido è *list*.




