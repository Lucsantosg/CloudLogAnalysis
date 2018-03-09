---

copyright:
  years: 2017, 2018

lastupdated: "2018-02-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# Kubernetes クラスター内のリソースのロギング
{: #containers_kubernetes}

{{site.data.keyword.Bluemix_notm}} の {{site.data.keyword.loganalysisshort}} サービスを使用して、Kubernetes クラスター内にあるリソースのログを表示、フィルタリング、および分析できます。
{:shortdesc}

デフォルトでは、クラスターから {{site.data.keyword.loganalysisshort}} サービスへのログの送信は自動的には有効になりません。**注:** これは、新しいクラスターに対して最近行われた変更です。以前は、クラスターを作成すると、コンテナー・プロセスが STDOUT (標準出力) および STDERR (標準エラー) に出力する情報は {{site.data.keyword.containershort}} によって自動的に収集され、{{site.data.keyword.loganalysisshort}} サービスに転送されていました。現在、ログを {{site.data.keyword.loganalysisshort}} サービスに自動的に転送するには、クラスター内に 1 つ以上のロギング構成を作成する必要があります。

クラスター・ログを処理するときには、以下の情報を考慮してください。

* 情報を STDOUT および STDERR に送信することが、コンテナーの情報を公開するための標準の Docker 規則です。
* コンテナーのログは、クローラーを使用して、コンテナーの外部からモニターおよび転送されます。 
* データは、クローラーによって {{site.data.keyword.Bluemix_notm}} 内のマルチテナント Elasticsearch に送信されます。 
* STDOUT および STDERR のログ、他のアプリケーション・ログ、ワーカー・ノード・ログ、Kubernetes システム・コンポーネント・ログ、および Ingress コントローラー・ログを {{site.data.keyword.loganalysisshort}} サービスに転送するようにクラスターを構成できます。詳しくは、『[追加アプリケーション・ログおよびクラスター・ログの収集](/docs/services/CloudLogAnalysis/containers/containers_kubernetes.html#collect_logs)』を参照してください。

## Public でのロギングについて
{: #public}

{{site.data.keyword.Bluemix_notm}} では、Public において、{{site.data.keyword.containershort}} によって自動的に収集されるコンテナー・ログおよび Kubernetes クラスター・ログを、{{site.data.keyword.loganalysisshort}} サービスを使用して保管および分析することができます。

1 つのアカウント内に 1 つ以上の Kubernetes クラスターを持つことができます。 クラスターがプロビジョンされるとすぐに、{{site.data.keyword.containershort}} によってログが自動的に収集されます。 

* アプリケーション・ログの収集は、ポッドがデプロイされるとすぐに行われます。 
* コンテナー・プロセスが STDOUT (標準出力) および STDERR (標準エラー) に出力する情報は {{site.data.keyword.containershort}} によって自動的に収集されます。

{{site.data.keyword.loganalysisshort}} サービスでの分析にそれらのログを使用できるようにするには、{{site.data.keyword.loganalysisshort}} にクラスター・ログを転送するようにクラスターを構成する必要があります。ログは、アカウント・ドメインまたはアカウント内のスペース・ドメインに転送できます。

* 米国南部地域で使用可能なクラスターは、米国南部地域で使用可能な {{site.data.keyword.loganalysisshort}} サービスにログを送信します。
* 米国東部地域で使用可能なクラスターは、米国南部地域で使用可能な {{site.data.keyword.loganalysisshort}} サービスにログを送信します。
* ドイツ地域で使用可能なクラスターは、ドイツ地域で使用可能な {{site.data.keyword.loganalysisshort}} サービスにログを送信します。
* シドニー地域で使用可能なクラスターは、シドニー地域で使用可能な {{site.data.keyword.loganalysisshort}} サービスにログを送信します。
* 英国地域で使用可能なクラスターは、ドイツ地域で使用可能な {{site.data.keyword.loganalysisshort}} サービスにログを送信します。


Kibana でクラスターのログ・データを分析するときには、以下の情報を考慮してください。

* ログの表示に使用する {{site.data.keyword.loganalysisshort}} インスタンスがプロビジョンされている Public 地域で Kibana を起動する必要があります。 
* 使用するユーザー ID には、ログを表示する許可が必要です。 

    アカウント・ドメイン内のログを表示するには、ユーザーは {{site.data.keyword.loganalysisshort}} サービスのための IAM ポリシーを必要とします。 ユーザーには**ビューアー**の許可が必要です。 
    
    スペース・ドメイン内のログを表示するユーザーには CF 役割が必要です。 詳しくは、『[ログを表示するユーザーに必要な役割](/docs/services/CloudLogAnalysis/kibana/analyzing_logs_Kibana.html#roles)』を参照してください。

長期保管のログ・データ (Log Collection) を管理するには、ご使用のユーザー ID が、{{site.data.keyword.loganalysisshort}} サービスと連携するための IAM ポリシーを持っている必要があります。 ご使用のユーザー ID が、**管理者**または**エディター**の許可を持っている必要があります。  詳しくは、『[ログを管理するユーザーに必要な役割](/docs/services/CloudLogAnalysis/manage_logs.html#roles)』を参照してください。

**注:** Kubernetes クラスターで作業する場合、名前空間 *ibm-system* および *kube-system* は予約済みです。 これらの名前空間で使用可能なリソースの許可を作成、削除、または変更しないでください。 これらの名前空間のログは、{{site.data.keyword.IBM_notm}} の使用を目的としています。




### ログをアカウント・ドメインに転送するクラスターのロギングの概略
{: #acc}


以下の図は、クラスターがログをアカウント・ドメインに転送する場合に、Public の {{site.data.keyword.containershort}} で行われるロギングの概略を示しています。

![Kubernetes クラスターにデプロイされたコンテナーのコンポーネント概要図](images/containers_kube.png "Kubernetes クラスターにデプロイされたコンテナーのコンポーネント概要図")



### ログをスペース・ドメインに転送するクラスターのロギングの概略
{: #space}

以下の図は、クラスターがログをスペース・ドメインに転送する場合に、Public の {{site.data.keyword.containershort}} で行われるロギングの概略を示しています。

![Kubernetes クラスターにデプロイされたコンテナーのコンポーネント概要図](images/containers_kube_1.png "Kubernetes クラスターにデプロイされたコンテナーのコンポーネント概要図")

   



## Dedicated でのロギングについて
{: #dedicated}

{{site.data.keyword.Bluemix_notm}} では、Dedicated で{{site.data.keyword.containershort}} によって自動的に収集されるコンテナー・ログおよび Kubernetes クラスター・ログを、Public で {{site.data.keyword.loganalysisshort}} サービスを使用して保管および分析することができます。

以下の情報を考慮してください。

* 1 つのアカウント内に 1 つ以上の Kubernetes クラスターを持つことができます。 クラスターがプロビジョンされるとすぐに、{{site.data.keyword.containershort}} によってログが自動的に収集されます。 
* {{site.data.keyword.loganalysisshort}} サービスからアプリケーション・ログおよびクラスター・ログを表示するには、クラスター内に 1 つ以上のロギング構成を定義する必要があります。各構成エントリーに、{{site.data.keyword.loganalysisshort}} サービスに転送するログ情報の種類を定義します。例えば、STDOUT および STDERR のログ・データは、ポッドがデプロイされるとすぐに収集されます。これらのログを転送するには、タイプが*コンテナー* のログ・ソースのロギング構成を定義する必要があります。
* ロギング構成を定義するときに、ログの送信先をアカウント・ドメインにするか、またはスペース・ドメインにするかを決定します。**注:** 現在、アカウント・ドメインには 1 日当たり 500 MB の検索割り当て量制限があるほか、長期保管を目的にログを Log Collection 内に保管することはできません。より大きなログを検索したり、Log Collection 内にログを保管したりできるようにするには、ログをスペース・ドメインに送信してください。
* ログをアカウント・ドメインに送信するためのロギング構成を定義すると、ログは、Dedicated {{site.data.keyword.containershort}} が実行されている、同じ Public 地域内のアカウント・ドメインに転送されます。

    米国南部地域で使用可能なクラスターは、米国南部地域で使用可能な {{site.data.keyword.loganalysisshort}} サービスにログを送信します。</br>
    米国東部地域で使用可能なクラスターは、米国南部地域で使用可能な {{site.data.keyword.loganalysisshort}} サービスにログを送信します。</br>
    ドイツ地域で使用可能なクラスターは、ドイツ地域で使用可能な {{site.data.keyword.loganalysisshort}} サービスにログを送信します。</br>
    シドニー地域で使用可能なクラスターは、シドニー地域で使用可能な {{site.data.keyword.loganalysisshort}} サービスにログを送信します。</br>
    英国地域で使用可能なクラスターは、ドイツ地域で使用可能な {{site.data.keyword.loganalysisshort}} サービスにログを送信します。


Kibana でクラスターのログ・データを表示および分析するときには、以下の情報を考慮してください。

* {{site.data.keyword.loganalysisshort}} インスタンスがプロビジョンされている Cloud Public 地域に対して Kibana を起動する必要があります。 
* ご使用のユーザー ID が、{{site.data.keyword.loganalysisshort}} サービスと連携するための IAM ポリシーを持っている必要があります。 アカウント・ドメイン内のログを表示するには、**ビューアー**の許可が必要です。  

長期保管のログ・データ (Log Collection) を管理するには、ご使用のユーザー ID が、{{site.data.keyword.loganalysisshort}} サービスと連携するための IAM ポリシーを持っている必要があります。 **管理者**または**エディター**の許可を持っている必要があります。  

以下の図は、Dedicated での {{site.data.keyword.containershort}} のロギングの概略を示します。

![Kubernetes クラスターにデプロイされたコンテナーのコンポーネント概要図](images/containers_kube_dedicated.png "Kubernetes クラスターにデプロイされたコンテナーのコンポーネント概要図")



## ログ・ソース
{: #log_sources}


ログを {{site.data.keyword.loganalysisshort}} サービスに転送するようにクラスターを構成できます。以下の表に、ログを {{site.data.keyword.loganalysisshort}} サービスに転送するために有効にできる各種のログ・ソースをリストします。

<table>
  <caption>Kuberenetes クラスターのログ・ソース</caption>
  <tr>
    <th>ログ・ソース</th>
	<th>説明</th>
	<th>ログ・パス</th>
  </tr>
  <tr>
    <td>コンテナー</td>
	<td>コンテナー・ログ。</td>
	<td>標準出力 (stdout) および標準エラー出力 (stderr) のログ。</td>
  </tr>
  <tr>
    <td>アプリケーション</td>
	<td>Kubernetes クラスターで実行される独自のアプリケーションのログ。</td>
	<td>`/var/log/apps/**/*.log`  </br>`/var/log/apps/**/*.err`</br>**注:** ポッドの場合、ログは、`/var/logs/apps/` 内または `/var/logs/apps/` の下の任意のサブディレクトリーに書き込むことができます。ワーカーの場合は、アプリがポッド内でログを書き込んでいるポッド内のディレクトリーに `/var/log/apps/` をマウントする必要があります。</td>
  </tr>
  <tr>
    <td>ワーカー</td>
	<td>Kubernetes クラスター内の仮想マシン・ワーカー・ノードのログ。 </td>
	<td>`/var/log/syslog` </br>`/var/log/auth.log`</td>
  </tr>
  <tr>
    <td>Kubernetes システム・コンポーネント</td>
	<td>Kubernetes システム構成要素のログ。</td>
	<td>*/var/log/kubelet.log* </br>*/var/log/kube-proxy.log*</td>
  </tr>
  <tr>
    <td>Ingress コントローラー</td>
	<td>Kubernetes クラスターに送信されるネットワーク・トラフィックを管理する Ingress コントローラーのログ。</td>
	<td>`/var/log/alb/ids/*.log` </br>`/var/log/alb/ids/*.err` </br>`/var/log/alb/customerlogs/*.log` </br>`/var/log/alb/customerlogs/*.err`</td>
  </tr>
</table>


## アプリケーション・ログを転送する場合の考慮事項
{: #forward_app_logs}

アプリケーション・ログのログ転送を有効にするには、**「ログ・ソース」**を**「アプリケーション」** に設定して、クラスターのロギング構成を定義する必要があります。

アプリケーション・ログ転送に関する次の点を確認してください。

* ホスト・ノード上の特定のディレクトリーにあるログを転送できます。これを行うには、マウント・パスを使用してコンテナーにホスト・パス・ボリュームをマウントします。このマウント・パスは、アプリケーション・ログの送信先となる、コンテナー上のディレクトリーとして機能します。ボリューム・マウントを作成すると、事前定義されたホスト・パス・ディレクトリー `/var/log/apps` が自動的に作成されます。

    例えば、デプロイメント記述子の volumeMounts セクションと volumes セクションのサンプルを参照してください。

    ```
    volumeMounts:
            - mountPath: /var/app
              name: application-log
    volumes:
        - name: application-log
          hostPath:
            path: /var/log/apps

    ```
    {: codeblock}

* ログは、`/var/log/apps` パスから再帰的に読み込まれます。`/var/log/apps` パスのサブディレクトリー内にもアプリケーション・ログを書き込むことができます。
    
* ファイル拡張子 **.log** または **.err** を持つアプリケーション・ログ・ファイルのみが転送されます。

* ログ転送を初めて有効にしたとき、アプリケーション・ログは先頭から読み取られる代わりに、最新のもの (末尾) から取得されます。 

    アプリケーション・ロギングが有効になる前に既に存在していたログの内容は読み取られません。ロギングが有効になった時点のログから読み取りが開始されます。ただし、ログ転送を初回に有効化した後では、ログは常に、前の続きから取得されます。

* 複数のコンテナーに */var/log/apps* ホスト・パス・ボリュームをマウントすると、すべてのコンテナーがそのホスト (ワーカー) 上の同じディレクトリーにログを書き込みます。コンテナーの書き込み先が同じファイル名である場合、コンテナーはホスト上のまったく同じファイルに書き込むので、ファイルは上書きされます。 

    **注:** すべてのコンテナーが同じファイル名に書き込む場合、ReplicaSets が 1 より大きいアプリケーション・ログを転送する目的で、ログ・ソースが*アプリケーション* に設定されたログ転送を有効にすることはしないでください。代わりに、アプリケーションからログを STDOUT および STDERR に書き込むことができ、そうするとログはコンテナー・ログとしてピックアップされます。STDOUT および STDERR に書き込まれるアプリケーション・ログを転送するには、ログ・ソースを*コンテナー* に設定したログ転送を有効にしてください。



## ログ・ドメインにログを転送する場合の考慮事項
{: #forward_logs_domain}

ログ・ファイルを {{site.data.keyword.loganalysisshort}} サービスに転送するようにクラスターを構成できます。 

ログの転送先は、アカウント・ドメインまたはスペース・ドメインにできます。

ログをスペース・ドメインとアカウント・ドメインのいずれに転送するかを決定する際には、以下の情報を考慮してください。

* ログをアカウント・ドメインに送信する場合、検索割り当て量は 1 日当たり 500 MB バイトであり、長期保管のためにログを Log Collection に保管することはできません。
* ログをスペース・ドメインに送信する場合は、1 日当たりの検索割り当て量を定義する {{site.data.keyword.loganalysisshort}} サービス・プランを選択でき、長期保管のためにログを Log Collection 内に保管できます。



## アプリケーション・ログおよびクラスター・ログの転送
{: #forward_logs}

ログを {{site.data.keyword.loganalysisshort}} サービスに転送するようにクラスターを構成するには、以下のステップを実行する必要があります。

1. ロギング構成をクラスターに追加するための許可がユーザー ID にあることを確認します。 

    クラスターを管理する許可が設定された {{site.data.keyword.containershort}} の IAM ポリシーが割り当てられているユーザーのみが、クラスターのロギング構成を作成、更新、または削除できます。管理者、オペレーター のいずれかの役割が必要です。

2. 端末を開き、クラスター・コンテキストをセットアップします。

3. クラスターのロギング構成を作成します。どのクラスター・ログを Log Analysis サービスに転送するのかを選択できます。

    stdout および stderr の自動ログ収集および転送を有効にするには、[コンテナー・ログの自動ログ収集および転送の有効化](/docs/services/CloudLogAnalysis/containers/containers_kube_other_logs.html#containers)を参照してください。</br>
    アプリケーション・ログの自動ログ収集および転送を有効にするには、[アプリケーション・ログの自動ログ収集および転送の有効化](/docs/services/CloudLogAnalysis/containers/containers_kube_other_logs.html#apps)を参照してください。</br>
    ワーカー・ログの自動ログ収集および転送を有効にするには、[ワーカー・ログの自動ログ収集および転送の有効化](/docs/services/CloudLogAnalysis/containers/containers_kube_other_logs.html#workers)を参照してください。</br>
    Kubernetes システム・コンポーネント・ログの自動ログ収集および転送を有効にするには、[Kubernetes システム・コンポーネント・ログの自動ログ収集および転送の有効化](/docs/services/CloudLogAnalysis/containers/containers_kube_other_logs.html#system)を参照してください。</br>
    Kubernetes Ingress コントローラー・ログの自動ログ収集および転送を有効にするには、[Kubernetes Ingress コントローラー・ログの自動ログ収集および転送の有効化](/docs/services/CloudLogAnalysis/containers/containers_kube_other_logs.html#controller)を参照してください。
    
4. ログをスペースに転送する場合、組織およびスペースの {{site.data.keyword.containershort}} キー所有者にも Cloud Foundry (CF) 許可を付与する必要があります。キー所有者には、組織の *orgManager* 役割と、スペースの *SpaceManager* と*開発者* の役割が必要です。

ログ・ファイルを {{site.data.keyword.loganalysisshort}} サービスに転送するようにクラスターを構成する方法について詳しくは、『[クラスター・ログの自動収集の有効化](/docs/services/CloudLogAnalysis/containers/containers_kube_other_logs.html#containers_kube_other_logs)』セクションを参照してください。


## {{site.data.keyword.Bluemix_notm}} のカスタム・ファイアウォール構成に対するネットワーク・トラフィックの構成
{: #ports}

追加ファイアウォールをセットアップしたか、または、{{site.data.keyword.Bluemix_notm}} インフラストラクチャー (SoftLayer) のファイアウォール設定をカスタマイズした場合、ワーカー・ノードから {{site.data.keyword.loganalysisshort}} サービスへの発信ネットワーク・トラフィックを許可する必要があります。 

カスタマイズしたファイアウォール内の次の IP アドレスに対して、各ワーカーから {{site.data.keyword.loganalysisshort}} サービスへ TCP ポート 443 および TCP ポート 9091 を開く必要があります。

<table>
  <tr>
    <th>地域</th>
    <th>取り込み URL</th>
	<th>パブリック IP アドレス</th>
  </tr>
  <tr>
    <td>ドイツ</td>
	<td>ingest-eu-fra.logging.bluemix.net</td>
	<td>158.177.88.43 <br>159.122.87.107</td>
  </tr>
  <tr>
    <td>英国</td>
	<td>ingest.logging.eu-gb.bluemix.net</td>
	<td>169.50.115.113</td>
  </tr>
  <tr>
    <td>米国南部</td>
	<td>ingest.logging.ng.bluemix.net</td>
	<td>169.48.79.236 <br>169.46.186.113</td>
  </tr>
  <tr>
    <td>シドニー</td>
	<td>ingest-au-syd.logging.bluemix.net</td>
	<td>130.198.76.125 <br>168.1.209.20</td>
  </tr>
</table>



## ログの検索
{: #log_search}

デフォルトでは、{{site.data.keyword.Bluemix_notm}} では、1 日当たり 500 MB までのログを Kibana を使用して検索できます。 

より大きなログを検索するために、{{site.data.keyword.loganalysisshort}} サービスを使用できます。 サービスには複数のプランが用意されています。 ログ検索の機能はプランによって異なります。例えば、*Log Collection *プランでは、1 日当たり 1 GB までのデータを検索できます。 選択可能なプランについて詳しくは、『[サービス・プラン](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans)』を参照してください。

ログを検索するときには、Kibana で使用可能な次のフィールドを考慮してください。

すべてのログ項目に共通するフィールド:

<table>
  <caption>共通フィールドのリスト</caption>
  <tr>
    <th>フィールド名</th>
	<th>説明</th>
	<th>値</th>
  </tr>
  <tr>
    <td>ibm-containers.region_str</td>
	<td>クラスターが使用可能な地域</td>
	<td>例えば、米国南部地域で使用可能なクラスターの場合、値は `us-south` です。</td>
  </tr>
  <tr>
    <td>ibm-containers.account_id_str</td>
	<td>アカウント ID</td>
	<td></td>
  </tr>
  <tr>
    <td>ibm-containers.cluster_id_str</td>
	<td>クラスター ID</td>
	<td></td>
	<tr>
    <td>ibm-containers.cluster_name_str</td>
	<td>クラスター名</td>
	<td></td>
  </tr>
</table>

コンテナー stdout および stderr のログの分析に役立つフィールド:

<table>
  <caption>アプリケーションのフィールドのリスト</caption>
  <tr>
    <th>フィールド名</th>
	<th>説明</th>
	<th>値</th>
  </tr>
  <tr>
    <td>kubernetes.container_name_str</td>
	<td>コンテナーの名前</td>
	<td></td>
  </tr>
  <tr>
    <td>kubernetes.namespace_name_str</td>
	<td>クラスター内でアプリケーションが実行されている名前空間</td>
	<td></td>
  </tr>
  <tr>
    <td>stream_str</td>
	<td>ログのタイプ</td>
	<td>*stdout* </br>*stderr*</td>
  </tr>
</table>

ワーカー・ログの分析に役立つフィールド:

<table>
  <caption>ワーカー関連フィールドのリスト</caption>
  <tr>
    <th>フィールド名</th>
	<th>説明</th>
	<th>値</th>
  </tr>
  
  <tr>
    <td>filename_str</td>
	<td>ファイルのパスおよび名前</td>
	<td>*/var/log/syslog*  </br>*/var/log/auth.log*</td>
  </tr>
  <tr>
    <td>tag_str</td>
	<td>ログのタイプ</td>
	<td>*logfiles.worker.var.log.syslog* </br>*logfiles.worker.var.log.auth.log*</td>
  </tr>
  <tr>
    <td>worker_str</td>
	<td>ワーカー名</td>
	<td>例: *w1*</td>
  </tr>
</table>

Kubernetes システム・コンポーネント・ログの分析に役立つフィールド:

<table>
  <caption>Kubernetes システム・コンポーネント関連フィールドのリスト</caption>
  <tr>
    <th>フィールド名</th>
	<th>説明</th>
	<th>値</th>
  </tr>
  <tr>
    <td>tag_str</td>
	<td>ログのタイプ</td>
	<td>*logfiles.kubernetes.var.log.kubelet.log* </br>*logfiles.kubernetes.var.log.kube-proxy.log*</td>
  </tr>
  <tr>
    <td>filename_str</td>
	<td>ファイルのパスおよび名前</td>
	<td>*/var/log/kubelet.log* </br>*/var/log/kube-proxy.log*</td>
  </tr>
 </table>

Ingress コントローラー・ログの分析に役立つフィールド:
 
<table>
  <caption>Ingress コントローラー関連フィールドのリスト</caption>
  <tr>
    <th>フィールド名</th>
	<th>説明</th>
	<th>値</th>
  </tr>
 <tr>
    <td>tag_str</td>
	<td>ログのタイプ</td>
	<td></td>
  </tr>
  <tr>
    <td>filename_str</td>
	<td>ファイルのパスおよび名前</td>
	<td>*/var/log/alb/ids/*.log* </br>*/var/log/alb/ids/*.err* </br>*/var/log/alb/customerlogs/*.log* </br>*/var/log/alb/customerlogs/*.err*</td>
  </tr>
</table>


## メッセージ内のフィールドを Kibana 検索フィールドとして使用できるようにするためのログの送信
{: #send_data_in_json}

デフォルトで、コンテナーのロギングは自動的に有効になります。 Docker ログ・ファイルのすべての項目は、Kibana で **message** フィールドに表示されます。 コンテナー・ログ項目の一部である特定のフィールドを使用して、Kibana でデータをフィルター操作および分析する必要がある場合は、有効な JSON フォーマットの出力を送信するようにアプリケーションを構成します。 例えば、JSON フォーマットのメッセージを  STDOUT (標準出力) および STDERR (標準エラー) に記録します。

メッセージで使用可能な各フィールドは構文解析されて、その値に一致するタイプのフィールドに変換されます。 例えば、以下の JSON メッセージの各フィールドをご覧ください。
    
```
{"field1":"string type",
        "field2":123,
        "field3":false,
        "field4":"4567"
    }
```
{: codeblock}
    
これらの各フィールドは、以下のように、フィルター操作と検索に使用できるフィールドとして使用可能です。
    
* `field1` は、ストリング型の `field1_str` として構文解析されます。
* `field2` は、整数型の `field1_int` として構文解析されます。
* `field3` は、ブール型の `field3_bool` として構文解析されます。
* `field4` は、ストリング型の `field4_str` として構文解析されます。
    

## Log Collection へのログの保管
{: #log_collection}

ログを操作する場合、{{site.data.keyword.Bluemix_notm}} でのデフォルトの動作に関する以下の情報を考慮してください。

* {{site.data.keyword.Bluemix_notm}} はログ・データを最大 3 日間保管します。
* 1 日に最大で 500 MB のデータが保管されます。 500 MB の上限を超えるログは破棄されます。 上限割り当ては、毎日午前 12:30 (UTC) にリセットされます。
* 1.5 GB までのデータを最大 3 日間検索可能です。 ログ・データは、データが 1.5 GB に達するか 3 日が過ぎると、ロールオーバーします (先入れ先出し)。
* ログは、長期保管のために Log Collection 内には保管されません。

{{site.data.keyword.loganalysisshort}} サービスには、必要な期間 Log Collection にログを保管できる追加プランがあります。 各プランの料金について詳しくは、『[サービス・プラン](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans)』を参照してください。 

Log Collection でログを管理するには、以下の情報を考慮してください。

* Log Collection 内でログを保持する日数を定義するために使用できるログ保存ポリシーを構成できます。 詳しくは、『[ログ保存ポリシー](/docs/services/CloudLogAnalysis/log_analysis_ov.html#policies)』を参照してください。
* Log Collection CLI または Log Collection API を使用して、ログを手動で削除できます。 
* Log Collection 内のログを管理するには、ユーザーに、{{site.data.keyword.Bluemix_notm}} の {{site.data.keyword.loganalysisshort}} サービスを使用して処理するための許可が設定された IAM ポリシーが必要です。詳しくは、[IAM 役割](/docs/services/CloudLogAnalysis/security_ov.html#iam_roles)を参照してください。

## ログの表示と分析
{: #logging_containers_ov_methods}

ログ・データを分析するには、Kibana を使用して高度な分析タスクを実行します。 Kibana は、分析および視覚化のためのオープン・ソース・プラットフォームであり、 さまざまなグラフ (図表や表など) でデータのモニター、検索、分析、および視覚化に使用することができます。 詳しくは、『[Kibana でのログの分析](/docs/services/CloudLogAnalysis/kibana/analyzing_logs_Kibana.html#analyzing_logs_Kibana)』を参照してください。

* Web ブラウザーから Kibana を直接起動できます。 詳しくは、『[Web ブラウザーから Kibana へのナビゲート](/docs/services/CloudLogAnalysis/kibana/launch.html#launch_Kibana_from_browser)』を参照してください。
* クラスターのコンテキストで {{site.data.keyword.Bluemix_notm}} UI から Kibana を起動できます。 詳しくは、『[Kubernetes クラスターにデプロイされたコンテナーのダッシュボードから Kibana へのナビゲート](/docs/services/CloudLogAnalysis/kibana/launch.html#launch_Kibana_for_containers_kube)』を参照してください。

コンテナーで実行されているアプリのログ・データを、JSON フォーマットで Docker ログ・コレクターに転送すると、JSON フィールドを使用して Kibana でログ・データを検索および分析することができます。 詳しくは、『[カスタム・フィールドを Kibana 検索フィールドとして構成](logging_containers_ov.html#send_data_in_json)』を参照してください。

Kibana でログを表示するには、以下の情報を考慮してください。

* スペース・ドメイン内のログを表示するユーザーは、クラスターに関連付けられたスペースの**監査員**の役割または**開発者**の役割を持っている必要があります。
* アカウント・ドメイン内のログを表示するユーザーは、{{site.data.keyword.loganalysisshort}} サービスと連携するための IAM ポリシーを持っている必要があります。 ログ項目の表示が許可される最小限の役割は**ビューアー**です。



## チュートリアル: Kubernetes クラスターにデプロイされているアプリのログを Kibana で分析
{: #tutorial1}

Kibana を使用した、Kubernetes クラスターにデプロイされているコンテナーのログの分析方法を学習するには、[Kubernetes クラスターにデプロイされているアプリのログを Kibana で分析](/docs/services/CloudLogAnalysis/tutorials/container_logs.html#container_logs)を参照してください。
