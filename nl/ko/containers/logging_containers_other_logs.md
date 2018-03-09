---

copyright:
  years: 2017, 2018

lastupdated: "2018-01-10"

---



{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 컨테이너에서 기본이 아닌 로그 데이터 수집(더 이상 사용되지 않음)
{: #logging_containers_other_logs}

{{site.data.keyword.Bluemix_notm}} 관리 인프라에 배치된 컨테이너 내부의 기본이 아닌 로그 위치에서 데이터를 캡처하려면 컨테이너를 작성할 때 환경 변수 **LOG_LOCATIONS**를 설정하십시오.
{:shortdesc}

* 컨테이너를 작성할 때 로그 파일에 대한 경로와 함께 **LOG_LOCATIONS** 환경 변수를 추가하십시오. 
* 쉼표로 구분하여 여러 개의 로그 파일을 추가할 수 있습니다. 

## IBM Cloud 콘솔을 통해 기본이 아닌 로그 데이터 수집
{: #logging_containers_collect_data_ui}

콘솔을 통해 기본이 아닌 데이터를 수집하려면 다음 단계를 완료하십시오.

1. 카탈로그에서 **컨테이너**를 선택하고 이미지를 선택하십시오. 

    표시되는 이미지의 목록에는 {{site.data.keyword.IBM_notm}}에서 제공되는 이미지와 개인용 {{site.data.keyword.Bluemix_notm}} 레지스트리에 저장된 이미지가 포함됩니다. 

2. 컨테이너를 정의하십시오. 유형을 선택하고, 컨테이너의 이름을 입력하고, 그 크기를 선택하고, IP 주소 세부사항 및 포트와 같은 기타 속성을 정의하십시오. 자세한 정보는 [{{site.data.keyword.Bluemix_notm}} UI를 통해 단일 컨테이너 작성 및 배치](/docs/containers/container_single_ui.html#gui)를 참조하십시오. 

3. **고급 옵션** 섹션을 펼쳐서 **새 환경 변수 추가**를 선택하십시오.

4. **LOG_LOCATIONS** 변수를 추가하고 그 값을 분석하려는 로그에 설정하십시오.

    예를 들면, 최신 Liberty 이미지를 기반으로 하는 컨테이너를 추가할 때 *dpkg.log* 로그 파일을 분석하려면 환경 변수를 다음 값으로 설정하십시오. 
    
    <table>
      <caption>표 1. 로그 위치 샘플 값</caption>
      <tbody>
        <tr>
          <th align="center">변수 이름</th>
          <th align="center">값</th>
        </tr>
        <tr>
          <td align="left">LOG_LOCATIONS</td>
          <td align="left">/var/log/dpkg.log</td>
        </tr>
      </tbody>
    </table>

4. **작성**을 클릭하십시오.

컨테이너 대시보드가 열립니다. 컨테이너의 상태가 *실행 중*인지 확인한 후에 **모니터링 및 로그** 탭에서 로그를 확인하십시오.


## CLI를 통해 기본이 아닌 로그 데이터 수집
{: #logging_containers_collect_data_cli}

CLI를 통해 기본이 아닌 로그 데이터를 수집하려면 다음 단계를 완료하십시오.

1. {{site.data.keyword.containershort}} CLI를 사용하도록 터미널을 설정하십시오. 자세한 정보는 [{{site.data.keyword.containershort}} CLI 설정](/docs/containers/container_cli_cfic_install.html)을 참조하십시오. 

2. `bx login` 명령을 사용하여 Cloud Foundry CLI에 로그인하십시오. 프롬프트가 표시되면 {{site.data.keyword.IBM_notm}} ID, 비밀번호, 조직 및 영역을 입력하십시오.  

3. `bx cf ic login` 명령을 사용하여 {{site.data.keyword.containershort}}에 로그인하십시오. 

4. 이미지에서 단일 컨테이너를 작성하십시오. 기본이 아닌 로그 위치를 포함하려면 LOG_LOCATIONS 환경 변수를 포함하십시오.   

    Kibana에서 해당 로그 정보를 볼 수 있도록 사용자 정의 위치를 추가하려면 컨테이너를 작성할 때 **LOG_LOCATIONS** 환경 변수를 추가하십시오. 다음 명령을 입력하십시오.
    
    `docker run -p portNumber -e "LOG_LOCATIONS=log1,log2" --name containerName registry.domain_name/imageName:imageTag`
    
    여기서
    
     <table>
      <caption>표 3. 명령 옵션</caption>
      <tbody>
        <tr>
          <th align="center">옵션</th>
          <th align="center">설명</th>
        </tr>
        <tr>
          <td align="left">-p</td>
          <td align="left"> 인터넷에서 사용자의 앱에 액세스 가능하도록 하려면 공용 포트를 노출해야 합니다. 사용 중인 이미지에 대해 Dockerfile에 지정된 포트를 포함합니다. <br> 사용하려는 IP 프로토콜을 표시하도록 UDP와 TCP 사이에서 선택할 수 있습니다. 프로토콜을 지정하지 않으면 포트가 자동으로 TCP 트래픽에 대해 노출됩니다. <br> 공용 포트를 노출할 때 노출된 포트에서만 공개 데이터를 전송 및 수신할 수 있게 하는 컨테이너에 대한 공용 네트워크 보안 그룹을 작성합니다. 기타 공용 포트는 닫히고 인터넷에서 앱에 액세스하는 데 사용할 수 없습니다. <br> 여러 개의 -p 옵션을 사용하여 포트를 여러 개 포함할 수 있습니다. </td>
        </tr>
        <tr>
          <td align="left">-e</td>
          <td align="left">환경 변수를 설정합니다. <br> 여러 개의 키를 개별적으로 나열할 수 있습니다. 환경 변수 이름 및 값을 모두 따옴표로 묶으십시오. <br> 컨테이너에서 모니터링할 로그 파일을 추가하려면 LOG_LOCATIONS 환경 변수를 로그 파일의 경로와 함께 포함시키십시오. </td>
        </tr>
        <tr>
          <td align="left">--name</td>
          <td align="left">컨테이너의 이름을 정의합니다. </td>
        </tr>
	<tr>
          <td align="left">registry.domain_name</td>
          <td align="left">공용 지역의 레지스트리입니다. 예를 들어, 미국 남부 지역의 경우 기본 도메인 이름은 `ng.bluemix.net`이며 영국의 경우 기본 도메인 이름이 `eu-gb.bluemix.net`입니다. </td>
        </tr>
        <tr>
          <td align="left">imageName</td>
          <td align="left">추가하려는 이미지의 이름입니다.</td>
        </tr>
	<tr>
          <td align="left">imageTag</td>
          <td align="left">추가하려는 이미지의 태그입니다.</td>
        </tr>
      </tbody>
    </table>
    
    예를 들어, 최신 Liberty 이미지를 기반으로 컨테이너를 작성하고 로그 파일 `/var/log/dpkg.log`를 포함하려면 다음 명령을 사용하십시오. 
    
    `docker run -p 9080 -e "LOG_LOCATIONS=/var/log/dpkg.log" --name MyContainer registry.ng.bluemix.net/ibmliberty:latest`
    
    dpkg.log 파일은 컨테이너의 작성 중에 일반적으로 생성되는 표준 Ubuntu 로그 파일이지만, Kibana에 자동으로 푸시되지 않습니다.

컨테이너의 상태를 확인하려면 `docker ps` 명령을 실행하십시오. 상태가 *실행 중*이면 {{site.data.keyword.Bluemix_notm}} 콘솔에서 명령행 또는 Kibana를 통해 로그를 확인하십시오. 



