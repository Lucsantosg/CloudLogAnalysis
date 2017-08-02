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


# Protokolle über die Befehlszeilenschnittstelle analysieren
{: #analyzing_logs_cli}

In {{site.data.keyword.Bluemix}} können Sie Protokolle über die Befehlszeilenschnittstelle (CLI) anzeigen, filtern und analysieren. Verwenden Sie die Befehlszeile, um die Protokolle programmgesteuert zu verwalten. 
{:shortdesc}

Verwenden Sie zur Analyse von Cloud Foundry-Anwendungsprotokollen den folgenden Befehl: `cf logs`.
Weitere Informationen finden Sie unter [CF-App-Protokolle über die Befehlszeilenschnittstelle analysieren](logging_view_cli.html#analyzing_cf_logs_cli).

Verwenden Sie zur Analyse von Docker-Containerprotokollen den folgenden Befehl: `cf ic logs`.
Weitere Informationen finden Sie unter [Docker-Containerprotokolle über die Befehlszeilenschnittstelle analysieren](logging_view_cli.html#analyzing_container_logs_cli). Dieses Feature gilt nur für Container, die in der {{site.data.keyword.Bluemix_notm}}-verwalteten Cloudinfrastruktur bereitgestellt sind.


## CF-App-Protokolle über die Befehlszeilenschnittstelle analysieren
{: #analyzing_cf_logs_cli}

Verwenden Sie den Befehl **cf logs**, um Protokolle über eine Cloud Foundry-App und die Systemkomponenten anzuzeigen, die mit ihr interagieren, wenn Sie die App in {{site.data.keyword.Bluemix_notm}} bereitstellen. Der Befehl **cf logs** zeigt die Protokolldatenströme STDOUT und STDERR einer Cloud Foundry-Anwendung an.

Um die Protokolle anzuzeigen, an denen Sie interessiert sind, oder um Inhalte auszuschließen, die Sie nicht anzeigen möchten, können Sie den Befehl **cf logs** mit Filteroptionen wie **cut** und **grep** in der 'cf'-Befehlszeilenschnittstelle verwenden:

* Informationen zum Anzeigen der Protokolle für eine Cloud Foundry-App finden Sie unter [Protokoll für eine Cloud Foundry-App anzeigen](logging_view_cli.html#full_log_cli).
* Informationen zum Anzeigen der neuesten Protokolldatensätze für eine Cloud Foundry-App finden Sie unter [Neueste Protokolleinträge für eine Cloud Foundry-App anzeigen](logging_view_cli.html#tailing_log_cli).
* Informationen zum Anzeigen der Protokolldatensätze für eine Cloud Foundry-App in einem bestimmten Zeitbereich finden Sie unter [Abschnitt eines Cloud Foundry-Protokolls anzeigen](logging_view_cli.html#partial_log_cli).
* Informationen zum Anzeigen von Einträgen in den Protokollen für eine Cloud Foundry-App, die bestimmte Schlüsselwörter enthalten, finden Sie unter [Protokolleinträge anzeigen, die bestimmte Schlüsselwörter enthalten](logging_view_cli.html#partial_by_keyword_log_cli).


### Protokoll für eine Cloud Foundry-App anzeigen
{: #full_log_cli}

Führen Sie die folgenden Schritte aus, um alle für eine Cloud Foundry-App verfügbaren Protokolle anzuzeigen:

1. Öffnen Sie ein Terminal und melden Sie sich bei {{site.data.keyword.Bluemix}} an.

2. Führen Sie den folgenden Befehl von der Befehlszeile aus, um alle Protokolle anzuzeigen:

   <pre class="pre screen"><code>cf logs <var class="keyword varname">App-Name</var></code></pre>
   
   
### Neueste Protokolleinträge für eine Cloud Foundry-App anzeigen
{: #tailing_log_cli}

Führen Sie die folgenden Schritte aus, um die neuesten für eine Cloud Foundry-App verfügbaren Protokolle anzuzeigen:

1. Öffnen Sie ein Terminal und melden Sie sich bei {{site.data.keyword.Bluemix}} an.

2. Führen Sie den folgenden Befehl von der Befehlszeile aus, um alle Protokolle anzuzeigen:

     <pre class="pre screen"><code>cf logs <var class="keyword varname">App-Name</var> --recent</code></pre>

<div class="note tip"><span class="tiptitle">Tipp:</span> Wenn Sie den Befehl <span class="keyword cmdname">cf push</span> oder <span class="keyword cmdname">cf start</span> in einem Befehlszeilenfenster ausführen, können Sie <samp class="ph codeph">cf logs appname --recent</samp> in einem anderen Befehlszeilenfenster eingeben, um die Protokolle in Echtzeit zu sehen. </div>


### Abschnitt eines Cloud Foundry-Protokolls anzeigen
{: #partial_log_cli}

Führen Sie die folgenden Schritte aus, um einen Teil der für eine Cloud Foundry-App verfügbaren Protokolle in einem bestimmten Zeitbereich anzuzeigen:

1. Öffnen Sie ein Terminal und melden Sie sich bei {{site.data.keyword.Bluemix}} an.

2. Führen Sie den folgenden Befehl von der Befehlszeile aus, um alle Protokolle anzuzeigen:

    <pre class="pre screen"><code>cf logs <var class="keyword varname">App-Name</var> --recent  | cut -c 29-40,46-</code></pre>
    
    Weitere Informationen zur Option **cut** können Sie durch Eingabe von **cut --help** abrufen.


### Protokolleinträge anzeigen, die bestimmte Schlüsselwörter enthalten
{: #partial_by_keyword_log_cli}

Führen Sie die folgenden Schritte aus, um Protokolleinträge anzuzeigen, die bestimmte Schlüsselwörter für eine Cloud Foundry-App enthalten:

1. Öffnen Sie ein Terminal und melden Sie sich bei {{site.data.keyword.Bluemix}} an.

2. Führen Sie den folgenden Befehl von der Befehlszeile aus, um alle Protokolle anzuzeigen:

    <pre class="pre screen"><code>cf logs <var class="keyword varname">App-Name</var> --recent | grep '<var class="keyword varname">Schlüsselwort</var>'</code></pre>
    

Beispiel: Um Protokolleinträge anzuzeigen, die das Schlüsselwort **APP** enthalten, können Sie den folgenden Befehl verwenden:

<pre class="pre screen"><code>cf logs App-Name --recent | grep '\[App'</code></pre>

Weitere Informationen zur Option **grep** können Sie durch Eingabe von **grep --help** abrufen.


### Cloud Foundry-Anwendungsprotokolle
{: #cf_app_logs_cli}

Die folgenden Protokolle sind für eine Cloud Foundry-Anwendung verfügbar, nachdem Sie sie in {{site.data.keyword.Bluemix}} bereitgestellt haben:

**buildpack.log**

Diese Protokolldatei zeichnet differenzierte Informationsereignisse für das Debugging auf. Mithilfe dieses Protokolls können Sie Probleme bei der Buildpack-Ausführung beheben.

Um Daten für die Datei *buildpack.log* zu generieren, müssen Sie das Buildpack-Tracing aktivieren, indem Sie folgenden Befehl eingeben: `cf set-env appname JBP_LOG_LEVEL DEBUG`
   
Um dieses Protokoll anzuzeigen, geben Sie den folgenden Befehl ein: `cf files appname app/.buildpack-diagnostics/buildpack.log`


**staging_task.log**

Diese Protokolldatei zeichnet Nachrichten nach den Hauptschritten der Staging-Task auf. Mithilfe dieses Protokolls können Sie Staging-Probleme beheben.

Um dieses Protokoll anzuzeigen, geben Sie den folgenden Befehl ein: `cf files appname logs/staging_task.log`


**Hinweis:** Informationen zur Aktivierung der Anwendungsprotokollierung finden Sie unter [Laufzeitfehler beheben](/docs/debug/index.html#debugging-runtime-errors).

## Docker-Container-Protokolle über die Befehlszeilenschnittstelle analysieren
{: #analyzing_container_logs_cli}

**Hinweis:** Dieses Feature gilt nur für Container, die in der {{site.data.keyword.Bluemix_notm}}-verwalteten Cloudinfrastruktur bereitgestellt sind.

Verwenden Sie den Befehl `cf ic logs`, um Protokolle von einem Container in {{site.data.keyword.Bluemix_notm}} anzuzeigen. Sie können die Protokolle z. B. verwenden, um zu analysieren, warum ein Container gestoppt wurde, oder um die Ausgabe des Containers zu überprüfen. 

Um die Anwendungsfehler für die in einem Container ausgeführte App über den Befehl `cf ic logs` anzuzeigen, muss die Anwendung ihre Protokolle in die Standardausgabedatenströme STDOUT und STDERR schreiben. Wenn Sie Ihre Anwendung so konzipieren, dass sie in diese Standardausgabedatenströme schreibt, können Sie die Protokolle über die Befehlszeile anzeigen, auch wenn der Container beendet wird oder ausfällt.

Weitere Informationen zu dem Befehl `cf ic logs` finden Sie unter [Befehl 'cf ic logs'](/docs/containers/container_cli_reference_cfic.html#container_cli_reference_cfic__logs).


