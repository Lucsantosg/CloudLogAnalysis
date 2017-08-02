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

# Configuración de la CLI del componente de recopilación de registros
{: #config_log_collection_cli}

El servicio {{site.data.keyword.loganalysisshort}} incluye una interfaz de línea de mandatos (CLI) que puede utilizar para gestionar los registros en la nube. La CLI es un plugin de Cloud Foundry (CF). Puede utilizar mandatos para ver el estado del registro, para descargar registros y para configurar la política de retención de registros. La CLI ofrece distintos tipos de ayuda: ayuda general para obtener información sobre la CLI y los mandatos soportados, ayuda sobre mandatos para ver cómo se utiliza un mandato o ayuda sobre submandatos para aprender a utilizar un submandato de un mandato.
{:shortdesc}


## Instalación de la CLI de recopilación de registros
{: #install_cli}

Para instalar la CLI de recopilación de registros, siga estos pasos:

1. Compruebe que la CLI CF está disponible en el sistema. 

    Para obtener más información, consulte [Requisitos previos](/docs/services/CloudLogAnalysis/how-to/manage-logs/config_log_collection_cli.html#pre_req).

2. Instale el plugin de CF de recopilación de registros:

    * Para Linux, consulte [Instalación de la CLI de recopilación de registros en Linux](/docs/services/CloudLogAnalysis/how-to/manage-logs/config_log_collection_cli.html#install_cli_linux).
    * Para Windows, consulte [Instalación de la CLI de recopilación de registros en Windows](/docs/services/CloudLogAnalysis/how-to/manage-logs/config_log_collection_cli.html#install_cli_windows).
    * Para Mac OS X, consulte [Instalación de la CLI de recopilación de registros en Mac OS X](/docs/services/CloudLogAnalysis/how-to/manage-logs/config_log_collection_cli.html#install_cli_mac).
 

## Requisito previo
{: #pre_req}

La CLI de recopilación de registros es un plugin de CF. Antes de instalarlo, tenga en cuenta los casos de ejemplo siguientes:

* Va a instalar la CLI de CF por primera vez:

     Instale el plugin de CF. Para obtener más información, consulte [Instalación de la CLI de cf ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](http://docs.cloudfoundry.org/cf-cli/install-go-cli.html "Icono de enlace externo"){: new_window}. 

* Tiene el paquete de la CLI de {{site.data.keyword.Bluemix_notm}} instalado:

    La CLI de CF está empaquetada en el paquete de la CLI de {{site.data.keyword.Bluemix_notm}}.

* Va a necesitar la CLI de {{site.data.keyword.Bluemix_notm}} para gestionar otros recursos de nube:  

    Instale el paquete de la CLI de {{site.data.keyword.Bluemix_notm}}, consulte [Instalación de la CLI de {{site.data.keyword.Bluemix_notm}}](/docs/cli/reference/bluemix_cli/index.html#install_bluemix_cli).

A continuación, verifique que el plugin de CF está disponible. Ejecute el siguiente mandato desde una sesión en el sistema:
    
```
cf -v
```
{: codeblock}
    
La salida tiene el aspecto siguiente:
    
```
cf version 6.25.0+787326d.2017-02-28
```
{: screen}

**Nota:** no puede mezclar mandatos de CLI de {{site.data.keyword.Bluemix_notm}}, es decir, mandatos `bx` y mandatos de CLI de CF, es decir mandatos de `cf`.



	
## Instalación de la CLI de recopilación de registros en Linux
{: #install_cli_linux}

Siga estos pasos para instalar el plugin de CF de recopilación de registros en Linux:

1. Instale el plugin de la CLI de recopilación de registros.

    1. Descargue el último release del plugin de la CLI del servicio {{site.data.keyword.loganalysisshort}} (IBM-Logging) de [la página de la CLI de Bluemix](https://clis.ng.bluemix.net/ui/repository.html#cf-plugins). 
	
		Seleccione el valor de plataforma: **linux64**.
		Pulse **Guardar archivo**. 
    
    2. Descomprima el plugin.
    
        Por ejemplo, para descomprimir el plugin `logging-cli-linux64.gz` en Ubuntu, ejecute el siguiente mandato:
        
        ```
        gunzip logging-cli-linux64.gz
        ```
        {: codeblock}

    3. Convierta el archivo en ejecutable.
    
        Por ejemplo, para convertir el archivo `logging-cli-linux64` en ejecutable, ejecute el siguiente mandato:
        
        ```
        chmod a+x logging-cli-linux64
        ```
        {: codeblock}

    4. Instale el plugin de CF de registro.
    
        Por ejemplo, para convertir el archivo `logging-cli-linux64` en ejecutable, ejecute el siguiente mandato:
        
        ```
        cf install-plugin -f logging-cli-linux64
        ```
        {: codeblock}

2. Defina la variable de entorno **LANG**.

    Establezca *LANG* en el valor predeterminado: *en_US.UTF-8* si el entorno local del sistema no recibe soporte de CF. Para obtener información sobre los entornos locales soportados de CF, consulte [Iniciación a la CLI de cf![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.cloudfoundry.org/cf-cli/getting-started.html "Icono de enlace externo"){: new_window}
	
	Por ejemplo, en un sistema Ubuntu, edite el archivo *~/.bashrc* y especifique las siguientes líneas:
    
    ```
    # add entry for logging CLI
    export LANG = en_US.UTF-8
    ```
    {: codeblock}
    
    Abra una nueva ventana de terminal y ejecute el mandato siguiente para verificar que las variables LANG y LOGGING_ENDPOINT estén establecidas:
    
    ```
    $echo LANG
    en_US.UTF-8
    ```
    {: screen}   
    
3. Verifique la instalación del plugin de la CLI de registro.
  
    Por ejemplo, compruebe la versión del plugin. Ejecute el mandato siguiente:
    
    ```
    cf logging --version
    ```
    {: codeblock}
    
    La salida tiene el aspecto siguiente:
   
    ```
    cf logging version 0.3.5
    ```
    {: screen}


## Instalación de la CLI de recopilación de registros en Windows
{: #install_cli_windows}

Siga estos pasos para instalar el plugin de CF de recopilación de registros en Windows:

1. Descargue el último release del plugin de la CLI del servicio {{site.data.keyword.loganalysisshort}} (IBM-Logging) de [la página de la CLI de Bluemix](https://clis.ng.bluemix.net/ui/repository.html#cf-plugins). 
	
	1. Seleccione el valor de plataforma: **win64**. 
	2. Pulse **Guardar archivo**.  
    
2. Ejecute el mandato **cf install-plugin** para instalar el plugin de recopilación de registros en Windows. 

    ```
	cf install-plugin PluginName
	```
	{: codeblock}
	
	donde *PluginName* es el nombre del archivo que ha descargado.
	
    Por ejemplo, para instalar el plugin *logging-cli-win64_v1.0.1.exe*, ejecute el mandato siguiente desde una ventana de terminal: 	
	```
	cf install-plugin logging-cli-win64_v1.0.1.exe
	```
	{: codeblock}
	
    Cuando el plugin esté instalado, recibirá el mensaje siguiente: `El plugin IBM-Logging 1.0.1 se ha instalado correctamente.`

3. Verifique la instalación del plugin de la CLI de registro.

    Por ejemplo, compruebe la versión del plugin. Ejecute el mandato siguiente:
    
    ```
    cf logging --version
    ```
    {: codeblock}
    
    La salida tiene el aspecto siguiente:
   
    ```
    cf logging version 1.0.1
    ```
    {: screen}
	

## Instalación de la CLI de recopilación de registros en Mac OS X
{: #install_cli_mac}

Siga estos pasos para instalar el plugin de CF de recopilación de registros en Mac OS X:

1. Descargue el último release del plugin de la CLI del servicio {{site.data.keyword.loganalysisshort}} (IBM-Logging) de [la página de la CLI de Bluemix](https://clis.ng.bluemix.net/ui/repository.html#cf-plugins).
	
	1. Seleccione el valor de plataforma: **osx**.
	2. Pulse **Guardar archivo**.

2. Ejecute el mandato **cf install-plugin** para instalar el plugin de recopilación de registros en Mac OS X.
    ```
	cf install-plugin PluginName
	```
	{: codeblock}
	
	donde *PluginName* es el nombre del archivo que ha descargado.
	
    Por ejemplo, para instalar el plugin *logging-cli-darwin_v1.0.1*, ejecute el mandato siguiente desde un terminal:
	
	```
	cf install-plugin logging-cli-darwin_v1.0.1
	```
	{: codeblock}
	
    Cuando el plugin esté instalado, recibirá el mensaje siguiente: `El plugin IBM-Logging 1.0.1 se ha instalado correctamente.`

3. Verifique la instalación del plugin de la CLI de registro.

    Por ejemplo, compruebe la versión del plugin. Ejecute el mandato siguiente:
    
    ```
    cf logging --version
    ```
    {: codeblock}
    
    La salida tiene el aspecto siguiente:
   
    ```
    cf logging version 1.0.1
    ```
    {: screen}
	
	
## Desinstalación de la CLI de recopilación de registros
{: #uninstall_cli}

Para desinstalar la CLI de registro, suprima el plugin.
{:shortdesc}

Siga estos pasos para desinstalar la CLI del servicio {{site.data.keyword.loganalysisshort}}:

1. Verifique la versión del plugin de la CLI de registro que se ha instalado.

    Por ejemplo, compruebe la versión del plugin. Ejecute el mandato siguiente:
    
    ```
    cf plugins
    ```
    {: codeblock}
    
    La salida tiene el aspecto siguiente:
   
    ```
    Listing Installed Plugins...
    OK

    Plugin Name   Version   Command Name   Command Help
    IBM-Logging   1.0.1     logging        IBM Logging plug-in
    ```
    {: screen}
    
2. Si el plugin está instalado, ejecute `cf uninstall-plugin` para desinstalar el plugin de la CLI de registro.

    Ejecute el mandato siguiente:
        
    ```
    cf uninstall-plugin IBM-Logging
    ```
    {: codeblock}
  

## Obtención de ayuda general
{: #general_cli_help}

Para obtener información general sobre la CLI y los mandatos soportados, siga estos pasos:

1. Inicie la sesión en una región, organización o espacio de {{site.data.keyword.Bluemix_notm}}. 

    Por ejemplo, para iniciar sesión en la región EE. UU. sur, ejecute el siguiente mandato:
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Obtenga información sobre los mandatos soportados y sobre la CLI. Ejecute el mandato siguiente:

    ```
    cf logging help 
    ```
    {: codeblock}
    
    

## Obtención de ayuda sobre un mandato
{: #command_cli_help}

Para obtener ayuda sobre cómo utilizar un mandato, siga los pasos siguientes:

1. Inicie la sesión en una región, organización y espacio de {{site.data.keyword.Bluemix_notm}}. 

    Por ejemplo, para iniciar sesión en la región EE. UU. sur, ejecute el siguiente mandato:
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Obtenga la lista de mandatos soportados e identifique el que necesita. Ejecute el mandato:

    ```
    cf logging help 
    ```
    {: codeblock}

3. Obtenga ayuda sobre el mandato. Ejecute el mandato siguiente:

    ```
    cf logging help *Mandato*
    ```
    {: codeblock}
    
    donde *Mandato* es el nombre de un mandato de la CLI, como por ejemplo *status*.



## Obtención de ayuda sobre un submandato
{: #subcommand_cli_help}

Un mandato puede tener submandatos. Para obtener ayuda sobre los submandatos, siga los pasos siguientes:

1. Inicie la sesión en una región, organización y espacio de {{site.data.keyword.Bluemix_notm}}. 

    Por ejemplo, para iniciar sesión en la región EE. UU. sur, ejecute el siguiente mandato:
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Obtenga la lista de mandatos soportados e identifique el que necesita. Ejecute el mandato:

    ```
    cf logging help 
    ```
    {: codeblock}

3. Obtenga ayuda sobre el mandato e identifique los submandatos soportados. Ejecute el mandato siguiente:

    ```
    cf logging help *Mandato*
    ```
    {: codeblock}
    
    donde *Mandato* es el nombre de un mandato de la CLI, como por ejemplo *session*.

4. Obtenga ayuda sobre el mandato e identifique los submandatos soportados. Ejecute el mandato siguiente:

    ```
    cf logging *Mandato* help *Submandato*
    ```
    {: codeblock}
    
    donde 
    
    * *Mandato* es el nombre de un mandato de la CLI, como por ejemplo *status*.
    * *Submandato* es el nombre de un submandato soportado, como por ejemplo, para el mandato *session*, un submandato válido es *list*.




