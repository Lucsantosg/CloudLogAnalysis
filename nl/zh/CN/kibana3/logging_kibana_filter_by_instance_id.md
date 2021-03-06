---

copyright:
  years: 2015, 2018

lastupdated: "2018-01-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# 在 Kibana 中按实例标识过滤 Cloud Foundry 应用程序日志
{: #logging_kibana_instance_id}

在 Kibana 仪表板上按应用程序的实例标识 (instance_id) 来查看和过滤 {{site.data.keyword.Bluemix_notm}} 实例日志。可以从 Cloud Foundry 应用程序的**日志**选项卡访问 Kibana 仪表板。
{:shortdesc}

要在 Kibana 仪表板上按 instance_id 查看和过滤 Cloud Foundry 应用程序日志，请完成以下任务：

1. 访问 Cloud Foundry 应用程序的**日志**选项卡。 

    1. 单击 {{site.data.keyword.Bluemix_notm}} **应用程序**仪表板上的应用程序名称。
    2. 单击**日志**选项卡。 
    
    这将显示应用程序的日志。

2. 访问应用程序的 Kibana 仪表板。单击**高级视图** ![“高级视图”链接](images/logging_advanced_view.jpg "“高级视图”链接")。这将显示 Kibana 仪表板。

3. 在 Kibana 仪表板上，单击**转至已保存的缺省值**图标 ![“转至已保存的缺省值”图标](images/logging_default_dash.jpg "“转至已保存的缺省值”图标") 以显示空间的所有日志。在**所有事件**窗口中，单击向右箭头图标以显示所有字段。 

    ![具有向右箭头图标的“所有事件”窗口](images/logging_all_events_no_fields.jpg "具有向右箭头图标的“所有事件”窗口")

4. 在**字段**窗格中，选择 **application_id** 和 **instance_id** 以显示**所有事件**窗口中的 application_id 和 instance_id 字段。

    ![选择了 application_id 和 instance_id 字段的“所有事件”窗口](images/logging_all_events_app_instance_select.jpg "选择了 application_id 和 instance_id 字段的“所有事件”窗口")

5. 在**所有事件**窗口中，单击日志事件行以显示该事件的详细信息。选择显示您要过滤的 instance_id 的事件。

    ![显示所选日志事件详细信息的“所有事件”窗口](images/logging_selected_log_event.jpg "显示所选日志事件详细信息的“所有事件”窗口")

6. 添加过滤器以包含或排除应用程序标识的信息。 

    * 要添加包含特定应用程序标识信息的过滤器，请单击表 application_id 行中的**放大镜** ![“放大镜”图标](images/logging_magnifying_glass.jpg) 图标。 
    
           ![application_id 字段的过滤条件](images/logging_application_id_filter.jpg "application_id 字段的过滤条件")
    
    * 要添加排除特定应用程序标识信息的过滤器，请单击表 application_id 行中的**排除** ![“排除”图标](images/logging_exclusion_icon.png) 图标。 
    
           ![排除应用程序标识的过滤条件](images/logging_application_id_exclude_filter.jpg "排除应用程序标识的过滤条件")
    
    这将向 Kibana 仪表板添加新过滤条件。
 

7. 添加过滤器以包含或排除应用程序实例标识的信息。 

    * 要添加包含特定实例标识信息的过滤器，请单击表 instance_id 行中的**放大镜** ![“放大镜”图标](images/logging_magnifying_glass.jpg "“放大镜”图标") 图标。 

    ![instance_id 字段的过滤条件](images/logging_instance_id_filter.jpg "instance_id 字段的过滤条件")

     * 要添加排除特定实例标识信息的过滤器，请单击表 instance_id 行中的**排除** ![“排除”图标](images/logging_exclusion_icon.png "“排除”图标") 图标。 
    
           ![排除实例标识的过滤条件](images/logging_application_instance_id_exclude_filter.jpg "排除实例标识的过滤条件")
    
    这将向 Kibana 仪表板添加新过滤条件。

9. 保存仪表板。当您完成创建过滤器后，单击**保存**图标 ![“保存”图标](images/logging_save.jpg "“保存”图标") 并输入仪表板的名称。 

    **注：**如果尝试使用包含空格的名称来保存仪表板，那么不会保存该仪表板。请输入不带空格的名称并单击**保存**图标。

    ![保存仪表板名称](images/logging_save_dashboard.jpg "保存仪表板名称")。

您已创建了按 instance_id 过滤日志条目的仪表板。您可以通过单击**文件夹**图标 ![“文件夹”图标](images/logging_folder.jpg "“文件夹”图标") 并按名称选择仪表板，随时装入已保存的仪表板。 
