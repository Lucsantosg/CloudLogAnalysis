---

copyright:
  years: 2017, 2018

lastupdated: "2018-01-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Protokollaufbewahrungsrichtlinie konfigurieren
{: #configuring_retention_policy}

Standardmäßig ist die Aufbewahrungsrichtlinie inaktiviert und die Protokolle werden unbegrenzt lange aufbewahrt. Verwenden Sie den Befehl **bx logging option-update**, um die Aufbewahrungsrichtlinie zu ändern.
{:shortdesc}

Mit dem Befehl **bx logging option-show** wird die Aufbewahrungsrichtlinie angezeigt, die die maximale Anzahl von Tagen definiert, für die die Protokolle in 'Log Collection' aufbewahrt werden. 

Wenn Sie eine Aufbewahrungsrichtlinie festlegen, werden die Protokolle nach Ablauf des Aufbewahrungszeitraums automatisch gelöscht.


## Protokollaufbewahrungsrichtlinie für ein Konto inaktivieren
{: #disable_retention_policy_space}

Wenn Sie die Aufbewahrungsrichtlinie inaktivieren, werden alle Protokolle beibehalten. 

Führen Sie die folgenden Schritte aus, um eine Aufbewahrungsrichtlinie zu inaktivieren:

1. Melden Sie sich bei einer Region, Organisation und bei einem Bereich in {{site.data.keyword.Bluemix_notm}} an. 

    Weitere Informationen finden Sie unter [Wie melde ich mich bei {{site.data.keyword.Bluemix_notm}} an?](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
	
2. Rufen Sie die Konto-ID ab.

    Weitere Informationen finden Sie unter [Wie rufe ich die GUID eines Kontos ab?](/docs/services/CloudLogAnalysis/qa/cli_qa.html#account_guid).
    
3. Legen Sie den Aufbewahrungszeitraum auf **-1** fest, um den Aufbewahrungszeitraum zu inaktivieren. Führen Sie den folgenden Befehl aus:

    ```
    bx logging option-update -r account -i AccountID -e AUFBEWAHRUNGSWERT
	```
    {: codeblock}
	
	Der AUFBEWAHRUNGSWERT ist eine numerische Zahl, die die Anzahl der Tage angibt.
    
**Beispiel**
    
Um beispielsweise den Aufbewahrungszeitraum für ein Konto mit der ID *12345677fgh436902a3* zu inaktivieren, führen Sie den folgenden Befehl aus:

```
bx logging option-update -r account -i 12345677fgh436902a3 -e -1
```
{: codeblock}


## Aufbewahrungsrichtlinie für einen Bereich inaktivieren
{: #disable_retention_policy_space}

Wenn Sie die Aufbewahrungsrichtlinie inaktivieren, werden alle Protokolle beibehalten.  

Führen Sie die folgenden Schritte aus, um eine Aufbewahrungsrichtlinie zu inaktivieren:

1. Melden Sie sich an einer Region, einer Organisation und einem Bereich in {{site.data.keyword.Bluemix_notm}} an. 

    Weitere Informationen finden Sie unter [Wie melde ich mich bei {{site.data.keyword.Bluemix_notm}} an?](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
    
2. Legen Sie den Aufbewahrungszeitraum auf **-1** fest, um den Aufbewahrungszeitraum zu inaktivieren. Führen Sie den folgenden Befehl aus:

    ```
    bx logging option-show -e AUFBEWAHRUNGSWERT
	```
    {: codeblock}
	
	Der AUFBEWAHRUNGSWERT ist eine numerische Zahl, die die Anzahl der Tage angibt.
    
**Beispiel**
    
Um beispielsweise den Aufbewahrungszeitraum für einen Bereich mit der ID *d35da1e3-b345-475f-8502-cfgh436902a3* zu inaktivieren, führen Sie den folgenden Befehl aus:

```
bx logging option-update -e -1
```
{: codeblock}


## Protokollaufbewahrungsrichtlinie für ein Konto überprüfen
{: #check_retention_policy_space}

Um die für ein Konto angegebene Aufbewahrungsrichtlinie abzurufen, führen Sie die folgenden Schritte aus:

1. Melden Sie sich an einer Region, einer Organisation und einem Bereich in {{site.data.keyword.Bluemix_notm}} an. 

    Weitere Informationen finden Sie unter [Wie melde ich mich bei {{site.data.keyword.Bluemix_notm}} an?](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).

2. Rufen Sie die Konto-ID ab.

    Weitere Informationen finden Sie unter [Wie rufe ich die GUID von einem Konto ab?](/docs/services/CloudLogAnalysis/qa/cli_qa.html#account_guid).
    
3. Rufen Sie den Aufbewahrungszeitraum ab. Führen Sie den folgenden Befehl aus:

    ```
    bx logging option-show -r account -i AccountID
    ```
    {: codeblock}

    Die Ausgabe sieht wie folgt aus:

    ```
    bx logging option-show -r account -i kjskdsjfksjdflkjdsfbbd06461b066
    Showing log options of resource: kjskdsjfksjdflkjdsfbbd06461b066 ...

    Resource ID                              Retention   
    a:kjskdsjfksjdflkjdsfbbd06461b066       30   
	```
    {: screen}
	
## Protokollaufbewahrungsrichtlinie für einen Bereich überprüfen
{: #check_retention_policy_space}

Um die für einen Bereich angegebene Aufbewahrungsrichtlinie abzurufen, führen Sie die folgenden Schritte aus:

1. Melden Sie sich an einer Region, einer Organisation und einem Bereich in {{site.data.keyword.Bluemix_notm}} an. 

    Weitere Informationen finden Sie unter [Wie melde ich mich bei {{site.data.keyword.Bluemix_notm}} an?](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
    
2. Rufen Sie den Aufbewahrungszeitraum ab. Führen Sie den folgenden Befehl aus:

    ```
    bx logging option-show
    ```
    {: codeblock}

    Die Ausgabe sieht wie folgt aus:

    ```
    bx logging option-show
    Showing log options of resource: 12345678-1234-2edr-a9de-378620d6fab5 ...

    SpaceId                                Retention   
    12345678-1234-2edr-a9de-378620d6fab5   30   
	```
    {: screen}
    


## Protokollaufbewahrungsrichtlinie auf Kontoebene festlegen
{: #set_retention_policy_space}

Führen Sie die folgenden Schritte aus:

1. Melden Sie sich an einer Region, einer Organisation und einem Bereich in {{site.data.keyword.Bluemix_notm}} an. 

    Weitere Informationen finden Sie unter [Wie melde ich mich bei {{site.data.keyword.Bluemix_notm}} an?](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).

2. Rufen Sie die Konto-ID ab.

    Weitere Informationen finden Sie unter [Wie rufe ich die GUID von einem Konto ab?](/docs/services/CloudLogAnalysis/qa/cli_qa.html#account_guid).
    
3. Legen Sie den Aufbewahrungszeitraum fest. Führen Sie den folgenden Befehl aus:

    ```
    bx logging option-update -r account -i AccountID -e AUFBEWAHRUNGSWERT
    ```
    {: codeblock}
    
    Dabei ist *AUFBEWAHRUNGSWERT* eine ganze Zahl, die die Aufbewahrungsdauer von Protokollen in Tagen angibt. 
    
    
**Beispiel**
    
Beispiel: Wenn alle Protokolltypen nur für 15 Tage in Ihrem Konto verbleiben sollen, führen Sie den folgenden Befehl aus:

```
bx logging option-update -r account -i AccountID -e 15
```
{: codeblock}



## Protokollaufbewahrungsrichtlinie für einen Bereich festlegen
{: #set_retention_policy_account}

Um den Aufbewahrungszeitraum für einen Bereich anzuzeigen, führen Sie die folgenden Schritte aus:

1. Melden Sie sich an einer Region, einer Organisation und einem Bereich in {{site.data.keyword.Bluemix_notm}} an. 

    Weitere Informationen finden Sie unter [Wie melde ich mich bei {{site.data.keyword.Bluemix_notm}} an?](/docs/services/CloudLogAnalysis/qa/cli_qa.html#login).
    
2. Legen Sie den Aufbewahrungszeitraum fest. Führen Sie den folgenden Befehl aus:

    ```
    bx logging option-update -e AUFBEWAHRUNGSWERT
    ```
    {: codeblock}
    
    Dabei ist *AUFBEWAHRUNGSWERT* eine ganze Zahl, die die Aufbewahrungsdauer von Protokollen in Tagen angibt.
    
    
**Beispiel**
    
Beispiel: Wenn Protokolle für ein ganzes Jahr in einem Bereich verbleiben sollen, führen Sie den folgenden Befehl aus:

```
bx logging option-update -e 365
```
{: codeblock}




