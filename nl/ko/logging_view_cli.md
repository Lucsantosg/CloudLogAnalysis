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


# CLI에서 로그 분석
{: #analyzing_logs_cli}

{{site.data.keyword.Bluemix}}에서 명령행 인터페이스를 통해 로그 보기, 필터링 및 분석을 할 수 있습니다. 로그를 프로그래밍 방식으로 관리하려면 명령행을 사용하십시오.
{:shortdesc}

Cloud Foundry(CF) 애플리케이션 로그를 분석하려면 `cf logs` 명령을 사용하십시오.
자세한 정보는 [CLI에서 CF 앱 로그 분석](logging_view_cli.html#analyzing_cf_logs_cli)을 참조하십시오.

Docker 컨테이너 로그를 분석하려면 `cf ic logs` 명령을 사용하십시오.
자세한 정보는 [CLI에서 Docker 컨테이너 로그 분석](logging_view_cli.html#analyzing_container_logs_cli)을 참조하십시오. 이 기능은 {{site.data.keyword.Bluemix_notm}} 관리 클라우드 인프라에서 배치된 컨테이너에만 적용됩니다.


## CLI에서 CF 앱 로그 분석
{: #analyzing_cf_logs_cli}

**cf logs** 명령을 사용하여 Cloud Foundry 앱에서 그리고 {{site.data.keyword.Bluemix_notm}}에서 앱을 배치할 때 상호작용하는 시스템 컴포넌트에서 로그를 표시하십시오. **cf logs** 명령은 Cloud Foundry 애플리케이션의 STDOUT 및 STDERR 로그 스트림을 표시합니다.

관심이 있는 로그를 보거나 보고 싶지 않은 컨텐츠를 제외하기 위해 cf 명령행 인터페이스에서 **cut** 및 **grep**과 같은 필터링 옵션과 함께 **cf logs** 명령을 사용할 수 있습니다.

* Cloud Foundry 앱에 대한 로그를 보려면 [Cloud Foundry 앱의 로그 보기](logging_view_cli.html#full_log_cli)를 참조하십시오.
* Cloud Foundry 앱에 대한 최신 로그 레코드를 보려면 [Cloud Foundry 앱에 대한 최신 로그 항목 보기](logging_view_cli.html#tailing_log_cli)를 참조하십시오.
* 특정 시간 범위에서 Cloud Foundry 앱에 대한 로그 레코드를 보려면 [로그의 섹션 보기](logging_view_cli.html#partial_log_cli)를 참조하십시오.
* 특정 키워드가 포함된 Cloud Foundry 앱에 대한 로그에서 항목을 보려면 [특정 키워드가 포함된 로그 항목 보기](logging_view_cli.html#partial_by_keyword_log_cli)를 참조하십시오.


### Cloud Foundry 앱의 로그 보기
{: #full_log_cli}

Cloud Foundry 앱에 사용 가능한 모든 로그를 보려면 다음 단계를 완료하십시오.

1. 터미널을 열고 {{site.data.keyword.Bluemix}}에 로그인하십시오.

2. 명령행에서 모든 로그를 표시하려면 다음 명령을 실행하십시오.

   <pre class="pre screen"><code>cf logs <var class="keyword varname">appname</var></code></pre>
   
   
### Cloud Foundry 앱에 대한 최신 로그 항목 보기
{: #tailing_log_cli}

Cloud Foundry 앱에 사용 가능한 최신 로그를 보려면 다음 단계를 완료하십시오.

1. 터미널을 열고 {{site.data.keyword.Bluemix}}에 로그인하십시오.

2. 명령행에서 모든 로그를 표시하려면 다음 명령을 실행하십시오.

     <pre class="pre screen"><code>cf logs <var class="keyword varname">appname</var> --recent</code></pre>

<div class="note tip"><span class="tiptitle">팁:</span> 명령행 창에 <span class="keyword cmdname">cf push</span> 또는 <span class="keyword cmdname">cf start</span> 명령을 실행하는 경우, 다른 명령행 창에 <samp class="ph codeph">cf logs appname --recent</samp>를 입력하여
로그를 실시간으로 확인할 수 있습니다. </div>


### Cloud Foundry 로그의 섹션 보기
{: #partial_log_cli}

시간 범위 내에서 Cloud Foundry 앱에 사용 가능한 로그의 일부를 보려면 다음 단계를 완료하십시오.

1. 터미널을 열고 {{site.data.keyword.Bluemix}}에 로그인하십시오.

2. 명령행에서 모든 로그를 표시하려면 다음 명령을 실행하십시오.

    <pre class="pre screen"><code>cf logs <var class="keyword varname">appname</var> --recent  | cut -c 29-40,46-</code></pre>
    
    **cut** 옵션에 대한 자세한 정보를 보려면 **cut --help**를 입력하십시오.


### 특정 키워드가 포함된 로그 항목 보기
{: #partial_by_keyword_log_cli}

Cloud Foundry 앱에 대한 특정 키워드가 포함된 로그 항목을 표시하려면 다음 단계를 완료하십시오.

1. 터미널을 열고 {{site.data.keyword.Bluemix}}에 로그인하십시오.

2. 명령행에서 모든 로그를 표시하려면 다음 명령을 실행하십시오.

    <pre class="pre screen"><code>cf logs <var class="keyword varname">appname</var> --recent | grep '<var class="keyword varname">keyword</var>'</code></pre>
    

예를 들어, 키워드 **APP**이 포함된 로그 항목을 표시하기 위해 다음 명령을 사용할 수 있습니다.

<pre class="pre screen"><code>cf logs appname --recent | grep '\[App'</code></pre>

**grep** 옵션에 대한 자세한 정보를 보려면 **grep --help**를 입력하십시오. 


### Cloud Foundry 애플리케이션 로그
{: #cf_app_logs_cli}

{{site.data.keyword.Bluemix}}에서 Cloud Foundry 애플리케이션을 배치한 후에 다음 로그를 Cloud Foundry 애플리케이션에 대해 사용할 수 있습니다. 

**buildpack.log**

이 로그 파일은 디버깅에 대해 세분화된 정보 이벤트를 기록합니다. 이 로그를 사용하여 빌드팩 실행 문제점을 해결할 수 있습니다. 

*buildpack.log* 파일에 데이터를 생성하려면 `cf set-env appname JBP_LOG_LEVEL DEBUG` 명령을 사용하여 빌드팩 추적을 사용으로 설정해야 합니다. 
   
이 로그를 보려면 `cf files appname app/.buildpack-diagnostics/buildpack.log` 명령을 입력하십시오. 


**staging_task.log**

이 로그 파일은 스테이징 태스크의 주요 단계 후 메시지를 기록합니다. 이 로그를 사용하여 스테이징 문제점을 해결할 수 있습니다. 

이 로그를 보려면 `cf files appname logs/staging_task.log` 명령을 입력하십시오.


**참고:** 애플리케이션 로깅 사용 방법에 대한 정보는 [런타임 오류 디버깅](/docs/debug/index.html#debugging-runtime-errors)을 참조하십시오. 

## CLI에서 Docker 컨테이너 로그 분석
{: #analyzing_container_logs_cli}

**참고:** 이 기능은 {{site.data.keyword.Bluemix_notm}} 관리 클라우드 인프라에서 배치된 컨테이너에만 적용됩니다.

`cf ic logs` 명령을 사용하여 {{site.data.keyword.Bluemix_notm}}의 컨테이너에서 로그를 표시하십시오. 예를 들면, 컨테이너가 중지된 이유를 분석하거나 컨테이너 출력을 검토하기 위해 로그를 사용할 수 있습니다. 

`cf ic logs` 명령을 통해 컨테이너에서 실행되는 앱에 대한 애플리케이션 오류를 보려면 애플리케이션이 표준 출력(STDOUT) 및 표준 오류(STDERR) 출력 스트림에 해당 로그를 작성해야 합니다. 이러한 표준 출력 스트림을 작성하도록 애플리케이션을 설계하는 경우, 컨테이너가 종료되거나 충돌하는 경우에도 명령행을 통해 로그를 볼 수 있습니다.

`cf ic logs` 명령에 대한 자세한 정보는 [cf ic logs 명령](/docs/containers/container_cli_reference_cfic.html#container_cli_reference_cfic__logs)을 참조하십시오.


