---

copyright:
  years: 2017, 2018

lastupdated: "2018-07-25"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# IAM-Token abrufen
{: #auth_iam}

Zum Verwalten der im Konto verfügbaren Protokolle über die {{site.data.keyword.loganalysisshort}}-API müssen Sie ein Authentifizierungstoken verwenden. Sie können die Befehlszeilenschnittstelle von {{{site.data.keyword.Bluemix_notm}} verwenden, um das IAM-Token abzurufen. Das Token hat eine Ablaufzeit. 
{:shortdesc}


## IAM-Token abrufen
{: #iam_token_cli}

Führen Sie die folgenden Schritte über das Terminal aus, um das Berechtigungstoken über die {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle abzurufen:

1. Installieren Sie die {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle.

   Weitere Informationen finden Sie unter [{{site.data.keyword.Bluemix}}-Befehlszeilenschnittstelle herunterladen und installieren](/docs/cli/index.html#overview).
   
   Fahren Sie mit dem nächsten Schritt fort, wenn die Befehlszeilenschnittstelle bereits installiert ist.
    
2. Melden sich bei einer Region in {{site.data.keyword.Bluemix_notm}} an. 

    Weitere Informationen finden Sie unter [Wie melde ich mich bei {{site.data.keyword.Bluemix_notm}} an?](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
	
3. Führen Sie den Befehl `ibmcloud iam oauth-tokens` aus, um das IAM-Token abzurufen.

    ```
	ibmcloud iam oauth-tokens
	```
	{: codeblock}
	
	Die Ausgabe enthält das IAM-Token, das Sie für die Authentifizierung Ihrer Benutzer-ID in diesem Bereich und dieser Organisation benötigen. Sie können das IAM-Token in eine Shellvariable wie `$iam_token` exportieren.



**Hinweis:** Wenn Sie das Token verwenden, entfernen Sie *Bearer* aus dem Wert des Tokens, den Sie in einem API-Aufruf übergeben.

