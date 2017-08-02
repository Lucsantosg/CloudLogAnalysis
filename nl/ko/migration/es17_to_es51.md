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

# ELK 스택을 버전 5.1로 업그레이드한 이후의 마이그레이션 고려사항 
{: #es17_to_es51}

{{site.data.keyword.Bluemix}}에서 ElasticSearch(ELK) 스택이 버전 1.7에서 버전 2.3으로 업그레이드되었습니다. 새 기능, 로그 수집을 위한 URLS, Kibana에서 로그 분석을 위한 새 URL을 사용할 수 있습니다. 자세한 정보는 [ElasticSearch 5.1 ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.elastic.co/guide/en/elasticsearch/reference/5.1/index.html "외부 링크 아이콘")을 참조하십시오.
{:shortdesc}

이 기능은 Kubernetes 클러스터에 배치되는 Docker 컨테이너를 사용하여 로깅 서비스를 사용하는 사용자에게 적용되지 않습니다. 이러한 컨테이너에서는 이미 ELK 스택 버전 2.3을 사용합니다.

## 지역
{: #regions}

ELK 스택 버전 5.1은 다음 지역에서 사용 가능합니다. 

* 미국 남부


## 새로운 기능
{: #features}

1. 로그 및 메트릭으로 작업하기 위한 다른 URL.

    ELK 1.7에서는 로그 및 메트릭을 표시하고 모니터하기 위해 같은 URL을 공유했습니다. ELK 5.1로 업그레이드하면 로그 및 메트릭을 보기 위한 개별 URLS가 있습니다. 자세한 정보는 [로깅 URL](#logging)을 참조하십시오.
    
2. Kibana 5.1에 대한 지원. 

    {{site.data.keyword.Bluemix_notm}} UI에서 또는 새 로깅 URL에서 직접 Kibana를 실행할 수 있습니다. 자세한 정보는 [Kibana를 사용한 로그 분석](/docs/services/CloudLogAnalysis/kibana/analyzing_logs_Kibana.html#analyzing_logs_Kibana)을 참조하십시오.
    
    Kibana 3은 더 이상 사용되지 않습니다. [ELK 1.7 로깅 URL](#logging)을 통해 Kibana 3을 실행할 수 있습니다. 지역별로 다른 URL이 있습니다. **참고:** Kibana 3 대시보드에 대한 액세스 권한이 현재 Kibana 3 대시보드를 Kibana 5.1 대시보드와 비교하고 마이그레이션하는 데 사용 가능합니다.  
    
    ELK 1.7 스택에 빌드된 Kibana 대시보드가 있는 경우, ELK 5.1 환경으로 마이그레이션해야 합니다.
    
    Kibana 5.1에 대한 자세한 정보는 [Kibana User Guide ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.elastic.co/guide/en/kibana/5.1/index.html "외부 링크 아이콘"){: new_window}을 참조하십시오.
    
3. 사용자 정의 필드에 추가된 유형 기반 접미부.

    Kibana 검색 필드로 사용자 정의 필드를 구성할 수 있습니다. 메시지에서 사용 가능한 각 필드는 값과 일치하는 필드의 유형으로 구문 분석됩니다. 예를 들면, 다음과 같은 JSON 메시지의 각 필드입니다.  

    ```
    {"field1":"string type",
     "field2":123,
     "field3":false,
     "field4":"4567"
     }
    ```
    {: screen}
    
    필터링과 검색에 사용할 수 있는 필드로서 사용 가능합니다. 

    * field1은 문자열 유형의 field1_str로 구문 분석됩니다.
    * field2는 정수 유형의 field1_int로 구문 분석됩니다.
    * field3은 부울 유형의 field3_bool로 구문 분석됩니다.
    * field4는 문자열 유형의 field4_str로 구문 분석됩니다.
    
    샘플 JSON 메시지는 사용자가 로깅 서비스에 전송한 로그입니다. 

    **참고:** 이 기능은 Elastic 5.1에서만 사용 가능합니다. 이 기능은 Kibana3 대시보드가 중단되는 것을 방지하기 위해 Elastic 1.7에서는 사용할 수 없습니다. 


## 로깅 
{: #logging}

{{site.data.keyword.Bluemix_notm}}에 로그를 전송하고 Kibana의 데이터를 분석하는 데 다른 URL이 사용됩니다.

다음 표에는 미국 남부 지역의 새 URL이 나열되어 있습니다.

<table>
  <caption>미국 남부 지역의 URL</caption>
    <tr>
      <th>유형</th>
      <th>ELK 1.7 </th>
	  <th>ELK 5.1 </th>
    </tr>
  <tr>
    <td>로그에 대한 수집 URL</td>
    <td>logs.opvis.bluemix.net:9091</td>
	<td>ingest.logging.ng.bluemix.net:9091</td>
  </tr>
   <tr>
    <td>로그 분석을 위한 Kibana URL</td>
    <td>https://logmet.ng.bluemix.net</td>
	<td>https://logging.ng.bluemix.net</td>
  </tr>
</table>

