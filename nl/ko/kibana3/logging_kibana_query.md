---

copyright:
  years: 2015, 2018

lastupdated: "2018-01-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Kibana에서 조회로 Cloud Foundry 앱 로그 필터링
{: #logging_kibana_query}

Kibana에서 핵심 용어에 대한 로그를 검색하고 해당 용어로 필터링하는 조회를 작성합니다. Kibana를 사용하여 대시보드에서 조회를 시각적으로 비교할 수 있습니다. Cloud Foundry 앱의 **로그** 탭에서 Kibana 대시보드에 액세스할 수 있습니다.
{:shortdesc}

Kibana 대시보드에서 Cloud Foundry 앱 로그에 대한 조회를 작성하려면 다음 태스크를 완료하십시오. 

1. Cloud Foundry 앱의 **로그** 탭에 액세스하십시오.  

    1. {{site.data.keyword.Bluemix_notm}} **앱** 대시보드에서 앱 이름을 클릭하십시오. 
    2. **로그** 탭을 클릭하십시오. 
    
    앱의 로그가 표시됩니다.

2. 앱의 Kibana 대시보드에 액세스하십시오. **고급 보기** ![고급 보기 링크](images/logging_advanced_view.jpg "고급 보기 링크")를 클릭하십시오. Kibana 대시보드가 표시됩니다.

3. Kibana 대시보드에서 **조회** ![조회 아이콘](images/logging_query.jpg "조회 아이콘")를 클릭하여 필드를 표시하십시오. 앱의 **로그** 탭에 있는 앱 로그를 보기 위해 Kibana에 액세스하는 경우 앱의 application_id에 대한 모든 로그를 표시하는 조회가 작성됩니다. 
	
    조회를 편집하려면 **조회** 필드를 클릭하고 검색 용어를 입력하십시오. 

    * 키워드 또는 키워드 일부를 검색하려면 단어 뒤에 와일드카드 기호 \*를 입력하십시오(예: `Java*`). 
	* 특정 문구를 검색하려면 큰따옴표 안에 해당 문구를 입력하십시오(예: `"Java/1.8.0"`).
	* 더 복잡한 검색을 작성하려면 논리 용어 AND 및 OR를 사용할 수 있습니다(예: `"Java/1.8.0" OR "Java/1.7.0"`).
	* 특정 필드 내의 값을 검색하려면 *log_field_name:search_term* 형식으로 검색을 입력하십시오(예: `instance_id:1`).
	* 특정 로그 필드에 대한 값의 범위를 검색하려면 *log_field_name:[start_of_range TO end_of_range]* 형식으로 검색을 입력하십시오(예: `instance_id:[1 TO 2]`).

4. 두 개의 개별 조회 결과를 비교하기 위해 대시보드에 다른 조회 용어를 추가할 수 있습니다. 다른 조회를 추가하려면 **조회** 필드의 끝에 있는 **+** 아이콘을 클릭하십시오. 

    ![조회 필드](images/logging_query_field.jpg "조회 필드")
	
    와일드카드 \*가 포함된 새 **조회** 필드가 표시됩니다. 이 조회는 모든 항목을 포함하도록 Kibana에 지시합니다. 
	
    ![추가 조회 필드](images/logging_additional_query_field.jpg "추가 조회 필드")
	
    새 조회에 대한 결과로 대시보드가 업데이트됩니다. **시간별 이벤트** 분할창은 각 조회에 대한 용어 수가 소괄호 안에 표시된 두 조회에 대한 그래픽 표시를 보여줍니다.  
	
    ![두 조회에 대한 그래프를 표시하는 대시보드](images/logging_dashboard_queries.jpg "두 조회에 대한 그래프를 표시하는 대시보드")
	
5. 새 **조회** 필드를 클릭하여 해당 컨텐츠를 편집하고 조회 조건을 추가하십시오(예: `instance_id:1`). **시간별 이벤트** 분할창을 사용하여 조회 결과를 비교하십시오.

    ![두 조회에 대한 그래프를 표시하는 대시보드](images/logging_dashboard_queries2.jpg "두 조회에 대한 그래프를 표시하는 대시보드")

6. 조회를 삭제하려면 삭제할 **조회** 필드 위에 마우스를 올려 **삭제** 아이콘이 표시되게 하십시오. **삭제** 아이콘을 클릭하십시오. 

    ![삭제 아이콘이 있는 조회 필드](images/logging_delete_query.jpg "삭제 아이콘이 있는 조회 필드")

7. 이 대시보드를 인식 가능한 이름으로 저장하려면 **저장** 아이콘 ![저장 아이콘](images/logging_save.jpg "저장 아이콘")을 클릭하고 대시보드의 이릉을 입력하십시오.  

    **참고:** 이름에 공백이 있는 대시보드를 저장하는 경우 저장되지 않습니다. 공백이 없는 이름을 입력하고 **저장** 아이콘을 클릭하십시오. 

    ![대시보드 이름 저장](images/logging_save_dashboard.jpg "대시보드 이름 저장")


