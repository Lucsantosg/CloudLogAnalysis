---

copyright:
  years: 2017, 2018

lastupdated: "2018-01-10"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# クラスター・ログの自動収集の有効化
{: #containers_kube_other_logs}

{{site.data.keyword.loganalysisshort}} サービスでクラスター・ログを表示および分析できるためには、ログを {{site.data.keyword.loganalysisshort}} サービスに転送するようにクラスターを構成する必要があります。 
{:shortdesc}

## ステップ 1: 許可を確認する
{: step1}

クラスターを管理する許可が設定された {{site.data.keyword.containershort}} の IAM ポリシーを持つユーザーのみが、この機能を有効にすることができます。 *管理者*、*オペレーター* のいずれかの役割が必要です。

ユーザー ID に、クラスターを管理するために割り当てられた IAM ポリシーがあることを確認するには、以下のステップを実行します。

**注:** アカウント所有者、または、ポリシーを割り当てる許可を持つユーザーのみが、このステップを実行できます。

1. {{site.data.keyword.Bluemix_notm}} コンソールにログインします。 Web ブラウザーを開き、{{site.data.keyword.Bluemix_notm}} ダッシュボード: [http://bluemix.net ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](http://bluemix.net){:new_window} を起動します。
	
	ユーザー ID とパスワードを使用してログインすると、{{site.data.keyword.Bluemix_notm}} UI が開きます。

2. メニュー・バーから、**「管理」>「アカウント」>「ユーザー」**をクリックします。  「*ユーザー*」ウィンドウに、現在選択されているアカウントにおけるユーザーのリストが、E メール・アドレスと共に表示されます。
	
3. ユーザー ID を選択し、そのユーザー ID に {{site.data.keyword.containershort}} の*ビューアー* 許可を持つポリシーがあることを確認します。




## ステップ 2: クラスター・コンテキストをセットアップする
{: #step2}

以下のステップを実行します。

1. {{site.data.keyword.Bluemix_notm}} で、地域、組織、およびスペースにログインします。 

    詳しくは、『[{{site.data.keyword.Bluemix_notm}} にログインするにはどうすればよいですか](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login)』を参照してください。
    
2. {{site.data.keyword.loganalysisshort}} サービス・プラグインを初期化します。

	```
	bx cs init
	```
	{: codeblock}

3. 端末コンテキストをクラスターに設定します。
    
	```
	bx cs cluster-config ClusterName
	```
	{: codeblock}

    このコマンド実行の出力では、構成ファイルへのパスを設定するためにご使用の端末で実行する必要のあるコマンドが示されます。 例えば、*MyCluster* という名前のクラスターの場合は、以下のようになります。

	```
	export KUBECONFIG=/Users/ibm/.bluemix/plugins/container-service/clusters/MyCluster/kube-config-hou02-MyCluster.yml
	```
	{: codeblock}

4. ご使用の端末で環境変数を設定するコマンドをコピーして貼り付け、**Enter** を押します。



## ステップ 3: クラスターを構成する
{: step3}

どのクラスター・ログを {{site.data.keyword.loganalysisshort}} サービスに転送するのかを選択できます。 

* stdout および stderr の自動ログ収集および転送を有効にするには、[コンテナー・ログの自動ログ収集および転送の有効化](/docs/services/CloudLogAnalysis/containers/containers_kube_other_logs.html#containers)を参照してください。
* アプリケーション・ログの自動ログ収集および転送を有効にするには、[アプリケーション・ログの自動ログ収集および転送の有効化](/docs/services/CloudLogAnalysis/containers/containers_kube_other_logs.html#apps)を参照してください。
* ワーカー・ログの自動ログ収集および転送を有効にするには、[ワーカー・ログの自動ログ収集および転送の有効化](/docs/services/CloudLogAnalysis/containers/containers_kube_other_logs.html#workers)を参照してください。
* Kubernetes システム・コンポーネント・ログの自動ログ収集および転送を有効にするには、[Kubernetes システム・コンポーネント・ログの自動ログ収集および転送の有効化](/docs/services/CloudLogAnalysis/containers/containers_kube_other_logs.html#system)を参照してください。
* Kubernetes Ingress コントローラー・ログの自動ログ収集および転送を有効にするには、[Kubernetes Ingress コントローラー・ログの自動ログ収集および転送の有効化](/docs/services/CloudLogAnalysis/containers/containers_kube_other_logs.html#controller)を参照してください。



## ステップ 4: {{site.data.keyword.containershort_notm}} キー所有者の許可を設定する
{: #step4}

ログをスペースに転送する場合、組織およびスペースの {{site.data.keyword.containershort}} キー所有者にも Cloud Foundry (CF) 許可を付与する必要があります。キー所有者には、組織の *orgManager* 役割と、スペースの *SpaceManager* と*開発者* の役割が必要です。

以下のステップを実行します。

1. {{site.data.keyword.containershort}} キー所有者であるアカウントのユーザーを識別します。端末から次のコマンドを実行します。

    ```
    bx cs api-key-info ClusterName
    ```
    {: codeblock}
    
    ここで、*ClusterName* はクラスターの名前です。
    
2. {{site.data.keyword.containershort}} キー所有者として識別されたユーザーに、組織の *orgManager* 役割とスペースの *SpaceManager* および*開発者* の役割があることを確認します。

    {{site.data.keyword.Bluemix_notm}} コンソールにログインします。 Web ブラウザーを開き、{{site.data.keyword.Bluemix_notm}} ダッシュボード ([http://bluemix.net ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](http://bluemix.net){:new_window}) を起動します。ユーザー ID とパスワードでログインすると、{{site.data.keyword.Bluemix_notm}} UI が開きます。

    メニュー・バーから、**「管理」>「アカウント」>「ユーザー」**をクリックします。  「*ユーザー*」ウィンドウに、現在選択されているアカウントにおけるユーザーのリストが、E メール・アドレスと共に表示されます。
	
    ユーザーの ID を選択し、ユーザーに組織の *orgManager* 役割とスペースの *SpaceManager* および*開発者* の役割があることを確認します。
 
3. ユーザーに適切な許可がない場合は、以下のステップを実行します。

    1. ユーザーに次の許可を付与します。組織の *orgManager* 役割。スペースの *SpaceManager* および*開発者* の役割。詳しくは、[IBM Cloud UI を使用して、スペース・ログを表示する許可をユーザーに付与する](/docs/services/CloudLogAnalysis/security/grant_permissions.html#grant_permissions_ui_space)を参照してください。
    
    2. ロギング構成を更新します。次のコマンドを実行します。
    
        ```
        bx cs logging-config-refresh ClusterName
        ```
        {: codeblock}
        
        ここで、*ClusterName* はクラスターの名前です。
  




## コンテナー・ログの自動ログ収集および転送の有効化 
{: #containers}

*stdout* および *stderr* ログ・ファイルを {{site.data.keyword.loganalysisshort}} サービスに送信するには、以下のコマンドを実行します。

```
bx cs logging-config-create ClusterName --logsource container --namespace '*' --type ibm --hostname EndPoint --port 9091 --org OrgName --space SpaceName 
```
{: codeblock}

各部分の説明: 

* *ClusterName* はクラスターの名前です。
* *EndPoint* は、{{site.data.keyword.loganalysisshort}} サービスがプロビジョンされた地域内のロギング・サービスの URL です。エンドポイントのリストについては、[エンドポイント](/docs/services/CloudLogAnalysis/log_ingestion.html#log_ingestion_urls)を参照してください。
* *OrgName* は、スペースがある組織の名前です。
* *SpaceName* は、{{site.data.keyword.loganalysisshort}} サービスがプロビジョンされたスペースの名前です。


例えば、stdout および stderr のログをドイツ地域のアカウント・ドメインに転送するロギング構成を作成するには、次のコマンドを実行します。

```
bx cs logging-config-create MyCluster --logsource container --type ibm --namespace '*' --type ibm --hostname ingest-eu-fra.logging.bluemix.net --port 9091 
```
{: screen}

stdout および stderr のログをドイツ地域のスペース・ドメインに転送するロギング構成を作成するには、次のコマンドを実行します。

```
bx cs logging-config-create MyCluster --logsource container --type ibm --namespace '*' --type ibm --hostname ingest-eu-fra.logging.bluemix.net --port 9091 --org MyOrg --space MySpace
```
{: screen}



## アプリケーション・ログの自動ログ収集および転送の有効化 
{: #apps}

*/var/log/apps/**/.log* および */var/log/apps/*/.err* ログ・ファイルを {{site.data.keyword.loganalysisshort}} サービスに送信するには、以下のコマンドを実行します。

```
bx cs logging-config-create ClusterName --logsource application --type ibm --hostname EndPoint --port 9091 --org OrgName --space SpaceName 
```
{: codeblock}

各部分の説明: 

* *ClusterName* はクラスターの名前です。
* *EndPoint* は、{{site.data.keyword.loganalysisshort}} サービスがプロビジョンされた地域内のロギング・サービスの URL です。エンドポイントのリストについては、[エンドポイント](/docs/services/CloudLogAnalysis/log_ingestion.html#log_ingestion_urls)を参照してください。
* *OrgName* は、スペースがある組織の名前です。
* *SpaceName* は、{{site.data.keyword.loganalysisshort}} サービスがプロビジョンされたスペースの名前です。


例えば、アプリケーション・ログをドイツ地域のスペース・ドメインに転送するロギング構成を作成するには、次のコマンドを実行します。

```
bx cs logging-config-create MyCluster --logsource application --type ibm --hostname ingest-eu-fra.logging.bluemix.net --port 9091 --org MyOrg --space MySpace
```
{: screen}

例えば、アプリケーション・ログをドイツ地域のアカウント・ドメインに転送するロギング構成を作成するには、次のコマンドを実行します。

```
bx cs logging-config-create MyCluster --logsource application --type ibm --hostname ingest-eu-fra.logging.bluemix.net --port 9091 
```
{: screen}



## ワーカー・ログの自動ログ収集および転送の有効化 
{: #workers}


*/var/log/syslog* および */var/log/auth.log* ログ・ファイルを {{site.data.keyword.loganalysisshort}} サービスに送信するには、以下のコマンドを実行します。

```
bx cs logging-config-create ClusterName --logsource worker --type ibm --hostname EndPoint --port 9091 --org OrgName --space SpaceName 
```
{: codeblock}

各部分の説明: 

* *ClusterName* はクラスターの名前です。
* *EndPoint* は、{{site.data.keyword.loganalysisshort}} サービスがプロビジョンされた地域内のロギング・サービスの URL です。エンドポイントのリストについては、[エンドポイント](/docs/services/CloudLogAnalysis/log_ingestion.html#log_ingestion_urls)を参照してください。
* *OrgName* は、スペースがある組織の名前です。
* *SpaceName* は、{{site.data.keyword.loganalysisshort}} サービスがプロビジョンされたスペースの名前です。



例えば、ワーカー・ログをドイツ地域のスペース・ドメインに転送するロギング構成を作成するには、次のコマンドを実行します。

```
bx cs logging-config-create MyCluster --logsource worker  --type ibm --hostname ingest-eu-fra.logging.bluemix.net --port 9091 --org OrgName --space SpaceName 
```
{: screen}

例えば、ワーカー・ログをドイツ地域のアカウント・ドメインに転送するロギング構成を作成するには、次のコマンドを実行します。

```
bx cs logging-config-create MyCluster --logsource worker  --type ibm --hostname ingest-eu-fra.logging.bluemix.net --port 9091 
```
{: screen}



## Kubernetes システム・コンポーネント・ログの自動ログ収集および転送の有効化
{: #system}

*/var/log/kubelet.log* および */var/log/kube-proxy.log* ログ・ファイルを {{site.data.keyword.loganalysisshort}} サービスに送信するには、以下のコマンドを実行します。

```
bx cs logging-config-create ClusterName --logsource kubernetes --type ibm --hostname EndPoint --port 9091 --org OrgName --space SpaceName 
```
{: codeblock}

各部分の説明: 

* *ClusterName* はクラスターの名前です。
* *EndPoint* は、{{site.data.keyword.loganalysisshort}} サービスがプロビジョンされた地域内のロギング・サービスの URL です。エンドポイントのリストについては、[エンドポイント](/docs/services/CloudLogAnalysis/log_ingestion.html#log_ingestion_urls)を参照してください。
* *OrgName* は、スペースがある組織の名前です。
* *SpaceName* は、{{site.data.keyword.loganalysisshort}} サービスがプロビジョンされたスペースの名前です。



例えば、Kubernetes システム・コンポーネント・ログをドイツ地域のスペース・ドメインに転送するロギング構成を作成するには、次のコマンドを実行します。

```
bx cs logging-config-create MyCluster --logsource kubernetes --type ibm --hostname ingest-eu-fra.logging.bluemix.net --port 9091 --org OrgName --space SpaceName 
```
{: screen}

例えば、Kubernetes システム・コンポーネント・ログをドイツ地域のアカウント・ドメインに転送するロギング構成を作成するには、次のコマンドを実行します。

```
bx cs logging-config-create MyCluster --logsource kubernetes --type ibm --hostname ingest-eu-fra.logging.bluemix.net --port 9091 
```
{: screen}



## Kubernetes Ingress コントローラー・ログの自動ログ収集および転送の有効化
{: #controller}

*/var/log/alb/ids/.log*、*/var/log/alb/ids/.err*、*/var/log/alb/customerlogs/.log*、および /var/log/alb/customerlogs/.err* ログ・ファイルを {{site.data.keyword.loganalysisshort}} サービスに送信するには、以下のコマンドを実行します。

```
bx cs logging-config-create ClusterName --logsource ingress --type ibm --hostname EndPoint --port 9091 --org OrgName --space SpaceName s
```
{: codeblock}

各部分の説明: 

* *ClusterName* はクラスターの名前です。
* *EndPoint* は、{{site.data.keyword.loganalysisshort}} サービスがプロビジョンされた地域内のロギング・サービスの URL です。エンドポイントのリストについては、[エンドポイント](/docs/services/CloudLogAnalysis/log_ingestion.html#log_ingestion_urls)を参照してください。
* *OrgName* は、スペースがある組織の名前です。
* *SpaceName* は、{{site.data.keyword.loganalysisshort}} サービスがプロビジョンされたスペースの名前です。



例えば、Ingress コントローラー・ログをドイツ地域のスペース・ドメインに転送するロギング構成を作成するには、次のコマンドを実行します。

```
bx cs logging-config-create MyLoggingDemoCluster --logsource ingress --type ibm --hostname ingest-eu-fra.logging.bluemix.net --port 9091 --org OrgName --space SpaceName 
```
{: screen}

例えば、Ingress コントローラー・ログをドイツ地域のアカウント・ドメインに転送するロギング構成を作成するには、次のコマンドを実行します。

```
bx cs logging-config-create MyLoggingDemoCluster --logsource ingress --type ibm --hostname ingest-eu-fra.logging.bluemix.net --port 9091  
```
{: screen}


