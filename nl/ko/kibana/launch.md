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


# Kibana 대시보드로 이동
{: #launch}

{{site.data.keyword.loganalysisshort}} 서비스에서, {{site.data.keyword.Bluemix}} UI에서 또는 웹 브라우저에서 직접 Kibana를 실행할 수 있습니다.
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} 관리 클라우드 인프라에서 배치된 Docker 컨테이너 및 CF 앱의 경우, Kibana를 실행하는 리소스의 맥락에서 데이터를 보고 분석하기 위해 {{site.data.keyword.Bluemix_notm}}에서 Kibana를 실행할 수 있습니다. 예를 들면, 그 특정 앱의 맥락에서 Kibana에서 사용자의 특정 CF 앱 로그에 실행할 수 있습니다.
    
Kubernetes 인프라에서 배치된 Docker 컨테이너와 같은 클라우드 리소스의 경우, 제공된 {{site.data.keyword.Bluemix_notm}} 영역 내의 서비스에서 집계된 로그 데이터를 보기 위해 직접 브라우저 링크 또는 {{site.data.keyword.loganalysisshort}} 서비스 대시보드에서 Kibana를 실행할 수 있습니다. 대시보드에 표시되는 데이터 필터링에 사용되는 조회는 {{site.data.keyword.Bluemix_notm}} 조직에서 영역에 대한 로그 항목을 검색합니다. Kibana가 표시하는 로그 정보에는 사용자가 로그인한 {{site.data.keyword.Bluemix_notm}} 조직의 영역 내에 배치된 모든 리소스에 대한 레코드가 포함되어 있습니다.  

클라우스 리소스 및 Kibana를 실행하기 위해 지원되는 탐색 방법이 다음 표에 나열되어 있습니다.

<table>
<caption>표 1. 리소스의 목록 및 지원되는 탐색 메소드. </caption>
  <tr>
    <th>리소스 </th>
	<th>{{site.data.keyword.loganalysisshort}} 서비스 대시보드에서 Kibana 대시보드로 이동</th>
    <th>Bluemix 대시보드에서 Kibana 대시보드로 이동</th>
    <th>웹 브라우저에서 Kibana 대시보드로 이동</th>
  </tr>
  <tr>
    <td>CF 앱</td>
	<td>예</td>
    <td>예</td>
    <td>예</td>
  </tr>  
  <tr>
    <td>Kubernetes 클러스터에 배치된 컨테이너</td>
	<td>예</td>
    <td>아니오</td>
    <td>예</td>
  </tr>  
  <tr>
    <td>{{site.data.keyword.Bluemix_notm}} 관리 클라우드 인프라에서 배치된 컨테이너</td>
	<td>예</td>
    <td>예</td>
    <td>예</td>
  </tr>  
</table>

Kibana에 대한 자세한 정보는 [Kibana User Guide ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.elastic.co/guide/en/kibana/5.1/index.html "외부 링크 아이콘"){: new_window}을 참조하십시오.
    

