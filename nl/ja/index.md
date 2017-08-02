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

# 概説のチュートリアル
{: #getting-started-with-cla}

この概説チュートリアルでは、{{site.data.keyword.loganalysislong}} サービスを使用した高度な分析タスクを実行するためのステップを順に説明します。ここでは、Kubernetes クラスターにデプロイされたアプリに関するコンテナー・ログの検索方法および分析方法を説明します。
{:shortdesc}

## 始める前に
{: #prereqs}

[{{site.data.keyword.Bluemix_notm}} アカウント](https://console.bluemix.net/registration/)を作成します。使用するユーザー ID は、{{site.data.keyword.Bluemix_notm}} アカウントのメンバーまたは所有者でなければならず、そのアカウントは、Kubernetes クラスターの作成、クラスターへのアプリケーションのデプロイ、および、Kibana での高度な分析のための {{site.data.keyword.Bluemix_notm}} でのログの照会を実行できる権限を持っている必要があります。

コマンド・ラインから Kubernetes クラスターの管理およびアプリのデプロイを実行できる端末セッションを開きます。このチュートリアルの例では Ubuntu Linux システムを使用しています。

コマンド・ラインから {{site.data.keyword.containershort}} を管理するには、ご使用のローカル環境に [CLI プラグインをインストール](/docs/containers/cs_cli_install.html#cs_cli_install_steps)します。 



## ステップ 1: Kubernetes クラスターにアプリをデプロイする
{: #step1}

1. [Kubernetes クラスターを作成します](/docs/containers/cs_cluster.html#cs_cluster_ui)。

2. Linux 端末で[クラスター・コンテキストをセットアップ](/docs/containers/cs_cli_install.html#cs_cli_configure)します。コンテキストを設定すると、Kubernetes クラスターを管理し、Kubernetes クラスターにアプリケーションをデプロイできるようになります。

3. Kubernetes クラスター内でサンプル・アプリをデプロイし、実行します。[演習 1 の手順を実行](/docs/containers/cs_tutorials.html#cs_apps_tutorial)してください。

    以下のアプリは Hello World Node.js アプリです。

    ```
    var express = require('express')
    var app = express()

    app.get('/', function(req, res) {
      res.send('Hello world! Your app is up and running in a cluster!\n')
    })
    app.listen(8080, function() {
      console.log('Sample app is listening on port 8080.')
    })
    ```
	{: codeblock}

    アプリがデプロイされたら、アプリが STDOUT (標準出力) および STDERR (標準エラー出力) に送信するすべてのログ項目のログ収集が自動的に有効になります。 

    このサンプル・アプリでは、ブラウザーでアプリをテストすると、アプリはメッセージ `Sample app is listening on port 8080.` を標準出力に書き込みます。

## ステップ 2: Kibana ダッシュボードへのナビゲート
{: #step2}

あるクラスターのログ・データを分析するには、そのクラスターが作成されたクラウド・パブリック地域の Kibana にアクセスする必要があります。 

例えば、米国南部地域で Kibana を起動するには、以下の URL にナビゲートします。

```
https://logging.ng.bluemix.net/
```
{: codeblock}

    
    
## ステップ 3: Kibana でログ・データを分析する
{: #step3}

1. **「Discover」**ページで、表示されるイベントを確認します。 

    Hello-World サンプル・アプリケーションは 1 つのイベントを生成します。
    
    「Available fields」セクションには、フィールドのリストが表示されます。これらのフィールドを使用して、新しい照会を定義したり、ページに表示される表にリストされる項目をフィルター操作したりできます。
    
    以下の表に、新しい検索照会を定義するために使用できる共通フィールドを示します。この表には、サンプル・アプリによって生成されるイベントに対応するサンプル値も含まれています。
    
     <table>
              <caption>表 2. コンテナー・ログの共通フィールド</caption>
               <tr>
                <th align="center">フィールド</th>
                <th align="center">説明</th>
                <th align="center">例</th>
              </tr>
              <tr>
                <td>*docker.container_id_str*</td>
                <td> このフィールドの値は、Kubernetes クラスターのポッドでアプリを実行するコンテナーの GUID に対応します。</td>
                <td></td>
              </tr>
              <tr>
                <td>*ibm-containers.region_str*</td>
                <td>このフィールドの値は、このログ項目が収集される {{site.data.keyword.Bluemix_notm}} 地域に対応します。</td>
                <td>us-south</td>
              </tr>
              <tr>
                <td>*kubernetes.container_name_str*</td>
                <td>このフィールドの値は、コンテナーの名前を示します。</td>
                <td>hello-world-deployment</td>
              </tr>
              <tr>
                <td>*kubernetes.host*</td>
                <td>このフィールドの値は、インターネットからアプリにアクセスするために使用できるパブリック IP を示します。</td>
                <td>169.47.218.231</td>
              </tr>
              <tr>
                <td>*kubernetes.labels.label_name*</td>
                <td>ラベル・フィールドはオプションです。ラベルはなくてもよく、複数あってもかまいません。各ラベルは接頭部 `kubernetes.labels.` で始まり、*label_name* が続きます。</td>
                <td>サンプル・アプリでは、次の 2 つのラベルがあります。<br>* *kubernetes.labels.pod-template-hash_str* = 3355293961 <br>* *kubernetes.labels.run_str* =	hello-world-deployment  </td>
              </tr>
              <tr>
                <td>*kubernetes.namespace_name_str*</td>
                <td>このフィールドの値は、ポッドが実行されている Kubernetes 名前空間を示します。</td>
                <td>default</td>
              </tr>
              <tr>
                <td>*kubernetes.pod_id_str*</td>
                <td>このフィールドの値は、コンテナーが稼働しているポッドの GUID に対応します。</td>
                <td>d695f346-xxxx-xxxx-xxxx-aab0b50f7315</td>
              </tr>
              <tr>
                <td>*kubernetes.pod_name_str*</td>
                <td>このフィールドの値は、ポッド名を示します。</td>
                <td>hello-world-deployment-3xxxxxxx1-xxxxx8</td>
              </tr>
              <tr>
                <td>*message*</td>
                <td>これは、アプリケーションによってログに記録される完全なメッセージです。</td>
                <td>Sample app is listening on port 8080.</td>
              </tr>
        </table>
    
2. **「Discover」**ページでデータをフィルター操作します。  

    分析に使用できるすべての項目が表で示されます。リストされる項目は、「Search」バーに表示される検索照会に対応します。アスタリスク (*) は、このページに対して構成された期間内のすべての項目を表示する場合に使用される文字です。 
    
    例えば、Kubernetes 名前空間によってデータをフィルター操作するために、「Search」バーの照会を変更するとします。この場合、次のようにしてカスタム・フィールド *kubernetes.namespace_name_str* に基づくフィルターを追加します。
    
    1. *「Available fields」*セクションで、フィールド *kubernetes.namespace_name_str* を選択します。このフィールドの有効な値のサブセットが表示されます。    
    
    2. 値 **default** を選択します。これは、前のステップでサンプル・アプリをデプロイした名前空間です。
    
        値を選択すると、「Search」バーにフィルターが追加され、表には、選択したばかりの基準に一致する項目のみが表示されるようになります。     
    
    フィルターの編集シンボルを選択して、検索する名前空間の名前を変更できます。   
    
    以下の照会が表示されます。
    
    ```
	{
    "query": {
          "match": {
            "kubernetes.namespace_name_str": {
              "query": "default",
              "type": "phrase"
            }
          }
        }
    }
    ```
	{: codeblock}
    
    別の名前空間 *mynamespace1* にある項目を検索するには、照会を次のように変更します。
    
    ```
	{
    "query": {
          "match": {
            "kubernetes.namespace_name_str": {
              "query": "mynamespace1",
              "type": "phrase"
            }
          }
        }
    }
    ```
	{: codeblock}
    
    データが何も表示されない場合は、時間フィルターを変更してみてください。詳しくは、『[時間フィルターの設定](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#set_time_filter)』を参照してください。
    

詳しくは、『[Kibana でのログのフィルタリング](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#filter_logs)』を参照してください。


## 次のステップ
{: #next_steps}

次に、Kibana ダッシュボードを構築します。詳しくは、『[ダッシュボードを使用した Kibana でのログの分析](/docs/services/CloudLogAnalysis/kibana/analize_logs_dashboard.html#analize_logs_dashboard)』を参照してください。
                                                                                                                      

