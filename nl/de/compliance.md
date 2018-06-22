---

copyright:
  years: 2017, 2018

lastupdated: "2018-04-20"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Compliance
{: #compliance}

[{{site.data.keyword.Bluemix}} bietet eine Cloud-Plattform und Services, die den strengen Sicherheitsstandards von IBM entsprechen.](/docs/security/compliance.html#compliance). Der {{site.data.keyword.loganalysislong}}-Service ist ein DevOps-Service, der für {{site.data.keyword.Bluemix_notm}} erstellt wurde.
{:shortdesc}


## Datenschutz-Grundverordnung

Die Datenschutz-Grundverordnung (DSGVO) zielt darauf ab, einen harmonisierten Rahmen für den Datenschutz in der EU zu schaffen und den Bürgern eine bessere Kontrolle über ihre personenbezogenen Daten zu ermöglichen und gleichzeitig strenge Regeln für das Speichern und Verarbeiten von Daten weltweit festzulegen. Die Verordnung enthält auch Vorschriften für den freien Verkehr personenbezogener Daten innerhalb und außerhalb der EU. 

**Haftungsausschluss:** Der {{site.data.keyword.loganalysisshort}}-Service speichert und zeigt Protokolldatensätze von Cloud-Ressourcen, die in Ihrem Konto in {{site.data.keyword.Bluemix_notm}} ausgeführt werden, sowie von Protokollen an, die Sie möglicherweise von außerhalb von {{site.data.keyword.Bluemix_notm}} gesendet haben. Personenbezogene Daten dürfen in keinem der in {{site.data.keyword.loganalysisshort}} gespeicherten Protokolleinträge enthalten sein, da diese Daten anderen Benutzern in Ihrem Unternehmen zugänglich sind und diese Daten anderen Benutzern in Ihrem Unternehmen sowie {{site.data.keyword.IBM_notm}} zur Verfügung stehen, um den Cloud-Service zu unterstützen. 

### Regionen
{: #regions}

Der {{site.data.keyword.loganalysisshort}}-Service soll bis zum Stichtag am 25. Mai 2018 der Einführung der Datenschutz-Grundverordnung in den {{site.data.keyword.Bluemix_notm}} Public-Regionen DSGVO-konform sein, in denen der Service verfügbar ist.


### Datenspeicherung
{: #data_retention}

Der {{site.data.keyword.loganalysisshort}}-Service enthält 2 Datenrepositorys, in denen Ihre Daten gespeichert werden können: 

* Log Search - enthält die Protokolldaten, die für die Analyse über Kibana verfügbar sind. 
* Log Collection - enthält die Protokolldaten für den Langzeitspeicher. 

Je nach {{site.data.keyword.loganalysisshort}}-Serviceplan werden die Daten in Log Search oder in Log Search und Log Collection gespeichert. Der Standard- oder Lite-Plan speichert die Datein in Log Search. Alle anderen Pläne speichern die Daten in Log Search und in Log Collection.

* Protokolle, die in 'Log Search' gespeichert sind, werden nach drei Tagen gelöscht.
* Protokolle, die in 'Log Collection' gespeichert sind, werden so lange aufbewahrt, bis Sie entweder eine Aufbewahrungsrichtlinie konfigurieren oder sie manuell löschen. Die Protokolle werden standardmäßig in 'Log Collection' unbegrenzt aufbewahrt.



### Daten löschen
{: #data_deletion}

Beachten Sie die folgenden Informationen:

* Protokolle, die in 'Log Search' gespeichert sind, werden nach drei Tagen gelöscht.

* Protokolle, die in 'Log Collection' gespeichert sind, werden nach einer bestimmten Anzahl von Tagen gelöscht, wenn Sie eine Aufbewahrungsrichtlinie konfigurieren oder wenn Sie sie manuell löschen.  

    Sie können eine Protokollaufbewahrungsrichtlinie konfigurieren, die die Anzahl Tage definiert, für die Protokolle in 'Log Collection' aufbewahrt werden. Weitere Informationen finden Sie in [Protokollaufbewahrungsrichtlinie mithilfe des {{site.data.keyword.Bluemix_notm}}-Plug-ins anzeigen und konfigurieren](/docs/services/CloudLogAnalysis/how-to/manage-logs/configuring_retention_policy_cloud.html#configuring_retention_policy).

    Sie können die ['Log Collection'-API](https://console.bluemix.net/apidocs/948-ibm-cloud-log-collection-api?&language=node&env_id=ibm%3Ayp%3Aus-south#introduction){: new_window} oder die ['Log Collection'-Befehlszeilenschnittstelle](/docs/services/CloudLogAnalysis/reference/log_analysis_cli_cloud.html#log_analysis_cli){: new_window} verwenden, um Protokolle manuell aus 'Log Collection' zu löschen. 

    Sie können mit der Befehlszeilenschnittstelle die Protokolle aus 'Log Collection' manuell löschen. Weitere Informationen finden Sie [bx logging log-delete mithilfe des {{site.data.keyword.Bluemix_notm}}-Plug-ins](/docs/services/CloudLogAnalysis/how-to/manage-logs/deleting_logs_cloud.html#deleting_logs).


Wenn Sie von einem kostenpflichtigen Plan in den Standard- oder Lite-Plan wechseln, werden in 'Log Collection' die Protokolle in ungefähr einem Tag gelöscht.

Sie können jederzeit ein Support-Ticket öffnen und anfordern, dass alle Ihre Daten aus 'Log Search' und 'Log Collection' gelöscht werden. Informationen zum Öffnen eines IBM Support-Tickets finden Sie in [Kontaktaufnahme mit dem Support](https://www.{DomainName}/docs/support/index.html#contacting-support).



### Weitere Informationen
{: #info}

Weitere Informationen finden Sie in den folgenden Abschnitten:

[{{site.data.keyword.Bluemix_notm}}-Datenschutzkonformität](/docs/security/compliance.html#compliance)

[Datenschutzgrundverordnung - {{site.data.keyword.IBM_notm}} offizielle Seite](https://www.ibm.com/data-responsibility/gdpr/)



