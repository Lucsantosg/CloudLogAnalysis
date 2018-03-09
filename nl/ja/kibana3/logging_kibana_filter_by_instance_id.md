---

copyright:
  years: 2015, 2018

lastupdated: "2018-01-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Kibana でのインスタンス ID による Cloud Foundry アプリ・ログのフィルタリング
{: #logging_kibana_instance_id}

Kibana ダッシュボードで {{site.data.keyword.Bluemix_notm}} インスタンス・ログを表示して、アプリのインスタンス ID (instance_id) でフィルタリングします。 Kibana ダッシュボードには、Cloud Foundry アプリの**「ログ」**タブからアクセスできます。 
{:shortdesc}

Kibana ダッシュボードで Cloud Foundry アプリ・ログを表示して、instance_id でフィルタリングするには、以下のタスクを行います。

1. Cloud Foundry アプリの**「ログ」**タブにアクセスします。 

    1. {{site.data.keyword.Bluemix_notm}} **「アプリ」**ダッシュボードでアプリ名をクリックします。
    2. **「ログ」**タブをクリックします。 
    
    アプリのログが表示されます。

2. アプリの Kibana ダッシュボードにアクセスします。 **「詳細ビュー」** ![「詳細ビュー」リンク](images/logging_advanced_view.jpg "「詳細ビュー」リンク") をクリックします。 Kibana ダッシュボードが表示されます。

3. Kibana ダッシュボードで、**「Go to saved default」**アイコン ![「Go to saved default」アイコン](images/logging_default_dash.jpg "「Go to saved default」アイコン") をクリックし、スペースのすべてのログを表示します。 **「ALL EVENTS」**ウィンドウで、右矢印アイコンをクリックしてすべてのフィールドを表示します。 

    ![右矢印アイコンの付いた「ALL EVENTS」ウィンドウ](images/logging_all_events_no_fields.jpg "右矢印アイコンの付いた「ALL EVENTS」ウィンドウ")

4. **「フィールド」**ペインで **application_id** と **instance_id** を選択して、**「ALL EVENTS」**ウィンドウに application_id フィールドと instance_id フィールドを表示します。

    ![application_id フィールドと instance_id フィールドが選択された「ALL EVENTS」ウィンドウ](images/logging_all_events_app_instance_select.jpg "application_id フィールドと instance_id フィールドが選択された「ALL EVENTS」ウィンドウ")

5. **「ALL EVENTS」**ウィンドウで、ログ・イベント行をクリックすると、そのイベントの詳細が表示されます。 フィルターに掛ける instance_id を表示するイベントを選択します。

    ![選択されたログ・イベントの詳細を表示する「All Events」ウィンドウ](images/logging_selected_log_event.jpg "選択されたログ・イベントの詳細を表示する「All Events」ウィンドウ")

6. 特定のアプリ ID に関する情報を含める、または除外するためのフィルターを追加します。 

    * 特定のアプリケーション ID に関する情報を含めるフィルターを追加するには、表の application_id 行で**拡大鏡**アイコン ![拡大鏡アイコン](images/logging_magnifying_glass.jpg) をクリックします。 
    
           ![application_id フィールドのフィルター条件](images/logging_application_id_filter.jpg "application_id フィールドのフィルター条件")
    
    * * 特定のアプリケーション ID に関する情報を除外するフィルターを追加するには、表の application_id 行にある**除外** ![除外アイコン](images/logging_exclusion_icon.png) アイコンをクリックします。 
    
           ![アプリケーション IDを除外するためのフィルター条件](images/logging_application_id_exclude_filter.jpg "アプリケーション ID を除外するためのフィルター条件")
    
    Kibana ダッシュボードに新しいフィルター条件が追加されました。
 

7. 特定のアプリ ID に関する情報を含める、または除外するためのフィルターを追加します。 

    * 特定のインスタンス ID に関する情報を含めるフィルターを追加するには、表の instance_id 行で**拡大鏡** ![拡大鏡アイコン](images/logging_magnifying_glass.jpg "拡大鏡アイコン") アイコンをクリックします。 

    ![instance_id フィールドのフィルター条件](images/logging_instance_id_filter.jpg "instance_id フィールドのフィルター条件")

     * 特定のインスタンス ID に関する情報を除外するフィルターを追加するには、表の instance_id 行で**除外** ![除外アイコン](images/logging_exclusion_icon.png "除外アイコン") アイコンをクリックします。 
    
           ![インスタンス ID を除外するためのフィルター条件](images/logging_application_instance_id_exclude_filter.jpg "インスタンス ID を除外するためのフィルター条件")
    
    Kibana ダッシュボードに新しいフィルター条件が追加されました。

9. ダッシュボードを保存します。 フィルターの作成が終了したら、**「Save」**アイコン ![「Save」アイコン](images/logging_save.jpg "「Save」アイコン") をクリックして、ダッシュボードの名前を入力します。 

    **注:** スペースを含む名前でダッシュボードを保存しようとすると、保存されません。 スペースを含まない名前を入力し、**「Save」**アイコンをクリックしてください。

    ![ダッシュボード名の保存](images/logging_save_dashboard.jpg "ダッシュボード名の保存")

ログ項目を instance_id でフィルタリングするダッシュボードを作成しました。 **「Folder」**アイコン ![「Folder」アイコン](images/logging_folder.jpg "「Folder」アイコン") をクリックし、ダッシュボードを名前で選択することで、保存したダッシュボードをいつでもロードできます。 
