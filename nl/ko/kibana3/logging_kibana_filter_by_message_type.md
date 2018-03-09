---

copyright:
  years: 2015, 2018

lastupdated: "2018-01-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Kibana에서 메시지 유형별로 Cloud Foundry 앱 로그 필터링
{: #logging_kibana_message_type_filter}

Kibana 대시보드에서 메시지 유형별로 {{site.data.keyword.Bluemix_notm}} 애플리케이션 로그를 보고 필터링합니다. Cloud Foundry 앱의 **로그** 탭에서 Kibana 대시보드에 액세스할 수 있습니다.
{:shortdesc}

Kibana 대시보드에서 메시지 유형별로 Cloud Foundry 앱 로그를 보고 필터링하려면 다음 단계를 완료하십시오. 

1. Cloud Foundry 앱의 **로그** 탭에 액세스하십시오.  

    1. {{site.data.keyword.Bluemix_notm}} **앱** 대시보드에서 앱 이름을 클릭하십시오. 
    2. **로그** 탭을 클릭하십시오. 
    
    앱의 로그가 표시됩니다.

2. 앱의 Kibana 대시보드에 액세스하십시오. **고급 보기** ![고급 보기 링크](images/logging_advanced_view.jpg "고급 보기 링크")를 클릭하십시오. Kibana 대시보드가 표시됩니다.

3. **모든 이벤트** 창에서 오른쪽 화살표 아이콘을 클릭하여 모든 필드를 표시하십시오. 

    ![오른쪽 화살표 아이콘이 있는 모든 이벤트 창](images/logging_all_events_no_fields.jpg "오른쪽 화살표 아이콘이 있는 모든 이벤트 창")

4. **필드** 분할창에서 **message_type**을 선택하여 **모든 이벤트** 창의 각 항목을 생성한 컴포넌트를 표시하십시오. 

    ![message_type 필드가 선택된 모든 이벤트 창](images/logging_message_type.png "message_type 필드가 선택된 모든 이벤트 창")

5. **ALL EVENTS** 창에서 로그 이벤트 행을 클릭하여 해당 이벤트에 대한 세부사항을 표시하십시오. 필터링하려는 **message_type**을 표시하는 이벤트를 선택하십시오. 

    ![선택한 로그 이벤트의 세부사항을 표시하는 모든 이벤트 창](images/logging_message_type_add_filter.png "선택한 로그 이벤트의 세부사항을 표시하는 모든 이벤트 창")

6. 메시지 유형에 대한 정보를 포함시키거나 제외할 필터를 추가하십시오.  

    * 메시지 유형에 대한 정보를 포함시키는 필터를 추가하려면 표의 message_type 행에 있는 **돋보기** ![돋보기 아이콘](images/logging_magnifying_glass.jpg "돋보기 아이콘") 아이콘을 클릭하십시오. 
    
           ![message_type 필드에 대한 필터 조건](images/logging_message_type_filter.png "message_type 필드에 대한 필터 조건")
    
    * 메시지 유형에 대한 정보를 제외하는 필터를 추가하려면 표의 message_type 행에 있는 **제외** ![제외 아이콘](images/logging_exclusion_icon.png "제외 아이콘") 아이콘을 클릭하십시오. 
    
    새 필터 조건이 Kibana 대시보드에 추가됩니다.

7. 원하는 경우 이전 단계를 반복하여 다른 메시지 유형에 대한 필터를 추가하십시오. 전체 메시지 유형 목록을 보려면 [로그 형식](../logging_view_kibana3.html#kibana_log_format_cf)을 참조하십시오.

9. 대시보드를 저장하십시오.     
        
    필터 작성을 완료하면 **저장** 아이콘 ![저장 아이콘](images/logging_save.jpg "저장 아이콘")을 클릭하고 대시보드의 이릉을 입력하십시오.  
      
    **참고:** 이름에 공백이 있는 대시보드를 저장하는 경우 저장되지 않습니다. 공백이 없는 이름을 입력하고 **저장** 아이콘을 클릭하십시오. 
    
    ![대시보드 이름 저장](images/logging_save_dashboard.jpg "대시보드 이름 저장").

메시지 유형별로 로그 항목을 필터링하는 대시보드를 작성했습니다. **폴더** 아이콘 ![폴더 아이콘](images/logging_folder.jpg "폴더 아이콘")을 클릭하고 이름으로 대시보드를 선택하여 저장된 대시보드를 언제든 로드할 수 있습니다. 
