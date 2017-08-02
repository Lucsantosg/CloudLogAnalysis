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


# 플랜 변경
{: #change_plan}

`cf update-service` 명령을 실행하거나 서비스 대시보드에서 {{site.data.keyword.Bluemix_notm}}의 {{site.data.keyword.loganalysisshort}} 서비스 플랜을 변경할 수 있습니다. 플랜은 언제든지 업그레이드하거나 줄일 수 있습니다.
{:shortdesc}

## UI를 통해 서비스 플랜 변경
{: #change_plan_ui}

서비스 대시보드에서 {{site.data.keyword.Bluemix_notm}}의 서비스 플랜을 변경하려면 다음 단계를 완료하십시오.

1. {{site.data.keyword.Bluemix_notm}}에 로그인한 후에 {{site.data.keyword.Bluemix_notm}} 대시보드에서 {{site.data.keyword.loganalysisshort}} 서비스를 클릭하십시오.  
    
2. {{site.data.keyword.Bluemix_notm}} UI에서 **플랜** 탭을 선택하십시오.

    현재 플랜에 대한 정보가 표시됩니다.
	
3. 새 플랜을 선택하여 플랜을 업그레이드하거나 줄이십시오.  

4. **저장**을 클릭하십시오.



## CLI를 통해 서비스 플랜 변경
{: #change_plan_cli}

CLI를 통해 Bluemix의 서비스 플랜을 변경하려면 다음 단계를 완료하십시오.

1. {{site.data.keyword.Bluemix_notm}} 지역, 조직 및 영역에 로그인하십시오.  

    예를 들어, 미국 남부 지역에 로그인하려면 다음 명령을 실행하십시오.
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
	
2. 현재 플랜을 확인하고, 영역에서 사용할 수 있는 서비스의 목록에서 {{site.data.keyword.loganalysisshort}} 서비스 이름을 가져오려면 `cf services` 명령을 실행하십시오. 

    필드 **name**의 값은 플랜을 변경하는 데 사용해야 하는 값입니다. 

    예: 
	
	```
	$ cf services
    Getting services in org MyOrg / space dev as xxx@yyy.com...
    OK
    
    name              service          plan      bound apps   last operation
    Log Analysis-a4   ibmLogAnalysis   premium                create succeeded
    ```
	{: screen}
    
3. 플랜을 업그레이드하거나 줄이십시오. `cf update-service` 명령을 실행하십시오.
    
	```
	cf update-service service_name [-p new_plan]
	```
	{: codeblock}
	
	여기서 
	
	* *service_name*은 서비스의 이름입니다. 값을 가져오기 위해 `cf services` 명령을 실행할 수 있습니다. 
	* *new_plan*은 플랜의 이름입니다.
	
	여러 가지 플랜과 그 지원되는 값이 다음 표에 나열되어 있습니다.
	
	<table>
	  <caption>표 1. 플랜 목록.</caption>
	  <tr>
	    <th>플랜</th>
	    <th>이름</th>
	  </tr>
	  <tr>
	    <td>라이트</td>
	    <td>lite</td>
	  </tr>
	  <tr>
	    <td>로그 콜렉션</td>
	    <td>premium</td>
	  </tr>
	  <tr>
	    <td>2GB/일 검색의 로그 콜렉션</td>
	    <td>premiumsearch2</td>
	  </tr>
	  <tr>
	    <td>5GB/일 검색의 로그 콜렉션</td>
	    <td>premiumsearch5</td>
	  </tr>
	  <tr>
	    <td>10GB/일 검색의 로그 콜렉션</td>
	    <td>premiumsearch10</td>
	  </tr>
	</table>
	
	예를 들어, *라이트* 플랜으로 플랜을 줄이려면 다음 명령을 실행하십시오.
	
	```
	cf update-service "Log Analysis-a4" -p lite
    Updating service instance Log Analysis-a4 as xxx@yyy.com...
    OK
	```
	{: screen}

4. 새 플랜이 변경되었는지 확인하십시오. `cf services` 명령을 실행하십시오.

    ```
	cf services
    Getting services in org MyOrg / space dev as xxx@yyy.com...
    OK

    name              service          plan   bound apps   last operation
    Log Analysis-a4   ibmLogAnalysis   lite                update succeeded
	```
	{: screen}






