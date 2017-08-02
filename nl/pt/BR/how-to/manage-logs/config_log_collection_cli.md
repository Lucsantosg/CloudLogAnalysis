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

# Configurando a CLI de coleta de log
{: #config_log_collection_cli}

O serviço {{site.data.keyword.loganalysisshort}} inclui uma interface da linha de comandos (CLI) que pode ser usada para gerenciar os logs na nuvem. A CLI é um plug-in Cloud Foundry (CF). É possível usar comandos para visualizar o status do log, fazer download de logs e configurar a política de retenção de log. A CLI oferece diferentes tipos de ajuda: ajuda geral para aprender sobre a CLI e os comandos suportados, ajuda de comando para aprender como usar um comando ou ajuda de subcomando para aprender como usar um subcomando para um comando.
{:shortdesc}


## Instalando a CLI de Coleta de Log
{: #install_cli}

Para instalar a CLI de Coleção de logs, conclua as etapas a seguir:

1. Verifique se o CF CLI está disponível no sistema. 

    Para obter mais informações, veja [Pré-requisito](/docs/services/CloudLogAnalysis/how-to/manage-logs/config_log_collection_cli.html#pre_req).

2. Instale o plug-in CF da Coleção de logs:

    * Para Linux, veja [Instalando a CLI de Coleção de logs no Linux](/docs/services/CloudLogAnalysis/how-to/manage-logs/config_log_collection_cli.html#install_cli_linux).
    * Para Windows, veja [Instalando a CLI de Coleção de logs no Windows](/docs/services/CloudLogAnalysis/how-to/manage-logs/config_log_collection_cli.html#install_cli_windows).
    * Para Mac OS X, veja [Instalando a CLI de Coleção de logs no Mac OS X](/docs/services/CloudLogAnalysis/how-to/manage-logs/config_log_collection_cli.html#install_cli_mac).
 

## Pré-requisito
{: #pre_req}

A CLI de Coleção de logs é um plug-in CF. Antes de instalá-la, considere os cenários a seguir:

* Você está instalando o CF CLI pela primeira vez:

     Instale o plug-in CF. Para obter mais informações, veja [Instalando o cf CLI ![Ícone de link externo](../../../../icons/launch-glyph.svg "Ícone de link externo")](http://docs.cloudfoundry.org/cf-cli/install-go-cli.html "Ícone de link externo"){: new_window}. 

* Você tem o pacote CLI do {{site.data.keyword.Bluemix_notm}} instalado:

    O CF CLI vem empacotado no pacote CLI do {{site.data.keyword.Bluemix_notm}}.

* A CLI do {{site.data.keyword.Bluemix_notm}} será necessária para gerenciar outros recursos em nuvem:  

    Instale o pacote CLI do {{site.data.keyword.Bluemix_notm}}, veja [Instalando a CLI do {{site.data.keyword.Bluemix_notm}}](/docs/cli/reference/bluemix_cli/index.html#install_bluemix_cli).

Em seguida, verifique se o plug-in CF está disponível. Execute o comando a seguir em uma sessão do sistema:
    
```
cf -v
```
{: codeblock}
    
A saída é semelhante ao seguinte:
    
```
Cf version 6.25.0+787326d.2017-02-28
```
{: screen}

**Nota:** não é possível combinar comandos da CLI do {{site.data.keyword.Bluemix_notm}}, isto é, comandos `bx`, nem os comandos do CF CLI, isto é, comandos `cf`.



	
## Instalando a CLI de Coleção de logs no Linux
{: #install_cli_linux}

Conclua as etapas a seguir para instalar o plug-in CF da Coleção de logs no Linux:

1. Instale o plug-in da CLI da Coleção de logs.

    1. Faça download da liberação mais recente do plug-in da CLI do serviço {{site.data.keyword.loganalysisshort}} (IBM-Logging) da [página CLI do Bluemix](https://clis.ng.bluemix.net/ui/repository.html#cf-plugins). 
	
		Selecione o valor de plataforma: **linux64**.
		Clique em **Salvar arquivo**. 
    
    2. Descompacte o plug-in.
    
        Por exemplo, para descompactar o arquivo ZIP do plug-in `logging-cli-linux64.gz` no Ubuntu, execute o comando a seguir:
        
        ```
        Gunzip log-cli-linux64.gz
        ```
        {: codeblock}

    3. Torne o arquivo executável.
    
        Por exemplo, para tornar o arquivo `logging-cli-linux64` executável, execute o comando a seguir:
        
        ```
        Chmod a + x log-cli-linux64
        ```
        {: codeblock}

    4. Instale o plug-in CF de log.
    
        Por exemplo, para tornar o arquivo `logging-cli-linux64` executável, execute o comando a seguir:
        
        ```
        Cf install-plugin -f log-cli-linux64
        ```
        {: codeblock}

2. Configure a variável de ambiente **LANG**.

    Configure *LANG* para o valor padrão: *en_US.UTF-8* se o código de idioma do sistema não for suportado por CF. Para obter informações sobre códigos de idioma CF suportados, veja [Introdução à CLI do cf ![Ícone de link externo](../../../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.cloudfoundry.org/cf-cli/getting-started.html "Ícone de link externo"){: new_window}
	
	Por exemplo, em um sistema Ubuntu, edite o arquivo *~/.bashrc* e insira as linhas a seguir:
    
    ```
    # add entry for logging CLI
    export LANG = en_US.UTF-8
    ```
    {: codeblock}
    
    Abra uma nova janela do terminal e execute o comando a seguir para verificar se as variáveis LANG e LOGGING_ENDPOINT estão configuradas:
    
    ```
    $echo LANG
    en_US.UTF-8
    ```
    {: screen}   
    
3. Verifique a instalação do plug-in da CLI de criação de log.
  
    Por exemplo, verifique a versão do plug-in. Execute o comando a seguir:
    
    ```
    Cf criação -- version
    ```
    {: codeblock}
    
    A saída é semelhante ao seguinte:
   
    ```
    Log cf version 0.3.5
    ```
    {: screen}


## Instalando a CLI de Coleção de logs no Windows
{: #install_cli_windows}

Conclua as etapas a seguir para instalar o plug-in CF da Coleção de logs no Windows:

1. Faça download da liberação mais recente do plug-in da CLI do serviço {{site.data.keyword.loganalysisshort}} (IBM-Logging) da [página CLI do Bluemix](https://clis.ng.bluemix.net/ui/repository.html#cf-plugins). 
	
	1. Selecione o valor de plataforma: **win64**. 
	2. Clique em **Salvar arquivo**.  
    
2. Execute o comando **cf install-plugin** para instalar o plug-in Coleção de logs no Windows. 

    ```
	cf install-plugin PluginName
	```
	{: codeblock}
	
	em que *PluginName* é o nome do arquivo que foi transferido por download.
	
    Por exemplo, para instalar o plug-in *logging-cli-win64_v1.0.1.exe*, execute o comando a seguir de uma janela do terminal:
	
	```
	cf install-plugin logging-cli-win64_v1.0.1.exe
	```
	{: codeblock}
	
    Quando o plug-in estiver instalado, você receberá a mensagem a seguir: `Plug-in IBM-Logging 1.0.1 instalado com sucesso.`

3. Verifique a instalação do plug-in da CLI de criação de log.

    Por exemplo, verifique a versão do plug-in. Execute o comando a seguir:
    
    ```
    Cf criação -- version
    ```
    {: codeblock}
    
    A saída é semelhante ao seguinte:
   
    ```
    cf logging version 1.0.1
    ```
    {
	

## Instalando a CLI de Coleção de logs no Mac OS X
{: #install_cli_mac}

Conclua as etapas a seguir para instalar o plug-in CF da Coleção de logs no Mac OS X:

1. Faça download da liberação mais recente do plug-in da CLI do serviço {{site.data.keyword.loganalysisshort}} (IBM-Logging) da [página CLI do Bluemix](https://clis.ng.bluemix.net/ui/repository.html#cf-plugins).
	
	1. Selecione o valor de plataforma: **osx**.
	2. Clique em **Salvar arquivo**.

2. Execute o comando **cf install-plugin** para instalar o plug-in Coleção de logs no Mac OS X.

    ```
	cf install-plugin PluginName
	```
	{: codeblock}
	
	em que *PluginName* é o nome do arquivo que foi transferido por download.
	
    Por exemplo, para instalar o plug-in *logging-cli-darwin_v1.0.1*, execute o comando a seguir de um terminal:
	
	```
	cf install-plugin logging-cli-darwin_v1.0.1
	```
	{: codeblock}
	
    Quando o plug-in estiver instalado, você receberá a mensagem a seguir: `Plug-in IBM-Logging 1.0.1 instalado com sucesso.`

3. Verifique a instalação do plug-in da CLI de criação de log.

    Por exemplo, verifique a versão do plug-in. Execute o comando a seguir:
    
    ```
    Cf criação -- version
    ```
    {: codeblock}
    
    A saída é semelhante ao seguinte:
   
    ```
    cf logging version 1.0.1
    ```
    {
	
	
## Desinstalando a CLI de Coleção de logs
{: #uninstall_cli}

Para desinstalar a CLI de criação de log, exclua o plug-in.
{:shortdesc}

Conclua as etapas a seguir para desinstalar a CLI do serviço {{site.data.keyword.loganalysisshort}}:

1. Verifique a versão do plug-in da CLI de criação de log que está instalada.

    Por exemplo, verifique a versão do plug-in. Execute o comando a seguir:
    
    ```
    cf plugins
    ```
    {: codeblock}
    
    A saída é semelhante ao seguinte:
   
    ```
    Listing Installed Plugins...
    OK

    Plugin Name   Version   Command Name   Command Help
    IBM-Logging   1.0.1     logging        IBM Logging plug-in
    ```
    {
    
2. Se o plug-in estiver instalado, execute o `cf uninstall-plugin` para desinstalar o plug-in da CLI de criação de log.

    Execute o comando a seguir:

    ```
    Cf uninstall-plugin IBM-Logging
    ```
    {: codeblock}
  

## Obtendo ajuda geral
{: #general_cli_help}

Para obter informações gerais sobre a CLI e quais comandos são suportados, conclua as etapas a seguir:

1. Efetue login na região, na organização e no espaço do {{site.data.keyword.Bluemix_notm}}.

    Por exemplo, para efetuar login na região sul dos EUA, execute o comando a seguir:
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Liste informações sobre os comandos suportados e a CLI. Execute o comando a seguir:

    ```
    cf logging help 
    ```
    {: codeblock}
    
    

## Obtendo ajuda sobre um comando
{: #command_cli_help}

Para obter ajuda sobre como usar um comando, conclua as etapas a seguir:

1. Efetue login em uma região, uma organização e um espaço do {{site.data.keyword.Bluemix_notm}}. 

    Por exemplo, para efetuar login na região sul dos EUA, execute o comando a seguir:
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Obtenha a lista de comandos suportados e identifique aquele que você precisa. Execute o comando:

    ```
    cf logging help 
    ```
    {: codeblock}

3. Obter ajuda sobre o comando. Execute o comando a seguir:

    ```
    cf logging help *Command*
    ```
    {: codeblock}
    
    em que *Command* é o nome de um comando da CLI, por exemplo, *status*.



## Obtendo ajuda sobre um subcomando
{: #subcommand_cli_help}

Um comando pode ter subcomandos. Para obter ajuda sobre subcomandos, conclua as etapas a seguir:

1. Efetue login em uma região, uma organização e um espaço do {{site.data.keyword.Bluemix_notm}}. 

    Por exemplo, para efetuar login na região sul dos EUA, execute o comando a seguir:
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. Obtenha a lista de comandos suportados e identifique aquele que você precisa. Execute o comando:

    ```
    cf logging help 
    ```
    {: codeblock}

3. Obtenha ajuda sobre o comando e identifique os subcomandos suportados. Execute o comando a seguir:

    ```
    cf logging help *Command*
    ```
    {: codeblock}
    
    em que *Command* é o nome de um comando da CLI, por exemplo, *session*.

4. Obtenha ajuda sobre o comando e identifique os subcomandos suportados. Execute o comando a seguir:

    ```
    Cf de log *Command * ajuda *Subcommand
    ```
    {: codeblock}
    
    em que 
    
    * *Command* é o nome de um comando da CLI, por exemplo, *status*.
    * *Subcommand* é o nome de um subcomando suportado, por exemplo, para o comando *session*, um subcomando válido é *list*.




