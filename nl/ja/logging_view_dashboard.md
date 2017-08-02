---

copyright:
  years: 2017

lastupdated: "2017-07-19"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Bluemix UI でのログの分析
{: #analyzing_logs_bmx_ui}

{{site.data.keyword.Bluemix}} では、Cloud Foundry アプリごと、または {{site.data.keyword.IBM_notm}} が管理するインフラストラクチャーで稼働する Docker コンテナーごとにあるログ・タブを使用して、ログの表示、フィルタリング、および分析を行うことができます。
{:shortdesc}

##  Cloud Foundry アプリのログへのナビゲート
{: #launch_logs_tab_bmx_ui_cf}

Cloud Foundry アプリのデプロイメントまたはランタイムのログを表示するには、以下の手順を実行します。

1. 「アプリ」ダッシュボードで Cloud Foundry アプリの名前をクリックします。 
    
2. アプリ詳細ページで**「ログ」**をクリックします。
    
    **「ログ」**タブでは、アプリの最近のログを表示したり、最新のログ (ログ・ファイルの末尾) をリアルタイムで確認することができます。また、コンポーネント (ログ・タイプ)、アプリ・インスタンス ID、およびエラーで、ログをフィルター操作できます。
    
デフォルトでは、{{site.data.keyword.Bluemix_notm}} コンソールから分析用に使用可能なログには、過去 24 時間のデータが含まれます。

**ヒント:** 過去 24 時間より前のカスタム期間のデータを分析する場合は、『[Kibana での高度なログ分析](/docs/services/CloudLogAnalysis/kibana/analyzing_logs_Kibana.html#analyzing_logs_Kibana)』を参照してください。 





##  Bluemix で管理されている Docker コンテナーのログへのナビゲート
{: #launch_logs_tab_bmx_ui_containers}

{{site.data.keyword.IBM_notm}} が管理するクラウド・インフラストラクチャーにデプロイされた Docker コンテナーのデプロイメント・ログまたはランタイム・ログを表示するには、以下の手順を実行します。

1. 「アプリ」ダッシュボードで単一コンテナーまたはコンテナー・グループをクリックします。 
    
2. アプリ詳細ページで**「モニターおよびログ (Monitoring and Logs)」**をクリックします。

3. **「ロギング」**タブを選択します。
    
    **「ロギング」**タブでは、コンテナーの最近のログを表示したり、最新のログ (ログ・ファイルの末尾) をリアルタイムで確認することができます。 
	
	
	

## CF アプリ・ログのログ・フォーマット
{: #log_format_cf}

{{site.data.keyword.Bluemix_notm}} Cloud Foundry アプリのログは、以下のようなパターンの固定フォーマットで表示されます。

<code><var class="keyword varname">コンポーネント</var>/<var class="keyword varname">インスタンス ID</var>/<var class="keyword varname">メッセージ</var>/<var class="keyword varname">タイム・スタンプ</var></code>

各ログ項目には、以下のフィールドが含まれています。

| フィールド| 説明|
|-------|-------------|
| タイム・スタンプ| ログ・ステートメントの時刻。タイム・スタンプは、ミリ秒単位まで定義されます。|
| コンポーネント| ログを生成したコンポーネント。各種コンポーネントのリストについては、『[CF アプリのログ・ソース](cfapps/logging_cf_apps.html#logging_bluemix_cf_apps_log_sources)』を参照してください。<br> 各コンポーネント・タイプの後に、1 個のスラッシュと、アプリケーション・インスタンスを示す数字が続きます。0 は最初のインスタンスに割り当てられる数字、1 は 2 番目のインスタンスに割り当てられる数字であり、以下同様になります。|
| メッセージ| コンポーネントによって発行されたメッセージ。メッセージは、コンテキストによって異なります。|
{: caption="表 1. CF アプリのログ項目フィールド" caption-side="top"}


## コンテナー・ログのログ・フォーマット
{: #log_format_containers}

コンテナーのログは、以下のようなパターンの固定フォーマットで表示されます。

<code><var class="keyword varname">タイム・スタンプ</var>/<var class="keyword varname">マシン</var>/<var class="keyword varname">メッセージ</var>  </code>

各ログ項目には、以下のフィールドが含まれています。

| フィールド| 説明|
|-------|-------------|
| 日時| ログ・ステートメントの時刻。タイム・スタンプは、ミリ秒単位で定義されます。|
| マシン| コンテナーが実行されているホスト名。|
| メッセージ| 発行されたメッセージ。メッセージは、コンテキストによって異なります。|
{: caption="表 2. Docker コンテナーのログ項目フィールド" caption-side="top"}

