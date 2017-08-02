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


# エラー・メッセージ
{: #error_msgs}

{{site.data.keyword.Bluemix}} で {{site.data.keyword.loganalysisshort}} サービスを使用するときに、以下のエラー・メッセージが表示されることがあります。
{:shortdesc}

## BXNLG020001W
{: #BXNLG020001W}

**メッセージの説明**

{{site.data.keyword.loganalysisfull}} インスタンス {インスタンス GUID} について Bluemix スペース {スペース GUID} に割り振られた毎日の割り当て量に達しました。ログ検索ストレージについての現在の毎日の割り当ては 500MB です。これは 3 日間ログ検索ストレージに保存され、この間 Kibana での検索が可能です。1 日により多くのデータをログ検索ストレージに保管して、すべてのログをログ収集ストレージに保存できるようにプランをアップグレードするには、このスペースの {{site.data.keyword.loganalysisshort}} サービス・プランをアップグレードしてください。サービス・プランとプランのアップグレード方法について詳しくは、『[プラン](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans)』を参照してください。


**メッセージの説明** 

ライト・サービス・プランで割り振られたログ検索ストレージの割り当て量に達すると、ID *BXNLG020001W* のメッセージが表示されることがあります。ライト・プランは、{{site.data.keyword.Bluemix_notm}} スペースで {{site.data.keyword.loganalysisshort}} サービスをプロビジョンするとデフォルトで設定される補完的なサービス・プランです。ログ検索ストレージについての現在の毎日の割り当ては 500MB です。これは 3 日間ログ検索ストレージに保存され、この間 Kibana での検索が可能です。

**リカバリー**

1 日により多くのデータをログ検索ストレージに保管して、すべてのログをログ収集ストレージに保存できるようにプランをアップグレードするには、このスペースの {{site.data.keyword.loganalysisshort}} サービス・プランをアップグレードしてください。サービス・プランとプランのアップグレード方法について詳しくは、『[プラン](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans)』を参照してください。


## BXNLG020002W 
{: #BXNLG020002W}


**メッセージの説明**

{{site.data.keyword.loganalysisfull}} インスタンス {インスタンス GUID} について Bluemix スペース {スペース GUID} に割り振られた毎日の割り当て量に達しました。ログ検索ストレージについての現在の毎日の割り当ては XXX です。これは 3 日間保存され、この間 Kibana での検索が可能です。これは、ログ収集ストレージでのログ保存ポリシーには影響を与えません。1 日により多くのデータをログ検索ストレージに保管できるようにプランをアップグレードするには、このスペースの {{site.data.keyword.loganalysisshort}} サービス・プランをアップグレードしてください。サービス・プランとプランのアップグレード方法について詳しくは、『[プラン](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans)』を参照してください。

XXX は、現在のプランで検索可能なデータのサイズを表します。

**メッセージの説明** 

{{site.data.keyword.loganalysisfull}} インスタンス {インスタンス GUID} について {{site.data.keyword.Bluemix_notm}} スペース {スペース GUID} に割り振られた毎日の割り当て量に達しました。ログ検索ストレージについての現在の毎日の割り当ては 500MB、2 GB、5 GB、または 10 GB です。これは 3 日間保存され、この間 Kibana での検索が可能です。これは、ログ収集ストレージでのログ保存ポリシーには影響を与えません。

**リカバリー**

1 日により多くのデータをログ検索ストレージに保管できるようにプランをアップグレードするには、このスペースの {{site.data.keyword.loganalysisshort}} サービス・プランをアップグレードしてください。サービス・プランとプランのアップグレード方法について詳しくは、『[プラン](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans)』を参照してください。




