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

# バージョン 5.1 への ELK Stack のアップグレード後のマイグレーション考慮事項 
{: #es17_to_es51}

{{site.data.keyword.Bluemix}} において、ElasticSearch (ELK) Stack はバージョン 1.7 からバージョン 2.3 にアップグレードされました。新機能 (ログを取り込むための URL、および Kibana でログを分析するための新規 URL) が使用可能になりました。詳しくは、[ElasticSearch 5.1 ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.elastic.co/guide/en/elasticsearch/reference/5.1/index.html "外部リンク・アイコン") を参照してください。
{:shortdesc}

この機能は、Kubernetes クラスターにデプロイされた Docker コンテナーでロギング・サービスを使用するユーザーには適用されません。これらのコンテナーは、既に ELK Stack バージョン 2.3 を使用しています。

## 地域
{: #regions}

ELK Stack バージョン 5.1 は以下の地域で使用可能です。

* 米国南部


## 新機能
{: #features}

1. ログおよびメトリックを処理するためのさまざまな URL。

    ELK 1.7 では、ログおよびメトリックの表示およびモニターを行うために、同じ URL が共有されていました。ELK 5.1 にアップグレードすると、ログとメトリックを別々の URL で表示できるようになります。詳しくは、『[ロギング URL](#logging)』を参照してください。
    
2. Kibana 5.1 のサポート 

    Kibana は、{{site.data.keyword.Bluemix_notm}} UI から起動するか、または、新規ロギング URL から直接起動することができます。詳しくは、『[Kibana でのログの分析](/docs/services/CloudLogAnalysis/kibana/analyzing_logs_Kibana.html#analyzing_logs_Kibana)』を参照してください。
    
    Kibana 3 は推奨されません。Kibana 3 は [ELK 1.7 ロギング URL](#logging) を介して起動できます。地域ごとに異なる URL があります。**注:** 現在、Kibana 3 ダッシュボードを Kibana 5.1 ダッシュボードにマイグレーションするため、および両者を比較するために、Kibana 3 ダッシュボードへのアクセスが可能になっています。 
    
    ELK 1.7 スタック上に構築された Kibana ダッシュボードがある場合、それらを ELK 5.1 環境にマイグレーションする必要があります。
    
    Kibana 5.1 について詳しくは、「[Kibana User Guide ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.elastic.co/guide/en/kibana/5.1/index.html "外部リンク・アイコン"){: new_window}」を参照してください。
    
3. カスタム・フィールドへのタイプ・ベースの接尾語の追加

    カスタム・フィールドを Kibana 検索フィールドとして構成できます。メッセージ中にある各フィールドが構文解析され、その値に一致するタイプのフィールドに変換されます。例えば、以下の JSON メッセージの各フィールドをご覧ください。 

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

    **注:** この機能は、Elastic 5.1 でのみ使用可能です。Kibana3 ダッシュボードの中断を回避するようにするために、この機能は Elastic 1.7 では使用できません。


## ロギング 
{: #logging}

{{site.data.keyword.Bluemix_notm}} へのログの送信、および Kibana でのデータの分析に、異なる URL が使用されます。

以下の表に、米国南部地域の新規 URL をリストします。

<table>
  <caption>米国南部地域の URL</caption>
    <tr>
      <th>タイプ </th>
      <th>ELK 1.7 </th>
	  <th>ELK 5.1 </th>
    </tr>
  <tr>
    <td>ログの取り込み URL</td>
    <td>logs.opvis.bluemix.net:9091</td>
	<td>ingest.logging.ng.bluemix.net:9091</td>
  </tr>
   <tr>
    <td>ログ分析用の Kibana URL</td>
    <td>https://logmet.ng.bluemix.net</td>
	<td>https://logging.ng.bluemix.net</td>
  </tr>
</table>

