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


# Plan ändern
{: #change_plan}

Sie können Ihren {{site.data.keyword.loganalysisshort}}-Serviceplan in {{site.data.keyword.Bluemix_notm}} im Service-Dashboard oder durch Ausführen des Befehls `cf update-service` ändern. Sie können Ihren Plan jederzeit aktualisieren oder reduzieren.
{:shortdesc}

## Serviceplan über die Benutzerschnittstelle ändern
{: #change_plan_ui}

Um Ihren Serviceplan in {{site.data.keyword.Bluemix_notm}} im Service-Dashboard zu ändern, führen Sie die folgenden Schritte aus: 

1. Melden Sie sich an {{site.data.keyword.Bluemix_notm}} an und klicken Sie anschließend im {{site.data.keyword.Bluemix_notm}}-Dashboard auf den {{site.data.keyword.loganalysisshort}}-Service.  
    
2. Wählen Sie die Registerkarte **Plan** in der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle aus.

    Daraufhin werden Informationen zu Ihrem aktuellen Plan angezeigt.
	
3. Wählen Sie einen neuen Plan aus, um Ihren Plan zu aktualisieren oder zu reduzieren. 

4. Klicken Sie auf **Speichern**.



## Serviceplan über die Befehlszeilenschnittstelle ändern
{: #change_plan_cli}

Um Ihren Serviceplan in Bluemix über die Befehlszeilenschnittstelle zu ändern, führen Sie die folgenden Schritte aus:

1. Melden Sie sich unter {{site.data.keyword.Bluemix_notm}} an einer Region, einer Organisation und einem Bereich an. 

    Führen Sie zum Beispiel den folgenden Befehl aus, um sich an der Region 'USA (Süden)' anzumelden: 
	
	```
    cf login -a https://api.ng.bluemix.net
    ```
    {: codeblock}
	
2. Führen Sie den Befehl `cf services` aus, um Ihren aktuellen Plan zu prüfen und um den {{site.data.keyword.loganalysisshort}}-Servicenamen aus der Liste der Services anzufordern, die in dem Bereich verfügbar sind. 

    Der Wert für das Feld **name** ist der Name, den Sie verwenden müssen, um den Plan zu ändern. 

    Beispiel:
	
	```
	$ cf services
    Getting services in org MyOrg / space dev as xxx@yyy.com...
    OK
    
    name              service          plan      bound apps   last operation
    Log Analysis-a4   ibmLogAnalysis   premium                create succeeded
    ```
	{: screen}
    
3. Aktualisieren oder reduzieren Sie Ihren Plan. Führen Sie den Befehl `cf update-service` aus.
    
	```
	cf update-service Servicename [-p neuer_Plan]
	```
	{: codeblock}
	
	Dabei gilt: 
	
	* *Servicename* ist der Name Ihres Service. Sie können den Befehl `cf services` ausführen, um den Wert abzurufen.
	* *neuer_Plan* ist der Name des Plans.
	
	In der folgenden Tabelle werden die verschiedenen Pläne und die unterstützten Werte aufgeführt:
	
	<table>
	  <caption>Tabelle 1. Liste der Pläne.</caption>
	  <tr>
	    <th>Plan</th>
	    <th>Name</th>
	  </tr>
	  <tr>
	    <td>Lite</td>
	    <td>lite</td>
	  </tr>
	  <tr>
	    <td>Log Collection</td>
	    <td>premium</td>
	  </tr>
	  <tr>
	    <td>Log Collection mit Suche bis 2GB/Tag</td>
	    <td>premiumsearch2</td>
	  </tr>
	  <tr>
	    <td>Log Collection mit Suche bis 5GB/Tag</td>
	    <td>premiumsearch5</td>
	  </tr>
	  <tr>
	    <td>Log Collection mit Suche bis 10GB/Tag</td>
	    <td>premiumsearch10</td>
	  </tr>
	</table>
	
	Beispiel: Um Ihren Plan auf den *Lite*-Plan zu reduzieren, führen Sie den folgenden Befehl aus:
	
	```
	cf update-service "Log Analysis-a4" -p lite
    Updating service instance Log Analysis-a4 as xxx@yyy.com...
    OK
	```
	{: screen}

4. Überprüfen Sie, ob der neue Plan geändert ist. Führen Sie den Befehl `cf services` aus.

    ```
	cf services
    Getting services in org MyOrg / space dev as xxx@yyy.com...
    OK

    name              service          plan   bound apps   last operation
    Log Analysis-a4   ibmLogAnalysis   lite                update succeeded
	```
	{: screen}






