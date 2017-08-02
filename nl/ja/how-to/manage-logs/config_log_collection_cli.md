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

# ログ収集 CLI の構成
{: #config_log_collection_cli}

{{site.data.keyword.loganalysisshort}} サービスには、クラウドでログを管理するために使用できるコマンド・ライン・インターフェース (CLI) が組み込まれています。この CLI は Cloud Foundry (CF) プラグインです。コマンドを使用して、ログ状況の表示、ログのダウンロード、ログ保存ポリシーの構成を行うことができます。この CLI にはいくつかの種類のヘルプがあります。一般ヘルプではこの CLI およびサポートされるコマンドについての情報が、コマンド・ヘルプではコマンドの使用方法が、サブコマンド・ヘルプではコマンドに対するサブコマンドの使用方法が提供されます。
{:shortdesc}


## ログ収集 CLI のインストール
{: #install_cli}

ログ収集 CLI をインストールするには、以下のステップを実行します。

1. CF CLI がご使用のシステムで使用可能であることを確認します。 

    詳しくは、『[前提条件](/docs/services/CloudLogAnalysis/how-to/manage-logs/config_log_collection_cli.html#pre_req)』を参照してください。

2. ログ収集 CF プラグインをインストールします。

    * Linux の場合、『[Linux へのログ収集 CLI のインストール](/docs/services/CloudLogAnalysis/how-to/manage-logs/config_log_collection_cli.html#install_cli_linux)』を参照してください。
    * Windows の場合、『[Windows へのログ収集 CLI のインストール](/docs/services/CloudLogAnalysis/how-to/manage-logs/config_log_collection_cli.html#install_cli_windows)』を参照してください。
    * Mac OS X の場合、『[Mac OS X へのログ収集 CLI のインストール](/docs/services/CloudLogAnalysis/how-to/manage-logs/config_log_collection_cli.html#install_cli_mac)』を参照してください。
 

## 前提条件
{: #pre_req}

ログ収集 CLI は CF プラグインです。これをインストールする前に、以下のシナリオを確認してください。

* 初めて CF CLI をインストールする場合:

     CF プラグインをインストールします。詳しくは、『[Installing the cf CLI ![外部リンク・アイコン](../../../../icons/launch-glyph.svg "外部リンク・アイコン")](http://docs.cloudfoundry.org/cf-cli/install-go-cli.html "外部リンク・アイコン"){: new_window}』を参照してください。 

* {{site.data.keyword.Bluemix_notm}} CLI パッケージがインストールされている場合:

    CF CLI は {{site.data.keyword.Bluemix_notm}} CLI パッケージにバンドルされています。

* その他のクラウド・リソースを管理するには、{{site.data.keyword.Bluemix_notm}} CLI が必要になります。  

    {{site.data.keyword.Bluemix_notm}} CLI パッケージをインストールします。『[{{site.data.keyword.Bluemix_notm}} CLI のインストール](/docs/cli/reference/bluemix_cli/index.html#install_bluemix_cli)』を参照してください。

その後、CF プラグインが使用可能であることを確認します。ご使用のシステムのセッションから以下のコマンドを実行します。
    
```
cf -v
```
{: codeblock}
    
出力は以下のようになります。
    
```
cf version 6.25.0+787326d.2017-02-28
```
{: screen}

**注:**  {{site.data.keyword.Bluemix_notm}} CLI コマンド (つまり `bx` コマンド) と CF CLI コマンド (つまり `cf` コマンド) を混用することはできません。



	
## Linux へのログ収集 CLI のインストール
{: #install_cli_linux}

Linux にログ収集 CF プラグインをインストールするには、以下のステップを実行します。

1. ログ収集 CLI プラグインをインストールします。

    1. 最新リリースの {{site.data.keyword.loganalysisshort}} サービス CLI プラグイン (IBM-Logging) を [Bluemix CLI ページ](https://clis.ng.bluemix.net/ui/repository.html#cf-plugins)からダウンロードします。 
	
		プラットフォーム値**「linux64」**を選択します。
		**「ファイルの保存」**をクリックします。 
    
    2. プラグインを unzip します。
    
        例えば、Ubuntu で `logging-cli-linux64.gz` プラグインを unzip するには、以下のコマンドを実行します。
        
        ```
        gunzip logging-cli-linux64.gz
        ```
        {: codeblock}

    3. ファイルを実行可能にします。
    
        例えば、ファイル `logging-cli-linux64` を実行可能にするには、次のコマンドを実行します。
        
        ```
        chmod a+x logging-cli-linux64
        ```
        {: codeblock}

    4. ロギング CF プラグインをインストールします。
    
        例えば、ファイル `logging-cli-linux64` を実行可能にするには、次のコマンドを実行します。
        
        ```
        cf install-plugin -f logging-cli-linux64
        ```
        {: codeblock}

2. 環境変数 **LANG** を設定します。

    ご使用のシステム・ロケールが CF でサポートされていない場合は、*LANG* をデフォルト値である *en_US.UTF-8* に設定します。CF でサポートされるロケールについては、[Getting Started with the cf CLI ![外部リンク・アイコン](../../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.cloudfoundry.org/cf-cli/getting-started.html "外部リンク・アイコン"){: new_window} を参照してください。
	
	例えば、Ubuntu システムでは、*~/.bashrc* ファイルを編集し、以下の行を入力します。
    
    ```
    # add entry for logging CLI
    export LANG = en_US.UTF-8
    ```
    {: codeblock}
    
    新しい端末ウィンドウを開き、次のコマンドを実行して、変数 LANG および LOGGING_ENDPOINT が設定されていることを検証します。
    
    ```
    $echo LANG
    en_US.UTF-8
    ```
    {: screen}   
    
3. ロギング CLI プラグインのインストールを検証します。
  
    例えば、プラグインのバージョンを確認します。次のコマンドを実行します。
    
    ```
    cf logging --version
    ```
    {: codeblock}
    
    出力は以下のようになります。
   
    ```
    cf logging version 0.3.5
    ```
    {: screen}


## Windows へのログ収集 CLI のインストール
{: #install_cli_windows}

Windows にログ収集 CF プラグインをインストールするには、以下のステップを実行します。

1. 最新リリースの {{site.data.keyword.loganalysisshort}} サービス CLI プラグイン (IBM-Logging) を [Bluemix CLI ページ](https://clis.ng.bluemix.net/ui/repository.html#cf-plugins)からダウンロードします。 
	
	1. プラットフォーム値**「win64」**を選択します。 
	2. **「ファイルの保存」**をクリックします。  
    
2. **cf install-plugin** コマンドを実行して、ログ収集プラグインを Windows にインストールします。 

    ```
	cf install-plugin PluginName
	```
	{: codeblock}

    ここで、「PluginName」はダウンロードしたファイルの名前です。
	
    例えば、プラグイン「logging-cli-win64_v1.0.1.exe」をインストールするには、端末ウィンドウから以下のコマンドを実行します。 	
	```
	cf install-plugin logging-cli-win64_v1.0.1.exe
	```
	{: codeblock}

    プラグインがインストールされたら、メッセージ「プラグイン IBM-Logging 1.0.1 は正常にインストールされました」が表示されます。

3. ロギング CLI プラグインのインストールを検証します。

    例えば、プラグインのバージョンを確認します。次のコマンドを実行します。

    ```
    cf logging --version
    ```
{: codeblock}

    出力は以下のようになります。```
    cf logging version 1.0.1
    ```
    {: screen}
	

## Mac OS X へのログ収集 CLI のインストール
{: #install_cli_mac}

Mac OS X にログ収集 CF プラグインをインストールするには、以下のステップを実行します。

1. 最新リリースの {{site.data.keyword.loganalysisshort}} サービス CLI プラグイン (IBM-Logging) を [Bluemix CLI ページ](https://clis.ng.bluemix.net/ui/repository.html#cf-plugins) からダウンロードします。
	
	1. プラットフォーム値「osx」を選択します。
	2. 「ファイルの保存」をクリックします。

2. 「cf install-plugin」コマンドを実行して、ログ収集プラグインを Mac OS X にインストールします。

    ```
	cf install-plugin PluginName
	```
	{: codeblock}
	
	ここで、「PluginName」はダウンロードしたファイルの名前です。
	
    例えば、プラグイン「logging-cli-darwin_v1.0.1」をインストールするには、端末から以下のコマンドを実行します。
	```
	cf install-plugin logging-cli-darwin_v1.0.1
	```
	{: codeblock}
	
    プラグインがインストールされたら、メッセージ「プラグイン IBM-Logging 1.0.1 は正常にインストールされました」が表示されます。

3. ロギング CLI プラグインのインストールを検証します。

    例えば、プラグインのバージョンを確認します。次のコマンドを実行します。

    ```
    cf logging --version
    ```
{: codeblock}

    出力は以下のようになります。```
    cf logging version 1.0.1
    ```
    {: screen}
	
	
## ログ収集 CLI のアンインストール
{: #uninstall_cli}

ロギング CLI をアンインストールするには、プラグインを削除します。
{:shortdesc}

{{site.data.keyword.loganalysisshort}} サービス CLI をアンインストールするには、以下のステップを実行します。

1. インストールされているロギング CLI プラグインのバージョンを確認します。

    例えば、プラグインのバージョンを確認します。次のコマンドを実行します。

    ```
    cf plugins
    ```
    {: codeblock}

    出力は以下のようになります。```
    Listing Installed Plugins...
    OK

    Plugin Name   Version   Command Name   Command Help
    IBM-Logging   1.0.1     logging        IBM Logging plug-in
    ```
    {: screen}

2. プラグインがインストールされている場合、「cf uninstall-plugin」を実行して、ロギング CLI プラグインをアンインストールします。
    次のコマンドを実行します。

    ```
    cf uninstall-plugin IBM-Logging
    ```
    {: codeblock}


## 一般ヘルプの入手
{: #general_cli_help}

CLI およびサポートされているコマンドに関する一般情報を入手するには、以下のステップを実行します。

1. {{site.data.keyword.Bluemix_notm}} 地域、組織、およびスペースにログインします。

     例えば、米国南部地域にログインするには、以下のコマンドを実行します。
	
	```
    cf login -a https://api.ng.bluemix.net
```
    {: codeblock}
    
2. サポートされるコマンドおよび CLI についての情報をリストします。次のコマンドを実行します。

    ```
    cf logging help 
    ```
    {: codeblock}
    
    

## コマンドに関するヘルプの利用
{: #command_cli_help}

コマンドの使用法に関するヘルプを利用するには、以下のステップを実行します。

1. {{site.data.keyword.Bluemix_notm}} 地域、組織、およびスペースにログインします。 

    例えば、米国南部地域にログインするには、以下のコマンドを実行します。
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. サポートされるコマンドのリストを取得し、必要なコマンドを識別します。コマンドを実行します。

    ```
    cf logging help
    ```
    {: codeblock}

3. 特定のコマンドに関するヘルプを取得します。次のコマンドを実行します。

    ```
    cf logging help *Command*
    ```
    {: codeblock}
    
    ここで、*Command* は CLI コマンドの名前です (例: *status*)。



## サブコマンドに関するヘルプの利用
{: #subcommand_cli_help}

コマンドにはサブコマンドがある場合があります。サブコマンドに関するヘルプを利用するには、以下のステップを実行します。

1. {{site.data.keyword.Bluemix_notm}} 地域、組織、およびスペースにログインします。 

    例えば、米国南部地域にログインするには、以下のコマンドを実行します。
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
    
2. サポートされるコマンドのリストを取得し、必要なコマンドを識別します。コマンドを実行します。

    ```
    cf logging help
    ```
    {: codeblock}

3. 特定のコマンドに関するヘルプを取得し、サポートされるサブコマンドを識別します。次のコマンドを実行します。

    ```
    cf logging help *Command*
    ```
    {: codeblock}
    
    ここで、*Command* は CLI コマンドの名前です (例: *session*)。

4. 特定のコマンドに関するヘルプを取得し、サポートされるサブコマンドを識別します。次のコマンドを実行します。

    ```
    cf logging *Command* help *Subcommand*
    ```
    {: codeblock}
    
    各部分の説明: 
    
    * *Command* は CLI コマンドの名前です (例: *status*)。
    * *Subcommand* はサポートされるサブコマンドの名前です (例: コマンド *session* の有効なサブコマンドは *list* です)。




