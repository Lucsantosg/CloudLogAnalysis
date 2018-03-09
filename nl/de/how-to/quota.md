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


# Suchkontigent und tägliche Nutzung berechnen
{: #quota}

Um das Kontigent und die aktuelle tägliche Nutzung einer Protokolldomäne für den {{site.data.keyword.loganalysisshort}}-Service abzurufen, können Sie einen cURL-Befehl ausführen. 
{:shortdesc}


## Suchkontigent und tägliche Nutzung eines Kontos berechnen
{: #account}

Führen Sie die folgenden Schritte aus:

1. Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an. 

    Weitere Informationen finden Sie unter [Wie melde ich mich bei {{site.data.keyword.Bluemix_notm}} an?](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).

2. Rufen Sie die ID des Kontos ab. Führen Sie den folgenden Befehl aus:

    ```
	bx iam accounts
	```
    {: codeblock}	

	Es wird eine Liste von Konten mit den jeweiligen GUIDs angezeigt.
	
	Exportieren Sie die Konto-ID in eine Shellvariable. Beispiel:
	
	```
	export AccountID="1234567891234567812341234123412"
	```
	{: screen}

3. Rufen Sie das UAA-Token ab. 

    Weitere Informationen finden Sie unter [UAA-Token abrufen](/docs/services/CloudLogAnalysis/security/auth_uaa.html#auth_uaa).

    Exportieren Sie das UAA-Token in eine Shellvariable. 'Bearer' darf nicht mit eingeschlossen werden. Beispiel:
	
	```
	export TOKEN="xxxxxxxxxxxxxxxxxxxxx"
	```
	{: screen}

4. Rufen Sie das Kontigent und die aktuelle Nutzung der Domäne ab. Führen Sie den folgenden Befehl aus:

    ```
    curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: a-${AccountID}" -XGET ENDPUNKT/quota/usage
	```
	{: codeblock}
	
	Dabei ist *ENDPUNKT* für jede Region anders. Eine Liste der Endpunkte pro Region finden Sie unter [Endpunkte protokollieren](/docs/services/CloudLogAnalysis/manage_logs.html#endpoints).
	
	Führen Sie beispielsweise den cURL-Befehl aus, um das Kontigent für das Konto in der Region 'USA (Süden)' abzurufen:
	
	```
    curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: a-${AccountID}" -XGET https://logging.ng.bluemix.net/quota/usage
	```
	{: codeblock}
	
	Das Ergebnis enthält die Informationen zum täglichen Kontigent und der täglichen Nutzung.
	
	```
    curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: a-${AccountID}" -XGET https://logging.ng.bluemix.net/quota/usage
    HTTP/1.1 200 OK
    Server: nginx/1.10.3 (Ubuntu)
    Date: Wed, 29 Nov 2017 13:18:20 GMT
    Content-Type: application/json; charset=utf-8
    Content-Length: 52
    Connection: keep-alive

   {
      "usage": {
        "dailyallotment": 524288000,
        "current": 2115811531
       }
    }
    ```
    {: screen}

	
## Suchkontigent und tägliche Nutzung eines Bereichs berechnen
{: #space}

Führen Sie die folgenden Schritte aus:

1. Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an. 

    Weitere Informationen finden Sie unter [Wie melde ich mich bei {{site.data.keyword.Bluemix_notm}} an?](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).

2. Rufen Sie die ID des Bereichs ab.

    Weitere Informationen finden Sie unter [Wie rufe ich die GUID von einem Bereich ab?](/docs/services/CloudLogAnalysis/qa/cli_qa.html#space_guid).
	
	Exportieren Sie die Bereichs-ID in eine Shellvariable. Beispiel:
	
	```
	export SpaceID="xxxxxxxxxxxxxxxxxxxxx"
	```
	{: screen}

3. Rufen Sie das UAA-Token ab. 

    Weitere Informationen finden Sie unter [UAA-Token abrufen](/docs/services/CloudLogAnalysis/security/auth_uaa.html#auth_uaa).

    Exportieren Sie das UAA-Token in eine Shellvariable. 'Bearer' darf nicht mit eingeschlossen werden. Beispiel:
	
	```
	export TOKEN="xxxxxxxxxxxxxxxxxxxxx"
	```
	{: screen}

4. Rufen Sie das Kontigent und die aktuelle Nutzung der Domäne ab. Führen Sie den folgenden Befehl aus:

    ```
    curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: a-${SpaceID}" -XGET ENDPUNKT/quota/usage
	```
	{: codeblock}
	
	Dabei ist *ENDPUNKT* für jede Region anders. Eine Liste der Endpunkt pro Region finden Sie unter [Endpunkte protokollieren](/docs/services/CloudLogAnalysis/manage_logs.html#endpoints).

    Führen Sie beispielsweise den folgenden cURL-Befehl aus, um das Kontigent und die Nutzung für eine Bereichsdomäne in der Region 'USA (Süden)' abzurufen:
	
    ```
    curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: a-${SpaceID}" -XGET https://logging.ng.bluemix.net/quota/usage
	```
	{: codeblock}
	
	Das Ergebnis enthält die Informationen zum täglichen Kontigent und der täglichen Nutzung.
	
	```
    curl -k -i --header "X-Auth-Token:${TOKEN}" --header "X-Auth-Project-Id: a-${SpaceID}" -XGET https://logging.ng.bluemix.net/quota/usage
    HTTP/1.1 200 OK
    Server: nginx/1.10.3 (Ubuntu)
    Date: Wed, 29 Nov 2017 13:18:20 GMT
    Content-Type: application/json; charset=utf-8
    Content-Length: 52
    Connection: keep-alive

   {
      "usage": {
        "dailyallotment": 524288000,
        "current": 2115811531
       }
    }
    ```
    {: screen}



