---

copyright:
  years: 2017, 2018

lastupdated: "2018-01-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 概説のチュートリアル
{: #getting-started-with-cla}

このチュートリアルを使用して、{{site.data.keyword.Bluemix}} で {{site.data.keyword.loganalysislong}} サービスを使用した作業を開始する方法を学習します。
{:shortdesc}

## 目標
{: #objectives}

* {{site.data.keyword.loganalysislong}} サービスをスペースにプロビジョンします。
* ログを管理するには、コマンド・ラインをセットアップします。
* スペース内のログをユーザーが表示するための許可を設定します。
* ログを表示するために使用できるオープン・ソース・ツールである Kibana を起動します。


## 始める前に
{: #prereqs}

{{site.data.keyword.Bluemix_notm}} アカウントのメンバーまたは所有者であるユーザー ID が必要です。{{site.data.keyword.Bluemix_notm}} ユーザー ID を取得するには、[「登録」![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.bluemix.net/registration/){:new_window} にアクセスしてください。

このチュートリアルでは、米国南部地域で {{site.data.keyword.loganalysisshort}} サービスをプロビジョンし、このサービスを使用して作業を行う方法を説明します。


## ステップ 1: {{site.data.keyword.loganalysisshort}} サービスのプロビジョン
{: #step1}

**注:** Cloud Foundry (CF) スペース内に {{site.data.keyword.loganalysisshort}} サービスのインスタンスをプロビジョンします。スペースごとに 1 つのサービス・インスタンスのみが必要です。アカウント・レベルで {{site.data.keyword.loganalysisshort}} サービスをプロビジョンすることはできません。 

{{site.data.keyword.Bluemix_notm}} で {{site.data.keyword.loganalysisshort}} サービスのインスタンスをプロビジョンするには、以下のステップを実行します。

1. {{site.data.keyword.Bluemix_notm}} ([http://bluemix.net ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://bluemix.net){:new_window}) にログインします。  

2. {{site.data.keyword.loganalysisshort}} サービスをプロビジョンしたい地域、組織、およびスペースを選択します。  

3. **「カタログ」**をクリックします。 {{site.data.keyword.Bluemix_notm}} で使用可能なサービスのリストが開きます。

4. **「DevOps」**カテゴリーを選択して、表示されたサービスのリストをフィルタリングします。

5. **「Log Analysis」**タイルをクリックします。

6. サービス・プランを選択します。 デフォルトでは、**「ライト」**プランが設定されています。

    サービス・プランについて詳しくは、『[サービス・プラン](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans)』を参照してください。
	
7. **「作成」**をクリックして、ログインしている {{site.data.keyword.Bluemix_notm}} スペースで {{site.data.keyword.loganalysisshort}} サービスをプロビジョンします。




## ステップ 2: [オプション] {{site.data.keyword.loganalysisshort}} サービスのサービス・プランの変更
{: #step2}

さらに多くの検索割り当て量、ログの長期保管、またはその両方が必要な場合、{{site.data.keyword.loganalysisshort}} サービス・インスタンスのプランを {{site.data.keyword.Bluemix_notm}} UI から変更するか、`bx cf update-service` コマンドを実行することで変更して、これらの機能を有効にできます。 

サービス・プランはいつでもアップグレードまたは削減することができます。

詳しくは、『[{{site.data.keyword.loganalysisshort}} サービス・プラン](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans)』を参照してください。

**注:** プランを有料プランに変更すると、コストがかかります。

{{site.data.keyword.Bluemix_notm}} UI でサービス・プランを変更するには、以下のステップを実行します。

1. {{site.data.keyword.Bluemix_notm}} ([http://bluemix.net ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://bluemix.net){:new_window}) にログインします。  

2. {{site.data.keyword.loganalysisshort}} サービスを使用可能な地域、組織、およびスペースを選択します。  

3. {{site.data.keyword.Bluemix_notm}} *ダッシュボード*から {{site.data.keyword.loganalysisshort}} サービス・インスタンスをクリックします。 
    
4. {{site.data.keyword.loganalysisshort}} ダッシュボードで**「プラン」**タブを選択します。

    現在のプランに関する情報が表示されます。
	
5. プランをアップグレードまたは削減するため、新しいプランを選択します。 

6. **「保存」**をクリックします。



## ステップ 3: {{site.data.keyword.loganalysisshort}} サービスを使用して作業するためのローカル環境のセットアップ
{: #step3}


{{site.data.keyword.loganalysisshort}} サービスには、Log Collection (長期保管コンポーネント) に保管されているログの管理に使用できるコマンド・ライン・インターフェース (CLI) が組み込まれています。 

{{site.data.keyword.loganalysisshort}} {{site.data.keyword.Bluemix_notm}} プラグインを使用して、ログ状況の表示、ログのダウンロード、ログ保存ポリシーの構成を行うことができます。 

この CLI にはいくつかの種類のヘルプがあります。一般ヘルプではこの CLI およびサポートされるコマンドについての情報が、コマンド・ヘルプではコマンドの使用方法が、サブコマンド・ヘルプではコマンドに対するサブコマンドの使用方法が提供されます。

{{site.data.keyword.Bluemix_notm}} リポジトリーから {{site.data.keyword.loganalysisshort}} CLI をインストールするには、以下のステップを実行します。

1. {{site.data.keyword.Bluemix_notm}} CLI をインストールします。

   詳しくは、『[{{site.data.keyword.Bluemix_notm}} CLI のインストール](/docs/cli/reference/bluemix_cli/download_cli.html#download_install)』を参照してください。

2. {{site.data.keyword.loganalysisshort}} プラグインをインストールします。次のコマンドを実行します。

    ```
    bx plugin install logging-cli -r Bluemix
    ```
    {: codeblock}
 
3. {{site.data.keyword.loganalysisshort}} プラグインがインストールされたことを確認します。
  
    例えば、以下のコマンドを実行して、インストール済みのプラグインのリストを表示します。
    
    ```
    bx plugin list
    ```
    {: codeblock}
    
    出力は以下のようになります。
   
    ```
    bx plugin list
    Listing installed plug-ins...

    Plugin Name          Version   
    logging-cli          0.1.1   
    ```
    {: screen}




## ステップ 4: ユーザーがログを表示するための許可の設定
{: #step4}

ユーザーが実行を許可される {{site.data.keyword.loganalysisshort}} アクションを制御するために、ユーザーに役割とポリシーを割り当てることができます。 

{{site.data.keyword.Bluemix_notm}} には 2 つのタイプのセキュリティー権限があり、それらの権限によって、ユーザーが {{site.data.keyword.loganalysisshort}} サービスを使用した処理を行うときに実行できるアクションが制御されます。

* Cloud Foundry (CF) 役割: ユーザーに CF 役割を付与して、ユーザーがスペース内のログを表示するために必要な許可を定義します。
* IAM 役割: ユーザーに IAM ポリシーを付与して、ユーザーがアカウント・ドメイン内のログを表示するために必要な許可と、ユーザーが Log Collection 内に保管されているログを管理するために必要な許可を定義します。 


以下のステップを実行して、スペース内のログを表示するための許可をユーザーに付与します。

1. {{site.data.keyword.Bluemix_notm}} コンソールにログインします。

    Web ブラウザーを開き、{{site.data.keyword.Bluemix_notm}} ダッシュボード: [http://bluemix.net ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://bluemix.net){:new_window} を起動します。
	
	ユーザー ID とパスワードを使用してログインすると、{{site.data.keyword.Bluemix_notm}} UI が開きます。

2. メニュー・バーから、**「管理」>「アカウント」>「ユーザー」**をクリックします。 

    「*ユーザー*」ウィンドウに、現在選択されているアカウントにおけるユーザーのリストが、E メール・アドレスと共に表示されます。
	
3. ユーザーがアカウントのメンバーである場合、リストからユーザー名を選択するか、または、**「アクション」**メニューから*「ユーザーの管理」*をクリックします。

    ユーザーがアカウントのメンバーでない場合、『[ユーザーの招待](/docs/iam/iamuserinv.html#iamuserinv)』を参照してください。

4. **「Cloud Foundry アクセス権限」**を選択してから、組織を選択します。

    その組織で使用可能なスペースのリストが表示されます。

5. {{site.data.keyword.loganalysisshort}} サービスをプロビジョンしたスペースを選択します。次に、メニュー・アクションから**「スペースの役割の編集」**を選択します。

6. *監査員* を選択します。 

    1 つ以上のスペースの役割を選択できます。*管理者*、*開発者*、および*監査員* のすべての役割が、ユーザーにログの表示を許可します。
	
7. **「役割の保存」**をクリックします。


詳しくは、[許可の付与](/docs/services/CloudLogAnalysis/security/grant_permissions.html#grant_permissions_ui_account)を参照してください。



## ステップ 5: Kibana の起動
{: #step5}

ログ・データを表示および分析するには、ログ・データが使用可能な Cloud Public 地域の Kibana にアクセスする必要があります。 


米国南部地域の Kibana を起動するには、Web ブラウザーを開き、次の URL を入力します。

```
https://logging.ng.bluemix.net/ 
```
{: codeblock}


その他の地域の Kibana を起動する方法について詳しくは、[Web ブラウザーから Kibana へのナビゲート](/docs/services/CloudLogAnalysis/kibana/launch.html#launch_Kibana_from_browser)を参照してください。

**注:** Kibana を起動したときに、*「無効なベアラー・トークン」*を示すメッセージが表示された場合、スペース内での許可を確認してください。このメッセージは、そのユーザー ID にログを表示するための許可がないことを示しています。
    

## 次のステップ 
{: #next_steps}

ログを生成します。以下のチュートリアルのいずれかを試してください。

* [Kubernetes クラスターにデプロイされたアプリに関する Kibana でのログの分析](/docs/services/CloudLogAnalysis/tutorials/container_logs.html#container_logs){:new_window} 

    このチュートリアルでは、クラスターをプロビジョンし、{{site.data.keyword.Bluemix_notm}} の {{site.data.keyword.loganalysisshort}} サービスにログを送信するためにクラスターを構成し、クラスター内にアプリをデプロイし、Kibana を使用してそのクラスターのコンテナー・ログを表示およびフィルタリングするまでのエンドツーエンドのシナリオを機能させるために必要なステップを示しています。     
    
* [Cloud Foundry アプリのログの Kibana での分析](/docs/tutorials/application-log-analysis.html#generate-access-and-analyze-application-logs){:new_window}                                                                                                            

    このチュートリアルでは、Python Cloud Foundry アプリケーションをデプロイし、いろいろなタイプのログを生成し、Kibana を使用して CF ログを表示、検索、および分析するまでのエンドツーエンドのシナリオを機能させるために必要なステップを示しています。
   








