---

copyright:
  years: 2017

lastupdated: "2017-05-23"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Kubernetes 클러스터에 배치된 앱에 대한 Kibana에서 로그 분석
{: #kibana_tutorial_1}

Kibana를 시작하십시오. Kubernetes 클러스터에 배치된 앱에 대한 컨테이너 로그를 검색하고 분석하는 방법을 학습합니다.
{:shortdesc}

**참고:** 이 튜토리얼을 완료하려면 다른 단계와 연결된 튜토리얼을 완료하십시오.

## 전제조건
{: #prereq}

1. Kubernetes 클러스터를 작성하고, 클러스터에 앱을 배치하고, Kibana에서 고급 분석을 위해 {{site.data.keyword.Bluemix_notm}}에서 로그를 조회할 수 있는 권한이 있는 Bluemix 계정의 소유자이거나 구성원입니다.

2. Kubernetes 클러스터를 관리할 수 있는 터미널 세션이 있고 명령행에서 앱을 배치합니다. 이 튜토리얼에 소개되는 예는 Ubuntu Linux 시스템에 대해 제공됩니다. 

3. 명령행에서 {{site.data.keyword.containershort}}를 관리하기 위해 Ubuntu 시스템에 [CLI 플러그인을 설치](/docs/containers/cs_cli_install.html#cs_cli_install_steps)합니다. 


## 1단계: Bluemix에서 Kubernetes 시작하고 실행하기
{: #step1}

다음 단계를 완료하십시오.

1. [Kubernetes 클러스터를 작성하십시오](/docs/containers/cs_cluster.html#cs_cluster_ui).

2. 클러스터 컨텍스트를 설정하십시오. 

    예를 들어, Linux 터미널에서 컨텍스트를 설정하려면 [CLI를 구성하여 IBM Bluemix Container Service의 클러스터에 대한 kubectl 명령 실행](/docs/containers/cs_cli_install.html#cs_cli_configure)의 단계를 완료하십시오.

컨텍스트가 설정된 후에 Kubernetes 클러스터를 관리하고, Kubernetes 클러스터에서 애플리케이션을 배치할 수 있습니다.

## 2단계: Kubernetes 클러스터에서 앱 배치
{: #step2}

Kubernetes 클러스터에서 샘플 앱을 배치하고 실행하십시오. [학습 1에 대한 단계를 완료](/docs/containers/cs_tutorials.html#cs_apps_tutorial)하십시오.

앱은 Hello World Node.js 앱입니다.

```
var express = require('express')
var app = express()

app.get('/', function(req, res) {
  res.send('Hello world! Your app is up and running in a cluster!\n')
})
app.listen(8080, function() {
  console.log('Sample app is listening on port 8080.')
})
```
{: screen}

앱이 배치되면 로그 콜렉션이 앱에서 stdout(표준 출력) 및 stderr(표준 오류)에 전송한 로그 항목에 대해 자동으로 사용 가능하게 설정됩니다.  

이 샘플 앱에서는 앱을 브라우저에서 테스트하면 앱이 `Sample app is listening on port 8080.` 메시지를 stdout에 작성합니다.


## 3단계: Kibana에서 로그 데이터 분석
{: #step3}

1. 브라우저에서 Kibana를 실행하십시오. 

    클러스터에 대한 로그 데이터를 분석하려면 클러스터가 작성된 클라우드 공용 지역에서 Kibana에 액세스해야 합니다. 
    
    ```
	https://logging.ng.bluemix.net/
	```
	{: codeblock}

    그 다음에 브라우저에서 URL을 실행하여 Kibana를 여십시오.

2. **검색** 페이지에서 표시된 이벤트를 보십시오.

    샘플 Hello-World 애플리케이션은 한 개의 이벤트를 생성합니다.

    ![Kibana의 검색 페이지](images/sampleapp_2.gif "Kibana의 검색 페이지")

    *사용 가능한 필드* 섹션에서는 페이지에 표시된 표에 나열된 항목을 필터링하거나 새 조회를 정의하는 데 사용할 수 있는 필드의 목록을 볼 수 있습니다.

    새 검색 조회를 정의하는 데 사용할 수 있는 공통 필드가 다음 표에 나열되어 있습니다. 표에는 샘플 앱에서 생성된 이벤트에 해당하는 샘플 값이 포함되어 있습니다.

     <table>
              <caption>표 2. 컨테이너 로그를 위한 공통 필드</caption>
               <tr>
                <th align="center">필드</th>
                <th align="center">설명</th>
                <th align="center">예</th>
              </tr>
              <tr>
                <td>*docker.container_id_str*</td>
                <td> 이 필드의 값은 Kubernetes 클러스터의 포드에서 앱을 실행하는 컨테이너의 GUID에 해당합니다.</td>
                <td></td>
              </tr>
              <tr>
                <td>*ibm-containers.region_str*</td>
                <td>이 필드의 값은 로그 항목이 수집된 {{site.data.keyword.Bluemix_notm}} 지역에 해당합니다.</td>
                <td>us-south</td>
              </tr>
              <tr>
                <td>*kubernetes.container_name_str*</td>
                <td>이 필드의 값은 컨테이너의 이름에 대해 알려줍니다.</td>
                <td>hello-world-deployment</td>
              </tr>
              <tr>
                <td>*kubernetes.host*</td>
                <td>이 필드의 값은 인터넷에서 앱에 액세스하기 위해 사용할 수 있는 공인 IP에 대해 알려줍니다.</td>
                <td>169.47.218.231</td>
              </tr>
              <tr>
                <td>*kubernetes.labels.label_name*</td>
                <td>레이블 필드는 선택 사항입니다. 0 이상의 레이블이 있습니다. 각 레이블은 접두부 `kubernetes.labels.`으로 시작하고 그 뒤에 *label_name*이 옵니다. </td>
                <td>샘플 앱에서는 두 개의 레이블을 볼 수 있습니다. <br>* *kubernetes.labels.pod-template-hash_str* = 3355293961 <br>* *kubernetes.labels.run_str* =	hello-world-deployment  </td>
              </tr>
              <tr>
                <td>*kubernetes.namespace_name_str*</td>
                <td>이 필드의 값은 포드가 실행되는 Kubernetes 네임스페이스에 대해 알려줍니다.</td>
                <td>default</td>
              </tr>
              <tr>
                <td>*kubernetes.pod_id_str*</td>
                <td>이 필드의 값은 컨테이너가 실행되는 포드의 GUID에 해당합니다.</td>
                <td>d695f346-xxxx-xxxx-xxxx-aab0b50f7315</td>
              </tr>
              <tr>
                <td>*kubernetes.pod_name_str*</td>
                <td>이 필드의 값은 포드 이름에 대해 알려줍니다.</td>
                <td>hello-world-deployment-3xxxxxxx1-xxxxx8</td>
              </tr>
              <tr>
                <td>*message*</td>
                <td>애플리케이션에 의해 로그된 전체 메시지입니다.</td>
                <td>샘플 앱은 포트 8080에서 청취 중입니다.</td>
              </tr>
        </table>
    
    
    
3. *검색* 페이지에서 데이터를 필터링하십시오.

    표에서 분석에 사용할 수 있는 모든 항목을 볼 수 있습니다. 나열된 항목은 *검색* 표시줄에 표시된 검색 조회에 해당합니다. 별표(*)를 사용하여 페이지에 구성된 기간 내의 모든 항목을 표시하십시오.

    예를 들어, Kubernetes 네임스페이스로 데이터를 필터링하려면 *검색* 표시줄 조회를 수정하십시오. 사용자 정의 필드 *kubernetes.namespace_name_str*을 기반으로 필터를 추가하십시오.

    1. **사용 가능한 필드** 섹션에서 *kubernetes.namespace_name_str* 필드를 선택하십시오. 필드에 사용 가능한 값의 서브세트가 표시됩니다.

    2. **default** 값을 선택하십시오. 이는 이전 단계에서 샘플 앱을 배치한 네임스페이스입니다.

        값을 선택한 후에 필터가 *검색 표시줄*에 추가되고 방금 선택한 기준과 일치하는 항목만 표에 표시됩니다.

    ![기본 Kubernetes 네임스페이스에 대한 검색용 필터](images/sampleapp_k4_1.gif "기본 Kubernetes 네임스페이스에 대한 검색용 필터")

    필터의 편집 기호를 선택하여 검색하는 네임스페이스 이름을 수정할 수 있습니다.

    ![필터에 사용 가능한 조치](images/sampleapp_k4_1.gif "필터에 사용 가능한 조치")

    다음과 같은 조회가 표시됩니다.

    ```
	{
        "query": {
          "match": {
            "kubernetes.namespace_name_str": {
              "query": "default",
              "type": "phrase"
            }
          }
        }
      }
    ```
	{: screen}
    
    *mynamespace1*과 같은 다른 네임스페이스에서 항목을 검색하려면 조회를 수정하십시오.

    ```
	{
        "query": {
          "match": {
            "kubernetes.namespace_name_str": {
              "query": "mynamespace1",
              "type": "phrase"
            }
          }
        }
      }
    ```
	{: screen}
    
    데이터를 볼 수 없는 경우 시간 필터를 변경해보십시오. 자세한 정보는 [시간 필터 설정](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#set_time_filter)을 참조하십시오.


자세한 정보는 [Kibana에서 로그 필터링](/docs/services/CloudLogAnalysis/kibana/filter_logs.html#filter_logs)을 참조하십시오.