##  로그 분석 서비스의 대시보드에서 Kibana로 이동
{: #launch_Kibana_from_log_analysis}

Kibana에 표시되는 데이터 필터링에 사용되는 조회는 {{site.data.keyword.Bluemix_notm}} 조직에서 영역에 대한 로그 항목을 검색합니다.  
	
Kibana가 표시하는 로그 정보에는 사용자가 로그인한 {{site.data.keyword.Bluemix_notm}} 조직의 영역 내에 배치된 모든 리소스에 대한 레코드가 포함되어 있습니다. 

{{site.data.keyword.loganalysisshort}} 서비스의 대시보드에서 Kibana를 실행하려면 다음 단계를 완료하십시오. 

1. {{site.data.keyword.Bluemix_notm}}에 로그인한 후에 {{site.data.keyword.Bluemix_notm}} 대시보드에서 {{site.data.keyword.loganalysisshort}} 서비스를 클릭하십시오.  
    
2. {{site.data.keyword.Bluemix_notm}} UI에서 **관리** 탭을 선택하십시오.

3. **실행**을 클릭하십시오. Kibana 대시보드가 열립니다. 

기본적으로 **검색** 페이지는 기본 인덱스 패턴이 선택되고 시간 필터가 최근 15분으로 설정되어 로드됩니다.  

검색 페이지에 로그 항목이 표시되지 않는 경우, 시간 선택도구를 조정하십시오.자세한 정보는 [시간 필터 설정](filter_logs.html#set_time_filter)을 참조하십시오.

	
	
##  웹 브라우저에서 Kibana로 이동
{: #launch_Kibana_from_browser}

Kibana에 표시되는 데이터 필터링에 사용되는 조회는 {{site.data.keyword.Bluemix_notm}} 조직에서 영역에 대한 로그 항목을 검색합니다.  
	
Kibana가 표시하는 로그 정보에는 사용자가 로그인한 {{site.data.keyword.Bluemix_notm}} 조직의 영역 내에 배치된 모든 리소스에 대한 레코드가 포함되어 있습니다. 

브라우저에서 Kibana를 실행하려면 다음 단계를 완료하십시오.

1. 웹 브라우저를 열고 Kibana를 실행하십시오. 그런 다음, Kibana 사용자 인터페이스에 로그인하십시오. 
    
    그 예로 미국 남부 지역에서 Kibana를 실행하기 위해 사용해야 하는 URL이 다음 표에 나열되어 있습니다.
      
    <table>
          <caption>표 1. 지역별 Kibana 실행을 위한 URL</caption>
           <tr>
            <th>지역</th>
            <th>URL</th>
          </tr>
          <tr>
            <td>미국 남부</td>
            <td>https://logging.ng.bluemix.net/ </td>
          </tr>
    </table>
	
	Kibana의 검색 페이지가 열립니다.
	
2. 로그 데이터를 보고 분석하려는 {{site.data.keyword.Bluemix_notm}} 영역에 대한 인덱스 패턴을 선택하십시오.

    1. **default-index**를 클릭하십시오.
	
	2. 그 영역에 대한 인덱스 패턴을 선택하십시오. 인덱스 패턴의 형식은 다음과 같습니다. 
	
	    ```
	    [logstash-Space_ID-]YYYY.MM.DD 
	    ```
        {screen}
	
	    여기서 *Space_ID*는 로그 데이터를 보고 분석하려는 {{site.data.keyword.Bluemix_notm}} 영역의 GUID입니다. 
	
검색 페이지에 로그 항목이 표시되지 않는 경우, 시간 선택도구를 조정하십시오.자세한 정보는 [시간 필터 설정](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#set_time_filter)을 참조하십시오.


	
##  CF 앱의 대시보드에서 Kibana로 이동
{: #launch_Kibana_from_cf_app}

Kibana에 표시되는 데이터 필터링에 사용되는 조회는 Kibana를 실행하는 {{site.data.keyword.Bluemix_notm}} CF 앱에 대한 로그 항목을 검색합니다. 

Kibana에서 Cloud Foundry 애플리케이션의 로그를 보려면 다음 단계를 완료하십시오.

1. {{site.data.keyword.Bluemix_notm}}에 로그인한 후에 {{site.data.keyword.Bluemix_notm}} 대시보드에서 앱 이름 또는 컨테이너를 클릭하십시오.  
    
2. {{site.data.keyword.Bluemix_notm}} UI 의 로그 탭을 여십시오.

    CF 앱의 경우, 탐색줄에서 **로그**를 클릭하십시오.
    로그 탭이 열립니다.  

3. **고급 보기**를 클릭하십시오. Kibana 대시보드가 열립니다. 

    기본적으로 **검색** 페이지는 기본 인덱스 패턴이 선택되고 시간 필터가 최근 30초로 설정되어 로드됩니다. 검색 조회는 CF 앱의 모든 항목과 일치하도록 설정됩니다.

    검색 페이지에 로그 항목이 표시되지 않는 경우, 시간 선택도구를 조정하십시오.자세한 정보는 [시간 필터 설정](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#set_time_filter)을 참조하십시오.


##  컨테이너의 대시보드에서 Kibana로 이동
{: #launch_Kibana_for_containers}

이 방법은 {{site.data.keyword.Bluemix_notm}} 관리 클라우드 인프라에서 배치된 컨테이너에만 적용됩니다.

Kibana에 표시되는 데이터 필터링에 사용되는 조회는 Kibana를 실행하는 컨테이너에 대한 로그 항목을 검색합니다. 

Kibana에서 Docker 컨테이너의 로그를 보려면 다음 단계를 완료하십시오.

1. {{site.data.keyword.Bluemix_notm}}에 로그인한 후에 {{site.data.keyword.Bluemix_notm}} 대시보드에서 컨테이너를 클릭하십시오.  
    
2. {{site.data.keyword.Bluemix_notm}} UI 의 로그 탭을 여십시오.

    {{site.data.keyword.IBM_notm}} 관리 클라우드 인프라에서 배치된 컨테이너의 경우, 탐색줄에서 **모니터링 및 로그**를 선택한 후에 **로깅** 탭을 클릭하십시오. 
    
    로그 탭이 열립니다.  

3. **고급 보기**를 클릭하십시오. Kibana 대시보드가 열립니다. 

    기본적으로 **검색** 페이지는 기본 인덱스 패턴이 선택되고 시간 필터가 최근 30초로 설정되어 로드됩니다. 검색 조회는 Docker 컨테이너의 모든 항목과 일치하도록 설정됩니다.

    검색 페이지에 로그 항목이 표시되지 않는 경우, 시간 선택도구를 조정하십시오.자세한 정보는 [시간 필터 설정](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#set_time_filter)을 참조하십시오.

	



