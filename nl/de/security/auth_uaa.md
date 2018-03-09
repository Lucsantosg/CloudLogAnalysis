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


# UAA-Token abrufen
{: #auth_uaa}

Zum Verwalten von Protokollen über die {{site.data.keyword.loganalysisshort}}-API müssen Sie ein Authentifizierungstoken verwenden. Sie können das UAA-Token über die Befehlszeilenschnittstelle von {{site.data.keyword.loganalysisshort}} abrufen. Das Token hat eine Ablaufzeit. 
{:shortdesc}

		
## UAA-Token über die Log Analysis-Befehlszeilenschnittstelle (CF-Plug-in) abrufen
{: #uaa_cli}


Führen Sie die folgenden Schritte aus, um das Berechtigungstoken abzurufen:

1. Installieren Sie die {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle.

   Weitere Informationen finden Sie unter [{{site.data.keyword.Bluemix}}-Befehlszeilenschnittstelle herunterladen und installieren](/docs/cli/reference/bluemix_cli/download_cli.html#download_install).
   
   Fahren Sie mit dem nächsten Schritt fort, wenn die Befehlszeilenschnittstelle bereits installiert ist.
    
2. Melden Sie sich bei einer Region, Organisation und bei einem Bereich in {{site.data.keyword.Bluemix_notm}} an. 

    Weitere Informationen finden Sie unter [Wie melde ich mich bei {{site.data.keyword.Bluemix_notm}} an?](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
	
3. Um das UAA-Token für {{site.data.keyword.Bluemix_notm}} abzurufen, führen Sie den Befehl `bx cf oauth-token` aus.

    ```
	bx cf oauth-token
	```
	{: codeblock}
	
	Die Ausgabe enthält das UAA-Token, das Sie für die Authentifizierung Ihrer Benutzer-ID in diesem Bereich und dieser Organisation benötigen.
	

**Hinweis:** Wenn Sie das Token verwenden, entfernen Sie *Bearer* aus dem Wert des Tokens, den Sie in einem API-Aufruf übergeben.
