---

copyright:
  years: 2015, 2018

lastupdated: "2018-01-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Kibana でのメッセージ・タイプによる Cloud Foundry アプリ・ログのフィルタリング
{: #logging_kibana_message_type_filter}

Kibana ダッシュボードで {{site.data.keyword.Bluemix_notm}} アプリケーション・ログを表示して、メッセージ・タイプでフィルタリングします。 Kibana ダッシュボードには、Cloud Foundry アプリの**「ログ」**タブからアクセスできます。 
{:shortdesc}

Kibana ダッシュボードで Cloud Foundry アプリ・ログを表示して、メッセージ・タイプでフィルタリングするには、以下のタスクを行います。

1. Cloud Foundry アプリの**「ログ」**タブにアクセスします。 

    1. {{site.data.keyword.Bluemix_notm}} **「アプリ」**ダッシュボードでアプリ名をクリックします。
    2. **「ログ」**タブをクリックします。 
    
    アプリのログが表示されます。

2. アプリの Kibana ダッシュボードにアクセスします。 **「詳細ビュー」** ![「詳細ビュー」リンク](images/logging_advanced_view.jpg "「詳細ビュー」リンク") をクリックします。 Kibana ダッシュボードが表示されます。

3. **「ALL EVENTS」**ウィンドウで、右矢印アイコンをクリックしてすべてのフィールドを表示します。 

    ![右矢印アイコンの付いた「ALL EVENTS」ウィンドウ](images/logging_all_events_no_fields.jpg "右矢印アイコンの付いた「ALL EVENTS」ウィンドウ")

4. **「Fields」**ペインで **message_type** を選択し、各ログ項目を生成したコンポーネントを**「ALL EVENTS」**ウィンドウに表示します。

    ![message_type フィールドが選択された「ALL EVENTS」ウィンドウ](images/logging_message_type.png "message_type フィールドが選択された「ALL EVENTS」ウィンドウ")

5. **「ALL EVENTS」**ウィンドウで、ログ・イベント行をクリックすると、そのイベントの詳細が表示されます。 フィルタリングする **message_type** を示しているイベントを選択します。

    ![選択されたログ・イベントの詳細を表示する「ALL EVENTS」ウィンドウ](images/logging_message_type_add_filter.png "選択されたログ・イベントの詳細を表示する「ALL EVENTS」ウィンドウ")

6. 特定のメッセージ・タイプに関する情報を含める、または除外するためのフィルターを追加します。 

    * 特定のメッセージ・タイプに関する情報を含めるフィルターを追加するには、表の message_type 行で**拡大鏡**アイコン ![拡大鏡アイコン](images/logging_magnifying_glass.jpg "拡大鏡アイコン") をクリックします。 
    
           ![message_type フィールドのフィルター条件](images/logging_message_type_filter.png "message_type フィールドのフィルター条件")
    
    * 特定のメッセージ・タイプに関する情報を除外するフィルターを追加するには、表の message_type 行で**「Exclusion」**アイコン ![「Exclusion」アイコン](images/logging_exclusion_icon.png "「Exclusion」アイコン") をクリックします。 
    
    Kibana ダッシュボードに新しいフィルター条件が追加されました。

7. オプションで、前のステップを繰り返して他のメッセージ・タイプに関するフィルターを追加します。 メッセージ・タイプの全リストを表示するには、『[ログのフォーマット (Log format)](../logging_view_kibana3.html#kibana_log_format_cf)』を参照してください。

9. ダッシュボードを保存します。    
        
    フィルターの作成が終了したら、**「Save」**アイコン ![「Save」アイコン](images/logging_save.jpg "「Save」アイコン") をクリックして、ダッシュボードの名前を入力します。 
      
    **注:** スペースを含む名前でダッシュボードを保存しようとすると、保存されません。 スペースを含まない名前を入力し、**「Save」**アイコンをクリックしてください。
    
    ![ダッシュボード名の保存](images/logging_save_dashboard.jpg "ダッシュボード名の保存")

ログ項目をメッセージ・タイプでフィルタリングするダッシュボードを作成しました。 **「Folder」**アイコン ![「Folder」アイコン](images/logging_folder.jpg "「Folder」アイコン") をクリックし、ダッシュボードを名前で選択することで、保存したダッシュボードをいつでもロードできます。
