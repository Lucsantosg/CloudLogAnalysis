---

copyright:
  years: 2017, 2018

lastupdated: "2018-01-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 시작하기 튜토리얼
{: #getting-started-with-cla}

이 튜토리얼을 사용하여 {{site.data.keyword.Bluemix}}의 {{site.data.keyword.loganalysislong}} 서비스에 대한 작업을 시작하는 방법을 학습할 수 있습니다.
{:shortdesc}

## 목표
{: #objectives}

* 영역에서 {{site.data.keyword.loganalysislong}} 서비스를 프로비저닝합니다.
* 로그를 관리하도록 명령행을 설정합니다.
* 사용자가 영역의 로그를 볼 수 있도록 권한을 설정합니다.
* 로그를 보는 데 사용할 수 있는 오픈 소스 도구인 Kibana를 실행합니다.


## 시작하기 전에
{: #prereqs}

{{site.data.keyword.Bluemix_notm}} 계정의 구성원이거나 소유자인 사용자 ID가 있어야 합니다. {{site.data.keyword.Bluemix_notm}} 사용자 ID를 얻으려면 [등록 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.bluemix.net/registration/){:new_window}으로 이동하십시오.

이 튜토리얼은 미국 남부 지역에서 {{site.data.keyword.loganalysisshort}} 서비스를 프로비저닝하고 이에 대해 작업하기 위한 지시사항을 제공합니다.


## 1단계: {{site.data.keyword.loganalysisshort}} 서비스 프로비저닝
{: #step1}

**참고:** CF(Cloud Foundry) 영역에서 {{site.data.keyword.loganalysisshort}} 서비스의 인스턴스를 프로비저닝합니다. 영역당 하나의 서비스 인스턴스만 필요합니다. 계정 레벨에서 {{site.data.keyword.loganalysisshort}} 서비스를 프로비저닝할 수 없습니다. 

{{site.data.keyword.Bluemix_notm}}에서 {{site.data.keyword.loganalysisshort}} 서비스의 인스턴스를 프로비저닝하려면 다음 단계를 완료하십시오. 

1. {{site.data.keyword.Bluemix_notm}}([http://bluemix.net ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://bluemix.net){:new_window})에 로그인하십시오.  

2. {{site.data.keyword.loganalysisshort}} 서비스를 프로비저닝하려는 지역, 조직 및 영역을 선택하십시오.  

3. **카탈로그**를 클릭하십시오. {{site.data.keyword.Bluemix_notm}}에서 사용 가능한 서비스의 목록이 열립니다. 

4. **DevOps** 카테고리를 선택하여 표시된 서비스의 목록을 필터링하십시오. 

5. **로그 분석** 타일을 클릭하십시오. 

6. 서비스 플랜을 선택하십시오. 기본적으로 **라이트** 플랜이 설정됩니다. 

    서비스 플랜에 대한 자세한 정보는 [서비스 플랜](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans)을 참조하십시오.
	
7. 사용자가 로그인한 {{site.data.keyword.Bluemix_notm}} 영역의 {{site.data.keyword.loganalysisshort}} 서비스를 프로비저닝하려면 **작성**을 클릭하십시오. 




## 2단계: [선택사항] {{site.data.keyword.loganalysisshort}} 서비스에 대한 서비스 플랜 변경
{: #step2}

추가 검색 할당량, 로그의 장기 스토리지 또는 둘 다가 필요한 경우 {{site.data.keyword.Bluemix_notm}} UI를 통해 또는 `bx cf update-service` 명령을 실행하여 이러한 기능을 사용으로 설정함으로써 {{site.data.keyword.loganalysisshort}} 서비스 인스턴스 플랜을 변경할 수 있습니다. 

언제든지 서비스 플랜을 업그레이드하거나 줄일 수 있습니다.

자세한 정보는 [{{site.data.keyword.loganalysisshort}} 서비스 플랜](/docs/services/CloudLogAnalysis/log_analysis_ov.html#plans)을 참조하십시오.

**참고:** 플랜을 유료 사용제로 변경하면 비용이 발생합니다.

{{site.data.keyword.Bluemix_notm}} UI에서 서비스 플랜을 변경하려면 다음 단계를 완료하십시오.

1. {{site.data.keyword.Bluemix_notm}}([http://bluemix.net ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://bluemix.net){:new_window})에 로그인하십시오.  

2. {{site.data.keyword.loganalysisshort}} 서비스가 사용 가능한 지역, 조직 및 영역을 선택하십시오.  

3. {{site.data.keyword.Bluemix_notm}} *대시보드*에서 {{site.data.keyword.loganalysisshort}} 서비스 인스턴스를 클릭하십시오. 
    
4. {{site.data.keyword.loganalysisshort}} 대시보드에서 **플랜** 탭을 선택하십시오. 

    현재 플랜에 대한 정보가 표시됩니다.
	
5. 새 플랜을 선택하여 플랜을 업그레이드하거나 줄이십시오.  

6. **저장**을 클릭하십시오.



## 3단계: {{site.data.keyword.loganalysisshort}} 서비스에 대해 작업하도록 로컬 환경 설정
{: #step3}


{{site.data.keyword.loganalysisshort}} 서비스에는 로그 콜렉션(장기 스토리지 컴포넌트)에 저장된 로그를 관리하는 데 사용할 수 있는 명령행 인터페이스(CLI)가 포함됩니다. 

{{site.data.keyword.loganalysisshort}} {{site.data.keyword.Bluemix_notm}} 플러그인을 사용하여 로그 상태를 보고 로그를 다운로드하고 로그 보존 정책을 구성할 수 있습니다.  

CLI는 여러 유형의 도움말을 제공합니다. CLI 및 지원되는 명령에 대해 알기 위한 일반 도움말, 명령 사용 방법을 알기 위한 명령 도움말 또는 명령의 하위 명령 사용 방법을 알기 위한 하위 명령 도움말이 있습니다.


{{site.data.keyword.Bluemix_notm}} 저장소에서 {{site.data.keyword.loganalysisshort}} CLI를 설치하려면 다음 단계를 완료하십시오.

1. {{site.data.keyword.Bluemix_notm}} CLI를 설치하십시오. 

   자세한 정보는 [{{site.data.keyword.Bluemix_notm}} CLI 설치](/docs/cli/reference/bluemix_cli/download_cli.html#download_install)를 참조하십시오. 

2. {{site.data.keyword.loganalysisshort}} 플러그인을 설치하십시오. 다음 명령을 실행하십시오.

    ```
    bx plugin install logging-cli -r Bluemix
    ```
    {: codeblock}
 
3. {{site.data.keyword.loganalysisshort}} 플러그인이 설치되었는지 확인하십시오.
  
    예를 들어, 다음 명령을 실행하여 설치된 플러그인의 목록을 확인하십시오.
    
    ```
    bx plugin list
    ```
    {: codeblock}
    
    출력은 다음과 같습니다.
   
    ```
    bx plugin list
    Listing installed plug-ins...

    Plugin Name          Version   
    logging-cli          0.1.1   
    ```
    {: screen}




## 4단계: 사용자가 로그를 볼 수 있도록 권한 설정
{: #step4}

사용자가 수행할 수 있는 {{site.data.keyword.loganalysisshort}} 조치를 제어하기 위해 사용자에게 역할 및 정책을 지정할 수 있습니다. 

{{site.data.keyword.Bluemix_notm}}에는 사용자가 {{site.data.keyword.loganalysisshort}} 서비스에 대해 작업할 때 수행할 수 있는 조치를 제어하는 두 가지 유형의 보안 권한이 있습니다.

* CF(Cloud Foundry) 역할: 사용자가 영역의 로그를 보기 위해 보유해야 하는 권한을 정의하려면 사용자에게 CF 역할을 부여합니다.
* IAM 역할: 사용자가 계정 도메인의 로그를 보기 위해 보유해야 하는 권한과 로그 콜렉션에 저장된 로그를 관리하기 위해 보유해야 하는 권한을 정의하려면 사용자에게 IAM 정책을 부여합니다. 


사용자에게 영역의 로그를 볼 수 있는 권한을 부여하려면 다음 단계를 완료하십시오.

1. {{site.data.keyword.Bluemix_notm}} 콘솔에 로그인하십시오. 

    웹 브라우저를 열고 {{site.data.keyword.Bluemix_notm}} 대시보드를 실행하십시오. [http://bluemix.net ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://bluemix.net){:new_window} 
	
	사용자 ID 및 비밀번호를 사용하여 로그인하면 {{site.data.keyword.Bluemix_notm}} UI가 열립니다. 

2. 메뉴 표시줄에서 **관리 > 계정 > 사용자**를 클릭하십시오.  

    *사용자* 창에 현재 선택한 계정의 이메일 주소와 함께 사용자 목록이 표시됩니다. 
	
3. 사용자가 계정의 구성원인 경우 목록에서 사용자 이름을 선택하거나 *조치* 메뉴에서 **사용자 관리**를 클릭하십시오. 

    사용자가 계정의 구성원이 아닌 경우 [사용자 초대](/docs/iam/iamuserinv.html#iamuserinv)를 참조하십시오. 

4. **Cloud Foundry 액세스**를 선택한 후 조직을 선택하십시오.

    해당 조직에서 사용 가능한 영역의 목록이 나열됩니다.

5. {{site.data.keyword.loganalysisshort}} 서비스를 프로비저닝한 영역을 선택하십시오. 그런 다음 메뉴 조치에서 **영역 역할 편집**을 선택하십시오.

6. *감사자*를 선택하십시오. 

    하나 이상의 영역 역할을 선택할 수 있습니다. *관리자*, *개발자* 및 *감사자* 역할 모두는 사용자가 로그를 보도록 허용합니다.
	
7. **역할 저장**을 클릭하십시오.


자세한 정보는 [권한 부여](/docs/services/CloudLogAnalysis/security/grant_permissions.html#grant_permissions_ui_account)를 참조하십시오.



## 5단계: Kibana 실행
{: #step5}

로그 데이터를 보고 분석하려면 로그 데이터가 사용 가능한 클라우드 공용 지역에서 Kibana에 액세스해야 합니다. 


미국 남부 지역에서 Kibana를 실행하려면 웹 브라우저를 열고 다음 URL을 입력하십시오.

```
https://logging.ng.bluemix.net/ 
```
{: codeblock}


다른 지역에서 Kibana를 실행하는 방법에 대한 자세한 정보는 [웹 브라우저에서 Kibana로 이동](/docs/services/CloudLogAnalysis/kibana/launch.html#launch_Kibana_from_browser)을 참조하십시오.

**참고:** Kibana를 실행할 때 *bearer 토큰이 올바르지 않음*을 나타내는 메시지가 표시되는 경우 영역의 권한을 확인하십시오. 이 메시지는 사용자 ID에 로그를 볼 수 있는 권한이 없음을 표시합니다.
    

## 다음 단계 
{: #next_steps}

로그를 생성합니다. 다음 튜토리얼을 시도하십시오.

* [Kubernetes 클러스터에 배치된 앱에 대한 Kibana에서 로그 분석](/docs/services/CloudLogAnalysis/tutorials/container_logs.html#container_logs){:new_window} 

    이 튜토리얼은 다음 엔드 투 엔드 시나리오 작업을 수행하는 데 필요한 단계를 보여줍니다(클러스터 프로비저닝, {{site.data.keyword.Bluemix_notm}}에서 {{site.data.keyword.loganalysisshort}} 서비스로 로그를 보내도록 클러스터 구성, 클러스터에서 앱 배치, 해당 클러스터에 대한 컨테이너 로그 보기 및 필터링하도록 Kibana를 사용).     
    
* [Kibana에서 Cloud Foundry 앱에 대한 로그 분석](/docs/tutorials/application-log-analysis.html#generate-access-and-analyze-application-logs){:new_window}                                                                                                            

    이 튜토리얼은 Python Cloud Foundry 애플리케이션 배치, 여러 유형의 로그 생성, Kibana를 사용하여 CF 로그 보기, 검색 및 분석과 같은 엔드 투 엔드 시나리오 작업을 수행하는 데 필요한 단계를 보여줍니다.
   








