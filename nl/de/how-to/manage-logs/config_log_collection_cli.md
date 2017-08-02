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

# Befehlszeilenschnittstelle für 'Log Collection' konfigurieren
{: #config_log_collection_cli}

Der {{site.data.keyword.loganalysisshort}}-Service beinhaltet eine Befehlszeilenschnittstelle (CLI), die Sie zur Verwaltung Ihrer Protokolle in der Cloud verwenden können. Die Befehlszeilenschnittstelle ist ein Cloud Foundry-Plug-in. Sie können Befehle verwenden, um den Status des Protokolls anzuzeigen, um Protokolle herunterzuladen und um die Protokollaufbewahrungsrichtlinie zu konfigurieren. Die Befehlszeilenschnittstelle bietet verschiedene Arten von Hilfe: erweiterte Hilfe zu den CLI- und unterstützten Befehlen sowie Hilfe zur Verwendung von Befehlen und Unterbefehlen.
{:shortdesc}


## Befehlszeilenschnittstelle für 'Log Collection' installieren
{: #install_cli}

Führen Sie die folgenden Schritte aus, um die Befehlszeilenschnittstelle für 'Log Collection' zu installieren: 

1. Überprüfen Sie, ob die CF-Befehlszeilenschnittstelle auf Ihrem System verfügbar ist.  

    Weitere Informationen finden Sie unter [Voraussetzungen](/docs/services/CloudLogAnalysis/how-to/manage-logs/config_log_collection_cli.html#pre_req). 

2. Installieren Sie das CF-Plug-in für 'Log Collection': 

    * Die Schritte für Linux finden Sie unter [Befehlszeilenschnittstelle von 'Log Collection' unter Linux installieren](/docs/services/CloudLogAnalysis/how-to/manage-logs/config_log_collection_cli.html#install_cli_linux). 
    * Die Schritte für Windows finden Sie unter [Befehlszeilenschnittstelle von 'Log Collection' unter Windows installieren](/docs/services/CloudLogAnalysis/how-to/manage-logs/config_log_collection_cli.html#install_cli_windows). 
    * Die Schritte für Mac OS X finden Sie unter [Befehlszeilenschnittstelle von 'Log Collection' unter Mac OS X installieren](/docs/services/CloudLogAnalysis/how-to/manage-logs/config_log_collection_cli.html#install_cli_mac). 
 

## Voraussetzungen
{: #pre_req}

Die Befehlszeilenschnittstelle für 'Log Collection' ist ein CF-Plug-in. Berücksichtigen Sie vor der Installation die folgenden Szenarios: 

* Sie installieren die CF-Befehlszeilenschnittstelle zum ersten Mal: 

     Installieren Sie das CF-Plug-in. Weitere Informationen finden Sie unter [CF-Befehlszeilenschnittstelle installieren ![Symbol für externen Link](../../../../icons/launch-glyph.svg "Symbol für externen Link")](http://docs.cloudfoundry.org/cf-cli/install-go-cli.html "Symbol für externen Link"){: new_window}.  

* Sie haben das Paket für die {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle installiert: 

    Die CF-Befehlszeilenschnittstelle wird als Bundle mit dem Paket der {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle bereitgestellt. 

* Von der {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle sollen weitere Cloudressourcen verwaltet werden:   

    Installieren Sie das Paket mit der {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle; Informationen hierzu finden Sie unter [{{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle installieren](/docs/cli/reference/bluemix_cli/index.html#install_bluemix_cli). 

Stellen Sie sicher, dass das CF-Plug-in verfügbar ist. Führen Sie den folgenden Befehl in einer Sitzung auf Ihrem System aus: 
    
```
cf -v
```
{: codeblock}
    
Die Ausgabe sieht wie folgt aus:
    
```
cf version 6.25.0+787326d.2017-02-28
```
{: screen}

**Hinweis:** Sie können die Befehle der {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle nicht kombiniert verwenden; dies bedeutet, `bx`-Befehle und CF-CLI-Befehle, also `cf`-Befehle. 



	
## Befehlszeilenschnittstelle für 'Log Collection' unter Linux installieren
{: #install_cli_linux}

Führen Sie die folgenden Schritte aus, um das CF-Plug-in für 'Log Collection' unter Linux zu installieren: 

1. Installieren Sie das CLI-Plug-in für 'Log Collection'. 

    1. Laden Sie die aktuelle Version des CLI-Plug-ins für den {{site.data.keyword.loganalysisshort}}-Service (IBM-Logging) von der [Bluemix-CLI-Seite](https://clis.ng.bluemix.net/ui/repository.html#cf-plugins) herunter.  
	
		Wählen Sie den Wert für die Plattform aus: **linux64**.	Klicken Sie auf die Schaltfläche zum Speichern der Datei (**Save file**).  
    
    2. Dekomprimieren Sie das Plug-in.
    
        Beispiel: Um das Plug-in `logging-cli-linux64.gz` in Ubuntu zu dekomprimieren, führen Sie den folgenden Befehl aus:
        
        ```
        gunzip logging-cli-linux64.gz
        ```
        {: codeblock}

    3. Machen Sie die Datei zu einer ausführbaren Datei.
    
        Beispiel: Um die Datei `logging-cli-linux64` in eine ausführbare Datei umzuwandeln, führen Sie den folgenden Befehl aus:
        
        ```
        chmod a+x logging-cli-linux64
        ```
        {: codeblock}

    4. Installieren Sie das CF-Plug-in für die Protokollierung.
    
        Beispiel: Um die Datei `logging-cli-linux64` in eine ausführbare Datei umzuwandeln, führen Sie den folgenden Befehl aus:
        
        ```
        cf install-plugin -f logging-cli-linux64
        ```
        {: codeblock}

2. Legen Sie einen Wert für die Umgebungsvariable **LANG** fest. 

    Geben Sie für *LANG* den Standardwert an: *en_US.UTF-8*, wenn die Ländereinstellung Ihres Systems nicht von CF unterstützt wird. Weitere Informationen zu den von CF unterstützten Ländereinstellungen finden Sie unter [Einführung in die CF-Befehlszeilenschnittstelle ![Symbol für externen Link](../../../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.cloudfoundry.org/cf-cli/getting-started.html "Symbol für externen Link"){: new_window}.
	
	Beispiel: Bearbeiten Sie in einem Ubuntu-System die Datei *~/.bashrc* und fügen Sie die folgenden Zeilen ein:
    
    ```
    # add entry for logging CLI
    export LANG = en_US.UTF-8
    ```
    {: codeblock}
    
    Öffnen Sie ein neues Terminalfenster und führen Sie den folgenden Befehl aus, um zu überprüfen, ob die Variablen LANG und LOGGING_ENDPOINT festgelegt wurden:
    
    ```
    $echo LANG
    en_US.UTF-8
    ```
    {: screen}   
    
3. Überprüfen Sie die Installation des CLI-Plug-ins für die Protokollierung.
  
    Überprüfen Sie beispielsweise die Version des Plug-ins. Führen Sie den folgenden Befehl aus:
    
    ```
    cf logging --version
    ```
    {: codeblock}
    
    Die Ausgabe sieht wie folgt aus:
   
    ```
    cf logging version 0.3.5
    ```
    {: screen}


## Befehlszeilenschnittstelle für 'Log Collection' unter Windows installieren
{: #install_cli_windows}

Führen Sie die folgenden Schritte aus, um das CF-Plug-in für 'Log Collection' unter Windows zu installieren: 

1. Laden Sie die aktuelle Version des CLI-Plug-ins für den {{site.data.keyword.loganalysisshort}}-Service (IBM-Logging) von der [Bluemix-CLI-Seite](https://clis.ng.bluemix.net/ui/repository.html#cf-plugins) herunter.  
	
	1. Wählen Sie den Wert für die Plattform aus: **win64**.	 
	2. Klicken Sie auf die Schaltfläche zum Speichern der Datei (**Save file**).   
    
2. Führen Sie den Befehl **cf install-plugin** aus, um das Plug-in für 'Log Collection' unter Windows zu installieren.  

    ```
	cf install-plugin PluginName
	```
	{: codeblock}
	
	Hierbei steht *PluginName* für den Namen der Datei, die Sie heruntergeladen haben.
	
    Beispiel: Zum Installieren des Plug-ins *logging-cli-win64_v1.0.1.exe* führen Sie den folgenden Befehl in einem Terminalfenster aus:
	
	```
	cf install-plugin logging-cli-win64_v1.0.1.exe
	```
	{: codeblock}
	
    Wenn das Plug-in installiert ist, wird folgende Nachricht angezeigt: 'Plugin IBM-Logging 1.0.1 successfully installed.' `

3.  Überprüfen Sie die Installation des CLI-Plug-ins für die Protokollierung.

    Überprüfen Sie beispielsweise die Version des Plug-ins. Führen Sie den folgenden Befehl aus:
    
    ```
    cf logging --version
    ```
    {: codeblock}
    
    Die Ausgabe sieht wie folgt aus:
   
    ```
    cf logging version 1.0.1
    ```
    {: screen}
	

## CLI für 'Log Collection' unter Mac OS X installieren
{: #install_cli_mac}

Führen Sie die folgenden Schritte aus, um das CF-Plug-in für 'Log Collection' unter Mac OS X zu installieren:

1. Laden Sie die neueste Version des Plug-ins für den {{site.data.keyword.loganalysisshort}}-Service (IBM-Logging) von der [Bluemix-CLI-Seite] (https://clis.ng.bluemix.net/ui/repository.html#cf-plugins) herunter.
	
	1. Wählen Sie den Wert für die Plattform aus: **osx**.
	2. Klicken Sie auf die Schaltfläche zum Speichern der Datei (**Save file**).

2. Führen Sie den Befehl **cf install-plugin** aus, um das Plug-in für 'Log Collection' unter Mac OS X zu installieren.

    ```
	cf install-plugin PluginName
	```
	{: codeblock}
	
	Hierbei steht *PluginName* für den Namen der Datei, die Sie heruntergeladen haben.
	
    Beispiel: Zum Installieren des Plug-ins *logging-cli-darwin_v1.0.1.exe* führen Sie den folgenden Befehl in einem Terminalfenster aus:
	
	```
	cf install-plugin logging-cli-darwin_v1.0.1
	```
	{: codeblock}
	
    Wenn das Plug-in installiert ist, wird folgende Nachricht angezeigt: 'Plugin IBM-Logging 1.0.1 successfully installed.' `

3.  Überprüfen Sie die Installation des CLI-Plug-ins für die Protokollierung.

    Überprüfen Sie beispielsweise die Version des Plug-ins. Führen Sie den folgenden Befehl aus:
    
    ```
    cf logging --version
    ```
    {: codeblock}
    
    Die Ausgabe sieht wie folgt aus:
   
    ```
    cf logging version 1.0.1
    ```
    {: screen}
	
	
## Befehlszeilenschnittstelle für 'Log Collection' deinstallieren
{: #uninstall_cli}

Löschen Sie zum Deinstallieren der Befehlszeilenschnittstelle für die Protokollierung das Plug-in.
{:shortdesc}

Führen Sie die folgenden Schritte aus, um die {{site.data.keyword.loganalysisshort}}-Service-CLI zu deinstallieren:

1. Überprüfen Sie die Version des installierten CLI-Plug-ins für die Protokollierung.

    Überprüfen Sie beispielsweise die Version des Plug-ins. Führen Sie den folgenden Befehl aus:
    
    ```
    cf plugins
    ```
    {: codeblock}
    
    Die Ausgabe sieht wie folgt aus:
   
    ```
    Listing Installed Plugins...
    OK

    Plugin Name   Version   Command Name   Command Help
    IBM-Logging   1.0.1     logging        IBM Logging plug-in
    
    ```
    {: screen}
    
2. Wenn das Plug-in installiert ist, führen Sie den Befehl `cf uninstall-plugin` aus, um das Plug-in für die Protokollierung zu deinstallieren.

    Führen Sie den folgenden Befehl aus:
        
    ```
    cf uninstall-plugin IBM-Logging
    ```
    {: codeblock}
  

## Erweiterte Hilfe erhalten
{: #general_cli_help}

Führen Sie die folgenden Schritte aus, um allgemeine Informationen zur Befehlszeilenschnittstelle und den unterstützten Befehlen zu erhalten:

1. Melden Sie sich unter {{site.data.keyword.Bluemix_notm}} an einer Region, einer Organisation und einem Bereich an. 

    Führen Sie zum Beispiel den folgenden Befehl aus, um sich an der Region 'USA (Süden)' anzumelden:
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Listen Sie Informationen zu den unterstützten Befehlen und zur Befehlszeilenschnittstelle auf. Führen Sie den folgenden Befehl aus:

    ```
    cf logging help 
    ```
    {: codeblock}
    
    

## Hilfe zu einem Befehl abrufen
{: #command_cli_help}

Gehen Sie wie folgt vor, um Hilfe zur Verwendung eines Befehls abzurufen:

1. Melden Sie sich unter {{site.data.keyword.Bluemix_notm}} an einer Region, einer Organisation und einem Bereich an. 

    Führen Sie zum Beispiel den folgenden Befehl aus, um sich an der Region 'USA (Süden)' anzumelden:

	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Rufen Sie die Liste der unterstützten Befehle auf und suchen Sie nach dem gewünschten Befehl. Führen Sie den folgenden Befehl aus:

    ```
    cf logging help 
    ```
    {: codeblock}

3. Rufen Sie Hilfeinformationen zu dem Befehl ab. Führen Sie den folgenden Befehl aus:

    ```
    cf logging help *Befehl*
    ```
    {: codeblock}
    
    Dabei ist *Befehl* der Name eines CLI-Befehls, z. B. *status*.



## Hilfe zu einem Unterbefehl abrufen
{: #subcommand_cli_help}

Ein Befehl kann Unterbefehle haben. Gehen Sie wie folgt vor, um Hilfe zu Unterbefehlen abzurufen:

1. Melden Sie sich unter {{site.data.keyword.Bluemix_notm}} an einer Region, einer Organisation und einem Bereich an. 

    Führen Sie zum Beispiel den folgenden Befehl aus, um sich an der Region 'USA (Süden)' anzumelden: 
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Rufen Sie die Liste der unterstützten Befehle auf und suchen Sie nach dem gewünschten Befehl. Führen Sie den folgenden Befehl aus:

    ```
    cf logging help 
    ```
    {: codeblock}

3. Rufen Sie Hilfeinformationen zu dem Befehl ab und ermitteln Sie die unterstützten Unterbefehle. Führen Sie den folgenden Befehl aus:

    ```
    cf logging help *Befehl*
    ```
    {: codeblock}
    
    Dabei ist *Befehl* der Name eines CLI-Befehls, z. B. *session*.

4. Rufen Sie Hilfeinformationen zu dem Befehl ab und ermitteln Sie die unterstützten Unterbefehle. Führen Sie den folgenden Befehl aus:

    ```
    cf logging *Befehl* help *Unterbefehl*
    ```
    {: codeblock}
    
    Dabei gilt: 
    
    * *Befehl* ist der Name eines CLI-Befehls, z. B. *status*.
    * *Unterbefehl* ist der Name eines unterstützten Unterbefehls; z. B. ist *list* ein gültiger Unterbefehl für den Befehl *session*.




