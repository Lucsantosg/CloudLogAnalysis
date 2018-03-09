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

# バージョン 5.1 への Elastic スタックのアップグレード後のマイグレーション考慮事項 
{: #es17_to_es51}

{{site.data.keyword.Bluemix}} において、ElasticSearch (ELK) Stack はバージョン 1.7 からバージョン 5.1 にアップグレードされました。 新機能として、ログを取り込むための新規 URL、および Kibana でログを分析するための新規 URL が使用可能になりました。 詳しくは、[ElasticSearch 5.1 ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.elastic.co/guide/en/elasticsearch/reference/5.1/index.html) を参照してください。
{:shortdesc}

この機能は、Kubernetes クラスターにデプロイされた Docker コンテナーでロギング・サービスを使用するユーザーには適用されません。 

## 地域
{: #regions}

Elastic バージョン 5.1 は以下の地域で使用可能です。

* 英国
* 米国南部
* ドイツ
* シドニー


## 新機能
{: #features}

1. ログおよびメトリックを処理するためのさまざまな URL。

    Elastic 1.7 では、ログおよびメトリックの表示およびモニターを行うために、同じ URL が共有されていました。 Elastic 5.1 にアップグレードすると、ログとメトリックを別々の URL で表示できるようになります。 詳しくは、『[ロギング URL](#logging)』を参照してください。
    
2. Kibana 5.1 のサポート。

    Kibana は、{{site.data.keyword.Bluemix_notm}} UI から起動するか、または、新規ロギング URL から直接起動することができます。 詳しくは、『[Kibana ダッシュボードへのナビゲート](/docs/services/CloudLogAnalysis/kibana/launch.html#launch)』を参照してください。
    
    Kibana 3 および Kibana 4 は、非推奨です。
	
	**注:** 地域ごとに異なる URL があります。 ご使用のダッシュボードを Kibana 5.1 ダッシュボードにマイグレーションするため、および両者を比較するために、現在は英国において Kibana 4 ダッシュボードへのアクセスが可能になっています。 
    
    ダッシュボードを Elastic 5.1 環境にマイグレーションする必要があります。
    
    Kibana 5.1 について詳しくは、「[Kibana User Guide ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.elastic.co/guide/en/kibana/5.1/index.html){: new_window}」を参照してください。
    
3. カスタム・フィールドへのタイプ・ベースの接尾語の追加

    カスタム・フィールドを Kibana 検索フィールドとして構成できます。 メッセージ中にある各フィールドが構文解析され、その値に一致するタイプのフィールドに変換されます。 例えば、以下の JSON メッセージの各フィールドをご覧ください。 

    ```
    {"field1":"string type",
        "field2":123,
        "field3":false,
        "field4":"4567"
    }
    ```
    {: screen}
    
    これらの各フィールドは、以下のように、フィルター操作と検索に使用できるフィールドとして使用可能です。

    * field1 は、ストリング型の field1_str として構文解析されます。
    * field2 は、整数型の field1_int として構文解析されます。
    * field3 は、ブール型の field3_bool として構文解析されます。
    * field4 は、ストリング型の field4_str として構文解析されます。
    
    このサンプル JSON メッセージは、ロギング・サービスに送信したログです。 

    **注:** この機能は、Elastic 5.1 でのみ使用可能です。 Kibana3 ダッシュボードの中断を回避するようにするために、この機能は Elastic 1.7 では使用できません。


## ロギング URL
{: #logging}

{{site.data.keyword.Bluemix_notm}} へのログの送信、および Kibana でのデータの分析に、異なる URL が使用されます。

以下の表に、米国南部地域の URL をリストします。

<table>
  <caption>表 1. 米国南部地域の URL</caption>
    <tr>
      <th>タイプ</th>
      <th>Elastic 1.7 </th>
	    <th>Elastic 5.1 </th>
    </tr>
  <tr>
    <td>ログの取り込み URL</td>
    <td>logs.opvis.bluemix.net:9091</td>
  	<td>ingest.logging.ng.bluemix.net:9091</td>
  </tr>
   <tr>
    <td>ログ分析用の Kibana URL</td>
    <td>[https://logmet.ng.bluemix.net](https://logmet.ng.bluemix.net)</td>
	  <td>[https://logging.ng.bluemix.net](https://logging.ng.bluemix.net)</td>
  </tr>
</table>

以下の表に、英国地域の URL をリストします。

<table>
  <caption>表 2. 英国地域の URL</caption>
  <tr>
     <th>タイプ</th>
      <th>Elastic 1.7 </th>
	    <th>Elastic 5.1 </th>
  </tr>
  <tr>
     <td>ログの取り込み URL</td>
	   <td>logs.eu-gb.opvis.bluemix.net:9091</td>
	   <td>ingest.logging.eu-gb.bluemix.net:9091</td>
  </tr>
  <tr>
     <td>ログ分析用の Kibana URL</td>
	 <td>[https://logmet.eu-gb.bluemix.net](https://logmet.eu-gb.bluemix.net)</td>
	 <td>[https://logging.eu-gb.bluemix.net](https://logging.eu-gb.bluemix.net)</td>
  </tr>
</table>

以下の表に、フランクフルト地域の URL をリストします。

<table>
  <caption>表 3. フランクフルト地域の URL</caption>
  <tr>
     <th>タイプ</th>
      <th>Elastic 2.3 </th>
	    <th>Elastic 5.1 </th>
  </tr>
  <tr>
     <td>ログの取り込み URL</td>
	 <td>ingest.logging.eu-de.bluemix.net</td>
	 <td>ingest-eu-fra.logging.bluemix.net</td>
  </tr>
  <tr>
     <td>ログ分析用の Kibana URL</td>
	 <td>[https://logging.eu-de.bluemix.net](https://logging.eu-de.bluemix.net)</td>
	 <td>[https://logging.eu-fra.bluemix.net](https://logging.eu-fra.bluemix.net)</td>
  </tr>
</table>



